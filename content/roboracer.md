---
title: "RoboRacer — autonomous-racing labs"
description: "Auto-graded autonomous-racing labs with per-commit LLM-tutor feedback: ROS 2 nodes graded by tiered unit + closed-loop simulation."
---

[한국어](./roboracer.ko/)

**RoboRacer** adapts the open [RoboRacer](https://roboracer.ai/learn) autonomous-racing
curriculum into browser-only, auto-graded labs. Each lab is a ROS 2 node the student
implements; on every commit, GitHub Actions grade it inside a prebuilt container —
cheap structural/unit checks first, then a closed-loop physics simulation — and an
LLM tutor reads the failing tests and the student's code to explain what went wrong.
No local ROS install; a GitHub account and a browser are enough.

## Honest status

The grading pipeline is **proven** — demonstrated on Lab 2 and validated end-to-end on
Lab 4 Python and Lab 6 Python, which are **live** on the Classroom. The remaining labs
exist as built templates but their graders are not all yet validated and deployed; the
table says so.

- **✓ live** — validated end-to-end and live on the Classroom (invite below).
- **demo** — shown as a public worked demo (video + write-up), not a self-serve invite.
- **grader fixes in flight** — student template exists; grader regression being worked
  on a side branch — invite withheld so a student push isn't met with a broken autograder.
- **built — deploy pending** — student template exists; grader validation + Classroom
  posting still to come.
- **planned** — re-deploy or first deploy scheduled, but neither the template nor the
  Classroom assignment is in the new roboracer Classroom yet.

## The labs

| Lab | Topic | Python | C++ |
|---|---|---|---|
| 2 | Automatic Emergency Braking | demo + re-deploy planned · [demo + video](/wiki/roboracer-lab02/) | — |
| 3 | Wall Following (PID) | built ✓ — classroom pending | built ✓ — classroom pending |
| 4 | Follow the Gap | **✓ live** · [Accept assignment](https://classroom.github.com/a/mxXkLIMf) | **✓ live** · [Accept assignment](https://classroom.github.com/a/G_IF3gLI) |
| 5 | Scan Matching (PLICP) | — | **✓ live** · [Accept assignment](https://classroom.github.com/a/L-DehS19) |
| 6 | Pure Pursuit | **✓ live** · [Accept assignment](https://classroom.github.com/a/ehA0rYJt) | **✓ live** · [Accept assignment](https://classroom.github.com/a/Fo9vQlQC) |
| 7 | Motion Planning (RRT) | built — deploy pending | built — deploy pending |
| 8 | Perception / Vision | built — deploy pending | — |
| 9 | Model Predictive Control | built — deploy pending | — |

Lab 1 (Intro to ROS 2) is intentionally outside the auto-graded track — its deliverables
are pub/sub plumbing and `colcon` workspace setup, which the upstream RoboRacer course
already treats as the ungraded warm-up before Lab 2 onward.

## How a lab is graded

Grading is **tiered and fail-fast**: cheap structural and unit tests run first, then a
**closed-loop physics simulation** (deterministic, headless — fast enough to run on
every commit), then the AI tutor, with the verdict and feedback in the GitHub Step
Summary next to the green/red badge. The [Lab 2 demo](/wiki/roboracer-lab02/) is a full
worked example. A planned iteration runs the full **f1tenth_gym** *after* the lightweight
simulation passes, to generate the original labs' richer deliverables (full-track laps,
trajectories) without paying that cost on submissions that fail the quick check.

## Credit

Adapted from the open **RoboRacer** autonomous-racing curriculum
([roboracer.ai/learn](https://roboracer.ai/learn)) — Lab 02 through 09. We adapt the
topics and grading; original course materials remain the authors'.
