# 11. NVIDIA DLI 6 | OpenUSD 디지털 트윈

> USD Stage·Composition Arc·디지털 트윈 자산 구조화 | Omniverse 연동·씬 그래프(Scene Graph) 설계 | OpenUSD 인증 시험 대비

## 1. 학습 목표
- USD(Universal Scene Description)의 Stage·Prim·Attribute·Layer 개념을 이해한다.
- Composition Arc(리파인·서브레이어·볼드 등)를 활용한 자산 구조화를 할 수 있다.
- 디지털 트윈·물리 AI 자산을 Omniverse와 연동할 때의 씬 그래프 설계 원리를 익힌다.
- NVIDIA OpenUSD 개발 인증(NCP-OUSD 기초 수준) 대비 학습을 시작한다.

## 2. 교육 내용 (주요 주제)

### 2.1 USD 기초 (Stage·Prim·Attribute)
- USD란: 3D 씬 기술·합성·공유 개방형 프레임워크 (Pixar → NVIDIA Omniverse 코어)
- Stage/USD(Payload), Prim, Property(Attribute/Relationship), TimeCode
- Layer 스택: 로컬 레이어·서브레이어, 토닝(강도순위: local > sublayer > reference...)
- Python API: `Usd.Stage`, `UsdGeom.Mesh`, `Usd.Prim`, 속성 값 읽기·쓰기
- USD 뷰어: `usdview`, Omniverse Kit, umdf(DCC)

### 2.2 Composition Arc와 자산 구조화
- 주요 Composition Arc: **reference, payload, sublayer, variant set, instancing**
- 예: 기본 로봇 모델을 reference로 공유 → 시나리오별 variant(팔 유무·색상)로 치환
- 자산 구조 원칙: 한 자산 = 하나의 디렉터리(usda + texture), 명명 규칙, 레이어 분리(모델/애니메이션/재질)
- 디버깅: `usdview --diff`, ARC 강도의 곤란 사례(복합) 연습

### 2.3 디지털 트윈·씬 그래프 설계
- 디지털 트윈 정의: 물리 자산의 실시간 가상 카피 — **단일 소스 트루스(Single Source of Truth)**
- 씬 그래프 설계: 부품극품(학습용 공장 라인)→센서→로봇→프로세스 정보를 USD 계층으로
- Omniverse 연동: USD를 공용 시맨틱으로 하는 마이크로서비스(넴버타/데이터 브릿지)
- Isaac Sim 연계: 로봇 USD 씬은 바로 Isaac Lab/Omniverse Replicator로 재사용
- 물리 AI 시대의 USD: OpenUSD를 물리·센서·동작 정보까지 확장(AOUSD 규격)

### 2.4 OpenUSD 인증 시험 대비 (NCP-OUSD)
- 자격: NVIDIA-Certified Professional: OpenUSD Development (60~70문항, 120분, $200)
- 학습 경로(무료): Learn OpenUSD — ① Stages/Prims/Attributes ② Traversal·ModelKinds ③ Strength Ordering ④ Composition Arcs ⑤ 데이터 교환·벨리데이션 ⑥ Asset Modularity·Instancing
- 출제 영역(요약): Composition(복합 아크) 23%, Data Exchange 15%, Pipeline Development 14%, Customizing USD 6% 기타
- 로드맵: 본 챕터에서 기본 개념(2.1~2.2) → 심화 과정 적용실습 후 12주 내 시험 응시

## 3. Hands-On 실습
1. Python으로 USD Stage 생성: 큐브 3개 + Transform + 재질 속성 (usda 파일로 저장·열람)
2. reference/payload/variant 실습: 로봇 자산의 버전별 variant 전환
3. 레이어 분리 연습: "모델.usda"(구조) + "재질.usda"(표면) + stage로 합성
4. usdview/Omniverse에서 디버깅 (strong-order 우선순위 확인)
5. 마이크로 디지털 트윈: 간단한 라인 씬(컨베이어+팔 파지 반복) USD로 구조화 → Isaac Sim에서 열기
6. Learn OpenUSD 인증용 코스 1~7 이수 (무료)

## 4. 환경 및 하드웨어 준비사항
| 항목 | 권장 사항 |
|------|-----------|
| Python | 3.10+ / USD Python 바인딩(`pxr`) 또는 usd-core pip |
| USD 도구 | USD 바이너리(distutils 빌드 포함), usdview, usdcat |
| Omniverse | Omniverse Kit 프로그램 또는 Isaac Sim 내 USD 코어 |
| GPU | USD 학습 자체는 CPU 가능. Omniverse 렌더·물리 사용 시 GPU(RTX 4080 권장) |
| 클라우드 | Brev(Isaac USD 환경), 시험 응시는 노트북+카메라 |
| 자격시험 비용 | $200 — 응시 전 블루프린트·스터디가이드 확인 |

## 5. NVIDIA 공식 연계 리소스
- Learn OpenUSD(무료 학습경로): https://developer.nvidia.com/openusd
- OpenUSD 개발 인증: https://www.nvidia.com/en-us/learn/certification/openusd-development-professional
- NVIDIA OpenUSD 문서: https://docs.omniverse.nvidia.com/usd/latest/index.html
- AOUSD(Alliance for OpenUSD): https://aousd.org
- OpenUSD pip(PyPI usd-core): https://pypi.org/project/usd-core/

## 6. 참고 자료
- OpenUSD 공식 문서: https://openusd.org
- USD 101 스터디: Pixar "USD Course"
- 디지털 트윈 산업 사례: NVIDIA Omniverse Digital Twin 블로그/화이트페이지