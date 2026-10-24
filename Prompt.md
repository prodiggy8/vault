**Context**

- Founding engineer at Latent, building Latent Monitor.
- Tray app that collects modular, anonymous, aggregated activity signals from employees.
	- SOPs and AI training data
- We were piloting at a Brazilian credit fund on about 50 machines.

Server -> Tauri, webview
Watchers -> mostly Python


- Since we didn’t have direct access to the machines at this client, since funds are heavily regulated, I had to build an update service.

- On Windows it worked like this:
	- Read a signed manifest with beta and stable channels and rollout percentages
	- App checks for this manifest on startup, apply rollout percentage
	- Download the Inno Setup installer and check its hash
	- Stop the background processes
	- Launch the installer silently and exit
	- The installer swaps the files and restarts the app.

Every step passed unit tests and my manual testing in a Windows VM, so we enabled it for a first batch of 5 machines.

**What happened and how I found out**

- A few days later I shipped a new module that was supposed to get telemetry from Microsoft Office
- Update was successful
- Only 2 of the 5 machines had them.
- Our installations table showed them still on the old version.
	- App crashed altogether!

**Stopping the bleeding**

I reverted the version in the manifest and told the team about a gap of a few hours in the data.

- The revert protected the machines that hadn’t updated yet, but it couldn’t help the 3 that broke.

**Root cause**

- When I re-ran the update in my VM, it failed this time.
- With extra logging and some digging into how Inno Setup behaves, I found two bugs.

First, a race on a named mutex. The installer decides whether the app is running by checking for a mutex, and the tray held it until the moment it exited. If the installer’s check landed before the tray finished closing, it concluded the app was still running. Normally it would ask the user to close the app, but I had made the install fully silent, so it just aborted. The tray was gone, the installer was gone, and nothing was running.

Second, on machines where the update succeeded, the restarted tray showed the old UI. The UI is a WebView2, which runs as a child process, and that child survived the update.

**The fix**

The tray now releases the mutex _before_ launching the installer. The tray and its child processes now live in a Windows Job Object, so killing the tray kills everything under it. That same night, I got on a call with the client’s IT contact and we patched the 3 machines together. Having a good relationship with them made that possible.

**Why it got past me**

- There was no automated end-to-end testing at all, only my manual VM runs.
- I hadn’t enabled installer logging, so the step that failed left no trace.
- No alerting: nothing would have told us if I hadn’t happened to look.
- My recovery mechanism, a flag file for interrupted updates, depended on the tray starting again. That was exactly the thing that had failed.

**What I changed, or would change**

- End-to-end tests on every PR.
- Telemetry across the whole update path, including the installer.
- Alerts on how versions are spread across the fleet and on when each machine last sent signals.
- A canary machine at the client, which was their IT admin’s.
- Longer term, a separate update service. That’s the pattern many Windows apps use, because it can recover the app even when the app itself is dead.

The lesson I took away: recovery can’t depend on the component that failed.

**Transition to the demo**