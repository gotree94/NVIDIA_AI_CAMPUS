# 08. NVIDIA DLI 3 | Isaac Lab 강화학습

> 강화학습 환경 설계·PPO·SAC 알고리즘 적용 | 병렬 시뮬레이션 학습(서버측 처리)·보상함수 설계

## 1. 학습 목표
- 강화학습(RL)의 핵심 개념(MDP, 정책, 가치함수, 보상)을 이해한다.
- Isaac Lab의 매니저 기반(Manager-based) 환경 설계 방식을 이해한다.
- PPO(정책경사)와 SAC(오프폴리시)를 로봇 태스크에 적용·훈련·평가할 수 있다.
- GPU 병렬 환경(수천 개 env)으로 학습 속도를 확보하는 원리를 이해하고 사용한다.
- 태스크 성공률을 높이는 보상함수 설계(밀집/희소/쉐이핑/커리큘럼)를 할 수 있다.

## 2. 교육 내용 (주요 주제)

### 2.1 강화학습 기초 (Isaac Lab 관점)
- MDP: 상태 S, 행동 A, 전이함수 P, 보상 R, 감가율 γ
- 정책 π(a|s), 가치함수 V/Q, TD학습·부트스트래핑
- on-policy(PPO) vs off-policy(SAC·TD3) — 표본 효율·탐험 차이
- Isaac Lab의 병렬 학습: **수천 개 환경을 GPU에서 동시 시뮬레이션** — 샘플 속도 대폭 향상

### 2.2 Isaac Lab 환경 설계 (Manager-based)
- 구성 요소: Scene(로봇·물체·지면) / Action Manager / Observation Manager / **Reward Manager** / Termination Manager / Command Manager / Curriculum Manager
- `configclass` 기반 배선, `mdp` 패키지의 내장 보상 함수 재사용
- 예: "Reach" 태스크 — 엔드이펙터가 목표 pose 추종하도록 env 정의
- `rsl_rl`/`skrl`/RLlib 등 RL 라이브러리 인터페이스

### 2.3 PPO·SAC 적용
- **PPO**: 클리핑된 Surrogate Objective, GAE(advantage), 대량 병렬 환경 학습 — Isaac Lab 기본/추천
- **SAC**: off-policy + 엔트로피 정규화, 재생 버퍼, 자동 온도조절 — 샘플 효율 높음
- 훈련 실행: `python scripts/skrl/train.py --task <Task>-v0 --headless --num_envs 4096`
- 훈련 모니터링: 텐서보드(보상·학습률·엔트로피), 체크포인트 저장/로드
- 평가: `zero_agent`/`random_agent` 스크립트, 에피소드 성공률·평균 보상

### 2.4 병렬 학습·서버 처리
- GPU 병렬화: num_envs(권장 2048~16384)와 GPU 메모리 스케일링
- headless(무헤드) 모드로 서버/클라우드에서 대규모 학습
- 학습 구성: `args`(frames, steps, batch_size, lr, schedule), 동일 시드 재현
- 멀티 GPU(필요 시)나 클라우드(Brev L40S, DGX)로 스케일

### 2.5 보상함수 설계
- 희소 vs 밀집 보상, 쉐이핑(위치 오차·속도), 액션 페널티(부드러움)
- 보상 가중치의 미세조정, tanh 커널로 근거리 수렴 가속
- 도메인 상태(Yaw, 거리) 기반 커리큘럼으로 난이도 자동 상승
- 실패 모드 진단: termination(넘어짐·시간초과) 가중 설계
- 16장에서 심화(Sim-to-Real, 모방학습)로 이어짐

## 3. Hands-On 실습
1. Isaac Lab 설치 및 예제 태스크 실행: Cartpole(Legacy) and Reach/Manipulator
2. Cartpole을 PPO로 훈련해 "균형 유지" 정책 학습·성공 기준 달성
3. 2-DOF/Franka Reach 태스크를 4096 env로 병렬 훈련 (headless) — Elapsed 비교
4. 커스텀 보상(위치오차+속도 페널티+orientation) 추가·가중치 실험
5. 학습된 체크포인트를 Isaac Sim에 로드해 정책 평가(잘 되는/안 되는 케이스 분석)
6. (심화) SAC로 동일 태스크 비교 학습

## 4. 환경 및 하드웨어 준비사항
| 항목 | 권장 사항 |
|------|-----------|
| Isaac Sim | 최신 안정판(Isaac Sim 6.x 계열) 설치 |
| Isaac Lab | 별도 설치(파이썬 패키지) — https://github.com/isaac-sim/IsaacLab |
| RL 라이브러리 | rsl_rl(skrl/skrl에서 PPO) 또는 skrl(PPO·SAC), tensorboard, torch |
| GPU 서버 | **수천 env 병렬 시점부터 RTX 4080/4090 or L40S 권장**; 학습 대형→클라우드 |
| RAM | 32GB+(권장 64GB) — 병렬 env마다 메모리 증가 |
| 저장 | 학습 로그·체크포인트를 위한 SSD 여유 50GB+ |
| 클라우드 | Brev L40S 인스턴스(Isaac Launchable 포함) |
| Docker | NVIDIA 컨테이너 도구(NVIDIA Container Toolkit) |

## 5. NVIDIA 공식 연계 리소스
- Isaac Lab GitHub(예제 기반): https://github.com/isaac-sim/IsaacLab
- Getting Started with Isaac Lab(공식 학습경로): https://docs.nvidia.com/learning/physical-ai/getting-started-with-isaac-lab/latest/
- Isaac Lab 문서(docs.isaacsim 파라미터): tasks/environments/보상용어 문서화
- Isaac Lab 벤치마크(GPU 종류별 SPS): README Benchmark table

## 6. 참고 자료
- PPO 논문(Schulman et al. 2017), SAC 논문(Haarnoja et al. 2018)
- "Deep Reinforcement Learning Hands-On"(Maxim Lapan)
- 가상환경 병렬 시뮬레이션 리뷰(arXiv: Isaac Gym/Gymnasium 등)