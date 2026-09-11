# NVIDIA AI CAMPUS 1기 — 교육 커리큘럼 상세 정리

> NVIDIA developer.nvidia.com 자료를 토대로 정리한 **2개 과정(총 26챕터)** 챕터별 마크다운 모음 · 환경/하드웨어 준비사항 포함 (2026)

## 문서 구성
```
NVIDIA_AI_CAMPUS/
├── README.md                                    ← 이 파일 (전체 개요)
├── 01_AI_핵심_역량/
│   ├── 00_README_과정_개요.md
│   ├── 01_프로그래밍_데이터_기초.md          (#01 프로그래밍 & 데이터 기초)
│   ├── 02_머신러닝_이론_실습.md              (#02 머신러닝 이론 및 실습)
│   ├── 03_딥러닝_핵심_설계.md                (#03 딥러닝 핵심 설계)
│   ├── 04_컴퓨터비전_멀티모달_AI.md          (#04 컴퓨터비전 & 멀티모달 AI)
│   ├── 05_생성형_AI_LLM_응용.md              (#05 생성형 AI & LLM 응용)
│   ├── 06_AI_Agent_서비스_개발.md            (#06 AI Agent 서비스 개발)
│   ├── 07_NCA-GENL_자격시험_대비.md          (#07 NVIDIA NCA-GenL 출제영역·모의평가·자격시험)
│   ├── 08_Capstone_프로젝트.md               (#08 Capstone 프로젝트)
│   └── 09_취업역량_강화.md                   (#09 취업역량 강화)
└── 02_AI_Robotics/
    ├── 00_README_과정_개요.md
    ├── 01_리눅스_기초_로봇_개발환경.md        (#01 리눅스 기초 | 로봇 개발환경)
    ├── 02_파이썬_자율시스템_기초.md          (#02 파이썬 | 자율시스템 기초)
    ├── 03_머신러닝_딥러닝_Physical_AI_코어.md(#03 ML·DL | Physical AI 코어)
    ├── 04_LLM_RAG_생성형_AI_서비스.md        (#04 LLM·RAG | 생성형 AI 서비스)
    ├── 05_ROS2_기초.md                       (#05 ROS2 기초)
    ├── 06_DLI1_로봇_운동학_제어.md           (#06 DLI1 운통학·제어)
    ├── 07_DLI2_Isaac_Sim_입문.md             (#07 DLI2 Isaac Sim 입문)
    ├── 08_DLI3_Isaac_Lab_강화학습.md         (#08 DLI3 Isaac Lab RL)
    ├── 09_DLI4_Isaac_ROS_인식_내비게이션.md  (#09 DLI4 Isaac ROS)
    ├── 10_DLI5_자율_로봇_심화.md             (#10 DLI5 자율로봇 심화)
    ├── 11_DLI6_OpenUSD_디지털_트윈.md        (#11 DLI6 OpenUSD 디지털 트윈)
    ├── 14_ROS2_로봇제어_모션제어.md          (#14 ROS2 로봇제어)
    ├── 15_비전인식_OpenCV_3D.md              (#15 비전인식 OpenCV·3D)
    ├── 16_강화학습_로봇_제어_최적화.md       (#16 강화학습 최적화 프로젝트)
    └── 17_멀티모달_인터랙션_캡스톤.md        (#17 멀티모달 행동제어 캡스톤)
```

## 두 과정 구조 한 눈에

### 과정 1: AI 기초 역량 → 핵심 AI 기술 → AI Agent 실전 개발 → 프로젝트·커리어
```
[AI 기초 역량] 01. 프로그래밍 & 데이터  02. 머신러닝 이론·실습  03. 딥러닝 핵심 설계
[핵심 AI 기술] 04. 컴퓨터비전 & 멀티모달 AI  05. 생성형 AI & LLM 응용
[AI Agent 실전] 06. AI Agent 서비스 개발  07. NCA-GenL 시험 대비
[프로젝트·커리어] 08. Capstone  09. 취업역량 강화
```

### 과정 2: 개발환경 & AI 기초 → 강화학습·자율 로봇 → OpenUSD → 실전 캡스톤
```
[개발환경·기초] 01. 리눅스 02. 파이썬 03. ML·DL(Physical AI) 04. LLM·RAG
[로봇 SW] 05. ROS2 기초 06. DLI 운동학·제어 07. DLI Isaac Sim
[RL·자율로봇 심화] 08. DLI Isaac Lab RL 09. DLI Isaac ROS 10. DLI 자율로봇 심화
[디지털 트윈] 11. DLI OpenUSD
[실전] 14. 로봇제어 15. 비전인식 16. RL 최적화 17. 멀티모달 캡스톤(Jetson)
```

## 공통 준비사항 체크리스트 (교육 시작 전)
- [ ] **NVIDIA 계정 3종 가입**: Developer Program(docs·NGC)·NGC API Key·learn.nvidia.com(DLI)
- [ ] **개발 PC**: Ubuntu 22.04(WSL2) + Python 3.10~3.12 + VS Code
- [ ] **GPU(권장)**: 로컬 RTX 4080급(16GB VRAM) — 딥러닝·Isaac Sim 최소/권장 사양
- [ ] **클라우드 GPU 대안**: NVIDIA Brev(L40S) 가입 및 인스턴스 생성 방법 숙지
- [ ] **자격 대비**: NCA-GENL($125) DLI 필수 과정 4개 이수 + 모의고사 — 그 외 NCP-OUSD($200) 선택
- [ ] **로봇 에지(선택·예산 고려)**: Jetson Orin Nano Super Dev Kit($249) + 카메라·마이크·모터
- [ ] 공식 자료 링크: (아래 표)

## 주요 공식 자료 링크
| 항목 | URL |
|------|-----|
| NVIDIA Developer | https://developer.nvidia.com |
| NVIDIA DLI(교육·수료증) | https://learn.nvidia.com |
| DLI 전 과정 카탈로그 | https://www.nvidia.com/en-us/training/online |
| NVIDIA 인증(전체) | https://www.nvidia.com/en-us/learn/certification |
| NGC 카탈로그 | https://catalog.ngc.nvidia.com |
| build.nvidia.com(무료 LLM API) | https://build.nvidia.com |
| NVIDIA Brev(GPU 클라우드) | https://brev.dev |
| Isaac Sim 문서 | https://docs.isaacsim.omniverse.nvidia.com |
| Isaac Lab | https://github.com/isaac-sim/IsaacLab |
| Isaac ROS | https://developer.nvidia.com/isaac/ros |
| Jetson | https://developer.nvidia.com/embedded/jetson-modules |
| OpenUSD/인증 | https://developer.nvidia.com/openusd |
| Learn OpenUSD(무료) | https://docs.nvidia.com/learn-openusd/latest/ |
| NVIDIA AI Blueprints | https://github.com/NVIDIA-AI-Blueprints |
| NVIDIA AI 학습 경로 | https://www.nvidia.com/en-us/learn/learning-paths |

## 참고 (면책)
- 가격·버전·사양·출제 비중 등은 2026년 9월 기준 공식 페이지를 참고해 정리한 것으로, 최신 변경 사항은 각 공식 페이지에서 재확인하시기 바랍니다.
- 각 챕터 내 실습 난이도와 기간은 교육 운영 계획에 따라 조정될 수 있습니다.