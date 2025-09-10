---
title: Platform Mobile SDK으로 수집된 데이터를 Adobe Analytics에 매핑
description: 모바일 앱에서 Adobe Analytics에 대한 데이터를 수집하고 매핑하는 방법을 알아봅니다.
solution: Data Collection,Experience Platform,Analytics
jira: KT-14636
exl-id: 406dc687-643f-4f7b-a8e7-9aad1d0d481d
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 0%

---

# Analytics 데이터 수집 및 매핑

모바일 데이터를 Adobe Analytics에 매핑하는 방법을 알아봅니다.

이전 단원에서 수집하여 Platform Edge Network으로 전송한 [event](events.md) 데이터는 Adobe Analytics을 포함하여 데이터스트림에 구성된 서비스로 전달됩니다. 데이터를 보고서 세트의 올바른 변수에 매핑합니다.

![아키텍쳐](assets/architecture-aa.png){zoomable="yes"}

## 전제 조건

* ExperienceEvent 추적에 대한 이해.
* 샘플 앱에서 XDM 데이터를 성공적으로 보냈습니다.
* 이 단원에 사용할 수 있는 Adobe Analytics 보고서 세트입니다.

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* Adobe Analytics 서비스로 데이터 스트림을 구성합니다.
* Analytics 변수의 자동 매핑을 이해합니다.
* XDM 데이터를 Analytics 변수에 매핑하는 처리 규칙을 설정합니다.

## Adobe Analytics 데이터스트림 서비스 추가

Edge Network에서 Adobe Analytics으로 XDM 데이터를 전송하려면 [데이터 스트림 만들기](create-datastream.md)의 일부로 설정한 데이터 스트림으로 Adobe Analytics 서비스를 구성합니다.

1. 데이터 수집 UI에서 **[!UICONTROL 데이터스트림]** 및 데이터스트림을 선택합니다.

1. ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 서비스 추가]**&#x200B;를 선택합니다.

1. **[!UICONTROL 서비스]** 목록에서 [!UICONTROL Adobe Analytics] 추가,

1. **[!UICONTROL 보고서 세트 ID]**&#x200B;에서 사용할 Adobe Analytics의 보고서 세트 이름을 입력하십시오.

1. **[!UICONTROL 사용]**&#x200B;을(를) 전환하여 서비스를 사용하도록 설정하십시오.

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

   ![데이터 스트림 서비스로 Adobe Analytics 추가](assets/datastream-service-aa.png){zoomable="yes"}


## 자동 매핑

대부분의 표준 XDM 필드는 Analytics 변수에 자동으로 매핑됩니다. [전체 목록](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/xdm-var-mapping)을 참조하세요.

### 예 #1 - s.products

처리 규칙을 사용하여 채울 수 없는 [products 변수](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/products)이(가) 좋은 예입니다. XDM 구현을 사용하면 `productListItems`에 필요한 모든 데이터를 전달하고 `s.products`은(는) Analytics 매핑을 통해 자동으로 채워집니다.

이 개체:

```swift
"productListItems": [
    [
      "name":  "Yoga Mat",
      "SKU": "5829",
      "priceTotal": "49.99",
      "quantity": 1
    ],
    [
      "name":  "Water Bottle",
      "SKU": "9841",
      "priceTotal": "30.00",
      "quantity": 3
    ]
]
```

결과 위치:

```
s.products = ";5829;1;49.99,9841;3;30.00"
```

>[!NOTE]
>
>`productListItems[].SKU`과(와) `productListItems[].name`이(가) 모두 데이터를 포함하는 경우 `productListItems[].SKU`의 값이 사용됩니다. 자세한 내용은 [Adobe Experience Edge의 Analytics 변수 매핑](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/xdm-var-mapping)을 참조하십시오.


### 예 #2 - scAdd

자세히 살펴보면 모든 이벤트에는 `value`(필수) 및 `id`(선택 사항)의 두 필드가 있습니다. `value` 필드는 이벤트 수를 늘리는 데 사용됩니다. `id` 필드는 serialization에 사용됩니다.

이 개체:

```swift
"commerce" : {
  "productListAdds" : {
    "value" : 1
  }
}
```

결과 위치:

```
s.events = "scAdd"
```

이 개체:

```swift
"commerce" : {
  "productListAdds" : {
    "value" : 1,
    "id": "321435"
  }
}
```

결과 위치:

```
s.events = "scAdd:321435"
```

## Assurance를 사용한 유효성 검사

[Assurance](assurance.md)을(를) 사용하여 경험 이벤트를 보내고 있으며 XDM 데이터가 올바르고 Analytics 매핑이 예상대로 발생하고 있는지 확인할 수 있습니다.

1. [설치 지침](assurance.md#connecting-to-a-session) 섹션을 검토하여 시뮬레이터 또는 장치를 Assurance에 연결하십시오.

1. **[!UICONTROL productListAdds]** 이벤트를 보냅니다(장바구니에 제품 추가).

1. ExperienceEvent 히트를 봅니다.

   ![analytics xdm 히트](assets/analytics-assurance-experiencevent.png){zoomable="yes"}

1. JSON의 XDM 부분을 검토합니다.

   ```json
   "xdm" : {
     "productListItems" : [ {
       "SKU" : "LLWS05.1-XS",
       "name" : "Desiree Fitness Tee",
       "priceTotal" : 24
     } ],
   "timestamp" : "2023-08-04T12:53:37.662Z",
   "eventType" : "commerce.productListAdds",
   "commerce" : {
     "productListAdds" : {
       "value" : 1
     }
   }
   // ...
   ```

1. **[!UICONTROL analytics.mapping]** 이벤트를 검토하십시오.

   ![analytics xdm 히트](assets/analytics-assurance-mapping.png){zoomable="yes"}

Analytics 매핑에서 다음을 참고하십시오.

* **[!UICONTROL 이벤트]**&#x200B;은(는) `scAdd`을(를) 기준으로 `commerce.productListAdds`(으)로 채워집니다.
* **[!UICONTROL pl]**(products 변수)은 `productListItems`을(를) 기반으로 연결된 값으로 채워집니다.
* 모든 컨텍스트 데이터를 포함하여 이 이벤트에는 다른 흥미로운 정보가 있습니다.


## 컨텍스트 데이터로 매핑

Analytics로 전달된 XDM 데이터는 표준 및 사용자 지정 필드를 모두 포함하는 [컨텍스트 데이터](https://github.com/Adobe-Marketing-Cloud/mobile-services/blob/master/docs/ios/getting-started/proc-rules.md?lang=en)&#x200B;(으)로 변환됩니다.

컨텍스트 데이터 키는 다음 구문에 따라 구성됩니다.

```
a.x.[xdm path]
```

예:

```
// Standard Field
a.x.commerce.saveforlaters.value

// Custom Field
a.x._techmarketingdemos.appinformation.appstatedetails.screenname
```

>[!NOTE]
>
>사용자 지정 필드는 Experience Cloud 조직 식별자 아래에 위치합니다.
>
>테넌트 이름 `_techmarketingdemos`이(가) 조직의 고유 값으로 대체되었습니다.



이 XDM 컨텍스트 데이터를 보고서 세트의 Analytics 데이터에 매핑하려면 다음을 수행할 수 있습니다.

### 필드 그룹 사용

* **[!UICONTROL Adobe Analytics ExperienceEvent 전체 확장]** 필드 그룹을 스키마에 추가합니다.

  ![Analytics ExperienceEvent FullExtension 필드 그룹](assets/schema-analytics-extension.png){zoomable="yes"}

* [이벤트 데이터 추적](events.md) 단원에서 수행한 작업과 유사한 Adobe Analytics ExperienceEvent 전체 확장 필드 그룹에 따라 앱에서 XDM 페이로드를 빌드하거나
* 규칙 작업을 사용하여 Adobe Analytics ExperienceEvent 전체 확장 필드 그룹에 데이터를 첨부하거나 수정하는 규칙을 Tags 속성에 작성합니다. 자세한 내용은 [SDK 이벤트에 데이터 첨부](https://developer.adobe.com/client-sdks/documentation/user-guides/attach-data/) 또는 [SDK 이벤트에서 데이터 수정](https://developer.adobe.com/client-sdks/documentation/user-guides/attach-data/)을 참조하십시오.


### 머천다이징 eVar

Analytics 설정에서 [머천다이징 eVar](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/conversion-variables/merchandising-evars)을(를) 사용하는 경우 [이벤트 데이터 추적](events.md)에서 정의한 XDM 페이로드를 확장하여 해당 머천다이징 정보를 캡처해야 합니다. 머천다이징 변수의 예는 `evar1`과(와) 같이 제품 색상을 캡처하려는 경우 `&&products = ...;evar1=red;event10=50,...;evar1=blue;event10=60`입니다.

* JSON에서:

  ```json
  {
    "productListItems": [
        {
            "SKU": "LLWS05.1-XS",
            "name": "Desiree Fitness Tee",
            "priceTotal": 24,
            "_experience": {
                "analytics": {
                    "events1to100": {
                        "event10": {
                            "value": 50
                        }
                    },
                    "customDimensions": {
                        "eVars": {
                            "eVar1": "red",
                        }
                    }
                }
            }
        }
    ],
    "eventType": "commerce.productListAdds",
    "commerce": {
        "productListAdds": {
            "value": 1
        }
    }
  }
  ```

* 코드에서:

  ```swift
  var xdmData: [String: Any] = [
    "productListItems": [
      [
        "name":  productName,
        "SKU": sku,
        "priceTotal": priceString,
        "_experience" : [
          "analytics": [
            "events1to100": [
              "event10": [
                "value:": value
              ]
            ],
            "customDimensions": [
              "eVars": [
                "eVar1": color
              ]
            ]
          ]
        ]
      ]
    ],
    "eventType": "commerce.productViews",
    "commerce": [
      "productViews": [
        "value": 1
      ]
    ]
  ]
  ```


### 처리 규칙 사용

다음은 이 데이터를 사용하는 처리 규칙의 모습입니다.

* **[!UICONTROL 값]**(1) **[!UICONTROL 앱 화면 이름(eVar2)]**(2)을 값 **[!UICONTROL a.x._techmarketingdemo.appstatedetails.screenname]**(3)으로 덮어씁니다(**[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]**(4) **[!UICONTROL 이(가) 설정된 경우]**(5)).

* **[!UICONTROL 이벤트를 설정]** (6) **[!UICONTROL 위시리스트에 추가(이벤트 3)]** (7)을(를) **[!UICONTROL a.x.commerce.saveForLaters.value(컨텍스트)]** (8) **[!UICONTROL a.x.commerce.saveForLaters.value(컨텍스트)]** (9) **[!UICONTROL 이(가) 설정된 경우]** (10).

![분석 처리 규칙](assets/analytics-processing-rules.png){zoomable="yes"}

>[!IMPORTANT]
>
>
>자동으로 매핑된 변수 중 일부는 처리 규칙에서 사용하지 못할 수 있습니다.
>
>
>처리 규칙에 처음 매핑하면 XDM 객체의 컨텍스트 데이터 변수가 인터페이스에 표시되지 않습니다. 이 문제를 해결하려면 를 저장하고 다시 편집하십시오. 이제 모든 XDM 변수가 표시됩니다.


[처리 규칙을 사용하여 contextData 변수를 prop 및 eVar에 매핑](https://experienceleague.adobe.com/en/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules)을 참조하십시오.

>[!TIP]
>
>이전 모바일 앱 구현과 달리 페이지/화면 보기와 다른 이벤트 사이에는 차이가 없습니다. 대신 처리 규칙에서 **[!UICONTROL 페이지 이름]** 차원을 설정하여 **[!UICONTROL 페이지 보기]** 지표를 증가시킬 수 있습니다. 자습서에서 사용자 지정 `screenName` 필드를 수집하므로 처리 규칙에서 화면 이름을 **[!UICONTROL 페이지 이름]**&#x200B;에 매핑하는 것이 좋습니다.

## Analytics 모바일 확장에서 마이그레이션

[Adobe Analytics 모바일 확장](https://developer.adobe.com/client-sdks/solution/adobe-analytics/#add-analytics-to-your-application)을 사용하여 모바일 애플리케이션을 개발한 경우 [`MobileCore.trackAction`](https://developer.adobe.com/client-sdks/home/base/mobile-core/api-reference/#trackaction) 및 [`MobileCore.trackState`](https://developer.adobe.com/client-sdks/home/base/mobile-core/api-reference/#trackstate) API 호출을 사용했을 수 있습니다.

권장되는 Edge Network을 사용하도록 마이그레이션하고자 하는 경우 다음과 같은 옵션이 있습니다.

* [이벤트 데이터 추적](configure-tags.md#extension-configuration) 방법에 대한 단원에서 설명한 대로 [`Edge.sendEvent`Edge Network 확장](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#sendevent)을 구현하고 [&#128279;](events.md) API를 사용합니다. 이 자습서에서는 이 구현에 중점을 둡니다.
* [Edge Bridge 확장](https://developer.adobe.com/client-sdks/solution/adobe-analytics/migrate-to-edge-network/#implement-the-edge-bridge-extension)을 구현하고 [`MobileCore.trackAction`](https://developer.adobe.com/client-sdks/home/base/mobile-core/api-reference/#trackaction) 및 [`MobileCore.trackState`](https://developer.adobe.com/client-sdks/home/base/mobile-core/api-reference/#trackstate) API 호출을 계속 사용합니다. 자세한 내용 및 별도의 자습서는 [Edge Bridge 확장 구현](https://developer.adobe.com/client-sdks/solution/adobe-analytics/migrate-to-edge-network/#implement-the-edge-bridge-extension)을 참조하십시오.




>[!SUCCESS]
>
>데이터스트림에서 Adobe Analytics 서비스를 활성화하여 Experience Edge XDM 개체를 Adobe Analytics 변수에 매핑하도록 앱을 설정했습니다. 해당되는 경우 처리 규칙 사용.<br/> Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하고 싶거나 향후 콘텐츠에 대한 제안이 있는 경우 이 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com:443/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)에서 공유하십시오.

다음: **[Experience Platform에 데이터 보내기](platform.md)**
