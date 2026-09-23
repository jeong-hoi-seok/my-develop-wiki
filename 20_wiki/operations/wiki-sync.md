---
id: operation-wiki-sync
title: 위키 동기화
aliases: [위키 동기화]
type: operation
status: active
created_at: 2026-06-30
created_by: 정회석
updated_at: 2026-09-23
updated_by: 정회석
audit_log:
  - action: created
    at: 2026-06-30
    by: 정회석
  - action: updated
    at: 2026-07-02
    by: 정회석
  - action: updated
    at: 2026-09-23
    by: 정회석
    note: "GitHub 버전·커밋 비교, 미발행 버전과 작업 브랜치 변경 보존 기준 보완"
  - action: updated
    at: 2026-09-23
    by: 정회석
    note: "사용자 요청에 따른 외부 저장소 식별정보와 비교 문구 제거"
tags: [common, convention, wiki, sync]
stack: common
scope: wiki-sync
source:
  - "사용자 개인 위키 개선 요청, 2026-09-23"
relations:
  - id: operation-wiki-versioning
    label: related
  - id: index-index
    label: related
---
# 위키 동기화

## 한 줄 요약

GitHub Release·`origin/main`·현재 브랜치의 버전과 커밋을 비교합니다. 버전 불일치만으로 로컬 문서를 덮어쓰지 않습니다. 버전 변경·발행 절차는 [[wiki-versioning]]을 따릅니다.

## 확인 순서

my-develop-wiki 저장소에서 현재 브랜치·변경 파일을 확인하고 원격 참조를 갱신합니다.

```sh
git status --short --branch
git fetch origin main --tags
git rev-list --left-right --count HEAD...origin/main
gh release view --json tagName,targetCommitish,publishedAt,url
git show origin/main:20_wiki/index.md
```

[20_wiki/index.md](/20_wiki/index.md)의 `version`은 `X.Y.Z`, tag는 `vX.Y.Z`입니다. 작업 브랜치의 변경 이유·worklog도 함께 확인합니다. 버전 숫자가 같아도 커밋 차이가 있으면 같은 내용이라고 단정하지 않습니다.

## 상태별 처리

| 상태 | 처리 |
|---|---|
| 현재 브랜치가 `main`, 작업 트리가 깨끗하고 원격이 앞섬 | `git pull --ff-only origin main`으로 갱신 |
| 작업 브랜치 또는 로컬 수정이 있음 | 버전·커밋 차이를 보고하고 작업 보존. 임의 pull·reset·rebase 금지 |
| `origin/main`의 버전이 최신 Release보다 높음 | 미발행 변경인지 확인. tag·Release를 임의 생성하지 않음 |
| 현재 작업 브랜치에서 다음 버전을 준비 중 | worklog의 이전·새 버전과 이유 확인. 릴리즈와의 차이를 동기화 실패로 취급하지 않음 |
| 원격·Release 조회 실패 | 실패 원인과 확인 가능한 로컬 범위 보고. 최신이라고 단정하지 않음 |

`gh release view`는 마지막으로 발행된 GitHub Release를 확인하는 용도입니다. 발행할 때는 [[wiki-versioning]]에 따라 실제 병합 커밋과 같은 이름의 tag·Release 존재 여부를 별도로 확인합니다. 이 문서의 조회 절차 자체는 발행 권한을 부여하지 않습니다.

## 관련 문서

- [[index]]
- [[wiki-versioning]]
- [[branch-strategy]]
