---
title: Platform Mobile SDK를 사용하여 Experience Platform에 데이터 전송
description: Experience Platform으로 데이터를 전송하는 방법에 대해 알아봅니다.
solution: Data Collection,Experience Platform
feature: Mobile SDK,Data Ingestion
jira: KT-14637
exl-id: fdd2c90e-8246-4d75-a6db-df3ef31946c4
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 2%

---

# Experience Platform으로 데이터 보내기

모바일 앱 데이터를 Adobe Experience Platform으로 전송하는 방법에 대해 알아봅니다.

이 선택적 단원은 Real-time Customer Data Platform(Real-Time CDP), Journey Optimizer 및 Customer Journey Analytics의 모든 고객과 관련이 있습니다. Experience Cloud 제품의 기반인 Experience Platform은 모든 데이터(Adobe 및 비Adobe)를 강력한 고객 프로필로 변환하는 개방형 시스템입니다. 이러한 고객 프로필은 실시간으로 업데이트되며 AI 기반 인사이트를 사용하여 모든 채널에 적합한 경험을 제공할 수 있습니다.

이전 단원에서 Platform Edge Network으로 수집 및 전송한 [event](events.md), [lifecycle](lifecycle-data.md) 및 [identity](identity.md) 데이터는 Adobe Experience Platform을 포함하여 데이터 스트림에 구성된 서비스로 전달됩니다.

![아키텍쳐](assets/architecture-aep.png)


## 전제 조건

Adobe Experience Platform에 대해 조직이 프로비저닝되고 권한이 부여되어야 합니다.

액세스 권한이 없는 경우 [이 단원을 건너뛰세요](install-sdks.md).

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* Experience Platform 데이터 세트를 만듭니다.
* 데이터를 Experience Platform에 전달하도록 데이터 스트림을 구성합니다.
* 데이터 세트의 데이터를 확인합니다.
* 실시간 고객 프로필에 대한 스키마 및 데이터 세트를 활성화합니다.
* 실시간 고객 프로필에서 데이터의 유효성을 검사합니다.
* ID 그래프에서 데이터의 유효성을 검사합니다.


## 데이터 세트 만들기

Adobe Experience Platform에 성공적으로 수집된 모든 데이터는 데이터 세트로 데이터 레이크 내에 유지됩니다. 데이터 집합은 스키마(열) 및 필드(행)를 포함하는 데이터 컬렉션(일반적으로 테이블)에 대한 저장소 및 관리 구성입니다. 데이터 세트에는 저장하는 데이터의 다양한 측면을 설명하는 메타데이터도 포함됩니다. 자세한 내용은 [설명서](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=ko)를 참조하세요.

1. 오른쪽 상단의 앱 ![앱](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) 메뉴에서 Experience Platform 인터페이스를 선택하여 해당 인터페이스로 이동합니다.


1. 왼쪽 탐색 메뉴에서 **[!UICONTROL 데이터 세트]**&#x200B;를 선택합니다.

1. ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 데이터 집합 만들기]**&#x200B;를 선택합니다.

1. **[!UICONTROL 스키마에서 데이터 집합 만들기]**를 선택합니다.
   ![데이터 집합 홈](assets/dataset-create.png)

1. 스키마를 검색합니다. 예를 들어 검색 필드에서 `Luma Mobile`을(를) 사용하는 경우가 있습니다.
1. 스키마를 선택하세요(예: **[!DNL Luma Mobile App Event Schema]**).

1. **[!UICONTROL 다음]**을 선택합니다.
   ![데이터 집합 구성](assets/dataset-configure.png)

1. **[!UICONTROL 이름]**(예: `Luma Mobile App Events Dataset` 및 **[!UICONTROL 설명]**)을 제공하십시오.

1. **[!UICONTROL 마침]**을 선택합니다.
   ![데이터 집합 완료](assets/dataset-finish.png)


## Adobe Experience Platform 데이터스트림 서비스 추가

Edge Network에서 Adobe Experience Platform으로 XDM 데이터를 보내려면 [데이터 스트림 만들기](create-datastream.md)의 일부로 설정한 데이터 스트림에 Adobe Experience Platform 서비스를 추가하십시오.

>[!IMPORTANT]
>
>이벤트 데이터 세트를 만든 경우에만 Adobe Experience Platform 서비스를 활성화할 수 있습니다.

1. 데이터 수집 UI에서 **[!UICONTROL 데이터스트림]** 및 데이터스트림을 선택합니다.

1. ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 서비스 추가]**&#x200B;를 선택합니다.

1. [!UICONTROL 서비스] 목록에서 **[!UICONTROL Adobe Experience Platform]**&#x200B;을(를) 선택하십시오.

1. **[!UICONTROL 사용]**&#x200B;을(를) 전환하여 서비스를 사용하도록 설정하십시오.

1. 이전에 만든 **[!UICONTROL 이벤트 데이터 세트]**(예: **[!DNL Luma Mobile App Event Dataset]**)를 선택하십시오.

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

   ![데이터 스트림 서비스로 Adobe Experience Platform 추가](assets/datastream-service-aep.png)
1. 최종 구성은 다음과 같아야 합니다.

   ![데이터 스트림 설정](assets/datastream-settings.png)


## 데이터 세트의 데이터 유효성 검사

데이터 세트를 만들고 데이터 스트림을 업데이트하여 Experience Platform으로 데이터를 전송했으므로 Platform Edge Network으로 전송된 모든 XDM 데이터는 Platform으로 전달되고 데이터 세트에 도달합니다.

앱을 열고 이벤트를 추적하는 화면으로 이동합니다. 라이프사이클 지표를 트리거할 수도 있습니다.

플랫폼 인터페이스에서 데이터 세트를 엽니다. 데이터가 데이터 세트에 일괄적으로 도착하는 것을 볼 수 있습니다. 데이터는 일반적으로 15분마다 마이크로 배치로 도착하므로 데이터가 즉시 표시되지 않을 수 있습니다.

![데이터 랜딩 플랫폼 데이터 집합 배치 유효성 검사](assets/platform-dataset-batches.png)

또한 **[!UICONTROL 데이터 집합 미리 보기]** 기능을 사용하여 예제 레코드와 필드를 볼 수 있습니다.
![Platform 데이터 세트로 전송된 라이프사이클 유효성 검사](assets/lifecycle-platform-dataset.png)

데이터 유효성 검사를 위한 보다 강력한 도구는 플랫폼의 [쿼리 서비스](https://experienceleague.adobe.com/docs/platform-learn/tutorials/queries/explore-data.html?lang=ko-KR)입니다.

## 실시간 고객 프로필 활성화

Experience Platform의 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 서드파티 데이터를 비롯한 여러 채널의 데이터를 결합하는 각 개별 고객에 대한 거시적인 보기를 구축할 수 있습니다. 프로필을 사용하면 서로 다른 고객 데이터를 하나의 통합 보기로 통합하여 모든 고객 상호 작용에 대해 실행 가능한 타임스탬프 계정을 제공할 수 있습니다.

### 스키마 활성화

1. 스키마를 엽니다(예: **[!DNL Luma Mobile App Event Schema]**).
1. **[!UICONTROL 프로필]**&#x200B;을 사용하도록 설정합니다.
1. 이 스키마에 대한 **[!UICONTROL 데이터를 선택하면 identityMap 필드에 기본 ID가 포함됩니다.대화 상자의]**.
1. 스키마를 **[!UICONTROL 저장]**&#x200B;합니다.

   ![프로필에 대해 스키마 사용](assets/platform-profile-schema.png)

### 데이터 세트 활성화

1. 데이터 집합(예: **[!DNL Luma Mobile App Event Dataset]**)을 엽니다.
1. **[!UICONTROL 프로필]**&#x200B;을 사용하도록 설정합니다.

   ![프로필에 대한 데이터 세트 활성화](assets/platform-profile-dataset.png)

### 프로필의 데이터 유효성 검사

앱을 열고 이벤트를 추적할 화면으로 이동합니다. 예: Luma 앱에 로그인하고 구매합니다.

Assurance를 사용하여 identityMap에서 전달된 ID 중 하나(이메일, lumaCrmId 또는 ECID)(예: CRM ID)를 찾습니다.

![ID 값 가져오기](assets/platform-identity.png)

Platform 인터페이스에서

1. **[!UICONTROL 프로필]**(으)로 이동한 다음 상단 막대에서 **[!UICONTROL 찾아보기]**&#x200B;를 선택합니다.
1. 방금 가져온 ID 세부 정보(예: **[!UICONTROL ID 네임스페이스]**&#x200B;에 대한 `Luma CRM ID` 및 **[!UICONTROL ID 값]**&#x200B;에 대해 복사한 값)를 지정하십시오. **[!UICONTROL 보기]**&#x200B;를 선택합니다.
1. 세부 정보를 보려면 프로필을 선택합니다.

![ID 값 조회](assets/platform-profile-lookup.png)

**[!UICONTROL 세부 정보]** 화면에서 **[!UICONTROL **&#x200B;연결된 ID **]**를 포함하여 사용자에 대한 기본 정보를 볼 수 있습니다.
![프로필 세부 정보](assets/platform-profile-details.png)

**[!UICONTROL 이벤트]**&#x200B;에서 이 사용자의 모바일 앱 구현에서 수집된 이벤트를 볼 수 있습니다.

![프로필 이벤트](assets/platform-profile-events.png)


프로필 세부 사항 화면에서 다음을 수행합니다.

1. ID 그래프를 보려면 링크를 클릭하거나 **[!UICONTROL ID]**(으)로 이동한 다음 상단 막대에서 **[!UICONTROL ID 그래프]**&#x200B;을(를) 선택하십시오.
1. ID 값을 조회하려면 `Luma CRM ID`을(를) **[!UICONTROL ID 네임스페이스]**(으)로 지정하고 복사된 값을 **[!UICONTROL ID 값]**(으)로 지정합니다. **[!UICONTROL 보기]**&#x200B;를 선택합니다.

   이 시각화는 프로필에 함께 연결된 모든 ID와 해당 출처를 보여 줍니다. 다음은 이 Mobile SDK 자습서(데이터 Source 2)와 [Web SDK 자습서](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=ko-KR)(데이터 Source 1)를 모두 완료하여 수집된 데이터로 구성된 ID 그래프의 예입니다.

   ![ID 값 가져오기](assets/platform-profile-identitygraph.png)


## 다음 단계

Customer Journey Analytics에서 분석하고 Real-time Customer Data Platform에서 세그먼트를 작성하는 작업을 포함하여 마케터와 분석가가 Experience Platform에서 캡처한 데이터로 수행할 수 있는 작업이 훨씬 더 많습니다. 출발이 좋으시네요!


>[!SUCCESS]
>
>이제 Edge Network은 물론 Adobe Experience Platform에도 데이터를 전송하도록 앱을 설정했습니다.<br>Adobe Experience Platform Mobile SDK에 대한 학습에 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하고 싶거나 향후 콘텐츠에 대한 제안이 있는 경우 이 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)에서 공유하십시오.

다음: **[푸시 알림 만들기 및 보내기](journey-optimizer-push.md)**
