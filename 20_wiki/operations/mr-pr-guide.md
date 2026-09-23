---
id: operation-mr-pr-guide
title: MR PR 작성 가이드
aliases: [MR PR 작성 가이드]
type: operation
status: active
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
    note: "개발 외에서도 쓰이는 규칙이라 conventions에서 operations로 재분류"
  - action: updated
    at: 2026-07-02
    by: 정회석
    note: "relations 단방향 정리"
  - action: updated
    at: 2026-07-02
    by: 정회석
    note: "im-not-ai 윤문으로 개조식 종결 4곳 서술형 자연화"
  - action: updated
    at: 2026-07-02
    by: 정회석
    note: "AI 작성 규칙에 AI attribution 문구 금지 추가"
  - action: updated
    at: 2026-07-09
    by: 정회석
    note: "AI 작성 규칙에 writing-style AI 티 금지 준수와 im-not-ai 윤문 점검 추가"
  - action: updated
    at: 2026-07-23
    by: 정회석
    note: "템플릿 사용 절 추가, Default·Release 선택 조건과 raw 템플릿 폴더 설치 규칙, 작성 규칙 재배치"
  - action: updated
    at: 2026-09-23
    by: 정회석
    note: "GitHub PR 템플릿·실제 변경 범위·worklog 연결로 개인화, 회사 스프린트 규칙 제외"
  - action: updated
    at: 2026-09-23
    by: 정회석
    note: "사용자 요청에 따른 외부 저장소 식별정보와 비교 문구 제거"
tags: [common, operation, git, mr, pr]
stack: common
scope: mr-pr-authoring
source:
  - "사용자 개인 위키 개선 요청, 2026-09-23"
relations:
  - id: operation-wiki-versioning
    label: related
---
# PR / MR 작성 가이드

## 한 줄 요약

GitHub PR·GitLab MR은 실제 변경 범위와 검증 근거로 작성합니다. my-develop-wiki는 GitHub PR을 사용합니다.

## 범위 확인

1. 실제 현재 브랜치와 target을 확인합니다. 브랜치 구성은 [[branch-strategy]], 위키 target은 `main`입니다.
2. target의 원격 참조를 갱신하고 비교 기준 커밋·포함 커밋·파일 diff를 확인합니다. 비교 기준 커밋 자체와 target에만 있는 변경은 포함하지 않습니다.
3. 같은 source·target의 열린 PR/MR과 이미 병합된 변경을 확인해 중복 요청을 피합니다. 재작성·분리 작업은 최신 target에서 남은 변경만 비교합니다.
4. 확인한 source·target·비교 기준·커밋 범위를 사용자에게 공유합니다. 이미 요청받은 작성·반영 단계는 재확인하지 않고, target이나 범위가 불명확할 때만 묻습니다.

## 템플릿

| 대상 | 읽을 파일·기준 |
|---|---|
| my-develop-wiki | [.github/pull_request_template.md](/.github/pull_request_template.md) |
| 다른 GitHub 프로젝트 | 프로젝트 `.github/pull_request_template.md` 또는 선택한 PR 템플릿 |
| GitLab 프로젝트 | 프로젝트 `.gitlab/merge_request_templates/Default.md`. 별도 릴리즈 템플릿은 해당 프로젝트가 정한 경우 사용 |

기존 프로젝트 템플릿 구조를 유지합니다. 없으면 프로젝트 용도와 플랫폼에 맞는 최소 템플릿을 만들고 변경 내용에 포함합니다. GitLab 파일을 이름·경로만 바꿔 GitHub에 통째로 설치하지 않습니다.

[10_raw/merge_request_templates/Default.md](/10_raw/merge_request_templates/Default.md)와 [10_raw/merge_request_templates/Release.md](/10_raw/merge_request_templates/Release.md)는 보존 중인 템플릿 원본입니다. 실제 PR/MR은 해당 프로젝트의 활성 템플릿을 기준으로 작성합니다.

## 제목과 본문

- 제목은 [[commit-convention]]의 한국어 `type(scope): subject`와 명사형 종결을 따릅니다.
- 릴리즈 PR/MR의 버전·제목은 해당 프로젝트 기준과 사용자 요청으로 정합니다. 스프린트 날짜·횟수를 임의 생성하지 않습니다.
- 첫 문단에 해결한 문제와 바뀐 동작을 씁니다. 실제 diff와 맞는 변경만 설명하며, 구현 세부는 검토에 필요한 범위만 남깁니다.
- 검증은 수행한 환경·결과·미수행 범위를 구분합니다. 문서 변경은 링크·메타데이터·구조 확인으로 충분하며 실행하지 않은 앱 테스트를 체크하지 않습니다.
- [00_context/writing-style.md](/00_context/writing-style.md)를 따릅니다. AI 도구의 자동 서명·홍보 문구는 넣지 않습니다. 사용자 요청 시에만 별도 윤문 도구를 사용합니다.

## 화면 변경 증거

UI가 바뀌면 실행 가능한 환경에서 변경 화면·상태를 확인하고 의미 있는 캡처를 남깁니다. 이미 앱 실행·캡처를 요청받았다면 재확인하지 않습니다. 별도 환경 실행이나 캡처가 필요한데 승인 범위가 불명확하면 먼저 확인합니다.

캡처가 불가능하면 `스크린샷/영상 첨부 필요`와 이유를 씁니다. 사용자에게 작업을 넘기거나 실행하지 않은 화면을 확인했다고 쓰지 않습니다. before/after·실데이터·모의 데이터·시뮬레이터·실기기 검증을 구분합니다.

## worklog·버전 연결

- 기본 기록 단위는 PR/MR 하나입니다. 해당 변경의 미병합 worklog를 재사용하고, 본문에는 판단·검증 근거를 중복 복사하지 않습니다.
- 이미 병합된 변경을 모으는 릴리즈 PR은 기존 기록을 참조합니다. 새로운 결정·검증이 있을 때만 별도 기록을 만듭니다.
- 위키는 기록만 바꾸면 `none`, 규칙·구조를 바꾸면 같은 변경에서 `index.version`과 worklog에 이전·새 버전을 기록합니다. 상세는 [[wiki-versioning]]을 따릅니다.

## 반영 경계

커밋·push·PR/MR 생성·tag·Release는 각각 요청받은 범위만 실행합니다. 필요한 준비·검증을 끝낸 뒤 아직 승인되지 않은 반영 단계만 선택지로 확인합니다.

병합은 사용자가 직접 수행합니다. 에이전트는 merge·auto-merge를 실행하지 않습니다. 이 위키의 squash merge 후 tag·Release는 실제 병합 커밋을 확인하고 별도 요청 시에만 발행합니다.

## 관련 문서

- [[branch-strategy]]
- [[commit-convention]]
- [[worklog-writing-guide]]
- [[wiki-versioning]]
