---
id: operation-wiki-authoring-guide
title: 위키 작성 가이드
aliases: [위키 작성 가이드]
type: operation
status: active
created_at: 2026-07-01
created_by: 정회석
updated_at: 2026-09-23
updated_by: 정회석
audit_log:
  - action: created
    at: 2026-07-01
    by: 정회석
  - action: updated
    at: 2026-07-02
    by: 정회석
  - action: updated
    at: 2026-07-02
    by: 정회석
    note: "relations 단방향·객체 전용으로 개정"
  - action: updated
    at: 2026-07-02
    by: 정회석
    note: "10_raw 제거 반영, 경로 예시 교체"
  - action: updated
    at: 2026-07-02
    by: 정회석
    note: "AGENTS 중복 제거로 문서 기본 구조·stack 참조 우선순위 이관"
  - action: updated
    at: 2026-07-10
    by: 정회석
    note: "파일명 예시를 expo-sdk-version으로 갱신"
  - action: updated
    at: 2026-07-10
    by: 정회석
    note: "파일명 예시에서 expo 항목을 log-writing-guide로 교체"
  - action: updated
    at: 2026-09-23
    by: 정회석
    note: "worklog 경량 메타데이터·README 예외·과거 기록 보존 기준 반영"
  - action: updated
    at: 2026-09-23
    by: 정회석
    note: "사용자 요청에 따른 외부 저장소 식별정보와 비교 문구 제거"
tags: [common, convention, wiki]
stack: common
scope: wiki-authoring
source:
  - "사용자 개인 위키 개선 요청, 2026-09-23"
relations:
  - id: operation-wiki-versioning
    label: related
  - id: operation-agent-instruction-guide
    label: related
  - id: operation-project-wiki-guide
    label: related
---
# wiki-authoring-guide

## 한 줄 요약

일반 위키 문서의 **파일명·frontmatter·경로 표기 표준**입니다. my-develop-wiki와 소비 프로젝트의 위키 문서에 적용하며, 원본 보관소와 작업 기록은 아래 예외를 따릅니다.

## 적용 범위

- **적용**: my-develop-wiki의 `/20_wiki/`·`/00_context/`, 소비 프로젝트 `docs/`의 일반 위키 문서.
- **원본 예외**: my-develop-wiki의 `/10_raw/`와 소비 프로젝트의 `docs/raw/`. 원본에 문서 형식 강제 없음.
- **작업 기록 예외**: my-develop-wiki와 소비 프로젝트 모두 `docs/worklog/`의 경로·파일명·본문·frontmatter·기록 간 관계는 [[worklog-writing-guide]] 적용. 전체 위키 메타데이터 요구 없음.
- **안내 파일 예외**: 루트 `README.md`와 `docs/worklog/README.md`는 [[project-wiki-guide]]의 고정 안내 형식 적용. frontmatter 불필요.
- **기존 기록**: 과거 단일 파일·날짜별 로그·옛 메타데이터에 새 형식을 일괄 소급 적용하지 않음. 구버전 감지·미병합 기록 이관·원문 보존은 [[project-wiki-guide]]의 마이그레이션 절차 적용.

## 문서 기본 구조

```md
# 제목

## 한 줄 요약

## 핵심 내용

## 관련 문서
- [[]]

## 출처
-
```

## 파일명 규칙

- **영어, 전부 소문자, kebab-case.** 공백 대신 하이픈(`-`). 확장자 `.md`.
- 기술 고유명도 소문자로: `expo`, `fsd`, `mr`, `msw`.
- 한글은 파일명에 쓰지 않는다. 한글 제목은 frontmatter `title`로 보존한다.
- 예: `코드 리뷰` → `code-review.md`, `로그 작성 규칙` → `log-writing-guide.md`

## Frontmatter

**필수** (하나라도 없으면 안 됨):

| 키 | 값 |
|---|---|
| `id` | `<type>-<파일명>` — 파일명 기준 고유 식별자 (예: `operation-log-writing-guide`) |
| `title` | 한글 제목 — 사람이 읽는 이름, 영문 파일명의 짝 |
| `type` | 아래 [type 값](#type-값) 중 하나 |
| `status` | `active` / `draft` / `pending` / `superseded` / `collapsed` / `deprecated` / `archived` |
| `created_at` · `created_by` | 생성일 `YYYY-MM-DD` · 생성자(git author 이름) |
| `updated_at` · `updated_by` | 마지막 수정일 · 마지막 작업자 1명 |
| `audit_log` | 문서 액션 이력, 아래 [audit_log](#audit_log) |
| `tags` | 리스트 (예: `[common, operation, wiki]`) |
| `aliases` | `[한글 제목]` — `[[한글 제목]]` 위키링크가 그대로 열린다 |
| `stack` | `common` / `web` / `app` (기존 `platform` 대체) |
| `scope` | 문서 주제 슬러그 (예: `log-authoring`) |
| `relations` | 다른 위키 문서와의 명시적 관계, 아래 [relations](#relations) |

**선택**:

- `last_verified_at` · `last_verified_by` — 내용을 검증한 시점·검증자.
- `code_refs` — 코드 파일 참조. `{file, note?}` 객체 리스트.
- `source` 등 문서 성격에 맞게 추가.

### stack 참조 우선순위

프로젝트에 플랫폼이 명시돼 있으면 해당 `stack` 문서 + `common`을 우선 참조한다. 불명확하면 `common`부터.

### relations

`{id, label, note?}` 객체만 허용. plain 문자열(느슨한 참조)은 쓰지 않는다. `id`는 상대 문서의 frontmatter `id`(파일명 기준). label 표준: `related` / `depends-on` / `supersedes` / `superseded-by`.

**단방향으로 선언한다.** 관계는 한쪽에서만 선언하고 역방향 중복 선언은 금지.

- 방향: **참조하는 쪽이 선언한다** — 의존하는 문서, 또는 나중에 생긴 문서.
- 선언할 관계가 없으면 `relations: []`로 명시한다.

```yaml
relations:
  - id: operation-wiki-versioning
    label: related
    note: "선택 — 관계 맥락 한 줄"
  - id: convention-naming-convention
    label: depends-on
```

### audit_log

문서 관련 액션을 시간순으로 쌓는다. `action`은 `created` / `updated` / `verified` / `superseded` / `archived`.

```yaml
audit_log:
  - action: created
    at: 2026-07-01
    by: 홍길동
    note: "선택 — 변경 사유 한 줄"
  - action: updated
    at: 2026-07-02
    by: 홍길동
```

- 문서를 수정하면 `updated_at`·`updated_by` 갱신과 함께 `audit_log`에 항목을 **반드시 추가**한다.

### 실제 사용 예시

```yaml
---
id: operation-log-writing-guide
title: 로그 작성 규칙
aliases: [로그 작성 규칙]
type: operation
status: active
created_at: 2026-07-01
created_by: 정회석
updated_at: 2026-07-02
updated_by: 정회석
audit_log:
  - action: created
    at: 2026-07-01
    by: 정회석
    note: "일 단위 로그 규칙"
  - action: updated
    at: 2026-07-02
    by: 정회석
    note: "작성자 표기·버전 괄호 형식 도입, 커밋 해시 제거, 압축 기준일 명확화"
tags: [common, operation, wiki, log]
stack: common
scope: log-authoring
relations:
  - id: operation-wiki-authoring-guide
    label: related
  - id: operation-wiki-versioning
    label: related
  - id: operation-project-wiki-guide
    label: related
---
```

## type 값

| type | 용도 |
|---|---|
| `index` | 진입점 목차 (`index.md`) |
| `log` | 구버전 이력 문서에만 사용. 신규 worklog는 별도 경량 형식 |
| `concept` | 지식·개념·아키텍처 |
| `decision` | 기술 선택·결정 이유 |
| `convention` | 개발 산출물에 적용하는 규칙 (`/20_wiki/conventions/`) |
| `operation` | 개발 외 운영 규약·가이드 (`/20_wiki/operations/`) |
| `context` | 개인 정적 기준 (`/00_context/`) |

## 경로·링크 표기

에이전트가 참조를 바로 따라갈 수 있게 쓴다. 백틱 경로는 검색이 필요하지만 링크는 즉시 열린다.

### 저장소 안 파일 → 마크다운 링크 (필수)

my-develop-wiki 안에 실제로 존재하는 **파일**을 언급하면 백틱이 아니라 마크다운 링크로 쓴다.

- 링크 텍스트 = 저장소 루트 기준 경로 그대로, target = `/`로 시작하는 루트 절대경로.
- 상대경로(`../`, `./`) target 금지 — 문서 위치가 바뀌면 깨지고, 에이전트가 기준점을 헷갈린다.

```md
✅ [20_wiki/operations/wiki-versioning.md](/20_wiki/operations/wiki-versioning.md)
❌ `20_wiki/operations/wiki-versioning.md`
❌ [wiki-versioning](../operations/wiki-versioning.md)
```

- 같은 문서에서 같은 파일을 반복 언급하면 **처음 한 번만 링크**하고, 이후엔 `index.md`처럼 짧은 백틱 표기를 허용한다.

### 디렉토리 → 백틱 + 루트 절대경로

디렉토리는 링크하지 않고 백틱으로 쓰되 경로는 `/`로 시작한다: `/00_context/`, `/20_wiki/conventions/`.

### 저장소 밖 경로 → 백틱 유지

링크를 걸 파일이 이 저장소에 없으므로 링크 금지. 그대로 백틱.

- 소비 프로젝트의 파일: `docs/worklog/README.md`, `.gitignore`
- 일반 코드 예시: `android/`, `shared/api`, `app/`
- git 참조: `origin/main`, `vX.Y.Z`

### 문서 간 개념 연결 → `[[Wikilink]]` 유지

`/20_wiki/` 문서끼리의 개념 연결은 기존대로 `[[파일명]]`. 경로 링크는 "이 파일을 열어라"는 지시일 때만 쓴다.

### 모호한 지칭 금지

에이전트가 무엇을 가리키는지 즉시 알 수 없는 표현을 쓰지 않는다.

| ❌ 금지 | ✅ 대체 |
|---|---|
| 본진 | my-develop-wiki, 또는 실제 경로 |
| 상위 문서, `상위: [[index]]` 꼬리표 | 삭제 — index는 유일한 진입점이라 역참조 불필요 |
| 이 위키, 여기 | my-develop-wiki, 개별 프로젝트 `docs/` 등 명시 |

## 파일명 마이그레이션 절차

한글 파일명을 영문으로 바꿀 때:

1. `git mv`로 영어 kebab-case로 rename.
2. frontmatter에 `title`(한글)·`aliases`(한글) 추가하고 `updated_at`·`audit_log` 갱신.
3. 인바운드 `[[한글]]` 링크는 `aliases`로 자동 해결되지만, 가능하면 `[[영문]]`으로 갱신해 일관성을 유지한다.
4. `index.md`와 현재 안내 문서의 참조를 갱신하고 해당 worklog에 변경 기록을 남긴다. 과거 기록은 수정하지 않으며, 기존 경로 참조는 새 기록에 이전·새 경로를 남겨 추적한다. 링크 lint로 현재 안내의 깨짐 0을 확인한다.

## 관련
[[wiki-versioning]] · [[agent-instruction-guide]] · [[project-wiki-guide]]
