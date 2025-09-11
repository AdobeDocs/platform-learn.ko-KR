---
title: Platform Mobile SDK으로 프로필 데이터 수집
description: 모바일 앱에서 프로필 데이터를 수집하는 방법을 알아봅니다.
jira: KT-14634
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: 49d8c53d2ba2f9dcecf2470d855ad22f44763f6f
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 2%

---

# 프로필 데이터 수집

모바일 앱에서 프로필 데이터를 수집하는 방법을 알아봅니다.

프로필 확장 기능을 사용하여 클라이언트에 사용자 관련 속성을 저장할 수 있습니다. 이 정보는 최적의 성능을 위해 서버에 연결할 필요 없이 나중에 온라인 또는 오프라인 시나리오 중에 메시지를 타겟팅하고 개인화하는 데 사용할 수 있습니다.

프로필 확장은 CSOP(클라이언트측 작업 프로필)를 관리하고, API에 대응하는 방법을 제공하고, 사용자 프로필 속성을 업데이트하고, 사용자 프로필 속성을 생성된 이벤트로 나머지 시스템과 공유합니다.

프로필 데이터는 다른 확장에서 프로필 관련 작업을 수행하는 데 사용됩니다. 프로필 데이터를 사용하고 프로필 데이터를 기반으로 규칙을 실행하는 규칙 엔진 확장의 예를 들 수 있습니다. 설명서에서 [프로필 확장](https://developer.adobe.com/client-sdks/documentation/profile/)에 대해 자세히 알아보세요

>[!IMPORTANT]
>
>이 단원에서 설명하는 프로필 기능은 Adobe Experience Platform 및 플랫폼 기반 애플리케이션의 실시간 고객 프로필 기능과 별개입니다.


## 전제 조건

* SDK가 설치 및 구성된 앱을 빌드하고 실행했습니다.

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* 사용자 속성을 설정하거나 업데이트합니다.
* 사용자 속성을 검색합니다.


## 사용자 특성 설정 및 업데이트

사용자가 과거에 또는 최근에 구매했는지 여부를 앱에서 빠르게 알 수 있도록 타겟팅 및 개인화하는 데 도움이 될 것입니다. Luma 앱에서 설정해 보겠습니다.

>[!BEGINTABS]

>[!TAB iOS]

1. Xcode 프로젝트 탐색기에서 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!DNL MobileSDK]**(으)로 이동하여 `func updateUserAttribute(attributeName: String, attributeValue: String)` 함수를 찾습니다. 다음 코드를 추가합니다.

   ```swift
   // Create a profile map, add attributes to the map and update profile using the map
   var profileMap = [String: Any]()
   profileMap[attributeName] = attributeValue
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

   이 코드:

   1. `profileMap`(이)라는 빈 사전을 설정합니다.

   1. `attributeName`(예: `isPaidUser`) 및 `attributeValue`(예: `yes`)을(를) 사용하여 사전에 요소를 추가합니다.

   1. `profileMap` 사전을 `attributeDict`[`UserProfile.updateUserAttributes` API 호출의 ](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattributes) 매개 변수에 대한 값으로 사용합니다.

1. Xcode 프로젝트 탐색기에서 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!DNL ProductView]**(으)로 이동하여 `updateUserAttributes`(구매용 코드 내)에 대한 호출을 찾습니다 <img src="assets/purchase.png" width="15" /> 단추). 다음 코드를 추가합니다.

   ```swift
   // Update attributes
   MobileSDK.shared.updateUserAttribute(attributeName: "isPaidUser", attributeValue: "yes")
   ```

>[!TAB Android]

1. Android Studio 탐색기에서 **[!UICONTROL Android]** ![VDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!UICONTROL 모델]** > **[!UICONTROL MobileSDK]**(으)로 이동하여 `func updateUserAttribute(attributeName: String, attributeValue: String)` 함수를 찾습니다. 다음 코드를 추가합니다.

   ```kotlin
   // Create a profile map, add attributes to the map and update profile using the map
   val profileMap = mapOf(attributeName to attributeValue)
   UserProfile.updateUserAttributes(profileMap)
   ```

   이 코드:

   1. 이름이 `profileMap`인 빈 맵을 설정합니다.

   1. `attributeName`(예: `isPaidUser`) 및 `attributeValue`(예: `yes`)을(를) 사용하여 맵에 요소를 추가합니다.

   1. `profileMap` 맵을 `attributeDict`[`UserProfile.updateUserAttributes` API 호출의 ](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattributes) 매개 변수에 대한 값으로 사용합니다.

1. **[!UICONTROL Android]** ![VDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!UICONTROL 보기]** > **[!UICONTROL ProductView.kt]**(으)로 이동하여 `updateUserAttributes`(구매 코드 내)에 대한 호출을 찾습니다 <img src="assets/purchase.png" width="15" /> 단추). 다음 코드를 추가합니다.

   ```kotlin
   // Update attributes
   MobileSDK.shared.updateUserAttribute("isPaidUser", "yes")
   ```

>[!ENDTABS]

## 사용자 속성 가져오기

사용자의 속성을 업데이트하면 다른 Adobe SDK에서 사용할 수 있지만, 속성을 명시적으로 검색하여 앱이 원하는 대로 동작하도록 할 수도 있습니다.

>[!BEGINTABS]

>[!TAB iOS]

1. Xcode 프로젝트 탐색기에서 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!DNL HomeView]**(으)로 이동하여 `.onAppear` 수정자를 찾습니다. 다음 코드를 추가합니다.

   ```swift
   // Get attributes
   UserProfile.getUserAttributes(attributeNames: ["isPaidUser"]) { attributes, error in
       if attributes?.count ?? 0 > 0 {
           if attributes?["isPaidUser"] as? String == "yes" {
               showBadgeForUser = true
           }
           else {
               showBadgeForUser = false
           }
       }
   }
   ```

   이 코드:

   1. [`UserProfile.getUserAttributes` 배열에서 단일 요소로 ](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes) 특성 이름이 있는 `isPaidUser` `attributeNames` API를 호출합니다.
   1. 그런 다음 `isPaidUser` 특성의 값을 확인하고 `yes`이(가) 오른쪽 상단의 도구 모음에 있는 <img src="assets/paiduser.png" width="20"> 아이콘

>[!TAB Android]

1. Android Studio 프로젝트 탐색기에서 **[!UICONTROL Android]** ![VDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.androi]** > **[!DNL views]** > **[!DNL HomeView.kt]**(으)로 이동하여 `.onAppear` 수정자를 찾습니다. 다음 코드를 추가합니다.

   ```kotlin
   // Get attributes
   UserProfile.getUserAttributes(listOf("isPaidUser")) { attributes ->
       showBadgeForUser = attributes?.get("isPaidUser") == "yes"
   }
   ```

   이 코드:

   1. [`UserProfile.getUserAttributes` 배열에서 단일 요소로 ](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes) 특성 이름이 있는 `isPaidUser` `attributeNames` API를 호출합니다.
   1. 그런 다음 `isPaidUser` 특성의 값을 확인합니다. `yes`에서 코드는 개인 아이콘을 오른쪽 상단의 도구 모음에 있는 <img src="assets/paiduser.png" width="20"> 아이콘

>[!ENDTABS]

자세한 내용은 [API 참조](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes)를 참조하십시오.

## Assurance를 사용한 유효성 검사

1. [설치 지침](assurance.md#connecting-to-a-session) 섹션을 검토하여 시뮬레이터 또는 장치를 Assurance에 연결하십시오.
1. 앱을 실행하여 로그인하고 제품과 상호 작용합니다.

>[!BEGINTABS]

>[!TAB iOS]

1. 탭 표시줄에서 **[!UICONTROL 홈]**&#x200B;을(를) 선택합니다.
1. Assurance 아이콘을 왼쪽으로 이동합니다.
1. 로그인 시트를 열려면 다음을 선택합니다 <img src="assets/login.png" width="15" /> 단추입니다.

   <img src="./assets/mobile-app-events-1.png" width="300">

1. 임의의 이메일과 고객 ID를 삽입하려면 <img src="assets/insert.png" width="15" /> 단추 .
1. **[!UICONTROL 로그인]**&#x200B;을 선택합니다.

   <img src="./assets/mobile-app-events-2.png" width="300">

1. 탭 표시줄에서 **[!DNL Products]**&#x200B;을(를) 선택합니다.
1. 제품 하나를 선택하십시오.
1. 선택 <img src="assets/saveforlater.png" width="15" />.
1. 선택 <img src="assets/addtocart.png" width="20">.
1. 선택 <img src="assets/purchase.png" width="15" />.

   <img src="./assets/mobile-app-events-3.png" width="300">

1. **[!UICONTROL 홈]** 화면으로 돌아갑니다. 배지가 추가된 것을 확인해야 합니다 <img src="assets/person-badge-icon.png" width="15" />.

   <img src="./assets/personbadges.png" width="300">


>[!TAB Android]

1. 탭 표시줄에서 **[!UICONTROL 홈]**&#x200B;을(를) 선택합니다.
1. Assurance 아이콘을 왼쪽으로 이동합니다.
1. 로그인 시트를 열려면 다음을 선택합니다 <img src="assets/login.png" width="15" /> 단추입니다.

   <img src="./assets/mobile-app-events-1-android.png" width="300">

1. 임의의 이메일과 고객 ID를 삽입하려면 <img src="assets/insert.png" width="15" /> 단추 .
1. **[!UICONTROL 로그인]**&#x200B;을 선택합니다.

   <img src="./assets/mobile-app-events-2-android.png" width="300">

1. 탭 표시줄에서 **[!DNL Products]**&#x200B;을(를) 선택합니다.
1. 제품 하나를 선택하십시오.
1. 선택<img src="assets/heart.png" width="25">.
1. 선택 <img src="assets/addtocart.png" width="20">.
1. 선택 <img src="assets/purchase.png" width="15" />.

   <img src="./assets/mobile-app-events-3-android.png" width="300">

1. **[!UICONTROL 홈]** 화면으로 돌아갑니다. 개인 아이콘이 업데이트되었는지 확인해야 합니다.

   <img src="./assets/personbadges-android.png" width="300">

>[!ENDTABS]


Assurance UI에 업데이트된 **[!UICONTROL 값이 있는]** UserProfileUpdate **[!UICONTROL 및]** getUserAttributes`profileMap` 이벤트가 표시됩니다.

![프로필 유효성 검사](assets/profile-validate.png){zoomable="yes"}

>[!SUCCESS]
>
>이제 Adobe Experience Platform 및 (설정 시) Edge Network에서 프로필의 속성을 업데이트하도록 앱을 설정했습니다.
>
>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하고 싶거나 향후 콘텐츠에 대한 제안이 있는 경우 이 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)에서 공유하십시오.

다음: **[위치 사용](places.md)**
