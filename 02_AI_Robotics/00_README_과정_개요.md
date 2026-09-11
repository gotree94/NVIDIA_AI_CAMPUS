# NVIDIA AI CAMPUS 1기 — 02. AI Robotics 과정 (리눅스 → 자율 로봇 캡스톤)

> NVIDIA AI CAMPUS 1기 중 **AI Robotics** 과정 챕터별 정리 (NVIDIA DLI·Isaac Sim/Lab·Isaac ROS·Jetson·OpenUSD 기반, 2026)

## 과정 구성 (챕터별 파일)
| 챕터 | 주제 | 파일 |
|------|------|------|
| 01 | 리눅스 기초 | 로봇 개발환경 구축 | [01_리눅스_기초_로봇_개발환경.md](01_리눅스_기초_로봇_개발환경.md) |
| 02 | 파이썬 프로그래밍 | 자율시스템 기초 | [02_파이썬_자율시스템_기초.md](02_파이썬_자율시스템_기초.md) |
| 03 | 머신러닝·딥러닝 | Physical AI 코어 | [03_머신러닝_딥러닝_Physical_AI_코어.md](03_머신러닝_딥러닝_Physical_AI_코어.md) |
| 04 | LLM·RAG | 생성형 AI 서비스 개발 | [04_LLM_RAG_생성형_AI_서비스.md](04_LLM_RAG_생성형_AI_서비스.md) |
| 05 | ROS2 기초 | 로봇 소프트웨어 입문 | [05_ROS2_기초.md](05_ROS2_기초.md) |
| 06 | NVIDIA DLI 1 | 로봇 운동학·제어 기초 | [06_DLI1_로봇_운동학_제어.md](06_DLI1_로봇_운동학_제어.md) |
| 07 | NVIDIA DLI 2 | Isaac Sim 입문 | [07_DLI2_Isaac_Sim_입문.md](07_DLI2_Isaac_Sim_입문.md) |
| 08 | NVIDIA DLI 3 | Isaac Lab 강화학습 | [08_DLI3_Isaac_Lab_강화학습.md](08_DLI3_Isaac_Lab_강화학습.md) |
| 09 | NVIDIA DLI 4 | Isaac ROS 인식·내비게이션 | [09_DLI4_Isaac_ROS_인식_내비게이션.md](09_DLI4_Isaac_ROS_인식_내비게이션.md) |
| 10 | NVIDIA DLI 5 | 자율 로봇 심화과정 | [10_DLI5_자율_로봇_심화.md](10_DLI5_자율_로봇_심화.md) |
| 11 | NVIDIA DLI 6 | OpenUSD 디지털 트윈 | [11_DLI6_OpenUSD_디지털_트윈.md](11_DLI6_OpenUSD_디지털_트윈.md) |
| 14 | ROS2 로봇제어 | 모션제어·매니퓰레이션 | [14_ROS2_로봇제어_모션제어.md](14_ROS2_로봇제어_모션제어.md) |
| 15 | 비전인식 | OpenCV·3D 비전 | [15_비전인식_OpenCV_3D.md](15_비전인식_OpenCV_3D.md) |
| 16 | 강화학습 | 로봇 제어 최적화 프로젝트 | [16_강화학습_로봇_제어_최적화.md](16_강화학습_로봇_제어_최적화.md) |
| 17 | 멀티모달 인터랙션 | 로봇 행동제어 캡스톤 | [17_멀티모달_인터랙션_캡스톤.md](17_멀티모달_인터랙션_캡스톤.md) |

> 원본 커리큘럼 번호를 그대로 유지했습니다(12~13장은 교육과정에 미편성).

## 권장 학습 순서
```
Linux(01) → Python(02) → ML/DL(03) → LLM·RAG(04) → ROS2(05) → 운동학(06)
→ Isaac Sim(07) → Isaac Lab RL(08) → Isaac ROS(09) → 자율로봇 심화(10) → OpenUSD(11)
→ 로봇제어(14) → 3D 비전(15) → RL 프로젝트(16) → 멀티모달 캡스톤(17)
```

## 준비사항 요약 (전 과정 공통)
| 항목 | 내용 |
|------|------|
| OS (권장) | Ubuntu 22.04 (WSL2 포함) + NVIDIA 드라이버 |
| ROS2 | Humble (Isaac ROS 지원 버전 기준) |
| 시뮬레이터 | **NVIDIA Isaac Sim** — 최소 RTX 4080 / 16GB VRAM / 32GB RAM (권장: RTX 5080, 64GB) |
| 로봇 학습 | **Isaac Lab** — GPU 병렬(4096+ env), 훈련 시 추가 VRAM·RAM |
| 클라우드 GPU | NVIDIA Brev(L40S) / Isaac Launchable — 로컬 사양 부족 시 |
| 에지 실습 | **Jetson Orin Nano Super Dev Kit** (67 TOPS, 8GB) + 카메라/마이크/모터 |
| NGC 계정 | 컨테이너(Isaac Sim, NIM) 풀링용 API Key |
| 자격 대비 | OpenUSD 인증(NCP-OUSD) — 11장 참고, DLI 수료증 발급 |

## 주요 설치·접속 링크
- Isaac Sim 설치/요구사항: https://docs.isaacsim.omniverse.nvidia.com/latest/installation/requirements.html
- Isaac Lab: https://github.com/isaac-sim/IsaacLab
- Isaac ROS: https://developer.nvidia.com/isaac/ros
- Jetson: https://developer.nvidia.com/embedded/jetson-modules
- Brev: https://brev.dev
- DLI: https://learn.nvidia.com , https://www.nvidia.com/en-us/training/