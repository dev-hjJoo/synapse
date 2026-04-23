# ADR-0001: 아키텍처 결정은 ADR로 기록한다

- **Status**: Accepted
- **Date**: 2026-04-24
- **Deciders**: Owner

## Context
Synapse는 기획·디자인·아키텍처·AI·평가가 모두 연쇄적으로 얽힌 시스템이다. 결정의 근거가 대화·슬랙·머릿속에만 남으면, 이후 왜 그런 선택을 했는지 복원하기 어렵고 신규 참여자의 온보딩 비용이 커진다.

## Decision
비가역적이거나 영향 범위가 넓은 결정은 모두 **ADR(Architecture Decision Record)** 형식으로 `00_meta/adr/` 에 남긴다. 번호는 `NNNN` 4자리 제로 패딩.

## Rationale
- 저비용 · 저마찰: 텍스트 파일 한 개
- 버전 관리와 잘 어울림 (git 로그로 결정 히스토리 추적)
- 신규 합류자가 "왜 이렇게 되어 있는가"를 스스로 파악 가능

## Alternatives Considered
- **Notion/Confluence 위키만 사용** — 코드 저장소와 분리되어 드리프트 위험, 버전 히스토리 약함
- **커밋 메시지만 사용** — 결정 자체보다 변경 설명에 치우침, 포맷 일관성 부족

## Consequences
- (+) 결정의 근거·대안·트레이드오프가 보존됨
- (+) 리뷰 단위가 명확 (ADR 단위로 Accept/Reject)
- (−) 작성 오버헤드 → 큰 결정에만 쓰고, 작은 결정은 문서 본문으로

## References
- 템플릿: `00_meta/adr/0000-adr-template.md`
- Michael Nygard, "Documenting Architecture Decisions" (2011)
