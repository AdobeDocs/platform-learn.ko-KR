---
title: at.js 2.x와 웹 SDK 비교 | at.js 2.x에서 웹 SDK로 Target 마이그레이션
description: 기능, 함수, 설정 및 데이터 흐름 등 at.js 2.x와 Platform Web SDK의 차이점에 대해 알아봅니다.
source-git-commit: 63edfc214c678a976fbec20e87e76d33180e61f1
workflow-type: tm+mt
source-wordcount: '2156'
ht-degree: 8%

---

# at.js와 Platform Web SDK 비교

독립형 Adobe Target at.js 라이브러리는 Platform Web SDK와 크게 다릅니다. 다음 표는 마이그레이션 프로세스 중에 중점을 두어야 할 구현 영역을 평가하는 데 도움이 되는 참조입니다.

아래 정보를 검토하고 현재 기술 at.js 구현을 평가하면 다음을 이해할 수 있습니다.

- Platform Web SDK에서 지원하는 Target 기능
- 어떤 at.js 함수에는 이와 동일한 Platform Web SDK가 포함되어 있습니까
- Platform Web SDK에서 Target 설정을 적용하는 방법
- at.js 및 Platform Web SDK의 데이터 흐름이 어떻게 다른지

Platform Web SDK를 처음 사용하는 경우에는 걱정하지 마십시오. 아래 항목은 이 자습서 전체에서 자세히 다룹니다.

## 기능 비교

|  | at.js 2.x Target | Platform 웹 SDK |
|---|---|---|
| Target 프로필 업데이트 | 지원됨 | 지원됨 |
| SPA에 대한 트리거 보기 | 지원됨 | 지원됨 |
| Recommendations Target | 지원됨 | 지원됨 |
| 양식 기반 오퍼 가져오기 | 지원됨 | 지원됨 |
| 이벤트 추적 | 지원됨 | 지원됨 |
| A4T: 단일 페이지 애플리케이션 | 지원됨 | 지원됨 |
| A4T: 클릭 추적 | 지원됨 | 지원됨 |
| A4T: 클라이언트 측 로깅 | 지원됨 | 지원됨 |
| A4T: 서버 측 로깅 | 지원됨 | 지원됨 |
| 오퍼 적용 | 지원됨 | 지원됨 |
| 알림 없이 SPA에서 보기 다시 렌더링 | 지원됨 | 지원됨 |
| 하이브리드 애플리케이션 | 지원됨 | 지원됨 |
| QA URL | 지원됨 | 지원됨 |
| Mbox 타사 ID | 지원됨 | 지원됨 |
| 고객 속성 | 지원됨 | 지원됨 |
| 원격 오퍼 | 지원됨 | 지원됨 |
| 리디렉션 오퍼 | 지원됨 | 지원됨. 그러나 Platform Web SDK가 있는 페이지에서 at.js(반대 방향)가 있는 페이지로 리디렉션하는 것은 지원되지 않습니다. |
| On-Device Decisioning | 지원됨 | 현재 지원되지 않음 |
| Mbox 미리 가져오기 | 지원됨 | 기본적으로 모든 새 마이그레이션에서 활성화됨 - 2022년 10월 1일 이후에 시작됨 |
| 사용자 지정 이벤트 | 지원됨 | 지원되지 않음. 자세한 내용은 [공개 로드맵](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}) 을 참조하십시오. |
| 응답 토큰 | 지원됨 | 지원됨. 자세한 내용은 [전용 응답 토큰 설명서](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) at.js와 Platform Web SDK 간의 코드 예제 및 차이점에 대해 설명합니다. |
| 데이터 공급자 | 지원됨 | 지원되지 않음. 사용자 지정 코드는 Platform Web SDK를 트리거하는 데 사용할 수 있습니다 `sendEvent` 다른 공급자에서 데이터를 검색한 후의 명령 |


## 주목할 만한 설명선

|  | at.js 2.x Target | Platform 웹 SDK |
|---|---|---|
| 플리커 완화 | 비동기 구현을 위한 코드 조각 사전 숨김은 의 스타일 ID를 사용합니다. `at-body-style`. at.js는 응답이 수신되면 이 요소 ID를 찾아 스타일을 제거합니다. | 기본 코드 조각 사전 숨김은 `alloy-prehiding`. 웹 SDK는 at.js 코드 조각 사전 숨김과 호환되지 않으므로 마이그레이션 프로세스의 일부로 변경해야 합니다. |
| 페이지 로드 시 컨텐츠 자동 렌더링 | Target 전역 설정으로 제어됩니다. 활성화됨 `pageLoadEnabled` 가 로 설정되어 있습니다. `true`. | Platform Web SDK에 지정됨 `sendEvent` 명령. 를 설정하여 활성화됨 `renderDecisions` 옵션 `true`. |
| 수동으로 컨텐츠 렌더링 | 다음 `applyOffer()` 및 `applyOffers()` 함수는 HTML 설정만 지원합니다 | 다음 `applyPropositions` 명령은 유연성을 높이기 위해 HTML 설정, 교체 또는 추가를 지원합니다. |
| 사용자 지정 이벤트 추적 | 지원 대상 `trackEvent()` 및 `sendNotifications()` 함수 위에 있어야 합니다. 이러한 함수는 Target에만 해당되며 Adobe Analytics 지표에 영향을 주지 않습니다. | Platform Web SDK의 모든 데이터 `sendEvent` 호출은 Target에 전달됩니다. Target에 특별히 필요한 보충 데이터는 `sendEvent` eventType이 있는 명령 `decisioning.propositionDisplay` 또는 `decisioning.propositionInteract` Adobe Analytics 지표에 영향을 주지 않는지 확인합니다. |
| Target CNAME | 지원됨. Analytics 및 Experience Cloud ID 서비스에 사용되는 CNAME과 별개입니다. | 더 이상 관련이 없습니다. 단일 CNAME을 모든 Platform Web SDK 호출에 사용할 수 있습니다. |
| 디버깅 | 다음 `mboxDisable`, `mboxDebug`, 및 `mboxTrace` URL 매개 변수는 브라우저의 개발자 도구를 사용하여 디버깅하는 데 사용할 수 있습니다.<br><br>Adobe Experience Platform Debugger도 지원되는 디버깅 도구입니다. | 다음 `mboxDisable`, `mboxDebug`, 및 `mboxTrace` URL 매개 변수는 지원되지 않습니다.<br><br>를 추가하여 웹 SDK 디버깅을 설정할 수 있습니다 `alloy_debug=true` 쿼리 문자열 또는 실행 `alloy("setDebug", { "enabled": true });` 개발자 콘솔에서 게시할 수 있습니다.<br><br>Adobe Experience Platform Debugger 브라우저 확장 프로그램을 사용하여 디버깅을 위한 에지 추적을 시작할 수 있습니다.<br><br>자세한 내용은 [platform Web SDK 디버깅](debugging.md) 설명서 를 참조하십시오. |
| Analytics for Target (A4T) | SDID 값을 사용하여 Target 및 Analytics 호출 결합 | 기본적으로 결합하지 않고 지원됩니다 |

>[!NOTE]
>
>지정된 페이지에 대한 기존 AppMeasurement Adobe Analytics 구현을 그대로 유지하면서 Platform Web SDK로 Target을 마이그레이션하는 것은 지원되지 않습니다.
>
> at.js(및 AppMeasurement.js) 구현을 한 번에 한 페이지씩 Platform Web SDK로 마이그레이션할 수 있습니다. 이 방법을 사용하는 경우에는 [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) 및 [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) 옵션 `true` 사용 `configure` 명령.

## at.js 함수 및 Platform Web SDK에 상응하는 함수

아래 표에 요약된 Platform Web SDK를 사용하는 많은 at.js 함수에는 동등한 접근 방식이 있습니다. 에 대한 자세한 내용은 [at.js 함수](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/)를 보려면 Adobe Target 개발자 안내서 를 참조하십시오.

| at.js 2.x 함수 | Platform Web SDK에 상응하는 |
| --- | --- | 
| `getOffer()` 및 `getOffers()` | 및 를 요청하려면 [자동 렌더링](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#automatically-rendering-content) VEC 기반 Target, 다음 사용 `sendEvent` 명령 및 설정 `renderDecisions` 옵션을 true로 설정합니다.<br><br>양식 기반 경험을 요청하려면 또는 [수동 렌더링](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#manually-rendering-content) 컨텐츠, 일련의 `decisionScopes` (mbox) 사용 `sendEvent` 명령. |
| `applyOffer()` 및 `applyOffers()` | 를 사용하십시오 [`applyPropositions`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#applypropositions) 내용을 적용하는 명령 특정 선택기에 HTML을 설정, 대체 또는 추가하도록 선택할 수 있습니다. |
| `triggerView()` | Platform Web SDK는 자동으로 [보기 변경](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-trigger-a-view-change-in-a-single-page-application) 를 SPA VEC를 사용할 때 사용할 수 있도록 `web.webPageDetails.viewName` 속성은 `xdm` 옵션 `sendEvent` 명령. |
| `trackEvent()` 및 `sendNotifications()` | 를 사용하십시오 `sendEvent` 명령을 사용하여 명령 [특정 `eventType`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-track-events) 설정:<br><br>`decisioning.propositionDisplay` 는 활동을 렌더링한다는 신호를 보냅니다<br><br>`decisioning.propositionInteract` 마우스 클릭과 같은 활동과 사용자의 상호 작용을 신호합니다. |
| `targetGlobalSettings()` | 직접적인 동기는 없습니다. 자세한 내용은 [Target 설정 비교](detailed-comparison.md) 추가 세부 정보. |
| `targetPageParams()` 및 `targetPageParamsAll()` | 에 전달된 모든 데이터 `xdm` 옵션 `sendEvent` 명령이 Target mbox 매개 변수에 매핑됩니다. mbox 매개 변수의 이름은 직렬화된 점 표기법을 사용하여 지정되므로 Platform Web SDK로 마이그레이션하려면 새 mbox 매개 변수 이름을 사용하기 위해 기존 대상과 활동을 업데이트해야 할 수 있습니다. <br><br>의 일부로 전달된 데이터 `data.__adobe.target` 의 `sendEvent` 명령이 [Target 프로필 및 Recommendations 특정 매개 변수](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html#single-profile-update). |
| at.js 사용자 지정 이벤트 | 지원되지 않음. 자세한 내용은 [공개 로드맵](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}) 을 참조하십시오. [응답 토큰](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html) 는 의 일부로 노출됩니다 `propositions` 의 응답으로 `sendEvent` 호출. |

## at.js 설정 및 이에 상응하는 Platform Web SDK

at.js 라이브러리는 Target UI의 다양한 설정을 사용하여 구성 및 다운로드할 수 있습니다. 이러한 설정은 [`targetGlobalSettings()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/targetglobalsettings/) 함수 위에 있어야 합니다. 아래 표는 이러한 설정을 Platform Web SDK에서 사용할 수 있는 설정과 비교합니다.

| at.js 설정 | Platform Web SDK에 상응하는 |
| --- | --- |
| `bodyHiddenStyle` | 설정 [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#prehidingStyle) 사용 `configure` 명령 |
| `bodyHidingEnabled` | 다음과 같은 경우 `prehidingStyle` 는 `configure` 명령을 실행하면 이 기능이 활성화됩니다. 스타일이 정의되어 있지 않으면 Platform Web SDK에서 콘텐츠를 숨기지 않습니다. |
| `clientCode` | 자동 구성 |
| `cookieDomain` | 해당되지 않음 |
| `crossDomain` | 설정 `thirdPartyCookiesEnabled` 옵션 `true` 사용 `configure` 도메인 간 사용 사례에 대해 자사 및 타사 쿠키를 활성화하는 명령 |
| `cspScriptNonce` 및 `cspStyleNonce` | 다음 문서를 참조하십시오. [csp 구성](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-a-csp.html) |
| `dataProviders` | 지원되지 않음 |
| `decisioningMethod` | 모든 Platform Web SDK `sendEvent` 명령은 서버측 의사 결정을 사용합니다. 하이브리드 및 온장치 의사 결정은 지원되지 않습니다. |
| `defaultContentHiddenStyle` 및 `defaultContentVisibleStyle` | at.js 1.x에서만 적용할 수 있습니다. at.js 2.x와 유사하게, 사용자 지정 코드를 사용하여 양식 기반 경험에 대한 플리커(깜박임) 완화를 수행할 수 있습니다. |
| `deviceIdLifetime` | 지원되지 않음. If `targetMigrationEnabled` 가 로 설정되어 있습니다. `true` 사용 `configure` 명령, `mbox` 쿠키는 장치 라이프타임이 2년으로 설정된 상태로 설정됩니다. 이 값은 구성할 수 없습니다. |
| `enabled` | Target 기능이 데이터 스트림 구성으로 활성화되거나 비활성화됩니다 |
| `globalMboxAutoCreate` | 설정 `renderDecisions` 옵션 `true` 사용 `sendEvent` VEC 기반 경험을 자동으로 가져와서 렌더링하는 명령.<br><br>요청 `decisionScope` 대상 `__view__` vec 기반 경험을 수동으로 렌더링하려는 경우. |
| `imsOrgId` | 설정 `orgId` 사용 `configure` 명령 |
| `optinEnabled` 및 `optoutEnabled` | Platform Web SDK 를 참조하십시오 [개인 정보 보호 옵션](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html). 다음 `defaultConsent` 옵션은 Platform Web SDK에서 지원하는 모든 Adobe 솔루션에 적용됩니다. |
| `overrideMboxEdgeServer` 및 `overrideMboxEdgeServerTimeout` | 해당되지 않음. 모든 Platform Web SDK 요청은 Adobe Experience Platform Edge 네트워크를 사용합니다. |
| `pageLoadEnabled` | 설정 `renderDecisions` 옵션 `true` 사용 `sendEvent` 명령 |
| `secureOnly` | 지원되지 않음. Platform Web SDK는 `secure` 및 `sameSite="none"` 속성을 사용합니다. |
| `selectorsPollingTimeout` | 지원되지 않음. Platform Web SDK는 5초 값을 사용합니다. 필요한 경우 사용자 지정 코드를 사용하여 컨텐츠를 수동으로 렌더링할 수 있습니다. |
| `serverDomain` | 를 사용하십시오 `edgeDomain` 설정 `configure` 명령 |
| `telemetryEnabled` | 해당되지 않음 |
| `timeout` | 지원되지 않음. 플리커 완화 코드에 적절한 시간 초과가 포함되어 있는지 확인하는 것이 좋습니다. |
| `viewsEnabled` | 지원되지 않음. Target 보기에 대한 콘텐츠는 항상 첫 번째 페이지에서 가져옵니다 `sendEvent()` 인 경우 호출 `renderDecisions` 가 로 설정되어 있습니다. `true` 또는 `__view__` decisionScope가 요청에 포함되어 있습니다. |
| `visitorApiTimeout` | 해당되지 않음 |


## 시스템 다이어그램 비교

다음 다이어그램은 at.js를 사용하는 Target 구현과 Platform Web SDK를 사용하는 구현 간의 데이터 흐름 차이점을 이해하는 데 도움이 됩니다.

### at.js 2.x 시스템 다이어그램

![페이지 로드 시 at.js 2.0 동작](assets/target-at-js-2x-diagram.png){zoomable=&quot;yes&quot;}

| 호출 | 세부 사항 |
| --- | --- |
| 1 | 호출은 Experience Cloud ID(ECID)를 반환합니다. 사용자가 인증되면 다른 호출이 고객 ID를 동기화합니다. |
| 2 | at.js 라이브러리는 동기식으로 로드되며 문서 본문을 숨깁니다(at.js는 페이지에 구현된 코드 조각을 미리 숨기는 선택 사항을 사용하여 비동기식으로 로드할 수도 있음). |
| 3 | 페이지 로드 요청은 모든 구성된 매개 변수, ECID, SDID 및 고객 ID를 포함하여 이루어집니다. |
| 4 | 프로필 스크립트가 실행되고 프로필 저장소에 반영됩니다. 저장소는 대상 라이브러리의 적절한 대상(예: Analytics, Audience Manager 등에서 공유되는 대상)을 요청합니다. 고객 속성은 묶음 프로세스를 통해 프로필 저장소로 전송됩니다. |
| 5 | Target은 URL, 요청 매개 변수 및 프로필 데이터를 기반으로 현재 페이지 및 미래 보기를 위해 방문자에게 반환할 활동 및 경험을 결정합니다. |
| 6 | 추가적인 개인화를 위한 프로필 값을 선택적으로 포함하여 페이지로 다시 전송된 타깃팅된 컨텐츠.<br><br>현재 페이지의 타기팅된 콘텐츠는 기본 콘텐츠의 플리커 없이 가능한 한 빨리 나타납니다.<br><br>단일 페이지 애플리케이션의 향후 보기를 위한 타깃팅된 컨텐츠는 브라우저에서 캐시되므로, 보기가 트리거될 때 추가 서버 호출 없이 즉시 적용할 수 있습니다. triggerView() 동작에 대한 다음 다이어그램을 참조하십시오. |
| 7 | 페이지에서 데이터 수집 서버로 전송된 Analytics 데이터. |
| 8 | Target 데이터는 SDID를 통해 Analytics 데이터에 대응되며 Analytics 보고 저장소로 처리됩니다. 그런 다음 Analytics 데이터는 A4T 보고서를 통해 Analytics 및 Target 모두에서 볼 수 있게 됩니다. |

자세한 내용은 개발자 안내서 를 참조하십시오. [단일 페이지 애플리케이션에 at.js를 사용하여 Target 구현](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application/).

### Platform Web SDK 시스템 다이어그램

![Platform Web SDK를 사용한 Adobe Target Edge 의사 결정 다이어그램](assets/target-platform-web-sdk.png)

| 호출 | 세부 사항 |
| --- | --- |
| 1 | 장치는 Platform Web SDK를 로드합니다. Platform Web SDK는 XDM 데이터, 데이터 스트림 환경 ID, 전달된 매개 변수 및 고객 ID(선택 사항)를 사용하여 Edge 네트워크에 요청을 보냅니다. 페이지(또는 컨테이너)는 미리 숨겨져 있습니다. |
| 2 | 에지 네트워크는 방문자 ID, 동의 및 지리적 위치 및 장치 친숙한 이름과 같은 기타 방문자 컨텍스트 정보로 보강하기 위해 에지 서비스에 요청을 보냅니다. |
| 3 | 에지 네트워크는 방문자 ID 및 전달된 매개 변수를 사용하여 보강된 개인화 요청을 Target 에지에 보냅니다. |
| 4 | 프로필 스크립트가 실행된 다음 Target 프로필 저장소에 반영됩니다. 프로필 저장소는 대상 라이브러리의 세그먼트를 가져옵니다(예: Adobe Analytics, Adobe Audience Manager, Adobe Experience Platform에서 공유된 세그먼트). |
| 5 | Target은 URL 요청 매개 변수 및 프로필 데이터를 기반으로 현재 페이지 보기 및 미리 가져오기 위한 향후 보기에 대해 방문자에게 표시할 활동 및 경험을 결정합니다. 그런 다음 Target이 이를 다시 에지 네트워크로 보냅니다. |
| 6 | a. 에지 네트워크는 개인화 응답을 다시 페이지로 보냅니다. 원할 경우 추가적인 개인화를 위한 프로필 값을 포함할 수 있습니다. 현재 페이지의 개인화된 콘텐츠는 기본 콘텐츠의 플리커 없이 가능한 한 빨리 나타납니다.<br><br>나. SPA(단일 페이지 애플리케이션)의 사용자 작업으로 표시되는 보기에 대한 개인화된 콘텐츠는 추가적인 서버 호출 없이 즉시 렌더링하도록 캐시됩니다.<br><br>c. Edge 네트워크는 방문자 ID와 쿠키의 다른 값(예: 동의, 세션 ID, ID, 쿠키 확인, 개인화 등)을 보냅니다. |
| 7 | 에지 네트워크는 Analytics for Target(A4T) 세부 사항(활동, 경험 및 전환 메타데이터)을 Analytics 에지에 전달합니다. |

자세한 내용은 개발자 안내서 를 참조하십시오. [단일 페이지 애플리케이션용 Platform Web SDK를 사용하여 Target 구현](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html).

현재 Target 구현과 사용 중인 기능에 대한 기술적 이해를 했으면 다음 단계를 수행하여 다음을 수행합니다 [초기 설정](initial-setup.md).

>[!NOTE]
>
>Adobe는 at.js에서 웹 SDK로 Target 마이그레이션을 성공적으로 수행할 수 있도록 최선을 다하고 있습니다. 마이그레이션에 문제가 발생했거나 이 안내서에 중요한 정보가 누락된 것 같은 경우에는 로그인한 후 알려 주십시오 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
