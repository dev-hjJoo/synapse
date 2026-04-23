---
status: Draft
owner: PM
version: 0.1
last_updated: 2026-04-24
---

# 로드맵

시점 목표 없이, **마일스톤별 완료 기준(DoD)** 으로 관리합니다.

---

## M0 — Scaffolding  ✅
**DoD**
- [x] 디렉토리 구조
- [x] 팀 헌장 (`00_meta/TEAM_CHARTER.md`)
- [x] 워크플로우 (`00_meta/WORKFLOW.md`)
- [x] 비전 (`02_product/VISION.md`)
- [x] PRD 스켈레톤
- [x] 기술 스택 제안
- [x] 평가 프레임워크 초안 (정량·정성)

---

## M1 — Discovery
**DoD**
- [ ] 5–8명 사용자 인터뷰 완료, `01_research/user_interviews/` 에 익명 노트
- [ ] 페르소나 2–3개 (`01_research/personas.md`)
- [ ] 경쟁사·대체 도구 분석 5건 이상 (`01_research/competitive_landscape.md`)
- [ ] 문제 진술문 1개로 수렴 (`01_research/problem_statement.md`)
- [ ] 가설 세그먼트 중 **우선순위 세그먼트** 결정

---

## M2 — Definition
**DoD**
- [ ] PRD v1 **Approved** (`02_product/PRD.md`)
- [ ] 북극성 지표·부지표 확정 → `06_evaluation/metrics_framework.md` 업데이트
- [ ] 기술 스택 ADR **Accepted** (`00_meta/adr/0002-*`)
- [ ] 로드맵 v1 (이 문서) 갱신

---

## M3 — Design
**DoD**
- [ ] IA + 주요 플로우 와이어프레임 (`03_design/wireframes/`)
- [ ] 하이파이 프로토타입 5–8 화면 (Figma 링크 `03_design/README.md`에 기록)
- [ ] 디자인 시스템 v0 (토큰·핵심 컴포넌트)
- [ ] 시스템 다이어그램 + 핵심 RFC 3–5개 Approved (`04_architecture/rfc/`)

---

## M4 — Build (MVP)
**DoD**
- [ ] 로컬 실행 가능한 end-to-end MVP
- [ ] 핵심 플로우 1개 통과: **PDF 업로드 → 이해 대화 → 다음 스텝 제안 1종**
- [ ] 평가 파이프라인 가동 (Langfuse + 골든셋 50개)
- [ ] 관측: Sentry · PostHog · Langfuse 연결

---

## M5 — Evaluate
**DoD**
- [ ] 8–10명 사용성 인터뷰 완료 및 녹취·노트 저장
- [ ] 정량 대시보드 작동 (활성·리텐션·AI 품질)
- [ ] 평가 리포트 발행 (`06_evaluation/reports/phase5_summary.md`)
- [ ] Next-Steps 백로그 도출

---

## M6+ — Iterate
리포트 결과에 따라 우선순위 재조정. 가능 후보:
- 브라우저 확장
- 팀 공유·권한
- 모바일 리더
- 한국어 논문·번역 대응 강화
