---
status: Draft
owner: Eval Lead
version: 0.1
last_updated: 2026-04-24
---

# 평가 프레임워크 — 정량 (Quantitative)

정성 평가는 `interview_protocol.md` 참고.

## 계층

### 1. 북극성 지표 (Phase 1 이후 확정)
**주간 활성 사용자당 "insight-to-action" 전환 수** (가설)

정의 초안: "논문을 연 세션 중, 읽은 뒤 다음 행동(구현 시작·아티팩트 생성·공유·저장된 후속 질의 실행)으로 이어진 세션의 비율 × 주간 활성 사용자".

### 2. Product Health

| 지표 | 정의 | MVP 목표 |
|------|------|----------|
| Activation Rate | 가입 후 7일 내 논문 1편 완독 + 에이전트 1회 이상 상호작용 | ≥ 50% |
| WAU / MAU | 주간/월간 활성 비율 | ≥ 40% |
| D7 Retention | 가입 후 7일 재방문율 | ≥ 25% |
| D30 Retention | 가입 후 30일 재방문율 | ≥ 15% |
| Median Session Length | 중앙값 세션 길이 | ≥ 8분 |

### 3. Feature Engagement

| 지표 | 정의 |
|------|------|
| Papers per user / week | 세션당 평균 논문 수 |
| Chat turns per paper | 논문당 에이전트 질의 횟수 |
| Web search triggers | 외부 자료 검색 호출 비율 |
| Citation click-through | 답변 인용을 실제로 열람한 비율 |
| Next-step acceptance | 제안된 다음 스텝을 실행한 비율 |

### 4. AI 품질 (전용 평가셋 기반)

| 지표 | 측정 | 목표 |
|------|------|------|
| Faithfulness | 답변이 원문 근거에 충실한가 (RAGAS + 사람 스팟) | ≥ 0.85 |
| Citation Accuracy | 인용한 페이지·단락의 정확도 | ≥ 0.90 |
| Answer Relevance | 질의 대비 관련도 (LLM-as-judge + 샘플 사람) | ≥ 0.80 |
| Latency p50 / p95 | 스트리밍 첫 토큰까지 지연 | ≤ 2s / ≤ 6s |
| Cost per session | LLM·임베딩·검색 합산 비용 | 목표치는 ADR에서 |

### 5. UX · 만족도

| 지표 | 방법 |
|------|------|
| SUS (System Usability Scale) | 사용성 인터뷰 후 10문항 |
| NPS | 분기별 in-app 설문 |
| Task Success Rate | 사용성 테스트 시나리오 완수율 ≥ 80% |
| Time on Task | 시나리오별 소요 시간 |

## 측정 도구

- **PostHog** — 이벤트·퍼널·리텐션·세션 리플레이
- **Langfuse** — LLM 트레이스·비용·자동 품질 점수
- **자체 평가 러너** — 골든셋 기반 정기 회귀 테스트 (`05_src/evals/`)
- **인터뷰 SUS·NPS** — `06_evaluation/reports/`에 요약

## 평가셋 (Golden Set)
- 초기 50개 → Phase 5까지 200개 목표
- 질의 유형 분포:
  - 개념 설명 · 수식 풀이 · 방법론 요약 · 결론 해석 · 인용 탐색 · 구현 단서 찾기
- 정답은 **참조 섹션·페이지**로 기록 (완전한 텍스트가 아닌 증거 포인터)
- 분기별 재라벨링 회의

## 릴리즈 게이트 (예시)
MVP → v1 승격 체크리스트:

- [ ] Faithfulness ≥ 0.85
- [ ] Citation Accuracy ≥ 0.90
- [ ] p95 지연 ≤ 6s
- [ ] Task Success Rate ≥ 80% (사용성 테스트)
- [ ] 사용자당 월 LLM 비용 ≤ $X (ADR에서 X 결정)
- [ ] 크리티컬 Sentry 이슈 0

## 리포팅 주기

| 지표군 | 주기 |
|--------|------|
| Product Health · Engagement | 주간 자동 리포트 |
| AI 품질 | 주간 자동 + 월간 사람 스팟 |
| 사용성 · NPS | Phase 마일스톤마다 |
| 비용 | 주간 대시보드 + 월간 리뷰 |
