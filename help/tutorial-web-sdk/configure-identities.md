---
title: ID 네임스페이스 구성
description: Adobe Experience Platform Web SDK에서 사용할 ID 네임스페이스를 구성하는 방법에 대해 알아봅니다. 이 수업은 Web SDK를 사용하여 Adobe Experience Cloud 구현 튜토리얼의 일부입니다.
feature: Web SDK,Identities
jira: KT-15400
exl-id: 7719dff4-6b30-4fa0-acae-7491c3208f15
source-git-commit: e0359d1bade01f79d0f7aff6a6e69f3e4d0c3b62
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 12%

---

# ID 네임스페이스 구성

Adobe Experience Platform Web SDK와 함께 사용할 ID 네임스페이스를 구성하는 방법을 알아봅니다.

[Adobe Experience Cloud Identity Service](https://experienceleague.adobe.com/en/docs/id-service/using/home)은(는) SDK 기반 Adobe 응용 프로그램에서 공통 방문자 ID(ECID)를 설정하여 응용 프로그램 간 대상 공유와 같은 Experience Cloud 기능을 지원합니다. 또한 고유한 고객 ID를 서비스로 보내어 장치 간 타깃팅 및 CRM(고객 관계 관리) 시스템과 같은 다른 시스템과의 통합을 가능하게 할 수 있습니다.

[Adobe Experience Platform ID 서비스](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)&#x200B;(예, 두 개 있음)에서는 ECID와 고객 ID를 사용하여 ID 그래프를 생성하므로 속성과 동작을 실시간 고객 프로필에 병합할 수 있습니다.

>[!NOTE]
>
>Web SDK에서 Adobe Analytics, Adobe Target 또는 Adobe Audience Manager을 구현하는 데 사용자 지정 ID 네임스페이스가 _필요하지 않습니다_(인증된 ID는 나중에 볼 수 있듯이 `xdm` 개체 대신 `data` 개체로 전달될 수 있음). Journey Optimizer, Real-Time Customer Data Platform, Customer Journey Analytics과 같은 플랫폼 기반 애플리케이션에는 ID 네임스페이스가 필요합니다. 자체 구현에서 ID 네임스페이스를 사용하지 않기로 결정할 수 있지만 이 자습서의 일부로 사용해야 합니다.

>[!NOTE]
>
> 데모 목적으로 이 단원의 연습에서는 자격 증명, **사용자: `test@adobe.com`/암호: 테스트**&#x200B;를 사용하여 [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html)에 로그인한 가상 고객의 ID 세부 정보를 캡처합니다.

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* ID 네임스페이스 이해
* 사용자 정의 ID 네임스페이스를 만들어 내부 CRM ID 캡처


## 전제 조건

다음 이전 단원을 이미 완료했을 것입니다.

* [스키마 구성](configure-schemas.md)

>[!IMPORTANT]
>
>웹 Experience Cloud JavaScript 라이브러리에는 방문자 ID 서비스 기능이 포함되어 있으므로 Adobe Experience Platform Web SDK을 구현할 때는 [SDK ID 확장](https://exchange.adobe.com/apps/ec/100160/adobe-experience-cloud-id-launch-extension)이 필요하지 않습니다.
>
> 웹 사이트에서 이미 방문자 API 또는 Experience Cloud ID 서비스 태그 확장 기능을 통해 웹 사이트에서 Experience Cloud ID 서비스를 사용하고 있으며 Adobe Experience Platform Web SDK으로 마이그레이션하는 동안 계속 사용하려면 최신 버전의 방문자 API 또는 Experience Cloud ID 서비스 태그 확장 기능을 사용해야 합니다. 자세한 내용은 [ID 마이그레이션](https://experienceleague.adobe.com/en/docs/experience-platform/edge/identity/overview)을 참조하십시오.

## ID 네임스페이스 만들기

이 연습에서는 Luma의 사용자 지정 ID 필드 `lumaCrmId`에 대한 ID 네임스페이스를 만듭니다. 동일한 네임스페이스 내에 일치하는 두 값이 있으면 두 개의 데이터 소스가 하나의 ID 그래프를 구성할 수 있기 때문에 ID 네임스페이스는 실시간 고객 프로필을 작성하는 데 중요한 역할을 합니다.

연습을 시작하기 전에 이 짧은 비디오를 통해 Adobe Experience Platform의 ID에 대해 자세히 알아보십시오.

>[!VIDEO](https://video.tv.adobe.com/v/27841?learn=on&enablevpops)

이제 Luma CRM ID에 대한 네임스페이스를 만듭니다.

1. [데이터 수집 인터페이스](https://experience.adobe.com/data-collection/){target="_blank"} 열기
1. 자습서에 사용할 샌드박스를 선택합니다

   >[!NOTE]
   >
   >Real-Time CDP 또는 Journey Optimizer과 같은 플랫폼 기반 애플리케이션의 고객인 경우 이 자습서에서는 개발 샌드박스를 사용하는 것이 좋습니다. 그렇지 않은 경우 **[!UICONTROL Prod]** 샌드박스를 사용하십시오.

1. 왼쪽 탐색에서 **[!UICONTROL ID]** 선택
1. **[!UICONTROL 찾아보기]** 선택

   페이지의 기본 인터페이스에 ID 네임스페이스 목록이 표시되어 이름, ID 기호, 마지막으로 업데이트된 날짜 및 표준 네임스페이스인지 사용자 정의 네임스페이스인지 여부를 보여 줍니다. 오른쪽 레일에는 [!UICONTROL ID 그래프 강도]에 대한 정보가 포함되어 있습니다.

1. **[!UICONTROL ID 네임스페이스 만들기]** 선택

   ![ID 보기](assets/configure-identities-screen.png)

1. 다음과 같이 세부 정보를 입력하고 **[!UICONTROL 만들기]**&#x200B;를 선택하세요.

   | 필드 | 값 |
   |---------------|-----------|
   | 표시 이름 | Luma CRM ID |
   | ID 심볼 | lumaCrmId |
   | 유형 | 개별 크로스 디바이스 ID |


   ![네임스페이스 만들기](assets/identities-create-namespace.png)


   ID 네임스페이스가 **[!UICONTROL ID]** 화면에 채워집니다.

   ![네임스페이스 만들기](assets/configure-identities-namespace-lumaCrmId.png)


>[!NOTE]
>
> [ID 만들기](create-identities.md) 단원에서 Platform Edge Network에 ID를 전송할 때 이 네임스페이스를 사용하는 방법을 배웁니다.

ID가 준비되었으므로 데이터 스트림을 구성할 수 있습니다.

[다음: ](configure-datastream.md)

>[!NOTE]
>
>Adobe Experience Platform 웹 SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하고 싶거나 향후 콘텐츠에 대한 제안이 있는 경우 이 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)에서 공유하십시오.
