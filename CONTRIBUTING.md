# Contributing to Synapse

Synapse는 **공개 개발(open development)** 을 지향합니다. 제품 기획·디자인·아키텍처·평가 문서가 코드보다 먼저 이곳에 쌓입니다. 피드백·제안·질문 모두 환영합니다.

이 문서는 기여 방법을 짧게 정리합니다. 팀 운영 규칙은 [`00_meta/TEAM_CHARTER.md`](00_meta/TEAM_CHARTER.md), 작업 흐름은 [`00_meta/WORKFLOW.md`](00_meta/WORKFLOW.md) 를 참고해 주세요.

## 참여 방법

| 하려는 일 | 권장 경로 |
|-----------|-----------|
| 방향성·아이디어 제안 | **Issue** — `Proposal` 템플릿 |
| 질문·자유로운 토론 | **Issue** — `Discussion` 템플릿 또는 **GitHub Discussions** |
| 문서 오탈자·링크 깨짐·사실 오류 | **Issue** — `Doc Fix` 템플릿 또는 **Pull Request** |
| 사용자 인터뷰 참여 | 모집 공지는 추후 이슈/README에 고지됩니다 |

작은 수정(오탈자 · 링크)은 바로 PR로 보내주셔도 됩니다.

## Pull Request 가이드

1. **브랜치**를 만들어 작업합니다. 브랜치 이름은 `type/topic` 권장 (예: `docs/vision-v2`, `feat/agent-graph`).
2. 커밋 메시지는 [Conventional Commits](https://www.conventionalcommits.org/) 를 따르며 **영문**으로 작성합니다. 자세한 규칙은 아래 "커밋 메시지 규칙" 섹션.
3. PR을 열 때 아래 체크리스트를 확인해 주세요.
   - [ ] 변경한 문서의 `frontmatter` (`last_updated`, 필요 시 `status`·`version`)를 업데이트했나요?
   - [ ] 관련 ADR·RFC가 있다면 상호 참조 링크를 추가했나요?
   - [ ] 링크 깨짐·마크다운 렌더 오류가 없는지 로컬에서 확인했나요?
   - [ ] 개인 식별 정보(PII) 또는 민감 데이터가 포함되지 않았나요?

## 커밋 메시지 규칙

### 형식

```
<type>(<scope>): <subject>

[optional body]

[optional footer]
```

- **제목(subject)** — 영문 명령형(imperative), 소문자 시작, 마침표 없음, 50자 이내 권장.
- **본문(body)** — 한 줄 띄우고 시작, 72자에서 줄바꿈. **왜(why)** 를 중심으로.
- **Breaking change** — `type!` 또는 footer `BREAKING CHANGE: ...`.

### Type

| Type | 용도 |
|------|------|
| `feat` | 새 기능·제품 산출물 추가 |
| `fix` | 버그·오탈자·깨진 링크 수정 |
| `docs` | 문서 추가·수정 (docs-first 단계 대부분) |
| `refactor` | 동작 변경 없는 구조 개선 |
| `test` | 테스트·평가셋 변경 |
| `chore` | 설정·의존성·CI 등 유지보수 |
| `style` | 포맷팅만 |

### Scope

폴더·역할 기준.

| Scope | 대상 |
|-------|------|
| `meta` | `00_meta/` (charter · workflow · ADR infra) |
| `adr` | 개별 ADR |
| `research` | `01_research/` |
| `product` | `02_product/` |
| `design` | `03_design/` |
| `arch` | `04_architecture/` (RFC 포함) |
| `agents` | `05_src/agents/` |
| `backend` · `frontend` | `05_src/` 하위 |
| `eval` | `06_evaluation/` |
| `infra` | 배포·Docker·CI |

### 예시

```
docs(product): add vision v0.1
docs(research): draft competitive landscape
docs(adr): accept ADR-0002 tech stack
chore: add public repo scaffolding (license, coc, templates)
fix(docs): correct broken link in roadmap
feat(agents): implement paper chunking service
```

## 문서 작성 원칙

- **한국어 우선**, 기술 용어·고유명사는 원어 허용.
- 모든 주요 문서는 상단에 `frontmatter` (status · owner · version · last_updated).
- 큰 결정은 [`ADR`](00_meta/adr/) · 큰 설계 제안은 [`RFC`](04_architecture/rfc/) 로.
- 템플릿에 포함된 대괄호 값(`[연구 담당자 이메일]` 등)은 **개인이 직접 사용할 때** 본인 정보로 치환해 주세요. 레포에는 항상 템플릿 형태를 유지합니다.

## 개인정보·리서치 윤리

- 사용자 인터뷰 **원본 녹취·노트·참여자 명단**은 레포에 커밋하지 않습니다 (`.gitignore` 로 차단).
- 공개 리포트에는 항상 **익명화된 요약**만 실립니다.
- 실명·이메일·소속 등 PII가 포함된 PR은 병합 전에 수정 요청드릴 수 있습니다.

## 라이선스

이 저장소는 [MIT License](LICENSE) 를 따릅니다. 기여하신 내용도 동일 라이선스로 공개됩니다. 라이선스 변경이 필요한 의견이 있다면 이슈로 열어 주세요.

## 행동 강령

기여자는 [Code of Conduct](CODE_OF_CONDUCT.md) 를 준수해 주세요. 요약: **서로 존중하고, 사실에 근거해 대화하며, 초심자의 질문을 환영합니다.**
