# 이채훈 | Lee Chae-hun

**Software Developer · Backend / AI / Data / Automation**

업무를 이해하고, 데이터에서 API·AI·사용자 화면까지 연결하는 개발자입니다.

Python·FastAPI 기반 백엔드를 중심으로 데이터 수집·검색, AI Agent와 모델 평가, React 기반 화면 연동, Docker 실행 환경을 다뤄 왔습니다. 사용자의 작업 흐름을 API·DB·화면으로 구체화하고, 상태 관리와 검증을 통해 기능이 안정적으로 이어지도록 구현합니다.

외식경영을 전공했으며, F&B 운영·농산물 유통·ESG 보고서·회계 등 업무 데이터를 다루는 프로젝트를 진행했습니다.

[GitHub](https://github.com/chaehun0i) · [Email](mailto:jt33_@naver.com)

## 구현 경험

| 영역 | 프로젝트에서 다룬 내용 |
| --- | --- |
| **Backend & Database** | 입력값 검사, 데이터 구조 설계, 여러 저장 작업의 일괄 처리, 승인 단계 관리, 중복·동시 요청 제어 |
| **AI & Machine Learning** | AI 작업의 저장·재개, 외부 기능 연결, 검색 자료에 근거한 답변 생성, 텍스트 분류 모델 학습·평가 |
| **Data & Retrieval** | Excel/CSV 입력, 문서 문자 추출, 기사·설문 수집, 키워드와 의미 유사도 검색 결합 |
| **Frontend & Integration** | React·TypeScript 화면과 API 연결, 작업 진행·승인·결과 조회, 오류·빈 상태 처리 |
| **Delivery & Validation** | Docker·Compose, GitHub Actions, 단위·회귀·PostgreSQL 통합·동시성 테스트 |

## Selected Projects

| 프로젝트 | 해결한 업무 | 형태 / 주요 담당 |
| --- | --- | --- |
| [**AI Accounting Office**](https://github.com/chaehun0i/ai-accounting-office) | 거래 자료를 전표·승인·장부·월마감과 연결 | 개인 / 서버·데이터베이스·AI·화면 연계 |
| [**ServIQ**](https://github.com/chaehun0i/fnb-voc-intelligence) | 고객 의견과 운영 자료의 근거 조사·사람 검토 | 개인 / 데이터 입력·검색·AI 조사·관리 화면 |
| [**WITH ESG**](https://github.com/shell-files/dev_skm) | 보고서·기사·설문을 ESG 보고서 초안으로 연결 | 4인 팀 / 자료 처리·검색 기반 생성·설문·초안 저장·양식 |
| [**햇들농산**](https://github.com/nobadai/mainproject) | 가격·재고·자금 조건을 반영한 판매 후보 생성·검증 | 5인 팀 / 재무·판매 AI·도구 실행 제어·초기 물류 실행 흐름 |
| [**금융안심이**](https://github.com/nobadai/miniproject) | 통화 텍스트의 위험 신호 분석과 근거 제공 | 6인 팀 / 모델 학습·평가·분석 API·CPU 배포 |

### AI Accounting Office — 회계 업무와 Agent 연계

**Python · FastAPI · SQLAlchemy · PostgreSQL · Alembic · LangGraph · TypeScript**

거래·증빙 입력부터 전표(거래를 기록하는 회계 문서) 작성, 다른 담당자의 승인, 장부 반영, 월마감과 재무 조회까지 연결하는 개인 프로젝트입니다.

- 같은 요청이 반복되어도 중복 처리하지 않도록 하고, 동시에 같은 데이터를 바꾸지 못하도록 제어했습니다. 처리 시점에 데이터 버전과 승인 내용의 변경 여부도 다시 확인했습니다.
- 서로 다른 PostgreSQL 연결에서 요청을 동시에 보내, 전표 번호가 겹치지 않고 같은 전표가 장부에 두 번 반영되지 않는지 검증했습니다.
- AI의 전표 제안은 사람이 검토한 뒤 **초안으로만 저장**합니다. 최종 승인과 장부 반영은 별도 절차로 분리했습니다.
- 거래·전표·월마감·AI 조회 화면을 서버에 연결하고, 현재 회사와 사용자 권한, 금액의 출처를 확인하도록 구성했습니다.

[Repository](https://github.com/chaehun0i/ai-accounting-office) · [동시성 테스트](https://github.com/chaehun0i/ai-accounting-office/blob/main/backend/tests/integration/test_posting_concurrency.py) · [Agent 구현 범위](https://github.com/chaehun0i/ai-accounting-office/blob/main/docs/platform/agent-runtime.md)

### ServIQ — F&B 운영 문제 조사 서비스

**Python · FastAPI · LangGraph · LangChain · MCP · PostgreSQL / pgvector · React**

고객 의견과 매장 운영 자료를 입력하면 관련 근거를 검색하고, AI가 원인·개선안을 제안해 사람이 검토하는 개인 프로젝트입니다.

- 고객 의견(VOC)과 Excel/CSV 파일의 입력값 검사·저장을 검색·조사·승인 흐름으로 연결했습니다.
- 단어가 일치하는 자료와 의미가 비슷한 자료를 함께 검색하고, 두 결과의 순위를 통합해 원문 출처와 함께 전달했습니다.
- LangGraph로 조사 진행 상태를 저장해, 사람의 승인을 기다리거나 작업이 중단되어도 이어서 진행하고 이미 완료한 결과는 재사용하도록 구현했습니다.
- 관리 화면에서 진행 상태·근거·다음 행동을 확인하도록 연결하고, AI가 기능을 실행하기 직전에 현재 권한과 허용 범위를 다시 검사했습니다.

로컬 Docker·샘플 데이터 기준으로 검증했습니다. 실제 매장 판매·전사 업무 시스템(POS/ERP)의 데이터 변경과 현장 개선 효과는 검증 범위에 포함하지 않습니다.

[Repository](https://github.com/chaehun0i/fnb-voc-intelligence) · [승인·재개 테스트](https://github.com/chaehun0i/fnb-voc-intelligence/blob/main/backend/tests/test_approval_resume.py) · [검색 테스트](https://github.com/chaehun0i/fnb-voc-intelligence/blob/main/backend/tests/test_hybrid_search.py)

### WITH ESG — ESG 보고서 생성 서비스

**Python · FastAPI · LangChain · PostgreSQL / pgvector · OCR · SQL**

지속가능경영보고서·기사·설문을 가공하고, 관련 자료 검색부터 ESG 보고서 초안 생성·저장·양식 적용까지 연결한 팀 프로젝트입니다.

- 3개년 보고서의 문자·표 추출(OCR/PDF 처리)을 공동 수행하고, 기사를 의미 유사도 검색에 사용할 수 있게 변환하며 설문 링크 생성·응답 수집을 담당했습니다.
- 보고서와 기사에서 관련 문단을 검색해 AI에 전달하고, 검색 자료를 근거로 ESG 보고서 초안을 생성하도록 연결했습니다.
- 실제 수치와 AI 설명문을 구분해 저장·불러오기를 구현하고, 생성 내용의 출처와 5개 주요 주제의 보고서 양식을 연결했습니다.
- PDF는 최대 3개를 동시에 추출하고, 문서마다 다른 주제 표현을 공통 분류 기준에 연결했습니다. 처리 시간 개선율은 별도로 측정하지 않았습니다.

[공식 팀 저장소](https://github.com/shell-files/dev_skm) · [AI 문단 생성](https://github.com/shell-files/dev_skm/blob/skm_test/backend/src/services/ai/service.py) · [초안 저장](https://github.com/shell-files/dev_skm/blob/skm_test/backend/src/services/draft/service.py)

### 햇들농산 — 농산물 매입·판매 Multi-Agent

**Python · LangGraph · Tool Calling · PostgreSQL · pytest**

가격·재고·자금 정보를 바탕으로 판매 후보를 만들고 재무·물류 조건을 검증하는 팀 프로젝트입니다. 재무 검토·판매 후보 생성 AI, 도구 실행 제어, 초기 물류 작업의 실행 흐름을 담당했습니다.

- 판매 실행 **9,937건**을 분석해 판매 후보를 만들기 전에 재무 정보가 전달된 사례가 **0건**임을 확인했습니다. 재무 정보를 먼저 받아 후보 생성에 사용하도록 입력 항목과 실행 순서를 바꿨습니다.
- 다음에 실행할 기능이 없거나 하나뿐이면 AI에게 선택을 묻지 않고 코드로 처리했습니다. 동일 조건의 세 가지 실행 방식에서 다음 기능을 고르는 AI 호출을 합계 **9회 → 3회**로 줄였습니다.
- 가격·수량·금액·추천안 식별자와 재무 판정은 코드로 확정하고, 언어 모델(LLM)은 전략 방향과 설명을 보조하도록 역할을 나눴습니다.
- 판매 후보 생성, 조건 검증, 결과 반영, 추천 순위 결정이 서로의 값을 잘못 바꾸지 않는지 반복 테스트로 확인했습니다.

[Repository](https://github.com/nobadai/mainproject)

### 금융안심이 — 보이스피싱 텍스트 분석

**Python · FastAPI · PyTorch · KoELECTRA · PostgreSQL · Docker**

준비된 통화 녹취·텍스트에서 위험 표현·대화 흐름·모델 점수를 결합해 위험도와 판단 근거를 제공한 6인 팀 프로젝트입니다.

- 공개 녹취로 피싱 23건·정상 23건 평가 자료를 구성하고, 한국어 텍스트 분류 모델인 KoELECTRA를 GPU 환경에서 학습했습니다.
- 긴 통화를 짧은 구간으로 나누어 분석했습니다. 데이터를 5개 묶음으로 나누어 번갈아 평가하고 초기 난수값 3개로 반복해 결과 변동을 확인했습니다(`5-fold × 3 seed`).
- 분석 결과를 서버와 데이터베이스에 연결했습니다. CPU 실행에 맞춰 PyTorch를 구성하고 불필요한 GPU 패키지와 빌드 캐시를 정리해 Docker 이미지를 **22.5GB → 2.87GB**로 줄였습니다.

소규모 평가셋의 결과와 일반화 성능을 구분합니다. Docker 수치는 이미지 용량 변화입니다.

[Repository](https://github.com/nobadai/miniproject)

> 개선 수치와 평가 결과는 각 프로젝트의 당시 기록과 비교 조건을 기준으로 합니다. 구현·검증 범위는 연결한 저장소와 문서에 정리했습니다.

<details>
<summary><strong>기술 용어 간단히 보기</strong></summary>

| 용어 | 이 프로필에서의 의미 |
| --- | --- |
| API / DB | 화면·프로그램이 서버 기능을 호출하는 연결 규칙 / 데이터를 저장하는 데이터베이스 |
| AI Agent | 주어진 업무 흐름에 따라 자료를 찾고 기능을 호출하는 AI 실행 프로그램 |
| RAG | 관련 자료를 먼저 검색한 뒤 그 자료를 근거로 AI 답변·문단을 생성하는 방식 |
| Embedding / pgvector | 자료의 의미를 숫자로 표현하는 변환 / PostgreSQL에서 의미 유사도 검색을 지원하는 확장 기능 |
| FTS / RRF | 단어 기반 전문 검색 / 여러 검색 결과를 순위 기준으로 통합하는 방식 |
| Tool Calling / MCP | AI가 정해진 기능을 호출하는 방식 / AI와 기능·자료 제공 시스템을 연결하는 표준 규약 |
| 멱등성 / 동시성 제어 | 같은 요청을 반복해도 중복 반영하지 않는 성질 / 동시 요청이 데이터를 잘못 덮거나 충돌하지 않도록 하는 제어 |
| 회귀 테스트 / CI | 변경 후 기존 기능이 깨지지 않았는지 확인하는 테스트 / 변경 사항을 자동으로 빌드·검사하는 절차 |

</details>

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
- **책임이 분명한 설계:** 금액·수량·업무 단계의 변경은 코드와 업무 규칙이 담당하고, AI의 제안은 검증과 사람의 판단에 연결합니다.
- **실패 이후의 동작:** 중복 요청, 처리 기준 데이터의 변경, 권한 변경, 재시작 상황을 정상 경로와 함께 확인합니다.
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
