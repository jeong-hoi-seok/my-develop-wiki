---
id: worklog-190c18ef
title: 개인 위키 초기 이관
scope: wiki-operations
authors:
- 정회석
created_at: 2026-09-23
updated_at: 2026-09-23
topics:
- legacy-migration
- wiki-import
- versioning
code_paths: []
related: []
---

# 개인 위키 초기 이관

## 이관 정보

- 원문 사건 날짜: 2026-07-13
- 이전 기록: `20_wiki/log.md`의 날짜별 로그 1번째 항목. 이전 문서 id는 `log-log`.
- 원문 기준: [기준 커밋의 기록](https://github.com/jeong-hoi-seok/my-develop-wiki/blob/ca984ed2dd9e16a2fc300a517c7316841b31edc8/20_wiki/log.md).
- 파일 생성일은 이관일입니다. 파일명·월 폴더는 사건 날짜를 사용하며, 기간 기록은 시작일을 사용합니다.

## 이관 본문

- **2026-07-13** (정회석) — [저장소명 생략] 전체 문서를 my-develop-wiki(GitHub)로 이관. GitLab 전용 요소(.gitlab-ci.yml, scripts/ci)는 제외. 프로젝트명·심볼릭링크·경로·원격 URL 참조를 my-develop-wiki 기준으로 일괄 변경, 위키 실체 경로를 ~/project/my-develop-wiki로 갱신, GitLab Release 표기를 GitHub Release로 교체. 저장소 정체성 변경으로 minor. version 0.25.0.

## 검증과 한계

- 과거 날짜·작성자·항목 범위와 `collapsed` 표기를 보존했습니다. 묶인 항목을 추측으로 나누거나 다시 요약하지 않았습니다.
- 사용자 요청으로 원문의 저장소명 1곳을 생략했습니다. 나머지 본문은 이관 전과 일치합니다.
- 본문의 정책·버전·검증 결과는 당시 기록입니다. 현재 규칙이나 이번 작업의 재검증 결과로 해석하지 않습니다.
