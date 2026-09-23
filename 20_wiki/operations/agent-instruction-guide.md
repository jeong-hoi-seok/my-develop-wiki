---
id: operation-agent-instruction-guide
title: 에이전트 지침 파일 작성 가이드
aliases: [에이전트 지침 파일 작성 가이드]
type: operation
status: draft
created_at: 2026-06-19
created_by: 정회석
updated_at: 2026-09-23
updated_by: 정회석
audit_log:
  - action: created
    at: 2026-06-19
    by: 정회석
  - action: updated
    at: 2026-07-02
    by: 정회석
  - action: updated
    at: 2026-07-02
    by: 정회석
    note: "relations 단방향 정리"
  - action: updated
    at: 2026-07-02
    by: 정회석
    note: "부트스트랩에 superpowers 설치 확인·gitignore 항목(docs/superpowers·.superpowers) 추가"
  - action: updated
    at: 2026-07-02
    by: 정회석
    note: "im-not-ai 윤문으로 축약어 머신차를 머신 차이로 풀어씀"
  - action: updated
    at: 2026-07-02
    by: 정회석
    note: "AGENTS 템플릿에 도구 활용 절 신설 context7 우선·superpowers 권장, CLAUDE.md 예시를 @AGENTS.md 한 줄 포인터로 교체"
  - action: updated
    at: 2026-07-07
    by: 정회석
    note: "AGENTS 템플릿에 작업 기록·MR/PR 필수 절 신설 — 작업 완료 시 worklog 기재, MR/PR 요청 시 mr-pr-guide 선행 숙지"
  - action: updated
    at: 2026-07-07
    by: 정회석
    note: "AGENTS 템플릿 도입부에 conventions·operations 선행 학습 필수 항목 추가"
  - action: updated
    at: 2026-07-07
    by: 정회석
    note: "템플릿 git 규칙을 보호 브랜치 일반화, branch-strategy 문서 참조 추가 — main 단일 가정 제거"
  - action: updated
    at: 2026-09-23
    by: 정회석
    note: "개인 프로젝트 지침·안전한 링크 연동·변경 단위 기록 반영, superpowers 의존 제거"
  - action: updated
    at: 2026-09-23
    by: 정회석
    note: "사용자 요청에 따른 외부 저장소 식별정보와 비교 문구 제거"
tags: [common, convention, agent]
stack: common
scope: agent-instruction-authoring
source:
  - "사용자 개인 위키 개선 요청, 2026-09-23"
relations:
  - id: operation-project-wiki-guide
    label: related
---
# 에이전트 지침 파일 작성 가이드

## 한 줄 요약

개인 프로젝트는 `~/my-develop-wiki`를 심볼릭링크로 참조하고, 실제 적용할 규칙은 프로젝트 `AGENTS.md`에 적습니다. 기록 도입과 기존 기록 전환은 [[project-wiki-guide]]를 따릅니다.

## 지침 파일

| 파일 | 역할 |
|---|---|
| `AGENTS.md` | 프로젝트 지침의 단일 기준. 위키 경로·실행 명령·브랜치·기록 방식을 명시 |
| `CLAUDE.md` | `AGENTS.md`를 읽는 포인터 |

기존 지침은 읽고 필요한 부분만 반영합니다. 프로젝트 고유 규칙을 템플릿으로 덮어쓰지 않고, 바꾼 내용을 사용자에게 알립니다. `CLAUDE.md`를 새로 만들 때는 아래 한 줄을 사용합니다.

```md
@AGENTS.md
```

## AGENTS.md 예시

```md
# AGENTS.md

모든 답변은 한국어로 작성한다. 개인 공통 기준은 my-develop-wiki를 참조하며,
이 프로젝트의 명시적 규칙이 우선한다.

- `./my-develop-wiki/20_wiki/index.md`를 먼저 읽는다.
- 미연동이면 위키의 `20_wiki/operations/agent-instruction-guide.md`에 따라 연동한다.
- index의 conventions·operations를 읽고 현재 프로젝트에 적용되는 기준을 확인한다.

## Git

실제 브랜치와 프로젝트 전략을 확인한다. 보호 브랜치에 직접 커밋·push하지 않는다.
커밋 전에 현재 브랜치를 확인하고 필요하면 작업 브랜치로 이동한다.
브랜치 기준은 `./my-develop-wiki/20_wiki/operations/branch-strategy.md`를 참조한다.
커밋·push·PR/MR·tag·Release는 요청받은 단계만 실행한다.
병합은 사용자가 직접 수행하며 에이전트는 merge·auto-merge를 실행하지 않는다.

## 작업 기록

도입·기존 기록 전환은 `./my-develop-wiki/20_wiki/operations/project-wiki-guide.md`를 따른다.
도입 후 기록 대상 결과가 생기면 `./my-develop-wiki/20_wiki/operations/worklog-writing-guide.md`에 따라
`docs/worklog/YYYY-MM/YYYY-MM-DD-<주제>-<식별자>.md`에 남긴다.
PR/MR 또는 독립 변경 하나당 기록 하나를 사용한다. 단순 조회·설명·상태 확인은 기록하지 않는다.
같은 변경의 미병합 기록을 재사용하며, 과거 맥락은 관련 메타데이터·본문만 검색한다.
구버전 기록은 프로젝트에 명시한 경로에서 보존하고 새 기록과 함께 조회한다.

## PR / MR

작성 요청을 받으면 `./my-develop-wiki/20_wiki/operations/mr-pr-guide.md`를 먼저 읽고
source·target·실제 diff·기존 요청 중복을 확인한 뒤 작성한다.

## 도구

라이브러리·프레임워크 문서는 Context7으로 대상 버전에 맞춰 조회한다.
사용자 지시와 프로젝트에서 채택한 도구·설정을 우선한다.
코드 리뷰 요청은 `./my-develop-wiki/20_wiki/conventions/code-review.md`를 따른다.
```

프로젝트가 실제 채택한 브랜치·패키지 매니저·실행 명령은 이 예시 아래에 구체적으로 적습니다. 위키를 연동했다는 이유로 기존 프로젝트의 도구나 브랜치를 바꾸지 않습니다.

## 위키 연동

1. `$HOME/my-develop-wiki`가 실제 위키 저장소인지 확인합니다. 없을 때만 아래 원격에서 clone합니다. 같은 이름의 다른 폴더가 있으면 덮어쓰지 않고 상태를 확인합니다.

   ```sh
   git clone https://github.com/jeong-hoi-seok/my-develop-wiki.git "$HOME/my-develop-wiki"
   ```

2. 소비 프로젝트 루트의 `my-develop-wiki` 경로를 확인합니다. 올바른 링크가 있으면 재사용하고, 경로가 없을 때만 생성합니다. 파일·디렉터리나 다른 링크가 있으면 강제 덮어쓰기 없이 대상부터 확인합니다. 위키 저장소 자체 안에는 자기 자신을 가리키는 링크를 만들지 않습니다.

   ```sh
   # macOS / Linux / WSL, 링크 경로가 없는 경우
   ln -s "$HOME/my-develop-wiki" ./my-develop-wiki
   ```

   ```powershell
   # Windows PowerShell, 링크 경로가 없는 경우
   New-Item -ItemType SymbolicLink -Path .\my-develop-wiki -Target "$HOME\my-develop-wiki"
   ```

3. 소비 프로젝트의 `.gitignore`에 링크와 로컬 도구 산출물 제외 항목을 유지합니다. 아래 산출물 제외는 도구 설치·사용을 요구하지 않습니다.

   ```gitignore
   my-develop-wiki
   docs/superpowers/
   .superpowers/
   ```

4. `./my-develop-wiki/20_wiki/index.md`가 실제로 열리는지 확인합니다. 링크 존재만으로 검증을 대신하지 않습니다. 실패하면 원인과 미확인 범위를 보고하고 링크 복구 전에는 연동 완료로 처리하지 않습니다.
5. [[wiki-sync]]에 따라 원격 상태를 확인하고 index를 읽습니다. [[project-wiki-guide]]에 따라 아직 승인되지 않은 기록 도입·전환만 확인합니다. 이미 요청·프로젝트 규칙으로 승인된 방식은 재확인 없이 적용합니다.

## 관련 문서

- [[project-wiki-guide]]
- [[worklog-writing-guide]]
- [[branch-strategy]]
- [[context7-instruction-guide]]
- [[code-review]]
