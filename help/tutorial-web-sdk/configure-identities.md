---
title: ID 네임스페이스 구성
description: Adobe Experience Platform Web SDK에서 사용할 ID 네임스페이스를 구성하는 방법에 대해 알아봅니다. 이 단원은 Web SDK를 사용하여 Adobe Experience Cloud 구현 자습서의 일부입니다.
feature: Web SDK,Identities
jira: KT-15400
exl-id: 7719dff4-6b30-4fa0-acae-7491c3208f15
source-git-commit: 8602110d2b2ddc561e45f201e3bcce5e6a6f8261
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 8%

---

# ID 네임스페이스 구성

Adobe Experience Platform Web SDK에서 사용할 ID 네임스페이스를 구성하는 방법에 대해 알아봅니다.

다음 [Adobe Experience Cloud ID 서비스](https://experienceleague.adobe.com/en/docs/id-service/using/home) 는 SDK 기반 Adobe 애플리케이션에서 공통 방문자 ID(ECID)를 설정하여 애플리케이션 간의 대상 공유와 같은 Experience Cloud 기능을 지원합니다. 또한 고유한 고객 ID를 서비스로 보내어 장치 간 타깃팅 및 CRM(고객 관계 관리) 시스템과 같은 다른 시스템과의 통합을 가능하게 할 수 있습니다.

다음 [Adobe Experience Platform ID 서비스](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home) (예, 두 개 있습니다!) 는 ECID 및 고객 ID를 사용하여 ID 그래프를 생성하므로 속성 및 동작을 실시간 고객 프로필에 병합할 수 있습니다.

>[!NOTE]
>
> 이 단원의 연습에서는 데모용으로 가상 고객에 로그인한 ID의 세부 정보를 캡처합니다. [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html) 자격 증명을 사용하여 **사용자: `test@adobe.com` / 암호: 테스트**.

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* ID 네임스페이스 이해
* 사용자 정의 ID 네임스페이스를 만들어 내부 CRM ID 캡처


## 전제 조건

다음 이전 단원을 이미 완료했을 것입니다.

* [스키마 구성](configure-schemas.md)

>[!IMPORTANT]
>
>다음 [Experience Cloud ID 확장](https://exchange.adobe.com/apps/ec/100160/adobe-experience-cloud-id-launch-extension) 웹 SDK JavaScript 라이브러리에는 방문자 ID 서비스 기능이 포함되어 있으므로 Adobe Experience Platform 웹 SDK를 구현할 때에는 이 필요하지 않습니다.
>
> 웹 사이트에서 이미 방문자 API 또는 Experience Cloud ID 서비스 태그 확장 기능을 통해 웹 사이트에서 Experience Cloud ID 서비스를 사용하고 있으며, Adobe Experience Platform Web SDK로 마이그레이션하는 동안 계속 사용하려면 최신 버전의 방문자 API 또는 Experience Cloud ID 서비스 태그 확장 기능을 사용해야 합니다. 다음을 참조하십시오 [ID 마이그레이션](https://experienceleague.adobe.com/en/docs/experience-platform/edge/identity/overview) 추가 정보.

## ID 네임스페이스 만들기

이 연습에서는 Luma의 사용자 지정 ID 필드에 대한 ID 네임스페이스를 만듭니다. `lumaCrmId`. 동일한 네임스페이스 내에 일치하는 두 값이 있으면 두 개의 데이터 소스가 하나의 아이덴티티 그래프를 구성할 수 있기 때문에 신원 네임스페이스는 실시간 고객 프로필을 작성하는 데 중요한 역할을 합니다.

연습을 시작하기 전에 이 짧은 비디오를 통해 Adobe Experience Platform의 ID에 대해 자세히 알아보십시오.

>[!VIDEO](https://video.tv.adobe.com/v/27841?learn=on)

이제 Luma CRM ID에 대한 네임스페이스를 만듭니다.

1. 를 엽니다. [데이터 수집 인터페이스](https://launch.adobe.com/){target="_blank"}
1. 자습서에 사용할 샌드박스를 선택합니다

   >[!NOTE]
   >
   >Real-Time CDP 또는 Journey Optimizer과 같은 플랫폼 기반 애플리케이션의 고객인 경우 이 자습서에서는 개발 샌드박스를 사용하는 것이 좋습니다. 그렇지 않으면 **[!UICONTROL Prod]** 샌드박스.

1. 선택 **[!UICONTROL ID]** 왼쪽 탐색
1. 선택 **[!UICONTROL 찾아보기]**

   페이지의 기본 인터페이스에 ID 네임스페이스 목록이 표시되어 이름, ID 기호, 마지막으로 업데이트된 날짜 및 표준 네임스페이스인지 사용자 정의 네임스페이스인지 여부를 보여 줍니다. 오른쪽 레일에는 다음 정보가 포함됩니다. [!UICONTROL ID 그래프 강도].

1. 선택 **[!UICONTROL ID 네임스페이스 만들기]**

   ![ID 보기](assets/configure-identities-screen.png)

1. 다음과 같이 세부 정보를 입력하고 다음을 선택합니다. **[!UICONTROL 만들기]**.

   | 필드 | 값 |
   |---------------|-----------|
   | 표시 이름 | Luma CRM ID |
   | ID 심볼 | lumaCrmId |
   | 유형 | 개별 교차 장치 ID |


   ![네임스페이스 만들기](assets/identities-create-namespace.png)


   ID 네임스페이스는 **[!UICONTROL ID]** 화면.

   ![네임스페이스 만들기](assets/configure-identities-namespace-lumaCrmId.png)


>[!NOTE]
>
> 다음에서 [ID 만들기](create-identities.md) 단원: Platform Edge Network에 ID를 전송할 때 이 네임스페이스를 사용하는 방법을 알아봅니다.

ID가 준비되었으므로 데이터 스트림을 구성할 수 있습니다.

[다음: ](configure-datastream.md)

>[!NOTE]
>
>Adobe Experience Platform Web SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나, 일반적인 피드백을 공유하거나, 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오. [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
