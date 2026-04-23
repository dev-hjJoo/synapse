---
status: Draft
owner: Eval Lead
version: 0.1
last_updated: 2026-04-24
---

# Golden Set Plan

AI 품질의 **자동 회귀 평가 기준**. 사람의 주관 없이 동일한 방식으로 반복 측정 가능해야 합니다.

## 1. 목표 규모

| 단계 | 규모 | 목적 |
|------|------|------|
| v0 (Phase 3 말) | 50 | 첫 릴리즈 게이트 |
| v1 (Phase 5) | 120 | MVP 회고 |
| v2 (MVP 이후) | 200+ | 정기 회귀 |

## 2. 쿼리 구성

### 2.1 쿼리 유형 분포 (v0 = 50건)

| 유형 | 건수 | 예시 |
|------|------|------|
| 개념 설명 | 12 | "이 논문에서 contrastive loss는 무엇인가?" |
| 수식 풀이 | 8 | "수식 (3)이 어떻게 유도되나?" |
| 방법론 요약 | 7 | "제안 방법을 단계별로 요약" |
| 결과 해석 | 5 | "Table 2가 의미하는 바는?" |
| 인용 · 참고문헌 탐색 | 5 | "저자가 prior work로 인용한 논문은?" |
| 구현 단서 | 5 | "이 방법을 구현하려면 무엇이 필요한가?" |
| 외부 탐색 | 3 | "이 논문의 후속 연구를 찾아줘" |
| 범위 밖 거부 | 5 | "이 논문 저자의 이메일은?" |

### 2.2 논문 샘플

- **도메인**: ML/NLP(15), Bio/Medicine(10), Physics(8), CS Systems(7), Social Sciences(5), Chemistry(5)
- **연도**: 최근 2년 중심 + 고전 5편
- **언어**: 영어 주력, 한국어 2편 포함
- **난이도**: 튜토리얼성 10, 메인스트림 25, 수학 집약 15

## 3. 레이블 스키마

```yaml
id: GS-0001
paper: arxiv:2401.12345
query: "이 논문의 주요 기여 3가지는?"
query_type: method_summary
difficulty: easy
level: practitioner
reference:
  - section: "1. Introduction"
    anchor: "page 1, paragraph 4"
    excerpt: "Our contributions are threefold..."
  - section: "Abstract"
    anchor: "page 1"
must_cite: true
acceptable_answers:
  covers:
    - "novel architecture"
    - "benchmark gains"
    - "open-sourced code"
forbidden:
  - "저자 이메일 · 연락처"
notes: "저자 자기 기술. 해석 여지 거의 없음."
version: 1
```

- **증거는 텍스트 전체가 아닌 포인터** (섹션·페이지·짧은 excerpt). 길이 편향 방지.
- `acceptable_answers.covers` 는 **키 포인트 세트**. LLM-as-judge · 사람 평가 모두 이 체크리스트로 채점.
- `level` 은 대상 사용자 수준 — 답변 톤 평가에 사용.

## 4. 채점 루브릭

| 지표 | 정의 | 방법 |
|------|------|------|
| Faithfulness | 답변이 원문 근거에 충실(환각 없음) | RAGAS + 사람 스팟 |
| Citation Accuracy | 인용한 페이지·단락이 실제로 맞음 | 자동 매칭 + 사람 스팟 |
| Coverage | `covers` 키 포인트 중 포함 비율 | LLM-as-judge + 사람 |
| Refusal Appropriateness | 범위 밖 쿼리에 거부·명확화 적절성 | LLM-as-judge |
| Latency | 첫 토큰 · 완료 시간 | 자동 |
| Cost | LLM · 임베딩 · 검색 합계 | 자동 |

각 점수는 [0, 1]. 가중 합계 = **Quality Score**.

## 5. 생성·검수 워크플로우

```
1. 초안 (작성자)                → 쿼리·참조·기대 답변 스케치
2. 동료 리뷰 (또는 24h 간격 셀프 재검토) → 모호성·누락 확인
3. 동결 (version: 1)               → 해시 고정, 변경 금지
4. 정기 재검토 (분기)              → 필요 시 새 version으로 갱신
```

## 6. 자동 평가 러너

- 위치: `05_src/evals/` (Phase 4 구축)
- 실행: CI (PR + 야간) · 로컬
- 입력: 골든셋 파일 + 대상 빌드 hash
- 출력: JSON 리포트 + Langfuse 연결
- **회귀 게이트**: PR에서 Quality Score 하락 ≥ 5% 경고, ≥ 10% 차단

## 7. 사람 스팟 체크

- 주간 10건 무작위 샘플
- 독립 2인 채점 → 불일치는 표준화 라운드로 해소
- 결과: `06_evaluation/reports/weekly-YYYY-WW.md`

## 8. 오픈 질문

- **저작권** — 골든셋에 원문 excerpt를 어느 길이까지 담을 수 있나 (fair use 범위)? 법률 검토 별도.
- **익명화** — 일부 논문의 저자 이메일 등 공개 개인정보 처리 정책.
- **언어별 편향** — 한국어 논문 결과가 영어 대비 과소/과대 측정될 가능성.

## 9. References

- [`metrics_framework.md`](metrics_framework.md)
- [`interview_protocol.md`](interview_protocol.md)
- RAGAS: https://docs.ragas.io/
- TREC COVID / MS MARCO — QA 평가셋 설계 참고
