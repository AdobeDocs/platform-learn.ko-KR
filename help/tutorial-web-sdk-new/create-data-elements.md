---
title: 데이터 요소 만들기
description: XDM 개체를 만들고 데이터 요소를 태그에 매핑하는 방법에 대해 알아봅니다. 이 단원은 Web SDK를 사용하여 Adobe Experience Cloud 구현 자습서의 일부입니다.
feature: Tags
source-git-commit: aff41fd5ecc57c9c280845669272e15145474e50
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 1%

---

# 데이터 요소 만들기

의 컨텐츠, 상거래 및 ID 데이터에 대한 태그에서 데이터 요소를 만드는 방법을 알아봅니다. [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html). 그런 다음 변수 데이터 요소 유형을 사용하여 XDM 스키마의 필드를 채웁니다.


>[!IMPORTANT]
>
>이 단원의 데이터는 `[!UICONTROL digitalData]` Luma 사이트의 데이터 레이어 데이터 레이어를 보려면 개발자 콘솔을 열고 을 입력합니다. `[!UICONTROL digitalData]` 전체 데이터 레이어를 확인할 수 있습니다.![digitalData 데이터 레이어](assets/data-element-data-layer.png)


## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* 데이터 레이어를 XDM에 매핑하는 다양한 방법 이해
* 콘텐츠 데이터를 캡처할 데이터 요소 만들기
* 데이터 요소를 XDM 개체 데이터 요소에 매핑


## 전제 조건

데이터 계층이 무엇인지 이해하고 있으며 자습서에서 다음 이전 단원을 완료했습니다.

* [XDM 스키마 구성](configure-schemas.md)
* [ID 네임스페이스 구성](configure-identities.md)
* [데이터스트림 구성](configure-datastream.md)
* [태그 속성에 설치된 Web SDK 확장](install-web-sdk.md)

## 데이터 레이어 접근 방식

Adobe Experience Platform의 태그 기능을 사용하여 데이터 레이어의 데이터를 XDM에 매핑하는 방법에는 여러 가지가 있습니다. 다음은 세 가지 접근 방식에 대한 몇 가지 장단점입니다.

* [데이터 레이어에서 XDM 구현](create-data-elements.md#implement-xdm-in-the-data-layer)
* [데이터 스트림의 XDM에 매핑](create-data-elements.md#map-to-xdm-in-the-datastream)
* [태그의 XDM에 매핑](create-data-elements.md#map-data-layer-in-tags)

>[!NOTE]
>
>이 자습서의 예제는 태그 접근 방식으로 XDM에 매핑 을 따르십시오.


### 데이터 레이어에서 XDM 구현

이 접근 방법에는 데이터 레이어의 구조로 완전히 정의된 XDM 개체를 사용하는 작업이 포함됩니다. 그런 다음 전체 데이터 레이어를 Adobe 태그의 XDM 개체 데이터 요소에 매핑합니다. 구현에서 태그 관리자를 사용하지 않는 경우 를 사용하여 애플리케이션에서 직접 XDM으로 데이터를 전송할 수 있으므로 이 방법이 이상적일 수 있습니다. [XDM sendEvent 명령](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#sending-xdm-data). Adobe 태그를 사용하는 경우 전체 데이터 레이어를 XDM에 대한 통과 JSON 개체로 캡처하는 사용자 지정 코드 데이터 요소를 만들 수 있습니다. 그런 다음 통과 JSON을 이벤트 보내기 작업의 XDM 개체 필드에 매핑합니다.

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

* 개별 데이터 레이어 변수를 XDM에 매핑하는 단계를 건너뜁니다.
* 개발 팀이 태그 지정 디지털 동작을 담당하는 경우 배포하는 것이 더 빠를 수 있습니다.

단점

* XDM으로 이동되는 데이터를 업데이트하기 위해 개발 팀 및 개발 주기에 전적으로 의존
* XDM이 데이터 레이어에서 정확한 페이로드를 수신하므로 유연성이 제한됨
* 빠른 배포를 위해 스크래핑, 지속성, 기능과 같은 태그 내장 기능을 사용할 수 없음
* 타사 픽셀에 데이터 레이어를 사용할 수 없습니다.
* 데이터 레이어와 XDM 간에 데이터를 변환할 수 없음

### 데이터 스트림의 XDM에 매핑

이 방법에서는 이라는 데이터 스트림 구성에 내장된 기능을 사용합니다. [데이터 수집을 위한 데이터 준비](https://experienceleague.adobe.com/docs/experience-platform/datastreams/data-prep.html) 및 는 태그의 데이터 레이어 변수를 XDM에 매핑하는 것을 건너뜁니다.

장점

* 개별 변수를 XDM에 매핑할 수 있어 유연함
* 다음에 대한 기능: [새 값 계산](https://experienceleague.adobe.com/docs/experience-platform/data-prep/functions.html) 또는 [데이터 유형 변환](https://experienceleague.adobe.com/docs/experience-platform/data-prep/data-handling.html) xdm으로 이동하기 전에 데이터 레이어에서
* 활용 [매핑 UI](https://experienceleague.adobe.com/docs/experience-platform/datastreams/data-prep.html#create-mapping) 포인트 앤 클릭 UI를 사용하여 소스 데이터의 필드를 XDM에 매핑하려면

단점

* 데이터 레이어 변수를 클라이언트측 타사 픽셀에 대한 데이터 요소로 사용할 수 없지만 Adobe 태그에서 이벤트 전달에 사용할 수 있습니다
* Adobe Experience Platform의 태그 기능에 있는 스크래핑 기능을 사용할 수 없습니다.
* 태그와 데이터스트림 모두에서 데이터 레이어를 매핑할 경우 유지 관리 복잡성이 증가합니다

### 태그의 데이터 레이어 매핑

이 접근 방법에는 개별 데이터 계층 변수 또는 데이터 계층 개체를 태그의 데이터 요소와 최종적으로 XDM에 매핑하는 작업이 포함됩니다. 이는 태그 관리 시스템을 사용하여 를 구현하는 기존 접근 방식입니다.

장점

* XDM에 도달하기 전에 개별 변수를 제어하고 데이터를 변환할 수 있는 가장 유연한 접근 방법입니다
* Adobe 태그 트리거 및 스크래핑 기능을 사용하여 데이터를 XDM에 전달할 수 있음
* 클라이언트측 서드파티 픽셀에 데이터 요소 매핑 가능

단점

* 구현에 더 오래 걸릴 수 있음

>[!TIP]
>
> Google 데이터 레이어
> 
> 조직에서 이미 Google Analytics을 사용하고 있고 웹 사이트에 기존 Google dataLayer 개체가 있는 경우 다음을 사용할 수 있습니다. [Google 데이터 레이어 확장](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/google-data-layer/overview.html?lang=en) Adobe 태그에서 참조할 수 있습니다. 이렇게 하면 IT 팀에 지원을 요청하지 않고도 Adobe 기술을 보다 신속하게 배포할 수 있습니다. Google 데이터 레이어를 XDM에 매핑하면 위와 동일한 단계를 따릅니다.

>[!IMPORTANT]
>
>앞에서 설명한 바와 같이 이 자습서의 예제는 태그의 XDM에 매핑 접근 방식을 따릅니다.

## 데이터 요소를 만들어 데이터 레이어 캡처

XDM 개체를 만들기 전에 [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} 데이터 계층:

1. 다음으로 이동 **[!UICONTROL 데이터 요소]** 및 선택 **[!UICONTROL 데이터 요소 추가]** (또는 **[!UICONTROL 새 데이터 요소 만들기]** 태그 속성에 기존 데이터 요소가 없는 경우)

   ![데이터 요소 만들기](assets/data-element-create.jpg)

1. 데이터 요소에 이름을 지정합니다 `page.pageInfo.pageName`
1. 사용 **[!UICONTROL JavaScript 변수]** **[!UICONTROL 데이터 요소 유형]** luma의 데이터 레이어에 있는 값을 가리키려면 다음을 수행합니다. `digitalData.page.pageInfo.pageName`

1. 다음 확인란을 선택합니다. **[!UICONTROL 소문자 강제 적용 값]** 및 **[!UICONTROL 텍스트 정리]** 케이스를 표준화하고 외부 공백을 제거하려면

1. 나가기 `None` (으)로 **[!UICONTROL 저장 기간]** 이 값은 모든 페이지에서 다르므로 설정

1. 선택 **[!UICONTROL 저장]**

   ![페이지 이름 데이터 요소](assets/data-element-pageName.jpg)

동일한 단계를 수행하여 이러한 추가 데이터 요소를 만듭니다.

* **`page.pageInfo.server`**  매핑됨
  `digitalData.page.pageInfo.server`

* **`page.pageInfo.hierarchie1`**  매핑됨
  `digitalData.page.pageInfo.hierarchie1`

* **`user.profile.attributes.username`**  매핑됨
  `digitalData.user.0.profile.0.attributes.username`

* **`user.profile.attributes.loggedIn`** 매핑됨
  `digitalData.user.0.profile.0.attributes.loggedIn`

* **`product.productInfo.sku`** 매핑됨 `digitalData.product.0.productInfo.sku`
<!--digitalData.product.0.productInfo.sku
    ```javascript
    var cart = digitalData.product;
    var cartItem;
    cart.forEach(function(item){
    cartItem = item.productInfo.sku;
    });
    return cartItem;
    ```
    -->
* **`product.productInfo.title`** 매핑됨 `digitalData.product.0.productInfo.title`
* **`cart.orderId`** 매핑됨 `digitalData.cart.orderId`
<!--
    ```javascript
    var cart = digitalData.product;
    var cartItem;
    cart.forEach(function(item){
    cartItem = item.productInfo.title;
    });
    return cartItem;
    ```
    -->
* **`product.category`** 사용 **[!UICONTROL 사용자 지정 코드]** **[!UICONTROL 데이터 요소 유형]** 및 다음 사용자 지정 코드를 사용하여 최상위 카테고리에 대한 사이트 URL을 구문 분석할 수 있습니다.

  ```javascript
  var cat = location.pathname.split(/[/.]+/);
  if (cat[5] == 'products') {
     return (cat[6]);
  } else if (cat[5] != 'html') { 
     return (cat[5]);
  }
  ```

* **`cart.productInfo`** 다음 사용자 지정 코드 사용:

  ```javascript
  var cart = digitalData.cart.cartEntries; 
  var cartItem = [];
  cart.forEach(function(item, index, array){
  cartItem.push({
  "SKU": item.sku
  });
  });
  return cartItem; 
  ```

* **`cart.productInfo.purchase`** 다음 사용자 지정 코드 사용:

  ```javascript
  var cart = digitalData.cart.cartEntries; 
  var cartItem = [];
  cart.forEach(function(item, index, array){
  var qty = parseInt(item.qty);
  var price = parseInt(item.price);
  cartItem.push({
  "SKU": item.sku,
  "quantity": qty,
  "priceTotal": price
  });
  });
  return cartItem; 
  ```



>[!CAUTION]
>
>다음 [!UICONTROL JavaScript 변수] 데이터 요소 유형은 배열 참조를 대괄호 대신 점으로 처리하므로 사용자 이름 데이터 요소를 로 참조합니다. `digitalData.user[0].profile[0].attributes.username` **작동하지 않음**.

## 변수 데이터 요소 만들기

데이터 요소를 만든 후 다음을 사용하여 XDM에 매핑합니다. **[!UICONTROL 변수]** xdm 개체에 사용되는 스키마를 정의하는 데이터 요소입니다. 이 개체는 다음 작업 중에 만든 XDM 스키마를 준수해야 합니다. [스키마 구성](configure-schemas.md) 레슨.

변수 데이터 요소를 만들려면 다음 작업을 수행하십시오.

1. 선택 **[!UICONTROL 데이터 요소 추가]**
1. 데이터 요소에 이름 지정 `xdm.variable.content`. 태그 속성을 더 잘 구성하려면 XDM과 관련된 데이터 요소를 &quot;xdm&quot; 접두사로 사용하는 것이 좋습니다
1. 다음 항목 선택 **[!UICONTROL Adobe Experience Platform 웹 SDK]** (으)로 **[!UICONTROL 확장]**
1. 다음 항목 선택 **[!UICONTROL 변수]** (으)로 **[!UICONTROL 데이터 요소 유형]**
1. 적절한 Experience Platform 선택 **[!UICONTROL 샌드박스]**
1. 적절한 항목 선택 **[!UICONTROL 스키마]**, 이 경우 `Luma Web Event Data`
1. 선택 **[!UICONTROL 저장]**

   ![변수 데이터 요소](assets/analytics-tags-data-element-xdm-variable.png)


이러한 단계를 마치면 다음 데이터 요소를 만들어야 합니다.

| 코어 확장 데이터 요소 | Platform Web SDK 데이터 요소 |
-----------------------------|-------------------------------
| `cart.orderId` | `xdm.variable.content` |
| `cart.productInfo` | |
| `cart.productInfo.purchase` | |
| `page.pageInfo.hierarchie1` | |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `product.productInfo.sku` | |
| `product.productInfo.title` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |

>[!TIP]
>
>향후 [태그 규칙 만들기](create-tag-rule.md) 단원, 당신은 어떻게 **[!UICONTROL 변수]** 데이터 요소를 사용하여 태그에 여러 규칙을 스택할 수 있습니다. **[!UICONTROL 변수 작업 유형 업데이트]**. 그런 다음 별도의 메서드를 사용하여 XDM 개체를 Adobe Experience Platform Edge Network로 독립적으로 보낼 수 있습니다 **[!UICONTROL 이벤트 전송 작업 유형]**.

이러한 데이터 요소가 준비되면 태그 규칙을 사용하여 Platform Edge Network에 데이터를 전송할 수 있습니다. 하지만 먼저 웹 SDK를 사용하여 ID를 수집하는 방법에 대해 알아봅니다.

[다음: ](create-identities.md)

>[!NOTE]
>
>Adobe Experience Platform Web SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나, 일반적인 피드백을 공유하거나, 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오. [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
