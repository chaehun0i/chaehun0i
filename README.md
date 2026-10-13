
# 이채훈 | Lee Chae-hun
**AI Backend Developer · AI Agent / RAG Developer**
업무 데이터에 **RAG와 AI Agent**를 연결하고,  
LLM 결과를 **API · Database · 업무 Workflow**로 구현하는 AI Backend 개발자입니다.
단순히 LLM API를 호출하는 것보다 다음 경계를 설계하는 데 집중합니다.
- **Agentic Workflow** — LangGraph 기반 상태 관리, 승인·중단·재시작, Feedback/Ranking 흐름
- **Tool Calling & MCP** — LangChain Tool Calling, MCP Read Tools, 실행 전 권한·의존성 재검증
- **RAG & Retrieval** — PostgreSQL FTS + pgvector + RRF 기반 Hybrid Retrieval과 Evidence 전달
- **Deterministic Boundary** — 금액·수량·판정 등 재현성이 필요한 값은 코드/Rule이 소유
- **Evaluation & Serving** — Golden case, 회귀 테스트, 5-fold × 3 seed, PyTorch, Docker/CI
---
## Tech Stack
### AI / Agent
`LangGraph` `LangChain Tool Calling` `MCP` `RAG` `LLM Gateway` `Structured Output`
### Retrieval / Data
`PostgreSQL` `pgvector` `FTS` `RRF` `Embedding` `OCR` `SQL`
### Backend
`Python` `FastAPI` `Pydantic` `REST API` `WebSocket` `Background Tasks`
### ML / Evaluation
`PyTorch` `KoELECTRA` `5-fold Cross Validation` `pytest` `Golden Evaluation`
### Infra / Dev
`Docker` `Docker Compose` `Git` `Linux` `GitHub Actions` `Nginx`
### Frontend
`TypeScript` `React` `Vite`
---
# Selected Projects
## 01. ServIQ — F&B 운영 문제 조사 Agent
> 고객 의견과 운영 자료를 조사해 **근거 기반 원인·개선안**을 제시하고 사람이 검토하는 AI Agent 서비스
**Personal Project · LangGraph · LangChain · MCP · RAG · FastAPI · PostgreSQL/pgvector**
Repository: https://github.com/chaehun0i/fnb-voc-intelligence
### What I built
- `LangGraph` checkpoint / interrupt-resume 기반 **승인 대기·중단·재시작 Workflow**
- `LangChain` Node Runtime + 공식 `MCP` SDK 기반 **4개 Read Tool** 연결
- Tool 실행 직전 Tenant / Role / Capability / Budget / Control을 다시 확인하는 **Harness 경계**
- PostgreSQL FTS + pgvector + RRF 기반 **Hybrid Retrieval**
- Evidence → RCA/CAPA → Human Approval → Verification 흐름 연결
- Evidence가 부족하거나 새 근거가 없으면 추정을 계속하지 않고 **bounded stop / fail-closed**
### Validation
- Python tests: **793 passed**
- Frontend: **198 passed**
- PostgreSQL smoke: **14 passed**
- 대표 업무 경로: **6 cases**
> 현재 로컬 Docker + Sample Data 기준이며 실제 POS/ERP 외부 Write는 연결하지 않았습니다.
---
## 02. 햇들농산 — 농산물 매입·판매 Multi-Agent
> 가격·재고·자금 정보를 바탕으로 판매 후보를 만들고 재무·물류 검증을 거쳐 추천안을 제공하는 업무 의사결정 Agent 서비스
**5-person Team · Finance Agent · Sales Agent · LangGraph · LangChain Tool Calling · Harness · PostgreSQL**
Repository: https://github.com/nobadai/mainproject
### My Role
**Finance Agent/Harness · Sales Agent/LangGraph · Logistics 초기 Runtime**을 설계·구현했습니다.
### Sales Agent
```text
Context
  ↓
Candidate Generation
  ↓
Validation Plan
  ↓
Feedback
  ↓
Evaluation / Ranking
  ↓
Self-check
  ↓
Recommendation

* LangGraph로 판매 후보 생성 → 검증 → Feedback → 평가·Ranking → Self-check 흐름 구성
* LLM은 전략 자세 선택과 설명에 참여
* 가격·수량·금액·추천 ID는 deterministic code가 계산
* Finance Verdict는 Sales가 재판정하지 않고 검증 결과를 보존

Finance Agent / Harness

* LangChain Tool Calling을 사용하되 Tool Call 자체를 실행 권한으로 취급하지 않음
* Harness에서 Capability / Dependency / Permission / Budget / Duplicate를 재검사
* 현금흐름·채권·여신·금액·Verdict는 deterministic Tool/Rule이 계산

Problem Solving Evidence

* 판매 실행 9,937건 분석 → 후보 생성 전 Finance Context 0건 확인
* PRE_SALES_FACTS 선행 전달로 Agent 간 Data Contract와 실행 순서 재설계
* 실행 가능한 Tool이 0~1개인 단계는 결정론적으로 처리해 Finance Tool Planner 호출 9 → 3 (-66.7%)
* Sales regression: 388 passed (PR #673 기준)

⸻

03. WITH ESG — ESG 보고서 생성 서비스

보고서·기사·설문 데이터를 확보·정제하고 RAG를 통해 근거 기반 ESG 보고서 초안을 생성하는 서비스

4-person Team · Data Engineering · OCR · pgvector · RAG · LangChain · FastAPI

Repository: https://github.com/shell-files/dev_skm

My Role

* 3개년 Sustainability Report 공동 OCR / PDF Parsing
* ESG 기사 데이터 처리·Embedding·Vectorization
* 설문 URL 생성·응답 Import
* PostgreSQL + pgvector 기반 관련 문단 검색
* 검색 Evidence를 Context로 전달하는 LangChain 기반 RAG 문단 생성
* AI 생성 문단 DB 저장 및 보고서 Template 연결

Data / RAG Flow

Reports / Articles / Survey
          ↓
OCR / Parsing / Import
          ↓
Cleaning / Structuring
          ↓
Embedding / pgvector
          ↓
RAG Context + Source + Numeric Data
          ↓
LLM Paragraph
          ↓
Report Draft

Engineering Decisions

* 정량 데이터와 LLM 생성 문장을 분리해 Text / Number 책임 경계 유지
* 원문 출처를 생성 Context와 연결해 결과를 대조할 수 있도록 구성
* PDF 추출을 최대 3개 작업 병렬 처리로 변경하고 공통 이슈 체계로 매핑

⸻

04. 금융안심이 — 보이스피싱 분석 서비스

위험 표현, 대화 순서, 문맥 분류를 결합해 보이스피싱 위험도와 판단 근거를 제공하는 분석 서비스

5-person Team · PyTorch · KoELECTRA · FastAPI · PostgreSQL · Docker

Repository: https://github.com/nobadai/miniproject

ML / Evaluation

* 공개 녹취 기반 피싱 23 + 정상 23 평가 데이터 구성
* 긴 통화를 Chunking하고 KoELECTRA 이진 분류를 CUDA 환경에서 학습·평가
* Rule + Sequence + KoELECTRA 세 신호를 결합해 위험 점수와 판단 근거 생성
* 5-fold × 3 seed 반복 평가로 단일 split 결과에 의존하지 않도록 검증

Serving / Docker

* CPU-only PyTorch 환경으로 Serving 구조 전환
* CUDA / Triton 의존성 제거
* BuildKit cache mount와 .dockerignore 정리
* Docker image: 22.5GB → 2.87GB
* uv dependency layer: 약 14GB → 약 1.56GB

Docker 수치는 배포 이미지 용량 최적화 결과이며 추론 성능 향상 수치가 아닙니다.

⸻

How I Design AI Services

1. Agent Workflow

AI Agent를 단일 LLM 호출이 아니라 상태·검증·중단·재시작이 있는 업무 Workflow로 설계합니다.

2. Deterministic Core

금액·수량·상태·Verdict처럼 재현성과 정확성이 필요한 값은 일반 코드와 Rule이 계산합니다.

3. Tool Execution Boundary

LLM의 Tool Call을 바로 실행하지 않고 권한·의존성·예산·중복·현재 상태를 실행 경계에서 다시 확인합니다.

4. Evidence-grounded RAG

검색 결과뿐 아니라 Source / Provenance / Numeric Data를 함께 전달해 AI 결과를 추적할 수 있도록 합니다.

5. Evaluation

Agent 실행 경로는 회귀 테스트와 Golden case로, ML 결과는 반복 평가로 검증합니다.

6. Fail-Closed

필수 데이터나 정책이 없을 때 임의의 값을 생성하기보다 멈추고 부족한 정보를 명시하는 구조를 선호합니다.

⸻

Current Focus

Agentic Workflow · LangGraph · LangChain Tool Calling · MCP
RAG · Hybrid Retrieval · PostgreSQL/pgvector
FastAPI · AI Evaluation · PyTorch · Docker · Git · Linux

⸻

Education & Award

* 심화 생성형 AI 활용 인재양성과정 — AI Agent · FastAPI/React · RAG (2026.07–09)
* 삼정 ESG 데이터 활용 AX Academy with AI Agent (2025.12–2026.06)
* 삼정 ESG AX Academy with AI Agent · 개인 부문 최우수상
* 한국관광대학교 외식경영학과 졸업 (2024.02)

⸻

Contact

* Email: jt33_@naver.com
* GitHub: https://github.com/chaehun0i

⸻

업무 데이터와 규칙 위에서 AI가 안전하게 판단하고, 검증 가능한 결과를 서비스로 연결하는 Backend를 만들고 있습니다.

