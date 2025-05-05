---
title: Target을 at.js 2.x에서 Web SDK로 마이그레이션
description: Adobe Target 구현을 at.js 2.x에서 Adobe Experience Platform Web SDK로 마이그레이션하는 방법에 대해 알아봅니다. 주제에는 라이브러리 개요, 구현 차이점 및 기타 주목할 만한 설명선이 포함됩니다.
exl-id: 43b9ae91-4524-4071-9eb4-12a0a8aec242
source-git-commit: 4690d41f92c83fe17eda588538d397ae1fa28af0
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 1%

---

# 양식 기반 작성기를 사용하는 Target 활동 렌더링

일부 Target 구현에서는 지역 mbox(이제 &quot;범위&quot;라고 함)를 사용하여 양식 기반 경험 작성기를 사용하는 활동의 콘텐츠를 전달할 수 있습니다. at.js Target 구현에서 mbox를 사용하는 경우 다음을 수행해야 합니다.

* `getOffer()` 또는 `getOffers()`을(를) 사용하는 at.js 구현의 모든 참조를 동일한 Platform Web SDK 메서드로 업데이트합니다.
* 노출이 계산되도록 `propositionDisplay` 이벤트를 트리거하는 코드를 추가하십시오.

## 요청 시 콘텐츠 요청 및 적용

Target의 양식 기반 작성기를 사용하여 만들어 지역 mbox에 전달된 활동은 Platform Web SDK에서 자동으로 렌더링할 수 없습니다. at.js와 유사하게, 특정 Target 위치에 전달된 오퍼는 요청 시 렌더링해야 합니다.


+++at.js `getOffer()` 및 `applyOffer()` 사용 예:

1. 위치에 대한 오퍼를 요청하려면 `getOffer()`을(를) 실행하십시오.
1. `applyOffer()`을(를) 실행하여 오퍼를 지정된 선택기에 렌더링합니다.
1. `getOffer()` 요청 시 활동 노출 수가 자동으로 증가합니다.

```JavaScript
// Retrieve an offer for the homepage-hero location
adobe.target.getOffer({
  "mbox": "homepage_hero",

  // Render offer to the #hero-banner selector
  "success": function(offers) {
    adobe.target.applyOffer({
      "mbox": "homepage_hero",
      "selector": "#hero-banner",
      "offer": offers
    });
  },
  "error": {
    console.log(error);
  },
  "timeout": 3000
});
```

+++

+++`applyPropositions` 명령을 사용하는 Platform Web SDK에 해당합니다.

1. `sendEvent` 명령을 실행하여 하나 이상의 위치(범위)에 대한 오퍼(제안)를 요청합니다.
1. 각 범위의 페이지에 콘텐츠를 적용하는 방법에 대한 지침을 제공하는 메타데이터 개체로 `applyPropositions` 명령을 실행하십시오.
1. `decisioning.propositionDisplay`의 eventType으로 `sendEvent` 명령을 실행하여 노출을 추적합니다.

```JavaScript
// Retrieve propositions for homepage_hero location (scope)
alloy("sendEvent", {
  "decisionScopes": ["homepage_hero"]
}).then(function(result) {
  var retrievedPropositions = result.propositions;
    
  // Render offer (proposition) to the #hero-banner selector by supplying extra metadata
  return alloy("applyPropositions", {
    "propositions": retrievedPropositions,
    "metadata": {
      // Specify each regional mbox or scope name along with a selector and actionType
      "homepage_hero": {
        "selector": "#hero-banner",
        "actionType": "setHtml"
      }
    }
  }).then(function(applyPropositionsResult) {
    var renderedPropositions = applyPropositionsResult.propositions;

    // Send the display notifications via sendEvent command
    alloy("sendEvent", {
      "xdm": {
        "eventType": "decisioning.propositionDisplay",
        "_experience": {
          "decisioning": {
            "propositions": renderedPropositions
          }
        }
      }
    });
  });
});
```

+++

Platform Web SDK는 지정된 `actionType`과(와) 함께 `applyPropositions` 명령을 사용하여 양식 기반 활동을 페이지에 적용하기 위한 보다 강력한 컨트롤을 제공합니다.

| `actionType` | 설명 | at.js `applyOffer()` | Platform Web SDK `applyPropositions` |
| --- | --- | --- | --- |
| `setHtml` | 컨테이너의 콘텐츠를 지운 다음 오퍼를 컨테이너에 추가합니다 | 예(항상 사용됨) | 예 |
| `replaceHtml` | 컨테이너를 제거하고 오퍼로 바꿉니다. | 아니요 | 예 |
| `appendHtml` | 지정된 선택기 뒤에 오퍼를 추가합니다. | 아니요 | 예 |

추가 렌더링 옵션 및 예제는 Platform Web SDK를 사용한 콘텐츠 렌더링에 대한 [전용 설명서](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html)를 참조하십시오.

## 구현 예

아래 예제 페이지는 이전 섹션에 설명된 구현에 따라 작성되며, `sendEvent` 명령에 추가 범위만 추가합니다.

+++여러 범위가 있는 Platform Web SDK 예

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>

  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>

  <!--Prehiding snippet for Target with asynchronous deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

  <!--Platform Web SDK base code-->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
  <script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>
  
  <!--Configure Platform Web SDK then send event-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    alloy("sendEvent", {
      // Request and render VEC-based activities
      "renderDecisions": true,
      // Request content for form-based activities using the "homepage_hero" scope
      "decisionScopes": ["homepage_hero"]
    }).then(function(result) {
      var retrievedPropositions = result.propositions;
        
      // Render offer (proposition) to the #hero-banner selector by supplying extra metadata
      return alloy("applyPropositions", {
        "propositions": retrievedPropositions,
        "metadata": {
          // Specify each regional mbox or scope name along with a selector and actionType
          "homepage_hero": {
            "selector": "#hero-banner",
            "actionType": "setHtml"
          }
        }
      }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
        alloy("sendEvent", {
          "xdm": {
            "eventType": "decisioning.propositionDisplay",
            "_experience": {
              "decisioning": {
                "propositions": renderedPropositions
              }
            }
          }
        });
      });
    });
  </script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div id="homepage-hero">Homepage Hero Banner Content</div>
</body>
</html>
```

다음으로 Platform Web SDK를 사용하여 [Target 매개 변수를 전달](send-parameters.md)하는 방법에 대해 알아봅니다.

>[!NOTE]
>
>at.js에서 Web SDK로 Target을 성공적으로 마이그레이션할 수 있도록 지원하기 위해 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)에 게시하여 알려 주십시오.
