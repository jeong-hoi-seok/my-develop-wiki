---
id: worklog-5aa8b667
title: 프로젝트 운영·도구 기준 정리
scope: wiki-operations
authors:
- 정회석
created_at: 2026-09-23
updated_at: 2026-09-23
topics:
- legacy-migration
- agent-rules
- branch-strategy
- package-manager
- node
code_paths: []
related: []
---

# 프로젝트 운영·도구 기준 정리

## 이관 정보

- 원문 사건 날짜: 2026-07-07
- 이전 기록: `20_wiki/log.md`의 날짜별 로그 4번째 항목. 이전 문서 id는 `log-log`.
- 원문 기준: [기준 커밋의 기록](https://github.com/jeong-hoi-seok/my-develop-wiki/blob/ca984ed2dd9e16a2fc300a517c7316841b31edc8/20_wiki/log.md).
- 파일 생성일은 이관일입니다. 파일명·월 폴더는 사건 날짜를 사용하며, 기간 기록은 시작일을 사용합니다.

## 이관 본문

- **2026-07-07** (정회석) — agent-instruction-guide AGENTS 템플릿에 작업 기록·MR/PR 필수 절 신설, 작업 완료 시 worklog 기재와 MR/PR 요청 시 mr-pr-guide 선행 숙지 의무화. project-wiki-guide의 worklog 온디맨드 기록을 작업 완료 시 기재로 개정, 파일 생성은 여전히 사용자 동의 필수. AGENTS 템플릿 도입부에 conventions·operations 선행 학습 필수 항목 추가. branch-strategy 신설, dionz-frontend 이슈 2 ingest로 인프라 main 단일 트랙과 사내 제품 prod/dev 트랙 이원화, 트랙 판별·보호 설정·FF 병합·rebase·릴리즈·hotfix 동기화 정리, AGENTS 템플릿 git 규칙을 보호 브랜치로 일반화. 에이전트 작동 방식 변경으로 minor. version 0.22.0. package-manager 신설, 사내 표준 pnpm 최신 버전과 packageManager 필드 고정·pnpm-lock.yaml 단일 lockfile 규칙 정리, npm·yarn 명령은 실행 직전 선택지형 확인 의무화, 목차 등록. 에이전트 작동 방식 변경으로 minor. version 0.23.0. node-version 신설, 권장 Node 24 LTS와 .nvmrc 메이저 고정·engines 필드 병행 선언 규칙 정리, 타 버전 사용은 실행 직전 선택지형 확인 의무화, package-manager와 relations 연결, 목차 등록. 패키지 매니저 문서와의 통합은 관심사 분리와 wiki-versioning 명칭 혼동 방지로 기각. 에이전트 작동 방식 변경으로 minor. version 0.24.0. im-not-ai로 package-manager·node-version 점검, 둘 다 AI 티 0건 클린 판정, 두 문서의 em dash 기호 7곳을 쉼표·마침표·콜론으로 대체. version 0.24.1.

## 검증과 한계

- 과거 날짜·작성자·항목 범위와 `collapsed` 표기를 보존했습니다. 묶인 항목을 추측으로 나누거나 다시 요약하지 않았습니다.
- 이관 본문은 이관 전 원문과 일치합니다.
- 본문의 정책·버전·검증 결과는 당시 기록입니다. 현재 규칙이나 이번 작업의 재검증 결과로 해석하지 않습니다.
