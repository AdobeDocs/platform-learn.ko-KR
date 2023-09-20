---
title: Assurance 설정
description: 모바일 앱에서 Assurance 확장을 구현하는 방법을 알아봅니다.
feature: Mobile SDK,Assurance
hide: true
source-git-commit: a2788110b1c43d24022672bb5ba0f36af66d962b
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 9%

---

# Assurance 설정

모바일 앱에서 Adobe Experience Platform Assurance를 설정하는 방법을 알아봅니다.

Assurance는 정식적으로 프로젝트 그리폰이라고 하며, 모바일 앱에서 데이터를 수집하거나 경험을 제공하는 방법을 검사, 증명, 시뮬레이션 및 확인하는 데 도움이 되도록 설계되었습니다.

Assurance를 통해 Adobe Experience Platform Mobile SDK에서 생성된 원시 SDK 이벤트를 검사할 수 있습니다. SDK에서 수집한 모든 이벤트를 검사할 수 있습니다. SDK 이벤트는 시간별로 정렬된 목록 보기에 로드됩니다. 각 이벤트에는 추가 정보를 제공하는 상세 보기가 있습니다. SDK 구성, 데이터 요소, 공유 상태 및 SDK 확장 버전을 검색할 수 있는 추가 보기도 제공됩니다. 에 대해 자세히 알아보기 [보증](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html) 를 참조하십시오.


## 전제 조건

* SDK를 설치 및 구성한 앱을 설정했습니다.

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* 조직에 액세스 권한이 있는지 확인합니다(없는 경우 요청).
* 기본 URL을 설정합니다.
* 필요한 iOS 관련 코드를 추가합니다.
* 세션에 연결.

## 액세스 확인

조직에서 Assurance에 액세스할 수 있는지 확인합니다. 사용자는 Adobe Experience Platform의 프로필에 추가되어야 합니다. 다음을 참조하십시오 [사용자 액세스](https://experienceleague.adobe.com/docs/experience-platform/assurance/user-access.html?lang=en) 자세한 내용은 Assurance 안내서 를 참조하십시오.

## 구현

일반에 더해서 [SDK 설치](install-sdks.md), 이전 단원에서 을(를) 완료했습니다. iOS에서도 앱의 Assurance 세션을 시작하려면 다음 항목을 추가해야 합니다.

1. 다음으로 이동 **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL SceneDelegate]** Xcode의 Project navigator에서.

1. `func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>`에 다음 코드를 추가합니다.

   ```swift
   // Called when the app in background is opened with a deep link.
   if let deepLinkURL = URLContexts.first?.url {
       // Start the Assurance session
       Assurance.startSession(url: deepLinkURL)
   }
   ```

   이 코드는 앱이 백그라운드에 있고 딥링크를 사용하여 열리면 보증 세션을 시작합니다.

추가 정보를 찾을 수 있음 [여기](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/api-reference/){target="_blank"}.

## 서명

Xcode에서 응용 프로그램을 처음 실행하기 전에 서명을 업데이트하십시오.

1. Xcode에서 프로젝트를 엽니다.
1. 선택 **[!DNL Luma]** 프로젝트 탐색기를 참조하십시오.
1. 다음 항목 선택 **[!DNL Luma]** 타겟.
1. 다음 항목 선택 **서명 및 기능** 탭.
1. 구성 **[!UICONTROL 서명 자동 관리]**, **[!UICONTROL 팀]**, 및 **[!UICONTROL 번들 식별자]**&#x200B;또는 특정 Apple 개발 프로비저닝 세부 정보를 사용하십시오.

   >[!IMPORTANT]
   >
   >각 번들 식별자는 고유해야 하므로 시작 프로젝트에 이미 입력된 기본값과 다른 고유한 번들 식별자를 선택해야 합니다.


   ![Xcode 서명 기능](assets/xcode-signing-capabilities.png){zoomable=&quot;yes&quot;}

## 기본 URL 설정

1. Xcode에서 프로젝트로 이동합니다.
1. 선택 **[!DNL Luma]** 프로젝트 탐색기를 참조하십시오.
1. 다음 항목 선택 **[!DNL Luma]** 타겟.
1. 다음 항목 선택 **정보** 탭.
1. 기본 URL을 추가하려면 아래로 스크롤하여 **URL 유형** 및 선택 **+** 단추를 클릭합니다.
1. 설정 **식별자** 을(를) 구성하는 번들 식별자 [서명](#signing) (예 `com.adobe.luma.tutorial.swiftui`) 및 a 설정 **URL 체계**, 예 `lumatutorialswiftui`.

   ![보증 url](assets/assurance-url-type.png)

iOS의 URL 체계에 대해 자세히 알아보려면 을 검토하십시오. [Apple 설명서](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target="_blank"}.

보증은 브라우저 또는 QR 코드를 통해 URL을 열어 작동합니다. 해당 URL은 앱을 열고 추가 매개 변수를 포함하는 기본 URL로 시작합니다. 이러한 고유한 매개 변수는 세션을 연결하는 데 사용됩니다.


## 세션에 연결

1. 시뮬레이터 또는 연결된 물리적 장치에서 애플리케이션을 실행합니다.
1. 선택 **[!UICONTROL 보증]** (데이터 수집 UI의 왼쪽 레일)
1. 선택 **[!UICONTROL 세션 만들기]**.
1. 선택 **[!UICONTROL 시작]**.
1. 다음을 제공합니다. **[!UICONTROL 세션 이름]** 과 같은 `Luma Mobile App Session` 및 **[!UICONTROL 기본 URL]**: Xcode에 입력한 URL 체계, 그 뒤에 오는 `://` 예: `lumatutorialswiftui://`
1. **[!UICONTROL 다음]**을 선택합니다.
   ![보증 생성 세션](assets/assurance-create-session.png)
1. 다음에서 **[!UICONTROL 새 세션 만들기]** 모달 대화 상자:

   실제 장치를 사용하는 경우:

   * 선택 **[!UICONTROL QR 코드 스캔]**. 실제 장치에서 카메라를 사용하여 QR 코드를 스캔하고 링크를 탭하여 앱을 엽니다.

     ![보증 qa 코드](assets/assurance-qr-code.png)

   시뮬레이터를 사용하는 경우:

   1. 선택 **[!UICONTROL 링크 복사]**.
   1. 다음을 사용하여 딥링크 복사 ![복사](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)  딥 링크를 사용하여 시뮬레이터에서 Safari로 앱을 엽니다.
      ![보증 복사 링크](assets/assurance-copy-link.png)

1. 앱이 로드되면 7단계에 표시된 PIN을 입력하라는 모달 대화 상자가 표시됩니다.

   <img src="assets/assurance-enter-pin.png" width="300">

   PIN을 입력하고 선택 **[!UICONTROL 연결]**.


1. 연결에 성공하면 다음을 볼 수 있습니다.
   * 앱 위에 떠 있는 보증 아이콘.

     <img src="assets/assurance-modal.png" width="300">

   * Assurance UI에서 제공되는 Experience Cloud 업데이트로, 다음을 표시합니다.

      1. 앱에서 들어오는 경험 이벤트.
      1. 선택한 이벤트에 대한 세부 정보.
      1. 장치 및 타임라인.

         ![보증 이벤트](assets/assurance-events.png)

문제가 발생하는 경우 다음을 검토하십시오. [기술](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/){target="_blank"} and [general documentation](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html){target="_blank"}.

>[!SUCCESS]
>
>이제 자습서의 나머지 부분에서 Assurance를 사용하도록 앱을 설정했습니다.<br/>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나, 일반적인 피드백을 공유하거나, 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오. [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)


다음: **[동의](consent.md)**
