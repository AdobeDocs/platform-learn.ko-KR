---
title: 매개 변수 보내기 - 모바일 앱의 Adobe Target 구현을 Adobe Journey Optimizer - Decisioning 확장 프로그램으로 마이그레이션합니다.
description: Experience Platform Web SDK을 사용하여 mbox, 프로필 및 엔티티 매개 변수를 Adobe Target에 보내는 방법을 알아봅니다.
exl-id: 927d83f9-c019-4a6b-abef-21054ce0991b
source-git-commit: e0359d1bade01f79d0f7aff6a6e69f3e4d0c3b62
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 1%

---

# Decisioning 확장을 사용하여 Target에 매개 변수 보내기

앱 아키텍처, 비즈니스 요구 사항 및 사용된 기능으로 인해 Target 구현은 모바일 애플리케이션에 따라 다릅니다. 대부분의 Target 구현에는 컨텍스트 정보, 대상 및 콘텐츠 권장 사항에 대한 다양한 매개 변수 전달이 포함됩니다.

Target 확장을 사용하면 `TargetParameters` 함수를 사용하여 모든 Target 매개 변수가 전달되었습니다.

Decisioning 확장 기능:

* 여러 Adobe 애플리케이션용 매개 변수를 XDM 개체에 전달할 수 있습니다
* Target에만 사용할 매개 변수는 `data.__adobe.target` 개체에 전달할 수 있습니다.


>[!IMPORTANT]
>
> Decisioning 확장을 사용하면 요청에서 전송된 매개 변수가 요청의 모든 범위에 적용됩니다. 서로 다른 범위에 대해 서로 다른 매개 변수를 설정해야 하는 경우 추가 요청을 수행해야 합니다.

## 사용자 지정 매개 변수

사용자 지정 mbox 매개 변수는 데이터를 Target에 전달하는 가장 기본적인 방법이며 `xdm` 또는 `data.__adobe.target` 개체로 전달할 수 있습니다.

## 프로필 매개 변수

프로필 매개 변수는 사용자의 Target 프로필에 장기간 데이터를 저장하므로 `data.__adobe.target` 개체에 전달해야 합니다.

## 엔티티 매개 변수

[엔터티 매개 변수](https://experienceleague.adobe.com/ko/docs/target/using/recommendations/entities/entity-attributes)은(는) Target 권장 사항에 대한 동작 데이터 및 보조 카탈로그 정보를 전달하는 데 사용됩니다. 프로필 매개 변수와 유사한 대부분의 엔터티 매개 변수는 `data.__adobe.target` 개체 아래에 전달되어야 합니다. 유일한 예외는 `xdm.productListItems` 배열입니다. 그러면 첫 번째 `SKU` 값이 `entity.id`(으)로 사용됩니다.

적절한 데이터 캡처를 위해서는 특정 항목의 엔터티 매개 변수 앞에 `entity.`이(가) 있어야 합니다. 권장 사항 알고리즘에 대해 예약된 `cartIds` 및 `excludedIds` 매개 변수는 접두사가 없어야 하며 각 값은 쉼표로 구분된 엔티티 ID 목록을 포함해야 합니다.

## 구매 매개 변수

구매 매개 변수는 성공적인 주문 후에 주문 확인 페이지에서 전달되며 Target 전환 및 최적화 목표에 사용됩니다. Decisioning 확장을 사용하는 Platform Mobile SDK 구현에서는 이러한 매개 변수와 가 `commerce` 필드 그룹의 일부로 전달된 XDM 데이터에서 자동으로 매핑됩니다.

`commerce` 필드 그룹에 `purchases.value`이(가) `1`(으)로 설정되어 있으면 구매 정보가 Target에 전달됩니다. 주문 ID와 주문 합계는 `order` 개체에서 자동으로 매핑됩니다. `productListItems` 배열이 있으면 `SKU` 값이 `productPurchasedId`에 사용됩니다.

`xdm` 개체에서 `commerce` 필드를 전달하지 않는 경우 `data.__adobe.target.orderId`, `data.__adobe.target.orderTotal` 및 `data.__adobe.target.productPurchasedId` 필드를 사용하여 주문 세부 정보를 target에 전달할 수 있습니다.

## 고객 ID (mbox3rdPartyId)

Target을 사용하면 단일 고객 ID를 사용하여 장치 및 시스템 간에 프로필을 동기화할 수 있습니다. 이 고객 ID는 XDM 개체의 `identityMap` 필드에 전달되고 데이터 스트림의 Target 타사 ID 필드에 매핑되어야 합니다.

## 테이블

| at.js 매개 변수 예 | Platform Web SDK 옵션 | 참고 |
| --- | --- | --- |
| `at_property` | N/A | 속성 토큰이 [데이터스트림](https://experienceleague.adobe.com/ko/docs/experience-platform/datastreams/configure#target)에 구성되어 `sendEvent` 호출에서 설정할 수 없습니다. |
| `pageName` | `xdm.web.webPageDetails.name` 또는 <br> `data.__adobe.target.pageName` | Target mbox 매개 변수는 `xdm` 개체의 일부 또는 `data.__adobe.target` 개체의 일부로 전달할 수 있습니다. |
| `profile.gender` | `data.__adobe.target.profile.gender` | 모든 Target 프로필 매개 변수를 `data` 개체의 일부로 전달하고 `profile.` 접두사가 추가되어 적절하게 매핑해야 합니다. |
| `user.categoryId` | `data.__adobe.target.user.categoryId` | `data` 개체의 일부로 전달해야 하는 Target의 카테고리 선호도 기능에 사용되는 예약된 매개 변수입니다. |
| `entity.id` | `data.__adobe.target.entity.id` <br>또는<br> `xdm.productListItems[0].SKU` | 엔티티 ID는 Target Recommendations 동작 카운터에 사용됩니다. 구현이 해당 필드 그룹을 사용하는 경우 이러한 엔터티 ID는 `data` 개체의 일부로 전달되거나 `xdm.productListItems` 배열의 첫 번째 항목에서 자동으로 매핑될 수 있습니다. |
| `entity.categoryId` | `data.__adobe.target.entity.categoryId` | 엔터티 범주 ID는 `data` 개체의 일부로 전달될 수 있습니다. |
| `entity.customEntity` | `data.__adobe.target.entity.customEntity` | 사용자 지정 엔티티 매개 변수는 권장 사항 제품 카탈로그를 업데이트하는 데 사용됩니다. 이러한 사용자 지정 매개 변수는 `data` 개체의 일부로 전달해야 합니다. |
| `cartIds` | `data.__adobe.target.cartIds` | Target의 장바구니 기반 권장 사항 알고리즘에 사용됩니다. |
| `excludedIds` | `data.__adobe.target.excludedIds` | 권장 사항 디자인에서 특정 엔티티 ID가 반환되지 않도록 하는 데 사용됩니다. |
| `mbox3rdPartyId` | `xdm.identityMap` 개체에 설정 | 여러 장치 및 고객 속성에서 Target 프로필을 동기화하는 데 사용됩니다. 고객 ID에 사용할 네임스페이스는 데이터 스트림의 [Target 구성](https://experienceleague.adobe.com/ko/docs/experience-platform/edge/personalization/adobe-target/using-mbox-3rdpartyid)에서 지정해야 합니다. |
| `orderId` | `xdm.commerce.order.purchaseID`<br>(`commerce.purchases.value`이(가) `1`(으)로 설정된 경우)<br> 또는<br> `data.__adobe.target.orderId` | 타겟 전환 추적을 위한 고유한 주문을 식별하는 데 사용됩니다. |
| `orderTotal` | `xdm.commerce.order.priceTotal`<br>(`commerce.purchases.value`이(가) `1`(으)로 설정된 경우)<br> 또는<br> `data.__adobe.target.orderTotal` | Target 전환 및 최적화 목표를 위한 주문 합계를 추적하는 데 사용됩니다. |
| `productPurchasedId` | `xdm.productListItems[0-n].SKU`<br>(`commerce.purchases.value`이(가) `1`(으)로 설정된 경우) <br>OR<br> `data.__adobe.target.productPurchasedId` | Target 전환 추적 및 권장 사항 알고리즘에 사용됩니다. |
| `mboxPageValue` | `data.__adobe.target.mboxPageValue` | [사용자 지정 점수](https://experienceleague.adobe.com/ko/docs/target/using/activities/success-metrics/capture-score) 활동 목표에 사용됩니다. |

{style="table-layout:auto"}


## 매개 변수 전달의 예

간단한 예를 사용하여 매개 변수를 Target에 전달할 때 확장 간의 차이점을 보여 주겠습니다.

### Android

>[!BEGINTABS]

>[!TAB SDK 최적화]

```Java
final Map<String, Object> data = new HashMap<>();
final Map<String, String> targetParameters = new HashMap<>();
 
// Mbox parameters
targetParameters.put("status", "platinum");
 
// Profile parameters - prefix with profile.
targetParameters.put("profile.gender", "male");
 
// Product parameters
targetParameters.put("productId", "pId1");
targetParameters.put("categoryId", "cId1");
 
// Order parameters
targetParameters.put("orderId", "id1");
targetParameters.put("orderTotal", "1.0");
targetParameters.put("purchasedProductIds", "ppId1");
 
data.put("__adobe", new HashMap<String, Object>() {
  {
    put("target", targetParameters);
  }
});
 
// Target location (or mbox)
final DecisionScope decisionScope = DecisionScope("myTargetLocation")
 
final List<DecisionScope> decisionScopes = new ArrayList<>();
decisionScopes.add(decisionScope);
 
Optimize.updatePropositions(decisionScopes, null, data);
```

>[!TAB SDK 타깃팅]

```Java
Map<String, String> mboxParameters = new HashMap<String, String>();
mboxParameters1.put("status", "platinum");
 
Map<String, String> profileParameters = new HashMap<String, String>();
profileParameters1.put("gender", "male");
 
List<String> purchasedProductIds = new ArrayList<String>();
purchasedProductIds.add("ppId1");
TargetOrder targetOrder = new TargetOrder("id1", 1.0, purchasedProductIds);
 
TargetProduct targetProduct = new TargetProduct("pId1", "cId1");
 
TargetParameters targetParameters = new TargetParameters.Builder()
                                    .parameters(mboxParameters)
                                    .profileParameters(profileParameters)
                                    .product(targetProduct)
                                    .order(targetOrder)
                                    .build();
```

>[!ENDTABS]

### iOS

>[!BEGINTABS]

>[!TAB SDK 최적화]

```Swift
var data: [String: Any] = [:]
var targetParameters: [String: String] = [:]
 
// Mbox parameters
targetParameters["status"] = "platinum"
 
// Profile parameters - prefix with profile.
targetParameters["profile.gender"] = "make"
 
// Product parameters
targetParameters["productId"] = "pId1"
targetParameters["categoryId"] = "cId1"
 
// Add order parameters
targetParameters["orderId"] = "id1"
targetParameters["orderTotal"] = "1.0"
targetParameters["purchasedProductIds"] = "ppId1"
 
data["__adobe"] = [
  "target": targetParameters
]
 
// Target location (or mbox)
let decisionScope = DecisionScope(name: "myTargetLocation")
Optimize.updatePropositions(for: [decisionScope] withXdm: nil andData: data)
```

>[!TAB SDK 타깃팅]

```Swift
let mboxParameters = [
                        "status": "platinum"
                     ]
 
let profileParameters = [
                            "gender": "male"
                        ]
 
let order = TargetOrder(id: "id1", total: 1.0, purchasedProductIds: ["ppId1"])
 
let product = TargetProduct(productId: "pId1", categoryId: "cId1")
 
let targetParameters = TargetParameters(parameters: mboxParameters, profileParameters: profileParameters, order: order, product: product))
```


>[!ENDTABS]






다음으로 Platform Web SDK을 사용하여 [Target 전환 이벤트를 추적](track-events.md)하는 방법에 대해 알아봅니다.

>[!NOTE]
>
>Target 확장에서 Decisioning 확장으로 모바일 Target을 성공적으로 마이그레이션할 수 있도록 지원하기 위해 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484?profile.language=ko#M625)에 게시하여 알려 주십시오.
