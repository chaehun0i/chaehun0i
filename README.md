# 이채훈 | Lee Chae-hun

**Backend Developer · AI Agent / RAG · 업무자동화**

업무 데이터를 AI가 활용할 수 있는 형태로 정리하고, RAG와 AI Agent의 결과를 실제 업무 흐름으로 연결하는 백엔드 개발자입니다.
Python·FastAPI·PostgreSQL을 중심으로 데이터 처리부터 API·DB·화면 연동·Docker 실행 환경까지 구현해 왔습니다.

- **Backend** — 트랜잭션·멱등성·동시성 제어와 업무 상태 관리
- **AI Agent / RAG** — 근거 기반 검색·생성, Human Approval, 하네스 엔지니어링
- **서비스 구현** — 도메인 규칙을 데이터 구조·API·사용자 화면으로 연결

외식경영 전공을 바탕으로 F&B·농산물 유통·ESG·회계 등 다양한 업무 도메인을 다뤘습니다.

[GitHub](https://github.com/chaehun0i) · [Email](mailto:jt33_@naver.com)

---

## Selected Projects

### ServIQ — F&B 운영 문제 조사 Agent

고객 의견과 매장 운영 자료를 검색해 원인과 개선안을 제안하고,  
사람이 근거를 확인한 뒤 승인할 수 있도록 만든 개인 프로젝트입니다.

**개인 프로젝트 · AI Runtime / Backend · 2026.09–현재**

[Repository](https://github.com/chaehun0i/fnb-voc-intelligence)

- **Agent Workflow:** LangGraph 기반 조사·중단·재개·Human Approval 구현
- **검색:** PostgreSQL FTS + pgvector + RRF 기반 Hybrid Retrieval
- **실행 제어:** Tool 권한·실행 한도를 검증하는 Harness와 React 운영 콘솔 연결

<details>
<summary>구현 상세 · 용어 설명 · 검증 기록</summary>

- VOC·Excel/CSV 입력 검증·저장을 검색·조사·승인 흐름으로 연결했습니다.
- LangGraph checkpoint(실행 상태 저장)와 interrupt/resume(검토를 위한 중단·재개)을 이용해 승인 대기, 중단, 재시작이 가능한 조사 흐름을 구현하고 완료 결과를 재사용하도록 구성했습니다.
- PostgreSQL FTS(키워드 검색)와 pgvector(벡터 검색) 결과를 RRF(검색 순위 결합 방식)로 결합해 Hybrid Retrieval을 구성하고 원문 출처를 전달했습니다.
- LangChain 처리 단계와 공식 MCP SDK 기반 Read Tool(외부 데이터를 조회하는 도구)을 연결했습니다.
- Tool 실행 직전에 권한, capability(사용 가능한 기능), budget(실행 자원 한도), 현재 상태 등을 다시 확인하는 Harness(Agent의 실행 조건과 안전장치를 관리하는 계층)를 구현했습니다.
- 근거가 부족하거나 새로운 자료가 없을 때 추가 추론을 중단하도록 실행 조건을 제한하고, React 운영 콘솔에 진행 상태·근거·승인 흐름을 연결했습니다.

**검증 기록:** Python 793 passed · Frontend 198 passed · PostgreSQL smoke 14 passed · 대표 업무 경로 6 cases. 각 수치는 기록 당시 기준입니다.

현재 로컬 Docker와 Sample Data를 기준으로 검증했으며 실제 POS/ERP 외부 Write 기능은 연결하지 않았습니다.

</details>

---

### AI Accounting Office — 회계 업무·Agent 연계 서비스

거래·증빙 입력부터 전표 작성, 독립 승인, Posting, 원장·월마감·재무 조회까지 연결하는 개인 프로젝트입니다.

**개인 프로젝트 · Backend / Database / Agent / 화면 연계 · 2026.10–현재**

[Repository](https://github.com/chaehun0i/ai-accounting-office)

- **회계 Backend:** 거래·전표·승인·Posting·월마감 API와 데이터 모델 구현
- **정합성:** 멱등성·동시성 제어와 승인 후 데이터 변경 검증
- **Agent 연계:** 전표 초안 생성과 승인·장부 반영을 분리하고 Next.js 화면 연결

<details>
<summary>구현 상세 · 용어 설명 · 검증 기록</summary>

- FastAPI·SQLAlchemy·PostgreSQL·Alembic으로 회사별 거래·전표·승인·장부의 데이터 모델과 업무 API를 구현했습니다.
- 멱등성 키, 원천 version, row lock, 승인 대상 digest(승인 시점의 내용을 식별하는 검증값)를 검증해 중복 처리와 stale approval(승인 후 원천 데이터가 바뀐 상태의 승인 적용)을 통제했습니다.
- 독립 PostgreSQL 연결에서 동시 Posting(전표의 장부 반영)의 전표 번호 발급과 동일 전표 중복 Posting 거부를 검증했습니다.
- LangGraph·Tool Registry(Agent가 호출할 Tool의 등록·관리 계층)·Application Service(업무 규칙을 실행하는 서비스 계층)를 연결해 거래 기반 전표 제안, 사람 검토 대기·재개, 기간별 회계 조회를 구성했습니다.
- 전표 제안의 금액은 원천 Transaction(거래 데이터)의 Decimal을 사용하고, Agent의 처리 결과는 DRAFT(검토 전 전표 초안) 생성으로 제한했습니다. 회계 승인·Posting은 별도 업무 명령이 담당합니다.
- Next.js·TypeScript 기반 거래·전표·월마감·AI 조회 화면을 API와 연결하고 회사·권한·출처·처리 상태를 확인할 수 있도록 구성했습니다.

**검증:** PostgreSQL 통합·동시성 테스트와 GitHub Actions의 Backend·Frontend·핵심 회계·스키마 검증을 구성했습니다. 실제 회계 업무 도입 효과나 전체 브라우저 E2E 완료를 주장하지 않습니다.

</details>

---

### 햇들농산 — 농산물 매입·판매 Multi-Agent

가격, 재고, 자금 정보를 이용해 판매 후보를 만들고  
재무·물류 조건을 검증해 추천안을 제공하는 팀 프로젝트입니다.

**5인 팀 · Finance Agent / Harness · Sales Agent / LangGraph · Logistics 초기 Runtime · 2026.08–09**

[Repository](https://github.com/nobadai/mainproject)

- **Multi-Agent:** Finance·Sales 실행 흐름과 Agent 간 데이터 전달 개선
- **문제 해결:** 판매 실행 **9,937건** 분석으로 후보 생성 전 재무 정보 누락 확인·수정
- **최적화:** 동일 조건의 세 모드 합산 Planner 호출 **9회 → 3회**, 업무 결과 동일성 검증

<details>
<summary>구현 상세 · 용어 설명 · 검증 기록</summary>

Sales Agent는 다음 흐름을 LangGraph 상태 기반으로 연결했습니다.

`Context → Candidate Generation → Validation → Feedback → Evaluation / Ranking → Self-check → Recommendation`

> 업무 정보 수집 → 판매 후보 생성 → 조건 검증 → 피드백 반영 → 평가·순위 산정 → 자체 점검 → 최종 추천의 흐름입니다.

- LLM은 전략 방향 선택과 설명에 사용하고, 가격·수량·금액·추천 ID는 코드에서 계산했습니다.
- Finance의 금액·현금흐름·한도·Verdict(재무 조건 충족 여부에 대한 판정) 역시 Tool/Rule 기반 계산 결과를 사용했습니다.
- 판매 실행 **9,937건**을 분석해 후보 생성 이전 Finance Context(판매 후보를 만들 때 필요한 재무 정보)가 **0건** 전달되던 문제를 확인했습니다.
- 후보 생성 전에 재무 정보를 전달하도록 Agent 간 입력 계약과 실행 순서를 수정했습니다.
- 실행 가능한 Finance Tool이 0~1개일 때는 코드에서 처리하도록 변경해, 동일 조건의 세 모드 합산 Finance Tool Planner(요청에 필요한 재무 Tool과 실행 순서를 결정하는 구성요소) 호출을 **9회 → 3회(-66.7%)**로 줄였습니다. Tool 실행·업무 결과·금액·판정·근거의 동일성을 확인했습니다.
- Sales Agent 경계 정리 기준 회귀 테스트 **388 passed**를 확인했습니다. 수치는 해당 검증 시점의 기록입니다.

</details>

---

### WITH ESG — ESG 보고서 생성 서비스

지속가능경영보고서, 기사, 설문 데이터를 정리하고  
RAG를 이용해 ESG 보고서 초안 생성에 연결한 팀 프로젝트입니다.

**4인 팀 · 자료 수집 / OCR / RAG / 보고서 양식 · 2025.12–2026.06**

[공식 팀 저장소](https://github.com/shell-files/dev_skm)

- **데이터 처리:** 3개년 보고서 공동 OCR·PDF Parsing, 기사 Embedding, 설문 연계
- **RAG:** PostgreSQL + pgvector 검색과 근거 기반 보고서 문단 생성
- **보고서 연계:** 실제 수치·생성 문장을 구분해 저장하고 5개 이슈 Template 연결

<details>
<summary>구현 상세 · 용어 설명 · 검증 기록</summary>

**담당**

- 3개년 Sustainability Report 공동 OCR / PDF Parsing
- ESG 기사 Embedding 및 Vectorization
- 설문 URL 생성과 응답 Import
- PostgreSQL + pgvector 기반 관련 문단 검색
- 검색 결과를 Context로 전달하는 RAG 문단 생성
- AI 생성 문단 DB 저장 및 5개 이슈 보고서 Template 연결

보고서에 사용되는 실제 수치와 LLM이 생성한 설명 문장을 구분해 저장하고,  
검색한 원문 출처를 함께 연결해 결과를 다시 확인할 수 있도록 구성했습니다. 지표와 서술문은 초안 저장·불러오기 흐름에 연결했습니다.

PDF 추출 과정은 최대 3개 작업을 병렬로 처리하도록 개선하고, 추출 결과를 공통 ESG 이슈 체계로 정리했습니다. 처리 시간 개선율은 별도로 측정하지 않았습니다.

</details>

---

### 금융안심이 — 보이스피싱 분석 서비스

통화 텍스트의 위험 표현, 대화 흐름, 문맥 분류 결과를 결합해  
보이스피싱 위험도와 판단 근거를 제공하는 팀 프로젝트입니다.

**6인 팀 · 위험 분석 / 모델 학습·평가 / 분석 API / CPU 배포 · 2026.07–08**

[Repository](https://github.com/nobadai/miniproject)

- **위험 분석:** Rule·Sequence·KoELECTRA 결합 및 분석 API 구현
- **모델 검증:** 피싱 23건·정상 23건 평가셋, **5-fold × 3 seed** 반복 평가
- **배포 최적화:** CPU-only PyTorch 구성으로 Docker 이미지 **22.5GB → 2.87GB**

<details>
<summary>구현 상세 · 용어 설명 · 검증 기록</summary>

- 공개 녹취를 바탕으로 피싱 23건, 정상 23건의 평가 데이터를 구성했습니다.
- 긴 통화를 Chunk 단위로 나누고 KoELECTRA 이진 분류 모델을 CUDA 환경에서 학습·평가했습니다.
- Rule(위험 표현 규칙), Sequence(대화 흐름 패턴), KoELECTRA(문맥 분류 모델) 세 신호를 결합해 위험 점수와 판단 근거를 생성했습니다.
- `5-fold × 3 seed` 반복 평가를 사용해 단일 데이터 분할 결과에만 의존하지 않도록 검증했습니다.
- 분석 결과를 FastAPI·PostgreSQL에 연결하고, Serving 환경은 CPU-only PyTorch 기준으로 구성했습니다.
- CUDA/Triton 의존성과 빌드 캐시를 정리해 Docker 이미지를 **22.5GB → 2.87GB**로 줄였습니다.

담당 범위는 준비된 녹취·텍스트 분석이며 통화 전사(STT) 전체 기능과 구분합니다. 소규모 평가셋의 일반화 한계가 있으며, Docker 수치는 이미지 용량 최적화 결과로 추론 속도 개선 수치는 아닙니다.

</details>

---

## Tech Stack

**Backend**  
`Python` `FastAPI` `Pydantic` `SQLAlchemy` `REST API` `WebSocket` `SSE`

**Database / Data**  
`PostgreSQL` `MariaDB` `SQL` `Alembic` `Excel/CSV` `OCR`

**AI / Agent / Retrieval**  
`LangGraph` `LangChain` `Tool Calling` `MCP` `RAG` `LLM Gateway` `pgvector` `FTS` `RRF` `Embedding`

**ML / Evaluation**  
`PyTorch` `KoELECTRA` `Cross Validation` `pytest` `Golden Evaluation`

**Frontend**  
`TypeScript` `React` `Next.js` `Vite`

**Infra / Development**  
`Docker` `Docker Compose` `Git` `Linux` `GitHub Actions` `Nginx`

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
