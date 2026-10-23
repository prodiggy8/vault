---
tags:
type:
author:
description:
aliases:
date created: Thursday, October 22nd 2026, 11:12:43 pm
date modified: Thursday, October 22nd 2026, 11:12:48 pm
---
1. Context & Ownership
2. Detection (how I found it and how long it took)
3. Stop the bleeding first (rollback, feature flag, pausing the pipeline, telling the people affected). Size the blast radius — what was hurt, since when, how badly.
4. Diagnosis by evidence. Formed hypothesis and ruled them out with data such as logs, metrics, queries, or a reproduction.
5. The real root cause
6. Fix with trade offs — a quick fix vs. a durable one
7. Prevention at the class level: made kind of bug detectable or impossible, with new alerts invariants, tests, or guardrails.
8. Reflection


- Specific numbers
- I wrote the bug is a green flag.
- Business impact

##### Background
- Engineer at Latent from March until August
- Working on Latent Monitor — it’s a multi-platform tray app that consumes several signals from employees’ machines such as mouse movement, clicks, keyboard behavior, apps used, network activity, etc. **Anonymous and aggregated.**
- Piloting with BFC Capital, a credit-fund from Brazil at about 50 machines.

##### Architecture
- The idea was to be a tray app running at all times, so it needed to be lightweight — we built most things from scratch instead of relying into frameworks like Electron. That includes auto-update services.
- Built the auto-updater. Following steps for the Windows version:
	- Beta and stable channels with rollout percentages
	- App reads signed manifest for latest version
	- Downloads Inno Setup installer and checks hash
	- Stops background processes and starts the installer **silently** then exits.
	- Installer swaps files and restarts the tray.

Every step worked in unit tests, in my test Windows VM, so I deployed into a test group of 5 credit analysts. It worked for the most part!

A few days later when shipping another feature (a new watcher for Microsoft Office apps), when inspecting the data warehouse for records of the new watcher, two of the machines simply stopped sending signals altogether, where the other 3 kept sending them normally.

They logged out? They turned off the watcher? The update failed?

- Open logs -> last line says “installer launched, exiting tray”
- However in the installation table, those users were still in the older version.

Diagnostic:
- Extra logs
- Testing in a VM



Latent Watchdog runs on the machines of [5–6] analysts at a credit company, a regulated client with its own IT team. I built the release and auto-update pipeline: a signed manifest in GCS, update channels, a staged
  rollout, and a silent installer handoff.

  The incident. On [date, ~May 6–7] I pushed an update. [? What went wrong for them: the tray disappeared, no data was collected, or the old UI kept running?] Because the client had locked-down machines and I had no remote
  access, [? when and how you found out: missing data in BigQuery, a user complaint, or the client telling you?]. In the middle of the night I called their IT manager. He SSHed into the machines and [? what he ran: started the
  tray by hand, killed the stuck installer, ran it again, or removed the update marker?].

  Containment. [? Did you pause the rollout or pull the manifest from GCS first? Did you tell the client a plan before fixing?]

  Diagnosis. It was three bugs with one symptom, "the tray never came back":
  1. A race on the mutex: the installer saw the tray still running and silently aborted. Fixed by releasing the mutex before starting the installer (0af381c).
  2. A silently skipped relaunch: the runasoriginaluser flag. Fixed in ba52b9c.
  3. Webview child processes held the UI files open, so the new exe ran with the old UI. Fixed by killing them and wiping the UI folder before install (ba52b9c).

  Why it hurt so much. The failure was silent, and the one thing that could report it (the tray's recovery marker) only runs when the tray starts. The only fix was a human on the machine, and the only humans were the client's IT
  staff. [? Is this when the SSH approach became the recovery runbook?]

  Prevention.
  - /update-event lifecycle telemetry.
  - Stable releases go to 25% first, behind a typed confirmation, and can't ship from a dirty working tree.
  - Crash-recovery marker with the installer's process ID.
  - Autostart at login as a fallback.
  - [? Anything agreed with the client: a maintenance window, a remote-access runbook, a pilot machine that updates first?]

  Reflection.
  - I spent a client's goodwill to learn that "install succeeded" isn't "app running".
  - The rollout ramp should be gated on a positive signal from updated machines. Today it's a manual decision.
  - The installer itself still writes no log.

  ---

  What I need from you

  1. Detection: how did you find out, and how long after the release?
  2. Impact: how many machines, and for how long? Was data lost or just delayed? (The watchers buffer locally, so maybe nothing was lost.)
  3. The call: what time was it, and did you have a runbook? What did he run over SSH, and on how many machines?
  4. Which bug bit in production: the mutex race, the skipped relaunch, or both?
  5. After: did you add anything because of this night specifically, such as the 25% stable rollout or the telemetry, or did those already exist?

  Answer these and I'll turn it into the final 5-minute version. One thing to double-check: SSH into Windows analyst machines is a little unusual. An interviewer may ask about it, so confirm it was SSH and not RDP or a
  remote-management tool like Intune.