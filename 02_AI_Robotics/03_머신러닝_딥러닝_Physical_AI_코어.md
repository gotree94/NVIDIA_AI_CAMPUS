# 03. 머신러닝·딥러닝 | Physical AI 코어

> scikit-learn 기반 회귀·분류·군집화·앙상블 | 신경망 순전파·역전파·경사하강법

## 1. 학습 목표
- scikit-learn으로 회귀·분류·군집화·앙상블 모델을 데이터에 맞게 적용·평가할 수 있다.
- 신경망의 순전파·역전파·경사하강법을 수식과 코드로 이해한다 (물리 AI 정책학습의 기반).
- 로봇 데이터(센서)에 ML 모델을 적용하는 실전 감각을 기른다 (Physics-informed ML 소개 포함).

## 2. 교육 내용 (주요 주제)

### 2.1 scikit-learn: 회귀·분류·군집화·앙상블
- **회귀**: `LinearRegression`, `Ridge`/`Lasso`, 다항, 평가(MAE/RMSE/R²)
- **분류**: 로지스틱, 결정트리, SVM, KNN, 평가(정확도·F1·ROC-AUC)
- **군집화**: K-Means, 계층적, DBSCAN + 실루엣 계수
- **앙상블**: RandomForest, GradientBoosting, XGBoost/LightGBM, Voting·Stacking
- 교차검증(KFold)·하이퍼파라미터(GridSearchCV/Optuna)·파이프라인
- 로봇 연계 예: 발판 위상 분류, 장애물 인식 피처(거리·각도) 학습, 내비게이션 히트맵

### 2.2 신경망 순전파·역전파·경사하강법
- 퍼셉트론 → MLP → 딥러닝 확장, 활성화(ReLU·Softmax·Sigmoid·GELU)
- 순전파 단계별 이해: `z = W·x + b`, `a = activation(z)`, 손실함수 선택
- 역전파: 연쇄법칙으로 각 파라미터의 그래디언트 계산, 체인 기반 코드 구현
- 경사하강법: SGD → Momentum → Adam, 학습률·배치의 역할
- 과적합/과소적합·정규화(Dropout·BatchNorm·weight decay)·Early Stopping
- **왜 물리 AI에서 DL인가**: 고차원 센서 입력(이미지·LiDAR) → 인식 + 강화학습 정책 표현

### 2.3 PyTorch 미니멀 워크플로
- `nn.Module` 정의 → `DataLoader` → `optimizer` → train/valid 루프
- 로봇 연계 데이터셋: 관절 각도·토크 시퀀스로 역기구학 근사, 동역학 예측(회귀)
- 재현성: seed 고정, 체크포인트 저장/로드
- (8장 심화) Isaac Lab의 PPO/SAC는 바로 이 신경망 구조 위에서 정책·가치망을 학습

## 3. Hands-On 실습
1. 가상 로봇 센서 데이터(거리·속도·관절각) 생성 → 분류(장애물 유무)·회귀(내려올 힘) 모델 성능 비교
2. 신경망을 NumPy로 직접 구현해 순전파·역전파 검증(MNIST 단순 이진분류)
3. PyTorch로 관절 시퀀스 → 다음 상태(토크) 예측 회귀 신경망 완성
4. GridSearchCV/Optuna로 앙상블 모델 최적화 + 학습 곡선 해석
5. 학습/검증 loss 곡선으로 과적합 진단 및 정규화 적용 실험

## 4. 환경 및 하드웨어 준비사항
| 항목 | 권장 사항 |
|------|-----------|
| OS | Ubuntu 22.04 (WSL2 OK) |
| Python | 3.10~3.12 |
| 라이브러리 | scikit-learn, numpy, matplotlib, pandas, torch/torchvision, optuna |
| GPU | CPU로 대부분 가능. 신경망 큰 실습은 GPU 권장(RTX 4080, 또는 Brev) |
| CUDA | PyTorch 2.x 필요시 CUDA 12.x 환경 (WSL2 지원) |

## 5. NVIDIA 공식 연계 리소스
- DLI: Getting Started with Deep Learning — https://learn.nvidia.com
- NVIDIA PhysicsNeMo · Physics-Informed ML(심화) — https://developer.nvidia.com/physicsnemo
- NVIDIA AI Workbench — 로컬/클라우드 통일된 ML 환경 https://www.nvidia.com/en-us/deep-learning-ai/solutions/data-science/workbench/
- RAPIDS cuML — GPU scikit-learn 대체 https://developer.nvidia.com/rapids/cuml

## 6. 참고 자료
- scikit-learn 문서: https://scikit-learn.org/stable/
- 딥러닝 참고서(추천): "Deep Learning"(C. Bishop), D2L(https://d2l.ai)