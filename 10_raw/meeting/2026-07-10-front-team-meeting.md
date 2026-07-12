# 프론트 팀 기술 싱크 미팅

예약자: 정회석
회의 진행 일정: 7월 10 10:30 (GMT+9) → 11:30
회의 장소: 회의실 A
회의 참여자: 정회석, 김종한, 김강훈
상태: 완료
Created by: 정회석
Created time: 2026년 7월 10일 오전 9:46
Last edited by: 정회석
Last edited time: 2026년 7월 10일 오후 1:10

# 회의 내용

## Husky, Linter 등 개발 컨벤션 정리 및 문서화

- ESLint + Prettier 사용
- husky
    - typecheck → pre-push
    - lint-staged → nano-staged → pre-commit
    - fsd 린터 → steiger로 변경 → 종한님이 옵션 재확인 후 린터 대응
- 관련 컨벤션 정리해서 위키 문서에 업데이트

## 디온즈 프로젝트의 모노레포 사용 여부 확인

- 모노레포 사용 안함

## 앱 개발 환경 관련 내용 공유 및 싱크

- Expo ci/cd 구축하기 → @정회석
- Expo Go 사용 중지(앱 삭제)
- Expo 54 → Expo 56 로 업그레이드
- 안드로이드 테스트 환경 셋팅 필요
    - 종한님이 안드 테스트 빌드 확인하시는 걸로
    - Expo ci/cd 시 확인 필요

## 앱 개발 기술 스택 관련 논의

### 스타일링

- `StyleSheet`  → 확정

### 상태 및 데이터 관리

- 서버 상태: `@tanstack/react-query` → 확정
- 전역 상태: `zustand` → 확정
- 폼 관리: `react-hook-form`  → 확정
- 데이터 검증: `zod` → 확정

### UI 및 성능

- 애니메이션: `react-native-reanimated` → 확정
- 제스처: `react-native-gesture-handler`  → 좀 더 찾아보기
- 대용량 리스트: `@shopify/flash-list`  → 무한 스크롤 필요 시 사용
- 바텀시트: `@gorhom/bottom-sheet` → 사용

### 로컬 저장

- 인증 토큰 등 민감 정보: `expo-secure-store`  → 필요시 사용 예정(로그인에서 필요)

### 날짜 처리

- day.js → 확정

### 웹

- storybook → 확정
- shadcn-ui(base-ui 기반) → 확정