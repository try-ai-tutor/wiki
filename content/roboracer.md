---
title: "RoboRacer — F1TENTH autonomous-racing labs"
description: "Auto-graded F1TENTH autonomous-racing labs with per-commit LLM-tutor feedback: ROS 2 nodes graded by tiered unit + closed-loop simulation."
---

**RoboRacer** adapts the open [F1TENTH](https://f1tenth.org) autonomous-racing
curriculum into browser-only, auto-graded labs. Each lab is a ROS 2 node the student
implements; on every commit, GitHub Actions grade it inside a prebuilt container —
cheap structural/unit checks first, then a closed-loop physics simulation — and an
LLM tutor reads the failing tests and the student's code to explain what went wrong.
No local ROS install; a GitHub account and a browser are enough.

## Honest status

The grading pipeline is **proven** — demonstrated on Lab 2 and validated end-to-end on
Lab 4 (Python), which is **live** on the Classroom. The remaining labs exist as built
templates but their graders are not yet validated and deployed; the table says so.

- **✓ live** — validated end-to-end and live on the Classroom (invite below).
- **demo** — shown as a public worked demo (video + write-up), not a self-serve invite.
- **built — deploy pending** — student template exists; grader validation + Classroom
  posting still to come.

## The labs

| Lab | Topic | Variants | Status | Join |
|---|---|---|---|---|
| 2 | Automatic Emergency Braking | Python | demo | [demo + video](/wiki/roboracer-lab02/) |
| 3 | Wall Following (PID) | Python · C++ | built — deploy pending | — |
| 4 | Follow the Gap | Python | **✓ live** | [Accept assignment](https://classroom.github.com/a/mxXkLIMf) |
| 4 | Follow the Gap | C++ | built — deploy pending | — |
| 5 | Scan Matching (PLICP) | C++ | built — deploy pending | — |
| 6 | Pure Pursuit | Python · C++ | built — deploy pending | — |
| 7 | Motion Planning (RRT) | Python · C++ | built — deploy pending | — |
| 8 | Perception / Vision | Python | built — deploy pending | — |
| 9 | Model Predictive Control | Python | built — deploy pending | — |

## How a lab is graded

Grading is **tiered and fail-fast**: cheap structural and unit tests run first, then a
**closed-loop physics simulation** (deterministic, headless — fast enough to run on
every commit), then the AI tutor, with the verdict and feedback in the GitHub Step
Summary next to the green/red badge. The [Lab 2 demo](/wiki/roboracer-lab02/) is a full
worked example. A planned iteration runs the full **f1tenth_gym** *after* the lightweight
simulation passes, to generate the original labs' richer deliverables (full-track laps,
trajectories) without paying that cost on submissions that fail the quick check.

## Credit

Adapted from the open **F1TENTH** autonomous-racing curriculum
([f1tenth.org](https://f1tenth.org)) — the standard Lab 2–9 sequence. We adapt the
topics and grading; original course materials remain the authors'.
