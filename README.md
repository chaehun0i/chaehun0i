# 이채훈 | Lee Chae-hun

> **AI와 데이터를 실제 서비스로 연결하는 Backend Developer**

Python과 FastAPI를 중심으로 백엔드 API와 데이터 처리 구조를 개발하고 있습니다.

데이터 수집부터 저장, 가공, 검색, AI 활용, 서비스 제공까지 이어지는
**전체 데이터 흐름을 이해하고 실제 서비스로 구현하는 개발자**를 지향합니다.

AI 모델 자체뿐만 아니라 **데이터를 어떻게 수집하고 처리하여 AI 기능으로 연결할지**,
그리고 이를 **안정적인 Backend와 서비스 구조로 제공하는 방법**에 관심이 있습니다.

* **AI Engineering** — RAG, Embedding, Vector Search 기반 AI 서비스 구현
* **Backend** — Python / FastAPI 기반 API 및 서비스 구조 설계
* **Data Engineering** — 데이터 수집·전처리, ETL 및 대용량 데이터 처리
* **Service Development** — React → API → Database로 이어지는 서비스 개발
* **Infrastructure** — Docker 기반 서비스 환경 및 CI/CD 구성

---

## Contact

* **Email**: `cognsoi.0312@gmail.com`
* **GitHub**: `chaehun0i`
* **Location**: Yongin, Korea

---

## Tech Stack

| Category             | Tech                                                                    |
| -------------------- | ----------------------------------------------------------------------- |
| **AI / LLM**         | LangChain, RAG, Sentence Transformers, Embedding, Vector Search, Ollama |
| **Backend**          | Python, FastAPI, Pydantic, REST API, WebSocket, JWT                     |
| **Database / Cache** | PostgreSQL, MariaDB, Redis, pgvector, SQL                               |
| **Data Engineering** | Pandas, PySpark, Apache Spark, Apache Airflow, ETL                      |
| **Data Collection**  | Selenium, BeautifulSoup, Web Crawling                                   |
| **Frontend**         | React, JavaScript, HTML, CSS, Bootstrap                                 |
| **Infra**            | Docker, Docker Compose, Nginx                                           |
| **CI/CD**            | GitHub Actions                                                          |
| **Tools**            | Git, GitHub, Chart.js, Streamlit                                        |

---

# Project Experience

## 01. AI 기반 ESG 보고서 자동 생성 플랫폼

> ESG 데이터 수집·전처리부터 RAG 기반 검색과 AI 보고서 문단 생성까지 연결한 서비스

**AI / RAG · Backend · Data Engineering · Full Stack**

### AI / RAG

* LangChain 기반 RAG 파이프라인 및 Prompt Chain 구성
* Sentence Transformers를 활용한 ESG 데이터 Embedding
* PostgreSQL + pgvector 기반 Vector 저장 및 유사도 검색
* 검색 결과를 기반으로 AI 보고서 문단을 생성하는 구조 구현
* AI 생성 결과와 원본 데이터 간 Fact 및 수치 정합성 검증

### Data Engineering

* ESG 관련 비정형 데이터 수집 및 전처리
* PySpark / SQL 기반 대용량 데이터 정제 및 처리
* 데이터 수집 → 전처리 → RAG 전처리 → Embedding으로 이어지는 데이터 흐름 구성
* Apache Airflow 기반 데이터 수집·전처리 작업 자동화 경험

### Backend / Frontend

* FastAPI 기반 REST API 개발
* Pydantic 기반 요청·응답 데이터 검증
* Service / Repository 패턴을 활용한 Backend 계층 분리
* React 기반 보고서 생성 및 사용자 화면 개발
* Backend API와 Frontend 간 데이터 연동 및 정합성 검증

### Troubleshooting

**검색 결과와 생성 문단의 연관성 저하**

* 메타데이터 필터링 및 템플릿 매핑 로직 적용
* 검색 결과와 ESG 문단 생성 주제 간 연관성 개선

**AI 생성 결과의 수치 누락 및 템플릿 미반영**

* 데이터 매핑 검증 로직 및 생성 전 검증 프로세스 구축
* 생성 결과의 데이터 정합성과 일관성 개선

**배포 환경의 Frontend ↔ Backend 통신 오류**

* Docker 및 Nginx Reverse Proxy 구성 개선
* 브라우저 CORS 및 서비스 통신 문제 해결

### Infrastructure / Collaboration

* Docker 기반 서비스 컨테이너화
* Nginx Reverse Proxy 구성
* GitHub Actions 기반 CI/CD
* Git Branch / Pull Request 기반 협업

---

## 02. CommitLens — Git 작업 분석 및 AI 커밋 지원 서비스

> Git 변경 데이터를 관리·분석하고, AI 기반 작업 요약과 커밋 메시지 추천으로 확장하기 위해 개발 중인 서비스

**Backend · Full Stack · Real-time Processing — In Progress**

### Backend

* FastAPI 기반 프로젝트 및 분석 실행 API 구현
* Model → Repository → Service → API 계층으로 Backend 관심사 분리
* Git 변경 파일 업로드 및 분석 실행 흐름 구현
* BackgroundTasks 기반 백그라운드 작업 처리
* WebSocket 기반 분석 진행 상태 실시간 전달
* 단일 파일 및 전체 업로드 용량 Validation / 예외 처리

### Database / Cache

* MariaDB 기반 프로젝트 및 분석 실행 데이터 관리
* Redis 기반 인증·세션 관리
* 프로젝트별 분석 실행 및 작업 이력 관리 구조 설계

### Frontend

* React + Vite 기반 서비스 UI 구현
* 프로젝트 관리 및 분석 실행 화면 구성
* 분석 진행 / 결과 요약 / 상세 분석 화면 구현
* REST API 기반 Backend 데이터 연동
* WebSocket 기반 분석 진행 상태 실시간 UI 반영

### Development Environment

* Docker Compose 기반 Backend / MariaDB / Redis 개발 환경 구성
* Frontend / Backend 분리 및 API 기반 서비스 구조 구현
* Git Branch / Pull Request 기반 개발

### Next — AI Integration

현재 Backend와 데이터 처리 구조를 구축하고 있으며,
다음 단계로 Git Diff와 변경 파일을 활용한 AI 기능을 연동할 예정입니다.

* 여러 파일의 변경 내용 및 연관 관계 분석
* 주요 코드 변경 사항 요약
* 변경 내용을 하나의 작업 단위로 정리
* 확인이 필요한 코드 및 주의사항 제공
* 분석 결과 기반 커밋 메시지 추천

---

## 03. 서울 지하철 빅데이터 분석 시스템

> 5개년 서울 지하철 이용 데이터를 활용한 대규모 데이터 처리 및 시각화 프로젝트

**Data Engineering · Big Data · Visualization**

### Data Engineering

* 2017~2021년 서울 지하철 이용 데이터 수집 및 정제
* 5개년 대규모 데이터셋 전처리
* PySpark 기반 대용량 데이터 처리 및 분석
* 분석 목적에 따른 데이터 가공 및 집계
* 분석 결과의 서비스 활용을 위한 데이터 구조화

### Visualization

* Chart.js 기반 인터랙티브 데이터 시각화
* 지하철 이용 데이터 탐색 Dashboard 구현

---

# Current Focus

현재 **AI · Backend · Data Engineering**을 중심으로 역량을 확장하고 있습니다.

### AI Engineering

* LLM / RAG / Vector Embedding
* AI 기능과 Backend 서비스 연동
* Vector Search 및 검색 기반 AI 서비스
* AI Output Validation
* 다양한 AI 분야의 프로젝트 경험 확장

### Backend Engineering

* Python / FastAPI
* REST API Design
* Backend Architecture
* Async / Background Processing
* WebSocket
* Authentication / Authorization
* Database / Cache

### Data Engineering

* Data Collection & Preprocessing
* ETL Pipeline
* Large-scale Data Processing
* Data Validation
* AI 활용을 위한 데이터 처리

---

## Currently

* **CommitLens** — Backend 및 서비스 구조 개발 / AI 기능 연동 준비
* **AI 심화과정** — AI 미니프로젝트 및 메인프로젝트 진행 예정

---

> **AI를 이해하는 Backend Developer, 데이터를 서비스로 연결할 수 있는 Developer로 성장하고 있습니다.**
