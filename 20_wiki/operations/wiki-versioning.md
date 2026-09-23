---
id: operation-wiki-versioning
title: 위키 버전 관리
aliases: [위키 버전 관리]
type: operation
status: active
created_at: 2026-06-25
created_by: 정회석
updated_at: 2026-09-23
updated_by: 정회석
audit_log:
  - action: created
    at: 2026-06-25
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
    note: "작업 절차 번호 7 누락 정정, 8·9를 7·8로"
  - action: updated
    at: 2026-09-23
    by: 정회석
    note: "기록 전용 none·같은 변경의 버전 확정·GitHub 발행과 사용자 병합 경계 반영"
  - action: updated
    at: 2026-09-23
    by: 정회석
    note: "사용자 요청에 따른 외부 저장소 식별정보와 비교 문구 제거"
tags: [common, convention, wiki, version]
stack: common
scope: wiki-versioning
source:
  - "사용자 개인 위키 개선 요청, 2026-09-23"
relations:
  - id: index-index
    label: related
  - id: operation-agent-instruction-guide
    label: related
---
# 위키 버전 관리

## 한 줄 요약

위키 버전은 [20_wiki/index.md](/20_wiki/index.md) frontmatter의 `version` 값으로 관리한다. 버전 대상 변경은 해당 변경 PR에서 버전 숫자를 확정한다. 사용자 병합 후 발행 요청을 받으면 그 커밋에 tag와 GitHub Release를 만든다. 형식은 SemVer를 빌려온다.

```txt
MAJOR.MINOR.PATCH
```

1.0 전까지는 `0.MINOR.PATCH`를 쓰고, `1.0.0`은 개인 위키의 운영 기준선이 안정됐을 때만 올린다(기준은 아래 [1.0.0 기준](#100-기준) 참고).

## 올리는 기준

여러 변경이 섞이면 가장 높은 기준 하나만 적용한다.

`minor`는 **드물게** 올린다. 1.0 전까지 `minor`는 곧 마일스톤이다. 하루 2회 이상이면 기준을 잘못 적용했을 가능성이 높으니 다시 검토한다.

### MINOR — 아래 셋 중 하나를 충족할 때만

`minor`는 **위키 범위·능력의 의미 있는 확장** 또는 **에이전트 작동 방식의 구조 변경**이다. "전엔 못 하던 걸 하게 됨" 수준.

1. **새 카테고리 + 실제 문서 3개 이상.** 1~2개거나 빈 카테고리는 `patch`.
2. **대형 ingest.** 새 raw 묶음으로 개념 문서 3개 이상 신설 + index 연결.
3. **작동 방식 구조 변경.** 판정 질문 = "이 변경 후 에이전트가 실제로 다르게 동작하나?" YES면 `minor`. (예: ingest 흐름 단계 추가·삭제, 폴더 역할 재정의, 경로 resolver 도입, 새 필수 선행 읽기 규칙)

### PATCH — 버전 대상인 나머지 변경

| 변경 | 예시 |
|---|---|
| 기존 컨벤션 보강 | 절차·항목·예외 추가 |
| 문서 이동·이름 변경 | 폴더·파일명 변경 |
| 단일 문서 신설 | 새 문서 1~2개, 워크플로 변화 없음 |
| 판단 기준 조정 | 기술결정 결론 변경, 컨벤션 문구 수정 |
| 기존 문서 보강 | 설명·예시·출처 추가 (양 많아도 patch) |
| 오탈자·표현 수정 | 의미 변화 없는 정리 |
| 현재 안내·목차 보정 | 누락 링크, 오래된 목차 갱신 |

### NONE — 기록만 변경

단순 질문 답변, 작업 기록의 추가·정정·검증 결과 보완, 내용과 운영 규칙을 바꾸지 않는 과거 기록 이관은 `none`이다. 기록만 바뀌면 `index.md`·공용 README·버전을 갱신하지 않는다. 작성 정책·메타데이터 규칙·도입 방식 자체를 바꾸면 `patch` / `minor` 기준으로 판단한다.

### 경계 케이스

| 상황 | 판정 | 이유 |
|---|---|---|
| 새 컨벤션 문서 1개, 워크플로 안 바뀜 | patch | 참고용 추가 |
| 새 컨벤션 + AGENTS 흐름에 강제 단계 생김 | minor | 작동 방식 변경(#3) |
| 카테고리 + 문서 2개 | patch | 3개 미만 |
| 기존 문서 10개 대량 보강 | patch | 양 ≠ 범위 확장 |
| 기술결정 결론 뒤집음 | patch | 단일 판단, 범위 그대로 |

### 릴리즈 케이던스

- 기록만 추가·정정하면 `none`으로 처리하고 `index.version`을 유지한다.
- `patch`·`minor` 변경은 같은 변경 PR에서 `index.version`을 갱신한다. 버전 숫자만 바꾸는 후속 PR을 만들지 않는다.
- tag·Release는 PR 병합 후 사용자가 요청한 단계에서 발행한다. 발행 전에는 같은 버전의 중복 tag·Release가 없는지 확인한다.

커밋·push·PR 생성·tag·Release 발행은 각각 별도 동작입니다. 앞 단계를 요청받았다고 다음 단계까지 실행하지 않습니다. 이미 요청받은 단계는 재확인하지 않습니다.

## 작업 절차

1. [[wiki-sync]]에 따라 원격 상태를 확인한다. 최신 GitHub Release와 `index.version`이 다르면 새 버전을 만들지 말고 미발행 버전인지 먼저 확인한다.
2. 실제 변경 범위로 `none` / `patch` / `minor`를 판단한다. 단순 질문처럼 기록 대상 결과가 없으면 파일 변경 없이 종료한다.
3. [[log-writing-guide]]에 따라 변경 단위 worklog에 bump 종류와 이유를 남긴다. `patch`·`minor`면 이전 버전과 새 버전도 함께 기록한다.
4. `patch`·`minor`면 같은 작업 브랜치에서 `index.version`·`updated_at`·`updated_by`·`audit_log`를 갱신한다. `none`이면 버전을 바꾸지 않는다.
5. 작업 브랜치 → PR → 사용자 squash merge로 반영한다. 커밋·push·PR은 사용자 요청·승인 범위에서만 실행하며 `main` 직접 커밋 금지. 에이전트는 merge·auto-merge를 실행하지 않는다.
6. 병합 후 tag·Release 요청을 받으면 squash merge 커밋의 `index.version`을 확인한다. 그 커밋에 `vX.Y.Z` tag를 붙이고 같은 이름의 GitHub Release를 만든다. 별도 릴리즈 준비 PR을 만들거나 병합하지 않는다.
7. Release 본문은 해당 버전 worklog의 변경 내용을 요약한다. 발행 실패 시 같은 버전·커밋에서 재개하고 새 버전을 중복 발급하지 않는다.

## 1.0.0 기준

아래를 만족하면 `1.0.0` 검토 가능.

- `AGENTS.md`와 주요 `에이전트 지침 파일 작성 가이드`가 개인 프로젝트 연동 방식까지 포함.
- `index.md`가 핵심 문서를 빠짐없이 가리킴.
- 주요 문서가 출처·플랫폼·상태를 가짐.
- 링크 lint 기준이 정해져 있고 큰 깨짐 없음.
- 공통 지식과 프로젝트 맥락 문서 역할이 명확히 분리됨.

## 관련 문서

- [[index]]
- [[agent-instruction-guide]]
