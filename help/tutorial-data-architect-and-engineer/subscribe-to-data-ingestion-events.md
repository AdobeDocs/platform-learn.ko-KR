---
title: 데이터 수집 이벤트 구독
seo-title: Subscribe to data ingestion events | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 데이터 수집 이벤트 구독
description: 이 단원에서는 Adobe Developer 콘솔 및 온라인 웹후크 개발 도구를 사용하여 웹후크를 설정하여 데이터 수집 이벤트에 가입합니다. 이러한 이벤트를 사용하여 후속 단원에서 데이터 수집 작업의 상태를 모니터링합니다.
role: Data Engineer
feature: Data Management
jira: KT-4348
thumbnail: 4348-subscribe-to-data-ingestion-events.jpg
exl-id: f4b90832-4415-476f-b496-2f079b4fcbbc
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 1%

---

# 데이터 수집 이벤트 구독

<!--25min-->

이 단원에서는 Adobe Developer 콘솔 및 온라인 웹후크 개발 도구를 사용하여 웹후크를 설정하여 데이터 수집 이벤트에 가입합니다. 이러한 이벤트를 사용하여 후속 단원에서 데이터 수집 작업의 상태를 모니터링합니다.

**데이터 엔지니어** 이 자습서 외부의 데이터 수집 이벤트에 가입하려고 합니다.
**데이터 설계자** _이 단원을 건너뛸 수 있음_ 로 이동 [일괄 처리 수집 단원](ingest-batch-data.md).

## 권한 필요

다음에서 [권한 구성](configure-permissions.md) 단원, 특히 이 단원을 완료하는 데 필요한 모든 액세스 제어를 설정합니다.

<!--* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

>[!IMPORTANT]
>
> 데이터 수집 이벤트에 의해 트리거되는 이러한 알림은에 적용됩니다. _모든 샌드박스_, 사용자 `Luma Tutorial`. 계정의 다른 데이터 수집 이벤트에서 시작된 알림도 표시될 수 있습니다.


## 웹후크 설정

이 연습에서는 webhook.site라는 온라인 도구를 사용하여 웹후크를 만듭니다(사용하려는 다른 웹후크 개발 도구를 언제든지 대체할 수 있음).

1. 다른 브라우저 탭에서 웹 사이트를 엽니다. [https://webhook.site/](https://webhook.site/)
1. 나중에 데이터 수집 단원에서 반환할 때 책갈피에 추가해야 하는 고유한 URL이 할당됩니다.

   ![Webhook.site](assets/ioevents-webhook-home.png)
1. 다음 항목 선택 **편집** 위쪽 탐색의 단추
1. 응답 본문으로 를 입력합니다. `$request.query.challenge$`. 이 단원의 뒷부분에서 설정한 Adobe I/O 이벤트 알림은 웹후크에 문제를 보내며, 이를 응답 본문에 포함해야 합니다.
1. **저장** 버튼을 선택합니다

   ![응답 편집](assets/ioevents-webhook-editResponse.png)

## 설정

1. 다른 브라우저 탭에서 [Adobe Developer 콘솔](https://console.adobe.io/)
1. 을(를) 엽니다 `Luma Tutorial API Project`
1. 다음 항목 선택 **[!UICONTROL 프로젝트에 추가]** 버튼을 누른 다음 선택 **[!UICONTROL 이벤트]**

   ![이벤트 추가](assets/ioevents-addEvents.png)
1. 다음을 선택하여 목록 필터링 **[!UICONTROL Experience Platform]**
1. 선택 **[!UICONTROL Platform 알림]**
1. 다음 항목 선택 **[!UICONTROL 다음]** 단추
   ![알림 추가](assets/ioevents-addNotifications.png)
1. 모든 이벤트 선택
1. 다음 항목 선택 **[!UICONTROL 다음]** 단추
   ![구독 선택](assets/ioevents-addSubscriptions.png)
1. 자격 증명을 구성하는 다음 화면에서 다음을 선택합니다. **[!UICONTROL 다음]** 단추 다시 입력
   ![자격 증명 화면 건너뛰기](assets/ioevents-clickNext.png)
1. 다음으로: **[!UICONTROL 이벤트 등록 이름]**, 입력 `Platform notifications`
1. 아래로 스크롤하고 을(를) 선택하여 **[!UICONTROL Webhook]** 섹션
1. 다음으로: **[!UICONTROL Webhook URL]**&#x200B;의 값을 붙여 넣습니다. **고유 URL** webhook.site의 필드
1. 다음 항목 선택 **[!UICONTROL 구성된 이벤트 저장]** 단추
   ![이벤트 저장](assets/ioevents-addWebhook.png)
1. 구성이 저장될 때까지 기다리십시오. `Platform notifications` 이벤트가 활성화 상태이며 웹후크 세부 정보가 있고 오류 메시지가 없습니다.
   ![구성 저장됨](assets/ioevents-webhookConfigured.png)
1. webhook.site 탭으로 다시 전환하면 Developer Console 구성의 유효성 검사로 인한 Webhook에 대한 첫 번째 요청이 표시됩니다.
   ![webhook.site의 첫 번째 요청](assets/ioevents-webhook-firstRequest.png)

지금은 데이터를 수집할 때 다음 단원에서 이러한 알림에 대해 자세히 알아봅니다.

## 추가 리소스

* [Webhook.site](https://webhook.site/)
* [데이터 수집 알림 설명서](https://experienceleague.adobe.com/docs/experience-platform/ingestion/quality/subscribe-events.html)
* [Adobe I/O 이벤트 시작하기 설명서](https://www.adobe.io/apis/experienceplatform/events/docs.html)

좋아, 이제 시작하자 [데이터 수집](ingest-batch-data.md)!
