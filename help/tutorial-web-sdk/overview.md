---
title: Web SDK 튜토리얼을 통해 Adobe Experience Cloud 구현
description: Adobe Experience Platform Web SDK를 사용하여 Experience Cloud 애플리케이션을 구현하는 방법을 알아봅니다.
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: 7ccbaaf4db43921f07c971c485e1460a1a7f0334
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 7%

---

# Web SDK 튜토리얼을 통해 Adobe Experience Cloud 구현

Adobe Experience Platform Web SDK를 사용하여 Experience Cloud 애플리케이션을 구현하는 방법을 알아봅니다.

Experience Platform Web SDK은 Adobe Experience Cloud 고객이 Adobe Experience Platform Edge Network을 통해 Adobe 애플리케이션 및 서드파티 서비스와 모두 상호 작용할 수 있도록 하는 클라이언트측 JavaScript 라이브러리입니다. 자세한 내용은 [Adobe Experience Platform Web SDK 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/edge/home)를 참조하십시오.

![Experience Platform 웹 SDK 아키텍처](assets/dc-websdk.png)

이 튜토리얼에서는 샘플 소매 웹 사이트인 Luma에서 Platform Web SDK을 구현하는 과정을 안내합니다. [Luma 사이트](https://luma.enablementadobe.com/content/luma/us/en.html)에는 사실적인 구현을 만들 수 있는 풍부한 데이터 레이어와 기능이 있습니다. 이 자습서에서는 다음 작업을 수행합니다.

* Luma 웹 사이트에 대한 Platform Web SDK 구현을 사용하여 자체 계정에서 고유한 태그 속성을 만듭니다.
* 데이터스트림, 스키마 및 ID 네임스페이스 등 웹 SDK 구현에 대한 모든 데이터 수집 기능을 구성합니다.
* 다음 Adobe Experience Cloud 애플리케이션을 추가합니다.
   * **[Adobe Experience Platform](setup-experience-platform.md)**(및 Adobe Real-Time Customer Data Platform, Adobe Journey Optimizer, Adobe Customer Journey Analytics과 같은 플랫폼에 구축된 애플리케이션)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**
* Web SDK에서 수집한 데이터를 Adobe이 아닌 대상으로 보내려면 이벤트 전달을 구현합니다.
* Experience Platform Debugger 및 Assurance을 사용하여 자체 Platform 웹 SDK 구현의 유효성을 검사합니다.

이 자습서를 완료한 후에는 자체 웹 사이트에서 Platform Web SDK을 통해 모든 마케팅 애플리케이션 구현을 시작할 준비가 되어 있어야 합니다.


>[!NOTE]
>
>[모바일 SDK](../tutorial-mobile-sdk/overview.md)에서도 유사한 다중 솔루션 자습서를 사용할 수 있습니다.

## 전제 조건

모든 Experience Cloud 고객은 Platform Web SDK을 사용할 수 있습니다. Web SDK을 사용하기 위해 Real-Time Customer Data Platform 또는 Journey Optimizer과 같은 플랫폼 기반 애플리케이션에 라이선스를 부여할 필요는 없습니다.

이 단원들에서는 Adobe 계정과 단원을 완료하는 데 필요한 권한이 있다고 가정합니다. 그렇지 않은 경우 회사의 Experience Cloud 관리자에게 연락하여 액세스 권한을 받아야 합니다.

* **데이터 수집**&#x200B;의 경우 다음이 있어야 합니다.
   * **[!UICONTROL 플랫폼]**—**[!UICONTROL 웹]** 및 라이선스가 있는 경우 **[!UICONTROL Edge]**&#x200B;에 대한 권한
   * **[!UICONTROL 속성 권한]**—권한: **[!UICONTROL 승인]**, **[!UICONTROL 개발]**, **[!UICONTROL 속성 편집]**, **[!UICONTROL 환경 관리]**, **[!UICONTROL 확장 관리]** 및 **[!UICONTROL 게시]**,
   * **[!UICONTROL 회사 권한]**—**[!UICONTROL 속성 관리]**&#x200B;에 대한 권한

     태그 권한에 대한 자세한 내용은 [설명서](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/admin/user-permissions)를 참조하세요.

* **Experience Platform**&#x200B;의 경우 다음을 수행해야 합니다.

   * **기본 프로덕션**, **&quot;프로덕션&quot;** 샌드박스에 액세스합니다.
   * **[!UICONTROL 데이터 모델링]**&#x200B;에서 **[!UICONTROL 스키마 관리]** 및 **[!UICONTROL 스키마 보기]**&#x200B;에 액세스합니다.
   * **[!UICONTROL Identity Management]**&#x200B;에서 **[!UICONTROL ID 네임스페이스 관리]** 및 **[!UICONTROL ID 네임스페이스 보기]**&#x200B;에 액세스합니다.
   * **[!UICONTROL 데이터 수집]**&#x200B;에서 **[!UICONTROL 데이터 스트림 관리]** 및 **[!UICONTROL 데이터 스트림 보기]**&#x200B;에 액세스합니다.
   * 플랫폼 기반 응용 프로그램의 고객이고 [Experience Platform 설정](setup-experience-platform.md) 단원을 완료하려는 경우 다음과 같은 작업도 수행해야 합니다.
      * **개발** 샌드박스에 액세스합니다.
      * **[!UICONTROL 데이터 관리]** 및 **[!UICONTROL 프로필 관리]**&#x200B;의 모든 권한 항목:

     Real-Time CDP과 같은 플랫폼 기반 애플리케이션의 고객이 아닌 경우에도 모든 Experience Cloud 고객이 필요한 기능을 사용할 수 있어야 합니다.

     플랫폼 액세스 제어에 대한 자세한 내용은 [설명서](https://experienceleague.adobe.com/ko/docs/experience-platform/access-control/home)를 참조하세요.

* 선택적 **Adobe Analytics** 단원의 경우 보고서 세트 설정, 처리 규칙 및 Analysis Workspace[에 대한 &#x200B;](https://experienceleague.adobe.com/ko/docs/analytics/admin/admin-console/home)관리자 액세스 권한이 있어야 합니다.

* 선택적 **Adobe Target** 단원의 경우 [편집자 또는 승인자](https://experienceleague.adobe.com/ko/docs/target/using/administer/manage-users/enterprise/properties-overview#section_8C425E43E5DD4111BBFC734A2B7ABC80) 액세스 권한이 있어야 합니다.

* 선택적 **Audience Manager** 단원의 경우 트레이트, 세그먼트 및 대상을 만들고, 읽고, 쓸 수 있는 액세스 권한이 있어야 합니다. 자세한 내용은 [Audience Manager의 역할 기반 액세스 제어](https://experienceleague.adobe.com/ko/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control)에 대한 자습서를 참조하십시오.


>[!NOTE]
>
>사용자가 HTML 및 JavaScript과 같은 프론트엔드 개발 언어를 잘 알고 있다고 가정합니다. 이러한 언어에 대해 전문가가 될 필요는 없지만 코드를 읽고 이해할 수 있는 경우 이 자습서를 통해 자세한 내용을 확인할 수 있습니다.

## 업데이트

* 2024년 4월 24일: 변수 설정/업데이트 변수 추가, 개인화 및 분석 요청 분할 등 주요 업데이트, Journey Optimizer 단원

## Luma 웹 사이트 로드

자습서 중에 필요할 때마다 쉽게 로드할 수 있도록 별도의 브라우저 탭에서 [Luma 웹 사이트](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"}를 로드하고 책갈피로 지정합니다. 호스팅된 프로덕션 사이트를 로드할 수 있는 것 외에 Luma에 대한 추가 액세스 권한이 필요하지 않습니다.

[![Luma 웹 사이트](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"}

그럼 시작해 보겠습니다!

>[!NOTE]
>
>Adobe Experience Platform 웹 SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하고 싶거나 향후 콘텐츠에 대한 제안이 있는 경우 이 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=ko)에서 공유하십시오.
