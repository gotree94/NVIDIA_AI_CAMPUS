# 07. NVIDIA DLI 2 | Isaac Sim 입문

> Isaac Sim 물리엔진·USD 씬 구성·URDF→USD 로봇 임포트 | 센서 시뮬레이션(카메라·LiDAR)·가상환경 조작

## 1. 학습 목표
- NVIDIA Isaac Sim의 물리엔진(PhysX)·렌더링·USD 씬 구성 개념을 이해한다.
- URDF(및 MJCF)·CAD 자산을 USD로 임포트해 로봇 씬을 구성할 수 있다.
- 카메라·LiDAR·IMU 등 센서 시뮬레이션을 설정하고 데이터를 수집할 수 있다.
- Isaac Sim UI·Python API로 가상환경을 조작(조명·재질·물체 배치)할 수 있다.
- Isaac Lab(8장)으로 넘어가기 위한 기반을 다진다.

## 2. 교육 내용 (주요 주제)

### 2.1 Isaac Sim 개요와 USD
- Isaac Sim: NVIDIA Omniverse 기반 로봇 물리 시뮬레이터 (Apache-2.0 오픈소스)
- **USD(Universal Scene Description)**: Stage/Parse, Prim(Prism), 계층 구조, 리파인
- 씬 구성: 프로젝트(스테이지) → 물체 배치 → 물리 속성(collider, articulation) → 센서
- Isaac Sim UI: 뷰포트, Stage 트리, 속성 패널, Extension 관리
- Python API: `simulation_app`, `World`, `PhysxCfg`, `shuffle`/set 속성

### 2.2 URDF→USD 임포트
- URDF 임포터: `import urdf`, xacro 지원. 조인트(회전·프리즈매틱)·링크·관성 자동 변환
- 임포트 설정: 미터 단위, 질량, 콜라이더 자동 생성
- USD 구조 살펴보기, 시각 재질 지정, 포즈 조정
- 임포트 후 검증: URDF의 조인트가 USD Articulation으로 올바르게 형성되었는지 확인
- 대안: MJCF(MJCF→USD), OnShape/CAD 컨버터, `omni.isaac.urdf`

### 2.3 센서 시뮬레이션
- 카메라: RGB·Depth·Segmentation(Action 복셀/Instance), 렌즈·해상도 설정
- LiDAR: Rotating/моно scan, noise 파라미터, NuScenes/MSI 출력
- IMU·GPS·접촉 센서, 로봇 관절 엔코더/속도 센서
- 센서 데이터 수집: 타이머/콜백, timestamps, 저장(COCO/KITTI) 및 Omniverse Replicator 합성 데이터
- ROS2 브리지 연동: `/camera`, `/scan` 토픽 발행 확인

### 2.4 가상환경 조작·합성 데이터
- 물리 시뮬레이션 제어: `step`, `reset`, 데카르트 좌표·피직스 셋업
- 조명(Dome/Sphere/Rect), 재질(PBR), 배경(옴니버스)+randomize (도메인 랜덤화 개념)
- 완성 즉시 Isaac Lab 환경 포팅 가능한 USD 빌드 구조 이해
- (연계: 08장에서 Isaac Lab 훈련 → 다시 Isaac Sim에서 평가)

## 3. Hands-On 실습
1. Isaac Sim 설치(로컬/클라우드) 및 Compatibility Checker 통과 확인
2. 기본 USD 씬에 큐브·평면 배치, 중력·충돌 동작 확인
3. URDF 로봇(Carter 또는 Franka) 임포트 → 구동(조인트 목표) → 조인트 동작 촬영
4. 카메라 RGB·Depth·Seg 위 RGB 이미지 저장, LiDAR 점군 RViz/Rgedit로 시각화
5. ROS2 브리지로 `/cmd_vel` 발행→시뮬레이션 로봇 이동→`/odom` 수신
6. Omniverse Replicator로 장면 randomize → COCO 형식 출력

## 4. 환경 및 하드웨어 준비사항
### Isaac Sim 시스템 요구사항 (2026, 공식 문서 기준)
| 항목 | 최소 | 권장(Best) |
|------|------|-----------|
| OS | Ubuntu 22.04/24.04, Windows 10/11 | Linux 권장(컨테이너) |
| GPU | **RTX 4080 (16GB VRAM)** | RTX 5080 (16GB) |
| CPU | Intel i7 7세대 / Ryzen 5, 4코어 | 8코어 이상 |
| RAM | **32GB** | 64GB |
| 저장 | 50GB SSD | 500GB SSD |
| 드라이버 | 최신 NVIDIA Game/Studio 드라이버 | - |

> 주의: 16GB 미만 VRAM은 복잡한 씬/고인치 렌더링 실습이 제한될 수 있음. Isaac Lab 학습은 추가 RAM/VRAM 필요.
> 미달 사양 PC는 **NVIDIA Brev / 클라우드 GPU(L40S 등)** 사용 권장.

### 4.1 설치 방법 선택
1. **로컬(권장 실습)**: Isaac Sim 앱(Windows/Linux) 설치
2. **컨테이너**: `nvcr.io/nvidia/isaac-sim` NGC 이미지 + Docker (`--gpus all`)
3. **클라우드**: Brev의 Isaac Launchable(1클릭) / AWS·GCP 등
4. **PIP 마이너**: `pip install isaacsim`(파이썬 환경)

## 5. NVIDIA 공식 연계 리소스
- Isaac Sim 홈: https://developer.nvidia.com/isaac/sim
- 요구사항·설치: https://docs.isaacsim.omniverse.nvidia.com/latest/installation/requirements.html
- Sight/Getting Started 시리즈(Docs NVIDIA Learning): https://docs.nvidia.com/learning/physical-ai/getting-started-with-isaac-sim/latest/
- URDF Importer: `omni.isaac.urdf` 확장 Fast URL(README)
- Omniverse Replicator: https://docs.omniverse.nvidia.com/extensions/latest/ext_replicator/getting_started.html

## 6. 참고 자료
- Isaac Sim Examples(GitHub): https://github.com/isaac-sim/IsaacSim
- USD 학습(Learn OpenUSD 무료): https://developer.nvidia.com/openusd