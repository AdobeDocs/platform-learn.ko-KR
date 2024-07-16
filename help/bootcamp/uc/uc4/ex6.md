---
title: Bootcamp - Customer Journey Analytics - 통찰력에서 작업까지
description: Bootcamp - Customer Journey Analytics - 통찰력에서 작업까지
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Audiences
exl-id: 7a38a0a4-46e4-41f2-9a75-316dfde7128f
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# 4.6 통찰력에서 작업까지

## 목표

- Customer Journey Analytics에서 수집된 보기를 기반으로 대상을 구축하는 방법을 이해합니다
- Real-Time CDP 및 Adobe Journey Optimizer에서 이 대상 사용

## 4.6.1 대상자 만들기 및 게시

프로젝트에서 **통화 느낌**&#x200B;이라는 필터를 만들어 콜센터에 대한 통화가 **긍정적**(으)로 분류된 사용자 수를 볼 수 있었습니다. 이제 이러한 사용자로 세그먼트를 만들고 여정 또는 통신 채널에서 활성화할 수 있습니다.

첫 번째 단계는 다음과 같습니다. 마지막 연습에서 만든 패널에서 **1행을 선택합니다. 통화 느낌 - 긍정적**, 마우스 오른쪽 단추를 클릭하고 **선택 항목에서 대상 만들기** 옵션을 선택하십시오.

![데모](./images/aud1.png)

다음으로 **yourLastName - CJA 대상자 호출 느낌에 따라 대상자에 이름을 지정합니다**:

![데모](./images/aud2.png)

대상자의 미리보기가 만들어지도록 할 수 있습니다.

![데모](./images/aud3.png)

마지막으로 **Publish**&#x200B;을(를) 클릭합니다.

![데모](./images/aud4.png)

## 4.6.2 대상자를 세그먼트의 일부로 사용

Adobe Experience Platform으로 돌아가서 **세그먼트 > 찾아보기**&#x200B;로 이동하면 CJA에서 만든 세그먼트를 확인할 수 있으며 활성화 및 여정에서 사용할 수 있습니다!

![데모](./images/aud5.png)

이제 Facebook 활성화 및 고객 여정에서 이 세그먼트를 사용하겠습니다!

## 4.6.3 Real-Time CDP에서 실시간으로 세그먼트 사용

Adobe Experience Platform에서 **세그먼트 > 찾아보기**(으)로 이동하여 CJA에서 만든 대상자를 찾습니다.

![데모](./images/aud6.png)

세그먼트를 클릭한 다음 **대상에 활성화**&#x200B;를 클릭합니다.

![데모](./images/aud7.png)

**bootcamp-facebook**(이)라는 대상을 선택한 후 **다음**&#x200B;을 클릭합니다.

![데모](./images/aud8.png)

**다음**&#x200B;을 다시 클릭합니다.

![데모](./images/aud9.png)

**대상자의 원본** 옵션을 선택하고 **고객으로부터 직접**(으)로 설정한 후 **다음**&#x200B;을(를) 클릭합니다.

![데모](./images/aud10.png)

**마침을 클릭합니다**.

![데모](./images/aud11.png)

이제 세그먼트가 Facebook의 사용자 지정 대상자에 연결됩니다. 이제 Adobe Journey Optimizer에서 동일한 세그먼트를 사용하겠습니다.

## 4.6.4 Adobe Journey Optimizer에서 세그먼트 사용

Adobe Experience Platform에서 **Journey Optimizer**&#x200B;을 클릭한 다음 왼쪽 메뉴에서 **여정**&#x200B;을(를) 클릭하고 **여정 만들기**&#x200B;를 클릭하여 여정 만들기를 시작합니다.

![데모](./images/aud20.png)

![데모](./images/aud21.png)

![데모](./images/aud22.png)

그런 다음 왼쪽 메뉴에서 **이벤트**&#x200B;에서 **세그먼트 자격**&#x200B;을(를) 선택하고 여정으로 끕니다.

![데모](./images/aud23.png)

세그먼트에서 **편집**&#x200B;을 클릭하여 세그먼트를 선택합니다.

![데모](./images/aud24.png)

CJA에서 이전에 만든 대상자를 선택하고 **저장**&#x200B;을 클릭합니다.

![데모](./images/aud25.png)

준비! 여기에서 이 세그먼트에 대한 자격이 있는 고객을 위한 여정을 만들 수 있습니다.

[사용자 흐름으로 돌아가기 4](./uc4.md)

[Voltar para todos 운영 체제](./../../overview.md)
