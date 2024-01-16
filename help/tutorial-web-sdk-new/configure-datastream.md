---
title: 데이터스트림 구성
description: 데이터 스트림을 활성화하고 Experience Cloud 솔루션을 구성하는 방법에 대해 알아봅니다. 이 단원은 Web SDK를 사용하여 Adobe Experience Cloud 구현 자습서의 일부입니다.
feature: Web SDK,Datastreams
source-git-commit: f08866de1bd6ede50bda1e5f8db6dbd2951aa872
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 3%

---

# 데이터스트림 구성

데이터 스트림을 활성화하고 Experience Cloud 애플리케이션을 구성하는 방법에 대해 알아봅니다.

데이터 스트림은 Adobe Experience Platform Edge Network에 Platform Web SDK에서 수집한 데이터를 보낼 위치를 알려줍니다. 데이터스트림 구성에서 Experience Cloud 애플리케이션, Experience Platform 계정 및 이벤트 전달을 활성화합니다. 다음을 참조하십시오. [데이터 스트림 구성의 기본 사항](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=ko-KR) 를 참조하십시오.

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* 데이터 스트림 만들기
* 데이터 스트림 무시 시작

## 전제 조건

데이터 스트림을 구성하기 전에 다음 단원을 이미 완료해야 합니다.

* [스키마 구성](configure-schemas.md)
* [ID 네임스페이스 구성](configure-identities.md)

## 데이터 스트림 만들기

이제 데이터 스트림을 만들어 Platform Edge Network에 Web SDK에서 수집한 데이터를 보낼 위치를 지정할 수 있습니다.

**데이터 스트림을 생성하려면 다음을 수행합니다.**

1. 를 엽니다. [데이터 수집 인터페이스](https://launch.adobe.com/){target="_blank"}
1. 올바른 샌드박스에 있는지 확인합니다

   >[!NOTE]
   >
   >Real-Time CDP과 같은 플랫폼 기반 애플리케이션의 고객인 경우 이 자습서에서는 개발 샌드박스를 사용하는 것이 좋습니다. 그렇지 않으면 **[!UICONTROL Prod]** 샌드박스.

1. 다음으로 이동 **[!UICONTROL 데이터스트림]** 왼쪽 탐색
1. 선택 **[!UICONTROL 새 데이터스트림]** 화면의 오른쪽
1. 입력 `Luma Web SDK: Development Environment` (으)로 **[!UICONTROL 이름]**. 이 이름은 나중에 태그 속성에서 Web SDK 확장을 구성할 때 참조됩니다.
1. 다음 항목 선택 `Luma Web Event Data` (으)로 **[!UICONTROL 이벤트 스키마]**
1. 선택 **[!UICONTROL 저장]**

   ![데이터 스트림 만들기](assets/datastream-create-new-datastream.png)

   >[!AVAILABILITY]
   >
   >매핑 기능은 나중에 이 자습서에 통합될 예정입니다.




다음 화면에서는 데이터 스트림에 Adobe 응용 프로그램과 같은 서비스를 추가할 수 있지만 자습서의 이 시점에서는 서비스를 추가하지 않습니다. 나중에 단원에서 그렇게 할 것입니다 [Experience Platform 설정](setup-experience-platform.md), [Analytics 설정](setup-analytics.md), [Audience Manager 설정](setup-audience-manager.md), [Target 설정](setup-target.md), 또는 [이벤트 전달](setup-event-forwarding.md).

>[!NOTE]
>
>자체 웹 사이트에서 Platform Web SDK를 구현할 때 세 개의 태그 환경(개발, 스테이지 및 프로덕션)에 매핑할 세 개의 데이터스트림을 만들어야 합니다. Adobe Real-time Customer Data Platform 또는 Adobe Journey Optimizer과 같은 플랫폼 기반 애플리케이션과 함께 Platform Web SDK를 사용하는 경우, 적절한 Platform 샌드박스에서 이러한 데이터스트림을 만들어야 합니다.

## 데이터 스트림 재정의

데이터 스트림 재정의를 사용하면 데이터 스트림에 대한 추가 구성을 정의한 다음 구현의 특정 조건에서 기본 구성을 재정의할 수 있습니다.


데이터 스트림 구성 재정의는 2단계 프로세스입니다.

1. 먼저 데이터 스트림 구성에서 데이터 스트림 재정의를 정의합니다. 이 작업은 재정의하려는 Adobe 애플리케이션별로 수행해야 합니다.
1. 그런 다음 웹 SDK 이벤트 전송 작업 또는 웹 SDK 태그 확장의 구성으로 Edge Network에 재정의를 전송합니다.

다음을 참조하십시오. [데이터 스트림 구성 무시 설명서](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overrides.html?lang=en) 데이터스트림 구성을 재정의하는 방법에 대한 자세한 지침을 확인하십시오.

Adobe Analytics 설정 단원에서 다음을 수행합니다 [platform 웹 SDK 이벤트 보내기 작업을 사용하여 페이지에 대한 보고서 세트 재정의](setup-analytics.md).

이제 태그 속성에 Platform Web SDK 확장을 설치할 준비가 되었습니다!

[다음: ](install-web-sdk.md)

>[!NOTE]
>
>Adobe Experience Platform Web SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나, 일반적인 피드백을 공유하거나, 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오. [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
