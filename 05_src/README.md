# 05_src — 소스 코드

실제 구현은 **Phase 4 (M4 — Build)** 부터 이 폴더에 등장합니다. 그 전까지는 설계 문서(`04_architecture/`)와 디자인(`03_design/`)이 선행됩니다.

## 예정 구조

```
05_src/
├── frontend/      Next.js 15 (App Router, TypeScript)
├── backend/       FastAPI (Python 3.12)
├── agents/        에이전트 그래프·프롬프트·툴 (Backend에서 import)
├── infra/         Docker Compose, 배포 스크립트
└── evals/         평가 골든셋·자동 평가 러너
```

## 규칙 (미리)
- 타입 엄격 (TS strict, mypy strict)
- 테스트: 핵심 비즈니스 로직 + AI 평가 러너
- 환경변수: `.env.example` 커밋, `.env` 는 git-ignore
- CI: lint · typecheck · test · build를 PR에서 전부

## 시작 전 점검
M4 진입 직전, 다음이 갖춰졌는지 확인:
- [ ] PRD v1 Approved
- [ ] 핵심 RFC 3–5개 Approved
- [ ] 디자인 프로토타입 Approved
- [ ] 기술 스택 ADR Accepted
- [ ] 평가 골든셋 50개 이상
