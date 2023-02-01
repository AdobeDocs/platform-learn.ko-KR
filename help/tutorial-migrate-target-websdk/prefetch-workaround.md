---
title: 미리 가져오기에 대한 해결 방법 | at.js 2.x에서 웹 SDK로 Target 마이그레이션
description: 미리 가져오기를 사용하여 매개 변수 전달에 대한 해결 방법을 구현하는 방법을 알아봅니다
source-git-commit: d061d2492d6d5e8e7a8a6e03ce63b9b6cd3793d8
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# 미리 가져오기에 대한 해결 방법

2022년 10월 1일 이전에 Experience Platform Web SDK를 사용하여 프로덕션 상태에 있지 않은 모든 Target 고객은 &quot;미리 가져오기&quot; 모드를 사용하여 Experience Platform Edge 네트워크의 Target을 요청합니다. 미리 가져오기를 사용하면 방문자가 페이지의 올바른 상태에 도달했을 때 적용할 준비가 되도록 브라우저에서 Target 오퍼을 미리 로드하고 캐시할 수 있습니다. 이 기능은 추가적인 네트워크 요청 없이 원하는 사용자 경험을 가능한 한 빨리 렌더링할 수 있으므로 단일 페이지 애플리케이션(SPA)에 유용합니다. 그러나 SPA 구현과 비 SPA 구현 모두에 중요한 의미가 있습니다.

방문자는 이제 네트워크 요청에서 오퍼 컨텐츠가 전달될 때 활동에서 방문자를 계산하지 않고, `propositionDisplay` sendEvent 요청은 웹 SDK에 의해 수행됩니다. 이러한 요청은 renderDecisions가 true로 설정되어 있고 경험이 페이지에서 성공적으로 렌더링되었을 때 VEC(시각적 경험 작성기) 활동에 의해 자동으로 수행됩니다. 사용자 지정 범위 및 renderDecisionals가 false로 설정된 경우 시행자가 progionDisplay 요청을 의도적으로 시작해야 합니다. 또한, _즉각적인 활동 자격 이외의 목적으로 사용되는 모든 매개 변수는 `propositionDisplay`  이벤트_.

## 해결 방법이 필요한 이유는 무엇입니까?

많은 Target 구현에서 전달되는 활동이 예상되지 않고 중요한 네트워크 요청이 수행되는 경우가 있습니다. 예를 들어 다음 항목에 대한 요청을 수행할 수 있습니다.

* 주문 전환 기록
* 프로필 매개 변수 설정
* 프로필 스크립트 트리거
* 엔티티 매개 변수를 전송하여 Recommendations 카탈로그를 채웁니다

안타깝게도 미리 가져오기 모드에서는 예상대로 작동하지 않습니다. 미리 가져오기 모드에서는 이 데이터가 `propositionDisplay`.

## 해결 방법은 무엇입니까?

해결 방법은 다음 세 부분으로 구성됩니다.

1. 사용자 지정 범위를 의 일부로 정의 `sendEvent`
1. 양식 기반 활동에서 사용자 지정 범위를 사용합니다(활동에서 기본 콘텐츠를 제공할 수 있음)
1. 다른 응답을 만들려면 응답 핸들러를 사용하십시오 `sendEvent` propDisplay에 대해 순서를 캡처하고 프로필 매개 변수를 설정하고 프로필 스크립트를 트리거하고 엔티티 매개 변수 등을 전송하는 데 필요한 매개 변수를 포함합니다.

예를 들어, 다음은 프로필 매개 변수를 전송하는 데 해결 방법을 사용하는 방법의 예입니다.


```JavaScript
var data = {
    "__adobe": {
        "target": {
            "profile.gender": "male"
        }
    }
};
// Send the initial event with the data object and custom decision scope
alloy("sendEvent", {
    "renderDecisions": true,
    data,
    decisionScopes: ['profile-param-example']
}).then(function(result) {
    var propositions = result.propositions;
    var ctaProposition;
    if (propositions) {
        // Find the discount proposition, if it exists.
        for (var i = 0; i < propositions.length; i++) {
            var proposition = propositions[i];
            if (proposition.scope === "profile-param-example") {
                ctaProposition = proposition;
                break;
            }
        }
    }
    if (ctaProposition) {
        // Send a "decisioning.propositionDisplay" event signaling that the proposition has been rendered, and includes the data object again
        alloy("sendEvent", {
            xdm: {
                eventType: "decisioning.propositionDisplay",
                _experience: {
                    decisioning: {
                        propositions: [{
                            id: ctaProposition.id,
                            scope: ctaProposition.scope,
                            scopeDetails: ctaProposition.scopeDetails
                        }]
                    }
                }
            },
            data
        });
    }
});
```

propDisplay의 일부로 프로필이 설정되면 방문자의 프로필에 저장되고 후속 요청에서 사용할 수 있습니다. 동일한 방법을 사용하여 주문 변환 세부 사항 및 엔티티 매개 변수를 보고할 수 있습니다.

태그에서 이벤트 보내기 완료 이벤트 유형을 사용하여 추가 sendEvent가 포함된 이벤트를 트리거합니다.

## 구현에서 미리 가져오기 모드를 사용하는지 어떻게 알 수 있습니까?

계정이 미리 가져오기 모드를 사용하고 있는지 확인하려면 고객 지원 티켓을 열어야 합니다.


>[!NOTE]
>
>Adobe는 at.js에서 웹 SDK로 Target 마이그레이션을 성공적으로 수행할 수 있도록 최선을 다하고 있습니다. 마이그레이션에 문제가 발생했거나 이 안내서에 중요한 정보가 누락된 것 같은 경우에는 로그인한 후 알려 주십시오 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).