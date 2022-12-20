---
title: 자습서에 대한 권한 구성
description: 웹 SDK를 사용하여 Adobe Experience Cloud 구현 자습서를 완료하는 데 필요한 권한을 Experience Platform 웹 SDK에 요청하고 구성하는 방법을 알아봅니다.
feature: Access Control
exl-id: d7c4f2c3-cf3c-4587-88f8-82113d250084
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 6%

---

# 자습서에 대한 권한 구성

Experience Platform 웹 SDK에 대한 액세스를 요청하고 이 자습서를 완료하는 데 필요한 권한을 구성하는 방법을 알아봅니다. 데이터 수집 인터페이스에서 태그를 사용하여 Platform Web SDK를 구현하려면 [Admin Console](https://adminconsole.adobe.com).

## 데이터 수집

* 권한 있음 **[!UICONTROL 개발]**, **[!UICONTROL 편집]**, **[!UICONTROL 승인]**, **[!UICONTROL 게시]**, **[!UICONTROL 확장 관리]**, **[!UICONTROL 환경 관리]**, 및 **[!UICONTROL 속성 관리]**. 태그 권한에 대한 자세한 내용은 [설명서](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html).
* 선택적 이벤트 전달 단원을 완료할 예정이라면 Edge 전달 및 권한 항목을 포함하는 제품 라이센스가 있어야 합니다 **[!UICONTROL 플랫폼]** > **[!UICONTROL Edge]**

## Experience Platform

Real-Time CDP과 같은 플랫폼 기반 애플리케이션의 고객이 아닌 경우에도 이러한 기능을 모든 Experience Cloud 고객이 사용할 수 있어야 합니다.

* 에 액세스 **기본 프로덕션**, **&quot;Prod&quot;** 샌드박스 ( )
* 액세스 권한 **[!UICONTROL 스키마 관리]** 및 **[!UICONTROL 스키마 보기]** 아래에 **[!UICONTROL 데이터 모델링]**
* 액세스 권한 **[!UICONTROL ID 네임스페이스 관리]** 및 **[!UICONTROL ID 네임스페이스 보기]** 아래에 **[!UICONTROL Identity Management]**
* 액세스 권한 **[!UICONTROL 데이터 스트림 관리]** 및 **[!UICONTROL 데이터 스트림 보기]** 아래에 **[!UICONTROL 데이터 수집]**
* 플랫폼 기반 애플리케이션의 고객이고 [Experience Platform 설정](setup-experience-platform.md) 또한 다음을 수행해야 합니다.
   * 액세스 권한 **개발** 샌드박스
   * 아래의 모든 권한 항목 **[!UICONTROL 데이터 관리]**, 및 **[!UICONTROL 프로필 관리]**:


플랫폼 액세스 제어에 대한 자세한 내용은 [설명서](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=ko).

## Adobe Analytics

선택 사항인 Adobe Analytics 단원의 경우 [보고서 세트 설정, 처리 규칙 및 Analysis Workspace에 대한 관리자 액세스 권한](https://experienceleague.adobe.com/docs/analytics/admin/admin-console/home.html?lang=ko-KR)

## Adobe Target

선택 사항인 Adobe Target 단원의 경우 [편집자 또는 승인자](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) 액세스 권한.

## Adobe Audience Manager

* 선택적 Audience Manager 단원의 경우 트레이트, 세그먼트 및 대상을 만들고, 읽고, 쓸 수 있는 액세스 권한이 있어야 합니다. 자세한 내용은 [Audience Manager의 역할 기반 액세스 제어](https://experienceleague.adobe.com/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control.html?lang=en).

이제 초기 구성 단계를 시작할 준비가 되었습니다.

[다음: ](configure-schemas.md)

>[!NOTE]
>
>Adobe Experience Platform Web SDK에 대한 학습에 시간을 내주셔서 감사합니다. 질문이 있거나 일반 피드백을 공유하거나 향후 컨텐츠에 대한 제안 사항이 있는 경우 해당 정보를 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
