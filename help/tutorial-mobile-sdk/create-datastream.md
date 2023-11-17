---
title: 데이터스트림 구성
description: Experience Platform에서 데이터 스트림을 만드는 방법을 알아봅니다.
feature: Mobile SDK,Datastreams
exl-id: 7b83f834-d1fb-45d1-8bcf-bc621f94725c
source-git-commit: 94ca4a238c241518219fb2e8d73f775836f86d86
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 4%

---

# 데이터 스트림 만들기

Experience Platform에서 데이터 스트림을 만드는 방법을 알아봅니다.

>[!INFO]
>
> 이 튜토리얼은 2023년 11월 말에 새 샘플 모바일 앱을 사용하는 새 튜토리얼로 대체됩니다

데이터 스트림은 Platform Edge Network의 서버측 구성입니다.  데이터 스트림은 Platform Edge Network로 들어오는 데이터가 Adobe Experience Cloud 애플리케이션 및 서비스로 적절하게 라우팅되도록 합니다. 자세한 내용은 [설명서](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html) 또는 이 [비디오](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=ko).

## 전제 조건

데이터 스트림을 생성하려면 조직에서 데이터 수집 인터페이스(이전의 )에서 이 기능에 대해 프로비저닝해야 합니다 [!UICONTROL 시작])에 대한 사용자 권한이 있어야 합니다. [!UICONTROL Experience Platform] > [!UICONTROL 데이터 수집] > **[!UICONTROL 데이터 스트림 관리]** 및 **[!UICONTROL 데이터스트림 보기]**.

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* 데이터 스트림을 사용할 시기를 알 수 있습니다.
* 데이터 스트림을 만듭니다.
* 데이터스트림 구성.

## 데이터 스트림 만들기

데이터 스트림은 [!UICONTROL 데이터 수집] 를 사용한 인터페이스 [!UICONTROL 데이터스트림] 구성 도구입니다. 데이터 스트림을 생성하려면 다음을 수행합니다.

1. 올바른 Platform 샌드박스에 있는지 확인합니다.
1. **[!UICONTROL 새 데이터스트림]**&#x200B;을 선택합니다.

   ![데이터스트림 홈](assets/mobile-datastream-new.png)

1. 예를 들어 이름을 입력합니다. `Luma App`.
1. 이전 단원에서 만든 스키마를 선택합니다.
1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

   ![새 데이터스트림](assets/mobile-datastream-name.png)


## 서비스 추가

다음으로 Experience Cloud 서비스를 데이터 스트림에 연결할 수 있습니다. Platform Mobile SDK가 Edge Network에 데이터를 전송할 때 데이터 스트림은 다음 서비스로 데이터를 전송합니다.

1. 추가 **[!UICONTROL Adobe Analytics]** 보고서 세트를 제공합니다.

1. 사용 **[!UICONTROL Adobe Audience Manager]** (선택 사항).

1. 사용 **[!UICONTROL Adobe Experience Platform]** 및 제공 **[!UICONTROL 데이터 세트]** (선택 사항).
   * 아직 만든 데이터 세트가 없는 경우 지침을 따르십시오 [여기](platform.md).

1. 최종 구성은 다음과 같아야 합니다.
   ![데이터 스트림 설정](assets/mobile-datastream-settings.png)


>[!NOTE]
>
>조직에서 사용하는 각 서비스를 활성화하면 모바일 앱에서 수집한 데이터를 어디에서나 사용할 수 있습니다. 데이터 스트림 설정에 대한 자세한 내용을 보려면 설명서를 검토하십시오. [여기](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html#adobe-experience-platform-settings).

자체 웹 사이트에서 Platform Mobile SDK를 구현할 때 세 개의 태그 환경(개발, 스테이지 및 프로덕션)에 매핑할 세 개의 데이터스트림을 만들어야 합니다. Adobe Real-time Customer Data Platform 또는 Adobe Journey Optimizer과 같은 플랫폼 기반 애플리케이션과 함께 Platform Mobile SDK를 사용하는 경우 적절한 Platform 샌드박스에서 이러한 데이터스트림을 만들어야 합니다.

다음: **[태그 구성](configure-tags.md)**

>[!NOTE]
>
>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나, 일반적인 피드백을 공유하거나, 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오. [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
