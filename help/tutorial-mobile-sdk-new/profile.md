---
title: 프로필 데이터 수집
description: 모바일 앱에서 프로필 데이터를 수집하는 방법을 알아봅니다.
hide: true
source-git-commit: cd1efbfaa335c08cbcc22603fe349b4594cc1056
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 1%

---

# 프로필 데이터 수집

모바일 앱에서 프로필 데이터를 수집하는 방법을 알아봅니다.

프로필 확장 기능을 사용하여 클라이언트에 사용자 관련 속성을 저장할 수 있습니다. 이 정보는 최적의 성능을 위해 서버에 연결할 필요 없이 나중에 온라인 또는 오프라인 시나리오 중에 메시지를 타겟팅하고 개인화하는 데 사용할 수 있습니다. 프로필 확장은 CSOP(클라이언트측 작업 프로필)를 관리하고, API에 대응하는 방법을 제공하고, 사용자 프로필 속성을 업데이트하고, 사용자 프로필 속성을 생성된 이벤트로 나머지 시스템과 공유합니다.

프로필 데이터는 다른 확장에서 프로필 관련 작업을 수행하는 데 사용됩니다. 프로필 데이터를 사용하고 프로필 데이터를 기반으로 규칙을 실행하는 규칙 엔진 확장의 예를 들 수 있습니다. 에 대해 자세히 알아보기 [프로필 확장](https://developer.adobe.com/client-sdks/documentation/profile/) 설명서에서

>[!IMPORTANT]
>
>이 단원에서 설명하는 프로필 기능은 Adobe Experience Platform 및 플랫폼 기반 애플리케이션의 실시간 고객 프로필 기능과 별개입니다.


## 전제 조건

* SDK가 설치 및 구성된 앱을 빌드하고 실행했습니다.
* 프로필 SDK를 가져왔습니다.

  ```swift
  import AEPUserProfile
  ```

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* 사용자 속성을 설정하거나 업데이트합니다.
* 사용자 속성을 검색합니다.


## 사용자 특성 설정 및 업데이트

사용자의 과거 또는 최근 구매 여부를 빠르게 파악하려면 앱의 타겟팅 및/또는 개인화에 유용합니다. Luma 앱에서 설정해 보겠습니다.

1. 다음으로 이동 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** >  **[!DNL MobileSDK]** xcode Project 탐색기에서 `func updateUserAttribute(attributeName: String, attributeValue: String)` 함수. 다음 코드를 추가합니다.

   ```swift
   // Create a profile map, add attributes to the map and update profile using the map
   var profileMap = [String: Any]()
   profileMap[attributeName] = attributeValue
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

   이 코드:

   1. 라는 빈 사전을 설정합니다. `profileMap`.

   1. 를 사용하여 사전에 요소를 추가합니다. `attributeName` (예 `isPaidUser`), 및 `attributeValue` (예 `yes`).

   1. 를 사용합니다. `profileMap` 사전을 값에 추가 `attributeDict` 매개 변수 [`UserProfile.updateUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattributes) API 호출.

1. 다음으로 이동 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!DNL ProductView]** 를 클릭하고 호출을 찾습니다. `updateUserAttributes` (구매 코드 내 <img src="assets/purchase.png" width="15" /> 추가할 수 있습니다). 다음 코드를 추가합니다.

   ```swift
   // Update attributes
   MobileSDK.shared.updateUserAttributes(attributeName: "isPaidUser", attributeValue: "yes")
   ```


## 사용자 속성 가져오기

사용자의 속성을 업데이트하면 다른 Adobe SDK에서 사용할 수 있지만, 속성을 명시적으로 검색하여 앱이 원하는 대로 동작하도록 할 수도 있습니다.

1. 다음으로 이동 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!DNL HomeView]** xcode Project 탐색기에서 `.onAppear` 수정자. 다음 코드를 추가합니다.

   ```swift
   // Get attributes
   UserProfile.getUserAttributes(attributeNames: ["isPaidUser"]) { attributes, error in
       if attributes?["isPaidUser"] as! String == "yes" {
           showBadgeForUser = true
       }
       else {
           showBadgeForUser = false
       }
   }
   ```

   이 코드:

   1. 호출 [`UserProfile.getUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes) 을 사용한 API `iPaidUser` 속성 이름 을 단일 요소로 사용 `attributeNames` 배열입니다.
   1. 그런 다음 의 값을 확인합니다. `isPaidUser` 속성 및 시기 `yes`, 다음에 배지를 추가합니다. <img src="assets/paiduser.png" width="20" /> 아이콘 을 클릭하여 제품에서 사용할 수 있습니다.

추가 설명서를 찾을 수 있습니다 [여기](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## Assurance를 통해 유효성 검사

1. 리뷰 [설치 지침](assurance.md) 섹션.
1. 앱을 설치하십시오.
1. 보증 생성 URL을 사용하여 앱을 실행합니다.
1. 앱을 실행하여 로그인하고 제품과 상호 작용합니다.

   1. Assurance 아이콘을 왼쪽으로 이동합니다.
   1. 선택 **[!UICONTROL 홈]** 을 클릭합니다.
   1. 로그인 시트를 열려면 다음을 선택합니다 <img src="assets/login.png" width="15" /> 추가할 수 있습니다.

      <img src="./assets/mobile-app-events-1.png" width="300">

   1. 임의의 이메일과 고객 ID를 삽입하려면 <img src="assets/insert.png" width="15" /> 추가할 수 있습니다 .
   1. 선택 **[!UICONTROL 로그인]**.

      <img src="./assets/mobile-app-events-2.png" width="300">

   1. 선택 **[!DNL Products]** 을 클릭합니다.
   1. 제품 하나를 선택하십시오.
   1. 선택 <img src="assets/saveforlater.png" width="15" />.
   1. 선택 <img src="assets/addtocart.png" width="20" />.
   1. 선택 <img src="assets/purchase.png" width="15" />.

      <img src="./assets/mobile-app-events-3.png" width="300">

   1. 다음으로 돌아가기: **[!UICONTROL 홈]** 화면. 추가된 배지가 표시됩니다. <img src="assets/person-badge-icon.png" width="15" />.

      <img src="./assets/personbadges.png" width="300">



1. Assurance UI에 **[!UICONTROL 사용자 프로필 업데이트]** 및 **[!UICONTROL getUserAttributes]** 업데이트된 이벤트 `profileMap` 값.
   ![프로필 유효성 검사](assets/profile-validate.png)

>[!SUCCESS]
>
>이제 Edge Network 및 Adobe Experience Platform을 사용하여 (설정 시) 프로필의 속성을 업데이트하도록 앱을 설정했습니다.<br/>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하려는 경우 또는 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

다음: **[지리적 위치 서비스 사용](places.md)**
