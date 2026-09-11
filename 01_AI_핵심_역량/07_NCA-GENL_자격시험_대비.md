# 07. NVIDIA NCA-GenL 출제 영역 학습·모의평가·자격시험 대비

> NVIDIA-Certified Associate: Generative AI LLMs (NCA-GENL) — LLM 기반 에이전트/애플리케이션 개발 기초 자격

## 1. 시험 개요 (2026년 기준)
| 항목 | 내용 |
|------|------|
| 자격명 | NVIDIA-Certified Associate: Generative AI LLMs (**NCA-GENL**) |
| 목적 | 생성형 AI·LLM 기반 애플리케이션을 개발·통합·운영하기 위한 기초 역량 검증 |
| 등급 | Associate (입문~초급) |
| 응시료 | $125 |
| 시간 | 60분 |
| 문항 수 | 약 55~60문항 (객관식) |
| 언어 | 영어 |
| 유효기간 | 2년 |
| 응시 방식 | 온라인 원격 감독(Proctored), 기간 내 응시 |
| 등록처 | https://www.nvidia.com/en-us/learn/certification/generative-ai-llm-associate |

## 2. 출제 영역(블루프린트)와 비중
| 영역 | 비중 | 주요 내용 |
|------|------|-----------|
| Core Machine Learning & AI Knowledge | **30%** | ML/DL 학습 원리, 모델 훈련·평가 개념 |
| Software Development | **24%** | 데이터 증강, LLM 앱 개발, LangChain 워크플로우 |
| Experimentation(실험) | **22%** | 멀티 실험 관리, LangChain/LangGraph 활용, 허깅페이스 transformers |
| Data Analysis & Visualization | **14%** | 데이터셋 준비·EDA, 가속 데이터 처리 |
| Trustworthy AI(신뢰 가능한 AI) | **10%** | 안전·윤리·책임 있는 생성형 AI 배포 |

## 3. 권장 교육 과정 (시험 대비 필수 코스)
> NCA-GENL을 위해 아래 과정 중 지정 과정을 이수하는 것이 권장됩니다 (일부는 컬렉션 구성).

| 과정 | 유형 | 시간/가격 | 연계 영역 |
|------|------|-----------|-----------|
| Getting Started with Deep Learning | Self-paced | 8h / $90 | Core ML/AI (30%) |
| Fundamentals of Deep Learning | 강사 워크숍 | 8h / $500 | Core ML/AI |
| Accelerating End-to-End Data Science Workflows | Self-paced | 8h / $90 | Data Analysis(14%)(미선택 택1권장) |
| Fundamentals of Accelerated Data Science | 강사 워크숍 | 8h / $500 | Data Analysis |
| Building LLM Applications with Prompt Engineering | Self-paced/워크숍 | 6~8h / $90 | SW Dev(24%) · Experimentation(22%) |
| Rapid Application Development with LLMs | Self-paced/워크숍 | 8h / $90 | LangChain·LangGraph·transformers 중심 |

## 4. 상세 학습 로드맵 (4단계)

### Step 1 — Core ML/AI 지식 (30%)
- 지도/비지도/강화학습 개념, 과적합/과소적합
- 신경망 학습 과정: 역전파, 손실함수, 옵티마이저, 배치/에폭
- 데이터 증강(Augmentation)이 모델 성능에 미치는 영향
- 모델 평가 지표와 데이터 분할(train/valid/test)
- → 관련 챕터: 본 커리큘럼 02·03장

### Step 2 — 데이터 분석·전처리 (14%)
- 가속 데이터사이언스: 구조화 데이터 처리, 특징 인코딩, 리스케일링
- RAPIDS(cuDF/cuML) 기반 워크플로의 이점
- 데이터 시각화로 성능 해석
- → 관련 챕터: 01·02장

### Step 3 — LLM 애플리케이션 개발 (24%) + 실험 (22%)
- 프롬프트 엔지니어링 best practice (zero/few-shot, CoT, 시스템 프롬프트)
- LangChain: 모델 호출, 프롬프트 템플릿, 체인, 문서 부하·분할
- Hugging Face `transformers`: 파이프라인 사용, 토크나이저, 모델 저장/로드
- RAG 파이프라인 구성과 벡터DB
- 에이전트: LangGraph 기반 도구 호출·멀티스텝
- 반복 실험의 중요성과 평가 자동화
- → 관련 챕터: 05·06장

### Step 4 — Trustworthy AI (10%)
- LLM 환각·편향·유해 콘텐츠 통제
- 가드레일, 책임 있는 배포, 사용자 안전 관리
- 프롬프트 인젝션 등 보안 위협 인지

## 5. 모의평가 / 자격시험 대비 전략
1. **공식 학습자료 확인**: NVIDIA 인증 페이지의 Study Guide 다운로드
2. **실전 코딩 연습**: LangChain/LangGraph 샘플 프로젝트 5개 이상 직접 구현
3. **모의시험**: Preporato 등 서드파티 NCA-GENL 모의시험 반복 풀이 (해설 위주)
4. **타이머 적용**: 60분/60문항 → 문항당 1분 규율로 속도 훈련
5. **핵심 용어 숙지**: token, temperature, RAG, embedding, fine-tuning, prompt injection, guardrail, attention, backpropagation, CUDA/cuDF 용어
6. **최신 자료 반영**: NVIDIA가 2년 주기로 시험 업데이트 — 응시 전 최신 블루프린트 확인
7. 응시 환경: 조용한 공간, 카메라·마이크 준비, 신분증 지참 (온라인 감독 요건)

## 6. 시험 등록 및 유의사항
- 등록: NVIDIA 인증 페이지 → Register for Exam → 결제($125) → 응시 기간 선택
- 재시험: 불합격 시 재응시 가능 (제재 규정 확인)
- 관리: 인증 포털에서 성적·자격 상태 확인, LinkedIn 배지 연결 가능
- 사전 준비: NVIDIA 계정(ID) 필수, 결제 수단(카드) 준비

## 7. NVIDIA 공식 연계 리소스
| 리소스 | 내용 | 링크 |
|--------|------|------|
| NCA-GENL 인증 페이지 | 등록·블루프린트·안내 | https://www.nvidia.com/en-us/learn/certification/generative-ai-llm-associate |
| 학습 경로(Generative AI & LLMs) | 인증 대비 로드맵 | https://www.nvidia.com/en-us/learn/learning-path |
| DLI sel-paced courses | 위 필수 과정 수강처 | https://www.nvidia.com/en-us/training/online |
| build.nvidia.com | 실습용 무료 모델 API | https://build.nvidia.com |
| Preporato NCA-GENL 가이드 | 시험 해설·모의시험 (참고) | https://preporato.com/blog/nvidia-nca-genl-certification-complete-guide |

## 8. 관련 추가 인증 (선택 확장)
| 자격 | 내용 |
|------|------|
| NCA-AIIO | AI Infrastructure, $125/1h |
| NCA-ADS | Accelerated Data Science, $125/1h |
| NCA-GENM | Generative AI Multimodal, $125/1h |
| NCP-GENL | Professional: Generative AI LLMs, $200/2h |
| NCP-AAI | Professional: Agentic AI, $200/2h |
| NCP-OUSD | Professional: OpenUSD Development, $200/2h |