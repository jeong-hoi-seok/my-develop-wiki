---
id: convention-lint-format
title: 린트·포맷 컨벤션
aliases: [린트·포맷 컨벤션]
type: convention
status: active
created_at: 2026-07-10
created_by: 정회석
updated_at: 2026-07-10
updated_by: 정회석
audit_log:
  - action: created
    at: 2026-07-10
    by: 정회석
    note: "2026-07-10 프론트팀 회의 결정. 사내 공용 ESLint+Prettier 표준에 consistent-type-imports 추가"
tags: [common, convention, eslint, prettier, lint, format]
stack: common
scope: lint-format
source: "https://typescript-eslint.io/rules/consistent-type-imports (조회 2026-07-10)"
relations:
  - id: convention-naming-convention
    label: related
    note: "네이밍 자동 검증도 린트가 담당"
---

# 린트·포맷 컨벤션

## 한 줄 요약

팀 공통 린터는 **ESLint + Prettier**다. 이 문서는 개발 프로젝트 전부에 적용하는 **범용 베이스**만 정한다. 프레임워크 전용 규칙은 각 프로젝트가 이 베이스 위에 알아서 얹는다.

## 원칙

1. **역할 분리.** Prettier는 포맷, ESLint는 코드 품질. 같은 일을 두 도구가 하지 않는다. Prettier는 ESLint 규칙으로 돌리지 않고 에디터 저장과 CI에서 직접 실행한다.
2. **import 정렬은 Prettier가 한다.** `@trivago/prettier-plugin-sort-imports` 담당. ESLint 쪽 정렬 규칙은 켜지 않는다. 둘 다 켜면 서로 고친 걸 되돌린다.
3. 프레임워크 전용은 각 프로젝트에서 설정하고, 여기서는 범용적인 부분들을 설정한다.
4. **프로젝트 확장은 자유, 완화는 신중히.** 규칙 추가는 자유. 베이스 규칙을 끄거나 낮출 때는 그 프로젝트 문서에 사유를 남긴다.

## 도구와 버전

- **ESLint 10**: 코드 품질 검사. JS 린트 생태계 표준이고, 10부터 flat config 전용이라 설정 방식이 하나로 통일된다.
- **Prettier 3**: 코드 포맷. 스타일 논쟁을 도구로 종결한다. import 정렬 플러그인 최신 버전이 3을 요구한다.

메이저만 고정하고 마이너·패치는 최신 안정을 따른다. 플러그인들은 두 메이저와의 peerDependencies 호환을 확인하고 설치한다. 2026-07-10 npm registry 기준 아래 설정의 플러그인 전부 호환 확인함.

## Prettier

기본값과 같은 옵션도 전부 명시한다. 개인 설정이 다른 사람에게도 같은 결과를 강제하고, 메이저 업그레이드로 기본값이 바뀌어도 팀 스타일이 유지된다.

```js
const config = {
  semi: true,
  bracketSameLine: false,
  bracketSpacing: true,
  endOfLine: 'lf',
  jsxSingleQuote: false,
  quoteProps: 'as-needed',
  singleQuote: true,
  trailingComma: 'all',
  printWidth: 100,
  tabWidth: 2,
  plugins: ['@trivago/prettier-plugin-sort-imports'],
  importOrder: ['<THIRD_PARTY_MODULES>', '^@/(.*)$', '^[.]/', '^[.]{2,}/'],
  importOrderCaseInsensitive: true,
  importOrderSortSpecifiers: true,
  importOrderSeparation: true,
  importOrderSideEffects: false,
};

export default config;
```

### 옵션 설명

| 옵션                | 값             | 효과                                         |
| ----------------- | ------------- | ------------------------------------------ |
| `semi`            | `true`        | 문장 끝 세미콜론 강제                               |
| `bracketSameLine` | `false`       | 여러 줄 JSX의 닫는 `>`를 다음 줄로 내림                 |
| `bracketSpacing`  | `true`        | 객체 리터럴 중괄호 안 공백 `{ foo }`                  |
| `endOfLine`       | `'lf'`        | 줄바꿈 LF 통일. Windows CRLF 섞임으로 인한 diff 오염 방지 |
| `jsxSingleQuote`  | `false`       | JSX 속성은 큰따옴표. HTML 관례와 일치                  |
| `quoteProps`      | `'as-needed'` | 객체 키 따옴표는 필요한 키에만                          |
| `singleQuote`     | `true`        | JS 문자열은 작은따옴표                              |
| `trailingComma`   | `'all'`       | 여러 줄 마지막 요소 뒤에도 쉼표. 항목 추가 시 diff가 한 줄만 나옴  |
| `printWidth`      | `100`         | 줄 길이 100자                                  |
| `tabWidth`        | `2`           | 들여쓰기 2칸                                    |

### import 정렬

`@trivago/prettier-plugin-sort-imports`가 저장 시 import 블록을 재배열한다.

| 순서 | 패턴 | 대상 |
|---|---|---|
| 1 | `<THIRD_PARTY_MODULES>` | 패턴에 안 걸린 외부 패키지. `react`, `@tanstack/react-query` 등 |
| 2 | `^@/(.*)$` | `@/` 시작 프로젝트 alias. `@/components` 등 |
| 3 | `^[.]/` | 같은 폴더 상대 경로. `./utils` 등 |
| 4 | `^[.]{2,}/` | 상위 폴더 상대 경로. `../hooks` 등 |

- `importOrderCaseInsensitive`: 그룹 안에서 대소문자 무시 알파벳 정렬.
- `importOrderSortSpecifiers`: `{ b, a }` → `{ a, b }`처럼 중괄호 안 이름도 정렬.
- `importOrderSeparation`: 그룹 사이에 빈 줄을 넣어 경계를 눈으로 구분.
- `importOrderSideEffects: false`: `import './globals.css'`, `import 'react-native-gesture-handler'`처럼 **순서 자체가 의미인 side-effect import는 원래 자리에 둔다.** 기본값 true면 이런 import까지 재배열돼 CSS cascade나 초기화 순서가 깨진다.
- alias 패턴은 `@/` 기준이다. 스코프 패키지가 alias 그룹에 섞이지 않게 `^@(.*)$` 대신 `^@/(.*)$`를 쓴다. 다른 alias 형태를 쓰는 프로젝트는 자기 설정에서 패턴을 바꾼다.

## ESLint

ESLint 10 flat config 기준.

```js
import js from '@eslint/js';
import prettierConfig from 'eslint-config-prettier/flat';
import { importX } from 'eslint-plugin-import-x';
import tseslint from 'typescript-eslint';

export const sharedConfig = [
  js.configs.recommended,
  ...tseslint.configs.recommended,
  importX.flatConfigs.typescript,
  {
    files: ['**/*.{js,mjs,cjs,ts,mts,cts,jsx,tsx}'],
    rules: {
      'no-console': ['warn', { allow: ['error'] }],
    },
  },
  {
    rules: {
      'no-undef': 'off',
      '@typescript-eslint/no-unused-vars': ['warn', { argsIgnorePattern: '^_' }],
      '@typescript-eslint/no-explicit-any': 'warn',
      '@typescript-eslint/consistent-type-imports': 'error',
      'import-x/no-duplicates': 'warn',
    },
  },
  prettierConfig,
];
```

`eslint-plugin-prettier`는 쓰지 않는다. Prettier를 ESLint fix로 실행하면 정렬 플러그인의 텍스트 이동 fix와 no-duplicates 병합 fix가 같은 import 블록에서 충돌해, `eslint --fix` 한 번에 **사용 중인 import가 조용히 삭제되는 것을 재현으로 확인했다.** 2026-07-10 검증. 충돌 규칙 해제는 `eslint-config-prettier`가 담당하고, 포맷 실행은 에디터 저장과 CI의 Prettier가 직접 한다.

### 구성 블록 설명

| 블록                               | 역할                                                                                               |
| -------------------------------- | ------------------------------------------------------------------------------------------------ |
| `js.configs.recommended`         | JS 기본 오류 검출. 중복 키, 도달 불가 코드, 비교 실수 등                                                             |
| `tseslint.configs.recommended`   | TypeScript 권장 세트. TS 전용 버그 패턴 검출.                                                                |
| `importX.flatConfigs.typescript` | import-x 플러그인 등록과 TS 해석 설정. 경로·이름 검증은 TS 컴파일러가 담당하므로 recommended 세트는 켜지 않고, 아래 no-duplicates만 쓴다 |
| `prettierConfig`                 | Prettier와 충돌하는 ESLint 포맷 규칙을 전부 끈다. **반드시 배열 마지막**                                              |

### 개별 규칙 설명

| 규칙                                           | 수준                        | 이유                                                 |
| -------------------------------------------- | ------------------------- | -------------------------------------------------- |
| `no-console`                                 | warn, `console.error`만 허용 | 디버그 로그가 배포 번들에 남는 것 방지. 오류 기록은 허용                  |
| `no-undef`                                   | off                       | 미정의 참조는 TS 컴파일러가 더 정확히 잡는다. ESLint 쪽은 TS 전역 타입에 오탐 |
| `@typescript-eslint/no-unused-vars`          | warn, `_` 프리픽스 무시         | 미사용 변수 검출. 의도적으로 안 쓰는 인자는 `_`로 표시                  |
| `@typescript-eslint/no-explicit-any`         | warn                      | `any`는 타입 검사 무력화. 금지가 아니라 경고로 두고 리뷰에서 판단           |
| `@typescript-eslint/consistent-type-imports` | error                     | 타입 전용 import를 `import type`으로 강제. 아래 근거 참고         |
| `import-x/no-duplicates`                     | warn                      | 같은 모듈을 두 줄로 import하면 한 줄로 병합 유도.                   |


## 셋팅 방법

### 설치

typescript가 설치된 프로젝트를 전제한다. tseslint와 TS resolver가 요구한다.

```bash
pnpm add -D eslint @eslint/js typescript-eslint \
  eslint-plugin-import-x eslint-import-resolver-typescript \
  eslint-config-prettier \
  prettier @trivago/prettier-plugin-sort-imports
```

`eslint-import-resolver-typescript`는 `importX.flatConfigs.typescript`가 요구한다. 없으면 파일마다 Resolve error 경고가 붙는다.

### 파일 배치

| 파일 | 내용 | git |
|---|---|---|
| `eslint.config.mjs` | 위 ESLint 설정 | 커밋 |
| `prettier.config.mjs` | 위 Prettier 설정 | 커밋 |
| `.prettierignore` | 아래 ignore | 커밋 |
| `.vscode/settings.json` | 아래 VSCode 설정 | 커밋. 팀 전체가 같은 에디터 동작을 공유한다 |
| `.vscode/extensions.json` | 아래 확장 권장 목록 | 커밋. 프로젝트 열 때 VSCode가 설치를 권유한다 |

### ignore

ESLint 10은 `.eslintignore` 파일을 지원하지 않는다. flat config 안 `ignores` 블록으로 지정한다.

```js
// eslint.config.mjs 배열 맨 앞에 추가
{ ignores: ['dist/', 'build/', 'coverage/'] },
```

Prettier는 `.prettierignore`를 쓴다. `node_modules`는 두 도구 다 기본 무시라 적지 않는다.

```
dist
build
coverage
pnpm-lock.yaml
```

`.next/`, `.expo/`, `android/`, `ios/` 같은 프레임워크 산출물은 해당 프로젝트에서 추가한다.

## VSCode 설정

`.vscode/settings.json`에 커밋한다. 저장 한 번으로 ESLint 자동 수정과 Prettier 포맷이 순서대로 걸리는 설정값이다. VSCode는 codeActions를 먼저, 포맷을 나중에 실행하므로 ESLint가 고친 코드를 Prettier가 마지막에 정리한다.

두 설정 모두 **명시적 저장에서만** 동작한다. autoSave의 afterDelay로 저장되는 경우엔 적용되지 않으므로 자동 적용을 기대하면 직접 저장한다.

```jsonc
{
  "editor.tabSize": 2,
  "editor.detectIndentation": false,
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit"
  },
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    "typescript",
    "typescriptreact"
  ],
  "eslint.workingDirectories": [{ "mode": "auto" }],
  "typescript.tsdk": "node_modules/typescript/lib",
  "prettier.requireConfig": true
}
```

확장이 없으면 위 설정은 아무 동작도 하지 않는다. `.vscode/extensions.json`을 함께 커밋해 설치를 유도한다.

```json
{
  "recommendations": ["esbenp.prettier-vscode", "dbaeumer.vscode-eslint"]
}
```

| 설정 | 효과 |
|---|---|
| `editor.tabSize` + `detectIndentation: false` | 들여쓰기 2칸 고정. 파일마다 다른 들여쓰기를 에디터가 추측하지 않는다 |
| `editor.formatOnSave` + `defaultFormatter` | 저장 시 Prettier 실행. 포맷 주체를 Prettier 확장으로 고정 |
| `editor.codeActionsOnSave` | 저장 시 ESLint 자동 수정 실행. 포맷과 별개로 코드 품질 수정 담당 |
| `eslint.validate` | JS·JSX·TS·TSX 전부 ESLint 검사 대상으로 지정 |
| `eslint.workingDirectories: auto` | ESLint 실행 기준 폴더를 자동 인식. 하위 폴더에 별도 설정이 있는 구조에서도 동작 |
| `typescript.tsdk` | 에디터가 전역 TS 대신 프로젝트에 설치된 TS 버전을 쓴다. 버전 차이로 인한 오탐 방지 |
| `prettier.requireConfig` | Prettier 설정 파일이 있는 프로젝트에서만 포맷 동작. 팀 설정 없는 곳에서 확장 기본값으로 제멋대로 바꾸는 사고 방지 |


## 관련 문서

- [[naming-convention]]
- [[code-review]]
