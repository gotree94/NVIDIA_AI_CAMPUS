# 04. LLM·RAG | 생성형 AI 서비스 개발

> LLM·RAG 개념과 생성형 AI 서비스 개발 | 로봇 운영·관리·사용자 인터페이스에 접목할 수 있는 LLM 기술

## 1. 학습 목표
- LLM의 구조·학습·추론과 RAG 파이프라인을 이해한다.
- 실제 문서 기반 RAG 서비스를 구축해 생성형 AI 서비스 개발 사이클을 경험한다.
- 로봇 시스템(사용자 대화, 작업 지시 분석, 문서화)에 LLM을 결합하는 설계를 할 수 있다.

## 2. 교육 내용 (주요 주제)

### 2.1 LLM 기초
- Transformer·Self-Attention·Decoder-only 구조, Tokenizer, Context Window
- 프롬프트 엔지니어링: 시스템 프롬프트, Few-shot, CoT, Tool Calling
- 모델 종류: 소형(3B~8B) vs 대형(70B+), 양자화(GPTQ/AWQ/4bit)
- GPU 추론: vLLM/SGLang/TensorRT-LLM 서버 개념, 토큰/초 성능
- (참고: 본 로봇과정은 경량 LLM을 종종 에지에서 사용 — Jetson에서 소형 LLM 실행)

### 2.2 RAG(Retrieval-Augmented Generation)
- 파이프라인: 문서 로드 → 청킹 → 임베딩 벡터화 → 벡터DB 색인 → 검색(유사도/하이브리드) → LLM 생성
- 벡터DB: FAISS(입문), Milvus, Chroma, Qdrant
- 고급: 하이브리드 검색(BM25+벡터), 리랭커, 메타데이터 필터링, chunk overlap 전략
- 평가: RAGAS / 정확도·재현율·환각 지표, 쿼리 유형별 실패 분석
- **로봇 연계 사례**: 로봇 운영 메뉴얼·안전 규정 RAG → "이 동작 가능?" 질의응답, 스케줄·수리 이력 검색

### 2.3 생성형 AI 서비스 개발 (RAG 앱)
- LLM 프레임워크: LangChain, LangGraph, LlamaIndex
- API: OpenAI 호환 API, **NVIDIA NIM**(컨테이너 추론 API), build.nvidia.com 무료 API
- 앱 계층: FastAPI 백엔드 + Streamlit UI, 스트리밍(SSE), 로깅·평가 자동화
- 이미지/PDF/음성 포함 멀티모달 RAG (NVIDIA AI Blueprint 멀티모달 RAG 예제)
- 안전: 가드레일(NVIDIA NeMo Guardrails)·프롬프트 인젝션 대응

## 3. Hands-On 실습
1. LangChain으로 PDF 2~3개를 넣어 RAG 챗봇 구축 (FAISS + NIM/로컬 LLM)
2. 하이브리드 검색·리랭커를 적용해 검색 품질 개선 및 RAG 지표 측정
3. Streamlit + FastAPI로 문서 Q&A 웹 서비스 배포
4. 멀티모달 RAG Blueprint(NVIDIA) 데모 실행
5. (연계) 소형 LLM을 Jetson에서 실행해 로컬 챗봇/요약 서비스 테스트

## 4. 환경 및 하드웨어 준비사항
| 항목 | 권장 사항 |
|------|-----------|
| Python | 3.10~3.12 |
| 라이브러리 | langchain, langchain-community, faiss-cpu, chromadb, pymupdf, streamlit, fastapi, openai |
| LLM 접근 | build.nvidia.com(NIM API, 무료) 또는 로컬 소형 모델 — GPU 16GB 이상 |
| 벡터DB | Chroma(경량) → Milvus(확장) |
| 실행 환경 | WSL2 Ubuntu 또는 NVIDIA Brev(Jupyter) |
| GPU(선택) | RTX 3060 이상이면 로컬 소형 LLM(Llama 3.1 8B 4bit 등) 가능 |

## 5. NVIDIA 공식 연계 리소스
- build.nvidia.com — 무료 NIM API 대시보드
- NVIDIA AI Blueprints(RAG, 멀티모달 RAG): https://github.com/NVIDIA-AI-Blueprints
- NeMo Guardrails: https://github.com/NVIDIA/NeMo-Guardrails
- DLI: Building RAG Agents with LLMs (8h, $90): https://learn.nvidia.com
- NIM 마이크로서비스: https://www.nvidia.com/en-us/ai-data-science/products/nim-microservices/

## 6. 참고 자료
- LangChain: https://python.langchain.com/
- LangGraph: https://langchain-ai.github.io/langgraph/
- RAGAS: https://docs.ragas.io/
- NVIDIA Robotics + 절차 문서화 사례(블로그/유튜브 GTC)