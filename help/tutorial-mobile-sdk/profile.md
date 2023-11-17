---
title: 프로필
description: 모바일 앱에서 프로필 데이터를 수집하는 방법을 알아봅니다.
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: 94ca4a238c241518219fb2e8d73f775836f86d86
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 2%

---

# 프로필

모바일 앱에서 프로필 데이터를 수집하는 방법을 알아봅니다.

>[!INFO]
>
> 이 튜토리얼은 2023년 11월 말에 새 샘플 모바일 앱을 사용하는 새 튜토리얼로 대체됩니다

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


## 설정 및 업데이트

사용자가 이전에 앱에서 구매했는지 여부를 빠르게 알 수 있는 타겟팅 및/또는 개인화에 유용합니다. Luma 앱에서 설정해 보겠습니다.

1. 다음으로 이동 `Cart.swift`

1. 아래 코드를 `processOrder() `함수.

   ```swift
   var profileMap = [String: Any]()
   profileMap["isPaidUser"] = "yes"
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

개인화 팀은 사용자의 충성도 수준을 기반으로 타깃팅할 수도 있습니다. Luma 앱에서 설정해 보겠습니다.

1. 다음으로 이동 `Account.swift`

1. 아래 코드를 `showUserInfo()` 함수.

   ```swift
   var profileMap = [String: Any]()
   profileMap["loyaltyLevel"] = loyaltyLevel
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

추가 `updateUserAttributes` 설명서를 찾을 수 있음 [여기](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattribute).

## 가져오기

사용자의 속성을 업데이트하면 다른 Adobe SDK에서 사용할 수 있지만 속성을 명시적으로 검색할 수도 있습니다.

```swift
UserProfile.getUserAttributes(attributeNames: ["isPaidUser","loyaltyLevel"]){
    attributes, error in
    print("Profile: getUserAttributes: ",attributes as Any)
}
```

추가 `getUserAttributes` 설명서를 찾을 수 있음 [여기](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## Assurance를 통해 유효성 검사

1. 리뷰 [설치 지침](assurance.md) 섹션.
1. 앱을 설치하십시오.
1. 보증 생성 URL을 사용하여 앱을 실행합니다.
1. 계정 아이콘을 선택한 다음 로그인을 선택합니다. 참고: 자격 증명을 제공할 수 없습니다.
1. 로그인 메뉴를 닫은 다음 계정 아이콘을 다시 선택합니다. 계정 세부 사항 화면으로 이동합니다. `loyaltyLevel` 이(가) 설정되어 있습니다.
1. 다음이 표시됩니다. **[!UICONTROL 사용자 프로필 업데이트]** Assurance UI의 이벤트(업데이트됨) `profileMap` 값.
   ![프로필 유효성 검사](assets/mobile-profile-validate.png)

다음: **[Adobe Analytics에 데이터 매핑](analytics.md)**

>[!NOTE]
>
>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나, 일반적인 피드백을 공유하거나, 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오. [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)