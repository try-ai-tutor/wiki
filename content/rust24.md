---
title: "Rust-24 — an introductory Rust track"
description: "24 auto-graded Rust assignments with per-commit LLM feedback, adapted from rustlings."
---

[한국어](./rust24.ko/)

**Rust-24** is a 24-assignment introductory Rust track delivered through the
same loop as the demo assignments on the home page: GitHub Classroom hands out
the assignment, GitHub Actions grade every commit inside a prebuilt Docker
image, and the AI tutor reads your code and the failing tests to explain what
went wrong. Students need nothing but a browser — no local Rust toolchain.

Each assignment maps 1:1 to one of the 24 numbered sections of
[`rust-lang/rustlings`](https://github.com/rust-lang/rustlings) (MIT-licensed),
restated as a single library-function exercise with hidden tests. rustlings is
MIT — we adapt the topics, not the exercise source.

## Current state

All **24 assignments are built, validated, and live** on the Classroom — all of **p000–p230** are created.

Accept an assignment from its invite link below — you need only a GitHub account
and a browser. All 24 (p000–p230) are live now.

## The track — six units of four

The 24 assignments are grouped into **six units of four**, so the track reads as a
paced sequence rather than one long list. All 24 (p000–p230) are live.

### Unit 1 · Foundations — p000–p030

| Slot | Topic | Classroom invite |
|---|---|---|
| p000 | Intro / hello world | [Accept assignment](https://classroom.github.com/a/RaaA8gTu) |
| p010 | Variables & mutability | [Accept assignment](https://classroom.github.com/a/fAbhXOtl) |
| p020 | Functions | [Accept assignment](https://classroom.github.com/a/oMXNhuq1) |
| p030 | Control flow (`if`) | [Accept assignment](https://classroom.github.com/a/fA0cRosR) |

### Unit 2 · Data & ownership — p040–p070

| Slot | Topic | Classroom invite |
|---|---|---|
| p040 | Primitive types | [Accept assignment](https://classroom.github.com/a/KdT0qwV1) |
| p050 | Vectors | [Accept assignment](https://classroom.github.com/a/zKAUyZ4G) |
| p060 | Move semantics | [Accept assignment](https://classroom.github.com/a/dhY2kuSG) |
| p070 | Structs | [Accept assignment](https://classroom.github.com/a/mLgko6kl) |

### Unit 3 · Modeling & organization — p080–p110

| Slot | Topic | Classroom invite |
|---|---|---|
| p080 | Enums & pattern matching | [Accept assignment](https://classroom.github.com/a/mXivwSQb) |
| p090 | Strings | [Accept assignment](https://classroom.github.com/a/2Tlm_w1F) |
| p100 | Modules | [Accept assignment](https://classroom.github.com/a/WgotTPfC) |
| p110 | Hash maps | [Accept assignment](https://classroom.github.com/a/cegK_jhG) |

### Unit 4 · Errors & abstraction — p120–p150

| Slot | Topic | Classroom invite |
|---|---|---|
| p120 | `Option` | [Accept assignment](https://classroom.github.com/a/wu9erNMQ) |
| p130 | Error handling | [Accept assignment](https://classroom.github.com/a/WtCzSpSt) |
| p140 | Generics | [Accept assignment](https://classroom.github.com/a/uSJY_kFp) |
| p150 | Traits | [Accept assignment](https://classroom.github.com/a/XA-8oXtT) |

### Unit 5 · Lifetimes & iterators — p160–p190

| Slot | Topic | Classroom invite |
|---|---|---|
| p160 | Lifetimes | [Accept assignment](https://classroom.github.com/a/N9_ljMud) |
| p170 | Tests | [Accept assignment](https://classroom.github.com/a/HyJnef3q) |
| p180 | Iterators | [Accept assignment](https://classroom.github.com/a/GHjL4Uy-) |
| p190 | Smart pointers | [Accept assignment](https://classroom.github.com/a/V2UbytiJ) |

### Unit 6 · Concurrency & tooling — p200–p230

| Slot | Topic | Classroom invite |
|---|---|---|
| p200 | Threads | [Accept assignment](https://classroom.github.com/a/oG1YT_4M) |
| p210 | Macros | [Accept assignment](https://classroom.github.com/a/dSr7UOas) |
| p220 | Clippy | [Accept assignment](https://classroom.github.com/a/io9bLu7h) |
| p230 | Type conversions | [Accept assignment](https://classroom.github.com/a/1AdTQH6Z) |

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
