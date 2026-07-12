---
id: log-log
title: 작업 이력
aliases: [작업 이력]
type: log
status: active
created_at: 2026-06-19
created_by: 정회석
updated_at: 2026-07-13
updated_by: 정회석
audit_log:
  - action: created
    at: 2026-06-19
    by: 정회석
  - action: updated
    at: 2026-07-02
    by: 정회석
    note: "version X.Y.Z 표기·collapsed 마커로 전체 재표기"
  - action: updated
    at: 2026-07-13
    by: 정회석
    note: "my-develop-wiki 이관 이력 추가"
tags: [wiki, log]
stack: common
scope: wiki-log
relations:
  - id: operation-log-writing-guide
    label: depends-on
---

# Log

작업 이력을 이 파일 하나에 날짜순으로 남긴다. 작성·압축 규칙은 [[log-writing-guide]]가 단일 기준.

## 날짜별 로그
- **2026-07-13** (정회석) — frontend-wiki 전체 문서를 my-develop-wiki(GitHub)로 이관. GitLab 전용 요소(.gitlab-ci.yml, scripts/ci)는 제외. 프로젝트명·심볼릭링크·경로·원격 URL 참조를 my-develop-wiki 기준으로 일괄 변경, 위키 실체 경로를 ~/project/my-develop-wiki로 갱신, GitLab Release 표기를 GitHub Release로 교체. 저장소 정체성 변경으로 minor. version 0.25.0.
- **2026-07-10** (정회석) — 프론트팀 회의 결정 반영으로 expo-sdk-54-pinning을 expo-sdk-version으로 개편. Expo Go 사용 중지, 54와 55 이상의 차이인 스토어 Expo Go 호환과 Legacy Architecture 경계 서술, development build 전환으로 54 고정 근거 소멸, 짝수 SDK 안정화 버전 선호로 56 채택, 패치 핀 중단. index 목차·context7-instruction-guide 링크·wiki-authoring-guide 예시 갱신. version 0.24.3. context7-instruction-guide와 wiki-authoring-guide에서 expo 버전 문서 참조·relations·예시 제거, 운영 가이드와 특정 기술 결정의 결합 해소. version 0.24.4. log 주간 압축, 06-24~07-02 일자 항목 7개를 collapsed 한 줄로 정리. version 0.24.5. lint-format 컨벤션 추가, 팀 공통 ESLint+Prettier 범용 베이스와 프로젝트 확장 원칙, 역할 분리와 import 정렬 Prettier 일원화, 사내 공용 설정에 consistent-type-imports를 근거와 함께 추가, import 정렬은 스코프 패키지 오분류 방지로 alias 패턴을 ^@/ 한정, side-effect import 원위치 고정과 그룹 빈 줄 추가, import-x는 recommended 미사용 상태의 죽은 off 설정을 제거하고 no-duplicates만 활성, 실검증으로 eslint-plugin-prettier fix 충돌이 import를 삭제하는 것을 재현해 eslint-config-prettier 단독으로 교체, TS resolver 패키지 설치 추가, VSCode는 requireConfig와 extensions.json 권장 목록으로 자동 적용 보강, 도구 버전 기준과 설치·ignore 셋팅·VSCode 공유 설정 정리, 목차 등록. version 0.24.6. git-hooks 컨벤션 추가, Husky 규격화와 pre-commit nano-staged 린트·포맷, pre-push는 typecheck 스크립트 이름만 계약으로 고정하고 구현은 tsc --noEmit 기본에 turbo 등 프로젝트 재량, GUI git 클라이언트 대응 nvm 로딩 스니펫을 두 hook에 적용, staged 단위와 전역 검사의 시점 분리 근거와 no-verify 우회 한계 정리, commit-msg commitlint는 회의 범위 밖이라 제외, 목차 등록. version 0.24.7.
- **2026-07-09** (정회석) — writing-style에 AI 티 금지 규칙 추가: em dash 기호·괄호 부가설명·신설 같은 행정 문서투 한자어·AI 상투어·근거 없는 평가어 금지, 사용자가 요청하면 im-not-ai humanize-korean 스킬로 윤문 점검. Before/After를 실제 MR 사례로 교체하고 문서 간소화. mr-pr-guide AI 작성 규칙에 writing-style 준수·윤문 점검 항목 추가. thinking-principles에서 writing-style과 겹치는 서술 프레이밍·적용 예시 절 제거, 행정투 표현 정리. AGENTS Context First 예시에 MR/PR·커밋 본문 작성 추가. version 0.24.2.
- **2026-07-07** (정회석) — agent-instruction-guide AGENTS 템플릿에 작업 기록·MR/PR 필수 절 신설, 작업 완료 시 worklog 기재와 MR/PR 요청 시 mr-pr-guide 선행 숙지 의무화. project-wiki-guide의 worklog 온디맨드 기록을 작업 완료 시 기재로 개정, 파일 생성은 여전히 사용자 동의 필수. AGENTS 템플릿 도입부에 conventions·operations 선행 학습 필수 항목 추가. branch-strategy 신설, dionz-frontend 이슈 2 ingest로 인프라 main 단일 트랙과 사내 제품 prod/dev 트랙 이원화, 트랙 판별·보호 설정·FF 병합·rebase·릴리즈·hotfix 동기화 정리, AGENTS 템플릿 git 규칙을 보호 브랜치로 일반화. 에이전트 작동 방식 변경으로 minor. version 0.22.0. package-manager 신설, 사내 표준 pnpm 최신 버전과 packageManager 필드 고정·pnpm-lock.yaml 단일 lockfile 규칙 정리, npm·yarn 명령은 실행 직전 선택지형 확인 의무화, 목차 등록. 에이전트 작동 방식 변경으로 minor. version 0.23.0. node-version 신설, 권장 Node 24 LTS와 .nvmrc 메이저 고정·engines 필드 병행 선언 규칙 정리, 타 버전 사용은 실행 직전 선택지형 확인 의무화, package-manager와 relations 연결, 목차 등록. 패키지 매니저 문서와의 통합은 관심사 분리와 wiki-versioning 명칭 혼동 방지로 기각. 에이전트 작동 방식 변경으로 minor. version 0.24.0. im-not-ai로 package-manager·node-version 점검, 둘 다 AI 티 0건 클린 판정, 두 문서의 em dash 기호 7곳을 쉼표·마침표·콜론으로 대체. version 0.24.1.
- **2026.06.24 ~ 2026.07.02** (정회석) · collapsed — 위키 운영 골격 확립. 버전 관리 컨벤션과 시작 전 필수 절차, 심볼릭링크 연동, 브랜치 MR 필수, git 반영 선택지형 확인 도입. 폴더를 concepts·conventions 대통합 뒤 principles·conventions·operations 3분류로 재편. 파일명 영문 kebab-case 전환, frontmatter 스키마 필수화, relations 단방향, 경로 링크 표준 정립. 결정 번복: raw 원문 보관을 폐기하고 라이브러리 문서는 context7 조회로 전환, concepts 24개 삭제로 판단·기준 중심 축소. code-review를 code-review-graph 필수로 개편, context7·superpowers 가이드와 AI attribution 금지 규칙 추가. version 0.5.0~0.21.10.
- **2026.06.19 ~ 2026.06.23** (정회석) · collapsed — 위키 초기화, raw ingest, 주요 개념·컨벤션 문서 생성. 구조 정립: 제목·파일명 직관화, 로그 일자별 분리, context frontmatter·scope 규칙, 기술개념 web/app 폴더 분리, AGENTS 표준 운영 문서화. 결정 번복: 원문요약 mandatory→조건부, 테스트 문서 23→6 병합. project-wiki-guide 신설. version 태깅 이전.
