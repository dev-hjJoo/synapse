---
status: Proposed
owner: Architect
version: 0.1
last_updated: 2026-04-24
---

# 기술 스택 제안 (Proposed)

> 이 문서는 **제안**입니다. 최종 확정은 `00_meta/adr/0002-tech-stack.md` (작성 예정)에서.

## 결정 요약 (TL;DR)

| 영역 | 기본 선택 | 이유 |
|------|----------|------|
| Frontend | Next.js 15 (App Router) + TypeScript | 스트리밍 UX·SSR·생태계 |
| UI | Tailwind + shadcn/ui | 빠른 프로토타이핑·접근성 |
| Backend | Python 3.12 + FastAPI | AI/ML과 같은 런타임·생태계 |
| DB | PostgreSQL + pgvector | 관계 + 벡터 한 DB |
| 스토리지 | S3 호환 (R2 or S3) | PDF 원본 |
| 큐 | Redis + Celery (or RQ) | 비동기 파싱·임베딩 |
| LLM | Claude (Opus/Sonnet/Haiku 계층) | 장문 추론·안전·비용 트레이드 |
| Agent | Claude Agent SDK → 필요 시 LangGraph | 단순에서 출발, 복잡할 때 확장 |
| 임베딩 | Voyage `voyage-3-large` | 과학 문서 검색 성능 |
| 웹 검색 | Tavily 또는 Exa | 신선도·학술 성향 |
| PDF 파싱 | Docling (IBM) | 수식·표·참고문헌 분리 |
| 인용 그래프 | Semantic Scholar API | 무료·광범위 |
| 관측 | Langfuse + PostHog + Sentry | LLM·프로덕트·에러 |
| 인증 | Clerk 또는 Supabase Auth | 이메일 + OAuth |
| 호스팅 | Vercel (FE) + Railway/Fly (BE) | 초기 단순성 |
| 공용 대안 | Supabase 통합 검토 | MVP 가속 vs 락인 |

## 프론트엔드

**Next.js 15 (App Router) + TypeScript**
- RSC·스트리밍이 에이전트 응답 UX에 자연스럽게 맞음
- SEO·공유 가능한 페이지(아티팩트·공개 노트) 고려

**Tailwind CSS + shadcn/ui**
- 초기 속도·접근성 기본, 디자인 시스템 이관 용이

**상태 관리**
- 서버: TanStack Query
- 클라이언트: Zustand 또는 Jotai (최소한으로)

## 백엔드

**Python 3.12 + FastAPI**
- AI 코드와 API가 한 런타임 → 배포·디버깅 단순
- 타입·pydantic·자동 문서화

**PostgreSQL + pgvector**
- 관계형 데이터(사용자·문서·노트·세션)와 벡터(청크 임베딩)를 한 DB에
- 초기 복잡도 낮음, 나중에 Weaviate/Pinecone로 분리 가능

**Redis + Celery / RQ**
- PDF 파싱·임베딩·웹 검색 파이프라인 비동기 처리
- 단순 작업은 FastAPI BackgroundTasks로 먼저 가다가 전환

**S3 호환 스토리지**
- 기본: Cloudflare R2 (egress 비용 유리)
- 대안: AWS S3

## AI / Agent

### LLM 계층화
| 용도 | 기본 모델 |
|------|-----------|
| 깊은 추론·합성 | Claude Opus (claude-opus-4-7) |
| 일반 대화·요약·설명 | Claude Sonnet (claude-sonnet-4-6) |
| 라우팅·분류·짧은 발췌 | Claude Haiku (claude-haiku-4-5) |

### 에이전트 프레임워크
- 1차: **Claude Agent SDK** — 단순한 툴콜·반복 루프에 적합
- 2차: **LangGraph** — 복잡한 상태 그래프(이해 에이전트가 여러 서브에이전트·재시도·분기 필요 시)

### 검색·RAG
- 임베딩: **Voyage `voyage-3-large`** (과학 문서 성능)
- 리랭커: **Cohere Rerank** 또는 자체 LLM-as-judge 리랭커
- 하이브리드 검색: BM25(Postgres `tsvector`) + 벡터 결합

### 도구 통합
- **Tavily** / **Exa** — 웹 검색
- **Semantic Scholar API** — 인용 그래프
- **arXiv API** — 최신 프리프린트
- **GitHub Code Search** — 구현 탐색

### PDF → 구조화
- **Docling** (IBM, 2024) — 수식·표·참고문헌 분리 양호
- 폴백: **Unstructured** 또는 **GROBID**

## 관측·평가
- **Langfuse** — LLM 트레이싱·비용·품질 메트릭
- **PostHog** — 이벤트·퍼널·리텐션·세션 리플레이
- **Sentry** — 에러·성능

## 배포·인프라
- **Vercel** — 프론트엔드
- **Railway / Fly.io** — FastAPI (GPU는 필요 시 Modal 또는 RunPod)
- **Supabase 검토** — 인증+Postgres+pgvector+Storage를 한 번에 묶을 경우 MVP 가속. 벤더 락인 리스크는 ADR에서 평가.

## 인증
- **Clerk** (드랍인 UX, 통합 쉬움) 또는 **Supabase Auth**
- 이메일 + Google OAuth 1차, 기관 SSO는 후순위

## 개발 경험
- 패키지: `pnpm` (FE), `uv` 또는 `poetry` (BE)
- 린트·포맷: `biome` 또는 `eslint`+`prettier` · `ruff`+`mypy`
- Pre-commit, GitHub Actions CI
- Docker Compose로 로컬 통합 환경

## 트레이드오프 요약

| 선택 | 대안 | 왜 이 선택 |
|------|------|-----------|
| FastAPI (Python) | Next.js API 단일 | AI 라이브러리가 파이썬 중심. 장기 서빙 성능·디버깅. |
| pgvector | Pinecone/Weaviate | MVP 복잡도 ↓. 관계·벡터 JOIN 용이. 성능 한계 오면 분리. |
| Claude Agent SDK | LangGraph 전체 | 오버엔지니어링 방지. 복잡 플로우에만 부분 도입. |
| Voyage 임베딩 | OpenAI/Cohere | 과학 도메인 벤치마크에서 경쟁력. 비용 합리적. |
| Supabase 검토 | 자체 호스팅 | MVP 가속. 락인 리스크는 ADR에서 대응 경로 명시. |

## 오픈 이슈 (ADR로 해결 필요)
1. **논문 저작권** — 사용자 업로드 PDF의 저장·공유 정책
2. **기본 모델 라우팅 정책** — 모든 질의를 Sonnet으로? Haiku로 라우팅 후 Opus로 승격?
3. **원격 / 로컬 모델** — 기관 사용자를 위한 self-host 경로
4. **데이터 거주(residency)** — 한국 사용자·연구 데이터 해외 전송 이슈
5. **비용 상한** — 사용자당 월 LLM 비용 상한·강제 정책
