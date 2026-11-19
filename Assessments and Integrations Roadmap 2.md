---
tags:
type:
author:
description:
aliases:
date created: Thursday, November 19th 2026, 11:23:12 am
date modified: Thursday, November 19th 2026, 3:45:06 pm
---

Goal:

> A Carnegie Mellon instructor should be able to turn an existing course into a public CS Learn course in an afternoon: import their materials, review what was imported, publish it on a rolling schedule, and keep improving it from semester to semester. 

### Roadmap

##### Fixing current problems

Grades can currently be forged, and the database is open to the public anon key.

| ID  | Urgent | Item                                                   | Effort |
| --- | ------ | ------------------------------------------------------ | ------ |
| 1   | ✓      | Fix leaks (e.g. anon key via `/simple`)                | 2      |
| 2   | ✓      | Server-owned questions: no answers in browser          | 6      |
| 3   | ✓      | Rate limits on AI-grading and code-execution endpoints | 5      |
| 4   | ✓      | RLS on grade and content tables                        | 8      |
| 5   | ✓      | Reformulate roles: add co-instructor and TA            | 6      |

##### Course management

| ID  | Urgent | Item                                                                                                                                                             | Effort |
| --- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| 6   | ✓      | Stable lesson identity: moving, splitting or merging lessons keeps learners' grades                                                                              | 4      |
| 7   | ✓      | Rolling release for courses (perhaps with percentages) plus drips (e.g. students get accessed to units weekly, by completion, or instructor sets dates for each) | 6      |
| 8   | ✓      | Preview as learner button for instructors                                                                                                                        | 4      |
| 9   | ✓      | Course versions: “updated since you completed” badge, release notes, etc.                                                                                        | 4      |
| 10  |        | Content health checks: broken links, missing alt text and captions, quiz point totals, external activities with no linked tool                                   | 4      |
| 11  |        | Revision history with restore                                                                                                                                    | 6      |

### Quizzes and grading

| ID  | Urgent | Item                                                                                                                                             | Effort |
| --- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------ | ------ |
| 12  | ✓      | **Question versioning and regrade policy.** Important for courses that will change.                                                              | 6      |
| 13  | ✓      | **Ungraded in-video quizzes** like in Coursera. Will involve interacting with the ingest team.                                                   | 6      |
| 15  | ✓      | **Graded quizzes that withhold scores, with cooldowns.** Another mechanism to prevent people brute-forcing.<br><br>Today points are shown always | 4      |
| 16  | ✓      | Attempt history and policies: keep every attempt, practice quizzes allow unlimited attempts with full feedback                                   | 4      |
| 17  | ✓      | A way to ask and handle regrades: we can either do like Gradescope or like Duolingo.                                                             | 4      |
| 18  | ✓      | Grader evaluation harness: something looking like promptfoo course-wide for instructors to manage grading.                                       | 4      |
| 19  | ✓      | Question bank: reuse, tags, random draws<br>Currently we only have question variants                                                             | 6      |
| 20  | ✓      | Symbolic expressions<br><br>Current type merely trims and normalizes characters                                                                  | 4      |
| 21  |        | Partial credit                                                                                                                                   | 4      |
| 22  |        | Rubrics for free-response grading                                                                                                                | 4      |
| 23  |        | Variant review UI                                                                                                                                | 4      |

### Programming assignments

Autolab’s current integration:

- OAuth connection
- Database schemas
- API client with token refresh

It doesn’t list assignments, doesn’t submit anything.

- Still need to understand Autolab more
- Why API and not LTI?
- Will we use CMU or custom instance?

| Option                                           | Description                                                                                                               | Strengths                                                                | Risks                                                                                                      |
| ------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------- |
| **A — CMU Autolab, accounts without Andrew IDs** | Public learners get accounts on CMU's instance; CS Learn enrolls them, links assessments and syncs scores through the API | Instructors' assignments already live there; nothing to operate          | CMU's account process and capacity at public scale; per-term Autolab courses mapped onto one living course |
| **B — CS Learn-operated Autolab**                | Self-hosted Autolab with Google or email sign-up; instructors set up their existing assessments there                     | Full control over accounts, scale and lifecycle; familiar to instructors | Operating Autolab and Tango; sandbox security for public code                                              |
| **C — Tango only**                               | CS Learn runs instructors' Autolab autograders through Tango with its own submission UI                                   | Native experience; reuses autograders                                    | Building the submission and feedback UI; operating Tango                                                   |
| **D — Cogniterra code challenges**               | Autograders deployed as Cogniterra steps; grades over LTI                                                                 | Available today; existing lab deploy pipelines                           | Limited languages and UI; grade passback unproven                                                          |
| **E — In-browser execution**                     | Practice exercises run in the learner's browser (Pyodide)                                                                 | Instant, free, unlimited scale                                           | Tests visible to learners; practice only; mostly Python                                                    |

| ID | Urgent | Item | Effort |
|---|---|---|---|
| 25 | [x] | Harden the existing Autolab client: idempotent migration, single-flight token refresh, OAuth `state`, retry on 401, reconnect banner, multiple Autolab base URLs (works for options A and B) | 4 |
| 26 | [x] | Spike: run 2–3 real pilot autograders through CMU Autolab (A), a self-hosted Autolab (B) and Tango directly (C); compare account handling, latency, cost and operations; recommend one. Includes confirming with `autolab-help@andrew.cmu.edu` how accounts without an Andrew ID are issued at scale | 6 |
| 27 | [x] | Instructor UI: attach an Autolab assessment to a lesson by browsing courses and assessments through the API; points come from Autolab. Autolab courses are per term (`02-180-f26`), so each term's course is mapped onto the living CS Learn course | 5 |
| 28 | [x] | Enrollment and score sync: enroll learners through `course_user_data`; scheduled score sync | 4 |
| 29 | [x] | Learner account linking: connect or provision each learner's Autolab account (OAuth with `user_submit` / `user_scores`, or admin provisioning) | 6 |
| 30 | [x] | Learner experience: deep link or embedded submission (`POST …/submit`), status, per-problem scores and autograder feedback (`…/submissions/:v/feedback`) | 6 |
| 31 | [x] | Cogniterra code challenges: one-click deploy from CS Learn | 5 |
| 32 | [x] | In-browser Python runner for practice code questions | 6 |
| 33 | [x] | Sandbox hardening and quotas for public submissions (no network; CPU, memory and time limits; per-learner quotas; abuse detection); security review | 8 |
| 34 | [ ] | Autograder authoring helpers: test-case editor, debuggable templates | 4 |

### Cogniterra and LTI

| ID  | Urgent | Item                                                                                                                                           | Effort |
| --- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| 35  | [x]    | Cogniterra: prove grade passback end to end; dedicated course and credentials; idempotent, locked sync; Instructor role on instructor launches | 4      |
| 36  | [x]    | Remove the unused LTI 1.3 tool scaffolding and its open tables                                                                                 | 2      |
| 37  | [ ]    | Attach any LTI 1.1/1.3 tool, not only Cogniterra                                                                                               | 4      |
| 38  | [ ]    | Course and lesson community links                                                                                                              | 2      |

### Progress and analytics

| ID  | Urgent | Item                                                                        | Effort |
| --- | ------ | --------------------------------------------------------------------------- | ------ |
| 39  | [x]    | Learner progress page across quizzes, code assignments and Cogniterra       | 4      |
| 40  | [x]    | Instructor analytics: per-unit funnel, drop-off, in-video quiz answer rates | 6      |
| 41  | [x]    | AI and compute cost per course and per learner                              | 2      |
| 42  | [ ]    | Item analysis: difficulty, discrimination, common wrong answers             | 4      |
| 43  | [ ]    | Results before and after a content edit                                     | 4      |
| 44  | [ ]    | Certificates of completion (if credentials are offered)                     | 4      |

---

## 2. Open decisions

1. **Credentials:** whether learners earn certificates, which assessments count, and the integrity checks required.
2. **Release style:** drip for everyone, or unlock per learner.
3. **Edit policy:** whether earlier grades stand when a graded question changes.
4. **Autolab hosting:** CMU's instance (option A) or a CS Learn instance (option B), and who operates it.
5. **AI budget per learner**, and what learners see when it runs out.
6. **Graded-quiz defaults:** cooldown length, attempt limit, and whether withheld answers are ever revealed (for example after the final attempt).