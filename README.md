# my-develop-wiki

개발 지식과 판단 기준을 모아두는 개인 위키입니다. 프로젝트에서 다시 쓸 기준과 작업의 이유를 정리합니다.

모든 작업의 진입점은 [20_wiki/index.md](/20_wiki/index.md), 에이전트 운영 규칙은 [AGENTS.md](/AGENTS.md)입니다. 개인 글쓰기·사고방식은 `/00_context/`에 둡니다.

## 구조

```text
my-develop-wiki/
├── 00_context/         개인 글쓰기·사고방식
├── 10_raw/             보존할 원본 자료
├── 20_wiki/
│   ├── principles/     원칙·기술 선택 기준
│   ├── conventions/    개발 전용 규칙
│   ├── operations/     작성·Git·에이전트 운영
│   └── index.md        유일한 진입점
├── docs/worklog/
│   ├── README.md       작성·조회 안내
│   └── YYYY-MM/
│       └── YYYY-MM-DD-<주제>-<식별자>.md
├── README.md           저장소 소개
├── AGENTS.md           에이전트 운영 규칙
└── CLAUDE.md           AGENTS.md 포인터
```

## 문서와 기록

지식 분류는 세 폴더와 index 목차로 관리합니다. 중요한 개념은 `[[파일명]]`으로 연결합니다. 버전별 라이브러리 사용법은 복사하지 않고 Context7과 공식 문서로 조회합니다.

작업 이유·선택·검증 한계는 변경 단위 worklog에 남깁니다. 단순 조회는 기록하지 않고, 과거 기록을 읽을 때도 필요한 것만 찾습니다. 작성·조회 안내는 [docs/worklog/README.md](/docs/worklog/README.md)를 따릅니다. 과거 기록도 월별 worklog 파일에서 조회합니다.

`/10_raw/`에는 다시 확인할 원문을 보관합니다. 현재 적용할 기준은 `/20_wiki/`와 대상 프로젝트 지침에서 확인합니다.

## 개인 프로젝트 연동

위키 실체는 `~/my-develop-wiki` 한 곳에 둡니다. 소비 프로젝트 루트에 `my-develop-wiki` 심볼릭링크를 만들고 `./my-develop-wiki/20_wiki/index.md`부터 읽습니다. 링크는 소비 프로젝트의 `.gitignore`에 등록하고 커밋하지 않습니다.

연동·기록 도입 절차는 [20_wiki/operations/agent-instruction-guide.md](/20_wiki/operations/agent-instruction-guide.md)를 따릅니다. 위키는 재사용할 기준이며, 소비 프로젝트의 실제 지침이 우선합니다.

## 변경 반영

이 저장소는 GitHub에서 작업 브랜치 → `main` PR → 사용자 squash merge로 반영합니다. 개인 앱의 `main`·`dev` 운영과 구분합니다. 커밋·push·PR·tag·Release는 요청받은 단계만 실행합니다.

위키 방식의 기존 출처: [Andrej Karpathy, LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).
