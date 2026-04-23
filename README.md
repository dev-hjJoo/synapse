# Synapse

> AI 에이전트가 논문을 깊이 이해하도록 돕고, 관련 자료를 연결해 주며,
> 다음 행동(구현·실험·후속 리서치)까지 이어주는 웹 플랫폼.

[![Docs first](https://img.shields.io/badge/stage-docs--first-informational)](00_meta/WORKFLOW.md)
[![Phase](https://img.shields.io/badge/phase-1%20discovery-blue)](02_product/ROADMAP.md)
[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

---

## 왜 만드나요

논문을 둘러싼 워크플로우는 네 단계로 나뉩니다 — **발견 → 저장 → 이해 → 행동**. 현재의 도구들은 대부분 셋 중 하나만 잘합니다. 정작 "**읽은 뒤에 무엇을 할 것인가**" 의 간극은 비어 있습니다.

Synapse는 그 간극을 메우려 합니다.

- **이해 보조** — 어려운 수식·용어·맥락을 사용자 수준에 맞춰 설명합니다.
- **연결** — 인용 논문·구현 코드·후속 자료를 한 자리에서 탐색합니다.
- **행동** — "이 아이디어를 내 프로젝트에 적용", "최소 재현 코드 작성", "팀 공유용 요약 생성" 같은 다음 스텝을 실제로 돕습니다.

## 지금 어디쯤인가요

**Phase 1 — Discovery.** 사용자 인터뷰와 경쟁 분석을 진행합니다. 실행 코드는 아직 없습니다. 대신 **기획·디자인·아키텍처·평가 문서가 먼저 공개적으로 쌓입니다.**

진행 상황은 [`02_product/ROADMAP.md`](02_product/ROADMAP.md) 에서 언제든 확인할 수 있습니다.

## 저장소 지도

| 경로 | 무엇이 있나요 | 주 오너 |
|------|--------------|---------|
| [`00_meta/`](00_meta/) | 팀 헌장 · 워크플로우 · 아키텍처 결정 기록(ADR) | 전체 |
| [`01_research/`](01_research/) | 시장·경쟁사·사용자 리서치 | UX Researcher, PM |
| [`02_product/`](02_product/) | 비전 · PRD · 로드맵 · 유저 스토리 | PM |
| [`03_design/`](03_design/) | 정보 구조(IA) · 와이어프레임 · 디자인 시스템 | Designer |
| [`04_architecture/`](04_architecture/) | 기술 스택 · 시스템 RFC · 다이어그램 | Architect |
| [`05_src/`](05_src/) | 실제 구현 (Phase 4 이후) | Dev · AI/ML |
| [`06_evaluation/`](06_evaluation/) | 정량·정성 평가 프레임워크·결과 | Eval Lead |

## 처음 읽기 좋은 순서

1. [**비전**](02_product/VISION.md) — 어떤 문제를, 누구를 위해, 왜 지금 푸나요
2. [**팀 헌장**](00_meta/TEAM_CHARTER.md) — 역할과 책임
3. [**워크플로우**](00_meta/WORKFLOW.md) — Phase·문서 성숙도·결정 방식
4. [**기술 스택 제안**](04_architecture/tech_stack.md) — 어떤 구조로 짓나요
5. [**평가 프레임워크**](06_evaluation/metrics_framework.md) — 성공은 어떻게 측정하나요
6. [**경쟁 지형도**](01_research/competitive_landscape.md) — 어디에 서 있나요

## 에이전트 팀 (역할 기반)

Synapse는 현재 **단일 오너** 가 주도하지만, 작업 단위로 아래 역할의 "모자" 를 바꿔 쓰는 방식으로 진행합니다. 합류하시면 역할 단위로 오너십을 재분배합니다.

- **PM** — 비전 · PRD · 로드맵 · 우선순위
- **UX Researcher** — 사용자 인터뷰 · 페르소나 · 여정
- **Product Designer** — IA · 와이어프레임 · 디자인 시스템
- **Architect** — 시스템 구조 · RFC · ADR
- **Backend / Frontend Dev** — 실행 코드
- **AI / ML Engineer** — 에이전트 그래프 · 검색 · 프롬프트 · 평가
- **Evaluation Lead** — 정량 메트릭 · 정성 인터뷰 분석 · 릴리즈 게이트

자세한 내용은 [`00_meta/TEAM_CHARTER.md`](00_meta/TEAM_CHARTER.md).

## 어떻게 기여하나요

- **아이디어 / 방향성 제안** → [`Proposal` 이슈](../../issues/new?template=proposal.md)
- **질문 / 토론** → [`Discussion` 이슈](../../issues/new?template=discussion.md) 또는 Discussions
- **오탈자 / 링크 / 사실 오류** → [`Doc Fix` 이슈](../../issues/new?template=doc_fix.md) 또는 Pull Request

커밋 메시지 형식(`[역할] 요약`)·PR 체크리스트 등 자세한 규칙은 [CONTRIBUTING](CONTRIBUTING.md) 을 참고해 주세요. 모든 상호작용은 [Code of Conduct](CODE_OF_CONDUCT.md) 를 따릅니다.

## 라이선스

[MIT License](LICENSE). 기여하신 내용도 동일 라이선스로 공개됩니다.

## 감사

Synapse는 많은 선행 도구·연구에 빚지고 있습니다 — arXiv, Semantic Scholar, Zotero, SciSpace, Elicit, NotebookLM, LangGraph, Claude Agent SDK, 그리고 오픈 리서치 커뮤니티. 구체 인용은 관련 문서에 분산되어 있습니다.
