---
title: 데이터 스트림 구성
description: 데이터 스트림을 활성화하고 Experience Cloud 솔루션을 구성하는 방법을 알아봅니다. 이 단원은 웹 SDK를 사용하여 Adobe Experience Cloud 구현 자습서의 일부입니다.
feature: Datastreams
exl-id: ca28374a-9fe0-44de-a7ac-0aa046712515
source-git-commit: 762195148f7594e30b361546941dfcd8076ab7b1
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 4%

---

# 데이터 스트림 구성

데이터 스트림을 활성화하고 Experience Cloud 솔루션을 구성하는 방법을 알아봅니다.

데이터 저장소는 Platform Web SDK에서 수집한 데이터를 보낼 위치를 Adobe Experience Platform Edge 네트워크에 알려줍니다. 데이터 스트림 구성에서 Experience Cloud 애플리케이션, Experience Platform 계정 및 이벤트 전달을 활성화합니다. 자세한 내용은 [데이터 스트림 구성의 기본 사항](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en) 를 참조하십시오.

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* 데이터 스트림 만들기
* Experience Cloud 애플리케이션 활성화
* Experience Platform 활성화

## 전제 조건

데이터 스트림을 구성하기 전에 다음 단원을 이미 완료했어야 합니다.

* [권한 구성](configure-permissions.md)
* [스키마 구성](configure-schemas.md)
* [ID 네임스페이스 구성](configure-identities.md)

## 데이터 스트림 만들기

이제 데이터 스트림을 만들어 Platform Edge 네트워크에 웹 SDK에서 수집한 데이터를 보낼 위치를 알려줄 수 있습니다.

**데이터 스트림을 만들려면 다음을 수행하십시오.**

1. 를 엽니다. [데이터 수집 인터페이스](https://launch.adobe.com/){target=&quot;_blank&quot;}
1. 올바른 샌드박스에 있는지 확인합니다

   >[!NOTE]
   >
   >실시간 CDP와 같은 플랫폼 기반 애플리케이션을 사용하는 경우에는 이 자습서에 개발 샌드박스를 사용하는 것이 좋습니다. 그렇지 않은 경우 **[!UICONTROL Prod]** 샌드박스

1. 이동 **[!UICONTROL 데이터 스트림]** 왼쪽 탐색
1. 선택 **[!UICONTROL 새 데이터 스트림]** 화면 오른쪽입니다.
1. Enter 키 `Luma Web SDK` 로서의 **[!UICONTROL 이름]**. 이 이름은 태그 속성에서 웹 SDK 확장을 구성할 때 나중에 참조됩니다.
1. 을(를) 선택합니다 `Luma Web Event Data` 로서의 **[!UICONTROL 이벤트 스키마]**
1. **[!UICONTROL 저장]**&#x200B;을 선택합니다

   ![데이터 스트림 만들기](assets/datastream-create-datastream.png)

   >[!AVAILABILITY]
   >
   >매핑 기능은 나중에 이 자습서에 통합됩니다.




다음 화면에서는 데이터 스트림에 Adobe 응용 프로그램과 같은 서비스를 추가할 수 있지만 이 시점에서 자습서의 서비스를 추가하지 않습니다. 너는 나중에 수업할 것이다 [Experience Platform 설정](setup-experience-platform.md), [Analytics 설정](setup-analytics.md), [Audience Manager 설정](setup-audience-manager.md), [설정 Target](setup-target.md), 또는 [이벤트 전달](setup-event-forwarding.md).

>[!NOTE]
>
>자체 웹 사이트에서 Platform Web SDK를 구현할 때는 세 개의 태그 환경(개발, 스테이지 및 프로덕션)에 매핑할 데이터 세트를 세 개 만들어야 합니다. Adobe Real-time Customer Data Platform 또는 Adobe Journey Optimizer과 같은 플랫폼 기반 애플리케이션과 함께 Platform Web SDK를 사용하는 경우, 해당 Platform 샌드박스에 해당 데이터 세트를 만들어야 합니다.

이제 태그 속성에 Platform Web SDK 확장을 설치할 준비가 되었습니다!

[다음: ](install-web-sdk.md)

>[!NOTE]
>
>Adobe Experience Platform Web SDK에 대한 학습에 시간을 내주셔서 감사합니다. 질문이 있거나 일반 피드백을 공유하거나 향후 컨텐츠에 대한 제안 사항이 있는 경우 해당 정보를 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
