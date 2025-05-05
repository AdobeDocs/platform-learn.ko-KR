---
title: Platform Mobile SDK 구현에 대한 보증 설정
description: 모바일 앱에서 Assurance 확장을 구현하는 방법을 알아봅니다.
feature: Mobile SDK,Assurance
jira: KT-14628
exl-id: e15774b2-2f52-400f-9313-bb4338a88918
source-git-commit: 576f85eda6e5888b9eafa15a705a99c3a70fed07
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 5%

---

# 보증 설정

모바일 앱에서 Adobe Experience Platform Assurance를 설정하는 방법을 알아봅니다.

Assurance는 정식적으로 프로젝트 그리폰이라고 하며, 모바일 앱에서 데이터를 수집하거나 경험을 제공하는 방법을 검사, 증명, 시뮬레이션 및 확인하는 데 도움이 되도록 설계되었습니다.

Assurance를 통해 Adobe Experience Platform Mobile SDK에서 생성된 원시 SDK 이벤트를 검사할 수 있습니다. SDK에서 수집한 모든 이벤트를 검사할 수 있습니다. SDK 이벤트는 시간별로 정렬된 목록 보기에 로드됩니다. 각 이벤트에는 추가 정보를 제공하는 상세 보기가 있습니다. SDK 구성, 데이터 요소, 공유 상태 및 SDK 확장 버전을 검색할 수 있는 추가 보기도 제공됩니다. 제품 설명서에서 [보증](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html?lang=ko)에 대해 자세히 알아보세요.


## 전제 조건

* SDK를 설치 및 구성한 앱을 설정했습니다.

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* 조직에 액세스 권한이 있는지 확인합니다(없는 경우 요청).
* 기본 URL을 설정합니다.
* 필요한 iOS 관련 코드를 추가합니다.
* 세션에 연결합니다.

## 액세스 확인

조직에서 Assurance에 액세스할 수 있는지 확인합니다. 사용자는 Adobe Experience Platform의 프로필에 추가되어야 합니다. 자세한 내용은 Assurance 가이드의 [사용자 액세스](https://experienceleague.adobe.com/docs/experience-platform/assurance/user-access.html?lang=ko)를 참조하십시오.

## 구현

이전 단원에서 완료한 일반 [SDK 설치](install-sdks.md) 외에도 iOS에서는 앱에 대한 Assurance 세션을 시작하려면 다음을 추가해야 합니다.

1. Xcode의 프로젝트 탐색기에서 **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL SceneDelegate]**(으)로 이동합니다.

1. `func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>`에 다음 코드를 추가합니다.

   ```swift
   // Called when the app in background is opened with a deep link.
   if let deepLinkURL = URLContexts.first?.url {
       // Start the Assurance session
       Assurance.startSession(url: deepLinkURL)
   }
   ```

   이 코드는 앱이 백그라운드에 있고 딥링크를 사용하여 열리면 보증 세션을 시작합니다.

자세한 내용은 [여기](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/api-reference/){target="_blank"}를 참조하십시오.



## 번들 식별자 정의

앱에 고유한 번들 식별자를 제공해야 합니다.

1. Xcode에서 프로젝트를 엽니다.
1. Project 탐색기에서 **[!DNL Luma]**&#x200B;을(를) 선택합니다.
1. **[!DNL Luma]** 대상을 선택하십시오.
1. **서명 및 기능** 탭을 선택합니다.
1. **[!UICONTROL 번들 식별자]**&#x200B;를 정의합니다.

   >[!IMPORTANT]
   >
   >각 번들 식별자가 고유해야 하므로 _unique_ 번들 식별자를 사용하고 `com.adobe.luma.tutorial.swiftui` 번들 식별자를 바꾸십시오. 일반적으로 `com.organization.brand.uniqueidentifier`과(와) 같은 번들 ID 문자열에 역방향 DNS 형식을 사용합니다. 이 자습서의 완성된 버전은 `com.adobe.luma.tutorial.swiftui`을(를) 사용합니다.


   ![Xcode 서명 기능](assets/xcode-signing-capabilities.png){zoomable="yes"}


## 기본 URL 설정

1. Xcode에서 프로젝트로 이동합니다.
1. Project 탐색기에서 **[!DNL Luma]**&#x200B;을(를) 선택합니다.
1. **[!DNL Luma]** 대상을 선택하십시오.
1. **정보** 탭을 선택합니다.
1. 기본 URL을 추가하려면 **URL 형식**(으)로 아래로 스크롤하고 **+** 단추를 선택하세요.
1. **Identifier**&#x200B;을(를) 선택한 번들 식별자로 설정하고 **URL 체계**&#x200B;를(를) 선택하십시오.

   ![보증 url](assets/assurance-url-type.png)

   >[!IMPORTANT]
   >
   >각 번들 식별자가 고유해야 하므로 _unique_ 번들 식별자를 사용하고 `com.adobe.luma.tutorial.swiftui` 번들 식별자를 바꾸십시오. 일반적으로 `com.organization.brand.uniqueidentifier`과(와) 같은 번들 ID 문자열에 역방향 DNS 형식을 사용합니다. [번들 식별자 정의](#define-bundle-identifier)에서 사용한 것과 동일한 번들 식별자를 사용할 수 있습니다.<br/>마찬가지로 고유한 URL 체계를 사용하고 이미 제공된 `lumatutorialswiftui`을(를) 고유한 URL 체계로 바꾸십시오.

iOS의 URL 체계에 대해 자세히 알아보려면 [Apple의 설명서](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target="_blank"}를 검토하십시오.

보증은 브라우저 또는 QR 코드를 통해 URL을 열어 작동합니다. 해당 URL은 앱을 열고 추가 매개 변수를 포함하는 기본 URL로 시작합니다. 이러한 고유한 매개 변수는 세션을 연결하는 데 사용됩니다.


## 세션에 연결

Xcode에서:

1. ![재생](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg)을 사용하여 시뮬레이터 또는 Xcode의 실제 장치에서 앱을 빌드하거나 다시 빌드하고 실행합니다.

   >[!TIP]
   >
   >선택적으로, 특히 예상치 못한 결과가 표시될 때 빌드를 &#39;정리&#39;할 수 있습니다. 이렇게 하려면 Xcode **[!UICONTROL Product]** 메뉴에서 **[!UICONTROL 빌드 폴더 정리...]**&#x200B;를 선택하십시오.


1. **[!UICONTROL Luma 앱에서 사용자의 위치를 사용할 수 있도록 허용]** 대화 상자에서 **[!UICONTROL 앱을 사용하는 동안 허용]**&#x200B;을 선택합니다.

   <img src="assets/geolocation-permissions.png" width="300">

1. **[!UICONTROL &quot;Luma 앱&quot;에서 알림을 보내려고 합니다]** 대화 상자에서 **[!UICONTROL 허용]**&#x200B;을 선택합니다.

   <img src="assets/notification-permissions.png" width="300">

1. 앱에서 활동을 추적할 수 있도록 하려면 **[!UICONTROL 계속...]**&#x200B;을(를) 선택하십시오.

   <img src="assets/tracking-continue.png" width="300">

1. **[!UICONTROL 다른 회사의 앱과 웹 사이트에서 사용자의 활동을 추적할 수 있도록 &quot;Luma 앱&quot; 허용]** 대화 상자에서 **[!UICONTROL 허용]**&#x200B;을 선택합니다.

   <img src="assets/tracking-allow.png" width="300">


브라우저에서:

1. 데이터 수집 UI로 이동합니다.
1. 왼쪽 레일에서 **[!UICONTROL 보증]**&#x200B;을 선택합니다.
1. **[!UICONTROL 세션 만들기]**&#x200B;를 선택합니다.
1. **[!UICONTROL 시작]**&#x200B;을 선택하세요.
1. `Luma Mobile App Session`과(와) 같은 **[!UICONTROL 세션 이름]**&#x200B;과(와) Xcode에 입력한 URL 체계인 **[!UICONTROL 기본 URL]**&#x200B;을(를) 제공한 다음 `://`을(를) 제공하십시오(예: `lumatutorialswiftui://`).
1. **[!UICONTROL 다음]**&#x200B;을 선택합니다.
   ![확인 세션 만들기](assets/assurance-create-session.png)
1. **[!UICONTROL 새 세션 만들기]** 모달 대화 상자에서:

   실제 장치를 사용하는 경우:

   * **[!UICONTROL QR 코드 스캔]**&#x200B;을 선택합니다. 앱을 열려면 실제 장치의 카메라를 사용하여 QR 코드를 스캔하고 링크를 탭합니다.

     ![보증 qa 코드](assets/assurance-qr-code.png)

   시뮬레이터를 사용하는 경우:

   1. **[!UICONTROL 링크 복사]**&#x200B;를 선택합니다.
   1. ![복사](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)를 사용하여 딥링크를 복사하고 딥링크를 사용하여 시뮬레이터에서 Safari가 있는 앱을 엽니다.

      ![보증 복사 링크](assets/assurance-copy-link.png)

1. 앱이 로드되면 7단계에 표시된 PIN을 입력하라는 모달 대화 상자가 표시됩니다.

   <img src="assets/assurance-enter-pin.png" width="300">

   PIN을 입력하고 **[!UICONTROL 연결]**&#x200B;을 선택하세요.


1. 연결에 성공하면 다음을 볼 수 있습니다.
   * 앱 위에 떠 있는 보증 아이콘.

     <img src="assets/assurance-modal.png" width="300">

   * Assurance UI에서 제공되는 Experience Cloud 업데이트로, 다음을 표시합니다.

      1. 앱에서 들어오는 경험 이벤트.
      1. 선택한 이벤트에 대한 세부 정보.
      1. 장치 및 타임라인.

         ![보증 이벤트](assets/assurance-events.png)

문제가 발생하면 [기술](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/){target="_blank"} 및 [일반 설명서](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html?lang=ko){target="_blank"}를 검토하십시오.


## 확장 확인

앱에서 최신 확장을 사용하는지 확인하려면:

1. **[!UICONTROL 구성]**&#x200B;을 선택합니다.

1. ![123](https://spectrum.adobe.com/static/icons/workflow_18/Smock_123_18_N.svg) **[!UICONTROL 확장 버전]**&#x200B;에 대해 ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg)를 선택하십시오.

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

   ![확장 버전 구성](assets/assurance-configure-extension-versions.png)

1. ![123](https://spectrum.adobe.com/static/icons/workflow_18/Smock_123_18_N.svg) **[!UICONTROL 확장 버전]**&#x200B;을 선택하여 사용 가능한 최신 확장과 앱 버전에서 사용되는 확장에 대한 개요를 확인하세요.

   ![확장 버전](assets/assurance-extension-versions.png)

1. 확장 버전(예: **[!UICONTROL 메시징]** 및 **[!UICONTROL 최적화]**)을 업데이트하려면 **[!UICONTROL 패키지 종속성]**(예: **[!UICONTROL AEPMessaging]**)에서 패키지(확장)를 선택하고 컨텍스트 메뉴에서 **[!UICONTROL 패키지 업데이트]**&#x200B;를 선택합니다. Xcode는 패키지 종속성을 업데이트합니다.


>[!NOTE]
>
>Xcode에서 확장(패키지)을 업데이트했으면 현재 세션을 닫았다가 삭제하고 [세션에 연결](#connecting-to-a-session) 및 [확장 확인](#verify-extensions)의 모든 단계를 반복하여 Assurance가 새 Assurance 세션에서 올바른 확장을 제대로 보고하는지 확인하십시오.





>[!SUCCESS]
>
>이제 자습서의 나머지 부분에서 Assurance를 사용하도록 앱을 설정했습니다.
>
>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하고 싶거나 향후 콘텐츠에 대한 제안이 있는 경우 이 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=ko)에서 공유하십시오.


다음: **[동의 구현](consent.md)**
