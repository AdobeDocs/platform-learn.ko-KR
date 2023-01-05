---
title: 이벤트 추적 | at.js 2.x에서 웹 SDK로 Target 마이그레이션
description: Experience Platform Web SDK를 사용하여 Adobe Target 전환 이벤트를 추적하는 방법을 알아봅니다.
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---


# Platform Web SDK를 사용하여 Target 전환 이벤트 추적

at.js와 유사한 Platform Web SDK를 사용하여 Target에 대한 전환 이벤트를 추적할 수 있습니다. 전환 이벤트는 일반적으로 다음 카테고리로 분류됩니다.

* 구성이 필요 없는 자동 추적 이벤트
* 우수 사례 Platform Web SDK 구현을 위해 조정해야 하는 구매 전환 이벤트
* 코드 업데이트가 필요한 비구매 전환 이벤트

## 목표 추적 비교

다음 표에서는 at.js 및 Platform Web SDK가 전환 이벤트를 추적하는 방법을 비교합니다

| 활동 목표 | at.js 2.x Target | Platform 웹 SDK |
|---|---|---|
| 전환 > 페이지 보기 | 자동으로 추적됩니다. 다음 값 기준 `context.address.url` at.js 요청 페이로드에서 을 참조하십시오. | 자동으로 추적됩니다. 다음 값 기준 `xdm.web.webPageDetails.URL` 에서 `sendEvent` 페이로드 |
| 전환 > mbox 확인함 | 디스플레이 mbox 위치 또는 알림을 사용하여 추적됨 `trackEvent()` 또는 `sendNotifications()` 사용 `type` 값 `display`. | Platform Web SDK를 사용하여 추적됨 `sendEvent` 를 사용하여 호출 `eventType` 의 `decisioning.propositionDisplay`. |
| 전환 > 요소를 클릭함 | VEC 기반 활동에 대해 자동으로 추적됩니다. 가 `notifications` 요청 내 페이로드 및 `type` 값 `click`. | VEC 기반 활동에 대해 자동으로 추적됩니다. Platform 웹 SDK로 표시됨 `sendEvent` 를 사용하여 호출 `eventType` 의 `decisioning.propositionInteract`. |
| 참여 > 페이지 보기 수 | 자동으로 추적됨 | 자동으로 추적됨 |
| 참여 > 사이트에서 보낸 시간 | 자동으로 추적됨 | 자동으로 추적됨 |

<!--
| Revenue > RPV, AOV, or Total Sales | Tracked based on the `orderTotal` parameter values for the specified mbox(es) | Tracked based on the `xdm.commerce.order.priceTotal` values. Its best to use the "any mbox" option in the goal setup. |
| Revenue > Orders | Tracked based on the unique `orderId` parameter values for the specified mbox(es) | Tracked based on the unique values for `xdm.commerce.order.purchaseID`. Its best to use the "any mbox" option in the goal setup. |
| Engagement > Custom Scoring | Tracked with the `mboxPageValue` parameter. Refer to the [dedicated documentation](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html) for more details. | Tracked with `data.__adobe.target.mboxPageValue` in the `sendEvent` payload |
-->

## 자동으로 추적된 이벤트

다음 전환 목표에서는 구현을 특별히 조정할 필요가 없습니다.

* 전환 > 페이지 보기
* 전환 > 요소를 클릭함
* 참여 > 페이지 보기 수
* 참여 > 사이트에서 보낸 시간

>[!NOTE]
>
>Platform Web SDK를 사용하면 요청 페이로드에서 전달된 값을 보다 강력하게 제어할 수 있습니다. QA URL 및 &quot;페이지 보기&quot; 전환 목표와 같은 Target 기능이 제대로 작동하는지 확인하려면, `xdm.web.webPageDetails.URL` 값에는 대/소문자를 사용하는 전체 페이지 URL이 포함되어 있습니다.

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

Target 구현에서는 일반적으로 사용자 지정 전환 이벤트를 사용하여 양식 기반 활동에 대한 클릭 수를 추적하거나, 플로우에서 전환을 나타내거나, 새 콘텐츠를 요청하지 않고 매개 변수를 전달하는 역할을 합니다.

아래 표는 몇 가지 일반적인 전환 추적 사용 사례에 해당하는 at.js 접근 방식과 Platform Web SDK에 대해 간략하게 설명합니다.

| 사용 사례 | at.js 2.x Target | Platform 웹 SDK |
|---|---|---|
| mbox 위치(범위)에 대한 클릭 전환 이벤트 추적 | 실행 `trackEvent()` 또는 `sendNotifications()` 사용 `type` 값 `click` 특정 mbox 위치에 대해 | 실행 `sendEvent` 이벤트 유형이 있는 명령 `decisioning.propositionInteract` |
| Target 프로필 매개 변수와 같은 추가 데이터를 포함할 수 있는 사용자 지정 전환 이벤트를 추적합니다 | 실행 `trackEvent()` 또는 `sendNotifications()` 사용 `type` 값 `display` 특정 mbox 위치에 대해 | 실행 `sendEvent` 이벤트 유형이 있는 명령 `decisioning.propositionDisplay` |

>[!NOTE]
>
>하지만 `decisioning.propositionDisplay` 특정 범위에 대한 노출 횟수를 늘리는 데 가장 일반적으로 사용되며 at.js에 대한 직접 대체로도 사용해야 합니다 `trackEvent()` 일반적으로 다음 `trackEvent()` 함수는 기본적으로 `display` 지정하지 않은 경우. 정의한 사용자 지정 전환에 올바른 이벤트 유형을 사용하려면 구현을 확인하십시오.

사용 방법에 대한 자세한 내용은 전용 at.js 설명서 를 참조하십시오 [`trackEvent()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-trackevent/) 및 [`sendNotifications()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21/) 추적 Target 이벤트에 대한 것입니다.

at.js 예 사용 `trackEvent()` mbox 위치에서 클릭을 추적하려면:

```JavaScript
adobe.target.trackEvent({
  "type": "click",
  "mbox": "homepage_hero"
});
```

Platform 웹 SDK 구현을 통해 `sendEvent` 명령, 채우기 `_experience.decisioning.propositions` XDM 필드 그룹 및 `eventType` 다음 두 값 중 하나를 선택합니다.

* `decisioning.propositionDisplay`: Target 활동을 렌더링한다는 신호를 보냅니다.
* `decisioning.propositionInteract`: 마우스 클릭처럼 활동과 사용자의 상호 작용에 신호를 보냅니다.

다음 `_experience.decisioning.propositions` XDM 필드 그룹은 개체 배열입니다. 각 객체의 속성은 `result.propositions` 이 경우 `sendEvent` 명령: `{ id, scope, scopeDetails }`

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

다음으로, 다음 방법을 배웁니다. [도메인 간 ID 공유 활성화](cross-domain.md) 를 사용하십시오.

>[!NOTE]
>
>Adobe는 at.js에서 웹 SDK로 Target 마이그레이션을 성공적으로 수행할 수 있도록 최선을 다하고 있습니다. 마이그레이션에 문제가 발생했거나 이 안내서에 중요한 정보가 누락된 것 같은 경우에는 로그인한 후 알려 주십시오 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).