
# 이채훈 | Lee Chae-hun

> **AI 기능을 실제 서비스 구조로 구현하는 Backend Developer**

Python과 FastAPI를 중심으로  
**데이터 · 업무 규칙 · AI를 API와 Database 위에서 연결하는 Backend**를 개발하고 있습니다.

단순히 LLM API를 호출하는 것보다,

- 어떤 데이터를 정본으로 사용할지
- 어떤 판단을 Rule과 코드가 담당할지
- 어떤 부분을 AI에게 맡길지
- 결과를 어떻게 검증하고 추적할지
- 실제 서비스의 API와 DB 구조로 어떻게 연결할지

를 함께 고민합니다.

현재는 **AI Agent, RAG, Search, Backend Architecture**를 중심으로
실제 업무 데이터를 활용하는 AI 서비스를 개발하고 있습니다.

---

## Contact

- **Email**: `cognsoi.0312@gmail.com`
- **GitHub**: `chaehun0i`
- **Location**: Yongin, Korea

---

## Tech Stack

### Core

`Python` `FastAPI` `PostgreSQL` `Pydantic` `SQL`

### AI / LLM

`LangChain` `LangGraph` `RAG` `Embedding` `Vector Search`  
`Sentence Transformers` `Ollama` `Gemini`

### Database / Data

`PostgreSQL` `pgvector` `MariaDB` `Redis`  
`Pandas` `PySpark` `Apache Spark`

### Backend / Service

`REST API` `WebSocket` `JWT`  
`Background Tasks` `Data Validation`

### Infrastructure

`Docker` `Docker Compose` `Nginx`  
`GitHub Actions` `EC2`

### Frontend

`React` `Vite` `JavaScript` `Chart.js`

### Data Collection

`Selenium` `BeautifulSoup` `Web Crawling`

---

# Selected Projects

## 01. 햇들농산 — 농산물 유통 의사결정 Multi-Agent System

> **매입 · 재고 · 판매 · 재무 데이터를 기반으로 업무 의사결정을 지원하는 Multi-Agent 서비스**

**AI Agent · Backend · PostgreSQL · LangGraph · LLM**

### Role

**Finance Agent / Sales Agent 담당**

재무와 판매 영역의 도메인 로직, Agent 흐름, 데이터 계약 및
다른 Agent와의 검증 구조를 설계·구현했습니다.

### Finance Agent

- 매입 전후 현금흐름과 지급 의무를 기반으로 재무 실행 가능성 검증
- 매입채무, 매출채권, 급여, 부채 상환 등 Cash Event 기반 Projection
- 최소 운영자금과 예상 최저 현금을 활용한 Finance Constraint 판정
- 판매안의 매출액, 마진, 결제조건, 채권 및 여신 검증
- `READY / RUNTIME_NOT_READY / ERROR`와
  `PASS / REVIEW_REQUIRED / FAIL` 상태 분리
- 수량·금액·판정은 결정론적 Rule에서 처리하고
  LLM은 해석과 설명에 한정

### Sales Agent

- 계약, 재고, 재무조건을 기반으로 판매 후보 생성
- Conservative / Balanced / Aggressive 시나리오 구성
- Finance / Logistics / Purchase 검증 결과 반영
- 실행 가능성, 재무 상태, 수익성, 재고 위험 등을 기반으로
  deterministic candidate ranking
- LangGraph 기반
  Context → Candidate → Validation → Feedback → Ranking → Self-check 흐름 구현
- 승인된 판매의 멱등 저장 및 충돌 검증

### Architecture

```text
Master
  │
  ├── Purchase Agent
  ├── Logistics Agent
  ├── Finance Agent
  ├── Sales Agent
  └── ML
````

각 Agent가 다른 도메인의 내부 데이터를 직접 수정하지 않도록
**도메인별 책임과 데이터 소유권을 분리**했습니다.

LLM의 Tool Call 자체를 실행 권한으로 사용하지 않고,
실제 실행 전 Capability와 Dependency를 코드에서 다시 검증합니다.

### Engineering Principles

* `0 != NULL`
* LLM은 금액·수량·최종 판정을 생성하지 않음
* Domain별 Source of Truth 분리
* 과거 시점 판단을 위한 `as_of` 기준 유지
* Evidence / `ref_id`를 통한 판단 근거 추적
* 입력 또는 정책이 부족하면 값을 추정하지 않고 Fail-Closed

---

## 02. F&B VOC Intelligence Platform

> **고객 리뷰와 VOC를 검색·분석하여 상품 문제와 개선 기회를 찾는 F&B 특화 RAG 서비스**

**Personal Project · AI Backend · RAG · Hybrid Search — In Progress**

### Data Layer

* Product / Review / VOC 데이터 구조 설계
* 데이터 Validation 및 Quality Check
* F&B VOC Pain Point Taxonomy 구성

### Search

* PostgreSQL Full Text Search 기반 Keyword Search
* pgvector 기반 Vector Search
* Keyword + Vector 결과를 결합하는 Hybrid Search
* Reciprocal Rank Fusion 기반 검색 결과 통합

### RAG Architecture

```text
Question
   ↓
Hybrid Retrieval
   ↓
Relevant VOC Evidence
   ↓
Context Builder
   ↓
Grounded Prompt
   ↓
LLM
   ↓
Answer + Sources
```

단순 리뷰 요약이 아니라
**실제 고객 VOC를 근거로 답변하는 구조**를 목표로 개발하고 있습니다.

### Current Status

* Data Layer 구현
* VOC EDA / Taxonomy 구성
* PostgreSQL 저장 구조 구현
* Vector Search 구현
* Hybrid Search 구현
* RAG Layer 개발 진행 중

---

## 03. AI 기반 ESG 보고서 자동 생성 플랫폼

> **ESG 데이터를 수집·정제하고 RAG를 통해 근거 기반 보고서 초안을 생성하는 서비스**

**AI / RAG · Backend · Data Engineering**

### Award

**개인 부문 최우수상 수상**

### AI / RAG

* LangChain 기반 RAG Pipeline 구현
* Sentence Transformers 기반 ESG 데이터 Embedding
* PostgreSQL + pgvector 기반 Vector Search
* 검색 Evidence를 기반으로 ESG 보고서 문단 생성
* 원본 데이터와 AI 출력 간 수치 및 Fact 정합성 검증

### Data Engineering

```text
Raw Data
   ↓
Cleaning
   ↓
Normalization
   ↓
Embedding
   ↓
Vector DB
   ↓
Retrieval
   ↓
LLM Generation
```

* ESG 비정형 데이터 수집 및 전처리
* Selenium 기반 데이터 수집
* PySpark / SQL 기반 데이터 정제
* RAG 활용을 위한 데이터 구조화

### Backend / Service

* FastAPI 기반 REST API
* Pydantic 기반 I/O Validation
* React 기반 보고서 생성 UI
* Docker / Nginx 기반 서비스 구성
* GitHub Actions 기반 CI/CD

### Key Troubleshooting

**검색 결과와 생성 문단의 연관성 저하**

→ Metadata Filtering과 Template Mapping을 추가하여
검색 Context와 생성 대상 ESG 항목 간 관계를 강화했습니다.

**AI 생성 과정에서 수치가 변경되는 문제**

→ 원본 Evidence와 생성 결과를 비교하는 검증 계층을 추가하여
AI가 임의의 수치를 생성하는 문제를 줄였습니다.

---

## 04. CommitLens — Git 작업 분석 및 AI 커밋 지원 서비스

> **Git 변경 데이터를 분석하여 개발 작업을 하나의 의미 있는 작업 단위로 정리하는 서비스**

**Personal Project · Backend · Full Stack — In Progress**

### Backend

* FastAPI 기반 Project / Analysis API
* Model → Repository → Service → API 계층 분리
* Git 변경 파일 업로드 및 분석 실행
* BackgroundTasks 기반 비동기 작업 처리
* WebSocket 기반 분석 진행 상태 전달
* 파일 및 전체 업로드 용량 Validation

### Database / Cache

* MariaDB 기반 Project / Analysis History 관리
* Redis 기반 인증 및 Session 관리

### Frontend

* React + Vite 기반 UI
* REST API 연동
* WebSocket 기반 분석 진행 상태 표시

### Next

Git Diff와 변경 파일을 기반으로

* 여러 파일의 변경 관계 분석
* 주요 변경 사항 요약
* 작업 단위 추론
* 코드 검토 포인트 제공
* Commit Message 추천

기능을 확장하고 있습니다.

---

# How I Build AI Services

AI 서비스에서 중요한 것은
**모델을 호출하는 것만이 아니라 모델이 어떤 데이터와 규칙 위에서 동작하는지를 설계하는 것**이라고 생각합니다.

그래서 프로젝트에서는 다음 원칙을 중요하게 다루고 있습니다.

### 1. Deterministic Core

금액, 수량, 상태 판정처럼
재현성과 정확성이 필요한 값은 일반 코드와 Rule에서 처리합니다.

### 2. AI as Interpretation Layer

LLM은 계산 결과를 변경하는 역할보다
결과 설명, 정보 연결, 대안 제시와 같은 역할에 사용합니다.

### 3. Data Ownership

하나의 데이터에 여러 Domain이 서로 다른 계산을 적용하지 않도록
Source of Truth와 Domain Ownership을 명확하게 정의합니다.

### 4. Evidence

AI 결과가 어떤 데이터와 정책을 기반으로 만들어졌는지
추적할 수 있는 구조를 지향합니다.

### 5. Fail-Closed

필요한 데이터나 정책이 없을 경우
임의의 값을 생성하기보다 판단을 중단하고
부족한 정보를 명확하게 반환하도록 설계합니다.

---

# Current Focus

현재 다음 영역을 중심으로 공부하고 개발하고 있습니다.

### AI Backend

* AI Agent Architecture
* Tool Calling
* Multi-Agent Orchestration
* RAG
* Hybrid Search
* Structured Output
* AI Output Validation

### Backend Engineering

* FastAPI Architecture
* PostgreSQL
* Transaction / Idempotency
* API Contract
* Domain Modeling
* Error / State Design

### Data / Retrieval

* PostgreSQL Full Text Search
* Vector Search
* pgvector
* Embedding
* Retrieval Evaluation
* Data Pipeline

### Infrastructure

* Docker / Docker Compose
* GitHub Actions
* Nginx
* EC2
* Service Deployment

---

## Currently

* **햇들농산** — Finance / Sales Agent 및 Multi-Agent 통합 고도화
* **F&B VOC Intelligence** — Hybrid Search 완료 / RAG Layer 개발
* **CommitLens** — Backend 및 AI 분석 구조 개발

---

> **정본 데이터와 업무 규칙을 기반으로
> AI가 안전하게 동작할 수 있는 Backend를 만들고 있습니다.**
