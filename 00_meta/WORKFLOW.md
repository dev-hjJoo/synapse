---
status: Approved
owner: All
version: 0.1
last_updated: 2026-04-24
---

# 작업 흐름 (Workflow)

## Phase 개요

```
Phase 0 — Scaffolding            (✅ 완료)
   ↓
Phase 1 — Discovery
   UX Researcher · PM
   · 사용자 인터뷰 5–8명
   · 시장·경쟁사 분석
   산출물: 페르소나, 경쟁 지형도, 사용자 여정, 문제 진술
   ↓
Phase 2 — Definition
   PM · Architect
   · PRD v1, 우선순위
   · 기술 스택 ADR 확정
   · 북극성 지표 확정
   산출물: PRD Approved, ADR Accepted, Roadmap v1
   ↓
Phase 3 — Design
   Designer · Architect
   · IA, 와이어프레임, 하이파이 프로토타입
   · 디자인 시스템 v0
   · 핵심 RFC 3–5개
   산출물: 디자인 Approved, 시스템 RFC Approved
   ↓
Phase 4 — Build (MVP)
   Backend · Frontend · AI/ML · Eval
   · end-to-end MVP
   · 평가 파이프라인 가동
   산출물: 실행 가능한 MVP
   ↓
Phase 5 — Evaluate
   UX Researcher · Eval Lead
   · 사용성 인터뷰 8–10명
   · 정량 대시보드
   산출물: 평가 리포트, Next-Steps 백로그
   ↓
   (반복)
```

Phase별 **완료 기준(DoD)** 은 `02_product/ROADMAP.md`에.

## 문서 버전 관리

모든 주요 문서 상단에 frontmatter:

```yaml
---
status: Draft | Review | Approved | Deprecated
owner: PM           # 역할명
version: 0.1
last_updated: 2026-04-24
---
```

- 큰 변경 → 별도 브랜치 → PR → 머지
- 오탈자·링크 수정은 `main` 직접 커밋 허용
- `Approved` 문서 변경은 항상 PR (변경 이유를 PR 본문에)

## Commit / PR 규칙

- **모든 변경은 feature 브랜치 → Pull Request 를 통해 머지**. `main` 직접 커밋 금지.
- 커밋 메시지는 [Conventional Commits](https://www.conventionalcommits.org/) — `type(scope): subject` 형식, **영문**.
  - 예: `docs(product): add vision v0.1`, `docs(arch): propose embedding model RFC`
- PR 제목도 같은 형식 (CI 에서 검증). 본문에 **무엇을·왜** 변경했는지 기록.
- [CodeRabbit](https://coderabbit.ai/) 이 PR 을 자동 리뷰. Squash merge 권장.
- 자세한 형식·Type·Scope 표·개발 세팅은 [CONTRIBUTING](../CONTRIBUTING.md) 참고.
- PR 체크리스트:
  - [ ] frontmatter 업데이트 (`last_updated`, 필요 시 `status`/`version`)
  - [ ] 링크 깨짐 확인
  - [ ] 관련 ADR·RFC 교차 참조
  - [ ] `pre-commit run --all-files` 통과

## ADR (Architecture Decision Record)

- 번호: 4자리 제로 패딩 (`0001`, `0002`, …)
- 파일명: `0001-decision-title-in-kebab-case.md`
- 상태: `Proposed → Accepted / Rejected / Superseded`
- 템플릿: `00_meta/adr/0000-adr-template.md`

## RFC

시스템 설계·API·주요 AI 파이프라인 변경처럼 사전 합의가 필요한 제안.

- 위치: `04_architecture/rfc/`
- 파일명: `rfc-NNNN-title.md`
- 섹션: 배경 · 제안 · 대안 · 영향 · 리스크 · 롤아웃

## 회의·비동기 커뮤니케이션

- 결정이 일어난 대화는 반드시 문서·ADR로 흡수. 대화만 남기지 말 것.
- 비동기 리뷰 기본, 필요 시 짧은 싱크.
