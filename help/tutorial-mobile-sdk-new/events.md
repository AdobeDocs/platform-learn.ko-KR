---
title: 이벤트 데이터 추적
description: 모바일 앱에서 이벤트 데이터를 추적하는 방법에 대해 알아봅니다.
hide: true
exl-id: b926480b-b431-4db8-835c-fa1db6436a93
source-git-commit: f592fc61ad28d04eba3c1c21a0a66bda6e816a5b
workflow-type: tm+mt
source-wordcount: '1390'
ht-degree: 0%

---

# 이벤트 데이터 추적

모바일 앱에서 이벤트를 추적하는 방법에 대해 알아봅니다.

Edge Network 확장은 Platform Edge Network에 경험 이벤트를 전송하기 위한 API를 제공합니다. 경험 이벤트 는 XDM ExperienceEvent 스키마 정의를 따르는 데이터가 포함된 개체입니다. 보다 간단하게, 모바일 앱에서 사람들이 하는 작업을 캡처합니다. Platform Edge Network에서 데이터를 수신하면 Adobe Analytics 및 Experience Platform과 같이 데이터 스트림에 구성된 애플리케이션 및 서비스로 전달할 수 있습니다. 에 대해 자세히 알아보기 [경험 이벤트](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) 를 참조하십시오.

## 전제 조건

* 모든 패키지 종속성은 Xcode 프로젝트에 있습니다.
* 에 등록된 확장 **[!UICONTROL AppDelegate]**.
* 개발을 사용하도록 MobileCore 확장을 구성했습니다. `appId`.
* 가져온 SDK.
* 위의 변경 사항으로 앱을 빌드하고 실행했습니다.

## 학습 목표

이 단원에서는 다음과 같은 작업을 수행합니다

* 스키마를 기반으로 XDM 데이터를 구성하는 방법을 이해합니다.
* 표준 필드 그룹을 기반으로 XDM 이벤트를 전송합니다.
* 사용자 지정 필드 그룹을 기반으로 XDM 이벤트를 보냅니다.
* XDM 구매 이벤트를 보냅니다.
* Assurance를 사용하여 확인합니다.

## 경험 이벤트 구성

Adobe Experience Platform Edge 확장은 이전에 정의한 XDM 스키마 다음에 오는 이벤트를 Adobe Experience Platform Edge Network로 전송할 수 있습니다.

프로세스는 다음과 같습니다.

1. 추적하려는 모바일 앱 상호 작용을 식별합니다.

1. 스키마를 검토하고 적절한 이벤트를 식별합니다.

1. 스키마를 검토하고 이벤트를 설명하는 데 사용해야 하는 추가 필드를 식별합니다.

1. 데이터 개체를 구성하고 채웁니다.

1. 이벤트를 만들고 전송합니다.

1. 유효성 검사.


### 표준 필드 그룹

표준 필드 그룹의 경우 프로세스는 다음과 같습니다.

* 스키마에서 수집하려는 이벤트를 식별합니다. 이 예제에서는 상거래 경험 이벤트(예: 제품 보기 )를 추적합니다.**[!UICONTROL 제품 보기]**) 이벤트.

  ![제품 보기 스키마](assets/datacollection-prodView-schema.png)

* 앱에서 경험 이벤트 데이터를 포함하는 개체를 만들려면 다음과 같은 코드를 사용합니다.

  ```swift
  var xdmData: [String: Any] = [
      "eventType": "commerce.productViews",
      "commerce": [
          "productViews": [
            "value": 1
          ]
      ]
  ]
  ```

   * `eventType`: 발생한 이벤트를 설명합니다. [알려진 값](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) 가능한 경우
   * `commerce.productViews.value`: 이벤트의 숫자 또는 부울 값. 부울(또는 Adobe Analytics의 &quot;카운터&quot;)인 경우 값은 항상 1로 설정됩니다. 숫자 또는 통화 이벤트인 경우 값은 1보다 클 수 있습니다.

* 스키마에서 상거래 제품 보기 이벤트와 관련된 추가 데이터를 식별합니다. 이 예에서는 다음을 포함합니다 **[!UICONTROL productListItem]** 상거래 관련 이벤트에 사용되는 표준 필드 세트입니다.

  ![제품 목록 항목 스키마](assets/datacollection-prodListItems-schema.png)
   * 주의: **[!UICONTROL productListItem]** 는 여러 제품을 제공할 수 있는 배열입니다.

* 이 데이터를 추가하려면 `xdmData` 추가 데이터를 포함할 대상:

  ```swift
  var xdmData: [String: Any] = [
      "eventType": "commerce.productViews",
          "commerce": [
          "productViews": [
              "value": 1
          ]
      ],
      "productListItems": [
          [
              "name":  productName,
              "SKU": sku,
              "priceTotal": priceString,
              "quantity": 1
          ]
      ]
  ]
  ```

* 이제 이 데이터 구조를 사용하여 `ExperienceEvent`:

  ```swift
  let productViewEvent = ExperienceEvent(xdm: xdmData)
  ```

* 및 를 사용하여 Platform Edge Network에 이벤트 및 데이터 보내기 `sendEvent` API:

  ```swift
  Edge.sendEvent(experienceEvent: productViewEvent)
  ```

다음 [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API는 AEP Mobile SDK로서 [`MobileCore.trackAction`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction) 및 [`MobileCore.trackState`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackstate) API 호출. 다음을 참조하십시오 [Analytics 모바일 확장에서 Adobe Experience Platform Edge Network로 마이그레이션](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/migrate-to-edge-network/) 추가 정보.

이제 Xcode 프로젝트에서 이 코드를 실제로 구현합니다.
앱에 서로 다른 상거래 제품 관련 작업이 있으며 사용자가 수행한 다음 작업에 따라 이벤트를 전송하려고 합니다.

* 보기: 사용자가 특정 제품을 볼 때 발생합니다.
* 장바구니에 추가: 사용자가 탭할 때 <img src="assets/addtocart.png" width="20" /> 제품 세부 사항 화면에서
* 나중에 저장: 사용자가 탭할 때 <img src="assets/saveforlater.png" width="15" /> 제품 세부 사항 화면에서
* 구매: 사용자가 탭할 때 <img src="assets/purchase.png" width="20" /> 제품 세부 사항 화면에서 다음을 수행합니다.

재사용 가능한 방식으로 상거래 관련 경험 이벤트 전송을 구현하려면 전용 함수를 사용합니다.

1. 다음으로 이동 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** xcode 프로젝트 탐색기에서 다음을 `func sendCommerceExperienceEvent(commerceEventType: String, product: Product)` 함수.

   ```swift
   // Set up a data dictionary, create an experience event and send the event.
   let xdmData: [String: Any] = [
       "eventType": "commerce." + commerceEventType,
       "commerce": [
           commerceEventType: [
               "value": 1
           ]
       ],
       "productListItems": [
           [
               "name": product.name,
               "priceTotal": product.price,
               "SKU": product.sku
           ]
       ]
   ]
   
   let commerceExperienceEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: commerceExperienceEvent)
   ```

   이 함수는 상거래 경험 이벤트 유형 및 제품을 매개 변수로 사용합니다.

   * 함수의 매개 변수를 사용하여 XDM 페이로드를 사전으로 설정합니다.
   * 사전을 사용하여 경험 이벤트를 설정합니다.
   * 을(를) 사용하여 경험 이벤트를 전송합니다. [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API.

1. 다음으로 이동 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!UICONTROL 제품 보기]** xcode 프로젝트 탐색기에서 `sendCommerceExperienceEvent` 함수:

   1. 위치: `.task` 수정자, 다음 범위 내 `ATTrackingManager.trackingAuthorizationStatus` 종료. 이 `.task` 수정자는 제품 보기가 초기화되어 표시될 때 호출되므로 특정 시점에 제품 보기 이벤트를 보내려고 합니다.

      ```swift
      // Send productViews commerce experience event
      MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productViews", product: product)
      ```

   1. 각 버튼에 대해(<img src="assets/saveforlater.png" width="15" />, <img src="assets/addtocart.png" width="20" /> 및 <img src="assets/purchase.png" width="20" />) 도구 모음에서 관련 호출을 도구 모음에 추가합니다 `ATTrackingManager.trackingAuthorizationStatus == .authorized` 종료:

      1. 대상 <img src="assets/saveforlater.png" width="15" />:

         ```swift
         // Send saveForLaters commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "saveForLaters", product: product)
         ```

      1. 대상 <img src="assets/addtocart.png" width="20" />:

         ```swift
         // Send productListAdds commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productListAdds", product: product)
         ```

      1. 대상 <img src="assets/purchase.png" width="20" />:

         ```swift
         // Send purchases commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
         ```

>[!TIP]
>
>Android용으로 개발하는 경우 맵(`java.util.Map`)를 XDM 페이로드를 구성하는 기본 인터페이스입니다.


### 사용자 정의 필드 그룹

앱 자체에서 화면 보기 및 상호 작용을 추적한다고 상상해 보십시오. 이 유형의 이벤트에 대해 사용자 정의 필드 그룹을 정의했음을 기억하십시오.

* 스키마에서 수집하려는 이벤트를 식별합니다.
  ![앱 상호 작용 스키마](assets/datacollection-appInteraction-schema.png)

* 객체 구성을 시작합니다.

  >[!NOTE]
  >
  >* 표준 필드 그룹은 항상 오브젝트 루트에서 시작합니다.
  >
  >* 사용자 정의 필드 그룹은 항상 Experience Cloud 조직에 고유한 개체에서 시작합니다. `_techmarketingdemos` 이 예제에서

  앱 상호 작용 이벤트의 경우 다음과 같은 개체를 구성합니다.

  ```swift
  let xdmData: [String: Any] = [
    "eventType": "application.interaction",
    "_techmarketingdemos": [
      "appInformation": [
          "appInteraction": [
              "name": "login",
              "appAction": [
                  "value": 1
                  ]
              ]
          ]
      ]
  ]
  ```

  화면 추적 이벤트의 경우 다음과 같은 개체를 구성합니다.

  ```swift
  var xdmData: [String: Any] = [
    "eventType": "application.scene",
    "_techmarketingdemos": [
        "appInformation": [
            "appStateDetails": [
                "screenType": "App",
                    "screenName": "luma: content: ios: us: en: login",
                    "screenView": [
                        "value": 1
                    ]
                ]
            ] 
        ]
  ]
  ```


* 이제 이 데이터 구조를 사용하여 `ExperienceEvent`.

  ```swift
  let event = ExperienceEvent(xdm: xdmData)
  ```

* Platform Edge Network에 이벤트 및 데이터를 전송합니다.

  ```swift
  Edge.sendEvent(experienceEvent: event)
  ```


여기서도 Xcode 프로젝트에서 이 코드를 실제로 구현해 보겠습니다.

1. 편의를 위해 **[!UICONTROL MobileSDK]**. 다음으로 이동 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** 를 입력합니다.

   1. 앱 상호 작용을 위한 것입니다. 에 이 코드 추가 `func sendAppInteractionEvent(actionName: String)` 함수:

      ```swift
      // Set up a data dictionary, create an experience event and send the event.
      let xdmData: [String: Any] = [
          "eventType": "application.interaction",
          tenant : [
              "appInformation": [
                  "appInteraction": [
                      "name": actionName,
                      "appAction": [
                          "value": 1
                      ]
                  ]
              ]
          ]
      ]
      let appInteractionEvent = ExperienceEvent(xdm: xdmData)
      Edge.sendEvent(experienceEvent: appInteractionEvent)
      ```

      이 함수는 작업 이름을 매개 변수로 사용하고,

      * 함수의 매개 변수를 사용하여 XDM 페이로드를 사전으로 설정합니다.
      * 사전을 사용하여 경험 이벤트를 설정합니다.
      * 을(를) 사용하여 경험 이벤트를 전송합니다. [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API.


   1. 그리고 화면 추적을 위한 것도 있습니다. 에 이 코드 추가 `func sendTrackScreenEvent(stateName: String) ` 함수:

      ```swift
      // Set up a data dictionary, create an experience event and send the event.
      let xdmData: [String: Any] = [
          "eventType": "application.scene",
          tenant : [
              "appInformation": [
                  "appStateDetails": [
                      "screenType": "App",
                      "screenName": stateName,
                      "screenView": [
                          "value": 1
                      ]
                  ]
              ]
          ]
      ]
      let trackScreenEvent = ExperienceEvent(xdm: xdmData)
      Edge.sendEvent(experienceEvent: trackScreenEvent)
      ```

      이 함수는 상태 이름을 매개 변수로 사용하고,

      * 함수의 매개 변수를 사용하여 XDM 페이로드를 사전으로 설정합니다.
      * 사전을 사용하여 경험 이벤트를 설정합니다.
      * 을(를) 사용하여 경험 이벤트를 전송합니다. [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API.

1. 다음으로 이동 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL 로그인 시트]**.

   1. 로그인 단추 닫기에 다음과 같은 강조 표시된 코드를 추가합니다.

      ```swift
      // Send app interaction event
      MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
      ```

   1. 다음 강조 표시된 코드를 추가합니다. `onAppear` 수정자:

      ```swift
      // Send track screen event
      MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: login")
      ```

## 유효성 검사

1. 리뷰 [설치 지침](assurance.md#connecting-to-a-session) 시뮬레이터 또는 장치를 Assurance에 연결하는 섹션입니다.

   1. Assurance 아이콘을 왼쪽으로 이동합니다.
   1. 선택 **[!UICONTROL 홈]** 탭 표시줄에서 **[!UICONTROL ECID]**, **[!UICONTROL 이메일]** 및 **[!UICONTROL CRM ID]** 홈 화면에서 다음을 수행합니다.
   1. 선택 **[!DNL Products]** 을 클릭합니다.
   1. 제품을 선택합니다.
   1. 선택 <img src="assets/saveforlater.png" width="15" />.
   1. 선택 <img src="assets/addtocart.png" width="20" />.
   1. 선택 <img src="assets/purchase.png" width="15" />.

      <img src="./assets/mobile-app-events-3.png" width="300">


1. Assurance UI에서 **[!UICONTROL hitReceived]** 의 이벤트 **[!UICONTROL com.adobe.edge.konductor]** 공급업체.
1. 이벤트를 선택하고 의 XDM 데이터를 검토합니다. **[!UICONTROL 메시지]** 개체. 또는 다음을 사용할 수 있습니다 ![복사](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) **[!UICONTROL 원시 이벤트 복사]** 기본 설정의 텍스트 또는 코드 편집기를 사용하여 이벤트를 붙여넣고 검사합니다.

   ![데이터 수집 유효성 검사](assets/datacollection-validation.png)


## 다음 단계

이제 앱에 데이터 수집을 추가할 수 있는 모든 도구가 있어야 합니다. 사용자가 앱에서 제품과 상호 작용하는 방식에 더 많은 인텔리전스를 추가하고 앱에 더 많은 앱 상호 작용 및 화면 추적 호출을 추가할 수 있습니다.

* 앱에 주문, 체크아웃, 빈 장바구니 및 기타 기능을 구현하고 이 기능에 관련 상거래 경험 이벤트를 추가합니다.
* 호출 반복 `sendAppInteractionEvent` 를 적절한 매개 변수로 사용하여 사용자가 다른 앱 상호 작용을 추적합니다.
* 호출 반복 `sendTrackScreenEvent` 를 사용하여 앱에서 사용자가 본 화면을 추적할 수 있습니다.

>[!TIP]
>
>리뷰 [완료된 앱](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) 추가 예제를 보려면 다음을 수행하십시오.


## Analytics 및 Platform에 이벤트 보내기

이벤트를 수집하여 Platform Edge Network로 전송했으므로 이제 [데이터스트림](create-datastream.md). 이후 단원에서는 이 데이터를 다음에 매핑합니다 [Adobe Analytics](analytics.md), [Adobe Experience Platform](platform.md) 및 과 같은 기타 Adobe Experience Cloud 솔루션 [Adobe Target](target.md) 그리고 Adobe Journey Optimizer.

>[!SUCCESS]
>
>이제 Adobe Experience Platform Edge Network와 데이터 스트림에 정의한 모든 서비스에 대한 상거래, 앱 상호 작용 및 화면 추적 이벤트를 추적하도록 앱을 설정했습니다.<br/>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하려는 경우 또는 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

다음: **[웹 보기 처리](web-views.md)**
