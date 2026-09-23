---
id: worklog-d7939742
title: 개인 위키 운영·작업 기록 개선
scope: wiki-operations
authors:
- 정회석
created_at: 2026-09-23
updated_at: 2026-09-23
topics:
- worklog
- legacy-migration
- personal-scope
- versioning
- agent-rules
code_paths: []
related:
- id: worklog-190c18ef
  relation: related
- id: worklog-a260676a
  relation: related
- id: worklog-0b1d8984
  relation: related
- id: worklog-5aa8b667
  relation: related
- id: worklog-e27a3374
  relation: related
- id: worklog-729c0550
  relation: related
---

# 개인 위키 운영·작업 기록 개선

## 변경과 이유

개인 프로젝트에서 재사용할 운영 기준과 작업 기록 방식을 정리했습니다. 단일 누적 로그를 변경 단위 파일로 전환하고, 필요한 과거 맥락만 찾아 읽도록 메타데이터와 조회 순서를 추가했습니다.

2026-09-23 후속 요청에 따라 기존 과거 기록도 현재 형식으로 옮기고 단일 로그 파일을 삭제했습니다. 본문·출처·변경 이력의 특정 저장소명과 불필요한 비교 문구도 제거했습니다.

## 반영 범위

| 영역 | 변경 |
|---|---|
| [AGENTS.md](/AGENTS.md)·[README.md](/README.md)·[[index]] | 개인 개발 지식 목적·기록 경로·사용자 병합 기준 정리 |
| [[worklog-writing-guide]]·[[log-writing-guide]]·[[project-wiki-guide]] | 변경 단위·월별 경로·9개 필드·선택적 조회·원문 이관 절차 |
| [[wiki-authoring-guide]] | worklog 경량 형식·README·원본 자료 예외 |
| [[agent-instruction-guide]]·[[context7-instruction-guide]] | 개인 위키 링크·대상 버전 조회·승인된 기록 방식 재사용 |
| [[wiki-versioning]]·[[wiki-sync]] | 기록 전용 none·같은 변경의 버전 확정·미발행 버전과 작업 브랜치 구분 |
| [[mr-pr-guide]]·[[branch-strategy]] | 위키의 main PR과 개인 앱의 main·dev 구분, 사용자 직접 병합 |
| [.github/pull_request_template.md](/.github/pull_request_template.md) | 개인 위키용 PR 템플릿 |
| [[package-manager]]·[[node-version]] | pnpm·Node 24 기본값, 프로젝트 버전 고정과 호환성 우선 |
| [[lint-format]]·[[git-hooks]] | 개인 코드 프로젝트 적용 범위와 기존 도구 존중 |
| [[expo-sdk-version]] | 안정 SDK·네이티브 호환성·프로젝트별 검증 기준 |
| [[code-review]] | 기존 도구·판단 기준 유지, 개인 재현·작업 기록 기준 정리 |
| [[naming-convention]]·[[commit-convention]] | 기존 기준 유지 |
| 도구 의존 | superpowers 필수 설치·전용 가이드 제거, 산출물 ignore 유지 |
| 개인 기준과 원본 | `/00_context/`·`/10_raw/`·[CLAUDE.md](/CLAUDE.md)·[.gitignore](/.gitignore) 유지 |

## 과거 기록 이관

이전 경로는 `20_wiki/log.md`, 문서 id는 `log-log`입니다. [기준 커밋](https://github.com/jeong-hoi-seok/my-develop-wiki/commit/ca984ed2dd9e16a2fc300a517c7316841b31edc8)의 날짜별 6항목을 기준으로 이관했습니다. 최근 안내·메타데이터만 달랐고 날짜별 본문은 같았습니다.

| 원문 사건 날짜 | 이관 파일 |
|---|---|
| 2026.06.19 ~ 2026.06.23 | [2026-06-19-wiki-bootstrap-729c0550.md](/docs/worklog/2026-06/2026-06-19-wiki-bootstrap-729c0550.md) |
| 2026.06.24 ~ 2026.07.02 | [2026-06-24-wiki-operations-e27a3374.md](/docs/worklog/2026-06/2026-06-24-wiki-operations-e27a3374.md) |
| 2026-07-07 | [2026-07-07-project-conventions-5aa8b667.md](/docs/worklog/2026-07/2026-07-07-project-conventions-5aa8b667.md) |
| 2026-07-09 | [2026-07-09-writing-principles-0b1d8984.md](/docs/worklog/2026-07/2026-07-09-writing-principles-0b1d8984.md) |
| 2026-07-10 | [2026-07-10-tooling-standards-a260676a.md](/docs/worklog/2026-07/2026-07-10-tooling-standards-a260676a.md) |
| 2026-07-13 | [2026-07-13-personal-wiki-import-190c18ef.md](/docs/worklog/2026-07/2026-07-13-personal-wiki-import-190c18ef.md) |

기존 항목 단위·날짜·작성자·`collapsed` 표기는 보존했습니다. 요청받은 저장소명 1곳을 생략했고, 해당 기록에 편집 범위를 밝혔습니다. 나머지 본문은 원문과 일치합니다. 이미 압축된 항목을 추측으로 분해하거나 복원하지 않았습니다.

이관 파일의 `created_at`·`updated_at`은 2026-09-23, 파일명 날짜·월 폴더는 원문 사건 날짜입니다. 기간 기록은 시작일을 사용했습니다. 위 `related`는 이관된 과거 기록의 참고 관계이며, 과거 정책을 현재 규칙으로 채택한다는 뜻은 아닙니다.

삭제 전 파일 SHA-256은 `d627a6bb817e34fe863a84f515b63ec47bd9ee5dde6ea1f2f55d55cae56556b1`입니다. 내용·누락·중복을 확인하고 구버전 파일을 삭제했습니다. 현재·과거 기록은 모두 [docs/worklog/README.md](/docs/worklog/README.md)에서 안내하는 방식으로 조회합니다.

## 버전

전체 작업은 운영 방식 변경으로 `minor`, `index.version`은 `0.27.0` → `0.28.0`입니다. 이번 과거 기록 이관은 같은 미병합 변경에 포함하며 버전을 추가로 올리지 않았습니다. 병합은 사용자가 진행하고, tag·Release는 별도 요청에 따라 발행합니다.

## 검증과 한계

- 과거 기록 6항목의 날짜·작성자·본문·항목 수 확인. 지정한 저장소명 1곳 생략 외 본문 일치.
- 메타데이터·고유 id·파일명·월 폴더·관계 대상·삭제 파일 참조 검증.
- 문서 전체의 특정 저장소명 잔존 여부 확인.
- 링크·목차·frontmatter·`git diff --check` 확인. 개인 기준·원본 자료·포인터·gitignore 유지 여부 확인.
- 과거 검증은 당시 기록으로 표시. 앱 빌드·테스트·hook 실행·Obsidian 화면 검증은 수행하지 않음.
- Node LTS와 Expo SDK 기준은 아래 공식 문서를 확인했으며, 다른 도구의 기존 예제를 전체 조합으로 재실행한 것은 아님.

## 외부 근거

- [Node.js 공식 릴리즈 목록](https://nodejs.org/en/about/previous-releases), 2026-09-23 조회.
- [Expo SDK 공식 레퍼런스](https://docs.expo.dev/versions/latest/), 2026-09-23 조회.
- [Expo SDK 업그레이드 안내](https://docs.expo.dev/workflow/upgrading-expo-sdk-walkthrough/), 2026-09-23 조회.
