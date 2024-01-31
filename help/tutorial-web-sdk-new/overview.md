---
title: Web SDK 튜토리얼을 통해 Adobe Experience Cloud 구현
description: Adobe Experience Platform Web SDK를 사용하여 Experience Cloud 애플리케이션을 구현하는 방법에 대해 알아봅니다.
recommendations: catalog, noDisplay
source-git-commit: 12e6e9d06ae0d6945c165032d89fd0f801d94ff2
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 4%

---

# Web SDK 튜토리얼을 통해 Adobe Experience Cloud 구현

Adobe Experience Platform Web SDK를 사용하여 Experience Cloud 애플리케이션을 구현하는 방법에 대해 알아봅니다.

Experience Platform Web SDK는 Adobe Experience Cloud 고객이 Adobe Experience Platform Edge Network를 통해 Adobe 애플리케이션 및 서드파티 서비스와 모두 상호 작용할 수 있도록 하는 클라이언트측 JavaScript 라이브러리입니다. 다음을 참조하십시오 [Adobe Experience Platform 웹 SDK 개요](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=ko-KR) 를 참조하십시오.

![Experience Platform 웹 SDK 아키텍처](assets/dc-websdk.png)

이 튜토리얼에서는 샘플 소매 웹 사이트인 Luma에서 Platform Web SDK를 구현하는 과정을 안내합니다. 다음 [Luma 사이트](https://luma.enablementadobe.com/content/luma/us/en.html) 에는 사실적인 구현을 구축할 수 있는 풍부한 데이터 레이어와 기능이 있습니다. 이 자습서에서는 다음 작업을 수행합니다.

* Luma 웹 사이트에 대한 Platform Web SDK 구현을 사용하여 자신의 계정에 고유한 태그 속성을 만듭니다.
* 데이터스트림, 스키마 및 ID 네임스페이스 등 웹 SDK 구현을 위한 모든 데이터 수집 기능을 구성합니다.
* 다음 Adobe Experience Cloud 애플리케이션을 추가합니다.
   * **[Adobe Experience Platform](setup-experience-platform.md)** (및 Adobe Real-time Customer Data Platform, Adobe Journey Optimizer, Adobe Customer Journey Analytics 등 플랫폼을 기반으로 구축된 애플리케이션)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**
* Web SDK에서 수집한 데이터를 Adobe이 아닌 대상으로 보내려면 이벤트 전달을 구현합니다.
* Experience Platform Debugger 및 Assurance를 사용하여 자체 Platform Web SDK 구현의 유효성을 검사합니다.

이 자습서를 완료하고 나면 자체 웹 사이트에서 Platform Web SDK를 통해 모든 마케팅 애플리케이션 구현을 시작할 수 있습니다.


>[!NOTE]
>
>에 대해 유사한 다중 솔루션 자습서를 사용할 수 있습니다. [Mobile SDK](../tutorial-mobile-sdk/overview.md).

## 전제 조건

모든 Experience Cloud 고객은 Platform Web SDK를 사용할 수 있습니다. Web SDK를 사용하기 위해 Real-time Customer Data Platform 또는 Journey Optimizer과 같은 플랫폼 기반 애플리케이션에 라이센스를 부여할 필요는 없습니다.

이 단원들에서는 사용자에게 Adobe 계정과 단원을 완료하는 데 필요한 권한이 있다고 가정합니다. 그렇지 않은 경우 Experience Cloud 관리자에게 연락하여 액세스 권한을 요청해야 합니다.

* 대상 **데이터 수집**, 다음을 보유해야 합니다.
   * **[!UICONTROL 플랫폼]**—다음에 대한 권한 **[!UICONTROL 웹]** 그리고 라이센스가 부여되면 **[!UICONTROL Edge]**
   * **[!UICONTROL 속성 권한]**—권한 대상 **[!UICONTROL 승인]**, **[!UICONTROL 개발]**, **[!UICONTROL 속성 편집]**, **[!UICONTROL 환경 관리]**, **[!UICONTROL 확장 관리]**, 및 **[!UICONTROL 게시]**,
   * **[!UICONTROL 회사 권한]**—권한 대상 **[!UICONTROL 속성 관리]**

     태그 권한에 대한 자세한 내용은 [설명서](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html).

* 대상 **Experience Platform**, 다음을 보유해야 합니다.

   * 액세스 권한: **기본 프로덕션**, **&quot;Prod&quot;** 샌드박스.
   * 액세스 대상: **[!UICONTROL 스키마 관리]** 및 **[!UICONTROL 스키마 보기]** 아래에 **[!UICONTROL 데이터 모델링]**.
   * 액세스 대상: **[!UICONTROL ID 네임스페이스 관리]** 및 **[!UICONTROL ID 네임스페이스 보기]** 아래에 **[!UICONTROL Identity Management]**.
   * 액세스 대상: **[!UICONTROL 데이터 스트림 관리]** 및 **[!UICONTROL 데이터스트림 보기]** 아래에 **[!UICONTROL 데이터 수집]**.
   * 플랫폼 기반 애플리케이션의 고객이고 다음을 완료할 경우 [Experience Platform 설정](setup-experience-platform.md) 단원:
      * 액세스 권한: **개발** 샌드박스.
      * 아래의 모든 권한 항목 **[!UICONTROL 데이터 관리]**, 및 **[!UICONTROL 프로필 관리]**:

     Real-Time CDP과 같은 플랫폼 기반 애플리케이션의 고객이 아니더라도 모든 Experience Cloud 고객이 필요한 기능을 사용할 수 있어야 합니다.

     Platform 액세스 제어에 대한 자세한 내용은 [설명서](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=ko).

* 선택 사항용 **Adobe Analytics** 단원, 다음을 수행해야 합니다. [보고서 세트 설정, 처리 규칙 및 Analysis Workspace에 대한 관리자 액세스](https://experienceleague.adobe.com/docs/analytics/admin/admin-console/home.html?lang=ko-KR)

* 선택 사항용 **Adobe Target** 단원, 다음을 수행해야 합니다. [편집자 또는 승인자](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) 액세스 권한.

* 선택 사항용 **Audience Manager** 단원, 트레이트, 세그먼트 및 대상을 만들고, 읽고, 쓸 수 있는 액세스 권한이 있어야 합니다. 자세한 내용은 다음 자습서를 참조하십시오. [Audience Manager의 역할 기반 액세스 제어](https://experienceleague.adobe.com/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control.html?lang=en).


>[!NOTE]
>
>사용자가 HTML 및 JavaScript와 같은 프론트엔드 개발 언어를 잘 알고 있다고 가정합니다. 이러한 언어에 대해 전문가가 될 필요는 없지만 코드를 읽고 이해할 수 있는 경우 이 자습서를 통해 자세한 내용을 확인할 수 있습니다.

## Luma 웹 사이트 로드

을(를) 로드합니다 [Luma 웹 사이트](https://luma.enablementadobe.com/content/luma/us/en.html) 자습서 중에 필요할 때마다 쉽게 로드할 수 있도록 별도의 브라우저 탭에서 책갈피를 지정합니다. 호스팅된 프로덕션 사이트를 로드할 수 있는 것 외에 Luma에 대한 추가 액세스 권한이 필요하지 않습니다.

[![Luma 웹 사이트](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)

그럼 시작해 보겠습니다!

[다음: ](configure-schemas.md)

>[!NOTE]
>
>Adobe Experience Platform Web SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나, 일반적인 피드백을 공유하거나, 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오. [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
