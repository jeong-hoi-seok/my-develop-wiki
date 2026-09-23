---
id: convention-git-hooks
title: Git Hook 컨벤션
aliases: [Git Hook 컨벤션]
type: convention
status: active
created_at: 2026-07-10
created_by: 정회석
updated_at: 2026-09-23
updated_by: 정회석
audit_log:
  - action: created
    at: 2026-07-10
    by: 정회석
    note: "2026-07-10 프론트팀 회의 결정. Husky 규격화, pre-commit nano-staged, pre-push typecheck"
  - action: updated
    at: 2026-09-23
    by: 정회석
    note: "개인 코드 프로젝트에 hook 적용 범위 한정, 기존 도구·런타임·검사 존중"
  - action: updated
    at: 2026-09-23
    by: 정회석
    note: "사용자 요청에 따른 외부 저장소 식별정보와 비교 문구 제거"
tags: [common, convention, git, husky, nano-staged, hook]
stack: common
scope: git-hooks
source:
  - "https://typicode.github.io/husky, https://github.com/usmanyunusov/nano-staged (조회 2026-07-10)"
  - "사용자 개인 위키 개선 요청, 2026-09-23"
relations:
  - id: convention-lint-format
    label: depends-on
    note: "pre-commit이 lint-format의 ESLint·Prettier 설정을 실행한다"
---
# Git Hook 컨벤션

## 한 줄 요약

개인 JS/TS 프로젝트가 Git hook을 도입할 때는 **Husky**와 **nano-staged**를 기본으로 쓴다. pre-commit은 staged 파일의 린트·포맷, pre-push는 프로젝트가 정의한 **typecheck**를 실행한다. 기존 hook은 프로젝트 규칙을 우선하며, 코드가 없는 위키에는 이 구성을 일괄 설치하지 않는다.

## 적용 범위

프로젝트에 해당 검사 스크립트가 있을 때만 연결한다. TypeScript를 쓰지 않는 프로젝트에 typecheck를 형식적으로 추가하지 않는다. hook은 로컬 검증이며, 채택한 CI 검사를 대신하지 않는다. 아래 예시는 nvm을 쓰는 환경 기준이므로 다른 버전 관리자는 해당 프로젝트에 맞춘다.

## 셋업

```bash
pnpm add -D husky nano-staged
pnpm exec husky init
```

`husky init`이 `package.json`에 `prepare` 스크립트를 넣고 `.husky/pre-commit`을 만든다. 생성된 pre-commit의 기본 내용은 아래 스크립트로 교체한다.

### package.json

```json
{
  "scripts": {
    "prepare": "husky",
    "typecheck": "tsc --noEmit"
  },
  "nano-staged": {
    "*.{js,jsx,ts,tsx,mjs,cjs}": ["eslint --fix", "prettier --write"],
    "*.{json,md,yml,yaml,css}": "prettier --write"
  }
}
```

### hook 스크립트

두 hook 모두 nvm 로딩 스니펫으로 시작한다. VSCode·Fork·Sourcetree 같은 GUI git 클라이언트는 hook을 실행할 때 shell init을 타지 않아 nvm 환경이 없고, pnpm을 못 찾아 hook이 실패한다. `.nvmrc`가 있으면 저장소 Node 버전을 직접 로드해 이 문제를 막는다([[node-version]]).

`.husky/pre-commit`:

```sh
#!/usr/bin/env sh

# shell init을 타지 않는 hook 환경에서 저장소 Node 버전을 로드한다.
if [ -f ".nvmrc" ]; then
  export NVM_DIR="${NVM_DIR:-$HOME/.nvm}"

  if [ -s "$NVM_DIR/nvm.sh" ]; then
    . "$NVM_DIR/nvm.sh"
    nvm use --silent >/dev/null
  fi
fi

pnpm nano-staged
```

`.husky/pre-push`:

```sh
#!/usr/bin/env sh

# shell init을 타지 않는 hook 환경에서 저장소 Node 버전을 로드한다.
if [ -f ".nvmrc" ]; then
  export NVM_DIR="${NVM_DIR:-$HOME/.nvm}"

  if [ -s "$NVM_DIR/nvm.sh" ]; then
    . "$NVM_DIR/nvm.sh"
    nvm use --silent >/dev/null
  fi
fi

pnpm typecheck
```

두 파일 모두 커밋한다. `set -e`는 쓰지 않는다. nvm.sh가 non-zero를 리턴하는 경우가 있어 hook이 엉뚱한 지점에서 죽고, 실질 명령이 하나뿐이라 마지막 exit code로 충분하다.

## 동작 방식

| 시점 | 대상 | 명령 | 이유 |
|---|---|---|---|
| pre-commit | staged 파일만 | `eslint --fix` 후 `prettier --write` | 코드 품질 수정 먼저, 포맷 마무리 나중. [[lint-format]] 검증에서 확인한 안전 순서다. 고친 내용은 그대로 커밋에 포함된다 |
| pre-commit | json·md·yml·css | `prettier --write` | 코드가 아니라 린트는 불필요, 포맷만 통일 |
| pre-push | 프로젝트 전체 | `pnpm typecheck` | 타입 오류는 파일 하나만 봐서는 못 잡는 전역 검사라 staged 단위와 안 맞는다. 커밋마다 돌리면 느리므로 push 시점에 1회 |

**스크립트 이름 `typecheck`는 hook과의 계약이라 고정이고, 명령은 프로젝트 구성에 맞게 정한다.**

## 관련 문서

- [[lint-format]]

## 출처

- Husky: https://typicode.github.io/husky
- nano-staged: https://github.com/usmanyunusov/nano-staged
