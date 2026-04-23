---
status: Approved
owner: All
version: 0.1
last_updated: 2026-04-24
---

# 팀 헌장 (Team Charter)

Synapse는 단일 오너가 주도하되, 각 단계에서 전문 역할의 "모자(hat)"를 바꿔 쓰는 방식으로 작업합니다. 각 역할은 명확한 책임·주요 산출물·인수인계를 가집니다. 공동 작업자가 합류하면 역할 단위로 오너십을 재분배합니다.

## 1. 역할 (Agent Roles)

### 1.1 Product Manager (PM)
- **책임**: 비전·목표 정의, PRD 작성, 로드맵 관리, 우선순위 결정, 이해관계자 커뮤니케이션
- **주요 산출물**: `02_product/VISION.md`, `02_product/PRD.md`, `02_product/ROADMAP.md`, 유저 스토리
- **입력**: 리서치 결과, 경쟁사 분석, 사용자 인터뷰 요약
- **핸드오프**: UX Researcher · Designer · Architect

### 1.2 UX Researcher
- **책임**: 사용자 인터뷰 기획·수행, 페르소나 정의, 사용자 여정 도출, 정성 데이터 분석
- **주요 산출물**: `01_research/personas.md`, `01_research/user_interviews/`, `06_evaluation/interview_protocol.md`, thematic analysis 리포트
- **입력**: PM의 리서치 질문, 타겟 사용자 가설
- **핸드오프**: PM · Designer

### 1.3 Product Designer
- **책임**: 정보구조(IA), 플로우, 와이어프레임, 하이파이 디자인, 디자인 시스템
- **주요 산출물**: `03_design/ia.md`, `03_design/wireframes/`, `03_design/design_system/`
- **입력**: PRD, 페르소나, 유저 여정
- **핸드오프**: Frontend Dev

### 1.4 Architect
- **책임**: 시스템 구조, 기술 스택 결정, RFC 작성, 비기능 요구사항(확장성·지연시간·비용)
- **주요 산출물**: `04_architecture/tech_stack.md`, `04_architecture/rfc/`, `00_meta/adr/`
- **입력**: PRD, 비기능 요구사항
- **핸드오프**: Backend · Frontend · AI/ML

### 1.5 Backend Dev
- **책임**: API, 데이터 모델, 인증, PDF/파일 처리 파이프라인, 비동기 작업 큐
- **주요 산출물**: `05_src/backend/`, OpenAPI 스펙
- **입력**: RFC, 데이터 모델

### 1.6 Frontend Dev
- **책임**: UI, 상태 관리, 리더·에디터, 에이전트 상호작용 UX, 스트리밍 응답
- **주요 산출물**: `05_src/frontend/`
- **입력**: 디자인, API 스펙

### 1.7 AI / ML Engineer
- **책임**: 논문 파싱·청킹, 임베딩·검색, 에이전트 그래프, 프롬프트 엔지니어링, 툴(웹 검색·인용 추적) 통합, 모델 평가 루프
- **주요 산출물**: `05_src/agents/`, `04_architecture/rfc/ai_*`, 모델·프롬프트 실험 노트
- **입력**: PRD, 평가 메트릭, 도메인 리서치
- **핸드오프**: Eval Lead

### 1.8 Evaluation Lead
- **책임**: 정량 메트릭 정의·측정, 정성 인터뷰 분석, 출시·회고 리포트, 품질 게이트 운영
- **주요 산출물**: `06_evaluation/metrics_framework.md`, `06_evaluation/reports/`, 릴리즈 게이트 체크리스트
- **입력**: 모든 산출물, 사용자 인터뷰 원본, 프로덕션 로그

## 2. 역할 전환 규칙

- 문서·코드 커밋 시 작성자 역할을 명시: `[PM] PRD 초안`, `[AI/ML] 논문 청킹 RFC`.
- 역할을 바꿀 때는 직전 역할의 산출물을 참조하고, 어떤 결정을 이어받았는지 문서 상단에 기록.
- 역할 간 충돌(예: PM이 원하는 기능 vs Architect의 기술 제약)은 **ADR** 로 해결.

## 3. 의사결정

| 유형 | 방식 |
|------|------|
| 가역적·영향 범위 작음 | 바로 진행, 문서 업데이트 |
| 비가역적·영향 범위 큼 | ADR 작성 (`00_meta/adr/`) |
| 팀 외부와 공유 필요 | RFC 작성 (`04_architecture/rfc/`) |

## 4. 산출물 성숙도

모든 주요 문서는 상태(frontmatter)를 가집니다.

- **Draft** — 작성자가 혼자 탐색 중. 바뀔 수 있음.
- **Review** — 리뷰 대기. 피드백 수용 가능.
- **Approved** — 합의된 현재 기준. 변경 시 PR 필요.
- **Deprecated** — 대체됐거나 폐기. 이유와 대체 문서 링크 명시.

## 5. 커뮤니케이션 기본값
- 문서 언어: 한국어. 고유명사·기술 용어는 원어 허용.
- 문서 내 작성 주체 명시 (누가 썼고, 누가 리뷰했는지 frontmatter).
- 정기 회고: 각 Phase 종료 시 `06_evaluation/reports/phaseN_retro.md`.
