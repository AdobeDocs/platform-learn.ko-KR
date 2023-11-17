---
title: 데이터스트림 구성
description: Experience Platform에서 데이터 스트림을 만드는 방법을 알아봅니다.
feature: Mobile SDK,Datastreams
hide: true
exl-id: d8b9df3d-49ee-4578-92c6-0f920a86fe7e
source-git-commit: 4a12f8261cf1fb071bc70b6a04c34f6c16bcce64
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 8%

---

# 데이터 스트림 만들기

Experience Platform에서 데이터 스트림을 만드는 방법을 알아봅니다.

데이터 스트림은 Platform Edge Network의 서버측 구성입니다. 데이터 스트림은 Platform Edge Network로 들어오는 데이터가 Adobe Experience Cloud 애플리케이션 및 서비스로 적절하게 라우팅되도록 합니다. 자세한 내용은 [설명서](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=ko-KR) 또는 이 [비디오](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=ko).

![아키텍처](assets/architecture.png)

## 전제 조건

데이터 스트림을 생성하려면 조직에서 데이터 수집 인터페이스(이전의 )에서 이 기능에 대해 프로비저닝해야 합니다 [!UICONTROL 시작])에 액세스하여 데이터 스트림을 관리하고 볼 수 있는 사용자 권한이 있어야 합니다.

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* 데이터 스트림을 사용할 시기를 알 수 있습니다.
* 데이터 스트림을 만듭니다.
* 데이터스트림 구성.

## 데이터 스트림 만들기

데이터 스트림은 [!UICONTROL 데이터 수집] 를 사용한 인터페이스 [!UICONTROL 데이터스트림] 구성 도구입니다. 데이터 스트림을 생성하려면 다음을 수행합니다.

1. 데이터 스트림은 샌드박스 수준에서 정의되므로 올바른 Experience Platform 샌드박스에 있는지 확인하십시오.
1. 선택 **[!UICONTROL 데이터스트림]** 왼쪽 레일에서.
1. **[!UICONTROL 새 데이터스트림]**&#x200B;을 선택합니다.

   ![데이터스트림 홈](assets/datastream-new.png)

1. 다음을 제공합니다. **[!UICONTROL 이름]**, 예 `Luma Mobile App` 및 a **[!UICONTROL 설명]**, 예 `Datastream for Luma Mobile App`.

   >[!NOTE]
   >
   >최종 미리 알림: 단일 샌드박스에 여러 사람과 함께 이 자습서를 진행하거나 공유 계정을 사용하는 경우 이름 지정 규칙의 일부로 ID를 추가하거나 앞에 추가하는 것이 좋습니다. 예를 들어 `Luma Mobile App Event Dataset` 대신 `Luma Mobile App Event Dataset - Joe Smith`을 사용합니다. 다음에서 참고 참조: [개요](overview.md).

1. 의 이전 단원에서 만든 스키마를 선택합니다 **이벤트 스키마** 목록을 표시합니다.
1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

   ![새 데이터스트림](assets/datastream-name.png)


## 서비스 추가

다음 단계를 거칠 때(선택 사항) [분석](analytics.md) 및 [Experience Platform](platform.md) 이 자습서의 단원에서는 Platform Edge Network로 전송된 데이터가 이러한 응용 프로그램으로 전달되도록 데이터 스트림에 서비스를 추가합니다.

<!--

### Adobe Analytics

1. Select **[!UICONTROL Add Service]**.

1. Add **[!UICONTROL Adobe Analytics]** from the [!UICONTROL Service] list, 

1. Enter the name of the report site that you want to use in **[!UICONTROL Report Suite ID]**.

1. Enable the service by switching **[!UICONTROL Enabled]** on.

1. Select **[!UICONTROL Save]**.

   ![Add Adobe Analytics as datastream service](assets/datastream-service-aa.png)


### Adobe Experience Platform

You might also want to enable the Adobe Experience Platform service. 

>[!IMPORTANT]
>
>You can only enable the Adobe Experience Platform service when having created an event dataset. If you don't already have an event dataset created, follow the instructions [here](platform.md).

1. Click ![Add](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Add Service]** to add another service.

1. Select **[!UICONTROL Adobe Experience Platform]** from the [!UICONTROL Service] list.

1. Enable the service by switching **[!UICONTROL Enabled]** on.

1. Select the **[!UICONTROL Event Dataset]** that you created as part of the [Create a dataset](platform.md#create-a-dataset) instructions, for example **Luma Mobile App Event Dataset**

1. Select **[!UICONTROL Save]**.

   ![Add Adobe Experience Platform as a datastream service](assets/datastream-service-aep.png)
1. The final configuration should look something like this.
   
   ![datastream settings](assets/datastream-settings.png)

-->


>[!NOTE]
>
>조직에서 사용하는 각 서비스를 활성화하면 모바일 앱에서 수집한 데이터를 어디에서나 사용할 수 있습니다. 데이터 스트림 설정에 대한 자세한 내용은 설명서를 참조하십시오 [여기](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=ko-KR).

자체 앱에서 Platform Mobile SDK를 구현할 때 궁극적으로 세 개의 데이터 스트림을 만들어 세 개의 태그 환경(개발, 스테이지 및 프로덕션)에 매핑해야 합니다. Adobe Real-time Customer Data Platform 또는 Adobe Journey Optimizer과 같은 플랫폼 기반 애플리케이션과 함께 Platform Mobile SDK를 사용하는 경우 적절한 샌드박스에서 이러한 데이터스트림을 만들어야 합니다.

>[!SUCCESS]
>
>이제 자습서의 나머지 부분에서 사용할 데이터 스트림이 있습니다.
>
>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하려는 경우 또는 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

다음: **[태그 속성 구성](configure-tags.md)**
