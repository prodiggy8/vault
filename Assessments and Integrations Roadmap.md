---
tags:
type:
author:
description:
aliases:
date created: Thursday, November 19th 2026, 10:46:25 am
date modified: Thursday, November 19th 2026, 10:48:37 am
---
Goal:

> A Carnegie Mellon instructor should be able to turn an existing course into a public CS Learn course in an afternoon: import their materials, review what was imported, publish it on a rolling schedule, and keep improving it from semester to semester. 


## Roadmap

### Epic 0 — Foundation

Grades can currently be forged and the database is open to the public anon key (see `cs-learn-bug.md`). An open sign-up makes this, and AI and compute cost, the first thing to fix.

| ID       | Phase | Item                                                                                                                                                                                                                                                    | Effort |
| -------- | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| 🔒 F0.9  | 1     | **Close known leaks: the `/simple` page exposes the anon key without sign-in; the Cogniterra shared secret is sent to the browser; tool rows are reused by consumer key alone; open redirect in Cogniterra OAuth; remove `scratch-inspect-course.mjs`** | S      |
| 🔒 F0.2  | 1     | Server-owned questions; no answer keys in learner payloads; instructor-only preview grading                                                                                                                                                             | L      |
| 🔒 F0.10 | 1     | Abuse and cost controls: rate limits on AI and code-execution endpoints, daily AI budget per course, email verification before graded work                                                                                                              | M–L    |
| 🔒 F0.3  | 1     | RLS lockdown on grade and content tables; every write goes through server actions                                                                                                                                                                       | XL     |
| F0.4     | 2     | Staff roles: owner, co-instructor, TA/reviewer, content editor; instructors manage their own staff                                                                                                                                                      | L      |


### Epic 1 — Course import

Instructors' materials live in Google Drive, Canvas, GitHub and notebooks. Lectures come from `scs-learn-video-pipeline`, which turns Panopto recordings into privacy-processed public video. A separate pipeline repo also builds courses from instructors' Drives.

| ID      | Phase | Item                                                                                                                                                                                                                                                                                                                           | I1.7Effort |
| ------- | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- |
| I1.1    | 1     | Canvas export (`.imscc`) import: modules → units, pages → lessons, files → attachments and slides, quizzes → questions, assignments → placeholders                                                                                                                                                                             | XL         |
| I1.3    | 1     | QTI quiz import (1.2 and 2.1) with a conversion report                                                                                                                                                                                                                                                                         | L          |
| I1.8    | 1     | Import review screen: source, confidence and needs-review flag for every AI decision; approve, move or merge before publishing                                                                                                                                                                                                 | L          |
| 🔒 I1.9 | 2     | **Re-import in place.** A living course is re-imported every semester, so this must update changed items without wiping instructor edits, never duplicate content, and **keep lesson ids stable** (completions and Cogniterra results are keyed to `lesson_id`). Track source ids and content hashes; send conflicts to review | XL         |
| I1.5    | 2     | Lecture intake from `scs-learn-video-pipeline`: processed videos, captions, chapters and transcripts become lesson video blocks (also feeds Q3.12)                                                                                                                                                                             | M–L        |
| I1.6    | 2     | Zip or folder upload through the same organize pipeline                                                                                                                                                                                                                                                                        | M          |
| I1.10   | 2     | Import report and one-click rollback                                                                                                                                                                                                                                                                                           | M          |
| I1.4    | 3     | Plain-text question format (Markdown/YAML or GIFT) with round-trip export                                                                                                                                                                                                                                                      | M          |
| I1.7    | 3     | GitHub repo and Jupyter notebook import                                                                                                                                                                                                                                                                                        | L          |

### Epic 2 — Authoring and course management

| ID | Phase | Item | Effort |
|---|---|---|---|
| 🔒 A2.8 | 1 | **Stable lesson identity:** moving, splitting or merging lessons keeps learners' completions and grades ("replaced by" mappings) | M |
| A2.2 | 2 | **Rolling release:** instructor-scheduled drip for everyone and/or unlock relative to each learner's join date; optional relative due dates ("suggested: 7 days after unlock") | L |
| A2.3 | 2 | Preview as learner; draft/published diff | M |
| A2.9 | 2 | **Learner changelog:** "updated since you completed it" badges, course release notes, offer to retake a changed quiz | M |
| A2.10 | 2 | Public course page: syllabus, instructor, outline, join button | M |
| A2.6 | 2 | Instructor onboarding: access request, first-course checklist, documentation | M |
| A2.4 | 3 | Content health check: broken links, missing alt text and captions, unreviewed AI content, point totals, unlinked external activities | M |
| A2.5 | 3 | Revision history with restore | L |
| A2.7 | 3 | Course templates | S–M |

### Epic 3 — Assessments

The platform offers three kinds of assessment, each with its own purpose and rules:
- **in-video check-ins:** ungraded, for engagement;
- **practice:** repeatable, with full feedback;
- **graded quizzes:** answers withheld, with cooldowns.

| ID | Phase | Item | Effort |
|---|---|---|---|
| 🔒 Q3.10 | 1 | **Question versioning and regrade policy.** Instructors keep editing a living course, but submissions are re-scored against the current questions today, so a changed answer key silently changes earlier grades. Every edit creates a new version; submissions record the version they answered; earlier grades stand unless the instructor regrades | L |
| Q3.12 | 2 | **In-video quizzes (ungraded).** A new assessment type, separate from lesson quizzes. Questions are pinned to video timestamps; the video pauses, the learner answers or skips, sees the explanation, and continues. Never counts toward grades or completion. Stored separately from quiz submissions; instructors see answer rates per question. About one question per 8–10 minutes of video | L |
| Q3.13 | 2 | **AI-drafted in-video questions:** Claude drafts a question at each chapter boundary from the video pipeline's transcript and chapters; the instructor approves, edits or drops each one | M |
| Q3.14 | 2 | **Graded quizzes that withhold answers, with cooldowns.** Per-quiz settings: after submitting, the learner sees only the score (no correct answers, no per-question correctness); a retake cooldown (for example 24 hours); an optional attempt limit. Enforced on the server: answers never reach the client, and cooldowns and limits are checked on submit. A fresh variant is drawn on each retake | M |
| Q3.1 | 2 | Attempt history and policies: keep every attempt; best/latest/average score; practice quizzes allow unlimited attempts with full feedback | M |
| Q3.5 | 2 | AI grading review queue: filters, overrides, audit, random spot checks | M |
| Q3.7 | 2 | Grader evaluation harness, model selection, prompt-injection hardening | M |
| Q3.2 | 2 | Question bank: reuse, tags, random draws (supports withheld-answer retakes) | L |
| Q3.3 | 3 | Symbolic and unit-aware grading; grader bug fixes | M |
| Q3.4 | 3 | Partial credit for structured question types | M |
| Q3.6 | 3 | Rubrics for free-response grading | M |
| Q3.8 | 3 | Variant review UI; asynchronous regeneration | M |
| Q3.11 | 3 | AI hints on wrong answers (practice and in-video only) | L |

### Epic 4 — Programming assignments

**Autolab is not limited to CMU accounts.** It is open source and actively maintained ([autolab/Autolab](https://github.com/autolab/Autolab)).
- **Accounts:** local email/password accounts with self-registration and email confirmation, and Google sign-in. CMU SSO (Shibboleth) is optional and set per instance. CMU's instance (`autolab.andrew.cmu.edu`) sends its sign-in page to CMU SSO; accounts without an Andrew ID are created by its administrators.
- **REST API v1** ([routes](https://github.com/autolab/Autolab/blob/master/config/routes.rb)):
  - enroll, update and drop users by email (`course_user_data`, `instructor_all`; the account must already exist);
  - list assessments, handouts and writeups;
  - submit on a learner's behalf (`POST …/submit`, `user_submit`, using that learner's own token);
  - read submissions with autograder feedback, and read scores.
- **OAuth:** authorization code plus device flow.
- **LTI:** roster sync only, with no grade service, so scores reach CS Learn through the REST API.
- **Grading:** Autolab grades with **Tango**, a separate REST service that runs autograders in Docker containers.

**Backend options**

| Option | Description | Strengths | Risks |
|---|---|---|---|
| **4A — CMU Autolab, accounts without Andrew IDs** | Public learners get accounts on CMU's instance; CS Learn enrolls them, links assessments and syncs scores through the API | Instructors' assignments already live there; nothing to operate | CMU's account process and capacity at public scale; per-term Autolab courses mapped onto one living course |
| **4B — CS Learn-operated Autolab** | Self-hosted Autolab with Google or email sign-up; instructors import existing assessments | Full control over accounts, scale and lifecycle; familiar to instructors | Operating Autolab and Tango; sandbox security for public code |
| **4C — Tango only** | CS Learn runs instructors' Autolab autograders through Tango with its own submission UI | Native experience; reuses autograders | Building submission and feedback UI; operating Tango |
| **4D — Cogniterra code challenges** | Autograders deployed as Cogniterra steps; grades over LTI | Available today; existing lab deploy pipelines | Limited languages and UI; grade passback unproven |
| **4E — In-browser execution** | Practice exercises run in the learner's browser (Pyodide) | Instant, free, unlimited scale | Tests visible to learners; practice only; mostly Python |

| ID | Phase | Item | Effort |
|---|---|---|---|
| P4.1 | 1 | Harden the existing Autolab client: idempotent migration, single-flight token refresh, OAuth `state`, retry on 401, reconnect banner, multiple Autolab base URLs (works for 4A and 4B) | M |
| P4.8 | 1 | Spike: run 2–3 real pilot autograders through CMU Autolab (4A), a self-hosted Autolab (4B) and Tango directly (4C); compare account handling, latency, cost and operations; recommend one. Includes confirming with `autolab-help@andrew.cmu.edu` how accounts without an Andrew ID are issued at scale | L |
| P4.3 | 1 | Instructor UI: attach an Autolab assessment to a lesson by browsing courses and assessments through the API; points come from Autolab. Autolab courses are per term (`02-180-f26`), so each term's course is mapped onto the living CS Learn course | M–L |
| P4.5 | 2 | Enrollment and score sync: enroll learners through `course_user_data`; scheduled score sync as a background job | M |
| P4.2 | 2 | Learner account linking: connect or provision each learner's Autolab account (OAuth with `user_submit` / `user_scores`, or admin provisioning) | L |
| P4.4 | 2 | Learner experience: deep link or embedded submission (`POST …/submit`), status, per-problem scores and autograder feedback (`…/submissions/:v/feedback`) | L |
| P4.9 | 2 | Cogniterra code challenges: one-click deploy from CS Learn | M–L |
| P4.10 | 2 | In-browser Python runner for practice code questions | L |
| P4.7 | 2 | Sandbox hardening and quotas for public submissions (no network; CPU, memory and time limits; per-learner quotas; abuse detection); security review | XL |
| P4.6 | 3 | Autograder import: assessment, handout and autograder from an instructor's Autolab course into the chosen backend | L |
| P4.11 | 3 | Autograder authoring helpers: test-case editor, debuggable templates | M |

### Epic 5 — Integrations

| ID | Phase | Item | Effort |
|---|---|---|---|
| 🔒 C5.1 | 1 | Cogniterra: prove grade passback end to end; dedicated course and credentials; idempotent, locked sync; Instructor role on instructor launches | M |
| C5.9 | 1 | Remove the unused LTI 1.3 tool scaffolding and its open tables | S |
| C5.6 | 3 | Attach any LTI 1.1/1.3 tool, not only Cogniterra | M |
| C5.8 | 3 | Course and lesson community links | S |

### Epic 6 — Progress and analytics

| ID | Phase | Item | Effort |
|---|---|---|---|
| G6.1 | 2 | Learner progress page across quizzes, code assignments and Cogniterra | M |
| G6.2 | 2 | Instructor analytics: per-unit funnel, drop-off, cohorts by join month, in-video quiz answer rates | L |
| G6.5 | 2 | AI and compute cost per course and per learner | S |
| G6.3 | 3 | Item analysis: difficulty, discrimination, common wrong answers | M |
| G6.4 | 3 | Results before and after a content edit | M |
| G6.7 | 3 | Certificates of completion (if credentials are offered) | M |

---

## 2. Open decisions

1. **Credentials:** whether learners earn certificates, which assessments count, and the integrity checks required.
2. **Release style:** drip for everyone, or unlock per learner.
3. **Edit policy:** whether earlier grades stand when a graded question changes.
4. **Autolab hosting:** CMU's instance (4A) or a CS Learn instance (4B), and who operates it.
5. **Import ownership:** the platform or the course-building pipeline (I1.0).
6. **AI budget per learner**, and what learners see when it runs out.
7. **Graded-quiz defaults:** cooldown length, attempt limit, and whether withheld answers are ever revealed (for example after the final attempt).