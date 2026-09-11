# 05. 생성형 AI & LLM 응용

> 생성형 AI·Transformer·LLM 구조 | LLM 기반 Agent Harness 설계 | Tool·Memory 연계 및 에이전트 실행 구조

## 1. 학습 목표
- Transformer 아키텍처(어텐션, Self-Attention, Multi-Head Attention)와 LLM 학습 파이프라인을 이해한다.
- 생성형 AI의 종류(LLM, Diffusion, VLM)와 활용 사례를 이해한다.
- 프롬프트 엔지니어링 기법을 익히고 LLM 애플리케이션을 개발한다.
- 프레임워크(LangChain, LangGraph, LlamaIndex 등)로 LLM 워크플로우를 구성한다.
- **Agent Harness**(에이전트 실행 구조)와 **Tool/Memory** 연계 원리를 이해하고 직접 설계한다.
- NVIDIA의 LLM 생태계(NIM, NeMo, AI Blueprints, Nemotron 모델)를 활용한다.

## 2. 교육 내용 (주요 주제)

### 2.1 Transformer와 LLM 구조
- Transformer 전체 구조: Encoder/Decoder, Positional Encoding
- Attention 메커니즘: Query/Key/Value, Scaled Dot-Product Attention, Multi-Head Attention
- LLM 계열: GPT 계열(Decoder-only), BERT(Encoder-only), T5(Encoder-Decoder)
- 핵심 개념: Tokenizer(BPE), Embedding, Context Window, Temperature/Top-p/Top-k
- 학습 단계: Pre-training(사전학습) → SFT(지도 미세조정) → RLHF/DPO → Inference
- 모델 배포 개념: KV-Cache, 양자화(GPTQ/AWQ/FP16/INT8), Inference 서버(vLLM, SGLang, TensorRT-LLM)

### 2.2 생성형 AI 응용
- 텍스트 생성, 요약, 번역, 코드 생성
- RAG(Retrieval-Augmented Generation): 문서 임베딩→벡터DB→검색→생성 파이프라인
  - 임베딩 모델, 벡터 데이터베이스(Milvus, FAISS), 청킹 전략, 리랭킹
- 순수 LLM 대비 RAG의 장점: 최신 지식 반영, 환각 감소, 출처 검증
- 프롬프트 엔지니어링: Few-shot, CoT(Chain-of-Thought), ReAct, 시스템 프롬프트 설계, FMES(Function calling)

### 2.3 LLM 기반 Agent Harness 설계
- **Agent 란?**: LLM이 추론(Reasoning)하고 도구(Tool)를 호출해 행동(Action)하는 루프
- **Agent Harness 구조 (핵심 학습 포인트)**:
  1. **LLM Orchestrator/Core**: 에이전트의 두뇌 — 계획 수립, 하위 태스크 분해
  2. **Tool Registry**: 함수·API·SDK를 LLM이 호출 가능한 형태로 노출 (Function Calling)
  3. **Memory System**: Short-term(대화 컨텍스트) + Long-term(문서/벡터DB)
  4. **Executor/Loop**: 행동 실행과 결과 피드백 반복 (ReAct, Plan-and-Execute, Reflexion)
- 에이전트 런타임: LangGraph, CrewAI, AutoGen, NVIDIA Agent Intelligence Toolkit
- 함수 호출(Function/Tool Calling) 실습: LLM이 계산기, DB 질의, API 호출을 스스로 선택
- 에이전트 평가: 정확도·지연시간·비용·환각 모니터링

### 2.4 NVIDIA LLM/생성형 AI 생태계
- **Nemotron 모델군 (NVIDIA 자체 LLM)**: LLaMA/Mistral은 물론 Nemotron 계열도 탐색
- **NVIDIA NIM (NVIDIA Inference Microservice)**: 사전 최적화 추론 컨테이너 — 5분 배포, OpenAI 호환 API
- **NVIDIA AI Blueprints**: RAG, 멀티모달 RAG, 디지털 휴먼 등 레퍼런스 구현
- **NVIDIA NeMo**: 모델 커스터마이징(파인튜닝)·가드레일(Guardrails)·평가 도구
- **build.nvidia.com**: 무료 NIM API로 즉시 시작 (Llama, Nemotron, DeepSeek, Phi 등)
- **Agent Intelligence Toolkit**: NIM을 결합한 에이전트 빌딩 라이브러리
- AI Workbench / NGC: 로컬-클라우드 일관된 개발 환경

## 3. Hands-On 실습
1. Hugging Face `transformers`로 GPT형 소형 모델 로드 및 생성 실습 (temperature/top_p 조작)
2. LangChain을 이용한 문서 기반 RAG 챗봇 구축 (PDF/웹 문서 + FAISS + LLM)
3. Function Calling으로 Tool 사용 에이전트 구현 (예: 날씨 API, 계산기, 데이터 조회)
4. LangGraph로 Stateful 멀티스텝 에이전트 루프 설계 (ReAct 패턴)
5. build.nvidia.com NIM API 또는 NVIDIA AI Blueprint(멀티모달 RAG)로 배포 실습

## 4. 개발 환경 및 하드웨어 준비사항

### 4.1 소프트웨어 환경
| 구성 | 권장 사항 |
|------|-----------|
| Python | 3.10 ~ 3.12 |
| 라이브러리 | transformers, langchain, langgraph, langchain-community, faiss-cpu, milvus(선택), pymupdf, openai |
| LLM 접근 방식 | (A) build.nvidia.com 무료 API — GPU 불필요 / (B) 로컬 NIM/모델 — GPU 필요 |
| 벡터DB | FAISS(입문), Milvus(운영), Chroma/Qdrant(경량) |
| 실행 환경 | VS Code + Jupyter, Streamlit/FastAPI로 앱화 |

### 4.2 하드웨어
| 추론 방식 | 요구 사항 |
|-----------|-----------|
| API 기반 (NIM API 등) | GPU 불요 — 브라우저/CPU만으로 전 과정 실습 가능 |
| 로컬 7~8B 모델 추론 | VRAM 8~16GB (RTX 3060~4080) 또는 4bit 양자화 + Ram 강조 |
| 로컬 70B+ 또는 파인튜닝 | VRAM 24GB+ (RTX 4090) 또는 클라우드(A100/H100) |
| 클라우드 추천 | NVIDIA Brev (L40S), DGX Cloud, NGC 컨테이너 |

## 5. NVIDIA 공식 연계 리소스
| 리소스 | 내용 | 링크 |
|--------|------|------|
| NVIDIA AI Blueprints | RAG·멀티모달 등 레퍼런스 템플릿 | https://github.com/NVIDIA-AI-Blueprints |
| build.nvidia.com | 무료 NIM 모델 API 대시보드 | https://build.nvidia.com |
| NIM 개요 | GPU 추론 마이크로서비스 | https://www.nvidia.com/en-us/ai-data-science/products/nim-microservices/ |
| NVIDIA Agent Intelligence Toolkit | 에이전트 구축 툴킷 | https://developer.nvidia.com/agent-intelligence-toolkit |
| NGC LLM 모델 | 사전 최적화 모델 | https://catalog.ngc.nvidia.com/models |
| DLI: Building RAG Agents with LLMs | NCP-GENL 대비 RAG 에이전트 과정 (8h, $90) | https://learn.nvidia.com |

## 6. 참고 자료
- OpenAI Function Calling / 개발 가이드 (개념 참고)
- LangChain 공식 문서: https://python.langchain.com/
- LangGraph 공식 문서: https://langchain-ai.github.io/langgraph/
- Hugging Face Transformers: https://huggingface.co/docs/transformers
- NVIDIA Generative AI Learning Path: https://www.nvidia.com/en-us/learn/learning-path