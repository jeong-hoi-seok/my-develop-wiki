---
id: decision-expo-sdk-version
title: Expo SDK 버전
aliases: [Expo SDK 버전, Expo SDK 54 버전 고정]
type: decision
status: active
created_at: 2026-06-19
created_by: 정회석
updated_at: 2026-07-10
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
    note: "relations 단방향 정리"
  - action: updated
    at: 2026-07-10
    by: 정회석
    note: "54 고정 문서를 버전 운용 문서로 개편. Expo Go 사용 중지와 SDK 56 업그레이드 결정 반영, 파일명 expo-sdk-54-pinning에서 변경"
tags: [frontend, react-native, expo, versioning]
stack: app
scope: expo-sdk-version
source: "https://expo.dev/changelog/sdk-56, https://docs.expo.dev/develop/development-builds/expo-go-to-dev-build (조회 2026-07-10)"
relations: []
---

# Expo SDK 버전

## 한 줄 요약

팀 표준 Expo SDK는 **56**이다. Expo Go 사용을 중지하면서 54에 고정할 이유가 사라졌다. 이후로는 짝수 SDK를 안정화 버전으로 보고 따라간다.

## 54와 그 이후의 차이

SDK 54는 두 경계의 마지막 버전이다. 우리가 54에 고정했던 이유도 이 둘이었다.

1. **스토어 Expo Go 마지막 지원 SDK.** App Store의 Expo Go는 54까지 실행한다. 55 이상은 TestFlight 베타나 development build가 필요하다. 조사 2026-06 기준.
2. **Legacy Architecture 마지막 SDK.** 54는 React Native 0.81 기반. 55부터 New Architecture 전용이다.

## 우리팀이 Expo Go를 쓰지 않는 이유

- **포함된 네이티브 모듈만 쓸 수 있다.** 커스텀 네이티브 모듈 추가 불가. TaskManager는 Android에서 아예 동작하지 않는다.
- **개발 환경과 배포 환경이 다르다.** 배포는 네이티브 빌드로 나가므로, Expo Go에서 되던 것이 빌드에서 깨지는 문제를 늦게 발견한다.
- **공식 권장도 development build다.** Expo는 Expo Go를 교육·빠른 시작 도구로 규정한다.

그래서 2026-07-10 회의에서 Expo Go 중지를 결정했다. 개발 테스트는 `expo-dev-client` 기반 development build로 한다.

## 그러면 54를 쓸 이유가 없다

1. development build는 프로젝트 SDK를 그대로 담아 빌드한다. 스토어 Expo Go 버전과 맞출 필요가 없다.
2. 레거시 아키텍처는 유예일 뿐이다. 55 이상은 New Architecture 전용이라 미룰수록 전환 부채만 쌓인다. 54의 critical fix 지원도 2026년 9~10월경 끝난다.

## 버전 선택 기준

- **짝수 SDK를 쓴다.** 팀은 짝수 버전을 안정화 버전으로 판단해 선호한다. 이 문서 작성일 기준 최신은 57이지만 56을 쓴다.
- **패치는 고정하지 않는다.** `~56.0.x` 범위로 두고 패치 업데이트를 수용한다.
- SDK 56 = React Native 0.85, React 19.2.3. context7 조회 2026-07-10.

## 트레이드오프

| 택한 것 | 포기한 것 |
|---|---|
| 최신 기능·보안 패치, New Architecture 전환 완료 | 스토어 Expo Go 즉시 테스트 편의 |
| 개발·배포 환경 일치 | development build 셋업 비용, Apple Developer 멤버십 |
| 업그레이드 부채 해소 | New Architecture 미대응 의존성 대응 비용 |

## 출처

- Expo SDK 56 changelog: https://expo.dev/changelog/sdk-56
- Expo Go에서 development build로 이전: https://docs.expo.dev/develop/development-builds/expo-go-to-dev-build
- Expo SDK 릴리즈 케이던스·유지보수 기간: https://expo.dev/changelog/sdk-57
- Expo Go and the App Store (May 2026): https://expo.dev/changelog/expo-go-and-app-store-may-2026
