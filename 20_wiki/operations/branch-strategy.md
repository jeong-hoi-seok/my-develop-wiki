---
id: operation-branch-strategy
title: 브랜치 전략
aliases: [브랜치 전략]
type: operation
status: active
created_at: 2026-07-07
created_by: 정회석
updated_at: 2026-09-23
updated_by: 정회석
audit_log:
  - action: created
    at: 2026-07-07
    by: 정회석
    note: "프로젝트 유형별 브랜치 전략 이원화 — 인프라 main 단일 트랙, 사내 제품 prod/dev 트랙. dionz-frontend 이슈 #2 ingest"
  - action: updated
    at: 2026-07-07
    by: 정회석
    note: "병합 방식 Squash 후 FF로 통일, 브랜치 보호 표·Rebase 규칙 삭제 등 문서 단순화"
  - action: updated
    at: 2026-07-30
    by: 정회석
    note: "개인 위키 트랙을 main+dev 단일 전략으로 정리 — 제품 prod/dev 트랙·hotfix·dionz 출처 제거"
  - action: updated
    at: 2026-09-23
    by: 정회석
    note: "개인 프로젝트 main·dev 전략 유지, 위키 main PR 흐름과 사용자 병합 구분"
  - action: updated
    at: 2026-09-23
    by: 정회석
    note: "사용자 요청에 따른 외부 저장소 식별정보와 비교 문구 제거"
tags: [common, operation, git, branch]
stack: common
scope: branch-strategy
source:
  - "사용자 개인 위키 개선 요청, 2026-09-23"
relations:
  - id: operation-commit-convention
    label: related
  - id: operation-mr-pr-guide
    label: related
---
# 브랜치 전략

## 한 줄 요약

이 위키는 작업 브랜치에서 `main`으로 PR을 보냅니다. 개인 개발 프로젝트의 기존 `main`·`dev` 전략은 유지하되, 실제 프로젝트 지침과 브랜치 구성을 먼저 확인합니다.

## 적용 범위

| 대상 | 기본 흐름 | 판단 기준 |
|---|---|---|
| my-develop-wiki | 작업 브랜치 → `main` | GitHub 위키 저장소. `dev`를 새로 만들지 않음 |
| `main`·`dev`를 쓰는 개인 앱 | `feature/*` → `dev` → `main` | `dev`는 개발 통합, `main`은 릴리즈 |
| 별도 전략이 있는 소비 프로젝트 | 해당 프로젝트 지침 | 위키 연동만으로 브랜치 구조를 바꾸지 않음 |

프로젝트 규칙과 실제 브랜치가 다르면 현재 target을 확인한 뒤 진행합니다. 다른 프로젝트의 배포·hotfix 절차를 자동 적용하지 않습니다.

## 작업 브랜치와 PR

- 보호 브랜치에는 직접 커밋·push하지 않습니다. 브랜치를 생략한 커밋 요청도 작업 브랜치부터 만듭니다.
- 이 위키의 작업 브랜치는 `docs/*`·`chore/*`·`fix/*`처럼 변경 목적을 드러냅니다. 개인 앱의 `dev` 대상 작업은 기존 기준대로 `feature/*`를 씁니다.
- source·target·비교 기준·포함 커밋·기존 PR 중복을 확인합니다. 제목과 본문은 [[commit-convention]]·[[mr-pr-guide]]를 따릅니다.
- 이 위키는 GitHub **Squash and merge**를 사용합니다. GitLab의 Fast-forward 설정을 GitHub에 그대로 적용하지 않습니다.
- 병합은 사용자가 직접 수행합니다. 에이전트는 merge·auto-merge를 실행하지 않습니다.

## 개인 앱 릴리즈

`dev` → `main`의 릴리즈 시점·버전·병합 방식은 해당 프로젝트에서 정합니다. 장기 유지하는 `dev`를 squash로 반영했다면 이후 이력 동기화 방식도 프로젝트에서 정하며, 보호 브랜치 강제 push를 기본 절차로 삼지 않습니다.

tag·Release는 실제 병합 커밋을 확인한 뒤 요청받은 단계만 실행합니다. 위키 자체 버전은 [[wiki-versioning]]을 따릅니다.

## 관련 문서

- [[commit-convention]]
- [[mr-pr-guide]]
- [[wiki-versioning]]
