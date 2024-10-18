---
title: Adobe Journey Optimizer - Decisioning Mobile 확장 기능을 통한 Target 구현 확인
description: Adobe Journey Optimizer - Decisioning Mobile 확장을 사용하여 활동을 확인하고 Adobe Target 구현을 디버깅하는 방법을 알아봅니다.
source-git-commit: afbc8248ad81a5d9080a4fdba1167e09bbf3b33d
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 1%

---

# Adobe Journey Optimizer - Decisioning Mobile 확장 구현의 유효성 검사

Target 확장에서 Decisioning 확장으로 Target 구현을 마이그레이션한 후 프로덕션 앱에 변경 사항을 게시하기 전에 모든 것이 제대로 작동하는지 확인하는 것이 중요합니다. Adobe은 이 페이지에서 자세히 다루는 다음 사항을 권장합니다.

* 기술 유효성 검사를 수행하여 기본 구현 및 Platform Mobile SDK 요청 및 응답이 정확한지 확인합니다
* Target 활동이 제대로 전달되고 렌더링되는지 확인합니다.
* 보고가 올바르게 작동하는지 확인
* 대상 및 프로필 스크립트를 다시 방문하여 Platform Mobile SDK 및 Optimie 확장과 호환되는지 확인하십시오
* Adobe 또는 서드파티 애플리케이션과의 통합이 올바르게 작동하는지 확인

모든 Target 구현은 사이트 아키텍처 및 사용되는 기능에 따라 다릅니다. 아래 표를 시작점으로 사용하여 구현에 고유한 항목을 추가할 수 있습니다. 이 자습서의 [디버깅 페이지](debugging.md)에는 이 유효성 검사에 도움이 되는 데 사용할 수 있는 도구가 표시됩니다.

## 기술 유효성 검사

| 유효성 검사 항목 | 참고 |
|---|---|
| | |


## 활동 전달 및 렌더링

| 유효성 검사 항목 | 메모 |
| | |

## 보고

| 유효성 검사 항목 | 메모 |
| | |

## 대상자 및 프로필 스크립트

| 유효성 검사 항목 | 참고 |
|---|---|
| | |

## Adobe 애플리케이션과 통합

| 유효성 검사 항목 | 메모 |
| | |

## 타사 애플리케이션과 통합

| 유효성 검사 항목 | 참고 |
|---|---|
| | |

위의 유효성 검사 단계를 수행한 후에는 Decisioning 확장이 포함된 Platform Mobile SDK 구현이 프로덕션으로 이동할 준비가 되었다고 확신할 수 있습니다.

다음으로 [Platform Web SDK를 사용하여 Target 구현 문제를 해결하는 방법](debugging.md)을 알아봅니다.

>[!NOTE]
>
>Target 확장에서 Decisioning 확장으로 모바일 Target을 성공적으로 마이그레이션할 수 있도록 지원하기 위해 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)에 게시하여 알려 주십시오.
