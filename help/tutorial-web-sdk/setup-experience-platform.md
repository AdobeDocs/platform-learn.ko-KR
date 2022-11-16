---
title: 웹 SDK를 사용하여 데이터를 Adobe Experience Platform으로 스트리밍
description: Web SDK를 사용하여 웹 데이터를 Adobe Experience Platform에 스트리밍하는 방법을 알아봅니다. 이 단원은 웹 SDK를 사용하여 Adobe Experience Cloud 구현 자습서의 일부입니다.
exl-id: 4d749ffa-e1c0-4498-9b12-12949807b369
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 5%

---

# 웹 SDK를 사용하여 데이터를 Experience Platform으로 스트리밍

Platform Web SDK를 사용하여 Adobe Experience Platform으로 웹 데이터를 스트리밍하는 방법을 알아봅니다.

Experience Platform은 Adobe Real-time Customer Data Platform, Adobe Customer Journey Analytics 및 Adobe Journey Optimizer과 같은 모든 새로운 Experience Cloud 애플리케이션의 백본입니다. 이러한 응용 프로그램은 웹 데이터 수집을 위한 최적의 방법으로 Platform Web SDK를 사용하도록 설계되었습니다.

Experience Platform은 이전에 만든 것과 동일한 XDM 스키마를 사용하여 Luma 웹 사이트에서 이벤트 데이터를 캡처합니다. 해당 데이터가 Platform Edge Network로 전송되면 데이터 스트림 구성에서 이 데이터를 Experience Platform에 전달할 수 있습니다.

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* Adobe Experience Platform 내에서 데이터 세트 만들기
* Web SDK 데이터를 Adobe Experience Platform에 보내도록 데이터 스트림을 구성합니다
* 실시간 고객 프로필을 위한 스트리밍 웹 데이터 활성화
* 데이터가 Platform 데이터 세트와 실시간 고객 프로필에 모두 전달되었는지 확인합니다

## 전제 조건

다음 단원을 이미 완료했어야 합니다.

* 다음 **초기 구성** 단원:
   * [권한 구성](configure-permissions.md)
   * [XDM 스키마 구성](configure-schemas.md)
   * [데이터 스트림 구성](configure-datastream.md)
   * [ID 네임스페이스 구성](configure-identities.md)

* 다음 **태그 구성** 단원:
   * [웹 SDK 확장 설치](install-web-sdk.md)
   * [데이터 요소 만들기](create-data-elements.md)
   * [태그 규칙 만들기](create-tag-rule.md)


## 데이터 집합 만들기

Adobe Experience Platform에 성공적으로 수집된 모든 데이터는 데이터 레이크 내에서 데이터 세트로 유지됩니다. A [데이터 세트](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=en) 는 스키마(열) 및 필드(행)를 포함하는 데이터 수집을 위한 저장 및 관리 구성입니다. 데이터 세트에는 저장하는 데이터의 다양한 측면을 설명하는 메타데이터도 포함됩니다.

이 연습에서는 다음에 대한 콘텐츠 및 전자 상거래 세부 사항을 추적하는 데이터 세트를 만듭니다 [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html).

>[!WARNING]
>
>이미 을(를) 만들어야 합니다. `Luma Web Event Data` 이전 단원에서 설명한 대로 스키마 [XDM 스키마 구성](configure-schemas.md).


1. 로 이동합니다. [Experience Platform 인터페이스](https://experience.adobe.com/platform/)
1. 이 자습서에서 사용하는 개발 샌드박스에 있는지 확인하십시오
1. 열기 **[!UICONTROL 데이터 세트]** 왼쪽 탐색에서
1. 선택 **[!UICONTROL 데이터 집합 만들기]**

   ![스키마 만들기](assets/experience-platform-create-dataset.png)

1. 을(를) 선택합니다 **[!UICONTROL 스키마에서 데이터 집합 만들기]** 옵션

   ![스키마에서 데이터 집합 만들기](assets/experience-platform-create-dataset-schema.png)

1. 을(를) 선택합니다 `Luma Web Event Data` 에서 만들어진 스키마 [이전 단원](configure-schemas.md) 그런 다음 **[!UICONTROL 다음]**

   ![데이터 집합, 스키마 선택](assets/experience-platform-create-dataset-schema-selection.png)

1. 다음을 제공합니다. **[!UICONTROL 이름]** 및 옵션 **[!UICONTROL 설명]** 참조하십시오. 이 연습에서는 `Luma Web Event Data`를 선택하고 을 선택합니다. **[!UICONTROL 완료]**

   ![데이터 집합 이름 ](assets/experience-platform-create-dataset-schema-name.png)

이제 데이터 세트가 Platform Web SDK 구현에서 데이터 수집을 시작하도록 구성되어 있습니다.

## 데이터 스트림 구성

이제 다음을 구성할 수 있습니다 [!UICONTROL 데이터 스트림] 데이터를에 보내기 [!UICONTROL Adobe Experience Platform]. 데이터 스트림은 태그 속성, Platform Edge 네트워크 및 Experience Platform 데이터 세트 간의 링크입니다.

1. 를 엽니다. [데이터 수집](https://experience.adobe.com/#/data-collection){target=&quot;blank&quot;} 인터페이스
1. 선택 **[!UICONTROL 데이터 스트림]** 왼쪽 탐색에서
1. 에서 만든 데이터 스트림을 엽니다. [데이터 스트림 구성](configure-datastream.md) 수업 `Luma Web SDK`

   ![Luma Web SDK 데이터 스트림을 선택합니다](assets/datastream-luma-web-sdk.png)

1. 선택 **[!UICONTROL 서비스 추가]**

   ![데이터 스트림에 서비스 추가](assets/experience-platform-addService.png)
1. 선택 **[!UICONTROL Adobe Experience Platform]** 로서의 **[!UICONTROL 서비스]**
1. 선택 `Luma Web Event Data` 로서의 **[!UICONTROL 이벤트 데이터 세트]**

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

   ![데이터 스트림 구성](assets/experience-platform-datastream-config.png)

에서 트래픽을 생성할 때 [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html) 태그 속성에 매핑되면 데이터가 Experience Platform에서 데이터 세트를 채웁니다!

## 데이터 집합 유효성 검사

이 단계는 데이터가 데이터 세트에 도달했는지 확인하는 데 중요합니다. 데이터 집합에 전송된 데이터의 유효성을 검사하는 두 가지 측면이 있습니다.

* 을 사용하여 유효성 검사 [!UICONTROL Experience Platform 디버거]
* 을 사용하여 유효성 검사 [!UICONTROL 데이터 집합 미리 보기]
* 을 사용하여 유효성 검사 [!UICONTROL 쿼리 서비스]

### Experience Platform Debugger

이러한 단계는 [Debugger 단원](validate-with-debugger.md). 하지만 데이터는 데이터 스트림에서 활성화한 후에만 Platform으로 전송되므로 몇 가지 샘플 데이터를 생성해야 합니다.

1. 를 엽니다. [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html) 을(를) 선택하고 을(를) 선택합니다. [!UICONTROL Experience Platform 디버거] 확장 아이콘

1. 태그 속성을 *your* 에 설명된 대로 개발 환경 [디버거를 사용하여 유효성 검사](validate-with-debugger.md) 단원

   ![디버거에 표시된 Launch 개발 환경](assets/experience-platform-debugger-dev.png)

1. 자격 증명 `test@adobe.com`/`test`를 사용하여 Luma 사이트에 로그인합니다.

1. [Luma 홈 페이지](https://luma.enablementadobe.com/content/luma/us/en.html)로 돌아갑니다.

1. 디버거에 의해 표시되는 Platform Web SDK 네트워크 비콘 내에서 &quot;events&quot; 행을 선택하여 팝업에서 세부 사항을 확장합니다

   ![디버거의 웹 SDK](assets/experience-platform-debugger-dev-eventType.png)

1. 팝업 내에서 &quot;identityMap&quot;을 검색합니다. 여기서는 authenticatedState, id 및 primary 키 3개가 있는 lumaCrmId가 표시됩니다
   ![디버거의 웹 SDK](assets/experience-platform-debugger-dev-idMap.png)

이제 데이터를 `Luma Web Event Data` 데이터 집합 및 &#39;데이터 집합 미리 보기&#39; 유효성 검사 준비

### 데이터 집합 미리 보기

데이터가 플랫폼의 데이터 레이크에 도달했는지 확인하려면 **[!UICONTROL 데이터 세트 미리 보기]** 기능. Web SDK 데이터는 데이터 레이크에 마이크로 배치되고 주기적으로 Platform 인터페이스에서 새로 고침됩니다. 생성한 데이터를 보려면 10~15분이 걸릴 수 있습니다.

1. 에서 [Experience Platform](https://experience.adobe.com/platform/) 인터페이스, 선택 **[!UICONTROL 데이터 세트]** 왼쪽 탐색에서 를 클릭하여 **[!UICONTROL 데이터 세트]** 대시보드 .

   대시보드는 조직에 대해 사용 가능한 모든 데이터 세트를 나열합니다. 세부 사항은 해당 이름, 데이터 세트가 준수하는 스키마 및 가장 최근 수집 실행 상태를 포함하여 나열된 각 데이터 세트에 대해 표시됩니다.

1. 을(를) 선택합니다 `Luma Web Event Data` 데이터 세트를 열어 **[!UICONTROL 데이터 집합 활동]** 화면.

   ![데이터 집합 Luma 웹 이벤트](assets/experience-platform-dataset-validation-lumaSDK.png)

   활동 화면에는 성공적인 배치와 실패한 배치 목록과 함께 사용 중인 메시지 수를 시각화하는 그래프가 포함되어 있습니다.

1. 에서 **[!UICONTROL 데이터 집합 활동]** 화면, 선택 **[!UICONTROL 데이터 세트 미리 보기]** 최대 100개의 데이터 행을 미리 보려면 화면의 오른쪽 상단 모서리 근처에 있습니다. 데이터 세트가 비어 있으면 미리 보기 링크가 비활성화됩니다.

   ![데이터 집합 미리 보기](assets/experience-platform-dataset-preview.png)

   미리 보기 창에서 데이터 세트에 대한 스키마의 계층 구조 보기가 오른쪽에 표시됩니다.

   ![데이터 집합 미리 보기 1](assets/experience-platform-dataset-preview-1.png)

>[!INFO]
>
>Adobe Experience Platform의 쿼리 서비스는 호수에서 데이터를 확인하는 보다 강력한 방법이지만 이 자습서의 범위를 벗어납니다. 자세한 내용은 [데이터 탐색](https://experienceleague.adobe.com/docs/platform-learn/tutorials/queries/explore-data.html?lang=ko-KR) 를 참조하십시오.


## 실시간 고객 프로필에 대한 데이터 세트 및 스키마 활성화

다음 단계는 실시간 고객 프로필을 위한 데이터 세트 및 스키마를 활성화하는 것입니다. 웹 SDK에서 데이터 스트리밍은 플랫폼으로 유입되는 많은 데이터 소스 중 하나이며 웹 데이터를 다른 데이터 소스와 통합하여 360도 고객 프로필을 빌드하려고 합니다. 실시간 고객 프로필에 대해 자세히 알려면 다음 짧은 비디오를 시청하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12&learn=on&captions=eng)

>[!CAUTION]
>
>자체 웹 사이트 및 데이터를 사용하여 작업하는 경우 실시간 고객 프로필에 대해 활성화하기 전에 데이터에 대한 강력한 유효성 검사가 권장됩니다.


**데이터 세트를 사용하려면**

1. 만든 데이터 세트를 엽니다. `Luma Web Event Data`

1. 을(를) 선택합니다 **[!UICONTROL 프로필 전환]** 켜는 것

   ![프로필 전환](assets/setup-experience-platform-profile.png)

1. 확인 **[!UICONTROL 활성화]** 데이터 집합

   ![프로필 활성화 전환](assets/setup-experience-platform-profile-enable.png)

**스키마를 활성화하려면**

1. 생성한 스키마를 엽니다. `Luma Web Event Data`

1. 을(를) 선택합니다 **[!UICONTROL 프로필 전환]** 켜는 것

   ![프로필 전환](assets/setup-experience-platform-profile-schema.png)

1. 선택 **[!UICONTROL 이 스키마의 데이터에 identityMap 필드에 기본 ID가 포함됩니다.]**

   >[!IMPORTANT]
   >
   >    실시간 고객 프로필로 전송된 모든 레코드에는 기본 ID가 필요합니다. 일반적으로 ID 필드는 스키마 내에 레이블이 지정됩니다. 그러나 ID 맵을 사용하는 경우 스키마 내에 ID 필드가 표시되지 않습니다. 이 대화 상자는 기본 ID를 염두에 두고 데이터를 전송할 때 ID 맵에 지정할지 확인하는 것입니다. 아시다시피 Web SDK는 ID 맵을 사용하고 ECID(Experience Cloud ID)는 기본 기본 ID입니다.


1. 선택 **[!UICONTROL 활성화]**

   ![프로필 활성화 전환](assets/setup-experience-platform-profile-schema-enable.png)

1. 선택 **[!UICONTROL 저장]** 업데이트된 스키마를 저장하려면

이제 프로필에 대해서도 스키마가 활성화되어 있습니다.

>[!IMPORTANT]
>
>    프로필에 대해 스키마를 활성화하면 비활성화하거나 삭제할 수 없습니다. 또한 이 시점 후에는 스키마에서 필드를 제거할 수 없습니다. 이러한 의미는 나중에 프로덕션 환경에서 자체 데이터를 사용할 때 기억해야 합니다. 이 자습서에서는 언제든지 삭제할 수 있는 개발 샌드박스를 사용해야 합니다.
>
>   
> 자체 데이터를 사용하여 작업하는 경우 다음 순서로 작업을 수행하는 것이 좋습니다.
> 
> * 먼저 일부 데이터를 데이터 세트에 수집합니다.
> * 데이터 수집 프로세스 중에 발생하는 모든 문제(예: 데이터 유효성 검사 또는 매핑 문제)를 해결합니다.
> * 프로필에 대한 데이터 세트 및 스키마 활성화
> * 데이터 다시 수집



### 프로필 유효성 검사

플랫폼 인터페이스(또는 Journey Optimizer 인터페이스)에서 고객 프로필을 확인하여 데이터가 실시간 고객 프로필에 도달했는지 확인할 수 있습니다. 이름에서 알 수 있듯이 프로필은 실시간으로 채워지므로 데이터 집합에 있는 데이터의 유효성을 검사하는 것과 같은 지연이 없습니다.

먼저 샘플 데이터를 더 생성해야 합니다. 태그 속성에 매핑되면 이 단원의 이전 단계부터 Luma 웹 사이트에 로그인하여 해당 웹 사이트에 로그인합니다. Inspect이 Platform Web SDK를 요청하여 `lumaCRMId`.

1. 에서 [Experience Platform](https://experience.adobe.com/platform/) 인터페이스, 선택 **[!UICONTROL 프로필]** 왼쪽 탐색

1. 로서의 **[!UICONTROL ID 네임스페이스]** 사용 `lumaCRMId`
1. 의 값을 복사하여 붙여넣습니다 `lumaCRMId` Experience Platform 디버거에서 검사한 호출을 전달했습니다. `112ca06ed53d3db37e4cea49cc45b71e`).

   ![프로필](assets/experience-platform-validate-dataset-profile.png)

1. 프로필에 `lumaCRMId`: 프로필 ID가 콘솔에서 채워집니다.

   ![프로필](assets/experience-platform-validate-dataset-profile-set.png)

1. 을(를) 클릭하여 [!UICONTROL 프로필 ID] 그리고 [!UICONTROL 고객 프로필] 콘솔을 채웁니다. 여기에서 `lumaCRMId`예: `ECID`:

   ![고객 프로필](assets/experience-platform-validate-dataset-custProfile.png)

이제 Experience Platform(및 실시간 CDP)를 위해 Platform Web SDK를 활성화했습니다! 그리고 Customer Journey Analytics! 그리고 Journey Optimizer!)!


[다음: ](setup-analytics.md)

>[!NOTE]
>
>Adobe Experience Platform Web SDK에 대한 학습에 시간을 내주셔서 감사합니다. 질문이 있거나 일반 피드백을 공유하거나 향후 컨텐츠에 대한 제안 사항이 있는 경우 해당 정보를 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)