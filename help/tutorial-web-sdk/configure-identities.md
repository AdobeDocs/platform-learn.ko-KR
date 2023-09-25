---
title: ID 네임스페이스 구성
description: Adobe Experience Platform Web SDK에서 사용할 ID 네임스페이스를 구성하는 방법에 대해 알아봅니다. 이 단원은 Web SDK를 사용하여 Adobe Experience Cloud 구현 자습서의 일부입니다.
feature: Web SDK,Tags,Identities
exl-id: 7719dff4-6b30-4fa0-acae-7491c3208f15
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 13%

---

# ID 네임스페이스 구성

Adobe Experience Platform Web SDK에서 사용할 ID 네임스페이스를 구성하는 방법에 대해 알아봅니다.

다음 [Adobe Experience Platform ID 서비스](https://experienceleague.adobe.com/docs/id-service/using/home.html) 는 솔루션 간 대상 공유와 같은 Experience Cloud 기능을 지원하기 위해 모든 Adobe 솔루션에 공통 방문자 ID를 설정합니다. 또한 고유한 고객 ID를 서비스로 보내어 장치 간 타깃팅 및 CRM(고객 관계 관리) 시스템과 같은 다른 시스템과의 통합을 가능하게 할 수 있습니다.

웹 사이트에서 이미 방문자 API 또는 Experience Cloud ID 서비스 태그 확장 기능을 통해 웹 사이트에서 Experience Cloud ID 서비스를 사용하고 있으며, Adobe Experience Platform Web SDK로 마이그레이션하는 동안 계속 사용하려면, 최신 버전의 방문자 API 또는 Experience Cloud ID 서비스 태그 확장 기능을 사용해야 합니다. 다음을 참조하십시오 [ID 마이그레이션](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en) 추가 정보.

>[!NOTE]
>
> 이 단원의 연습에서는 데모용으로 가상 고객에 로그인한 ID의 세부 정보를 캡처합니다. [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html) 자격 증명을 사용하여 **사용자: test@adobe.com / 암호: test**. 이러한 단계를 사용하여 고유한 목적을 위해 다른 ID를 만들 수 있지만 데이터 수집 인터페이스에서 ID 맵의 기능을 알아보려면 먼저 예제 ID를 캡처하는 방법을 따르는 것이 좋습니다.

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* ID 네임스페이스 이해
* 사용자 정의 ID 네임스페이스를 만들어 내부 CRM ID 캡처


## 전제 조건

다음 이전 단원을 이미 완료했을 것입니다.

* [권한 구성](configure-permissions.md)
* [스키마 구성](configure-schemas.md)

>[!IMPORTANT]
>
>다음 [Experience Cloud ID 확장](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) 웹 SDK JavaScript 라이브러리에는 방문자 ID 서비스 기능이 포함되어 있으므로 Adobe Experience Platform 웹 SDK를 구현할 때에는 이 필요하지 않습니다.

## ID 네임스페이스 만들기

이 연습에서는 Luma의 사용자 지정 ID 필드에 대한 ID 네임스페이스를 만듭니다. `lumaCrmId`. 동일한 네임스페이스 내에 일치하는 두 값이 있으면 두 개의 데이터 소스가 하나의 아이덴티티 그래프를 구성할 수 있기 때문에 신원 네임스페이스는 실시간 고객 프로필을 작성하는 데 중요한 역할을 합니다.

연습을 시작하기 전에 이 짧은 비디오를 통해 Adobe Experience Platform의 ID에 대해 자세히 알아보십시오.
>[!VIDEO](https://video.tv.adobe.com/v/27841?learn=on)

이제 Luma CRM ID에 대한 네임스페이스를 만듭니다.

1. 를 엽니다. [데이터 수집 인터페이스](https://launch.adobe.com/){target="_blank"}
1. 자습서에 사용할 샌드박스를 선택합니다

   >[!NOTE]
   >
   >Real-Time CDP과 같은 플랫폼 기반 애플리케이션의 고객인 경우 이 자습서에서는 개발 샌드박스를 사용하는 것이 좋습니다. 그렇지 않으면 **[!UICONTROL Prod]** 샌드박스.

1. 선택 **[!UICONTROL ID]** 왼쪽 탐색
1. 선택 **[!UICONTROL 찾아보기]**

   페이지의 기본 인터페이스에 ID 네임스페이스 목록이 표시되어 이름, ID 기호, 마지막으로 업데이트된 날짜 및 표준 네임스페이스인지 사용자 정의 네임스페이스인지 여부를 보여 줍니다. 오른쪽 레일에는 ID 그래프 강도에 대한 정보가 포함되어 있습니다.

1. **[!UICONTROL 신원 네임스페이스 만들기]**&#x200B;를 선택합니다

   ![ID 보기](assets/configure-identities-screen.png)

1. 다음과 같이 세부 정보를 입력하고 을(를) 선택합니다 **[!UICONTROL 만들기]**.

   | 필드 | 값 |
   |---------------|-----------|
   | 표시 이름 | Luma CRM ID |
   | ID 심볼 | lumaCrmId |
   | 유형 | 교차 장치 ID |


   ![네임스페이스 만들기](assets/identities-create-namespace.png)


   ID 네임스페이스는 **[!UICONTROL ID]** 화면.

   ![네임스페이스 만들기](assets/configure-identities-namespace-lumaCrmId.png)


>[!INFO]
>
> 다음에서 [데이터 요소 만들기](create-data-elements.md) 단원: Platform Edge Network에 ID를 전송할 때 이 네임스페이스를 사용하는 방법을 알아봅니다.

## 프로덕션 샌드박스에서 ID 네임스페이스 만들기

웹 SDK 확장의 현재 제한으로 인해 네임스페이스를 사용하여 개발 샌드박스로 데이터를 전송하려면 프로덕션 샌드박스에도 ID 네임스페이스를 만들어야 합니다. 따라서 이 자습서에서 개발 샌드박스를 사용하고 있는 경우 `Luma CRM ID` 프로덕션 샌드박스의 네임스페이스.

## 추가 리소스

* [Identity Service 설명서](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=ko-KR)
* [ID 서비스 API](https://www.adobe.io/experience-platform-apis/references/identity-service/)

ID가 준비되었으므로 데이터 스트림을 구성할 수 있습니다.

[다음: ](configure-datastream.md)

>[!NOTE]
>
>Adobe Experience Platform Web SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나, 일반적인 피드백을 공유하거나, 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오. [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
