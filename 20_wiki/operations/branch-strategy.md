---
id: operation-branch-strategy
title: 브랜치 전략
aliases: [브랜치 전략]
type: operation
status: active
created_at: 2026-07-07
created_by: 정회석
updated_at: 2026-07-30
updated_by: 정회석
audit_log:
  - action: created
    at: 2026-07-07
    by: 정회석
    note: "프로젝트 유형별 브랜치 전략 이원화 — 인프라 main 단일 트랙, 사내 제품 prod/dev 트랙. dionz-frontend 이슈 #2 ingest"
  - action: modified
    at: 2026-07-07
    by: 정회석
    note: "병합 방식 Squash 후 FF로 통일, 브랜치 보호 표·Rebase 규칙 삭제 등 문서 단순화"
  - action: modified
    at: 2026-07-30
    by: 정회석
    note: "개인 위키 트랙을 main+dev 단일 전략으로 정리 — 제품 prod/dev 트랙·hotfix·dionz 출처 제거"
tags: [common, operation, git, branch]
stack: common
scope: branch-strategy
relations:
  - id: operation-commit-convention
    label: related
  - id: operation-mr-pr-guide
    label: related
---

# 브랜치 전략

## 한 줄 요약

git 브랜치 운영 기준. `main`과 `dev` 두 브랜치를 쓴다. `main`은 릴리즈 상위 브랜치, `dev`는 개발 통합 브랜치다. 커밋 메시지·MR 제목은 [[commit-convention]], MR 본문·절차는 [[mr-pr-guide]]를 따른다.

## 브랜치 구성

| 브랜치      | 용도                                       |
| ----------- | ------------------------------------------ |
| `main`      | 릴리즈 상위 브랜치. protected. 릴리즈 시 version tag |
| `dev`       | 개발 통합 브랜치. default 브랜치           |
| `feature/*` | 개별 작업 브랜치. dev에서 분기, dev로 병합 |

```
feature/* → dev → main        (기본 흐름)
```

- 기능 추가뿐 아니라 dev 대상 모든 작업에 `feature/*`를 쓴다. 작업 성격은 브랜치명이 아니라 MR 제목의 type으로 구분한다.
- `main`·`dev`는 protected. 직접 커밋·push 금지, 변경은 작업 브랜치 → MR 경유.

## 병합 원칙

모든 병합은 MR 경유. Merge method는 **Squash 후 Fast-forward**로 통일한다. merge commit 없이 선형 히스토리를 유지한다.

| 병합 경로            | 방식                   |
| ------------------- | --------------------- |
| `feature/*` → `dev` | Squash 후 Fast-forward |
| `dev` → `main`      | Squash 후 Fast-forward |

## 릴리즈

1. `dev`를 `main`으로 병합한 뒤 `main`에 version tag를 생성·push한다.
2. version tag 생성은 실행 직전 사용자에게 반드시 확인한다.

## 관련 문서

- [[commit-convention]]
- [[mr-pr-guide]]
- [[wiki-versioning]]
