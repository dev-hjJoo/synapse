# Synapse

AI 에이전트가 논문을 깊이 이해하도록 돕고, 관련 자료를 연결해 주며, 다음 행동(구현·실험·후속 리서치)까지 이어주는 웹 플랫폼.

## 한 줄 비전
논문을 **읽는 도구**가 아니라, **이해의 스파크를 다음 행동으로 잇는** 플랫폼.

## 디렉토리 지도

| 경로 | 내용 | 주 오너 |
|------|------|---------|
| `00_meta/` | 팀 헌장, 워크플로우, 아키텍처 결정 기록(ADR) | 전체 |
| `01_research/` | 시장·경쟁사·사용자 리서치 | UX Researcher, PM |
| `02_product/` | 비전, PRD, 로드맵, 유저 스토리 | PM |
| `03_design/` | 정보구조(IA), 와이어프레임, 디자인 시스템 | Designer |
| `04_architecture/` | 기술 스택, 시스템 설계 RFC, 다이어그램 | Architect |
| `05_src/` | 실제 코드 (백엔드·프론트엔드·에이전트) | Dev, AI/ML |
| `06_evaluation/` | 정량·정성 평가 프레임워크·결과 | Eval Lead |

## 현재 단계
**Phase 0 — 스캐폴딩 완료.** 다음은 Phase 1 (Discovery): 사용자 리서치 + 시장 분석.

진행 상황은 [`02_product/ROADMAP.md`](02_product/ROADMAP.md) 참고.

## 시작하기

이 저장소는 **문서 우선(docs-first)** 으로 진화합니다. 코드는 Phase 4 이후 `05_src/` 에 등장합니다.

새로 합류하신 분이라면 아래 순서로 읽어보세요.

1. [`02_product/VISION.md`](02_product/VISION.md) — 이 프로젝트가 해결하려는 문제
2. [`00_meta/TEAM_CHARTER.md`](00_meta/TEAM_CHARTER.md) — 역할과 책임
3. [`00_meta/WORKFLOW.md`](00_meta/WORKFLOW.md) — Phase와 작업 흐름
4. [`04_architecture/tech_stack.md`](04_architecture/tech_stack.md) — 기술 스택 제안
5. [`06_evaluation/metrics_framework.md`](06_evaluation/metrics_framework.md) — 평가 지표

## 기여 규칙 요약
- 모든 문서는 버전 관리됩니다. 주요 결정은 `00_meta/adr/`에 ADR로 남깁니다.
- 커밋/PR 제목: `[역할] 요약` (예: `[PM] Synapse 비전 초안`).
- 큰 변경은 브랜치·PR로, 오탈자 수정은 main 직접 커밋 허용.
- 자세한 규칙은 [`00_meta/WORKFLOW.md`](00_meta/WORKFLOW.md).
