---
title: Web SDK에 대한 at.js 2.x 비교 | Target을 at.js 2.x에서 Web SDK로 마이그레이션
description: 기능, 함수, 설정 및 데이터 흐름을 포함하여 at.js 2.x와 Platform Web SDK의 차이점에 대해 알아봅니다.
exl-id: b6f0ac2b-0d8e-46ce-8e9f-7bbc61eb20ec
source-git-commit: 78f0dcc0aa4674eb071c5fd091b5df04eb971326
workflow-type: tm+mt
source-wordcount: '2152'
ht-degree: 8%

---

# Platform Web SDK에 대한 at.js 비교

독립형 Adobe Target at.js 라이브러리는 Platform Web SDK와 크게 다릅니다. 다음 표는 마이그레이션 프로세스 중에 초점을 두어야 할 구현 영역을 평가하는 데 도움이 되는 참조입니다.

아래 정보를 검토하고 현재 기술 at.js 구현을 평가한 후 다음을 이해할 수 있어야 합니다.

- Platform Web SDK에서 지원하는 Target 기능
- Platform Web SDK에 해당하는 at.js 함수가 있는 함수
- Target 설정을 Platform Web SDK에 적용하는 방법
- at.js와 Platform Web SDK의 데이터 흐름이 서로 다른 방식

Platform Web SDK를 처음 사용하는 경우 걱정하지 마십시오. 아래 항목은 이 자습서 전체에서 자세히 다룹니다.

## 기능 비교

| | Target at.js 2.x | Platform Web SDK |
|---|---|---|
| Target 프로필 업데이트 | 지원됨 | 지원됨 |
| SPA에 대한 트리거 보기 | 지원됨 | 지원됨 |
| Target Recommendations | 지원됨 | 지원됨 |
| 양식 기반 오퍼 가져오기 | 지원됨 | 지원됨 |
| 이벤트 추적 | 지원됨 | 지원됨 |
| A4T: 단일 페이지 애플리케이션 | 지원됨 | 지원됨 |
| A4T: 클릭 추적 | 지원됨 | 지원됨 |
| A4T: 클라이언트측 로깅 | 지원됨 | 지원됨 |
| A4T: 서버측 로깅 | 지원됨 | 지원됨 |
| 오퍼 적용 | 지원됨 | 지원됨 |
| 알림 없이 SPA에서 보기 다시 렌더링 | 지원됨 | 지원됨 |
| 하이브리드 애플리케이션 | 지원됨 | 지원됨 |
| QA URL | 지원됨 | 지원됨 |
| Mbox 타사 ID | 지원됨 | 지원됨 |
| 고객 속성 | 지원됨 | 지원됨 |
| 원격 오퍼 | 지원됨 | 지원됨 |
| 리디렉션 오퍼 | 지원됨 | 지원됨. 그러나 Platform Web SDK가 있는 페이지에서 at.js가 있는 페이지(및 반대 방향)로의 리디렉션은 지원되지 않습니다. |
| 온디바이스 의사 결정 | 지원됨 | 현재 지원되지 않음 |
| Mbox 미리 가져오기 | 사용자 지정 범위 및 SPA VEC에 대해 지원됨 | 현재 일반 VEC에 대해 지원되지 않음 |
| 사용자 지정 이벤트 | 지원됨 | 지원되지 않음. 다음을 참조하십시오. [공개 로드맵](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}) (현재 상태) |
| 응답 토큰 | 지원됨 | 지원됨. 다음을 참조하십시오. [전용 응답 토큰 설명서](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) at.js와 Platform Web SDK 간의 코드 예제 및 차이점 |
| 데이터 공급자 | 지원됨 | 지원되지 않음. 사용자 지정 코드를 사용하여 Platform Web SDK를 트리거할 수 있습니다. `sendEvent` 다른 공급자에서 데이터를 검색한 후의 명령입니다. |


## 주목할 만한 설명선

| | Target at.js 2.x | Platform Web SDK |
|---|---|---|
| 플리커 완화 | 비동기 구현을 위한 코드 조각 사전 숨김은 의 스타일 ID를 사용합니다. `at-body-style`. at.js는 응답이 수신된 후 스타일을 제거하기 위해 이 요소 ID를 찾습니다. | 기본 코드 조각 사전 숨김은 의 스타일 ID를 사용합니다 `alloy-prehiding`. 웹 SDK는 at.js 코드 조각 사전 숨김과 호환되지 않으므로 마이그레이션 프로세스의 일부로 변경해야 합니다. |
| 페이지 로드 시 자동으로 콘텐츠 렌더링 | Target 전역 설정으로 제어됩니다. 활성화된 경우 `pageLoadEnabled` 이(가) (으)로 설정됨 `true`. | Platform Web SDK에 지정됨 `sendEvent` 명령입니다. 을(를) 설정하여 사용 `renderDecisions` 옵션 대상 `true`. |
| 수동으로 컨텐츠 렌더링 | 다음 `applyOffer()` 및 `applyOffers()` 함수는 설정 HTML만 지원합니다. | 다음 `applyPropositions` 명령은 유연성을 높이기 위해 HTML 설정, 바꾸기 또는 추가를 지원합니다. |
| 사용자 지정 이벤트 추적 | 지원 대상 `trackEvent()` 및 `sendNotifications()` 함수. 이러한 함수는 Target에만 해당되며 Adobe Analytics 지표에 영향을 주지 않습니다. | Platform Web SDK의 모든 데이터 `sendEvent` 호출이 Target에 전달됩니다. Target에 특별히 필요한 보충 데이터가 다음 항목에 포함되어야 합니다. `sendEvent` eventType이 인 명령 `decisioning.propositionDisplay` 또는 `decisioning.propositionInteract` Adobe Analytics 지표가 영향을 받지 않도록 하기 위해 |
| 대상 CNAME | 지원됨. 이는 Analytics에 사용되는 CNAME 및 Experience Cloud ID 서비스와 별개입니다. | 더 이상 관련이 없습니다. 모든 Platform 웹 SDK 호출에 단일 CNAME을 사용할 수 있습니다. |
| 디버깅 | 다음 `mboxDisable`, `mboxDebug`, 및 `mboxTrace` URL 매개 변수는 브라우저의 개발자 도구를 사용하여 디버깅하는 데 사용할 수 있습니다.<br><br>Adobe Experience Platform Debugger은 지원되는 디버깅 도구이기도 합니다. | 다음 `mboxDisable`, `mboxDebug`, 및 `mboxTrace` URL 매개 변수는 지원되지 않습니다.<br><br>다음을 추가하여 웹 SDK 디버깅을 설정할 수 있습니다. `alloy_debug=true` 쿼리 문자열 또는 실행 중 `alloy("setDebug", { "enabled": true });` 개발자 콘솔에서 을 참조하십시오.<br><br>Adobe Experience Platform Debugger 브라우저 확장 기능을 사용하여 디버깅을 위한 Edge 추적을 시작할 수 있습니다.<br><br>다음을 참조하십시오. [platform Web SDK 디버깅](debugging.md) 설명서 를 참조하십시오. |
| Analytics for Target (A4T) | SDID 값을 사용하여 Target 및 Analytics 호출 연결 | 연결할 필요 없이 기본적으로 지원됨 |

>[!NOTE]
>
>지정된 페이지에 대한 기존 AppMeasurement Adobe Analytics 구현을 유지하면서 Target을 Platform Web SDK로 마이그레이션하는 기능은 지원되지 않습니다.
>
> at.js(및 AppMeasurement.js) 구현을 Platform Web SDK에 한 번에 한 페이지씩 마이그레이션할 수 있습니다. 이 방법을 사용하는 경우 를 설정하는 것이 가장 좋습니다. [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) 및 [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) 옵션 `true` (으)로 `configure` 명령입니다.

## at.js 함수 및 이에 상응하는 Platform Web SDK

많은 at.js 함수에는 아래 표에 설명된 Platform Web SDK를 사용하는 것과 동일한 접근 방식이 있습니다. 에 대한 자세한 내용은 [at.js 함수](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/)Adobe Target 개발자 안내서를 참조하십시오.

| at.js 2.x 함수 | Platform Web SDK에 해당하는 함수 |
| --- | --- | 
| `getOffer()` 및 `getOffers()` | 요청 및 [자동으로 렌더링](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#automatically-rendering-content) VEC 기반 경험을 타깃팅하려면 다음을 사용하십시오. `sendEvent` 명령 및 설정 `renderDecisions` 옵션을 true로 설정합니다.<br><br>양식 기반 경험을 요청하려면 다음을 수행하십시오 [수동으로 렌더링](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#manually-rendering-content) 콘텐츠, 배열 지정 `decisionScopes` (mbox)에 `sendEvent` 명령입니다. |
| `applyOffer()` 및 `applyOffers()` | 사용 [`applyPropositions`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#applypropositions) 내용을 적용하는 명령입니다. 특정 선택기에 HTML을 설정, 대체 또는 추가하도록 선택할 수 있습니다. |
| `triggerView()` | Platform Web SDK가 [변경 사항 보기](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-trigger-a-view-change-in-a-single-page-application) SPA VEC의 목적상 `web.webPageDetails.viewName` 속성은 아래에 설정됩니다. `xdm` 옵션 `sendEvent` 명령입니다. |
| `trackEvent()` 및 `sendNotifications()` | 사용 `sendEvent` 이 있는 명령 [특정 `eventType`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-track-events) 설정:<br><br>`decisioning.propositionDisplay` 활동을 렌더링한다는 신호를 보냅니다.<br><br>`decisioning.propositionInteract` 는 마우스 클릭과 같은 활동과 사용자 상호 작용을 나타냅니다. |
| `targetGlobalSettings()` | 직접 동등 항목 없음. 다음을 참조하십시오. [대상 설정 비교](detailed-comparison.md) 추가 세부 정보. |
| `targetPageParams()` 및 `targetPageParamsAll()` | 에 전달된 모든 데이터 `xdm` 옵션 `sendEvent` 명령은 Target mbox 매개 변수에 매핑됩니다. mbox 매개 변수는 직렬화된 점 표기법을 사용하여 이름이 지정되므로 Platform Web SDK로 마이그레이션하려면 기존 대상과 활동을 업데이트하여 새 mbox 매개 변수 이름을 사용해야 할 수 있습니다. <br><br>의 일부로 전달된 데이터 `data.__adobe.target` / `sendEvent` 명령이 다음에 매핑됨 [Target 프로필 및 Recommendations 관련 매개 변수](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html#single-profile-update). |
| at.js 사용자 지정 이벤트 | 지원되지 않음. 다음을 참조하십시오. [공개 로드맵](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}) (현재 상태) [응답 토큰](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html) 의 일부로 노출됩니다. `propositions` 에 대한 응답으로 `sendEvent` 호출합니다. |

## at.js 설정 및 이에 해당하는 Platform Web SDK

Target UI의 다양한 설정을 사용하여 at.js 라이브러리를 구성하고 다운로드할 수 있습니다. 이러한 설정은 다음을 사용하여 업데이트할 수도 있습니다. [`targetGlobalSettings()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/targetglobalsettings/) 함수. 아래 표는 이러한 설정을 Platform Web SDK에서 사용할 수 있는 설정과 비교합니다.

| at.js 설정 | Platform Web SDK에 해당하는 함수 |
| --- | --- |
| `bodyHiddenStyle` | 설정 [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#prehidingStyle) (으)로 `configure` 명령 |
| `bodyHidingEnabled` | 다음과 같은 경우 `prehidingStyle` 을 사용하여 정의됨 `configure` 명령을 실행하면 이 기능이 활성화됩니다. 스타일이 정의되지 않은 경우 Platform Web SDK는 콘텐츠를 숨기지 않습니다. |
| `clientCode` | 자동으로 구성됨 |
| `cookieDomain` | 해당되지 않음 |
| `crossDomain` | 설정 `thirdPartyCookiesEnabled` 옵션 대상 `true` (으)로 `configure` 도메인 간 사용 사례에 대해 자사 및 타사 쿠키를 활성화하는 명령 |
| `cspScriptNonce` 및 `cspStyleNonce` | 다음 설명서를 참조하십시오. [CSP 구성](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-a-csp.html) |
| `dataProviders` | 지원되지 않음 |
| `decisioningMethod` | 모든 Platform Web SDK `sendEvent` 명령은 서버측 의사 결정을 사용합니다. 하이브리드 및 온디바이스 의사 결정은 지원되지 않습니다. |
| `defaultContentHiddenStyle` 및 `defaultContentVisibleStyle` | at.js 1.x에서만 적용할 수 있습니다. at.js 2.x와 마찬가지로, 양식 기반 경험에 대한 플리커 완화는 사용자 지정 코드를 사용하여 수행할 수 있습니다. |
| `deviceIdLifetime` | 지원되지 않음. If `targetMigrationEnabled` 이(가) (으)로 설정됨 `true` (으)로 `configure` 명령, `mbox` cookie는 장치 라이프타임이 2년으로 설정된 상태로 설정됩니다. 이 값은 구성할 수 없습니다. |
| `enabled` | 대상 기능은 데이터 스트림 구성으로 활성화되거나 비활성화됩니다. |
| `globalMboxAutoCreate` | 설정 `renderDecisions` 옵션 대상 `true` (으)로 `sendEvent` vec 기반 경험을 자동으로 가져오고 렌더링하는 명령입니다.<br><br>요청 a `decisionScope` 대상 `__view__` vec 기반 경험을 수동으로 렌더링하려는 경우. |
| `imsOrgId` | 설정 `orgId` (으)로 `configure` 명령 |
| `optinEnabled` 및 `optoutEnabled` | Platform Web SDK 를 참조하십시오 [개인 정보 보호 옵션](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html). 다음 `defaultConsent` 옵션은 Platform Web SDK가 지원하는 모든 Adobe 솔루션에 적용됩니다. |
| `overrideMboxEdgeServer` 및 `overrideMboxEdgeServerTimeout` | 해당되지 않음. 모든 Platform Web SDK 요청은 Adobe Experience Platform Edge 네트워크를 사용합니다. |
| `pageLoadEnabled` | 설정 `renderDecisions` 옵션 대상 `true` (으)로 `sendEvent` 명령 |
| `secureOnly` | 지원되지 않음. Platform Web SDK는 `secure` 및 `sameSite="none"` 속성. |
| `selectorsPollingTimeout` | 지원되지 않음. Platform Web SDK는 5초 값을 사용합니다. 필요한 경우 사용자 지정 코드를 사용하여 콘텐츠를 수동으로 렌더링할 수 있습니다. |
| `serverDomain` | 사용 `edgeDomain` 를 사용하여 설정 `configure` 명령 |
| `telemetryEnabled` | 해당되지 않음 |
| `timeout` | 지원되지 않음. 깜박임 완화 코드에 적절한 시간 제한이 포함되어 있는지 확인하는 것이 좋습니다. |
| `viewsEnabled` | 지원되지 않음. Target 보기의 콘텐츠는 항상 첫 번째 위치에서 가져옵니다. `sendEvent()` 다음과 같은 경우 호출 `renderDecisions` 이(가) (으)로 설정됨 `true` 또는 `__view__` decisionScope가 요청에 포함되어 있습니다. |
| `visitorApiTimeout` | 해당되지 않음 |


## 시스템 다이어그램 비교

다음 다이어그램은 at.js를 사용하는 Target 구현과 Platform Web SDK를 사용하는 구현 간의 데이터 흐름 차이를 이해하는 데 도움이 됩니다.

### at.js 2.x 시스템 다이어그램

![페이지 로드 시 at.js 2.0 동작](assets/target-at-js-2x-diagram.png){zoomable=&quot;yes&quot;}

| 호출 | 세부 사항 |
| --- | --- |
| 1 | 호출이 ECID(Experience Cloud ID)를 반환합니다. 사용자가 인증되면 다른 호출이 고객 ID를 동기화합니다. |
| 2 | at.js 라이브러리는 동기식으로 로드되며 문서 본문을 숨깁니다(at.js는 페이지에 구현된 코드 조각을 미리 숨기는 선택 사항을 사용하여 비동기식으로 로드할 수도 있습니다). |
| 3 | 모든 구성된 매개 변수, ECID, SDID 및 고객 ID를 포함하는 페이지 로드 요청이 이루어집니다. |
| 4 | 프로필 스크립트가 실행되어 프로필 스토어에 반영됩니다. 저장소는 대상 라이브러리의 적절한 대상(예: Analytics, Audience Manager 등에서 공유되는 대상)을 요청합니다. 고객 속성은 묶음 프로세스를 통해 프로필 저장소로 전송됩니다. |
| 5 | Target에서는 URL, 요청 매개 변수 및 프로필 데이터를 기반으로 현재 페이지 및 미래 보기를 위해 방문자에게 반환할 활동 및 경험을 결정합니다. |
| 6 | 타깃팅된 컨텐츠를 다시 페이지로 전송하며, 원할 경우 추가적인 개인화를 위한 프로필 값을 포함할 수 있습니다.<br><br>현재 페이지의 타기팅된 콘텐츠는 기본 콘텐츠의 플리커 없이 가능한 한 빨리 나타납니다.<br><br>단일 페이지 애플리케이션의 향후 보기를 위한 타깃팅된 콘텐츠는 브라우저에 캐시되므로 보기가 트리거될 때 추가적인 서버 호출 없이 즉시 적용될 수 있습니다. |
| 7 | 페이지에서 데이터 수집 서버로 전송된 Analytics 데이터. |
| 8 | Target 데이터는 SDID를 통해 Analytics 데이터에 대응되며 Analytics 보고 저장소로 처리됩니다. 그런 다음 Analytics 데이터는 A4T 보고서를 통해 Analytics 및 Target 모두에서 볼 수 있게 됩니다. |

자세한 내용은 개발자 안내서 를 참조하십시오 [단일 페이지 애플리케이션용 at.js를 사용하여 Target 구현](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application/).

### Platform Web SDK 시스템 다이어그램

![Platform Web SDK를 사용한 Adobe Target Edge Decisioning 다이어그램](assets/target-platform-web-sdk.png)

| 호출 | 세부 사항 |
| --- | --- |
| 1 | 디바이스가 Platform Web SDK를 로드합니다. Platform Web SDK는 XDM 데이터, 데이터스트림 환경 ID, 전달된 매개 변수 및 고객 ID(선택 사항)를 사용하여 Edge Network에 요청을 보냅니다. 페이지(또는 컨테이너)가 미리 숨겨져 있습니다. |
| 2 | Edge 네트워크는 Edge 서비스에 요청을 전송하여 방문자 ID, 동의와 지리적 위치 및 장치 친화적 이름과 같은 기타 방문자 컨텍스트 정보로 보강합니다. |
| 3 | Edge 네트워크는 방문자 ID 및 전달된 매개 변수와 함께 보강된 개인화 요청을 Target Edge로 보냅니다. |
| 4 | 프로필 스크립트가 실행된 다음 Target 프로필 저장소에 반영됩니다. 프로필 저장소는 대상 라이브러리의 세그먼트(예: Adobe Analytics, Adobe Audience Manager, Adobe Experience Platform에서 공유된 세그먼트)를 가져옵니다. |
| 5 | Target은 URL 요청 매개 변수 및 프로필 데이터를 기반으로 현재 페이지 보기 및 향후 프리페치된 보기에 대해 방문자에게 표시할 활동 및 경험을 결정합니다. 그러면 Target이 이를 다시 에지 네트워크로 보냅니다. |
| 6 | a. 에지 네트워크는 추가적인 개인화를 위한 프로필 값을 선택적으로 포함하여 개인화 응답을 다시 페이지로 전송합니다. 현재 페이지의 개인화된 콘텐츠는 기본 콘텐츠의 플리커 없이 가능한 한 빨리 나타납니다.<br><br>b. 단일 페이지 애플리케이션(SPA)에서 사용자 작업의 결과로 표시되는 보기를 위한 개인화된 콘텐츠는 추가 서버 호출 없이 즉각적인 렌더링을 위해 캐시됩니다.<br><br>c. Edge 네트워크는 방문자 ID와 쿠키의 다른 값(예: 동의, 세션 ID, ID, 쿠키 확인, 개인화 등)을 전송합니다. |
| 7 | 에지 네트워크는 Analytics for Target(A4T) 세부 사항(활동, 경험 및 전환 메타데이터)을 Analytics 에지로 전달합니다. |

자세한 내용은 개발자 안내서 를 참조하십시오 [단일 페이지 애플리케이션용 Platform Web SDK를 사용하여 Target 구현](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html).

현재 Target 구현과 사용하는 기능에 대한 기술적인 이해를 완료한 후 다음 단계는 를 수행하는 것입니다. [초기 설정](initial-setup.md).

>[!NOTE]
>
>at.js에서 Web SDK로 Target을 성공적으로 마이그레이션할 수 있도록 지원하기 위해 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락되었다고 생각되는 경우 다음 위치에 게시하여 알려 주십시오. [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
