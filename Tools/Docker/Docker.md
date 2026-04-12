Containerization involves "encapsulating" software and all its dependencies so it can run uniformly and consistently on any infrastructure.

**Container:** abstraction at the application layer that packages code and dependencies together.

Hardware virtualization works with a hypervisor providing VMs with a virtual representation of the host's hardware. Different guest operating systems can be launched.

Operating-system-level virtualization is a method where the kernel allows the existence of multiple user-space instances. The virtualized environments are called *containers*. 

Docker on Windows machines will use the WSL2 kernel. On macOS, the back-end is a VM running on HyperKit.

*How it works?*
With a couple of kernel-level technologies.

- Control groups: software that provides resource metering and limiting for processes.
- Namespaces: software that wraps resources in abstraction that makes it appear to the processes that they have their own isolated instance of that resource.

**Image:** files that act as the template for creating containers; a frozen, read-only copy of a container. They are of a standard format across runtimes.

**Registry:** centralized place where images can be uploaded and downloaded, e.g. Docker Hub and Quay.

##### Docker Architecture

A client-service architecture. The Docker client talks to the Docker daemon, which builds runs and distributes containers.

![[Pasted image 20260307205525.png]]

Once an image has been fetched from the registry, it will be kept in a local cache.