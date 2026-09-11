# 09. NVIDIA DLI 4 | Isaac ROS 인식·내비게이션

> Isaac ROS GPU 가속 패키지·실시간 인식 파이프라인 | SLAM·Nav2 자율주행·비전 기반 장애물 회피

## 1. 학습 목표
- Isaac ROS의 GPU 가속 패키지(SLAM·탐지·세그멘테이션·DNN 인퍼런스) 구성을 이해한다.
- ROS2로 실시간 인식 파이프라인(카메라→DNN→탐지→추적)을 구축할 수 있다.
- SLAM(Map 생성+위치추정)과 Nav2(경로계획·제어)로 자율주행을 시뮬레이션할 수 있다.
- 비전 기반 장애물 회피(거리추정·가상필드 등)를 구현할 수 있다.

## 2. 교육 내용 (주요 주제)

### 2.1 Isaac ROS 개요
- Isaac ROS: Jetson/데스크톱용 GPU 가속 ROS2 패키지 모음
- 지원: ROS2 Humble, Ubuntu 22.04, x86(RTX) + aarch64(Jetson)
- 대표 패키지: `isaac_ros_detect_and_segment`(YOLO/DetectNet), `isaac_ros_pose_estimation`, `isaac_ros_slam`, `isaac_ros_navigation`(`isaac_ros_amr`), `isaac_ros_dnn_encoders`, `isaac_ros_object_detection`
- 개발 배포: **Dev Container**(Isaac ROS 개발자 컨테이너) 기반 권장 — 의존성·환경 격리
- GPU 가속 원리: VPI(Vision Programming Interface), TensorRT, cuDNN 파이프라인

### 2.2 실시간 인식 파이프라인
- 노드 체인 예: `camera(Isaac Sim) → image_rect → detect_and_segment(YOLOv8/DetectNet) → tracker(NvTracker) → rviz`
- VPI로 이미지 사전처리(리사이즈·바이래터럴) GPU 가속
- DNN: TensorRT 엔진 생성/양자화(INT8), `isaac_ros_tensor_rt`
- 기성 모델: PeopleSemSegNet(사람 분할), Bisenet(장면 분할) — Isaac Sim에서 시뮬레이션 카메라로 검증
- 결과 시각화: rqt_image_view, RViz2, Foxglove

### 2.3 SLAM과 Nav2 자율주행
- **SLAM 개념**: 동시 위치추정·지도 구축 — VSLAM(카메라)·LiDAR SLAM
- Isaac ROS SLAM(`isaac_ros_slam`) 실행: `/scan`(or visual odometry) → map/odom 토픽
- **Nav2**: costmap(정적/동적) → AMCL/pose 정합 → planner(Dijkstra/A*) → controller(DPP/MPP, "DWB") → cmd_vel
- 구성 노드: `amcl`, `map_server`, `planner_server`, `controller_server`, `bt_navigator`, `waypoint_follower`
- 시뮬레이션에서 Carter/irobot 구동: `carter_navigation` 패키지(Isaac Sim ROS 워크스페이스 내)
- 한계 인지: LiDAR 없이 카메라만 → 복잡·최적화 필요; Jetson 자원 한계

### 2.4 비전 기반 장애물 회피
- 접근법: YOLO 탐지 → 거리 추정(싱글 카메라 크기 모델) → VFH/우회명령
- DWA(Dynamic Window Approach)·가상 힘장(Vector Field Histogram) 소개
- 강화학습 접목(8·16장): 이미지 관찰 + PPO로 내비게이션 정책 학습
- 안전: 콜리전 불량/멈춤 에지 케이스, 속도 제한, 리스타트

## 3. Hands-On 실습
1. Isaac ROS Dev Container 빌드/시작(`isaac-ros` 설치 스크립트)
2. Isaac Sim(또는 Jetson 카메라)에서 이미지 → `isaac_ros_detect_and_segment`(사람) 감지·시각화
3. `isaac_ros_slam` 실행 → 이동하며 지도 증축, 자세 추정 확인
4. Nav2로 목적지 좌표 주고 자율 주행 → 경로·속도 플롯
5. 감지→회피 통합: 물체가 나타나면 회피 명령을 내는 노드 작성 (sim or 실물)

## 4. 환경 및 하드웨어 준비사항
| 항목 | 권장 사항 |
|------|-----------|
| OS | Ubuntu 22.04, ROS2 Humble |
| Isaac ROS | Dev Container 방식 권장 (Docker + NVIDIA Container Toolkit) |
| GPU | 데스크톱: RTX 4080 / Jetson: Orin Nano·NX·AGX (JetPack 6.x) |
| 카메라 | Isaac Sim 가상 카메라 또는 USB/CSI 실물 카메라(Jetson) |
| LiDAR(선택) | 시뮬레이션 가상 LiDAR 우선, 실물은 RPLiDAR 등 |
| 저장 | Isaac ROS 컨테이너 ~10-20GB, 모델 캐시 추가 |
| 시각화 | RViz2, Foxglove, rqt_image_view |

## 5. NVIDIA 공식 연계 리소스
- Isaac ROS 홈: https://developer.nvidia.com/isaac/ros
- Isaac Sim + ROS2 서비스 가이드(HIL/SIL): https://docs.nvidia.com/learning/physical-ai/getting-started-with-isaac-sim/latest/
- Isaac ROS SLAM·DNN·Navigation 문서: https://nvidia-isaac-ros.github.io/
- Jetson 환경 세팅(JetPack·jtop): https://docs.nvidia.com/jetson/orin-nano-devkit/user-guide/latest/

## 6. 참고 자료
- Nav2 공식: https://docs.nav2.org/
- ROS2 위치 추정 캘리브레이션(Simulation 카메라 파라미터) 자료
- ORB-SLAM3 / RTAB-Map 이해용 리뷰 자료