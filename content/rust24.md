---
title: "Rust-24 — an introductory Rust track"
description: "24 auto-graded Rust assignments with per-commit LLM feedback, adapted from rustlings."
---

**Rust-24** is a 24-assignment introductory Rust track delivered through the
same loop as the demo assignments on the home page: GitHub Classroom hands out
the assignment, GitHub Actions grade every commit inside a prebuilt Docker
image, and the AI tutor reads your code and the failing tests to explain what
went wrong. Students need nothing but a browser — no local Rust toolchain.

Each assignment maps 1:1 to one of the 24 numbered sections of
[`rust-lang/rustlings`](https://github.com/rust-lang/rustlings) (MIT-licensed),
restated as a single library-function exercise with hidden tests. rustlings is
MIT — we adapt the topics, not the exercise source.

## Honest status

All **24 assignments are now built and locally validated**; **eight are live** on the
Classroom and the rest are deploy-pending (rolling out). The status badge on each row
below is honest:

- **✓ ready** — built, validated end-to-end, and live on the Classroom.
- **built — deploy pending** — authored and locally validated; not yet on a
  student-facing Classroom repo.
- **scaffolded** — content drafted and locally validated, not yet on a
  student-facing repo.
- **planned** — not built yet (topic and learning goal fixed; no content).

Per-assignment GitHub Classroom invite links are filled in as each assignment
becomes class-ready. Until then each link is a `TODO` placeholder — there are
no invites for the deploy-pending slots yet. The track's Classroom lives at
<https://classroom.github.com/classrooms/275699733-try-ai-rust-tutor>.

## The 24 assignments

| Slot | Topic | Status | Classroom invite |
|---|---|---|---|
| p000 | Intro / hello world | ✓ ready | _TODO: add invite_ |
| p010 | Variables & mutability | scaffolded | _TODO: add invite_ |
| p020 | Functions | ✓ ready | [Accept assignment](https://classroom.github.com/a/oMXNhuq1) |
| p030 | Control flow (`if`) | ✓ ready | [Accept assignment](https://classroom.github.com/a/fA0cRosR) |
| p040 | Primitive types | ✓ ready | [Accept assignment](https://classroom.github.com/a/KdT0qwV1) |
| p050 | Vectors | ✓ ready | [Accept assignment](https://classroom.github.com/a/zKAUyZ4G) |
| p060 | Move semantics | ✓ ready | [Accept assignment](https://classroom.github.com/a/dhY2kuSG) |
| p070 | Structs | ✓ ready | [Accept assignment](https://classroom.github.com/a/mLgko6kl) |
| p080 | Enums & pattern matching | ✓ ready | [Accept assignment](https://classroom.github.com/a/mXivwSQb) |
| p090 | Strings | ✓ ready | [Accept assignment](https://classroom.github.com/a/2Tlm_w1F) |
| p100 | Modules | built — deploy pending | _TODO_ |
| p110 | Hash maps | built — deploy pending | _TODO_ |
| p120 | `Option` | built — deploy pending | _TODO_ |
| p130 | Error handling | built — deploy pending | _TODO_ |
| p140 | Generics | built — deploy pending | _TODO_ |
| p150 | Traits | built — deploy pending | _TODO_ |
| p160 | Lifetimes | built — deploy pending | _TODO_ |
| p170 | Tests | built — deploy pending | _TODO_ |
| p180 | Iterators | built — deploy pending | _TODO_ |
| p190 | Smart pointers | built — deploy pending | _TODO_ |
| p200 | Threads | built — deploy pending | _TODO_ |
| p210 | Macros | built — deploy pending | _TODO_ |
| p220 | Clippy | built — deploy pending | _TODO_ |
| p230 | Type conversions | built — deploy pending | _TODO_ |

## How an assignment works

Each slot is one library function with a `todo!()` stub. Implement it in
`src/lib.rs`, push to `main`, and the grader runs hidden tests baked into a
private Docker image — you see the pass/fail count and AI-generated feedback,
not the test code. This is the same recipe the p000 assignment proved
end-to-end.

## Credit

Topics and learning goals adapted from
[`rust-lang/rustlings`](https://github.com/rust-lang/rustlings) (MIT). No
rustlings exercise source text is reproduced.
