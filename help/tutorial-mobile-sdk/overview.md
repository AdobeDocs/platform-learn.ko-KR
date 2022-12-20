---
title: 모바일 앱에서 Adobe Experience Cloud 구현 튜토리얼 개요
description: Adobe Experience Cloud 모바일 애플리케이션을 구현하는 방법을 알아봅니다. 이 자습서에서는 샘플 Swift 앱에서의 Experience Cloud 애플리케이션 구현을 안내합니다.
recommendation: noDisplay,catalog
exl-id: daff4214-d515-4fad-a224-f7589b685b55
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 10%

---

# 모바일 앱에서 Adobe Experience Cloud 구현 튜토리얼

Adobe Experience Platform Mobile SDK를 사용하여 모바일 앱에서 Adobe Experience Cloud 애플리케이션을 구현하는 방법을 알아봅니다.

Experience Platform Mobile SDK는 Adobe Experience Cloud 고객이 Adobe Experience Platform Edge 네트워크를 통해 Adobe 애플리케이션 및 타사 서비스와 상호 작용할 수 있는 클라이언트측 SDK입니다. 자세한 내용은 [Adobe Experience Platform Mobile SDK 설명서](https://aep-sdks.gitbook.io/docs/) 를 참조하십시오.

![빌드 설정](assets/data-collection-mobile-sdk.png)


이 자습서에서는 Luma라는 샘플 소매 앱에서 Platform Mobile SDK의 구현을 안내합니다. 다음 [Luma 앱](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) 에는 사실적인 구현을 만들 수 있는 기능이 있습니다. 이 자습서를 완료하고 나면 모바일 앱에서 Platform Mobile SDK를 통해 모든 마케팅 솔루션 구현을 시작할 수 있습니다.

이 단원은 iOS을 위해 설계되고 Swift로 작성되지만, 많은 개념들이 Android™에도 적용됩니다.

이 자습서를 완료하면 다음 작업을 수행할 수 있습니다.

* 표준 및 사용자 지정 필드 그룹을 사용하여 스키마를 만듭니다.
* 데이터 스트림을 설정합니다.
* 모바일 태그 속성을 구성합니다.
* Experience Platform 데이터 세트를 설정합니다(선택 사항).
* 앱에 태그 확장 을 설치하고 구현합니다.
* 다음 Adobe Experience Cloud 애플리케이션/확장을 추가합니다.
   * [Adobe Experience Platform Edge(XDM)](events.md)
   * [라이프사이클 데이터 수집](lifecycle-data.md)
   * [XDM을 통한 Adobe Analytics](analytics.md)
   * [동의](consent.md)
   * [신원](identity.md)
   * [프로필](profile.md)
   * [Adobe Experience Platform](platform.md)
   * [Journey Optimizer을 사용한 푸시 메시지](journey-optimizer-push.md)
* Experience Cloud 매개 변수를 올바르게 [webview](web-views.md).
* 를 사용하여 구현의 유효성 검사 [Adobe Experience Platform 보증](assurance.md).

>[!NOTE]
>
>에 대해 유사한 다중 솔루션 자습서를 사용할 수 있습니다 [웹 SDK](../tutorial-web-sdk/overview.md).

## 전제 조건

이 단원들에서는 사용자에게 Adobe ID와 연습을 완료하는 데 필요한 권한이 있다고 가정합니다. 그렇지 않은 경우 Adobe 관리자에게 연락하여 액세스 권한을 요청해야 합니다.

* 데이터 수집에서는 다음을 수행해야 합니다.
   * **[!UICONTROL 플랫폼]**—권한 항목 **[!UICONTROL 모바일]**
   * **[!UICONTROL 속성 권한]**—권한 항목을 **[!UICONTROL 개발]**, **[!UICONTROL 승인]**, **[!UICONTROL 게시]**, **[!UICONTROL 확장 관리]**, 및 **[!UICONTROL 환경 관리]**.
   * **[!UICONTROL 회사 권한]**—권한 항목을 **[!UICONTROL 속성 관리]** 그리고 선택적 푸시 메시지 단원을 완료하는 경우, **[!UICONTROL 앱 구성 관리]**

      태그 권한에 대한 자세한 내용은 [태그의 사용자 권한](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=ko-KR)제품 설명서의 {target=&quot;_blank&quot;}.
* Experience Platform에서 다음을 수행해야 합니다.
   * **[!UICONTROL 데이터 모델링]**—스키마를 관리하고 볼 수 있는 권한 항목입니다.
   * **[!UICONTROL Identity Management]**- ID 네임스페이스를 관리하고 볼 수 있는 권한 항목입니다.
   * **[!UICONTROL 데이터 수집]**—데이터 저장소를 관리하고 볼 수 있는 권한 항목입니다.

   * Real-Time CDP, Journey Optimizer 또는 Customer Journey Analytics과 같은 플랫폼 기반 애플리케이션의 고객인 경우, 다음과 같은 내용이 있어야 합니다.
      * **[!UICONTROL 데이터 관리]**—데이터 세트를 관리하고 보기 위한 권한 항목으로서, _선택적 플랫폼 연습_ ( 플랫폼 기반 애플리케이션에 대한 라이센스가 필요).
      * 개발 **샌드박스** 이 자습서에 사용할 수 있는 항목입니다.
* Adobe Analytics의 경우 **보고서 세트** 을 사용하여 이 자습서를 완료할 수 있습니다.

모든 Experience Cloud 고객은 Mobile SDK를 배포하는 데 필요한 기능에 액세스할 수 있어야 합니다.

또한, 사용자가 [!DNL Swift]. 전문가가 될 필요는 없지만 코드를 읽고 이해할 수 있으면 단원을 최대한 활용할 수 있습니다.

## Luma 앱 다운로드

두 버전의 샘플 앱을 다운로드할 수 있습니다.

1. [Empty](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target=&quot;_blank&quot;} - 이 자습서에서 실습 연습을 완료하려면 Experience Cloud 코드가 없는 버전입니다.
1. [전체 구현](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target=&quot;_blank&quot;} - 참조를 위한 전체 Experience Cloud 구현이 있는 버전입니다.

그럼 시작해 보겠습니다!


다음: **[XDM 스키마 만들기](create-schema.md)**

>[!NOTE]
>
>Adobe Experience Platform Mobile SDK에 대한 학습에 시간을 내주셔서 감사합니다. 질문이 있거나 일반 피드백을 공유하거나 향후 컨텐츠에 대한 제안 사항이 있는 경우 해당 정보를 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)