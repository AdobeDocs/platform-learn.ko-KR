---
title: 데이터스트림 구성
description: Experience Platform에서 데이터 스트림을 만드는 방법을 알아봅니다.
feature: Mobile SDK,Datastreams
hide: true
source-git-commit: a2788110b1c43d24022672bb5ba0f36af66d962b
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 7%

---


# 데이터 스트림 만들기

Experience Platform에서 데이터 스트림을 만드는 방법을 알아봅니다.

데이터 스트림은 Platform Edge Network의 서버측 구성입니다. 데이터 스트림은 Platform Edge Network로 들어오는 데이터가 Adobe Experience Cloud 애플리케이션 및 서비스로 적절하게 라우팅되도록 합니다. 자세한 내용은 [설명서](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html) 또는 이 [비디오](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=ko).

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

(선택 사항)을 보낼 때 [분석](analytics.md) 및 [Experience Platform](platform.md) 이 자습서의 단원에서는 Platform Mobile SDK가 Edge Network에 데이터를 전송할 때 데이터 스트림이 구성된 서비스에 해당 데이터를 전송하도록 데이터 스트림에 서비스를 추가하는 것입니다.

### Adobe Analytics

1. **[!UICONTROL 서비스 추가]**&#x200B;를 선택합니다.

1. 추가 **[!UICONTROL Adobe Analytics]** 다음에서 [!UICONTROL 서비스] 목록,

1. 사용할 보고서 사이트의 이름을 입력하십시오. **[!UICONTROL 보고서 세트 ID]**.

1. 전환하여 서비스 활성화 **[!UICONTROL 활성화됨]** 켜짐.

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

   ![데이터 스트림 서비스로 Adobe Analytics 추가](assets/datastream-service-aa.png)


### Adobe Experience Platform

Adobe Experience Platform 서비스를 활성화할 수도 있습니다.

>[!IMPORTANT]
>
>이벤트 데이터 세트를 만든 경우에만 Adobe Experience Platform 서비스를 활성화할 수 있습니다. 아직 생성된 이벤트 데이터 세트가 없는 경우 지침을 따르십시오 [여기](platform.md).

1. 클릭 ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 서비스 추가]** 다른 서비스를 추가합니다.

1. [!UICONTROL 서비스] 목록에서 **[!UICONTROL Adobe Experience Platform]**&#x200B;을 선택합니다.

1. 전환하여 서비스 활성화 **[!UICONTROL 활성화됨]** 켜짐.

1. 다음 항목 선택 **[!UICONTROL 이벤트 데이터 세트]** 의 일부로 생성한 [데이터 세트 만들기](platform.md#create-a-dataset) 지침, 예 **Luma 모바일 앱 이벤트 데이터 세트**

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

   ![Adobe Experience Platform을 데이터스트림 서비스로 추가](assets/datastream-service-aep.png)
1. 최종 구성은 다음과 같아야 합니다.

   ![데이터 스트림 설정](assets/datastream-settings.png)


>[!NOTE]
>
>조직에서 사용하는 각 서비스를 활성화하면 모바일 앱에서 수집한 데이터를 어디에서나 사용할 수 있습니다. 데이터 스트림 설정에 대한 자세한 내용은 설명서를 참조하십시오 [여기](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html#adobe-experience-platform-settings).

자체 앱에서 Platform Mobile SDK를 구현할 때 궁극적으로 세 개의 데이터 스트림을 만들어 세 개의 태그 환경(개발, 스테이지 및 프로덕션)에 매핑해야 합니다. Adobe Real-time Customer Data Platform 또는 Adobe Journey Optimizer과 같은 플랫폼 기반 애플리케이션과 함께 Platform Mobile SDK를 사용하는 경우 적절한 샌드박스에서 이러한 데이터스트림을 만들어야 합니다.

>[!SUCCESS]
>
>이제 자습서의 나머지 부분에서 사용할 데이터 스트림이 있습니다.<br/>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하려는 경우 또는 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

다음: **[태그 구성](configure-tags.md)**
