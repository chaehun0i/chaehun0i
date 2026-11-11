# 이채훈 | Lee Chae-hun

**Software Developer · Backend / AI / Data / Automation**

업무를 이해하고, 데이터에서 API·AI·사용자 화면까지 연결하는 개발자입니다.

Python·FastAPI 기반 백엔드를 중심으로 데이터 수집·검색, AI Agent와 모델 평가, React 기반 화면 연동, Docker 실행 환경을 다뤄 왔습니다. 사용자의 작업 흐름을 API·DB·화면으로 구체화하고, 상태 관리와 검증을 통해 기능이 안정적으로 이어지도록 구현합니다.

외식경영을 전공했으며, F&B 운영·농산물 유통·ESG 보고서·회계 등 업무 데이터를 다루는 프로젝트를 진행했습니다.

[GitHub](https://github.com/chaehun0i) · [Email](mailto:jt33_@naver.com)

## 구현 경험

| 영역 | 프로젝트에서 다룬 내용 |
| --- | --- |
| **Backend & Database** | API 입력 검증, 관계형 데이터 모델링, 트랜잭션, 승인·상태 전이, 멱등성·동시성 제어 |
| **AI & Machine Learning** | LangGraph 상태 저장·재개, Tool Calling·MCP, RAG, KoELECTRA 학습·반복 평가 |
| **Data & Retrieval** | Excel/CSV 입력, 보고서 OCR, 기사·설문 수집, Embedding, pgvector·FTS·RRF 검색 |
| **Frontend & Integration** | React·TypeScript 화면과 API 연결, 작업 진행·승인·결과 조회, 오류·빈 상태 처리 |
| **Delivery & Validation** | Docker·Compose, GitHub Actions, 단위·회귀·PostgreSQL 통합·동시성 테스트 |

## Selected Projects

| 프로젝트 | 해결한 업무 | 형태 / 주요 담당 |
| --- | --- | --- |
| [**AI Accounting Office**](https://github.com/chaehun0i/ai-accounting-office) | 거래 자료를 전표·승인·장부·월마감과 연결 | 개인 / Backend·DB·Agent·화면 연계 |
| [**ServIQ**](https://github.com/chaehun0i/fnb-voc-intelligence) | 고객 의견과 운영 자료의 근거 조사·사람 검토 | 개인 / 데이터 입력·검색·Agent·운영 콘솔 |
| [**WITH ESG**](https://github.com/shell-files/dev_skm) | 보고서·기사·설문을 ESG 보고서 초안으로 연결 | 4인 팀 / 자료 처리·RAG·설문·초안 저장·양식 |
| [**햇들농산**](https://github.com/nobadai/mainproject) | 가격·재고·자금 조건을 반영한 판매 후보 생성·검증 | 5인 팀 / Finance·Sales Agent·Harness·초기 Logistics Runtime |
| [**금융안심이**](https://github.com/nobadai/miniproject) | 통화 텍스트의 위험 신호 분석과 근거 제공 | 5인 팀 / 모델 학습·평가·분석 API·CPU 배포 |

### AI Accounting Office — 회계 업무와 Agent 연계

**Python · FastAPI · SQLAlchemy · PostgreSQL · Alembic · LangGraph · TypeScript**

거래·증빙 입력부터 전표 작성, 독립 승인, 기표, 원장·재무 조회까지 연결하는 개인 프로젝트입니다.

- 멱등성 키, 원천 버전, 행 잠금, 승인 대상 digest를 확인해 중복 처리와 오래된 승인 사용을 통제했습니다.
- 독립 PostgreSQL 연결에서 동시 기표 번호 발급과 동일 전표의 중복 기표 거부를 검증했습니다.
- Agent의 전표 제안을 사람 검토 후 **DRAFT 생성**에 연결하고, 승인·기표는 별도 업무 명령으로 분리했습니다.
- 거래·전표·월마감·AI 조회 화면을 API에 연결하고 회사·권한·출처를 확인할 수 있도록 구성했습니다.

[Repository](https://github.com/chaehun0i/ai-accounting-office) · [동시성 테스트](https://github.com/chaehun0i/ai-accounting-office/blob/main/backend/tests/integration/test_posting_concurrency.py) · [Agent 구현 범위](https://github.com/chaehun0i/ai-accounting-office/blob/main/docs/platform/agent-runtime.md)

### ServIQ — F&B 운영 문제 조사 서비스

**Python · FastAPI · LangGraph · LangChain · MCP · PostgreSQL / pgvector · React**

고객 의견과 매장 운영 자료를 입력하면 관련 근거를 검색하고, AI가 원인·개선안을 제안해 사람이 검토하는 개인 프로젝트입니다.

- VOC·Excel/CSV 입력 검증과 저장을 검색·조사·승인 흐름으로 연결했습니다.
- PostgreSQL FTS와 pgvector 검색 결과를 RRF로 결합하고 원문 출처를 전달했습니다.
- LangGraph checkpoint와 interrupt/resume으로 승인 대기·중단·재시작과 완료 결과 재사용을 구현했습니다.
- 운영 콘솔에서 진행 상태·근거·다음 행동을 확인하도록 연결하고, 도구 실행 직전 권한·범위를 재검증했습니다.

로컬 Docker·샘플 데이터 기준으로 검증했습니다. 실제 POS/ERP 변경과 현장 개선 효과는 검증 범위에 포함하지 않습니다.

[Repository](https://github.com/chaehun0i/fnb-voc-intelligence) · [승인·재개 테스트](https://github.com/chaehun0i/fnb-voc-intelligence/blob/main/backend/tests/test_approval_resume.py) · [검색 테스트](https://github.com/chaehun0i/fnb-voc-intelligence/blob/main/backend/tests/test_hybrid_search.py)

### WITH ESG — ESG 보고서 생성 서비스

**Python · FastAPI · LangChain · PostgreSQL / pgvector · OCR · SQL**

지속가능경영보고서·기사·설문을 가공하고, 관련 자료 검색부터 ESG 보고서 초안 생성·저장·양식 적용까지 연결한 팀 프로젝트입니다.

- 3개년 보고서의 공동 OCR·PDF 추출, 기사 벡터화, 설문 URL 생성·응답 수집을 담당했습니다.
- pgvector로 검색한 관련 문단을 AI 문단 생성의 근거로 전달했습니다.
- 정량 지표와 서술문을 구분해 초안 저장·불러오기에 연결하고, AI 생성 출처와 5개 이슈 양식을 연결했습니다.
- PDF 추출은 최대 3개 작업으로 병렬 처리하고 공통 이슈 체계에 매핑했습니다. 처리 시간 개선율은 별도로 측정하지 않았습니다.

[공식 팀 저장소](https://github.com/shell-files/dev_skm) · [AI 문단 생성](https://github.com/shell-files/dev_skm/blob/skm_test/backend/src/services/ai/service.py) · [초안 저장](https://github.com/shell-files/dev_skm/blob/skm_test/backend/src/services/draft/service.py)

### 햇들농산 — 농산물 매입·판매 Multi-Agent

**Python · LangGraph · Tool Calling · PostgreSQL · pytest**

가격·재고·자금 정보를 바탕으로 판매 후보를 만들고 재무·물류 조건을 검증하는 팀 프로젝트입니다. Finance Agent/Harness, Sales Agent와 Logistics 초기 Runtime을 담당했습니다.

- 판매 실행 **9,937건**에서 후보 생성 전 재무 정보 전달이 **0건**이던 문제를 확인하고 선행 입력 계약과 실행 순서를 수정했습니다.
- 실행 가능한 도구가 0~1개일 때는 코드로 처리해, 동일 조건의 세 모드 합산 Planner 호출을 **9회 → 3회**로 줄였습니다.
- 가격·수량·금액·추천 ID와 Finance 판정은 코드로 계산하고, LLM의 역할을 전략 방향·설명과 분리했습니다.
- 후보 생성·검증·피드백·랭킹 경계를 회귀 테스트로 검증했습니다.

[Repository](https://github.com/nobadai/mainproject)

### 금융안심이 — 보이스피싱 텍스트 분석

**Python · FastAPI · PyTorch · KoELECTRA · PostgreSQL · Docker**

준비된 통화 녹취·텍스트에서 위험 표현·대화 흐름·모델 점수를 결합해 위험도와 판단 근거를 제공한 팀 프로젝트입니다.

- 공개 녹취 기반 피싱 23건·정상 23건 평가셋을 구성하고 KoELECTRA를 CUDA 환경에서 학습했습니다.
- 긴 통화를 Chunk로 처리하고, `5-fold × 3 seed` 반복 평가로 분할·초기값에 따른 변동을 확인했습니다.
- 분석 결과를 API·DB에 연결하고 CPU-only PyTorch와 의존성·빌드 캐시 정리로 Docker 이미지를 **22.5GB → 2.87GB**로 줄였습니다.

소규모 평가셋의 결과와 일반화 성능을 구분합니다. Docker 수치는 이미지 용량 변화입니다.

[Repository](https://github.com/nobadai/miniproject)

> 개선 수치와 평가 결과는 각 프로젝트의 당시 기록과 비교 조건을 기준으로 합니다. 구현·검증 범위는 연결한 저장소와 문서에 정리했습니다.

## Tech Stack

| 영역 | 사용 기술 |
| --- | --- |
| **Backend** | Python, FastAPI, Pydantic, SQLAlchemy, REST API, WebSocket / SSE |
| **Database & Data** | PostgreSQL, MariaDB, SQL, Alembic, pgvector, FTS, RRF, OCR, Excel / CSV |
| **AI & ML** | LangGraph, LangChain, MCP, Tool Calling, RAG, Embedding, PyTorch, KoELECTRA |
| **Frontend** | TypeScript, React, Next.js, Vite |
| **Development & Delivery** | Git, Docker, Docker Compose, GitHub Actions, Nginx, pytest |

## 개발할 때 중요하게 보는 것

- **업무와 데이터의 연결:** 입력·검토·승인·결과 확인의 흐름을 정리하고 API·DB·화면에 반영합니다.
- **책임이 분명한 설계:** 금액·수량·상태 전이는 코드와 업무 규칙이 담당하고, AI의 제안은 검증과 사람의 판단에 연결합니다.
- **실패 이후의 동작:** 중복 요청, 원천 변경, 권한 변경, 재시작 상황을 정상 경로와 함께 확인합니다.
- **설명할 수 있는 결과:** 구현 코드·출처·테스트·변경 이력으로 담당 범위와 한계를 남깁니다.

## Education & Award

- **심화 생성형 AI 활용 인재양성과정** · 2026.07–2026.09  
  AI Agent 프로젝트, FastAPI / React, RAG
- **삼정 ESG 데이터 활용 AX Academy with AI Agent** · 2025.12–2026.06  
  ESG 데이터 처리, AI 보고서 생성 프로젝트
- **삼정 ESG AX Academy with AI Agent · 개인 부문 최우수상**
- **한국관광대학교 외식경영학과 졸업** · 2024.02

## Contact

- **Email:** [jt33_@naver.com](mailto:jt33_@naver.com)
- **GitHub:** [chaehun0i](https://github.com/chaehun0i)
