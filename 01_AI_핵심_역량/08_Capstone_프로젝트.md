# 08. Capstone 프로젝트

> NVIDIA Brev 기반 AI 개발환경 활용 | 음성 비서·비전 AI·문서 자동화 Agent 개발 | NVIDIA Jetson 기반 멀티모달 AI 구현 · 팀 기반 기획·설계·개발·테스트·발표

## 1. 학습 목표
- NVIDIA Brev(클라우드 GPU)와 컨테이너 기반의 AI 개발환경을 실무처럼 활용할 수 있다.
- 음성 비서 / 비전 AI / 문서 자동화 등 실제 서비스형 AI 에이전트를 기획부터 배포까지 완성한다.
- NVIDIA Jetson(에지)에서 멀티모달 AI를 구현·시연한다.
- 팀 단위로 기획·설계·개발·테스트·발표의 전체 사이클을 경험한다.

## 2. 프로젝트 구성 (3대 트랙 선택)

### Track A. 음성 비서 에이전트 (Voice Assistant)
- **구성 요소**: ASR(음성→텍스트) → LLM(추론) → TTS(텍스트→음성)
- **기능 예시**: 음성 명령으로 일정 관리, 날씨/뉴스 조회(Tool 호출), 문서 검색(RAG)
- **NVIDIA 스택**: Speech NIM(ASR/TTS), NIM LLM, Agent Intelligence Toolkit
- **배포 대상**: 웹(STT/TTS 스트리밍) 또는 Jetson Orin Nano 마이크·스피커 연동

### Track B. 비전 AI 에이전트 (Vision AI)
- **구성 요소**: 실시간 카메라/영상 → 객체 감지 → LLM(VLM) 분석 → 리포트
- **기능 예시**: 출입구 사람·차량 감지, 공정 불량 검출, CCTV 영상 요약·검색
- **NVIDIA 스택**: YOLO→TensorRT, DeepStream 파이프라인, VLM(NIM)
- **배포 대상**: Jetson Orin Nano + CSI/USB 카메라, 또는 RTX GPU 로컬

### Track C. 문서 자동화 에이전트 (Document Automation)
- **구성 요소**: PDF/워드/엑셀/이미지 → 파싱 → 정제 → RAG → 요약/작성 → 저장·공유
- **기능 예시**: 계약서 요약·유효성 체크, 보고서 자동 생성, 설문/비용 데이터 집계
- **NVIDIA 스택**: 멀티모달 RAG Blueprint, NIM(vLLM/SGLang/TensorRT-LLM), Milvus
- **배포 대상**: Web 서비스(FastAPI+Streamlit) + 클라우드 GPU

## 3. 팀 기반 프로젝트 진행 (추천 일정)

| 단계 | 주차(제안) | 산출물 |
|------|-----------|--------|
| 기획 | 1~2주 | 문제 정의서, 페르소나, 기능 요구사항, MVP 범위 |
| 설계 | 2~3주 | 시스템 아키텍처 다이어그램, DB/벡터DB 스키마, API 계약, LLM 프롬프트 명세 |
| 개발 | 3~7주 | 에이전트 코어, Tool, 인증·보안, UI, 테스트 코드 |
| 테스트 | 7~8주 | 평가셋, 성능(지연/정확도), 환각/엣지케이스, 사용자 테스트 |
| 발표 | 8주 | 데모 영상, 아키텍처 발표, 회고 |

### 개발 프로세스 포인트
- **에이전트 설계**: 단일 vs 멀티 에이전트 결정, Tool Registry/메모리 설계
- **평가 지표**: 정확성, 지연시간, 비용, 사용자 만족 설문
- **보안**: API 키 분리(env), 프롬프트 인젝션 방어, 개인정보 식별·차단
- **형상 관리**: GitHub 브랜치/Git Flow, 코드리뷰, CI(선택)

## 4. 개발 환경 및 하드웨어 준비사항

### 4.1 NVIDIA Brev 개발환경 활용 (공식 권장 흐름)
1. https://brev.dev 접속 → 무료 가입(NVIDIA 계정 연동)
2. **Create Instance** → GPU 선택(예: **1x NVIDIA L40S** 또는 RTX급) → Deploy (5분 내 시작)
3. 접속 방법: 브라우저 Jupyter / `brev shell` (CLI SSH) / VS Code Remote SSH
4. Isaac/모델 컨테이너는 **Launchable**(원클릭 템플릿) 사용 가능
5. 실제 실습 조합 예: L40S + PyTorch 컨테이너 + Jupyter + Streamlit 포트포워딩

### 4.2 권장 하드웨어 구성
| 구성 | 내용 |
|------|------|
| 팀당 클라우드 GPU | Brev L40S 1기 (개발·학습), 필요 시 멀티 GPU |
| 데모 GPU(로컬) | RTX 4080/4090 또는 RTX 5080 (16GB 이상) |
| 에지(선택) | **Jetson Orin Nano Super Dev Kit** (67 TOPS, $249) + 마이크/카메라/스피커 키트 |
| 네트워크 | 클라우드-로컬 SSH 포트포워딩, Jetson 유선 이더넷 |
| 저장 | SharePoint/OneDrive·GitHub·NGC(모델 캐시) |

### 4.3 Jetson용 멀티모달 세팅 체크리스트
- [ ] JetPack 6.2 이상 SD 카드 이미지 플래싱 (https://developer.nvidia.com/embedded/jetpack)
- [ ] USB 마이크 배열(RESpeaker 등) 또는 USB 웹캠, 3.5mm 스피커
- [ ] `jtop` 설치 → 온도/전력/GPU 사용량 모니터링
- [ ] Docker 기반 Isaac ROS / NIM(Nano용) 컨테이너 준비
- [ ] 모델: Whisper/ASR 소형 모델, YOLO INT8, VLM 소형(Nano 추론 가능 모델 선택)

## 5. 평가 및 발표 기준
- 기술 완성도 (에이전트 동작 정확성·안정성)
- 사용자 경험 (UX 완성도, 응답 속도, 오류 처리)
- 설계 우수성 (아키텍처 근거, 확장성, 보안)
- 협업 프로세스 (깃 활발성, 일정 관리, 문서화)
- 발표력 (데모 시나리오, 문제 정의·해법 명확성, Q&A 대응)

## 6. NVIDIA 공식 연계 리소스
| 리소스 | 내용 | 링크 |
|--------|------|------|
| NVIDIA Brev | GPU 인스턴스·Launchable | https://brev.dev, https://developer.nvidia.com/brev |
| Jetson Orin Nano Super Kit | 에지 데모 하드웨어 | https://developer.nvidia.com/embedded/jetson-modules |
| Jetson AI Lab | 에지 실행 모델/예제 | https://www.jetson-ai-lab.com/ |
| NVIDIA AI Blueprints | 레퍼런스 앱(멀티모달 등) | https://github.com/NVIDIA-AI-Blueprints |
| NGC 컨테이너 | PyTorch·Isaac·NIM 이미지 | https://catalog.ngc.nvidia.com |
| Digital Twins for Physical AI 학습경로 | 물리 AI 융합 프로젝트 참고 | https://www.nvidia.com/en-us/learn/learning-paths |

## 7. 참고 자료
- Brev 퀵스타트: https://docs.nvidia.com/brev/latest/getting-started/quickstart.md
- Jetson Orin Nano User Guide: https://docs.nvidia.com/jetson/orin-nano-devkit/user-guide/latest/
- Speech NIM 튜토리얼: https://docs.nvidia.com/nim/speech/latest/