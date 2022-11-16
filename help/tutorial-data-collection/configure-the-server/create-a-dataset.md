---
title: 데이터 집합 만들기
description: 데이터 집합 만들기
exl-id: 19a60087-2f78-4510-b127-b1007a6b7a56
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# 데이터 집합 만들기

Adobe Experience Platform으로 보내는 데이터를 설명하는 것 외에도 데이터를 유지할 장소가 필요합니다. Adobe Experience Platform에서 데이터를 배치할 수 있는 이러한 버킷을 데이터 세트라고 합니다.

>[!NOTE]
>
>데이터 세트는 Platform Web SDK를 사용하여 Adobe Analytics, Adobe Target 및 Adobe Audience Manager으로 데이터를 보내거나 이벤트 전달을 사용하는 경우에만 필요하지 않습니다. 그러한 목적으로 Web SDK만 사용하는 경우 자습서의 이 페이지를 건너뛸 수 있습니다.

1. 선택 **[!UICONTROL 데이터 세트]** 아래에 [!UICONTROL 데이터 관리] Adobe Experience Platform의 왼쪽 메뉴에서 를 클릭합니다.
1. 다음으로, **[!UICONTROL 데이터 집합 만들기]** 오른쪽 상단 모서리의 명령.
   ![데이터 세트 보기](../assets/datasets-view.png)

## 스키마에서 데이터 집합 만들기

1. 에서 [!UICONTROL 워크플로우] 인터페이스에서 첫 번째 타일을 선택하고 **[!UICONTROL 스키마에서 데이터 집합 만들기]**.
1. 을 검색합니다. [이전에 만든 스키마](create-a-schema.md) 그리고 선택합니다.
   ![스키마 선택](../assets/schema-selection.png)
1. 선택 **[!UICONTROL 다음]** 이름과 설명을 입력합니다.
   ![데이터 집합 이름 및 설명](../assets/dataset-name-description.png)
1. 선택 **[!UICONTROL 완료]**. 데이터 세트가 만들어져서 데이터를 받을 준비가 되었습니다.

데이터 집합에 데이터를 보내기 시작할 때 Adobe Experience Platform은 데이터 집합에 배치하려는 데이터가 적용된 스키마를 준수하는지 확인합니다. 데이터가 스키마를 따르지 않으면 데이터가 거부되고 데이터 집합에 배치되지 않습니다. 이 유효성 검사 단계의 결과로 데이터 집합(Adobe 제품, 타사 또는 사용자 회사)의 소비자는 데이터 집합 데이터의 구조 및 청결에 대해 어느 정도 확신을 가질 수 있습니다.

데이터 세트 만들기에 대한 자세한 내용은 [데이터 세트 만들기 및 데이터 수집](/help/platform/data-ingestion/create-datasets-and-ingest-data.md).

[다음: ](create-a-datastream.md)

>[!NOTE]
>
>데이터 수집에 시간을 내어 주셔서 감사합니다. 질문이 있거나 일반 피드백을 공유하거나 향후 컨텐츠에 대한 제안 사항이 있는 경우 해당 정보를 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)

