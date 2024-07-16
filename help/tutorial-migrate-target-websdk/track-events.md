---
title: 이벤트 추적 | Target을 at.js 2.x에서 Web SDK로 마이그레이션
description: Experience Platform Web SDK를 사용하여 Adobe Target 전환 이벤트를 추적하는 방법에 대해 알아봅니다.
exl-id: 5da772bc-de05-4ea9-afbd-3ef58bc7f025
source-git-commit: 4690d41f92c83fe17eda588538d397ae1fa28af0
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# Platform Web SDK를 사용하여 Target 전환 이벤트 추적

Target에 대한 전환 이벤트는 at.js와 유사한 Platform Web SDK를 사용하여 추적할 수 있습니다. 전환 이벤트는 일반적으로 다음 범주에 속합니다.

* 구성이 필요하지 않은 자동 추적 이벤트
* 모범 사례 Platform Web SDK 구현을 위해 조정해야 하는 구매 전환 이벤트
* 코드 업데이트가 필요한 비구매 전환 이벤트

## 목표 추적 비교

다음 표에서는 at.js 및 Platform Web SDK에서 전환 이벤트를 추적하는 방법을 비교합니다

| 활동 목표 | Target at.js 2.x | Platform Web SDK |
|---|---|---|
| 전환 > 페이지 확인함 | 자동으로 추적됩니다. at.js 요청 페이로드의 `context.address.url` 값을 기반으로 합니다. | 자동으로 추적됩니다. `sendEvent` 페이로드의 `xdm.web.webPageDetails.URL` 값을 기반으로 함 |
| 전환 > mbox 확인함 | `type` 값이 `display`인 `trackEvent()` 또는 `sendNotifications()`을(를) 사용하여 디스플레이 mbox 위치 또는 알림에 대한 요청으로 추적되었습니다. | `decisioning.propositionDisplay`의 `eventType`을(를) 사용하여 Platform Web SDK `sendEvent` 호출로 추적했습니다. |
| 전환 > 요소를 클릭함 | VEC 기반 활동에 대해 자동으로 추적됩니다. in 요청 페이로드에 `notifications` 개체가 있고 `type` 값이 `click`인 at.js 네트워크 호출로 나타납니다. | VEC 기반 활동에 대해 자동으로 추적됩니다. `decisioning.propositionInteract`의 `eventType`을(를) 가진 Platform Web SDK `sendEvent` 호출로 나타납니다. |
| 참여 > 페이지 보기 수 | 자동으로 추적됨 | 자동으로 추적됨 |
| 참여 > 사이트에서 보낸 시간 | 자동으로 추적됨 | 자동으로 추적됨 |

<!--
| Revenue > RPV, AOV, or Total Sales | Tracked based on the `orderTotal` parameter values for the specified mbox(es) | Tracked based on the `xdm.commerce.order.priceTotal` values. Its best to use the "any mbox" option in the goal setup. |
| Revenue > Orders | Tracked based on the unique `orderId` parameter values for the specified mbox(es) | Tracked based on the unique values for `xdm.commerce.order.purchaseID`. Its best to use the "any mbox" option in the goal setup. |
| Engagement > Custom Scoring | Tracked with the `mboxPageValue` parameter. Refer to the [dedicated documentation](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html) for more details. | Tracked with `data.__adobe.target.mboxPageValue` in the `sendEvent` payload |
-->

## 자동으로 추적된 이벤트

다음 전환 목표에서는 구현을 특별히 조정할 필요가 없습니다.

* 전환 > 페이지 확인함
* 전환 > 요소 클릭
* 참여 > 페이지 보기 수
* 참여 > 사이트에서 보낸 시간

>[!NOTE]
>
>Platform Web SDK를 사용하면 요청 페이로드에서 전달된 값을 보다 세밀하게 제어할 수 있습니다. QA URL 및 &quot;페이지 확인함&quot; 전환 목표와 같은 Target 기능이 제대로 작동하는지 확인하려면 `xdm.web.webPageDetails.URL` 값에 적절한 문자 대/소문자가 있는 전체 페이지 URL이 포함되어 있는지 확인하십시오.

<!--
## Purchase conversion events

The following conversion goals are based on the order details information passed in the Platform Web SDK `sendEvent` payload:

* Revenue > Revenue per Visit (RPV)
* Revenue > Average Order Value (AOV)
* Revenue > Total Sales
* Revenue > Orders

Target at.js implementations typically use an order confirmation mbox with the `trackEvent()` or `sendNotifications()` functions to pass the order ID, order total, and a list of product IDs purchased. These methods are specific to Target.

The Platform Web SDK is a shared library for all Adobe applications and you may have other applications such as Adobe Analytics to consider. Because of this shared nature, its best send a single order confirmation call using the appropriate commerce XDM field group.

For more information and an example, refer to the tutorial section about [sending purchase parameters to Target](send-parameters.md#purchase-parameters). 
-->

## 사용자 지정 추적 이벤트

Target 구현은 일반적으로 사용자 지정 전환 이벤트를 사용하여 양식 기반 활동에 대한 클릭을 추적하거나, 흐름에서 전환을 나타내거나, 새 콘텐츠를 요청하지 않고 매개 변수를 전달하는 데 사용됩니다.

아래 표는 몇 가지 일반적인 전환 추적 사용 사례에 해당하는 at.js 접근 방식 및 Platform Web SDK에 대해 간략히 설명합니다.

| 활용 사례 | Target at.js 2.x | Platform Web SDK |
|---|---|---|
| mbox 위치(범위)에 대한 클릭 전환 이벤트 추적 | 특정 mbox 위치에 대해 `type` 값이 `click`인 `trackEvent()` 또는 `sendNotifications()`을(를) 실행합니다. | 이벤트 유형이 `decisioning.propositionInteract`인 `sendEvent` 명령 실행 |
| Target 프로필 매개 변수와 같은 추가 데이터를 포함할 수 있는 사용자 지정 전환 이벤트를 추적합니다 | 특정 mbox 위치에 대해 `type` 값이 `display`인 `trackEvent()` 또는 `sendNotifications()`을(를) 실행합니다. | 이벤트 유형이 `decisioning.propositionDisplay`인 `sendEvent` 명령 실행 |

>[!NOTE]
>
>`decisioning.propositionDisplay`은(는) 특정 범위의 노출을 늘리는 데 가장 일반적으로 사용되지만 일반적으로 at.js `trackEvent()`에 대한 직접 대체 요소로도 사용해야 합니다. 지정하지 않으면 `trackEvent()` 함수가 기본적으로 `display` 형식으로 설정됩니다. 구현을 확인하여 정의한 사용자 지정 전환에 대해 올바른 이벤트 유형을 사용하는지 확인하십시오.

Target 이벤트 추적에 [`trackEvent()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-trackevent/) 및 [`sendNotifications()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21/)을(를) 사용하는 방법에 대한 자세한 내용은 전용 at.js 설명서를 참조하십시오.

`trackEvent()`을(를) 사용하여 mbox 위치의 클릭을 추적하는 at.js 예:

```JavaScript
adobe.target.trackEvent({
  "type": "click",
  "mbox": "homepage_hero"
});
```

Platform Web SDK 구현을 사용하면 `sendEvent` 명령을 호출하고 `_experience.decisioning.propositions` XDM 필드 그룹을 채우고 `eventType`을(를) 다음 두 값 중 하나로 설정하여 이벤트와 사용자 작업을 추적할 수 있습니다.

* `decisioning.propositionDisplay`: Target 활동을 렌더링한다는 신호를 보냅니다.
* `decisioning.propositionInteract`: 마우스 클릭과 같이 사용자가 활동과 상호 작용하도록 신호를 보냅니다.

`_experience.decisioning.propositions` XDM 필드 그룹은 개체의 배열입니다. 각 개체의 속성은 `sendEvent` 명령에서 반환되는 `result.propositions`에서 파생됩니다. `{ id, scope, scopeDetails }`

```JavaScript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];

        if (item.schema === "https://ns.adobe.com/personalization/measurement") {
          // add metric to the DOM element
          const button = document.getElementById("form-based-click-metric");

          button.addEventListener("click", event => {
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
            // send the click track event
            alloy("sendEvent", {
              "xdm": {
                "eventType": "decisioning.propositionInteract",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          });
        }
      }
    }
  }
});
```

다음으로 일관된 방문자 프로필에 대해 [도메인 간 ID 공유를 활성화](cross-domain.md)하는 방법에 대해 알아봅니다.

>[!NOTE]
>
>at.js에서 Web SDK로 Target을 성공적으로 마이그레이션할 수 있도록 지원하기 위해 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)에 게시하여 알려 주십시오.
