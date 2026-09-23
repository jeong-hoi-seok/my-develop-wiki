---
id: decision-expo-sdk-version
title: Expo SDK 버전
aliases: [Expo SDK 버전, Expo SDK 54 버전 고정]
type: decision
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
    note: "relations 단방향 정리"
  - action: updated
    at: 2026-07-10
    by: 정회석
    note: "54 고정 문서를 버전 운용 문서로 개편. Expo Go 사용 중지와 SDK 56 업그레이드 결정 반영, 파일명 expo-sdk-54-pinning에서 변경"
  - action: updated
    at: 2026-09-23
    by: 정회석
    note: "회사 SDK 채택·짝수 선호·Expo Go 금지 대신 개인 앱의 안정 버전·호환성 판단 기준 반영"
  - action: updated
    at: 2026-09-23
    by: 정회석
    note: "사용자 요청에 따른 외부 저장소 식별정보와 비교 문구 제거"
tags: [frontend, react-native, expo, versioning]
stack: app
scope: expo-sdk-version
source:
  - "https://expo.dev/changelog/sdk-56, https://docs.expo.dev/develop/development-builds/expo-go-to-dev-build (조회 2026-07-10)"
  - "사용자 개인 위키 개선 요청, 2026-09-23"
relations: []
---
# Expo SDK 버전

## 한 줄 요약

개인 앱은 의존성·네이티브 빌드 호환성을 확인한 안정 SDK를 선택합니다. 채택한 SDK는 각 프로젝트의 설정과 검증 결과로 관리합니다.

## 버전 선택 기준

- 새 프로젝트는 공식 안정 릴리즈와 주요 의존성 지원 상태를 함께 확인합니다. 기존 프로젝트는 현재 SDK와 업그레이드 필요부터 확인합니다.
- 짝수·홀수라는 이유만으로 안정성을 판단하지 않습니다. 공식 지원 정책과 프로젝트의 호환성 검증을 기준으로 판단합니다.
- 업그레이드는 한 단계씩 진행하고 해당 SDK의 변경 사항·호환 버전을 조회합니다. 정확한 설치 절차는 [[context7-instruction-guide]]에 따라 공식 문서를 확인합니다.
- 채택한 SDK·버전 범위·실제 해결된 의존성은 프로젝트 설정과 lockfile로 관리합니다. 변경 이유·검증 결과는 해당 프로젝트 worklog에 남깁니다.
- 구버전에 머물면 막는 의존성·지원 조건·다음 확인 시점을 기록합니다. beta·canary는 별도 실험 목적이 있을 때만 검토합니다.

## Expo Go와 development build

Expo Go는 학습·빠른 기능 확인에 사용할 수 있습니다. 네이티브 의존성·설정이 필요한 개인 앱과 배포를 목표로 하는 앱은 development build를 기본으로 검토합니다. 공식 문서도 production 앱에 development build를 권장합니다.

이 선택은 Expo Go의 전면 금지가 아닙니다. 프로젝트가 필요한 네이티브 모듈을 포함할 수 있는지, 빌드와 실제 기기에서 확인해야 할 동작이 무엇인지로 판단합니다. development build를 사용했다는 사실만으로 배포 빌드 검증이 끝난 것은 아닙니다.

## 프로젝트에 남길 근거

- 현재·대상 SDK와 주요 네이티브 의존성의 호환 여부.
- 빌드·타입 검사·관련 기능 테스트 결과와 남은 문제.
- 시뮬레이터·실기기·배포 빌드 중 확인한 범위.
- 업그레이드를 보류했다면 이유와 재검토 조건.

## 트레이드오프

| 선택 | 비용·조건 |
|---|---|
| 호환성이 확인된 안정 SDK 채택 | 최신 기능 도입이 늦어질 수 있음 |
| development build 사용 | 네이티브 빌드·설치·재빌드 관리 필요 |
| 단계적 업그레이드 | 여러 단계의 검증 시간 필요 |

## 관련 문서

- [[context7-instruction-guide]]
- [[worklog-writing-guide]]

## 출처

- [Expo SDK 업그레이드 안내](https://docs.expo.dev/workflow/upgrading-expo-sdk-walkthrough/), 2026-09-23 확인. 단계적 업그레이드와 development build 권장.
- [Expo SDK 공식 레퍼런스](https://docs.expo.dev/versions/latest/), 2026-09-23 확인. SDK별 호환 관계와 prerelease 구분.
