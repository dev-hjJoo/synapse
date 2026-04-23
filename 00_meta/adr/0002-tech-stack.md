# ADR-0002: 기술 스택 (Proposed)

- **Status**: Proposed
- **Date**: 2026-04-24
- **Deciders**: Architect, AI/ML Engineer
- **Supersedes**: —
- **Related**: `04_architecture/tech_stack.md`

## Context

Synapse는 (1) PDF 파싱·구조화, (2) 벡터 검색 기반 대화 에이전트, (3) 웹 검색·인용 그래프 통합, (4) 스트리밍 UX, (5) 비동기 파이프라인을 요구한다. 동시에 **MVP를 빠르게 검증**해야 하며, 과도한 인프라 복잡도는 기피한다.

## Decision

아래 스택을 **기본값**으로 채택한다. 각 항목은 Phase 4 진입 전 재확인하며, 중대한 변경 사항이 생기면 Superseding ADR로 대체한다.

| 영역 | 선택 |
|------|------|
| Frontend | Next.js 15 (App Router) + TypeScript + Tailwind + shadcn/ui |
| Server state | TanStack Query |
| Backend | Python 3.12 + FastAPI |
| 관계형 DB | PostgreSQL 16 |
| 벡터 | pgvector (동일 Postgres 인스턴스) |
| 풀텍스트 | Postgres `tsvector` (하이브리드 검색) |
| 캐시·큐 | Redis + Celery (필요 시 RQ로 경량화) |
| 스토리지 | S3 호환 (Cloudflare R2 기본) |
| LLM | Claude 계층화 — Opus / Sonnet / Haiku |
| Agent | Claude Agent SDK 1차, 복잡 그래프 발생 시 LangGraph 부분 도입 |
| 임베딩 | Voyage `voyage-3-large` |
| 리랭커 | Cohere Rerank v3 또는 LLM-as-judge |
| 웹 검색 | Tavily 또는 Exa |
| 인용 그래프 | Semantic Scholar API |
| PDF 파싱 | Docling (IBM) |
| 관측 | Langfuse + PostHog + Sentry |
| 인증 | Clerk 1차 (대안 Supabase Auth) |
| 호스팅 | Vercel (FE) + Fly.io/Railway (BE) |

세부 근거와 트레이드오프는 `04_architecture/tech_stack.md`.

## Rationale

- **Python 백엔드**: AI 생태계가 파이썬 중심. 단일 언어 런타임이 디버깅·배포를 단순화.
- **pgvector**: MVP 단계에서 관계형+벡터를 한 DB에 두면 JOIN·운영이 용이. 성능 한계에 도달하면 벡터 분리 마이그레이션은 표준 경로 존재.
- **Claude 계층화**: 품질이 필요한 질의는 Opus, 일반은 Sonnet, 라우팅·분류는 Haiku로 비용·지연을 관리.
- **Docling**: 과학 논문의 수식·표·참고문헌 분리에 상대적으로 강함 (2024 오픈소스 리뷰 기준).
- **Langfuse**: 자가호스팅 가능한 LLM 관측. 비용·품질·트레이스를 한 곳에서.

## Alternatives Considered

- **Next.js API Routes 단일 스택** — AI 라이브러리 다양성·장기 성능에서 열세. 기각.
- **Pinecone/Weaviate 단독 벡터 DB** — 초기 운영 복잡도·비용 대비 이점이 아직 불분명. MVP엔 과대. 기각.
- **LangGraph 전면 채택** — 단순 툴콜 루프엔 오버엔지니어링. 복잡도가 증가한 시점에 부분 도입.
- **OpenAI + Assistants API 단일 의존** — 모델 락인·비용 구조가 장기적으로 불리. Claude 우선, 타 모델은 필요 시 어댑터로.
- **Supabase 풀스택 (Auth + Postgres + Storage)** — MVP 가속 매력적이나 벤더 락인 리스크. 스코프 재평가 후 별도 ADR로 결정.

## Consequences

**긍정**
- 단순·일관된 런타임 (Python BE / TS FE)
- 비용 관리 레버 (모델 계층화·하이브리드 검색)
- 관측·평가가 초기부터 연결된 설계

**부정 / 트레이드오프**
- Next.js에서 AI 로직을 직접 호출 불가 → 두 런타임 유지 비용
- pgvector가 극단적 스케일에선 한계 (수억 벡터 이상)
- Clerk 사용 시 벤더 의존

**재검토 조건**
- 사용자 100k+ 혹은 벡터 10M+ 도달
- 지연(p95 > 8s)이 LLM이 아닌 검색에서 발생
- 기관·SSO 요구가 출시 전 필수화

## References
- `04_architecture/tech_stack.md`
- Langfuse docs: https://langfuse.com/docs
- pgvector: https://github.com/pgvector/pgvector
- Docling: https://github.com/DS4SD/docling
