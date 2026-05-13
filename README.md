# 🤖 자율주행 장애물 회피 시스템

> LIDAR 기반 Differential Drive 차량의 장애물 회피 시스템

[![MATLAB](https://img.shields.io/badge/MATLAB-Simulink-orange.svg)](https://www.mathworks.com/products/simulink.html)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

## 📌 프로젝트 개요

자율 주행 자동차의 LIDAR 센서를 이용한 실시간 장애물 회피 시스템 개발 프로젝트입니다.

### 기본 정보

| 항목 | 내용 |
|------|------|
| **주제** | 자율 주행 자동차의 장애물 회피 시스템 |
| **차량 모델** | Differential Drive (원형 차체 + 좌우 바퀴 2개 + 캐스터) |
| **센서** | LIDAR |
| **제어 축** | Y축 횡방향 (Vx 일정 가정) |
| **구현 환경** | MATLAB Simulink |
| **팀 구성** | 3인 |

## 👥 팀원

- **손영탁** (20225283)
- **강성원** (20225262)
- **권영민** (20245304)

## 🧠 시스템 아키텍처

### 알고리즘 구성

| 역할 | 알고리즘 | 설명 |
|------|----------|------|
| **목표 추적** | Pure Pursuit | Look-ahead Point 기반 조향각 δ 계산 |
| **장애물 회피** | VFH (Vector Field Histogram) | LIDAR 데이터 → 장애물 밀도 히스토그램 → 회피 방향 선택 |
| **출력 안정화** | LPF (Low Pass Filter) | VFH 출력의 급격한 변화 제거 → 부드러운 조향 |
| **구동 변환** | Differential Drive 변환 | δ → ω → VL, VR 변환 |

### 알고리즘 흐름

```
[LIDAR] → [VFH] → [LPF] → [Pure Pursuit] → [δ → VL, VR 변환] → [Diff. Drive 모델]
                                ↑
                         [목표 지점 입력]
```

## 👤 역할 분담

### A — 차량 모델링 & 시스템 설계
- Differential Drive 모델 구현
- 차량 파라미터 설정
- 전체 Simulink 아키텍처 설계

### B — Pure Pursuit + LPF 구현
- Pure Pursuit 알고리즘 블록 구현
- Look-ahead Distance 튜닝
- LPF 블록 구현 및 α 파라미터 튜닝

### C — LIDAR + VFH 구현
- LIDAR 신호 모델링
- VFH 장애물 밀도 히스토그램 구현
- 회피 방향 선택 로직

## ⚙️ 주요 파라미터

| 파라미터 | 기호 | 값 |
|----------|------|-----|
| 전진 속도 (고정) | Vx | 0.5 m/s |
| 휠베이스 | L | 0.025 m |
| 트레드 | W | 실측값 (m) |
| Look-ahead Distance | ld | 튜닝 필요 |
| LPF 필터 계수 | α | 0 ~ 1 (튜닝 필요) |
| LIDAR 감지 거리 | d_lidar | 1 ~ 2 m |
| 안전거리 | d_safe | 실측 기반 계산 |
| VFH 셀 크기 | — | 5° |
| 질량 | m | 0.03776 kg |

## 📚 문서

- [알고리즘 상세 설명](docs/ALGORITHMS.md)
- [실험 결과 기록](docs/EXPERIMENTS.md)

## 🚀 시작하기

### 필요 환경
- MATLAB R2020b 이상
- Simulink
- Robotics System Toolbox (선택)

## 📊 주요 결과

- Look-ahead Distance 최적화를 통한 경로 추종 성능 향상
- VFH 알고리즘을 활용한 실시간 장애물 회피 성공
- LPF를 통한 안정적인 조향 제어 구현

자세한 실험 결과는 [EXPERIMENTS.md](docs/EXPERIMENTS.md)를 참고하세요.

## 📝 License

MIT License

## 🔗 참고 자료

- Pure Pursuit 알고리즘 논문
- VFH (Vector Field Histogram) 원본 논문
- MATLAB Simulink 공식 문서
