---
title: 신원
description: 모바일 앱에서 ID 데이터를 수집하는 방법에 대해 알아봅니다.
feature: Mobile SDK,Identities
hide: true
source-git-commit: 4101425bd97e271fa6cc15157a7be435c034e764
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 6%

---

# 신원

모바일 앱에서 ID 데이터를 수집하는 방법에 대해 알아봅니다.

Adobe Experience Platform Identity Service를 사용하면 디바이스와 시스템 간에 ID를 연결하여 고객과 고객의 행동을 더 잘 볼 수 있으므로 효과적인 개인 디지털 경험을 실시간으로 제공할 수 있습니다. ID 필드와 네임스페이스는 서로 다른 데이터 소스를 함께 연결하여 360도 실시간 고객 프로필을 만드는 접착제입니다.

에 대해 자세히 알아보기 [ID 확장](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) 및 [id 서비스](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=ko-KR) 설명서에서 참조하십시오.

## 전제 조건

* SDK가 설치 및 구성된 앱을 빌드하고 실행했습니다.

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* 사용자 지정 ID 네임스페이스를 설정합니다.
* ID를 업데이트합니다.
* ID 그래프의 유효성을 검사합니다.
* ECID 및 기타 ID를 가져옵니다.


## 사용자 정의 ID 네임스페이스 설정

ID 네임스페이스는 의 구성 요소입니다. [ID 서비스](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=ko-KR) id가 연관되는 컨텍스트의 지표 역할을 합니다. 예를 들어 `name@email.com` 값은 이메일 주소로, `443522` 값은 숫자 CRM ID로 구분합니다.

1. 데이터 수집 인터페이스에서 다음을 선택합니다. **[!UICONTROL ID]** 왼쪽 레일 탐색에서
1. **[!UICONTROL 신원 네임스페이스 만들기]**&#x200B;를 선택합니다.
1. 다음을 제공합니다. **[!UICONTROL 표시 이름]** / `Luma CRM ID` 및 **[!UICONTROL ID 심볼]** 값 `lumaCRMId`.
1. 선택 **[!UICONTROL 교차 장치 ID]**.
1. **[!UICONTROL 만들기]**&#x200B;를 선택합니다.

   ![id 네임스페이스 만들기](assets/identity-create.png)




## ID 업데이트

사용자가 앱에 로그인할 때 표준 ID(이메일)와 사용자 지정 ID(Luma CRM ID)를 모두 업데이트하려고 합니다.

1. 다음으로 이동 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL 유틸리티]** > **[!UICONTROL MobileSDK]** xcode 프로젝트 탐색기에서 `func updateIdentities(emailAddress: String, crmId: String)` 함수 구현. 다음 코드를 함수에 추가합니다.

   ```swift
   // Set up identity map
   let identityMap: IdentityMap = IdentityMap()
   
   // Add identity items to identity map
   let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
   let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
   identityMap.add(item:emailIdentity, withNamespace: "Email")
   identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
   
   // Update identities
   Identity.updateIdentities(with: identityMap)
   ```

   이 코드:

   1. 빈 을(를) 만듭니다. `IdentityMap` 개체.

      ```swift
      let identityMap: IdentityMap = IdentityMap()
      ```

   1. 설정 `IdentityItem` 이메일 및 CRM ID에 대한 개체입니다.

      ```swift
      let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
      let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
      ```

   1. 다음 항목 추가 `IdentityItem` 에 대한 오브젝트 `IdentityMap` 개체.

      ```swift
      identityMap.add(item:emailIdentity, withNamespace: "Email")
      identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
      ```

   1. 다음을 전송합니다. `IdentityItem` 의 일부로 개체 `Identity.updateIdentities` Edge Network에 대한 API 호출.

      ```swift
      Identity.updateIdentities(with: identityMap) 
      ```

1. 다음으로 이동 **[!UICONTROL Luma]** **[!UICONTROL Luma]** > **[!UICONTROL 보기]** > **[!UICONTROL 일반]** > **[!UICONTROL 로그인 시트]** xcode 프로젝트 탐색기에서 를 선택하고 **[!UICONTROL 로그인]** 단추를 클릭합니다. 다음 코드를 추가합니다.

   ```swift
   // call updaeIdentities
   MobileSDK.shared.updateIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                             
   ```


>[!NOTE]
>
>한 번에 여러 ID를 보낼 수 있습니다 `updateIdentities` 호출합니다. 이전에 전송된 ID를 수정할 수도 있습니다.


## ID 제거

다음을 사용할 수 있습니다. `removeIdentity` 저장된 클라이언트측 IdentityMap에서 id를 제거합니다. ID 확장은 Edge 네트워크에 대한 식별자 전송을 중지합니다. 이 API를 사용해도 서버측 사용자 프로필 그래프 또는 ID 그래프에서 식별자가 제거되지 않습니다.

1. 다음으로 이동 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL 일반]** > **[!UICONTROL MobileSDK]** xcode 프로젝트 탐색기에서 다음 코드를 `func removeIdentities(emailAddress: String, crmId: String)` 함수:

   ```swift
   Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
   Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCRMId")
   // reset email and CRM Id to their defaults
   currentEmailId = "testUser@gmail.com"
   currentCRMId = "112ca06ed53d3db37e4cea49cc45b71e"
   ```

1. 다음으로 이동 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL 보기]** > **[!UICONTROL 일반]** > **[!UICONTROL 로그인 시트]** xcode 프로젝트 탐색기에서 를 선택하고 **[!UICONTROL 로그아웃]** 단추를 클릭합니다. 다음 코드를 추가합니다.

   ```swift
   // call removeIdentities
   MobileSDK.shared.removeIdentities(emailAddress: currentEmailId, crmId: currentCRMId)
   dismiss()                   
   ```


## Assurance를 통해 유효성 검사

1. 리뷰 [설치 지침](assurance.md) 시뮬레이터 또는 장치를 Assurance에 연결하고 연결합니다.
1. Luma 앱에서
   1. 다음 항목 선택 **[!UICONTROL 홈]** 탭.
   1. 다음 항목 선택 <img src="assets/login.png" width="15" /> 오른쪽 상단의 아이콘
   1. 이메일 주소와 CRM ID를 제공하거나
   1. 선택 <img src="assets/insert.png" width="15" /> 을(를) 임의로 생성하려면 **[!UICONTROL 이메일]** 및 **[!UICONTROL CRM ID]**.
   1. 선택 **[!UICONTROL 로그인]**.

      <img src="./assets/identity1.png" width="300"> <img src="./assets/identity2.png" width="300">


1. 에 대한 Assurance 웹 UI를 살펴봅니다. **[!UICONTROL Edge Identity 업데이트 Id]** 다음에서 이벤트 발생 **[!UICONTROL com.adobe.grifcon.mobile]** 공급업체.
1. 이벤트를 선택하고 **[!UICONTROL ACPExtensionEventData]** 개체. 업데이트한 ID가 표시됩니다.
   ![id 업데이트 확인](assets/identity-validate-assurance.png)

## ID 그래프로 유효성 검사

의 단계를 완료하면 [Experience Platform 레슨](platform.md), 플랫폼 ID 그래프 뷰어에서 ID 캡처를 확인할 수 있습니다.

1. 선택 **[!UICONTROL ID]** (데이터 수집 UI)
1. 선택 **[!UICONTROL ID 그래프]** 을 클릭합니다.
1. 입력 `Luma CRM ID` (으)로 **[!UICONTROL ID 네임스페이스]** 및 CRM ID(예: `24e620e255734d8489820e74f357b5c8`)을 로 사용하는 경우 **[!UICONTROL ID 값]**.
1. 다음을 볼 수 있습니다. **[!UICONTROL ID]** 나열됨.

   ![id 그래프 유효성 검사](assets/identity-validate-graph.png)


>[!SUCCESS]
>
>이제 Edge Network에서 ID를 업데이트하고 Adobe Experience Platform으로 (설정 시) 앱을 설정했습니다.<br/>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하려는 경우 또는 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

다음: **[프로필](profile.md)**
