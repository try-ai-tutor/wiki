---
title: "Rust-24 — Rust 입문 트랙"
description: "rustlings를 기반으로 재구성한 24개의 자동 채점 Rust 과제, 매 커밋마다 LLM 피드백 제공."
---

[English version](./rust24/)

**Rust-24**는 홈페이지의 데모 과제와 동일한 흐름으로 진행되는 24개 과제의 Rust 입문 트랙입니다. GitHub Classroom이 과제를 배포하고, GitHub Actions가 사전 빌드된 Docker 이미지 안에서 매 커밋을 채점하며, AI 튜터(AI tutor)가 학생의 코드와 실패한 테스트를 읽어 무엇이 잘못되었는지 설명해 줍니다. 학생에게 필요한 것은 웹 브라우저뿐이며, 로컬에 Rust 툴체인을 설치할 필요가 없습니다.

각 과제는 [`rust-lang/rustlings`](https://github.com/rust-lang/rustlings)(MIT 라이선스)의 번호가 매겨진 24개 섹션 각각에 1:1로 대응하되, 숨겨진 테스트를 갖춘 라이브러리 함수 하나를 작성하는 형태로 재구성되어 있습니다. rustlings는 MIT 라이선스로 공개되어 있으며, 본 트랙은 주제만 차용했을 뿐 연습 문제의 원문은 그대로 가져오지 않았습니다.

## 솔직한 진행 상황

**24개 과제 전부가 빌드·검증·배포 완료** 상태이며, **p000–p230** 전 구간이 Classroom에 연속적으로 올라가 있습니다. 아래 표의 각 행에 표시된 상태 배지는 다음과 같이 정직하게 의미를 분류합니다.

- **✓ ready** — 빌드 및 종단 간(end-to-end) 검증을 마치고 Classroom에 배포됨.
- **built — deploy pending** — 작성 및 로컬 검증 완료, 다만 학생용 Classroom 저장소에는 아직 배포되지 않음.
- **scaffolded** — 콘텐츠 초안이 작성되어 로컬 검증을 마쳤으나, 학생용 저장소에는 아직 올라가지 않음.
- **planned** — 아직 빌드되지 않음(주제와 학습 목표는 확정되어 있으나 콘텐츠는 없음).

아래의 초대 링크로 과제를 수락하시면 됩니다 — GitHub 계정과 웹 브라우저만 있으면 됩니다. 24개 전체(p000–p230)가 현재 모두 활성화되어 있습니다.

## 트랙 구성 — 4개씩 묶인 6개 유닛

24개의 과제는 **4개씩 묶인 6개 유닛**으로 그룹화되어, 하나의 긴 목록이 아니라 일정한 호흡으로 진행되는 시퀀스로 읽힙니다. 24개 전체(p000–p230)가 활성화되어 있습니다.

### 유닛 1 · 기초(Foundations) — p000–p030

| Slot | 주제 | 상태 | Classroom 초대 |
|---|---|---|---|
| p000 | 소개 / hello world | ✓ ready | [Accept assignment](https://classroom.github.com/a/RaaA8gTu) |
| p010 | 변수와 가변성(variables & mutability) | ✓ ready | [Accept assignment](https://classroom.github.com/a/fAbhXOtl) |
| p020 | 함수(functions) | ✓ ready | [Accept assignment](https://classroom.github.com/a/oMXNhuq1) |
| p030 | 제어 흐름 (`if`) | ✓ ready | [Accept assignment](https://classroom.github.com/a/fA0cRosR) |

### 유닛 2 · 데이터와 소유권(data & ownership) — p040–p070

| Slot | 주제 | 상태 | Classroom 초대 |
|---|---|---|---|
| p040 | 기본 자료형(primitive types) | ✓ ready | [Accept assignment](https://classroom.github.com/a/KdT0qwV1) |
| p050 | 벡터(vectors) | ✓ ready | [Accept assignment](https://classroom.github.com/a/zKAUyZ4G) |
| p060 | 이동 의미론(move semantics) | ✓ ready | [Accept assignment](https://classroom.github.com/a/dhY2kuSG) |
| p070 | 구조체(structs) | ✓ ready | [Accept assignment](https://classroom.github.com/a/mLgko6kl) |

### 유닛 3 · 모델링과 구조화(modeling & organization) — p080–p110

| Slot | 주제 | 상태 | Classroom 초대 |
|---|---|---|---|
| p080 | 열거형과 패턴 매칭(enums & pattern matching) | ✓ ready | [Accept assignment](https://classroom.github.com/a/mXivwSQb) |
| p090 | 문자열(strings) | ✓ ready | [Accept assignment](https://classroom.github.com/a/2Tlm_w1F) |
| p100 | 모듈(modules) | ✓ ready | [Accept assignment](https://classroom.github.com/a/WgotTPfC) |
| p110 | 해시 맵(hash maps) | ✓ ready | [Accept assignment](https://classroom.github.com/a/cegK_jhG) |

### 유닛 4 · 오류 처리와 추상화(errors & abstraction) — p120–p150

| Slot | 주제 | 상태 | Classroom 초대 |
|---|---|---|---|
| p120 | `Option` | ✓ ready | [Accept assignment](https://classroom.github.com/a/wu9erNMQ) |
| p130 | 오류 처리(error handling) | ✓ ready | [Accept assignment](https://classroom.github.com/a/WtCzSpSt) |
| p140 | 제네릭(generics) | ✓ ready | [Accept assignment](https://classroom.github.com/a/uSJY_kFp) |
| p150 | 트레이트(traits) | ✓ ready | [Accept assignment](https://classroom.github.com/a/XA-8oXtT) |

### 유닛 5 · 수명과 이터레이터(lifetimes & iterators) — p160–p190

| Slot | 주제 | 상태 | Classroom 초대 |
|---|---|---|---|
| p160 | 수명(lifetimes) | ✓ ready | [Accept assignment](https://classroom.github.com/a/N9_ljMud) |
| p170 | 테스트(tests) | ✓ ready | [Accept assignment](https://classroom.github.com/a/HyJnef3q) |
| p180 | 이터레이터(iterators) | ✓ ready | [Accept assignment](https://classroom.github.com/a/GHjL4Uy-) |
| p190 | 스마트 포인터(smart pointers) | ✓ ready | [Accept assignment](https://classroom.github.com/a/V2UbytiJ) |

### 유닛 6 · 동시성과 도구(concurrency & tooling) — p200–p230

| Slot | 주제 | 상태 | Classroom 초대 |
|---|---|---|---|
| p200 | 스레드(threads) | ✓ ready | [Accept assignment](https://classroom.github.com/a/oG1YT_4M) |
| p210 | 매크로(macros) | ✓ ready | [Accept assignment](https://classroom.github.com/a/dSr7UOas) |
| p220 | Clippy | ✓ ready | [Accept assignment](https://classroom.github.com/a/io9bLu7h) |
| p230 | 형 변환(type conversions) | ✓ ready | [Accept assignment](https://classroom.github.com/a/1AdTQH6Z) |

## 과제는 어떻게 동작하나

각 슬롯은 `todo!()` 스텁이 포함된 라이브러리 함수 하나로 구성됩니다. 학생은 `src/lib.rs`에 이를 구현하고 `main` 브랜치에 푸시합니다. 그러면 채점기가 비공개 Docker 이미지에 내장된 숨겨진 테스트를 실행합니다. 학생에게는 통과/실패 개수와 AI가 생성한 피드백만 노출되며, 테스트 코드 자체는 공개되지 않습니다. 이 방식은 p000 과제에서 종단 간으로 이미 검증된 동일한 레시피를 그대로 따릅니다.

## 출처(Credit)

주제와 학습 목표는 [`rust-lang/rustlings`](https://github.com/rust-lang/rustlings)(MIT)에서 차용하였습니다. rustlings의 연습 문제 원문은 본 트랙에 그대로 포함되어 있지 않습니다.
