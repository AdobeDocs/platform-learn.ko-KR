---
title: 병합 정책 만들기
seo-title: Create merge policies | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 병합 정책 만들기
description: 이 단원에서는 병합 정책을 만들어 데이터가 프로필로 병합되는 방법을 결정합니다.
role: Data Architect, Data Engineer
feature: Profiles
jira: KT-4348
audience: data architect
doc-type: tutorial
activity: implement
thumbnail: 4348-create-merge-policies.jpg
exl-id: ec862bb2-7aa2-4157-94eb-f5af3a94295f
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# 병합 정책 만들기

<!--20 min-->

이 단원에서는 병합 정책을 만들어 여러 데이터 소스가 프로필로 병합되는 방식의 우선 순위를 지정합니다.

Adobe Experience Platform을 사용하면 여러 소스에서 데이터를 결합하여 각 개별 고객에 대한 전체 보기를 볼 수 있습니다. 이 데이터를 결합할 때 병합 정책은 데이터의 우선 순위 지정 방법과 어떤 데이터를 결합하여 해당 통합 보기를 만들지 결정합니다.

이 단원에서는 사용자 인터페이스를 사용하지만 병합 정책을 생성하기 위한 API 옵션도 있습니다.

**데이터 설계자**&#x200B;는 이 자습서 외부에서 병합 정책을 만들어야 합니다.

연습을 시작하기 전에 이 짧은 비디오를 통해 병합 정책에 대해 자세히 알아보십시오.
>[!VIDEO](https://video.tv.adobe.com/v/330433?learn=on&enablevpops)

## 권한 필요

[권한 구성](configure-permissions.md) 단원에서 이 단원을 완료하는 데 필요한 모든 액세스 제어를 설정합니다.

<!--* Permission items **[!UICONTROL Profile Management]** > **[!UICONTROL View Merge Policies]** and **[!UICONTROL Manage Merge Policies]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]** and **[!UICONTROL Manage Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## 병합 정책 및 결합 스키마 정보

일괄 처리 수집 단원에서 동일한 고객에 대해 약간 다른 정보가 있는 두 개의 레코드를 업로드했음을 상기할 수 있습니다. [!DNL Loyalty] 데이터에서 고객의 이름은 `Daniel`이고 `New York City`에 거주했지만 CRM 데이터에서 고객의 이름은 `Danny`이고 `Portland`에 거주했습니다. 고객 데이터는 시간이 지남에 따라 변경됩니다. `Portland`에서 `New York City`(으)로 이동했을 수 있습니다. 전화번호나 이메일 주소 같은 다른 것도 변합니다. 병합 정책은 두 데이터 소스가 동일한 사용자에 대해 서로 다른 정보를 제공할 때 이러한 유형의 충돌을 처리하는 방법을 결정하는 데 도움이 됩니다.

`Danny`이(가) 이름을 딴 이유는 무엇입니까? 다음 항목을 살펴보겠습니다.

1. Platform 사용자 인터페이스의 왼쪽 탐색에서 **[!UICONTROL 프로필]**&#x200B;을 선택합니다
1. **[!UICONTROL 병합 정책]** 탭으로 이동
1. 기본 병합 정책 순서는 타임스탬프입니다. 충성도 데이터 뒤에 CRM 데이터를 업로드했으므로 `Danny`이(가) 프로필에서 이름으로 사용되었습니다.

![병합 정책 화면](assets/mergepolicies-default.png)

프로필에 대해 여러 스키마를 사용하도록 설정하면 기본 클래스를 공유하는 모든 프로필이 사용하도록 설정된 레코드 스키마에 대해 [!UICONTROL 유니온 스키마]이(가) 자동으로 만들어집니다. **[!UICONTROL 유니온 스키마]** 탭으로 이동하여 [!UICONTROL 유니온 스키마]를 볼 수 있습니다.

![병합 정책 화면](assets/mergepolicies-unionSchema.png)

ExperienceEvent 클래스에 대한 유니온 스키마는 없습니다. ExperienceEvent 데이터가 여전히 프로필에 도착하지만, 시계열 기반이므로 각 이벤트에는 타임스탬프와 ID가 포함되어 있으며 충돌은 문제가 되지 않습니다.

기본 병합 정책이 마음에 들지 않으면 어떻게 해야 합니까? 충돌이 있을 때 Luma가 충성도 시스템이 진실의 출처가 되어야 한다고 결정하면 어떻게 됩니까? 이를 위해 병합 정책을 만듭니다.

## UI에서 병합 정책 만들기

1. 병합 정책 화면에서 오른쪽 상단의 **[!UICONTROL 병합 정책 만들기]** 단추를 선택합니다.
1. **[!UICONTROL 이름]**(으)로 `Loyalty Prioritized`을(를) 입력하십시오.
1. **[!UICONTROL 스키마]**&#x200B;로서 **[!UICONTROL XDM 프로필]**&#x200B;을(를) 선택합니다. 사용자 지정 클래스는 레코드 데이터이므로 병합 정책에도 사용할 수 있습니다.
1. **[!UICONTROL Id 결합]**&#x200B;에 대해 **[!UICONTROL 개인 그래프]**&#x200B;를 선택합니다.
1. **[!UICONTROL 특성 병합]**&#x200B;에 대해 **[!UICONTROL 데이터 집합 우선 순위]**&#x200B;를 선택하십시오.
1. `Luma Loyalty Dataset` 및 `Luma CRM Dataset`을(를) **[!UICONTROL 데이터 집합]** 패널로 끌어서 놓습니다.
1. `Luma Loyalty Dataset`을(를) `Luma CRM Dataset` 위로 끌어서 놓아 위에 있는지 확인하십시오.
1. **[!UICONTROL 저장]** 단추 선택
   <!--do i need to explain Private Graph? Is that GA?-->
   ![병합 정책](assets/mergepolicies-newPolicy.png)

## 병합 정책 유효성 검사

병합 정책이 예상대로 작동하는지 살펴보겠습니다.

1. **[!UICONTROL 찾아보기]** 탭으로 이동
1. **[!UICONTROL 병합 정책]**&#x200B;을(를) 새 `Loyalty Prioritized` 정책으로 변경
1. **[!UICONTROL ID 네임스페이스]**(으)로 `Luma CRM Id`을(를) 사용합니다.
1. **[!UICONTROL ID 값]**(으)로 `112ca06ed53d3db37e4cea49cc45b71e` 사용
1. **[!UICONTROL 프로필 표시]** 단추 선택
1. `Daniel`이(가) 돌아왔습니다!

![다른 병합 정책이 있는 프로필 보기](assets/mergepolicies-lookupProfileWithMergePolicy.png)

## 제한된 데이터 세트를 사용하여 병합 정책 만들기

데이터 세트 우선 순위를 사용하여 병합 정책을 생성할 때 오른쪽에 포함하는 동일한 기본 클래스의 데이터 세트만 프로필에 포함됩니다. 다른 병합 정책을 설정하겠습니다.

1. 병합 정책 화면에서 오른쪽 상단의 **[!UICONTROL 병합 정책 만들기]** 단추를 선택합니다.
1. **[!UICONTROL 이름]**(으)로 `Loyalty Only`을(를) 입력하십시오.
1. **[!UICONTROL 스키마]**(으)로 **[!UICONTROL XDM 프로필]**&#x200B;을(를) 선택하십시오.
1. **[!UICONTROL Id 결합]**&#x200B;에 대해 **[!UICONTROL 없음]**&#x200B;을 선택하세요.
1. **[!UICONTROL 특성 병합]**&#x200B;에 대해 **[!UICONTROL 데이터 집합 우선 순위]**&#x200B;를 선택하십시오.
1. `Luma Loyalty Dataset`만 **[!UICONTROL 선택한 데이터 세트]** 패널로 드래그 앤 드롭하십시오.
1. **[!UICONTROL 저장]** 단추 선택

![충성도 전용 병합 정책](assets/mergepolicies-loyaltyOnly.png)

## 병합 정책 유효성 검사

이제 이 병합 정책이 수행하는 작업을 살펴보겠습니다.

1. **[!UICONTROL 찾아보기]** 탭으로 이동
1. **[!UICONTROL 병합 정책]**&#x200B;을(를) 새 `Loyalty Only` 정책으로 변경
1. **[!UICONTROL ID 네임스페이스]**(으)로 `Luma CRM Id`을(를) 사용합니다.
1. **[!UICONTROL ID 값]**(으)로 `112ca06ed53d3db37e4cea49cc45b71e` 사용
1. **[!UICONTROL 프로필 표시]** 단추 선택
1. 프로필을 찾을 수 없음 확인:
   ![충성도 전용 CRM ID 조회 없음.](assets/mergepolicies-loyaltyOnly-noCrmLookup.png)

CRM ID는 `Luma Loyalty Dataset`의 ID 필드이지만 기본 ID만 프로필을 찾는 데 사용할 수 있습니다. 기본 ID `Luma Loyalty Id`을(를) 사용하여 프로필을 조회해 보겠습니다.&quot;

1. **[!UICONTROL ID 네임스페이스]**&#x200B;을(를) `Luma Loyalty Id`(으)로 변경
1. **[!UICONTROL ID 값]**(으)로 `5625458` 사용
1. **[!UICONTROL 프로필 표시]** 단추 선택
1. 프로필 ID를 선택하여 프로필 열기
1. **[!UICONTROL 특성]** 탭으로 이동
1. 휴대폰 번호 및 이메일 주소와 같은 CRM 데이터 세트의 다른 프로필 세부 정보는 다음 이유 때문에 사용할 수 없습니다
   ![충성도 전용 정책에 CRM 데이터를 볼 수 없습니다](assets/mergepolicies-loyaltyOnly-attributes.png)
1. **[!UICONTROL 이벤트]** 탭으로 이동
1. ExperienceEvent 데이터는 병합 정책 데이터 세트에 명시적으로 포함하지 않더라도 사용할 수 있습니다.
   ![충성도 전용 정책에 이벤트가 표시됩니다](assets/mergepolicies-loyaltyOnly-events.png)

## 병합 정책에 대한 자세한 정보

프로필 검색에서 사용된 병합 정책을 `Default Timebased`(으)로 변경하고 **[!UICONTROL 프로필 표시]** 단추를 선택합니다. 대니가 돌아왔어!

![다른 병합 정책이 있는 프로필 보기](assets/mergepolicies-backToDanny.png)

무슨 일이 일어나고 있는 거죠? 프로필 병합은 일회성이 아닙니다. 실시간 고객 프로필은 어떤 병합 정책이 사용되는지 등 다양한 요인을 기반으로 즉석으로 조립됩니다. 원하는 고객 보기에 따라 다른 컨텍스트에서 사용할 여러 병합 정책을 생성할 수 있습니다.

병합 정책의 주요 사용 사례는 데이터 거버넌스용입니다. 예를 들어, 개인화 사용 사례에는 사용할 수 없지만 _can_&#x200B;은(는) 광고 사용 사례에는 사용할 수 있는 타사 데이터를 플랫폼에 수집한다고 가정해 보겠습니다. 이 타사 데이터 세트를 제외하는 병합 정책을 만들고 이 병합 정책을 사용하여 광고 사용 사례에 대한 세그먼트를 작성할 수 있습니다.

## 추가 리소스

* [병합 정책 설명서](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/overview.html?lang=ko)
* [병합 정책 API(실시간 고객 프로필 API의 일부) 참조](https://www.adobe.io/experience-platform-apis/references/profile/#tag/Merge-policies)

이제 [데이터 거버넌스 프레임워크](apply-data-governance-framework.md)(으)로 이동하겠습니다.
