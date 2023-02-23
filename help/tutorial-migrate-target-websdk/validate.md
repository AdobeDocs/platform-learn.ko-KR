---
title: 웹 SDK를 사용하여 Target 구현 유효성 검사 | at.js 2.x에서 웹 SDK로 Target 마이그레이션
description: Adobe Experience Platform Web SDK를 사용하여 활동의 유효성을 확인하고 Adobe Target 구현을 디버깅하는 방법을 알아봅니다.
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 0%

---

# Platform Web SDK 구현의 유효성 검사

Target 구현을 at.js에서 Platform Web SDK로 마이그레이션한 후에는 프로덕션 사이트에 변경 사항을 게시하기 전에 모든 것이 제대로 작동하는지 확인하는 것이 중요합니다. Adobe은 다음 사항을 권장합니다.

* 기술 유효성 검사를 수행하여 기본 구현 및 Platform Web SDK 요청 및 응답이 올바른지 확인합니다
* Target 활동이 제대로 전달되고 렌더링되는지 확인합니다
* 보고가 올바르게 작동하는지 확인
* 대상 및 프로필 스크립트를 재방문하여 Platform Web SDK와 호환되는지 확인하십시오
* Adobe 또는 타사 애플리케이션과의 통합이 제대로 작동하는지 확인

모든 Target 구현은 사이트 아키텍처와 사용된 기능에 따라 다릅니다. 아래 표를 시작점으로 사용하고 구현에 고유한 항목을 추가할 수 있습니다. 다음 [디버깅 페이지](debugging.md) 이 자습서에서는 이 유효성 검사에 도움이 되는 데 사용할 수 있는 도구를 보여줍니다.

## 기술 유효성 검사

| 유효성 검사 항목 | 참고 |
|---|---|
| 코드 조각 사전 숨김을 하는 at.js가 더 이상 페이지에 없습니다 | Platform Web SDK에서는 ID가 있는 스타일을 자동으로 제거하지 않습니다 `at-body-style`. 이 이전 코드 조각을 페이지에 두면 코드 조각 시간 초과에 도달할 때까지 숨겨진 내용이 표시됩니다. |
| at.js 라이브러리가 더 이상 페이지에 없습니다 | 브라우저의 개발자 도구 콘솔에 &quot;adobe.target&quot; 개체가 없는지 확인합니다. Platform Web SDK와 at.js를 모두 포함하면 의도하지 않은 렌더링 동작이 발생합니다 |
| 필요한 매개 변수는 의 XDM 및 데이터 개체에 있습니다 `sendEvent` 요청 |  |
| 페이지 요청을 사용하여 카탈로그를 채우는 경우 Recommendations 카탈로그가 예상대로 업데이트됩니다 |  |
| 프로필 매개 변수가 Target에 성공적으로 전달되었습니다. | 디버거에서 에지 추적 보기 |
| 데이터 스트림 매퍼에서 XDM에 매핑된 매개 변수가 Target에 올바르게 전달됩니다 | 디버거 및/또는 보증의 Edge Trace 기능을 사용하여 유효성 검사 |
| Target 컨텐츠가 적용 가능한 `sendEvent` 응답 | 예상되 `renderDecisions` 옵션이 `true` 또는 범위가 요청되고 사용자가 특정 Target 활동에 대한 자격이 있습니다. |
| A `decisioning.propositionDisplay` 이벤트는 VEC 기반 활동 렌더링 후 실행됩니다 | 자동으로 렌더링되고 온디맨드로 렌더링되는 활동에는 별도의 이벤트 호출이 있어야 합니다 |
| A `decisioning.propositionDisplay` 양식 기반 활동 렌더링 후 이벤트 실행 | 특정 구현에만 적용할 수 있습니다. 이 호출을 실행하려면 사용자 지정 코드가 필요합니다. |
| A `decisioning.propositionDisplay` SPA 보기 변경 사항에 오퍼가 적용될 때 이벤트가 실행됩니다 | SPA 구현에만 적용 가능 |
| A `decisioning.propositionDisplay` SPA 구성 요소가 지정된 보기에 대해 다시 렌더링될 때 이벤트가 실행되지 않습니다. | SPA 구현에만 적용 가능 |
| A `decisioning.propsitionInteract` 이벤트는 활동 전환 후 실행됩니다 | at.js에서 마이그레이션된 &quot;요소를 클릭함&quot; 및 사용자 지정 전환 `trackEvent` 또는 `sendNotifications` 은 별도의 이벤트 호출을 가져야 합니다 |
| 응답 토큰은 `sendEvent` 응답 및 예상 값 | 응답 토큰은 웹 SDK에서 정상적으로 작동해야 합니다 |
| ECID는 Web SDK 및 at.js를 사용하는 페이지에서 일관됩니다 | 페이지별 마이그레이션에 적용됩니다. 리디렉션 오퍼는 이러한 유형의 마이그레이션에서 작동하지 않습니다 |


## 활동 전달 및 렌더링

| 유효성 검사 항목 | 참고 |
|---|---|
| VEC 기반 활동은 페이지 로드 시 제대로 렌더링됩니다 | 사용자 지정 코드 수정 사항과 요소 다시 정렬이나 텍스트 대체와 같은 기본 수정 사항을 모두 확인하는 것이 가장 좋습니다 |
| VEC 기반 활동은 SPA 보기 변경 시 제대로 렌더링됩니다 | SPA 구현에만 적용 가능 |
| 양식 기반 활동이 올바르게 렌더링됩니다 | 특정 구현에만 적용할 수 있습니다. 양식 기반 활동을 렌더링하려면 at.js와 유사한 사용자 지정 코드가 필요합니다. |
| 리디렉션을 사용하는 활동이 제대로 작동합니다 | 소스 페이지와 대상 페이지가 Platform Web SDK를 모두 사용하는 경우 리디렉션이 지원됩니다. at.js 페이지에서 Platform Web SDK 페이지로 또는 그 반대의 방법으로 Target 리디렉션이 지원되지 않습니다. |
| 원격 오퍼를 사용하는 활동이 제대로 작동합니다 | 일반적이지 않으므로 원격 오퍼에 대한 Target 오퍼 인벤토리를 확인합니다 |
| 플리커는 적절하게 완화됩니다 | 플리커(깜박임) 처리는 선택 사항이지만, 보유한 모든 완화 전략이 최적의 페이지 성능 및 사용자 경험을 위해 예상대로 작동하는지 확인합니다 |
| QA 링크가 예상대로 작동합니다 | 작동하지 않는 경우 web.webPageDetails.URL이 브라우저의 URL과 정확히 일치하는지 확인합니다 |
| 일반적으로 사용되는 모든 오퍼 유형이 예상대로 렌더링됩니다 |  |

## 보고

| 유효성 검사 항목 | 참고 |
|---|---|
| 방문자는 VEC 기반 활동으로 인한 것입니다 | 페이지 로드 수정 사항과 SPA 보기 수정 사항 모두에 대해 보고 기능이 예상대로 작동하는지 확인하는 것이 가장 좋습니다 |
| 방문자는 양식 기반 활동으로 인한 것입니다 | 사용된 렌더링 접근 방식에 따라, 구현을 위해 사용자 지정 코드가 필요할 수 있습니다. `decisioning.propositionDisplay` 이벤트 |
| 표준 변환 목표가 제대로 캡처됩니다 | 보고 소스로 Target 또는 Analytics에 적용됩니다 |
| 주문 전환과 세부 사항이 제대로 캡처됩니다 | 감사 보고서 확인 |
| 클릭 추적 전환이 올바르게 캡처됩니다 |  |
| 사용자 지정 전환 목표가 적절하게 캡처됩니다 | 예를 들어 전환 목표가 at.js에서 마이그레이션되었습니다 `trackEvent` 또는 `sendNotifications` 일반적으로 &quot;mbox 확인함&quot; 목표에 사용됩니다 |

## 대상 및 프로필 스크립트

| 유효성 검사 항목 | 참고 |
|---|---|
| 라이브 활동에 사용된 대상은 Platform Web SDK와 호환됩니다 | XDM 속성을 포함하도록 &quot;사용자 지정&quot;(mbox 매개 변수) 구성 요소를 사용하는 대상을 업데이트해야 합니다 |
| 모든 프로필 스크립트는 Platform Web SDK와 호환됩니다 | mbox 매개 변수를 사용하는 모든 프로필 스크립트는 XDM 속성을 포함하도록 업데이트해야 합니다 |
| Target 대상에 대해 활동이 반환됩니다 | Platform Web SDK와 호환되도록 수정하려는 대상에 대해 종단 간 유효성 검사를 수행하는 것이 가장 좋습니다 |
| 프로필 스크립트는 예상대로 평가됩니다 | 디버거에서 에지 추적 보기 |

## Adobe 애플리케이션과의 통합

| 유효성 검사 항목 | 참고 |
|---|---|
| Experience Cloud 대상에 대해 활동이 반환됩니다 | 예를 들어 Adobe Analytics에서 게시된 세그먼트가 있습니다 |
| Experience Platform 대상에 대해 활동이 반환됩니다 | RTCDP와 같은 Experience Platform 기반 애플리케이션에 대한 라이센스가 있는 경우에만 적용됩니다 |
| Audience Manager 대상에 대해 활동이 반환됩니다 | 예를 들어, 특정 페이지 방문을 기반으로 한 세그먼트 |
| Target 활동 데이터가 Analysis Workspace에 표시됩니다 | Adobe Analytics을 보고 소스로 사용하는 활동에 적용됩니다 |

## 타사 애플리케이션과의 통합

| 유효성 검사 항목 | 참고 |
|---|---|
| 응답 토큰 데이터가 타사 응용 프로그램으로 제대로 전달됩니다 | 통합 접근 방식은 다를 수 있지만, 일반적인 방법은 Target 응답 토큰을 사용하여 활동 및 경험 정보를 Google Analytics과 같은 다른 분석 도구에 전달하는 것입니다 |
| 타사의 정보는 XDM 또는 프로필 데이터로 전달됩니다 | 타사의 모든 관련 정보를 전달해야 합니다 `sendEvent` Target 호출 |

위의 유효성 검사 단계를 수행한 후에는 Platform Web SDK 구현이 프로덕션으로 이동할 준비가 되어 있음을 확신할 수 있습니다.

다음으로, 다음 방법을 배웁니다. [platform Web SDK를 사용한 Target 구현 문제 해결](debugging.md).

>[!NOTE]
>
>Adobe는 at.js에서 웹 SDK로 Target 마이그레이션을 성공적으로 수행할 수 있도록 최선을 다하고 있습니다. 마이그레이션에 문제가 발생했거나 이 안내서에 중요한 정보가 누락된 것 같은 경우에는 로그인한 후 알려 주십시오 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).