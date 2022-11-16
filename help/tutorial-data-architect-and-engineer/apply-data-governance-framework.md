---
title: 데이터 거버넌스 프레임워크 적용
seo-title: Apply the data governance framework | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 데이터 거버넌스 프레임워크 적용
description: 이 단원에서는 데이터 거버넌스 프레임워크를 샌드박스에 섭취시킨 데이터에 적용합니다.
role: Data Architect
feature: Data Governance
kt: 4348
thumbnail: 4348-apply-data-governance-framework.jpg
exl-id: 3cc3c794-5ffd-41bf-95d8-be5bca2e3a0f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 2%

---

# 데이터 거버넌스 프레임워크 적용

<!--15min-->

이 단원에서는 데이터 거버넌스 프레임워크를 샌드박스에 섭취시킨 데이터에 적용합니다.

Adobe Experience Platform 데이터 거버넌스를 사용하면 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 및 정책을 준수할 수 있습니다. 데이터 사용 제어를 포함하여 다양한 수준에서 Experience Platform 내에서 주요 역할을 합니다.

연습을 시작하기 전에 데이터 거버넌스에 대한 다음 간단한 비디오를 시청하십시오.
>[!VIDEO](https://video.tv.adobe.com/v/36653?quality=12&learn=on)

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&learn=on)

<!--
## Permissions required

In the [Configure Permissions](configure-permissions.md) lesson, you set up all the access controls required to complete this lesson, specifically:

* Permission items **[!UICONTROL Data Governance]** > **[!UICONTROL Manage Usage Labels]**, **[!UICONTROL Manage Data Usage Policies]** and **[!UICONTROL View Data Usage Policies]**
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` Product Profile
-->

## 비즈니스 시나리오

Luma는 충성도 프로그램의 구성원에게 충성도 데이터가 제3자와 공유되지 않을 것을 약속합니다. 이 시나리오는 나머지 단원에서 구현합니다.

## 데이터 거버넌스 레이블 적용

데이터 거버넌스 프로세스의 첫 번째 단계는 데이터에 거버넌스 레이블을 적용하는 것입니다. 이 작업을 수행하기 전에 사용 가능한 레이블을 간단히 살펴보겠습니다.

1. Platform 사용자 인터페이스에서 을(를) 선택합니다 **[!UICONTROL 정책]** 왼쪽 탐색
1. 로 이동합니다. **[!UICONTROL 레이블]** 탭에서 계정의 모든 레이블을 볼 수 있습니다.

기본 제공 레이블이 많이 있으며 를 통해 직접 만들 수 있습니다. [!UICONTROL 레이블 만들기] 버튼을 클릭합니다. 다음 세 가지 주요 유형이 있습니다. [!UICONTROL 계약 레이블], [!UICONTROL ID 레이블], 및 [!UICONTROL 중요 레이블] 이는 일반적으로 데이터가 제한될 수 있는 이유에 해당합니다. 각 레이블에는 [!UICONTROL 친숙한 이름] 그리고 짧게 [!UICONTROL 이름] 그냥 수형과 수식의 약어일 뿐입니다 예: [!DNL C1] 레이블은 충성도 정책에 필요한 &quot;타사 내보내기 없음&quot;에 대한 것입니다.

![데이터 거버넌스 레이블](assets/governance-policies.png)

이제 사용을 제한하려는 데이터에 레이블을 지정할 차례입니다.

1. Platform 사용자 인터페이스에서 을(를) 선택합니다 **[!UICONTROL 데이터 세트]** 왼쪽 탐색
1. 를 엽니다. `Luma Loyalty Dataset`
1. 로 이동합니다. **[!UICONTROL 데이터 거버넌스]** 탭
1. 개별 필드에 레이블을 적용하거나 전체 데이터 세트에 적용할 수 있습니다. 전체 데이터 세트에 레이블을 적용합니다. 연필 아이콘을 클릭합니다. 아이콘이 보이지 않는다면 브라우저를 더 넓게 하거나 가운데 패널을 오른쪽으로 스크롤해 보십시오.
   ![데이터 거버넌스](assets/governance-dataset.png)
1. 모달에서 **[!UICONTROL 계약 레이블]** 섹션을 확인하고 **[!UICONTROL C2]** 레이블
1. 을(를) 선택합니다 **[!UICONTROL 변경 내용 저장]** 버튼
   ![데이터 거버넌스](assets/governance-applyLabel.png)
1. 기본으로 돌아가기 [!UICONTROL 데이터 거버넌스] 화면, **[!UICONTROL 상속된 레이블 표시]** 켜면 데이터 집합에 있는 모든 필드에 레이블이 어떻게 적용되었는지 확인할 수 있습니다.
   ![데이터 거버넌스](assets/governance-labelsAdded.png)


<!--adding extra, unnecessary fields from field groups makes it harder to see which fields really need labels-->
<!--Are there any best practices for applying governance labels-->

## 데이터 거버넌스 정책 만들기

데이터에 레이블이 지정되었으므로 정책을 만들 수 있습니다.

1. Platform 사용자 인터페이스에서 을(를) 선택합니다 **[!UICONTROL 정책]** 왼쪽 탐색
1. 찾아보기 탭에는 C2 레이블을 마케팅 작업과 연결하는 &quot;타사 내보내기 제한&quot;이라는 기본 정책이 이미 있습니다 [!UICONTROL 타사로 내보내기]정확히 우리가 필요로 하는 것
1. 정책을 선택한 다음 를 통해 활성화합니다 **[!UICONTROL 정책 상태]** 전환
   ![데이터 거버넌스](assets/governance-enablePolicy.png)

을(를) 선택하여 고유한 정책을 만들 수 있습니다 **[!UICONTROL 정책 만들기]** 버튼을 클릭합니다. 이렇게 하면 여러 레이블과 마케팅 작업 제한을 결합할 수 있는 마법사가 열립니다.

## 거버넌스 정책 적용

거버넌스 정책의 시행은 분명히 프레임워크의 핵심 구성 요소입니다. 특히 Real-time Customer Data Platform에서 라이센스를 사용하거나 사용하지 않을 수 있는 데이터를 활성화하여 Platform에서 전송할 때 다운스트림이 발생합니다. 어느 쪽이든, 이 자습서의 범위를 벗어납니다. 하지만 망설이지 말고, 이 비디오에서 어떻게 정책이 적용되는지 자세히 알 수 있습니다. 제가 관련 부분에 대해 큐에 올라가 있습니다. 또한 정책이 위반될 때 발생하는 상황을 표시합니다.

>[!VIDEO](https://video.tv.adobe.com/v/33631/?t=151&quality=12&learn=on)


## 추가 리소스

* [데이터 거버넌스 설명서](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=ko)
* [데이터 집합 서비스 API 참조](https://www.adobe.io/experience-platform-apis/references/dataset-service/)
* [거버넌스 정책 서비스 API 참조](https://www.adobe.io/experience-platform-apis/references/policy-service/)

이제 다음으로 넘어갑시다 [쿼리 서비스](run-queries.md).
