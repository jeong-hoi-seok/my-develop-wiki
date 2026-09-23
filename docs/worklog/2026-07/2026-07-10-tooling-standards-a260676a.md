---
id: worklog-a260676a
title: SDK·린트·Git Hook 기준 정리
scope: tooling
authors:
- 정회석
created_at: 2026-09-23
updated_at: 2026-09-23
topics:
- legacy-migration
- expo
- lint
- format
- git-hooks
code_paths: []
related: []
---

# SDK·린트·Git Hook 기준 정리

## 이관 정보

- 원문 사건 날짜: 2026-07-10
- 이전 기록: `20_wiki/log.md`의 날짜별 로그 2번째 항목. 이전 문서 id는 `log-log`.
- 원문 기준: [기준 커밋의 기록](https://github.com/jeong-hoi-seok/my-develop-wiki/blob/ca984ed2dd9e16a2fc300a517c7316841b31edc8/20_wiki/log.md).
- 파일 생성일은 이관일입니다. 파일명·월 폴더는 사건 날짜를 사용하며, 기간 기록은 시작일을 사용합니다.

## 이관 본문

- **2026-07-10** (정회석) — 프론트팀 회의 결정 반영으로 expo-sdk-54-pinning을 expo-sdk-version으로 개편. Expo Go 사용 중지, 54와 55 이상의 차이인 스토어 Expo Go 호환과 Legacy Architecture 경계 서술, development build 전환으로 54 고정 근거 소멸, 짝수 SDK 안정화 버전 선호로 56 채택, 패치 핀 중단. index 목차·context7-instruction-guide 링크·wiki-authoring-guide 예시 갱신. version 0.24.3. context7-instruction-guide와 wiki-authoring-guide에서 expo 버전 문서 참조·relations·예시 제거, 운영 가이드와 특정 기술 결정의 결합 해소. version 0.24.4. log 주간 압축, 06-24~07-02 일자 항목 7개를 collapsed 한 줄로 정리. version 0.24.5. lint-format 컨벤션 추가, 팀 공통 ESLint+Prettier 범용 베이스와 프로젝트 확장 원칙, 역할 분리와 import 정렬 Prettier 일원화, 사내 공용 설정에 consistent-type-imports를 근거와 함께 추가, import 정렬은 스코프 패키지 오분류 방지로 alias 패턴을 ^@/ 한정, side-effect import 원위치 고정과 그룹 빈 줄 추가, import-x는 recommended 미사용 상태의 죽은 off 설정을 제거하고 no-duplicates만 활성, 실검증으로 eslint-plugin-prettier fix 충돌이 import를 삭제하는 것을 재현해 eslint-config-prettier 단독으로 교체, TS resolver 패키지 설치 추가, VSCode는 requireConfig와 extensions.json 권장 목록으로 자동 적용 보강, 도구 버전 기준과 설치·ignore 셋팅·VSCode 공유 설정 정리, 목차 등록. version 0.24.6. git-hooks 컨벤션 추가, Husky 규격화와 pre-commit nano-staged 린트·포맷, pre-push는 typecheck 스크립트 이름만 계약으로 고정하고 구현은 tsc --noEmit 기본에 turbo 등 프로젝트 재량, GUI git 클라이언트 대응 nvm 로딩 스니펫을 두 hook에 적용, staged 단위와 전역 검사의 시점 분리 근거와 no-verify 우회 한계 정리, commit-msg commitlint는 회의 범위 밖이라 제외, 목차 등록. version 0.24.7.

## 검증과 한계

- 과거 날짜·작성자·항목 범위와 `collapsed` 표기를 보존했습니다. 묶인 항목을 추측으로 나누거나 다시 요약하지 않았습니다.
- 이관 본문은 이관 전 원문과 일치합니다.
- 본문의 정책·버전·검증 결과는 당시 기록입니다. 현재 규칙이나 이번 작업의 재검증 결과로 해석하지 않습니다.
