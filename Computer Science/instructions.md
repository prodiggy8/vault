# DevSecOps Project

Components:
  - spring-petclinic (application)
  - Jenkings (CI)
  - SonarQube (static analysis)
  - Prometheus + Grafana (monitoring)
  - ZAP (security)
  - Ansible + VM/Vagrant (deployment) 
  - Docker (orchestration)

The production VM is Ubuntu 24 running on KVM/libvirt (the OS used to do this assignment has some issues with VirtualBox).

## Prerequisites

### Install Vagrant

```
wget -O https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install -y vagrant
```

### Install KVM/libvirt

```
sudo apt update && sudo apt install -y qemu-kvm libvirt-daemon-system libvirt-clients \
  libvirt-dev ebtables dnsmasq-base bridge-utils build-essential pkg-config
sudo usermod -aG libvirt,kvm $USER
vagrant plugin install vagrant-libvirt
```

## Fork and clone the repository

```
git clone https://github.com/prodiggy8/spring-petclinic
```

## Provision the production VM

The Vagrantfile (`devsecops/Vagrantfile`) defines an Ubuntu 24.04 image on

```
cd devsecops
sg libvirt -c "vagrant up --provider=libvirt"
vagrant status
```

### Routed-network

libvirt's network blocks traffic coming from the Docker subnet, `libvirt__forward_mode: "route"`
in the Vagrantfile fixes that but you need to recreate the network:

```
sg libvirt -c "vagrant halt"
sg libvirt -c "virsh -c qemu:///system net-destroy devsecops0"
sg libvirt -c "virsh -c qemu:///system net-undefine devsecops0"
sg libvirt -c "vagrant up"
docker run --rm busybox ping -c1 192.168.56.10
```

## Docker stack

All services are defined in `devsecops/docker-compose.yml` on the `devsecops-net`
bridge network. Jenkins is a custom image (`devsecops/jenkins/Dockerfile`) that
adds the Docker CLI, Ansible, blueocean, sonar, prometheus, etc. 

```
cd devsecops
docker compose build jenkins
docker compose up -d jenkins sonar-db prometheus grafana zap registry
docker compose up -d sonarqube
```

Endpoints:
Jenkins `:8080`
SonarQube `:9000`
Prometheus `:9090`
Grafana `:3000`
Registry `:5000`

## Configure Jenkins

1. Open `http://localhost:8080`. Run:
   ```
   docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
   ```
2. On Customize Jenkins, choose `Select plugins to install → None` (plugins
   are already there), then create your admin user.

## Configure SonarQube

1. Wait for SonarQube: 
   ```
   curl -s http://localhost:9000/api/system/status   # needs to say UP
   ```
2. Create the project and an analysis token, change the admin password as well.
   ```
   curl -s -u admin:admin -X POST "http://localhost:9000/api/projects/create?project=petclinic&name=petclinic"
   curl -s -u admin:admin -X POST "http://localhost:9000/api/user_tokens/generate?name=jenkins-petclinic"
   ```
3. In Jenkins: `Manage Jenkins → Credentials → System → Global → Add Credentials`
   - Kind: Secret text
   - Secret: the `squ_...` token
   - ID: `sonar-token`

The pipeline passes `-Dsonar.host.url=http://sonarqube:9000 -Dsonar.token=$SONAR_TOKEN`
so no secret is committed to the repo.

## Prometheus + Grafana 

Both are provisioned from files:
- `devsecops/prometheus/prometheus.yml` - job `jenkins` at `/prometheus`
- `devsecops/grafana/provisioning/datasources/datasource.yml` - Prometheus datasource
- `devsecops/grafana/provisioning/dashboards/json/jenkins.json` - Jenkins dashboard

## Add the Ansible SSH credential

The Ansible deploy stage needs the VM's SSH. Add in `Manage Jenkins → Credentials → Add Credentials`.
- Kind: SSH Username with private key
- ID: `petclinic-vm-ssh`, Username: `vagrant`
- Private key: paste the contents of
  `devsecops/.vagrant/machines/default/libvirt/private_key`

## Pipeline files

These are committed to the fork:

- `Dockerfile` - JRE image
- `ansible/inventory.ini` - targets `petclinic-vm` at `192.168.56.10`, user `vagrant`
- `ansible/deploy.yml` - installs Docker on the VM, pulls image, runs container
- `Jenkinsfile` - `pollSCM('* * * * *')` and stages for build and test, sonar analysis, docker build and push, ansible deploy, zap scan and report.

### ZAP scan

```
sh 'docker run --rm --user 0 --network devsecops-net -v zap_wrk:/zap/wrk zaproxy/zap-stable zap-baseline.py -t http://192.168.56.10:8080 -r zap-report.html'
sh 'docker run --rm -v zap_wrk:/zap/wrk busybox cat /zap/wrk/zap-report.html > zap-report.html'
```

### Other details: 

These were changes we have to make in the petclinic repo:
- nohttp policy: scans the whole repo and rejects `http://` URLs. Need to manually ignore the
  infra files and generated ZAP report from that check
- Docker-compose integration tests can't run in this CI and are
  out of scope, need to delete them 

Commit and push all pipeline files:
```
git add .
git commit -m "any message"
git push origin main
```

## Create and run the Jenkins pipeline job

1. Jenkins dashboard → New Item → name `petclinic` → Pipeline → ok.
2.
   - Definition: Pipeline script from SCM
   - SCM: Git
   - Repository URL: `https://github.com/prodiggy8/spring-petclinic.git`
   - Branch Specifier: `*/main`
   - Script Path: `Jenkinsfile`
3. Save, then Build Now.

## Verify the deployment

Open in browser: http://192.168.56.10:8080

## Demonstrate the SCM trigger 

Change something in the repo (maybe a title?) and then push the changes.
The pipeline in Jenkins should immediately be triggered.
