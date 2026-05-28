---
title: "RoboRacer — 자율주행 레이싱 실습"
description: "자율주행 레이싱 실습을 자동 채점 + 매 커밋 LLM 튜터 피드백 형태로 제공: 계층화된 단위 테스트와 폐루프 시뮬레이션으로 ROS 2 노드를 채점합니다."
---

[English version](./roboracer/)

**RoboRacer**는 공개 [RoboRacer](https://roboracer.ai/learn) 자율주행 레이싱 커리큘럼을 웹 브라우저만으로 수행 가능한 자동 채점 실습으로 재구성한 트랙입니다. 각 lab은 학생이 직접 구현하는 ROS 2 노드 하나이며, 학생이 커밋할 때마다 GitHub Actions가 사전 빌드된 컨테이너 안에서 채점을 진행합니다 — 먼저 비용이 낮은 구조 검사와 단위 테스트를 수행한 뒤, 이어서 폐루프(closed-loop) 물리 시뮬레이션을 실행합니다. 그리고 LLM 튜터가 실패한 테스트와 학생의 코드를 읽어 무엇이 잘못되었는지 설명해 줍니다. ROS를 로컬에 설치할 필요는 없으며, GitHub 계정과 웹 브라우저만 있으면 됩니다.

## 솔직한 진행 상황

채점 파이프라인은 이미 **검증된 상태**입니다 — Lab 2에서 시연되었고, **Lab 4 Python**과 **Lab 6 Python**에서 종단 간(end-to-end)으로 검증되어 현재 Classroom에 **활성화**되어 있습니다. 나머지 lab들은 학생 템플릿 형태로 구축되어 있으나 채점기가 모두 검증·배포된 상태는 아니며, 아래 표가 그 사실을 그대로 반영합니다.

- **✓ live** — 종단 간 검증을 마치고 Classroom에 활성화됨(아래 초대 링크 참조).
- **demo** — 공개된 워크스루(영상 + 글)로 시연되어 있으나, 셀프 서비스 초대 링크는 제공되지 않음.
- **grader fixes in flight** — 학생 템플릿은 존재하나, 채점기 회귀(regression) 수정이 별도 브랜치에서 진행 중 — 깨진 자동 채점기에 학생이 커밋을 마주치지 않도록 초대 링크는 보류 중.
- **built — deploy pending** — 학생 템플릿은 존재하나, 채점기 검증과 Classroom 게시는 아직 남아 있음.
- **planned** — 재배포 또는 최초 배포가 예정되어 있으나, 템플릿도 Classroom 과제도 아직 새 roboracer Classroom에 올라가지 않음.

## 실습 목록

| Lab | 주제 | Python | C++ |
|---|---|---|---|
| 2 | 자동 비상 제동(Automatic Emergency Braking) | demo + re-deploy 예정 · [demo + video](/wiki/roboracer-lab02/) | — |
| 3 | 벽 추종(Wall Following, PID) | built ✓ — classroom 준비중 | built ✓ — classroom 준비중 |
| 4 | Follow the Gap | **✓ live** · [Accept assignment](https://classroom.github.com/a/mxXkLIMf) | **✓ live** · [Accept assignment](https://classroom.github.com/a/G_IF3gLI) |
| 5 | 스캔 매칭(Scan Matching, PLICP) | — | **✓ live** · [Accept assignment](https://classroom.github.com/a/L-DehS19) |
| 6 | Pure Pursuit | **✓ live** · [Accept assignment](https://classroom.github.com/a/ehA0rYJt) | **✓ live** · [Accept assignment](https://classroom.github.com/a/Fo9vQlQC) |
| 7 | 모션 플래닝(Motion Planning, RRT) | built — deploy 준비중 | built — deploy 준비중 |
| 8 | 인식 / 비전(Perception / Vision) | built — deploy 준비중 | — |
| 9 | 모델 예측 제어(Model Predictive Control) | built — deploy 준비중 | — |

Lab 1(Intro to ROS 2)은 의도적으로 자동 채점 트랙에서 제외되어 있습니다. 그 산출물은 pub/sub 배선과 `colcon` 워크스페이스 구성으로, 원본 RoboRacer 강의에서도 Lab 2 이후의 본격적인 실습에 앞서 채점하지 않는 워밍업 단계로 다루고 있기 때문입니다.

## 실습 채점 방식

채점은 **계층화(tiered)되어 있고 fail-fast** 방식으로 동작합니다. 비용이 낮은 구조 검사와 단위 테스트가 먼저 실행되고, 이어서 **폐루프 물리 시뮬레이션**(결정론적, headless — 매 커밋마다 돌릴 수 있을 만큼 빠른 형태)이 실행되며, 마지막으로 AI 튜터가 동작합니다. 판정과 피드백은 GitHub Step Summary에서 통과/실패 배지 옆에 함께 표시됩니다. [Lab 2 데모](/wiki/roboracer-lab02/)가 전 과정을 완비한 워크스루 예시입니다. 향후 반복 계획에서는 가벼운 시뮬레이션이 통과된 *이후* 단계에서 **f1tenth_gym** 전체를 돌려, 원본 lab들이 요구하던 풍부한 산출물(전체 트랙 랩, 궤적 등)을 생성합니다. 단, 빠른 검사를 통과하지 못한 제출에 대해서는 그 비용을 지불하지 않습니다.

## 출처(Credit)

공개된 **RoboRacer** 자율주행 레이싱 커리큘럼([roboracer.ai/learn](https://roboracer.ai/learn))의 Lab 02 부터 09 까지를 차용하여 재구성하였습니다. 본 트랙은 주제와 채점 방식을 새로 구성한 것이며, 원본 강의 자료의 저작권은 원 저자에게 있습니다.
