---
title: 프로필
description: 모바일 앱에서 프로필 데이터를 수집하는 방법을 알아봅니다.
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 2%

---

# 프로필

모바일 앱에서 프로필 데이터를 수집하는 방법을 알아봅니다.

프로필 확장을 사용하여 클라이언트에 사용자 특성을 저장할 수 있습니다. 이 정보는 최적의 성능을 위해 서버에 연결하지 않고 나중에 온라인 또는 오프라인 시나리오 동안 메시지를 타겟팅하고 개인화하는 데 사용할 수 있습니다. 프로필 확장은 CSOP(클라이언트측 작업 프로필)를 관리하고, API에 대응하고, 사용자 프로필 속성을 업데이트하고, 사용자 프로필 속성을 생성된 이벤트로 시스템의 나머지 부분과 공유하는 방법을 제공합니다.

프로필 데이터는 다른 확장에서 프로필 관련 작업을 수행하는 데 사용됩니다. 예를 들어 프로필 데이터를 사용하고 프로필 데이터를 기반으로 규칙을 실행하는 규칙 엔진 확장이 있습니다. 추가 정보 [프로필 확장](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile) 설명서에서

>[!IMPORTANT]
>
>이 단원에서 설명하는 프로필 기능은 Adobe Experience Platform 및 플랫폼 기반 애플리케이션의 실시간 고객 프로필 기능과 별개입니다.


## 전제 조건

* SDK가 설치 및 구성된 앱을 성공적으로 빌드하고 실행합니다.
* 프로필 SDK를 가져왔습니다.

   ```swift
   import AEPUserProfile
   ```

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* 사용자 특성을 설정하거나 업데이트합니다.
* 사용자 특성을 검색합니다.


## 설정 및 업데이트

따라서 사용자가 이전에 앱에서 구매했는지 여부를 빠르게 파악할 수 있도록 타깃팅 및/또는 개인화에 유용합니다. Luma 앱에서 설정합니다.

1. 다음으로 이동 `Cart.swift`

1. 아래 코드를 `processOrder() `함수 위에 있어야 합니다.

   ```swift
   var profileMap = [String: Any]()
   profileMap["isPaidUser"] = "yes"
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

개인화 팀은 사용자의 충성도 수준을 기반으로 타겟팅할 수도 있습니다. Luma 앱에서 설정합니다.

1. 다음으로 이동 `Account.swift`

1. 아래 코드를 `showUserInfo()` 함수 위에 있어야 합니다.

   ```swift
   var profileMap = [String: Any]()
   profileMap["loyaltyLevel"] = loyaltyLevel
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

추가 `updateUserAttributes` 설명서를 찾을 수 있습니다. [여기](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile/profile-api-references#update-user-attributes).

## 가져오기

사용자의 속성을 업데이트하면 다른 Adobe SDK에서 사용할 수 있지만 속성을 명시적으로 검색할 수도 있습니다.

```swift
UserProfile.getUserAttributes(attributeNames: ["isPaidUser","loyaltyLevel"]){
    attributes, error in
    print("Profile: getUserAttributes: ",attributes as Any)
}
```

추가 `getUserAttributes` 설명서를 찾을 수 있습니다. [여기](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile/profile-api-references#get-user-attributes).

## 보증으로 유효성 검사

1. 를 검토합니다. [설정 지침](assurance.md) 섹션을 참조하십시오.
1. 앱을 설치하십시오.
1. Assurance 생성 URL을 사용하여 앱을 시작합니다.
1. 계정 아이콘을 선택한 다음 로그인을 선택합니다. 참고: 자격 증명을 제공하지 않았습니다.
1. 로그인 메뉴를 닫은 다음 계정 아이콘을 다시 선택합니다. 그러면 다음과 같은 계정 세부 사항 화면으로 이동합니다 `loyaltyLevel` 이(가) 설정되어 있습니다.
1. 다음 항목이 표시됩니다. **[!UICONTROL UserProfileUpdate]** Assurance UI에서 업데이트된 `profileMap` 값.
   ![프로필 유효성 검사](assets/mobile-profile-validate.png)

다음: **[Adobe Analytics에 데이터 매핑](analytics.md)**

>[!NOTE]
>
>Adobe Experience Platform Mobile SDK에 대한 학습에 시간을 내주셔서 감사합니다. 질문이 있거나 일반 피드백을 공유하거나 향후 컨텐츠에 대한 제안 사항이 있는 경우 해당 정보를 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)