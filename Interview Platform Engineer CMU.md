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

Every step worked in unit tests and in my test Windows VM, so it was deployed a squad of 5 credit analysts.

A few days later I shipped a new Microsoft Office watcher, when inspecting the data warehouse for records, only two of the machines had Office signals.

- Can’t access their machines, so looked network logs
	- App stopped sending ALL signals when I shipped the new feature
	- Installations table: the two were still in the old version.

Immediate Remediation:
- Revert new version in manifest
- Communicate with team: gap of a few hours in data

Diagnostic:
- Testing in VM: unlike last time, the update didn’t work this time.
- Extra logs included & research about Inno Setup behavior (lots of help of AI)

Causes:
1. Race on the mutex

The installer decides whether the app is running by checking a named mutex. The tray holds that mutex for its whole life, and released it only when it exited.
- The installer could start up before the tray had time to close.
- If the installer's check landed in that window, it saw the mutex and decided the app was still running.
- Since I decided for a completely silent installation, the "please close the app" prompt is suppressed and the installation was aborted.
- Since the installer holds no logs and it’s random behavior, it was quite hard to diagnose this.

2. Extra bug: restarted trays on successful updates contained old UI
- That’s because UI is a webview, which starts msedgewebview2.exe child process, which wasn’t killed before the update.

Why this got past me:
- Lack of automated, reproducible E2E tests in CI pipeline
- Poor logging: the installer didn’t log anything at all! which cost me hours of debugging.
- no safety net! 
	- I had a flag update-in-progress.json meant to recover from a crash, but it depended on the tray starting again!

After fixes:
- Called IT contact, we patched the affected applications the same night together
- Building good relationships with customers helped a lot here

  Why it hurt so much. The only fix was a human on the machine, and the only humans were the client's IT staff.

  Prevention.
  - E2E tests on every PR.
  - Telemetry in the full process: including the installer
  - Make the update service a separate service/daemon (planned but not realized; many Windows apps do this)
  - Canary machine in BFC (the IT admin!)
  - Alerts on failed updates with GCP Cloud monitoring.

