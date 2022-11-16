---
title: 신원
description: 모바일 앱에서 ID 데이터를 수집하는 방법을 알아봅니다.
exl-id: cbcd1708-29e6-4d74-be7a-f75c917ba2fa
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 4%

---

# 신원

모바일 앱에서 ID 데이터를 수집하는 방법을 알아봅니다.

Adobe Experience Platform Identity Service를 사용하면 장치 및 시스템 전반에서 ID를 브리징하여 고객 및 행동을 더 잘 파악할 수 있으므로 효과적이고 개인화된 디지털 경험을 실시간으로 제공할 수 있습니다. ID 필드와 네임스페이스는 서로 다른 데이터 소스를 결합하여 360도 실시간 고객 프로필을 만드는 접착제입니다.

추가 정보 [ID 확장](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network) 그리고 [id 서비스](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=ko-KR) 참조하십시오.

## 전제 조건

* SDK가 설치 및 구성된 앱을 성공적으로 빌드하고 실행합니다.

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* 표준 ID를 업데이트합니다.
* 사용자 지정 ID를 설정합니다.
* 사용자 지정 ID를 업데이트합니다.
* ID 그래프의 유효성을 확인합니다.
* ECID 및 기타 ID를 가져옵니다.

## 표준 ID 업데이트

사용자가 로그인할 때 사용자의 ID 맵을 업데이트하기 시작합니다.

1. 다음으로 이동 `Login.swift` Luma 앱에서 `loginButt`.

   Luma 샘플 앱에는 사용자 이름 또는 암호 유효성 검사가 없습니다. 단추를 눌러 &quot;로그인&quot;하면 됩니다.

1. 만들기 `IdentityMap` 및 `IdentityItem`.

   ```swift
   let identityMap: IdentityMap = IdentityMap()
   let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
   ```

1. 추가 `IdentityItem` 변환 후 `IdentityMap`

   ```swift
   identityMap.add(item:emailIdentity, withNamespace: "Email")
   ```

1. 호출 `updateIdentities` 를 입력하여 Platform Edge Network에 데이터를 보냅니다.

   ```swift
   Identity.updateIdentities(with: identityMap)
   ```

>[!NOTE]
>
>하나의 updateIdentities 호출에서 여러 ID를 보낼 수 있습니다. 이전에 보낸 ID를 수정할 수도 있습니다.


## 사용자 지정 ID 네임스페이스 설정

ID 네임스페이스는 [ID 서비스](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=en) ID가 연관되는 컨텍스트의 지표 역할을 합니다. 예를 들어 &quot;name@email.com&quot;이라는 값을 이메일 주소로 또는 &quot;443522&quot;이라는 값을 숫자 CRM ID로 구분합니다.

1. 데이터 수집 인터페이스에서 을(를) 선택합니다 **[!UICONTROL ID]** 왼쪽 레일 탐색에서 를 클릭합니다.
1. 선택 **[!UICONTROL ID 네임스페이스 만들기]**.
1. 다음을 제공합니다. **[!UICONTROL 표시 이름]** 의 `Luma CRM ID` 그리고 **[!UICONTROL ID 기호]** 값 `lumaCrmId`.
1. 선택 **[!UICONTROL 교차 장치 ID]**.
1. **[!UICONTROL 만들기]**&#x200B;를 선택합니다.

![id 네임스페이스 만들기](assets/mobile-identity-create.png)

## 사용자 지정 ID 업데이트

사용자 지정 ID를 만들었으므로 이제 다음을 수정하여 수집을 시작합니다 `updateIdentities` 이전 단계에서 추가한 코드입니다. IdentityItem을 만들어 IdentityMap에 추가하면 됩니다. 다음은 전체 코드 블록의 모습입니다.

```swift
//Hardcoded identity values
let emailAddress = "testuser@gmail.com"
let crmId = "112ca06ed53d3db37e4cea49cc45b71e"

// Create identity map
let identityMap: IdentityMap = IdentityMap()
// Add email (standard)
let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
identityMap.add(item:emailIdentity, withNamespace: "Email")
// Add lumaCrmId (custom)
let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
identityMap.add(item: crmIdentity, withNamespace: "lumaCrmId")
// Update
Identity.updateIdentities(with: identityMap)
```

## ID 제거

다음을 사용할 수 있습니다 `removeIdentity` 저장된 클라이언트측 IdentityMap에서 ID를 제거하려면 Identity 확장은 Edge Network에 대한 식별자 전송을 중지합니다. 이 API를 사용해도 서버측 사용자 프로필 그래프 또는 ID 그래프에서 식별자가 제거되지 않습니다.

다음을 추가합니다 `removeIdentity` 로그아웃 단추에 대한 코드 클릭 `Account.swift`.

```swift
// Logout
let logout = UIAlertAction(title: "Logout", style: .destructive, handler: { (action) -> Void in
    isLoggedIn = false;
    ////Hardcoded identity values
    let emailAddress = "testuser@gmail.com"
    let crmId = "112ca06ed53d3db37e4cea49cc45b71e"
    // Adobe Experience Platform - Remove Identity
    Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
    Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCrmId")
})
```

>[!NOTE]
>위의 예에서 `crmId` 및 `emailAddress` 하드 코딩되지만 실제 앱에서는 값이 동적입니다.

## 보증으로 유효성 검사

1. 를 검토합니다. [설정 지침](assurance.md) 섹션에서 시뮬레이터나 장치를 Assurance에 연결합니다.
1. 앱의 오른쪽 아래에서 계정 아이콘을 선택합니다.

   ![luma 앱 계정](assets/mobile-identity-login.png)
1. 을(를) 선택합니다 **로그인** 버튼을 클릭합니다.
1. 사용자 이름과 암호를 입력할 수 있는 옵션이 표시되며, 둘 다 선택 사항이므로 간단히 선택할 수 있습니다 **로그인**.

   ![luma 앱 로그인](assets/mobile-identity-login-final.png)
1. Assurance 웹 UI에서 `Edge Identity Update Identities` 이벤트 `com.adobe.griffon.mobile` 공급업체
1. 이벤트를 선택하고 의 데이터를 검토하십시오 `ACPExtensionEventData` 개체. 업데이트한 ID가 표시됩니다.
   ![id 업데이트 확인](assets/mobile-identity-validate-assurance.png)

## ID 그래프로 유효성 검사

에서 단계를 완료하면 [Experience Platform 단원](platform.md)를 채울 수도 있습니다.

![id 그래프 유효성 검사](assets/mobile-identity-validate.png)


다음: **[프로필](profile.md)**

>[!NOTE]
>
>Adobe Experience Platform Mobile SDK에 대한 학습에 시간을 내주셔서 감사합니다. 질문이 있거나 일반 피드백을 공유하거나 향후 컨텐츠에 대한 제안 사항이 있는 경우 해당 정보를 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)