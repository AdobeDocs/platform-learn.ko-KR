---
title: 이벤트
description: 모바일 앱에서 이벤트 데이터를 수집하는 방법에 대해 알아봅니다.
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 0%

---

# 이벤트

모바일 앱에서 이벤트를 추적하는 방법에 대해 알아봅니다.

Edge Network 확장은 Platform Edge Network에 경험 이벤트를 전송하기 위한 API를 제공합니다. 경험 이벤트 는 XDM ExperienceEvent 스키마 정의를 따르는 데이터가 포함된 개체입니다. 보다 간단하게, 모바일 앱에서 사람들이 하는 작업을 캡처합니다. Platform Edge Network에서 데이터를 수신하면 Adobe Analytics 및 Experience Platform과 같이 데이터 스트림에 구성된 애플리케이션 및 서비스로 전달할 수 있습니다. 에 대해 자세히 알아보기 [경험 이벤트](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) 를 참조하십시오.

## 전제 조건

* 모든 패키지 종속성이 Xcode 프로젝트에 있습니다.
* AppDelegate에 등록된 확장입니다.
* 개발 appId를 사용하도록 MobileCore를 구성했습니다.
* 가져온 SDK.
* 위의 변경 사항을 포함하여 앱을 빌드하고 실행했습니다.

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

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

  ```swift {highlight="2-8"}
  var xdmData: [String: Any] = [
      "eventType": "commerce.productViews",
      "commerce": [
          "productViews": [
            "id": sku,
            "value": 1
          ]
      ]
  ]
  ```

   * `eventType`: 발생한 이벤트를 설명합니다. [알려진 값](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) 가능한 경우
   * `commerce.productViews.id`: 제품의 SKU를 나타내는 문자열 값
   * `commerce.productViews.value`: 이벤트의 숫자 값을 제공합니다. 부울(또는 Adobe Analytics의 &quot;카운터&quot;)인 경우 값은 항상 1로 설정됩니다. 숫자 또는 통화 이벤트인 경우 값은 1보다 클 수 있습니다.

* 스키마에서 상거래 제품 보기 이벤트와 관련된 추가 데이터를 식별합니다. 이 예에서는 다음을 포함합니다 `productListItems` 상거래 관련 이벤트와 함께 사용되는 표준 필드 세트입니다.

  ![제품 목록 항목 스키마](assets/datacollection-prodListItems-schema.png)
   * 주의: `productListItems` 는 여러 제품을 제공할 수 있는 배열입니다.

* 이 데이터를 추가하려면 `xdmData` 추가 데이터를 포함할 대상:

```swift {highlight="9-16"}
var xdmData: [String: Any] = [
    "eventType": "commerce.productViews",
        "commerce": [
        "productViews": [
            "id": sku,
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

* 그런 다음 데이터 구조를 사용하여 `ExperienceEvent`:

  ```swift
  let productViewEvent = ExperienceEvent(xdm: xdmData)
  ```

* 또한 sendEvent API를 사용하여 Platform Edge Network에 이벤트 및 데이터를 전송합니다.

  ```swift
  Edge.sendEvent(experienceEvent: productViewEvent)
  ```

이제 Xcode 프로젝트에서 이 코드를 실제로 구현해 보겠습니다.
앱에 다른 상거래 제품 관련 작업(보기, 장바구니에 추가, 나중에 사용하기 위해 저장, 구매)이 있고 사용자가 수행한 이러한 작업을 기반으로 이벤트를 전송하려고 합니다.

1. 경험 이벤트 전송을 구성하려면 다음 위치로 이동하십시오. `MobileSDK`을(를) 클릭하고 다음을 `sendCommerceExperienceEvent` 함수. 이 함수는 상거래 경험 이벤트 및 제품을 매개 변수로 사용합니다.

   ```swift {highlight="2-22"}
   func sendCommerceExperienceEvent(commerceEventType: String, product: Product) {
     let xdmData: [String: Any] = [
         "eventType": "commerce." + commerceEventType,
         "commerce": [
             commerceEventType: [
                 "id": product.sku,
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
   
     Logger.viewCycle.info("About to send commerce experience event of type  \(commerceEventType)..."
     let commerceExperienceEvent = ExperienceEvent(xdm: xdmData)
     Edge.sendEvent(experienceEvent: commerceExperienceEvent)
   }
   ```

1. 위치 `ProductView` 에 다양한 호출 추가 `sendCommerceExperienceEvent` 함수:

   1. 위치: `.task` 의 수정자 `ATTrackingManager.trackingAuthorizationStatus` 종료. 다음 `.task` 수정자는 제품 보기가 초기화되어 표시될 때 호출되므로 특정 시점에 제품 보기 이벤트를 보내려고 합니다.

      ```swift {highlight="4-5"}
      .task {
          if ATTrackingManager.trackingAuthorizationStatus == .authorized {
               // Send commerce experience event
              MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productView", product: product)
          }
      }
      ```

   1. 제품 보기에서 사용할 수 있는 도구 모음의 각 버튼(나중에 사용하기 위해 장바구니에 추가 및 구매)에 대해 관련 호출을 추가합니다.

      * 나중을 위해 저장 / 위시리스트에 추가:

        ```swift {highlight="5-6"}
        Button {
            Task {
                if ATTrackingManager.trackingAuthorizationStatus == .authorized {
                // Send saveForLater commerce experience event
                    MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "saveForLaters", product: product)
                }
            }
            showSaveForLaterDialog.toggle()
        } label: {
            Label("", systemImage: "heart")
        }
        .alert(isPresented: $showSaveForLaterDialog, content: {
            Alert(title: Text( "Saved for later"), message: Text("The selected item is saved to your wishlist…"))
        })
        ```

      * 장바구니에 추가:

        ```swift {highlight="5-6"}
        Button {
            Task {
                if ATTrackingManager.trackingAuthorizationStatus == .authorized {
                    // Send productListAdds commerce experience event
                    MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productListAdds", product: product)
                }
            }
            showAddToCartDialog.toggle()
        } label: {
                Label("", systemImage: "cart.badge.plus")
        }
        alert(isPresented: $showAddToCartDialog, content: {
            Alert(title: Text( "Added to basket"), message: Text("The selected item is added to your basket…"))
        })
        ```

      * 구매용:

        ```swift {highlight="5-6"}
        Button {
            Task {
                if ATTrackingManager.trackingAuthorizationStatus == .authorized {
                    // Send purchase commerce experience event
                    MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
                }
            }
            showPurchaseDialog.toggle()
        } label: {
            Label("", systemImage: "creditcard")
        }
        .alert(isPresented: $showPurchaseDialog, content: {
            Alert(title: Text( "Purchases"), message: Text("The selected item is purchased…"))
        })
        ```

### 사용자 정의 필드 그룹

앱 자체에서 화면 보기 및 상호 작용을 추적한다고 상상해 보십시오. 이 유형의 이벤트에 대해 사용자 정의 필드 그룹을 정의했음을 기억하십시오.

* 스키마에서 수집하려는 이벤트를 식별합니다.
  ![앱 상호 작용 스키마](assets/datacollection-appInteraction-schema.png)

* 객체 구성을 시작합니다.

  >[!NOTE]
  >
  >  표준 필드 그룹은 항상 오브젝트 루트에서 시작합니다.
  >
  >  사용자 정의 필드 그룹은 항상 Experience Cloud 조직에 고유한 개체에서 시작합니다. `_techmarketingdemos` 이 예제에서

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


* 그런 다음 데이터 구조를 만들어 `ExperienceEvent`.

  ```swift
  let event = ExperienceEvent(xdm: xdmData)
  ```

* Platform Edge Network에 이벤트 및 데이터를 전송합니다.

  ```swift
  Edge.sendEvent(experienceEvent: event)
  ```


여기서도 Xcode 프로젝트에서 이 코드를 실제로 구현해 보겠습니다.

1. 편의를 위해 `MobileSDK`.

   앱 상호 작용을 위한 것입니다. 강조 표시된 코드를 `sendAppInteractionEvent(actionName)` 의 함수 **[!UICONTROL MobileSDK]**:

   ```swift {highlight="2-16"}
   func sendAppInteractionEvent(actionName: String) {
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
   }
   ```

   그리고 화면 추적을 위한 것도 있습니다. 강조 표시된 코드를 `sendTrackScreenEvent(stateName)` 의 함수 **[!UICONTROL MobileSDK]**:

   ```swift {highlight="2-17"}
   func sendTrackScreenEvent(stateName: String) {
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
   }
   ```

1. 다음으로 이동 **[!UICONTROL 로그인 시트]**.

   * 로그인 단추 닫기에 다음과 같은 강조 표시된 코드를 추가합니다.

     ```swift {highlight="3"}
     Button("Login") {                               
        // Send app interaction event
        MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
        dismiss()
     }
     .disabled(currentEmailId.isValidEmail == false)
     .buttonStyle(.bordered)
     ```

   * 다음 강조 표시된 코드를 추가합니다. `onAppear` 수정자:

     ```swift {highlight="13"}
     .onAppear {
        Task {
            if currentEmailId == "testUser@gmail.com" || currentEmailId.isValidEmail == false {
                // still allow to log in
                disableLogin = false
            }
            else {
                disableLogin = true
            }
        }
        // Send track screen event
        MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: login")
     }
     ```

### 유효성 검사

1. 리뷰 [설치 지침](assurance.md) 시뮬레이터 또는 장치를 Assurance에 연결하고 연결합니다.
1. 앱을 실행하여 로그인하고 제품과 상호 작용합니다.

   1. Assurance 아이콘을 왼쪽으로 이동합니다.
   1. 선택 **[!UICONTROL 홈]** 을 클릭합니다.
   1. 다음 항목 선택 **[!UICONTROL 로그인]** 단추를 클릭하여 로그인 시트를 엽니다.
   1. 다음 항목 선택 **[!UICONTROL A|]** 임의의 이메일과 고객 id를 삽입하는 버튼입니다.
   1. 선택 **[!UICONTROL 로그인]**.
   1. 선택 **[!UICONTROL 제품]** 을 클릭합니다.
   1. 제품을 선택합니다.
   1. 선택 **[!UICONTROL 나중에 저장]**.
   1. 선택 **[!UICONTROL 장바구니에 추가]**.
   1. 선택 **[!UICONTROL 구매]**.

      <img src="./assets/mobile-app-events-1.png" width="200"> <img src="./assets/mobile-app-events-2.png" width="200"> <img src="./assets/mobile-app-events-3.png" width="200">


1. 다음 항목을 찾습니다. **[!UICONTROL hitReceived]** 의 이벤트 **[!UICONTROL com.adobe.edge.konductor]** 공급업체.
1. 이벤트를 선택하고 의 XDM 데이터를 검토합니다. **[!UICONTROL 메시지]** 개체.
   ![데이터 수집 유효성 검사](assets/datacollection-validation.png)


### Luma 앱에서 구현

이제 Luma 앱에 데이터 수집을 추가할 수 있는 모든 도구가 있어야 합니다. 사용자가 제품과 상호 작용하는 방법에 인텔리전스를 추가하고 앱에 앱 상호 작용 및 화면 추적 호출을 추가할 수 있습니다.

* 앱에 주문, 체크아웃, 빈 장바구니 및 기타 기능을 구현하고 이 기능에 관련 상거래 경험 이벤트를 추가합니다.
* 호출 반복 `sendAppInteractionEvent` 를 적절한 매개 변수로 사용하여 사용자가 앱에서 다른 앱 상호 작용을 추적할 수 있습니다.
* 호출 반복 `sendTrackScreenEvent` 를 적절한 매개 변수로 사용하여 앱에서 사용자가 본 각 화면을 추적합니다.

>[!TIP]
>
>리뷰 [완전히 구현된 앱](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) 추가 예제를 보려면 다음을 수행하십시오.


## Analytics 및 Platform에 이벤트 보내기

이벤트를 수집하여 Platform Edge Network로 전송했으므로 이제 [데이터스트림](create-datastream.md). 이후 단원에서는 이 데이터를 다음에 매핑합니다 [Adobe Analytics](analytics.md) 및 [Adobe Experience Platform](platform.md).

>[!SUCCESS]
>
>이제 Adobe Experience Platform Edge Network와 데이터 스트림에 정의한 모든 서비스에 대한 상거래, 앱 상호 작용 및 화면 추적 이벤트를 추적하도록 앱을 설정했습니다.<br/>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하려는 경우 또는 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

다음: **[웹 보기 수](web-views.md)**
