# 15. 비전인식 | OpenCV·3D 비전

> OpenCV 이미지 처리·객체탐지·특징점 추출 | 3D 비전(포인트클라우드·깊이카메라)·캘리브레이션

## 1. 학습 목표
- OpenCV로 이미지 전처리와 객체탐지·특징점 추출을 수행할 수 있다.
- 깊이카메라·3D 포인트클라우드를 취득·처리하고 ROS2 인터페이스로 다룰 수 있다.
- 카메라 캘리브레이션(내부/외부 파라미터)과 이미지↔3D 변환을 이해하고 구현한다.
- 로봇 시각 인식 파이프라인(색·형태·위치 추정 → 파지 포즈)을 구축한다.

## 2. 교육 내용 (주요 주제)

### 2.1 OpenCV 기초·객체탐지·특징점
- 입출력·색공간, 변환/기하학, 필터·쓰레시홀드·형태학, 컨투어
- 에지 검출(Canny)·코너(Harris, Shi-Tomasi), 특징점(SIFT, ORB) + 매칭(BF/FLANN)
- 객체탐지 로컬: Haar 컨스케이드, 템플릿매칭, (딥러닝은 09장 YOLO로 확장)
- ROS2 연동: `cv_bridge`(Image메시지↔cv::Mat), `sensor_msgs/Image`

### 2.2 3D 비전: 포인트클라우드·깊이카메라
- 깊이 센서 종류: 스테레오, TOF(RealSense), 구조광 — 원리와 트레이드오프
- RGB-D 카메라: 내부 파라미터로 depth·color 정합 → PointCloud2 생성
- 포인트클라우드 처리: 배경 제거(PassThrough), Voxel 다운샘플, 색상 기반 분할, RANSAC 평면(Table) 추출
- ROS2: `sensor_msgs/PointCloud2`, `pcl_ros` 노드, RViz에서 점군 시각화
- 파지 포즈 도출: 물체 점군 → 중심·방향(주축분석) → 실시간 그리퍼 좌표

### 2.3 캘리브레이션
- 호모그래피/핀홀모델: f, cx, cy, 왜곡 계수 — 내부 파라미터
- 체커보드 캘리브레이션: `calibrateCamera`(OpenCV), `camera_calibration`(ROS2), aruco 캘리브레이션
- 외부 파라미터: 카메라↔base 프레임, eye-in-hand / eye-to-hand 교정(TF)
- 깊이 카메라 공장 셋업 시 참고값·한계 인지

### 2.4 통합 비전 파이프라인 (로봇)
- 파이프라인 예: **캘리브레이션 → 이미지 수신 → 물체 검출(색/특징) → 3D Center 구함 → 그리퍼 포즈 변환 → grasp**
- 제품: 물체 분류(타입/색) + 위치(2D→3D) + 방향 → 로봇 TF로 변환
- 깊이·컬러가 필요 없는 대안(단일 카메라 거리 추정) 비교

## 3. Hands-On 실습
1. OpenCV 직선/탐지: 컬러 스페이스 분할로 빨간 볼 인식, 컨투어→중심점·반지름
2. SIFT/ORB로 물체 특징 매칭 → 위치 워핑
3. (Isaac Sim 또는 실물) RGB-D 수신→PassThrough+Voxel+RANSAC 테이블 제거→물체 점군→중심 좌표
4. 체커보드/아루코 캘리브레이션으로 카메라 파라미터 계산 및 왜곡 보정 검증
5. 인식→그리퍼 포즈 변환이 적용된 "집기" 시뮬 시나리오 실행 (MoveIt 또는 Isaac 컨트롤러)

## 4. 환경 및 하드웨어 준비사항
| 항목 | 권장 사항 |
|------|-----------|
| 라이브러리 | OpenCV, numpy, open3d(또는 pcl), matplotlib |
| ROS2 | cv_bridge, pcl_ros, camera_calibration; rviz2 |
| 카메라(실물) | Intel RealSense D435(깊이)/ D415, 웹캠(캘리브레이션용) |
| 카메라(시뮬) | Isaac Sim camera(depth·RGB)로 동일 파이프라인 재현 |
| GPU | 처리 전부 CPU 가능. 딥러닝 탐지 사용 시 GPU(또는 Jetson) |
| 추가 HW | 체커보드·ArUCo 프린트, 그림 프레임(캘리 실습용) |

## 5. NVIDIA 공식 연계 리소스
- Get Started with AI on Jetson(DLI 무료) — Jetson에서 OpenCV 실습
- Building Video AI Applications at the Edge on Jetson(DLI, $90)
- Jetson 차량 비전 샘플: https://www.jetson-ai-lab.com/
- Isaac Sim Camera SDK 가이드

## 6. 참고 자료
- OpenCV 튜토리얼: https://docs.opencv.org/
- Open3D 문서: https://www.open3d.org/
- ROS2 Image/PointCloud2 메시지: http://docs.ros.org/en/humble/
- camera_calibration 패키지 문법