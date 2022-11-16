---
title: 데이터 집합 만들기
description: 데이터 집합 만들기
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 7705d292-a29c-4977-bcc6-f088a51713ea
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 4%

---

# 데이터 집합 만들기

Adobe Experience Platform으로 전송할 데이터를 설명하는 것 외에도 데이터를 유지할 장소가 필요합니다. Adobe Experience Platform에서 데이터를 배치할 수 있는 이러한 버킷을 데이터 세트라고 합니다.

데이터 세트를 만들려면 [!UICONTROL 데이터 세트] Adobe Experience Platform 내부 보기

![데이터 세트 보기](../../../assets/implementation-strategy/datasets-view.png)

클릭 [!UICONTROL 데이터 집합 만들기] 오른쪽 상단 모서리에서

데이터 집합 생성 프로세스 중에 [!UICONTROL 스키마에서 데이터 집합 만들기] 을(를) 선택합니다. [이전에 만든 스키마](create-a-schema.md).

![스키마 선택](../../../assets/implementation-strategy/schema-selection.png)

클릭 [!UICONTROL 다음] 이름과 설명을 입력합니다.

![데이터 집합 이름 및 설명](../../../assets/implementation-strategy/dataset-name-description.png)

[!UICONTROL 마침을 클릭합니다]. 데이터 세트가 만들어져서 데이터를 받을 준비가 되었습니다.

데이터 집합에 데이터를 보내기 시작하면 Adobe Experience Platform에서 데이터 집합에 배치하려는 데이터가 적용된 스키마를 준수하는지 확인합니다. 데이터가 스키마를 따르지 않으면 데이터가 거부되고 데이터 집합에 배치되지 않습니다. 이 유효성 검사 단계의 결과로 데이터 집합(Adobe 제품, 타사 또는 사용자 회사)의 소비자는 데이터 집합 데이터의 구조 및 청결에 대해 어느 정도 확신을 가질 수 있습니다.

데이터 세트 만들기에 대한 자세한 내용은 [데이터 세트 UI 안내서](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=ko).
