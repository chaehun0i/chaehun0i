# 이채훈 | Lee Chae-hun

**AI Backend Developer · AI Agent / RAG Developer**

업무 데이터를 AI가 활용할 수 있는 형태로 정리하고,  
RAG와 AI Agent의 결과를 API·DB·업무 흐름으로 연결하는 백엔드 개발자입니다.

LLM을 단순히 호출하는 기능보다 데이터 수집과 검색, Agent Workflow, Tool 실행 조건, 결과 검증까지 하나의 서비스 흐름으로 구현하는 데 관심이 있습니다.

현재는 **LangGraph 기반 Agentic Workflow, RAG, Tool Calling/MCP, FastAPI 기반 AI 서비스 개발**을 중심으로 경험을 쌓고 있습니다.

---

## Tech Stack

**AI / Agent**  
`LangGraph` `LangChain` `Tool Calling` `MCP` `RAG` `LLM Gateway`

**Retrieval / Data**  
`PostgreSQL` `pgvector` `FTS` `RRF` `Embedding` `OCR` `SQL`

**Backend**  
`Python` `FastAPI` `Pydantic` `REST API` `WebSocket` `Background Tasks`

**ML / Evaluation**  
`PyTorch` `KoELECTRA` `Cross Validation` `pytest` `Golden Evaluation`

**Infra / Development**  
`Docker` `Docker Compose` `Git` `Linux` `GitHub Actions` `Nginx`

**Frontend**  
`TypeScript` `React` `Vite`

---

## Selected Projects

### ServIQ — F&B 운영 문제 조사 Agent

고객 의견과 매장 운영 자료를 검색해 원인과 개선안을 제안하고,  
사람이 근거를 확인한 뒤 승인할 수 있도록 만든 개인 프로젝트입니다.

**Personal Project · LangGraph · LangChain · MCP · RAG · FastAPI · PostgreSQL/pgvector**

[Repository](https://github.com/chaehun0i/fnb-voc-intelligence)

- LangGraph checkpoint와 interrupt/resume을 이용해 승인 대기, 중단, 재시작이 가능한 조사 흐름을 구현했습니다.
- PostgreSQL FTS와 pgvector 검색 결과를 RRF로 결합해 Hybrid Retrieval을 구성했습니다.
- LangChain 처리 단계와 공식 MCP SDK 기반 Read Tool을 연결했습니다.
- Tool 실행 직전에 권한, capability, budget, 현재 상태 등을 다시 확인하는 Harness를 구현했습니다.
- 근거가 부족하거나 새로운 자료가 없을 때 추가 추론을 중단하도록 실행 조건을 제한했습니다.

**Validation**
- Python: **793 passed**
- Frontend: **198 passed**
- PostgreSQL smoke test: **14 passed**
- 대표 업무 경로: **6 cases**

현재 로컬 Docker와 Sample Data를 기준으로 검증했으며 실제 POS/ERP 외부 Write 기능은 연결하지 않았습니다.

---

### 햇들농산 — 농산물 매입·판매 Multi-Agent

가격, 재고, 자금 정보를 이용해 판매 후보를 만들고  
재무·물류 조건을 검증해 추천안을 제공하는 팀 프로젝트입니다.

**5-person Team · LangGraph · LangChain Tool Calling · Harness · PostgreSQL**

[Repository](https://github.com/nobadai/mainproject)

**담당**
- Finance Agent / Harness
- Sales Agent / LangGraph
- Logistics 초기 Runtime

Sales Agent는 다음 흐름을 LangGraph 상태 기반으로 연결했습니다.

`Context → Candidate Generation → Validation → Feedback → Evaluation / Ranking → Self-check → Recommendation`

- LLM은 전략 방향 선택과 설명에 사용하고, 가격·수량·금액·추천 ID는 코드에서 계산했습니다.
- Finance의 금액·현금흐름·한도·Verdict 역시 Tool/Rule 기반 계산 결과를 사용했습니다.
- 판매 실행 **9,937건**을 분석해 후보 생성 이전 Finance Context가 **0건** 전달되던 문제를 확인했습니다.
- `PRE_SALES_FACTS`를 선행 전달하도록 Agent 간 데이터 계약과 실행 순서를 수정했습니다.
- 실행 가능한 Finance Tool이 0~1개일 때는 코드에서 처리하도록 변경해 Planner 호출을 **9회 → 3회(-66.7%)**로 줄였습니다.
- Sales Agent 경계 정리 기준 회귀 테스트 **388 passed**를 확인했습니다.

---

### WITH ESG — ESG 보고서 생성 서비스

지속가능경영보고서, 기사, 설문 데이터를 정리하고  
RAG를 이용해 ESG 보고서 초안 생성에 연결한 팀 프로젝트입니다.

**4-person Team · Data Engineering · OCR · pgvector · RAG · LangChain · FastAPI**

[Repository](https://github.com/shell-files/dev_skm)

**담당**
- 3개년 Sustainability Report 공동 OCR / PDF Parsing
- ESG 기사 Embedding 및 Vectorization
- 설문 URL 생성과 응답 Import
- PostgreSQL + pgvector 기반 관련 문단 검색
- 검색 결과를 Context로 전달하는 RAG 문단 생성
- AI 생성 문단 DB 저장 및 보고서 Template 연결

보고서에 사용되는 실제 수치와 LLM이 생성한 설명 문장을 구분해 저장하고,  
검색한 원문 출처를 함께 연결해 결과를 다시 확인할 수 있도록 구성했습니다.

PDF 추출 과정은 최대 3개 작업을 병렬로 처리하도록 개선하고, 추출 결과를 공통 ESG 이슈 체계로 정리했습니다.

---

### 금융안심이 — 보이스피싱 분석 서비스

통화의 위험 표현, 대화 흐름, 문맥 분류 결과를 결합해  
보이스피싱 위험도와 판단 근거를 제공하는 팀 프로젝트입니다.

**5-person Team · PyTorch · KoELECTRA · FastAPI · PostgreSQL · Docker**

[Repository](https://github.com/nobadai/miniproject)

- 공개 녹취를 바탕으로 피싱 23건, 정상 23건의 평가 데이터를 구성했습니다.
- 긴 통화를 Chunk 단위로 나누고 KoELECTRA 이진 분류 모델을 CUDA 환경에서 학습·평가했습니다.
- Rule, Sequence, KoELECTRA 세 신호를 결합해 위험 점수와 판단 근거를 생성했습니다.
- `5-fold × 3 seed` 반복 평가를 사용해 단일 데이터 분할 결과에만 의존하지 않도록 검증했습니다.
- 학습 이후 Serving 환경은 CPU-only PyTorch 기준으로 구성했습니다.
- CUDA/Triton 의존성과 빌드 캐시를 정리해 Docker 이미지를 **22.5GB → 2.87GB**로 줄였습니다.

Docker 수치는 이미지 용량 최적화 결과이며 추론 속도 개선 수치는 아닙니다.

---

## What I Focus On

제가 AI 서비스를 구현할 때 중요하게 보는 부분은 다음과 같습니다.

**업무 흐름 안에서 동작하는 Agent**  
Agent를 한 번의 LLM 호출로 끝내지 않고 상태 저장, 승인, 재시작, 검증이 필요한 업무 흐름으로 구성하려고 합니다.

**LLM과 일반 코드의 역할 분리**  
금액, 수량, 상태, 판정처럼 결과가 재현되어야 하는 값은 가능한 한 코드와 Rule에서 계산하고, LLM은 해석과 판단 보조에 사용합니다.

**근거를 확인할 수 있는 RAG**  
검색 결과뿐 아니라 원문 출처와 필요한 정량 데이터를 함께 전달해 결과가 어디에서 나왔는지 확인할 수 있도록 구성합니다.

**검증 가능한 서비스**  
Agent Workflow는 회귀 테스트와 Golden case로, ML 모델은 평가 데이터와 반복 검증으로 확인하고 있습니다.

---

## Education & Award

- **심화 생성형 AI 활용 인재양성과정**  
  AI Agent · FastAPI/React · RAG  
  `2026.07 – 2026.09`

- **삼정 ESG 데이터 활용 AX Academy with AI Agent**  
  ESG 데이터 처리 · AI 보고서 생성  
  `2025.12 – 2026.06`

- **삼정 ESG AX Academy with AI Agent 개인 부문 최우수상**

- **한국관광대학교 외식경영학과 졸업**  
  `2024.02`

---

## Contact

**Email**  
jt33_@naver.com

**GitHub**  
https://github.com/chaehun0i
