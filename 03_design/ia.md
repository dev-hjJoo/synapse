---
status: Draft
owner: Designer
version: 0.1
last_updated: 2026-04-24
---

# Information Architecture (Outline)

> Phase 3 디자인 스프린트에서 확정됩니다. 이 문서는 **초안 스케치**.

## 최상위 구조

```
Synapse
├── Library         내 논문 · 컬렉션 · 노트
├── Reader          단일 논문 몰입 공간 (본문 + AI + 다음 스텝)
├── Explorations    인용 그래프 · 주제 클러스터 · 최근 질의
└── Settings        프로필 · 사용자 수준 · 연동(Zotero 등) · 청구
```

**단 하나의 핵심 동사**: *Read*. 나머지는 모두 보조.

## 주요 엔티티

| 엔티티 | 설명 | 주요 속성 |
|--------|------|-----------|
| `Paper` | 논문 한 편 | source, title, authors, refs, chunks, status |
| `Collection` | 사용자가 묶은 논문 집합 | name, papers[], shared? |
| `Conversation` | 논문에 대한 질의응답 세션 | paper, turns[] |
| `Note` | 자유 노트 | paper?, content, tags[] |
| `Highlight` | 원문 구간 표시 | paper, span, comment? |
| `Artifact` | 생성물 (요약·슬라이드·스캐폴딩) | type, source_paper, content |
| `Citation` | AI 답변이 참조한 원문 포인터 | paper, section, page, span |

## 상위 플로우 5개

### F1 — Import → Read

```
[paste URL / upload / ext share]
   ↓
파싱 진행률 (SSE)
   ↓
Reader 열림 (본문 + 메타; AI 패널 닫힘)
```

### F2 — Ask & Cite

```
Reader에서 텍스트 선택
   ↓
[질문하기] → 사이드 패널에 AI 답변 스트리밍
   ↓
답변 내 인용 칩 클릭
   ↓
본문의 해당 위치로 스크롤 + 하이라이트
```

### F3 — Next Step

```
읽기 완료 신호 (도달·체류시간·사용자 트리거)
   ↓
[다음 스텝 제안] 3–5장 카드
   ↓
선택 (예: "구현 스캐폴딩")
   ↓
Artifact 생성 → 저장 / 외부 공유
```

### F4 — Explore Citations

```
Reader의 참고문헌 [N]
   ↓
카드: 제목·초록·Synapse에 있는지 여부
   ↓
[열기] → 새 Reader 탭 or 그래프 뷰
```

### F5 — Library Triage

```
Library 뷰 → 필터(최근·태그·미완독)
   ↓
논문 카드: 제목·진행률·마지막 질의·생성된 아티팩트
   ↓
[계속 읽기]
```

## URL 구조 (초안)

```
/                         → Library (로그인 시)
/p/{paper_id}             → Reader
/p/{paper_id}/chat/{id}   → 특정 대화 (공유 가능)
/p/{paper_id}/artifact/{id} → 산출물 (공유 가능)
/explore                  → Explorations
/c/{collection_id}        → Collection view
/settings                 → Settings
```

## 네비게이션 모델

- **좌측 사이드바 (앱 레벨)**: Library · Explorations · Settings
- **Reader 내부**
  - 상단: 논문 메타 · 북마크 · 공유
  - 좌측 rail: 섹션 아웃라인 · 하이라이트
  - 우측 패널 (기본 닫힘): AI 대화 · 인용 그래프 · 다음 스텝
  - 중앙: 본문

## 검색 범위

| 쿼리 대상 | 위치 |
|-----------|------|
| 현재 논문 내부 | Reader의 command palette |
| 내 라이브러리 전체 (본문·노트·대화) | 앱 전역 command palette |
| 외부 (웹·학술 DB) | 에이전트가 툴로 호출 (`web_search`, `academic_search`) |

## 오픈 질문

- Library와 Explorations를 분리할지, 한 뷰에서 필터로 처리할지 — Phase 3 프로토타이핑에서 확인.
- Conversation을 `Paper`에 귀속시킬지 독립 엔티티로 둘지 — 공유·전역 검색 요구에 따라 결정.
- 공유 링크의 **기본 가시성** (비공개 vs 공개) — VISION의 "신뢰" 가치와 정렬되도록.
- 수식·코드 블록을 노트에 인라인으로 삽입하는 방식 (LaTeX vs MathML vs 이미지).

## 관련 문서

- [`design_principles.md`](design_principles.md)
- [`02_product/VISION.md`](../02_product/VISION.md)
- [`04_architecture/`](../04_architecture/) — 엔티티 구현 세부
