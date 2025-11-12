---
title: 모바일 앱에서 Adobe Experience Cloud 구현 자습서
description: Adobe Experience Cloud 모바일 애플리케이션을 구현하는 방법을 알아봅니다. 이 튜토리얼에서는 샘플 Swift 또는 Android 앱에서의 Experience Cloud 애플리케이션 구현을 안내합니다.
recommendations: noDisplay,catalog
last-substantial-update: 2023-11-29T00:00:00Z
exl-id: daff4214-d515-4fad-a224-f7589b685b55
source-git-commit: 342bb7efbe868622c4bc08e02568bce948fed61c
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 1%

---

# 모바일 앱에서 Adobe Experience Cloud 구현 자습서

Adobe Experience Platform Mobile SDK을 사용하여 모바일 앱에서 Adobe Experience Cloud 애플리케이션을 구현하는 방법을 알아봅니다.

Experience Platform Mobile SDK은 Adobe Experience Cloud 고객이 Adobe Experience Platform Edge Network을 통해 Adobe 애플리케이션 및 서드파티 서비스와 모두 상호 작용할 수 있도록 하는 클라이언트측 SDK입니다. 자세한 내용은 [Adobe Experience Platform Mobile SDK 설명서](https://developer.adobe.com/client-sdks/home/)를 참조하세요.

![아키텍쳐](assets/architecture.png){zoomable="yes"}


이 튜토리얼에서는 Luma라는 샘플 앱에서 Platform Mobile SDK을 구현하는 과정을 안내합니다. Luma 앱에는 사실적인 구현을 구축할 수 있는 기능이 있습니다. 이 자습서를 완료한 후에는 자체 모바일 앱에서 Experience Platform Mobile SDK을 통해 모든 마케팅 솔루션 구현을 시작할 준비가 되어 있어야 합니다.

단원은 다음을 위해 설계되었습니다.

* iOS, Swift 프로그래밍 언어 및 SwiftUI 프레임워크 사용.
* Android, Kotlin 및 Java 프로그래밍 언어 및 JetPack 작성 프레임워크 사용.

이 자습서를 완료하면 다음 작업을 수행할 수 있습니다.

* 표준 및 사용자 정의 필드 그룹을 사용하여 스키마를 만듭니다.
* 데이터 스트림을 설정합니다.
* 모바일 태그 속성을 구성합니다.
* Experience Platform 데이터 세트를 설정합니다(선택 사항).
* 앱에 태그 확장 설치 및 구현
* Experience Cloud 매개 변수를 [webview](web-views.md)에 올바르게 전달합니다.
* [Adobe Experience Platform Assurance](assurance.md)을(를) 사용하여 구현의 유효성을 검사합니다.
* 다음 Adobe Experience Cloud 애플리케이션 또는 확장을 추가합니다.
   * [Adobe Experience Platform Edge (XDM)](events.md)
   * [라이프사이클 데이터 수집](lifecycle-data.md)
   * [동의](consent.md)
   * [ID](identity.md)
   * [프로필](profile.md)
   * [장소](places.md)
   * [Analytics](analytics.md)
   * [Experience Platform](platform.md)
   * [Journey Optimizer을 사용한 푸시 메시지](journey-optimizer-push.md)
   * [Journey Optimizer을 사용한 인앱 메시지](journey-optimizer-inapp.md)
   * [Journey Optimizer을 통한 의사 결정 관리](journey-optimizer-offers.md)
   * [Target](target.md)


>[!NOTE]
>
>[웹 SDK](../tutorial-web-sdk/overview.md)에 유사한 다중 솔루션 자습서를 사용할 수 있습니다.

## 권한

이 단원들에서는 사용자에게 Adobe ID와 연습을 완료하는 데 필요한 사용자 수준 권한이 있다고 가정합니다. 그렇지 않은 경우 Adobe 관리자에게 연락하여 액세스 권한을 요청해야 합니다.

* 데이터 수집에서 다음을 수행해야 합니다.
   * **[!UICONTROL 플랫폼]**—권한 항목 **[!UICONTROL 모바일]**
   * **[!UICONTROL 속성 권한]**—권한 항목으로서 **[!UICONTROL 개발]**, **[!UICONTROL 승인]**, **[!UICONTROL 게시]**, **[!UICONTROL 확장 관리]** 및 **[!UICONTROL 환경 관리]**&#x200B;를 수행할 수 있습니다.
   * **[!UICONTROL 회사 권한]**—**[!UICONTROL 속성 관리]**&#x200B;에 대한 권한 항목

     태그 권한에 대한 자세한 내용은 제품 설명서에서 [태그에 대한 사용자 권한](https://experienceleague.adobe.com/en/docs/experience-platform/tags/admin/user-permissions){target="_blank"}을 참조하세요.
* Experience Platform에서 다음을 수행해야 합니다.
   * **[!UICONTROL 데이터 모델링]**—스키마를 관리하고 볼 수 있는 권한 항목입니다.
   * **[!UICONTROL Identity Management]**—id 네임스페이스를 관리하고 볼 수 있는 권한 항목입니다.
   * **[!UICONTROL 데이터 수집]**—데이터 스트림을 관리하고 볼 수 있는 권한 항목입니다.

   * Real-Time CDP, Journey Optimizer 또는 Customer Journey Analytics과 같은 플랫폼 기반 애플리케이션의 고객이고 관련 단원을 수행하려는 경우 다음 사항도 수행해야 합니다.
      * **[!UICONTROL 데이터 관리]**—데이터 집합을 관리하고 볼 수 있는 권한 항목입니다.
      * 이 자습서에 사용할 수 있는 개발 **샌드박스**.

   * Journey Optimizer 단원의 경우 **푸시 알림 서비스**&#x200B;를 구성하고 **앱 표면**, **여정**, **메시지** 및 **메시지 사전 설정**&#x200B;을 만들 수 있는 권한이 필요합니다. 또한 의사 결정 관리의 경우 **권한 수준**&#x200B;에 설명된 대로 **오퍼를 관리** 및 [의사 결정](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/access-control/high-low-permissions)할 수 있는 적절한 권한이 필요합니다.

* Adobe Analytics의 경우 이 자습서를 완료하는 데 사용할 수 있는 **보고서 세트**&#x200B;를 알고 있어야 합니다.

* Adobe Target의 경우 활동을 만들고 활성화할 수 있는 권한이 있어야 합니다.


>[!NOTE]
>
>이 자습서의 일부로 스키마, 데이터 세트, ID 등을 만듭니다. 한 샌드박스에서 여러 사람이 이 자습서를 진행하는 경우 이러한 개체를 만들 때 이름 지정 규칙의 일부로 ID를 추가하거나 앞에 추가하는 것이 좋습니다. 예를 들어 만들라는 지침이 있는 개체의 이름에 ` - <your name or initials>`을(를) 추가합니다.

## 버전 기록

* 2025년 9월 9일:
   * 함께 제공되는 지침이 포함된 앱의 Android 버전.
   * Journey Optimizer의 앱 표면 및 캠페인 기능 변경 사항에 대한 업데이트입니다.
* 2023년 11월 29일: 새로운 샘플 앱과 인앱 메시지, 의사 결정 관리 및 Adobe Target에 대한 새로운 단원으로 주요 검토.
* 2022년 3월 9일: 최초 게시

## Luma 앱 다운로드

>[!BEGINTABS]

>[!TAB iOS]

두 가지 버전의 샘플 앱을 다운로드할 수 있습니다. 두 버전 모두 [GitHub](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App)에서 다운로드/복제할 수 있습니다. 다음 두 개의 폴더를 찾습니다.

1. [시작](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}: 이 자습서에서 실습형 연습을 완료하는 데 필요한 대부분의 Experience Platform Mobile SDK 코드에 대해 코드가 없거나 자리 표시자 코드가 있는 프로젝트.
1. [완료](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}: 전체 구현이 참조되는 버전입니다.

플랫폼으로 iOS, 프로그래밍 언어로 [!DNL Swift], UI 프레임워크로 [!DNL SwiftUI], IDE(통합 개발 환경)로 [!DNL Xcode]을(를) 사용합니다. 그러나 설명된 구현 개념의 대부분은 다른 개발 플랫폼에 대해 유사합니다. 많은 사람들이 이미 이전의 iOS 및 Swift(UI) 개발 경험이 거의 또는 전혀 없는 상태에서 이 자습서를 성공적으로 완료했습니다. 전문가가 아니어도 단원을 완료할 수는 있지만, 코드를 읽고 이해할 수 있으면 단원을 최대한 활용할 수 있습니다.

App Store에서 최종 프로덕션 버전의 앱을 다운로드할 수 있습니다.

[![다운로드](assets/download-app.svg)](https://apps.apple.com/us/app/luma-app/id6466588487)

>[!TAB Android]

두 가지 버전의 샘플 앱을 다운로드할 수 있습니다. 두 버전 모두 [GitHub](https://github.com/adobe/Luma-Android)에서 다운로드하거나 복제할 수 있습니다. 다음 두 개의 폴더를 찾습니다.

1. [시작](https://github.com/adobe/Luma-Android){target="_blank"}: 이 자습서에서 실습형 연습을 완료하는 데 필요한 대부분의 Experience Platform Mobile SDK 코드에 대해 코드가 없거나 자리 표시자 코드가 있는 프로젝트.
1. [완료](https://github.com/adobe/Luma-Android){target="_blank"}: 전체 구현이 참조되는 버전입니다.

플랫폼으로 Android, 프로그래밍 언어로 [!DNL Kotlin]+[!DNL Java], UI 프레임워크로 [!DNL JetPack Compose], IDE(통합 개발 환경)로 [!DNL Android Studio]을(를) 사용합니다. 그러나 설명된 구현 개념의 대부분은 다른 개발 플랫폼에 대해 유사합니다. 많은 사람들이 이미 이전의 Android / Kotlin+Java / JetPack 작성 경험이 거의 없는 상태에서 이 자습서를 성공적으로 완료했습니다. 전문가가 아니어도 단원을 완료할 수는 있지만, 코드를 읽고 이해할 수 있으면 단원을 최대한 활용할 수 있습니다.

원하는 경우 Google Play에서 [만들어진 버전에 대한 테스트에 참여](https://play.google.com/apps/internaltest/4700642199234438150)할 수 있습니다.


>[!ENDTABS]

그럼 시작해 보겠습니다!

>[!SUCCESS]
>
>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하고 싶거나 향후 콘텐츠에 대한 제안이 있는 경우 이 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)에서 공유하십시오.

다음: **[XDM 스키마 만들기](create-schema.md)**
