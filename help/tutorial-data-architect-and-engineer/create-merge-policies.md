---
title: 병합 정책 만들기
seo-title: Create merge policies | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 병합 정책 만들기
description: 이 단원에서는 데이터가 프로필에 병합되는 방법을 결정하는 병합 정책을 만듭니다.
role: Data Architect, Data Engineer
feature: Profiles
kt: 4348
audience: data architect
doc-type: tutorial
activity: implement
thumbnail: 4348-create-merge-policies.jpg
exl-id: ec862bb2-7aa2-4157-94eb-f5af3a94295f
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 1%

---

# 병합 정책 만들기

<!--20 min-->

이 단원에서는 여러 데이터 소스를 프로필에 병합하는 방법에 대해 우선 순위를 지정하는 병합 정책을 만듭니다.

Adobe Experience Platform을 사용하면 여러 소스에서 데이터를 결합하여 각 개별 고객에 대한 전체 보기를 볼 수 있습니다. 이 데이터를 함께 가져올 때 병합 정책은 데이터의 우선 순위가 지정된 방식과 결합되는 데이터를 파악하여 해당 통합 보기를 만듭니다.

이 단원의 사용자 인터페이스를 유지하지만 병합 정책을 만들기 위해 API 옵션도 있습니다.

**데이터 설계자** 은 이 자습서의 외부에서 병합 정책을 만들어야 합니다.

연습을 시작하기 전에 이 짧은 비디오에서 병합 정책에 대해 자세히 알아보십시오.
>[!VIDEO](https://video.tv.adobe.com/v/330433?quality=12&learn=on)

## 필요한 권한

에서 [권한 구성](configure-permissions.md) 이 단원을 완료하는 데 필요한 모든 액세스 컨트롤을 설정합니다.

<!--* Permission items **[!UICONTROL Profile Management]** > **[!UICONTROL View Merge Policies]** and **[!UICONTROL Manage Merge Policies]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]** and **[!UICONTROL Manage Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## 병합 정책 및 결합 스키마 정보

배치 수집 단원에서 동일한 고객을 위해 약간 다른 정보를 사용하여 두 개의 레코드를 업로드했습니다. 에서 [!DNL Loyalty] 데이터, 고객의 이름은 `Daniel` 그리고 그는 `New York City`로 설정되지만 CRM 데이터에서 고객의 이름은 `Danny` 그리고 그는 `Portland`. 시간이 지남에 따라 고객 데이터가 변경됩니다. 아마도 그는 `Portland` to `New York City`. 전화번호, 이메일 주소 등 다른 것들도 변경됩니다. 병합 정책은 두 데이터 소스가 동일한 사용자에 대해 서로 다른 정보를 제공할 때 이러한 유형의 충돌을 처리하는 방법을 결정하는 데 도움이 됩니다.

그래서, 왜 `Danny` 성명으로 이기려고? 어디 한 번 보자.

1. Platform 사용자 인터페이스에서 을(를) 선택합니다 **[!UICONTROL 프로필]** 왼쪽 탐색
1. 로 이동합니다. **[!UICONTROL 정책 병합]** 탭
1. 기본 병합 정책이 타임스탬프 순서가 지정됩니다. 충성도 데이터 다음에 CRM 데이터를 업로드했으므로, `Danny` 은(는) 프로필의 이름으로 로그아웃됩니다.

![병합 정책 화면](assets/mergepolicies-default.png)

프로필에 대해 여러 스키마를 활성화하면 [!UICONTROL 결합 스키마] 모든 프로파일을 사용하는 경우 기본 클래스를 공유하는 기록 스키마에 대해 자동으로 만들어집니다. 을 볼 수 있습니다 [!UICONTROL 결합 스키마] 다음과 같이 **[!UICONTROL 결합 스키마]** 탭.

![병합 정책 화면](assets/mergepolicies-unionSchema.png)

ExperienceEvent 클래스에 대한 결합 스키마가 없습니다. ExperienceEvent 데이터가 여전히 프로필에 도착하지만, 시계열 기반이므로 각 이벤트에 타임스탬프와 ID가 포함되고 충돌은 문제가 되지 않습니다.

기본 병합 정책이 마음에 들지 않으면 어떻게 하시겠습니까? 충돌이 있을 때 Luma가 자신의 CRM 시스템을 진실의 근원이 되도록 결정하는 경우 어떻게 됩니까? 이를 위해 병합 정책을 만듭니다.

## UI에서 병합 정책 만들기

1. 병합 정책 화면에서 **[!UICONTROL 병합 정책 만들기]** 오른쪽 위의 단추
1. 로서의 **[!UICONTROL 이름]**, 입력 `Loyalty Prioritized`
1. 로서의 **[!UICONTROL 스키마]**, 선택 **[!UICONTROL XDM 프로필]** (사용자 지정 클래스는 레코드 데이터이므로 병합 정책에도 사용할 수 있습니다.)
1. 대상 **[!UICONTROL Id 결합]**, 선택 **[!UICONTROL 개인 그래프]**
1. 대상 **[!UICONTROL 속성 병합]**, 선택 **[!UICONTROL 데이터 집합 우선 순위]**
1. 드래그 앤 드롭 `Luma Loyalty Dataset` 및 `Luma CRM Dataset` 변환 후 **[!UICONTROL 데이터 집합]** 패널.
1. 확인 `Luma Loyalty Dataset` 위로 끌어서 놓으면 위에 표시됩니다 `Luma CRM Dataset`
1. **[!UICONTROL 저장]** 버튼을 선택합니다
<!--do i need to explain Private Graph? Is that GA?-->
![병합 정책](assets/mergepolicies-newPolicy.png)

## 병합 정책 유효성 검사

병합 정책이 우리가 기대하는 것을 수행하고 있는지 봅시다.

1. 로 이동합니다. **[!UICONTROL 찾아보기]** 탭
1. 변경 **[!UICONTROL 병합 정책]** 새 `Loyalty Prioritized` 정책
1. 로서의 **[!UICONTROL ID 네임스페이스]**, 사용 `Luma CRM Id`
1. 로서의 **[!UICONTROL ID 값]** 사용 `112ca06ed53d3db37e4cea49cc45b71e`
1. 을(를) 선택합니다 **[!UICONTROL 프로필 표시]** 버튼
1. `Daniel` 돌아왔어!

![다른 병합 정책을 사용하여 프로필 보기](assets/mergepolicies-lookupProfileWithMergePolicy.png)

## 제한된 데이터 세트로 병합 정책 만들기

데이터 집합 우선 순위를 사용하여 병합 정책을 만들 때 오른쪽에 포함하는 동일한 기본 클래스의 데이터 집합만 프로필에 포함됩니다. 다른 병합 정책을 설정하겠습니다

1. 병합 정책 화면에서 **[!UICONTROL 병합 정책 만들기]** 오른쪽 위의 단추
1. 로서의 **[!UICONTROL 이름]**, 입력  `Loyalty Only`
1. 로서의 **[!UICONTROL 스키마]**, 선택 **[!UICONTROL XDM 프로필]**
1. 대상 **[!UICONTROL Id 결합]**, 선택 **[!UICONTROL 없음]**
1. 대상 **[!UICONTROL 속성 병합]**, 선택 **[!UICONTROL 데이터 집합 우선 순위]**
1. 만 드래그 앤 드롭 `Luma Loyalty Dataset` to **[!UICONTROL 선택한 데이터 세트]** 패널.
1. **[!UICONTROL 저장]** 버튼을 선택합니다

![충성도 전용 병합 정책](assets/mergepolicies-loyaltyOnly.png)

## 병합 정책 유효성 검사

이제 이 병합 정책이 수행하는 작업을 살펴보겠습니다.

1. 로 이동합니다. **[!UICONTROL 찾아보기]** 탭
1. 변경 **[!UICONTROL 병합 정책]** 새 `Loyalty Only` 정책
1. 로서의 **[!UICONTROL ID 네임스페이스]**, 사용 `Luma CRM Id`
1. 로서의 **[!UICONTROL ID 값]** 사용 `112ca06ed53d3db37e4cea49cc45b71e`
1. 을(를) 선택합니다 **[!UICONTROL 프로필 표시]** 버튼
1. 프로필을 찾을 수 없는지 확인합니다.
   ![충성도 CRM Id 조회가 없습니다.](assets/mergepolicies-loyaltyOnly-noCrmLookup.png)

CRM ID는 `Luma Loyalty Dataset`그러나 기본 ID만 프로필을 조회하는 데 사용할 수 있습니다. 그럼, 1차 ID를 이용해서 프로파일을 찾아보죠 `Luma Loyalty Id`&quot;

1. 변경 **[!UICONTROL ID 네임스페이스]** to `Luma Loyalty Id`
1. 로서의 **[!UICONTROL ID 값]** 사용 `5625458`
1. 을(를) 선택합니다 **[!UICONTROL 프로필 표시]** 버튼
1. 프로필 ID를 선택하여 프로필을 엽니다
1. 로 이동합니다. **[!UICONTROL 속성]** 탭
1. Crm 데이터 세트의 다른 프로필 세부 사항(예: 휴대폰 번호 및 이메일 주소)은 Adobe에서만 사용할 수 있으므로 사용할 수 없습니다
   ![CRM 데이터가 충성도 전용 정책에서 볼 수 없음](assets/mergepolicies-loyaltyOnly-attributes.png)
1. 로 이동합니다. **[!UICONTROL 이벤트]** 탭
1. ExperienceEvent 데이터는 병합 정책 데이터 세트에 명시적으로 포함하지 않더라도 사용할 수 있습니다.
   ![충성도 전용 정책에서 이벤트를 볼 수 있습니다](assets/mergepolicies-loyaltyOnly-events.png)

## 병합 정책에 대한 자세한 정보

프로필 검색에서 다시 사용되는 병합 정책을 `Default Timebased` 을(를) 선택하고 을(를) 선택합니다. **[!UICONTROL 프로필 표시]** 버튼을 클릭합니다. 대니가 돌아왔어!

![다른 병합 정책을 사용하여 프로필 보기](assets/mergepolicies-backToDanny.png)

여기서 무슨 일이 일어나고 있습니까? 프로필 병합은 단 한 번의 일이 아닙니다. 실시간 고객 프로필은 사용되는 병합 정책을 포함하여 다양한 요소를 기반으로 즉시 어셈블됩니다. 원하는 고객 보기에 따라 다양한 컨텍스트에서 사용할 여러 병합 정책을 만들 수 있습니다.

병합 정책을 위한 주요 사용 사례는 데이터 거버넌스입니다. 예를 들어, 개인화 사용 사례에 사용할 수 없는, 타사 데이터를 Platform에 수집한다고 가정해 보겠습니다 _다음을 수행할 수 있습니다._ 광고 사용 사례에 사용됩니다. 이 타사 데이터 세트를 제외하는 병합 정책을 만들고 이 병합 정책을 사용하여 광고 사용 사례용 세그먼트를 작성할 수 있습니다.

## 추가 리소스

* [병합 정책 설명서](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/overview.html)
* [병합 정책 API(실시간 고객 프로필 API의 일부) 참조](https://www.adobe.io/experience-platform-apis/references/profile/#tag/Merge-policies)

이제 로 넘어갑시다 [데이터 거버넌스 프레임워크](apply-data-governance-framework.md).
