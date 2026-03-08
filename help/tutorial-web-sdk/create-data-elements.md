---
title: Platform Web SDK에 대한 데이터 요소 만들기
description: XDM 개체를 만들고 데이터 요소를 태그에 매핑하는 방법에 대해 알아봅니다. 이 수업은 Web SDK를 사용하여 Adobe Experience Cloud 구현 튜토리얼의 일부입니다.
feature: Tags
jira: KT-15401
exl-id: d662ec46-de9b-44ba-974a-f81dfc842e68
source-git-commit: 070fc02801d3403bf65ca732323338481e25b581
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 2%

---

# 데이터 요소 만들기

[Luma 데모 웹 사이트](https://luma.enablementadobe.com)에서 컨텐츠, 상거래 및 ID 데이터의 태그에 데이터 요소를 만드는 방법을 알아봅니다. 그런 다음 XDM 스키마의 필드를 채웁니다.



## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* 데이터 레이어를 XDM에 매핑하는 다양한 방법 이해
* 데이터 요소를 만들어 데이터 캡처
* XDM 개체에 데이터 요소 매핑


## 전제 조건

데이터 계층이 무엇인지 이해하고 자습서의 이전 단원을 완료했습니다.

* [XDM 스키마 구성](configure-schemas.md)
* [ID 네임스페이스 구성](configure-identities.md)
* [데이터스트림 구성](configure-datastream.md)
* [태그 속성에 설치된 웹 SDK 확장](install-web-sdk.md)


>[!IMPORTANT]
>
>이 단원의 데이터는 `[!UICONTROL adobeDataLayer]`Luma 사이트[의 &#x200B;](https://luma.enablementadobe.com) 데이터 레이어에서 가져옵니다. 데이터 레이어를 보려면 개발자 콘솔을 열고 `[!UICONTROL adobeDataLayer]`을(를) 입력하여 사용 가능한 전체 데이터 레이어를 확인하십시오.![adobeDataLayer 데이터 레이어](assets/data-element-data-layer-new.png)


## 데이터 레이어 접근 방식

Adobe Experience Platform의 태그 기능을 사용하여 데이터 레이어의 데이터를 XDM에 매핑하는 방법에는 여러 가지가 있습니다. 아래는 세 가지 다른 접근 방식의 몇 가지 장단점입니다. 원하는 경우 접근 방식을 결합할 수 있습니다.

1. 데이터 레이어에서 XDM 구현
1. 태그의 XDM에 매핑
1. 데이터 스트림의 XDM에 매핑

>[!NOTE]
>
>이 자습서의 예제는 태그 접근 방식으로 XDM에 매핑 을 따르십시오.


### 데이터 레이어에서 XDM 구현

이 접근 방식에서는 웹 개발자가 데이터 레이어의 구조로서 완전히 정의된 XDM 개체를 구현합니다. 그러면 전체 데이터 레이어를 태그의 XDM 개체에 매핑하기만 하면 됩니다. 구현에서 태그 관리자를 사용하지 않는 경우 [XDM sendEvent 명령](https://experienceleague.adobe.com/en/docs/experience-platform/edge/fundamentals/tracking-events#sending-xdm-data)을 사용하여 응용 프로그램에서 직접 XDM으로 데이터를 보낼 수 있으므로 이 방법이 이상적일 수 있습니다. 태그를 사용하는 경우 전체 데이터 레이어를 XDM에 대한 통과 JSON 개체로 캡처하는 사용자 지정 코드 데이터 요소를 만들 수 있습니다. 그런 다음 통과 JSON을 이벤트 보내기 작업의 XDM 개체 필드에 매핑합니다.

다음은 Adobe 클라이언트 데이터 레이어 형식을 사용하는 데이터 레이어의 모습에 대한 예입니다.

+++데이터 레이어 예제의 XDM

```JSON
window.adobeDataLayer.push({
"eventType": "web.webPageDetails.pageViews",
"web":{
         "webInteraction":{
            "linkClicks":{
               "id":"",
               "value":""
            },
            "URL":"",
            "name":"",
            "region":"",
            "type":""
         },
         "webPageDetails":{
            "pageViews":{
               "id":"",
               "value":"1"
            },
            "URL":"https://luma.enablementadobe.com/",
            "isErrorPage":"",
            "isHomePage":"",
            "name":"luma:home",
            "server":"enablementadobe.com",
            "siteSection":"home",
            "viewName":""
         },
         "webReferrer":{
            "URL":"",
            "type":""
         }
      }
});
```

+++

장점

* 데이터 레이어 변수를 XDM으로 다시 매핑하는 추가 단계를 제거합니다.
* 웹 개발 팀이 디지털 동작에 대한 태깅도 소유하는 경우 배포하는 것이 더 빠를 수 있습니다

단점

* XDM으로 이동되는 데이터를 업데이트하기 위해 개발 팀 및 개발 주기에 전적으로 의존
* XDM이 데이터 레이어에서 정확한 페이로드를 수신하므로 유연성이 제한됨
* 빠른 배포를 위해 스크래핑, 지속성, 기능과 같은 내장 태그 기능을 사용할 수 없음
* 타사 픽셀에는 데이터 레이어를 사용하기 어렵습니다. 그러나 이러한 픽셀을 [이벤트 전달](setup-event-forwarding.md)(으)로 이동해야 할 수도 있습니다.
* 데이터 레이어와 XDM 간에 데이터를 변환할 수 없음

### 태그의 XDM에 매핑

이 접근 방법에는 개별 데이터 계층 변수를 태그의 데이터 요소와 최종적으로 XDM에 매핑하는 작업이 포함됩니다. 이는 태그 관리 시스템을 사용하여 를 구현하는 기존 접근 방식입니다.

#### 장점

* XDM에 도달하기 전에 개별 변수를 제어하고 데이터를 변환할 수 있는 가장 유연한 접근 방법입니다
* Adobe 태그 트리거 및 스크래핑 기능을 사용하여 데이터를 XDM에 전달할 수 있음
* 클라이언트측 서드파티 픽셀에 데이터 요소 매핑 가능

#### 단점

* 데이터 레이어를 태그 데이터 요소로 재구성하는 데 시간이 소요됩니다


>[!IMPORTANT]
>
>앞에서 설명한 바와 같이 이 자습서의 예제는 태그의 XDM에 매핑 접근 방식을 따릅니다.

### 데이터 스트림의 XDM에 매핑

이 방법은 데이터 스트림 구성에 내장된 기능([데이터 수집을 위한 데이터 준비](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/data-prep))을 사용하고 데이터 레이어 변수를 태그의 XDM에 매핑하는 작업을 건너뜁니다.

#### 장점

* 포인트 앤 클릭 UI에서 개별 변수를 XDM에 유연하게 매핑
* XDM으로 이동하기 전에 데이터 레이어에서 [새 값을 계산](https://experienceleague.adobe.com/en/docs/experience-platform/data-prep/functions) 또는 [데이터 형식을 변환](https://experienceleague.adobe.com/en/docs/experience-platform/data-prep/data-handling)하는 기능

#### 단점

* 데이터 레이어 변수를 클라이언트측 타사 픽셀에 대한 데이터 요소로 사용할 수 없지만 이벤트 전달과 함께 사용할 수 있습니다
* 태그에서 스크래핑 기능을 사용할 수 없음
* 태그와 데이터스트림 모두에서 데이터 레이어를 매핑할 경우 유지 관리 복잡성이 증가합니다


>[!TIP]
>
> Google 데이터 레이어
> 
> 조직에서 이미 Google Analytics을 사용하고 있고 웹 사이트에 기존 Google dataLayer 개체가 있는 경우 태그에서 [Google 데이터 레이어 확장](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/google-data-layer/overview)을 사용할 수 있습니다. 이렇게 하면 IT 팀에 지원을 요청하지 않고도 Adobe 기술을 보다 신속하게 배포할 수 있습니다. Google 데이터 레이어를 XDM에 매핑하면 위와 동일한 단계를 따릅니다.


## 데이터 요소를 만들어 데이터 레이어 캡처

XDM 필드를 채우기 전에 먼저 필요한 데이터 포인트를 태그 데이터 요소로 캡처합니다.

1. **[!UICONTROL 데이터 요소]**(으)로 이동하여 **[!UICONTROL 데이터 요소 추가]**(또는 태그 속성에 기존 데이터 요소가 없는 경우 **[!UICONTROL 새 데이터 요소 만들기]**)를 선택합니다.

   ![데이터 요소 만들기](assets/data-element-create.png)

1. 데이터 요소에 이름을 지정합니다 `Page Name`
1. **[!UICONTROL JavaScript 변수]** **[!UICONTROL 데이터 요소 유형]**&#x200B;을(를) 사용하여 Luma의 데이터 계층에 있는 값을 가리킵니다. `adobeDataLayer.0.page.name`

1. **[!UICONTROL 소문자 값 강제 적용]** 및 **[!UICONTROL 클린 텍스트]** 상자를 체크하여 케이스를 표준화하고 외부 공백을 제거합니다

1. 이 값은 모든 페이지에서 다르므로 `None`을(를) **[!UICONTROL 저장 유지 시간]** 설정으로 둡니다.

1. **[!UICONTROL 저장]** 선택

   ![페이지 이름 데이터 요소](assets/data-element-pageName.png)

동일한 단계를 수행하여 이러한 추가 데이터 요소를 만듭니다.

* **`User Id`**&#x200B;이(가) 다음에 매핑됨
  `adobeDataLayer.0.user.id`

* **`User Logged In`**&#x200B;이(가) 다음에 매핑됨
  `adobeDataLayer.0.user.loggedIn`

* **`Ecommerce Product Id`**&#x200B;이(가) `adobeDataLayer.0.ecommerce.detail.products.0.id`에 매핑됨
* **`Ecommerce Product Name`**&#x200B;이(가) `adobeDataLayer.0.ecommerce.detail.products.0.name`에 매핑됨
* **`Ecommerce Purchase Id`**&#x200B;이(가) `adobeDataLayer.0.ecommerce.purchase.actionField.id`에 매핑됨
* **`Ecommerce Product Category`** **[!UICONTROL 사용자 지정 코드]** **[!UICONTROL 데이터 요소 형식]** 및 다음 사용자 지정 코드를 사용:

  ```javascript
  return adobeDataLayer[0].ecommerce.detail.products[0].category+":"+adobeDataLayer[0].ecommerce.detail.products[0].subcategory;
  ```

* 다음 사용자 지정 코드를 사용하는 **`Ecommerce Cart Products`**:

  ```javascript
  const cartProducts = adobeDataLayer
  .flatMap(evt => Array.isArray(evt?.ecommerce?.cart?.items) ? evt.ecommerce.cart.items : [])
  .filter(item => item && item.id && item.name && item.brand)
  .map(({ id, name, brand }) => ({ id, name, brand }));
  
  return cartProducts;
  ```

* 다음 사용자 지정 코드를 사용하는 **`Ecommerce Purchase Products`**:

  ```javascript
  const purchaseEvent = adobeDataLayer.find(e => e.event === "purchase");
  
  const currencyCode = purchaseEvent?.ecommerce?.currencyCode ?? "USD";
  
  const purchasedProducts = (purchaseEvent?.ecommerce?.purchase?.products || []).map(p => {
     const unitPrice = parseFloat(String(p.price).replace(/[^0-9.-]/g, "")) || 0;
     const qty = Number(p.quantity) || 0;
  
     return {
     SKU: p.id,                       // id -> SKU
     name: p.name,                    // name -> name
     quantity: qty,                   // quantity -> quantity
     priceTotal: unitPrice * qty,     // price -> priceTotal (unit price × quantity)
     currencyCode                     // "USD" -> currencyCode (from ecommerce.currencyCode)
     };
  });
  
  return(purchasedProducts);
  ```


>[!CAUTION]
>
>[!UICONTROL JavaScript 변수] 데이터 요소 형식은 배열 참조를 대괄호 대신 점으로 처리하므로 사용자 이름 데이터 요소를 `adobeDataLayer[0].page.name` **로 참조하면 작동하지 않습니다**.

## XDM 및 데이터 개체에 대한 변수 데이터 요소 만들기

방금 만든 데이터 요소는 XDM 개체(플랫폼 애플리케이션용)와 데이터 개체(Analytics, Target 및 Audience Manager용)를 빌드하는 데 사용됩니다. 이러한 개체에는 매우 쉽게 만들 수 있는 **[!UICONTROL 변수]** 데이터 요소라는 고유한 특수 데이터 요소가 있습니다.

XDM에 대한 변수 데이터 요소를 만들려면 [스키마 구성](configure-schemas.md) 단원에서 만든 스키마에 연결합니다.

1. **[!UICONTROL 데이터 요소 추가]** 선택
1. 데이터 요소 이름을 `XDM Variable`로 지정합니다. 태그 속성을 더 잘 구성하려면 XDM과 관련된 데이터 요소를 &quot;XDM&quot; 접두사로 사용하는 것이 좋습니다
1. **[!UICONTROL Adobe Experience Platform Web SDK]**&#x200B;을(를) **[!UICONTROL 확장]**(으)로 선택
1. **[!UICONTROL 변수]**&#x200B;을(를) **[!UICONTROL 데이터 요소 형식]**(으)로 선택합니다.
1. **[!UICONTROL XDM]**&#x200B;을(를) **[!UICONTROL 속성]**(으)로 선택
1. 스키마를 만든 **[!UICONTROL 샌드박스]**&#x200B;를 선택하십시오.
1. 적절한 **[!UICONTROL 스키마]**(이 경우 `Luma Web Event Data`)를 선택하십시오.
1. **[!UICONTROL 저장]** 선택

   ![XDM에 대한 변수 데이터 요소](assets/analytics-tags-data-element-xdm-variable.png)

그런 다음 데이터 개체에 대한 변수 데이터 요소를 만듭니다.

1. **[!UICONTROL 데이터 요소 추가]** 선택
1. 데이터 요소 이름을 `Data Variable`로 지정합니다.
1. **[!UICONTROL Adobe Experience Platform Web SDK]**&#x200B;을(를) **[!UICONTROL 확장]**(으)로 선택
1. **[!UICONTROL 변수]**&#x200B;을(를) **[!UICONTROL 데이터 요소 형식]**(으)로 선택합니다.
1. **[!UICONTROL data]**&#x200B;을(를) **[!UICONTROL property]**(으)로 선택
1. 이 자습서의 일부로 구현할 Experience Cloud 솔루션을 선택합니다
1. **[!UICONTROL 저장]** 선택

   ![데이터 개체에 대한 변수 데이터 요소](assets/data-element-data-variable.png)


이러한 단계를 마치면 다음 데이터 요소를 만들어야 합니다.

| 코어 확장 데이터 요소 | Platform 웹 SDK 확장 데이터 요소 |
| ----------------------------- | ------------------------------- |
| `Ecommerce Cart Products` | `Data Variable` |
| `Ecommerce Product Category` | `XDM Variable` |
| `Ecommerce Product Id` | |
| `Ecommerce Product Name` | |
| `Ecommerce Purchase Id` | |
| `Ecommerce Purchase Products` | |
| `Page Name` | |
| `User Id` | |
| `User Logged In` | |

이러한 데이터 요소가 준비되면 태그 규칙을 사용하여 Platform Edge Network에 데이터를 전송할 수 있습니다. 하지만 먼저 웹 SDK을 사용하여 ID를 수집하는 방법에 대해 알아봅니다.

>[!NOTE]
>
>Adobe Experience Platform 웹 SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하고 싶거나 향후 콘텐츠에 대한 제안이 있는 경우 이 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/adobe-experience-platform-18/tutorial-discussion-implement-adobe-experience-cloud-with-web-sdk-tutorial-248848)에서 공유하십시오.
