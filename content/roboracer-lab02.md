---
title: "RoboRacer Lab 02 — AEB safety demo"
description: "Closed-loop physics simulation + LLM tutor for F1Tenth autonomous emergency braking code. Three student states, three voices converging."
date: 2026-05-16
---

## What this is

A live demo of the LLM Coding Tutor applied to **F1Tenth autonomous-racing coursework** — specifically Lab 02, where students write a `safety_node` that must brake before colliding with obstacles. The grader runs in three layers and the AI tutor reads all three, so students see the same defect explained from three angles.

The demo deliberately models a real autonomous-vehicle safety property — **the brake decision must release when the threat clears** — that a naïve grader would silently let students get wrong.

**Watch the demo:** [youtu.be/sjjuj7pe4uw](https://youtu.be/sjjuj7pe4uw) — 15-minute demo presented at the **IEEE Intelligent Transportation Systems Society — Korea Chapter** pre-meeting for IV 2026 (2026-05-16).

## Three student states, three test outcomes

The demo replays the same lab through three commits a real student might make on the way to a correct solution:

| State | Code (`scan_callback`) | Result | What breaks |
|---|---|---|---|
| **Buggy** | `front_range = ranges[len(ranges) // 2]` | **6 / 11** | Looks at only the middle laser beam. Misses obstacles on the actual forward direction (which is at index 0 under the test's angle convention). Two unit tests + three physics-collision tests fail. |
| **Scalar** | `min_range = min(finite_ranges); ttc = min_range / speed` | **10 / 11** | Aggregates the lidar scan with `min()`, which lets a *lateral* obstacle (at θ = ±π/2, where closing rate is zero) trigger a false brake. Fails exactly one test: `test_no_brake_on_lateral_only_obstacle`. |
| **Per-beam (correct)** | `iTTC_i = r_i / max(-v · cos θ_i, 0)` | **11 / 11** | The README §III spec: range rate projected per beam via cosine. Side beams contribute zero closing rate even when their range is small. |

The grader is **outcome only**: did the car collide, did it brake when it shouldn't have. The AI tutor reads the failing test output plus the student's code and writes a paragraph or two explaining *why* the test broke, in plain language scaled to the student's level. On the scalar state, for example, the tutor names the cosine-projection requirement the student missed.

## Architecture

```
              ┌─────────────────────────────────────────────────┐
              │       GitHub Classroom — student repo           │
              │  push safety_node.py → classroom.yml workflow   │
              └─────────────────────────┬───────────────────────┘
                                        │
                          docker pull   ▼
              ┌─────────────────────────────────────────────────┐
              │       Grader image (Docker, GHCR-hosted)        │
              │   ROS 2 humble + pytest + scipy.integrate +     │
              │   gemini-python-tutor (LLM provider chain)      │
              └─────────────────────────┬───────────────────────┘
                                        │
                                        ▼
        ┌───────────────────┬───────────────────┬───────────────────┐
        │   Unit tests      │   Physics sim     │     AI tutor      │
        │  per-beam iTTC,   │  scipy.solve_ivp  │  reads test logs  │
        │  edge cases,      │  + collision      │  + student code   │
        │  false positives  │  event detection  │  + writes paragraph│
        └───────────────────┴───────────────────┴───────────────────┘
                                        │
                                        ▼
              ┌─────────────────────────────────────────────────┐
              │   GitHub Step Summary: 6/11 (or 10/11, 11/11)   │
              │   + per-scenario trajectory PNG + tutor markdown │
              └─────────────────────────────────────────────────┘
```

The **closed-loop physics simulation** runs five scenarios spanning the safety envelope (5 m/s, 10 m/s, 15 m/s head-on; stationary; intermittent lidar glitch). Vehicle dynamics use `a_max = 9.51 m/s²` and `scipy.integrate.solve_ivp` with event detection for sub-tick-precise collision and stop times. Total per-push grading overhead is ~100 ms.

## Why the brake decision releases when the threat clears

The F1Tenth ESC tracks the **last received** `/drive` target — the same behavior as a real automotive ECU. While the student's safety_node keeps publishing `drive.speed = 0.0` (because iTTC is still below the engagement threshold), the vehicle decelerates. When emission stops, the ESC's speed target reverts.

The grader models that faithfully. A naïve student whose code emits brake **once** on a single noisy lidar beam (no filtering, no multi-frame confirmation, no hysteresis) would produce exactly the failure mode NHTSA opened on Tesla in 2022 — **phantom braking** ([PE22-002](https://static.nhtsa.gov/odi/inv/2022/INOA-PE22002-7415.PDF)): a car that stops in the middle of a highway from a single misperception and never recovers. The grader's reference implementation uses a **production-pattern hysteresis controller** (engage at iTTC < 1.5 s, release at iTTC > 1.65 s — the same engage/release split used by Bosch and Mobileye ADAS). A student who internalizes "fire once, walk away" finds their car still passes the unit tests but under-decelerates and collides in the physics simulation.

This is the pedagogical bet: a grader that **fails the right way** teaches the right pattern. A grader that latches the brake permanently after the first emission would silently approve the phantom-braking design.

## The bug we're showing (and why it teaches)

The demo opens on the buggy state — `ranges[len(ranges) // 2]` — and walks through the failing test message. Then the student fixes to the scalar (`min(finite_ranges) / speed`) and reruns: now 10/11. *One* test still fails — the lateral-only test — and the tutor reads the new failure and explains the per-beam requirement. The student fixes to per-beam iTTC and reruns: 11/11.

The story is **two voices converging on the same defect**:
- The **test** says *"here is where it broke."*
- The **tutor** says *"here is why it broke, and here is the spec sentence that names the right fix."*

A human TA can read code and say the same things, but cannot read 50 commits a day, every day, every section, for 15 weeks. The tutor does.

## Roadmap — full f1tenth_gym in CI

The current physics simulation is a **1D longitudinal ODE solver**: enough to expose threshold-too-aggressive, missing-hysteresis, and single-tick noise-handling defects, and small enough to add ~100 ms per push to the autograder. The next step is to **wire the full f1tenth_gym simulator into the CI pipeline** so the same student commit that triggers unit tests also runs against:

- **Full 2-D vehicle dynamics** — single-track bicycle model with Pacejka tyre formulas, actuator lag, and yaw inertia. Catches defects that 1-D longitudinal dynamics cannot — for example, an AEB that brakes correctly straight-on but spins the car under panic-brake-while-cornering loads.
- **Realistic lidar simulation** — Gaussian beam noise, salt-and-pepper dropouts, finite range and angular resolution. The pedagogical hole flagged in the current grader (a naïve pure-threshold controller passes the 1-D scenarios because the synthetic lidar is noise-free) closes once gym's lidar is in the loop. Students who don't filter or hysteresis their iTTC will visibly chatter.
- **Track-based scenarios** — the canonical Levine, Spielberg, and Silverstone maps that the F1Tenth community already trains and benchmarks on. Lap-completion + collision-count + minimum-margin metrics over a full lap, not a single head-on geometry.
- **Multi-agent racing** — an opponent car running a published baseline (e.g., Disparity Extender or Follow-the-Gap) lets the student's safety_node face a moving threat. Currently out of scope for an introductory lab but well within reach as a Lab 5+ extension.

The technical blockers are not architectural — the grader image already runs ROS 2 humble and ships with rclpy. They are mostly about **CI runtime budget**:

- Full f1tenth_gym needs ~2-4 GB of additional dependencies in the image (gym, gym-extensions, numba, PyOpenGL for offscreen rendering). The current image is ~2 GB; growth is non-trivial but manageable.
- A single track lap at race pace takes 30-60 seconds of real time; running a 5-scenario battery would add several minutes per push. The 1-D ODE simulation runs in 5-10 seconds total.
- Offscreen rendering for the lidar simulation needs either headless OpenGL on the runner (works on GitHub-hosted runners with `xvfb-run`) or a swap to a pure-numpy 2D raycaster.

Path forward: **a tiered grading model**, where every push gets the fast 1-D physics layer (current), and a `gym-full` reusable workflow runs on a manual dispatch or on a slower nightly schedule. Students opt in for the deeper check; the autograder remains snappy for the inner loop. This is the same pattern the platform already uses for the heavier Heex monitoring layer.

Once gym is in CI, the same demo can be re-recorded with **a real Levine hallway lap** instead of a 1-D wall — and the AV-safety design rationale becomes a video of a vehicle that actually drives.

## Links

- [`roboracer-heex-agent-container`](https://github.com/try-ai-tutor/roboracer-heex-agent-container) — the grader image: tests, physics simulation, AI tutor entry points, Dockerfile. Source for `ghcr.io/try-ai-tutor/roboracer-heex-agent-container:latest`.
- [`f1tenth_lab2_template`](https://github.com/try-ai-tutor/f1tenth_lab2_template) — the student starter repository GitHub Classroom forks per student.
- [`f1tenth_lab2_tester`](https://github.com/try-ai-tutor/f1tenth_lab2_tester) — the autograder logic shared between the grader image and the upstream F1Tenth tester.
- [`gemini-python-tutor`](https://github.com/kangwonlee/gemini-python-tutor) — the LLM tutor (supports Gemini, Claude, Grok, Perplexity, NVIDIA NIM, or any OpenAI-compatible endpoint).
- [F1Tenth coursework upstream](https://github.com/f1tenth/f1tenth_lab_template) — the original lab series we extend.

The grader image, classroom workflow, AI tutor, and physics simulation are all separately versioned. Replacing one piece does not touch the others — the same architectural property that lets the platform serve introductory Python and autonomous-vehicle coursework with the same backbone.
