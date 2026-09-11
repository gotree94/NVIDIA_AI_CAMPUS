# 06. AI Agent 서비스 개발

> AI Agent 서비스 분석·활용 | Agent UX·기능·기술적 한계 분석 | LLM 기반 애플리케이션 활용

## 1. 학습 목표
- 실제 상용 AI 에이전트 서비스(챗봇, 코딩 에이전트, 문서 자동화 등)를 분석하고 활용할 수 있다.
- 에이전트 서비스의 UX·기능·기술적 한계를 체계적으로 평가할 수 있다.
- LLM 기반 애플리케이션(챗봇·RAG·문서 요약·검색)을 설계하고 구현할 수 있다.
- 에이전트 서비스를 엔드투엔드(기획→개발→배포→운영)로 완성하는 방법을 익힌다.
- NVIDIA의 에이전트 스택(NeMo, NIM, Blueprints, Agent Intelligence Toolkit)를 사용한다.

## 2. 교육 내용 (주요 주제)

### 2.1 AI Agent 서비스 분석·활용
- 에이전트 서비스 유형 조사: 고객지원 챗봇, 개인 비서, 코딩 에이전트(Assistant류), 문서/데이터 분석, 웹 검색 에이전트, 멀티모달 에이전트
- 각 서비스의 핵심 기능 분석: 대화 관리, Tool 호출, 메모리, 사람-에이전트 핸드오프
- 실제 사용 평가: 프롬프트로 유도한 결과 품질, 응답 지연, 비용, 환각 빈도
- 서비스별 기술 스택 추정: 사용된 LLM 규모, RAG/검색 여부, 에이전트 구조
- 벤치마크: 일반 LLM으로는 해결 못하고 에이전트 구조가 필요한 과제 식별

### 2.2 Agent UX·기능·기술적 한계 분석
- **UX 분석 관점**:
  - 대기 시간 체감(스트리밍 vs blocking), 결과 확신도 표현, 오류·한계 고지
  - 사용자 컨텍스트(대화 히스토리, 파일·화면 공유) 반영
  - 인간 개입(승인 단계) 설계 — 신뢰성과 책임
- **기능 분석 관점**:
  - 도구의 범위와 실패 처리, 멀티턴 대화의 일관성, 장기 기억
  - 사용자 개인화, 시스템 통합(API, DB, 워크플로) 수준
- **기술적 한계 분석 관점**:
  - 환각(Hallucination), 컨텍스트 길이 제한, 비용·지연·확장성
  - 보안/프라이버시(프롬프트 인젝션, 데이터 유출, RBAC)
  - 가드레일(Guardrails)과 정책(Policy) 적용 실패 사례
- **해결 방안 요약**: RAG로 신뢰도 보강, 멀티 에이전트 분업, 사람-인루프(HITL), 평가 자동화

### 2.3 LLM 기반 애플리케이션 활용·개발
- 애플리케이션 시나리오 설계: (1) 문서 Q&A, (2) 이메일/보고서 자동화, (3) 코드 분석·리뷰, (4) 데이터 질의(SQL), (5) 멀티모달 문서 분석
- 구현 파이프라인: 프롬프트 설계 → RAG 구축 → Tool 연동 → LLM 응답 → UI(Streamlit/FastAPI)
- 성능/품질 검증: 자동 평가셋, human feedback 루프, 실패 케이스 카탈로그
- 운영: 로깅(OpenTelemetry), 모니터링(지연/오류/비용), 롤백 전략
- NVIDIA 스택 활용: **AI Blueprints**(멀티모달 RAG, 디지털 휴먼), **NeMo Guardrails**, **NIM** 배포, **Agent Intelligence Toolkit**

## 3. Hands-On 실습
1. 공개 AI 에이전트 서비스 3종 비교 분석 리포트 작성 (동작·UX·한계·해법)
2. 문서 자동화 에이전트: 여러 PDF/엑셀을 읽고 요약·보고서 생성 (RAG + Tool)
3. 툴-연동 워크플로 에이전트: 사용자가 파일을 올리면 분류→분석→요약→이메일 초안까지 한 번에 (LangGraph)
4. 사람-인루프: 생성 결과를 사람이 승인해야 전송하는 에이전트 구현
5. 가드레일 적용: 민감정보 차단·주제 이탈 방지를 NeMo Guardrails 또는 프롬프트 규칙으로 구현
6. Streamlit/FastAPI로 웹 앱 배포 및 데모 (NVIDIA Brev 인스턴스에서)

## 4. 개발 환경 및 하드웨어 준비사항
| 구성 | 권장 사항 |
|------|-----------|
| Python | 3.10 ~ 3.12 |
| 프레임워크 | langchain, langgraph, crewai(선택), streamlit, fastapi, uvicorn |
| LLM | build.nvidia.com NIM API(무료) 또는 로컬 NIM — GPU가 있다면 로컬 배포 경험 권장 |
| 벡터DB | FAISS / Milvus / Chroma |
| 모니터링 | OpenTelemetry, LangSmith(선택), Prometheus/Grafana(선택) |
| GPU | API기반 실습은 불요. 로컬 추론/배포 실습 시 VRAM 16GB+ 권장 |
| 배포 | NVIDIA Brev(L40S), Docker + NGC NIM 컨테이너 |

## 5. NVIDIA 공식 연계 리소스
| 리소스 | 내용 | 링크 |
|--------|------|------|
| NVIDIA AI Blueprints | 레퍼런스 에이전트 앱 (RAG, 멀티모달 등) | https://github.com/NVIDIA-AI-Blueprints |
| build.nvidia.com/blueprints | 블루프린트 원클릭 배포 | https://build.nvidia.com/blueprints |
| NeMo Guardrails | LLM 애플리케이션 보안 가드레일 | https://github.com/NVIDIA/NeMo-Guardrails |
| Agent Intelligence Toolkit | NIM 기반 에이전트 라이브러리 | https://developer.nvidia.com/agent-intelligence-toolkit |
| NIM 마이크로서비스 | 모델 추론 서비스 | https://www.nvidia.com/en-us/ai-data-science/products/nim-microservices/ |
| NVIDIA NeMo | 에이전트 수명주기 관리·커스터마이징 | https://www.nvidia.com/en-us/ai-data-science/products/nemo/ |

## 6. 참고 자료
- NVIDIA Agentic AI 소개: https://www.nvidia.com/en-us/solutions/ai/agentic-ai/
- LangGraph 멀티에이전트 가이드: https://langchain-ai.github.io/langgraph/
- ReAct/CoT 논문 및 개념 자료
- VectorDB 비교: Milvus, FAISS, Chroma