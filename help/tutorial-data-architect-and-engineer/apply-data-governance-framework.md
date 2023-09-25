---
title: 데이터 거버넌스 프레임워크 적용
seo-title: Apply the data governance framework | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 데이터 거버넌스 프레임워크 적용
description: 이 단원에서는 데이터 거버넌스 프레임워크를 샌드박스에 수집한 데이터에 적용합니다.
role: Data Architect
feature: Data Governance
jira: KT-4348
thumbnail: 4348-apply-data-governance-framework.jpg
exl-id: 3cc3c794-5ffd-41bf-95d8-be5bca2e3a0f
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 2%

---

# 데이터 거버넌스 프레임워크 적용

<!--15min-->

이 단원에서는 데이터 거버넌스 프레임워크를 샌드박스에 수집한 데이터에 적용합니다.

Adobe Experience Platform 데이터 거버넌스를 사용하면 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 사항 및 정책을 준수할 수 있습니다. 데이터 사용을 제어하는 등 다양한 수준에서 Experience Platform 내에서 핵심적인 역할을 수행합니다.

연습을 시작하기 전에 데이터 거버넌스에 대한 다음 짧은 비디오를 시청하십시오.
>[!VIDEO](https://video.tv.adobe.com/v/36653?learn=on)

>[!VIDEO](https://video.tv.adobe.com/v/29708?learn=on)

<!--
## Permissions required

In the [Configure Permissions](configure-permissions.md) lesson, you set up all the access controls required to complete this lesson, specifically:

* Permission items **[!UICONTROL Data Governance]** > **[!UICONTROL Manage Usage Labels]**, **[!UICONTROL Manage Data Usage Policies]** and **[!UICONTROL View Data Usage Policies]**
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` Product Profile
-->

## 비즈니스 시나리오

Luma는 충성도 프로그램의 구성원에게 충성도 데이터를 서드파티와 공유하지 않겠다고 약속합니다. 이 시나리오는 단원의 나머지 부분에서 구현합니다.

## 데이터 거버넌스 레이블 적용

데이터 거버넌스 프로세스의 첫 번째 단계는 데이터에 거버넌스 레이블을 적용하는 것입니다. 그 전에 사용 가능한 레이블을 간단히 살펴보겠습니다.

1. Platform 사용자 인터페이스에서 를 선택합니다. **[!UICONTROL 정책]** 왼쪽 탐색
1. 로 이동 **[!UICONTROL 레이블]** 탭하여 계정의 모든 레이블을 볼 수 있습니다.

기본 제공 레이블이 많으며 를 통해 고유한 레이블을 만들 수 있습니다. [!UICONTROL 레이블 만들기] 단추를 클릭합니다. 세 가지 주요 유형이 있습니다. [!UICONTROL 계약 레이블], [!UICONTROL ID 레이블], 및 [!UICONTROL 중요 레이블] 일반적인 이유에 해당하는 데이터가 제한될 수 있습니다. 각 레이블에는 [!UICONTROL 알기 쉬운 이름] 약간이요 [!UICONTROL 이름] 이것은 단지 유형과 숫자의 약어일 뿐입니다. 예를 들어 [!DNL C1] 레이블은 &quot;서드파티 내보내기 없음&quot;에 대한 것으로, 이는 당사의 충성도 정책에 필요한 것입니다.

![데이터 거버넌스 레이블](assets/governance-policies.png)

이제 사용을 제한할 데이터에 레이블을 지정할 때입니다.

1. Platform 사용자 인터페이스에서 를 선택합니다. **[!UICONTROL 데이터 세트]** 왼쪽 탐색
1. 를 엽니다. `Luma Loyalty Dataset`
1. 로 이동 **[!UICONTROL 데이터 거버넌스]** 탭
1. 개별 필드에 레이블을 적용하거나 전체 데이터 세트에 적용할 수 있습니다. 전체 데이터 세트에 레이블을 적용합니다. 연필 아이콘을 클릭합니다. 아이콘이 보이지 않는다면 브라우저를 더 넓게 하거나 중간 패널을 오른쪽으로 스크롤해 보십시오.
   ![데이터 거버넌스](assets/governance-dataset.png)
1. 모달에서 **[!UICONTROL 약정 레이블]** 섹션 및 확인 **[!UICONTROL C2]** 레이블
1. 다음 항목 선택 **[!UICONTROL 변경 내용 저장]** 단추
   ![데이터 거버넌스](assets/governance-applyLabel.png)
1. 메인으로 돌아가기 [!UICONTROL 데이터 거버넌스] 화면, 포함 **[!UICONTROL 상속된 레이블 표시]** 켜면 데이터 세트의 모든 필드에 레이블이 적용된 방법을 볼 수 있습니다.
   ![데이터 거버넌스](assets/governance-labelsAdded.png)


<!--adding extra, unnecessary fields from field groups makes it harder to see which fields really need labels-->
<!--Are there any best practices for applying governance labels-->

## 데이터 거버넌스 정책 만들기

이제 데이터에 레이블이 지정되었으므로 정책을 만들 수 있습니다.

1. Platform 사용자 인터페이스에서 를 선택합니다. **[!UICONTROL 정책]** 왼쪽 탐색
1. 찾아보기 탭에는 C2 레이블을 마케팅 작업과 연결하는 &quot;타사 내보내기 제한&quot;이라는 기본 정책이 이미 있습니다 [!UICONTROL 서드파티로 내보내기]우리가 필요한 게 바로 그거예요!
1. 정책을 선택한 다음 를 통해 활성화합니다. **[!UICONTROL 정책 상태]** 전환
   ![데이터 거버넌스](assets/governance-enablePolicy.png)

다음을 선택하여 고유한 정책을 만들 수 있습니다. **[!UICONTROL 정책 만들기]** 단추를 클릭합니다. 여러 레이블과 마케팅 작업 제한을 결합할 수 있는 마법사가 열립니다.

## 거버넌스 정책 시행

거버넌스 정책의 집행은 분명 그 틀의 핵심 구성 요소이다. 특히 Real-time Customer Data Platform을 사용하여 데이터가 활성화되고 플랫폼 밖으로 전송될 때 다운스트림으로 적용되며, 사용자는 라이선스를 받거나 사용하지 않을 수 있습니다. 어느 경우든 이 자습서의 범위를 벗어납니다. 하지만 여러분은 매달려 있지 않습니다. 여러분은 제가 관련 부분까지 줄지은 이 비디오에서 정책이 어떻게 적용되는지에 대해 더 자세히 알아볼 수 있습니다. 또한 정책을 위반했을 때 발생하는 사항도 보여줍니다.

>[!VIDEO](https://video.tv.adobe.com/v/33631/?t=151&quality=12&learn=on)


## 추가 리소스

* [데이터 거버넌스 설명서](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=ko)
* [데이터 세트 서비스 API 참조](https://www.adobe.io/experience-platform-apis/references/dataset-service/)
* [거버넌스 정책 서비스 API 참조](https://www.adobe.io/experience-platform-apis/references/policy-service/)

이제 다음으로 이동하겠습니다. [쿼리 서비스](run-queries.md).
