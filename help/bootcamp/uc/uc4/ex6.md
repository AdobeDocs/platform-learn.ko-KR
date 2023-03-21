---
title: Bootcamp - Customer Journey Analytics - 인사이트에서 작업에 이르기까지
description: Bootcamp - Customer Journey Analytics - 인사이트에서 작업에 이르기까지
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: e5c2ad88967d7f6a45d3a5cc09ca4c9bc9a62a08
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# 4.6 인사이트에서 다음으로 시작

## 목표

- Customer Journey Analytics에 수집된 보기를 기반으로 대상을 만드는 방법을 이해합니다
- Real-Time CDP 및 Adobe Journey Optimizer에서 이 대상 사용

## 4.6.1 대상자 만들기 및 게시

프로젝트에서 다음 필터를 만들었습니다. **통화 감정** 그리고 가 **긍정적**. 이제 이러한 사용자로 세그먼트를 만들고 여정 또는 통신 채널에서 활성화할 수 있습니다.

첫 번째 단계는 다음과 같습니다. 마지막 연습에서 만든 패널에서 선을 선택합니다 **1. 전화 감상 - 긍정적**&#x200B;를 마우스 오른쪽 단추로 클릭하고 를 선택합니다. **선택 항목에서 대상 만들기** 옵션:

![데모](./images/aud1.png)

그런 다음 모델을 따라 대상자에게 이름을 지정합니다 **yourLastName - CJA 대상 호출 긍정적 감정**:

![데모](./images/aud2.png)

만들어지는 대상자의 미리 보기가 있을 수 있습니다.

![데모](./images/aud3.png)

마지막으로 **게시**.

![데모](./images/aud4.png)

## 4.6.2 세그먼트의 일부로서 대상 사용

Adobe Experience Platform으로 돌아가서 **세그먼트 > 찾아보기** 또한 CJA에서 만든 세그먼트를 준비하여 활동 및 여정에서 사용할 수 있습니다.

![데모](./images/aud5.png)

이제 Facebook 활성화 및 고객 여정에서 이 세그먼트를 사용하겠습니다.

## 4.6.3 Real-Time CDP에서 실시간으로 세그먼트 사용

Adobe Experience Platform에서 **세그먼트 > 찾아보기** cja에서 만든 대상자를 찾습니다.

![데모](./images/aud6.png)

세그먼트를 클릭한 다음 **대상에 활성화**:

![데모](./images/aud7.png)

이름이 지정된 대상을 선택합니다. **bootcamp-facebook**&#x200B;를 클릭한 다음 **다음**.

![데모](./images/aud8.png)

클릭 **다음** 다시 한 번

![데모](./images/aud9.png)

을(를) 선택합니다 **대상자의 기원** 옵션을 설정하고 **고객으로부터 직접**&#x200B;를 클릭합니다. **다음**.

![데모](./images/aud10.png)

**마침을 클릭합니다**.

![데모](./images/aud11.png)

이제 세그먼트가 Facebook의 사용자 지정 대상에 연결됩니다. 이제 Adobe Journey Optimizer에서 동일한 세그먼트를 사용하겠습니다.

## 4.6.4 Adobe Journey Optimizer에서 세그먼트 사용

Adobe Experience Platform에서 **Journey Optimizer**&#x200B;를 클릭한 다음 왼쪽 메뉴에서 **여정** 을 클릭하고 을 클릭하여 여정 만들기를 시작합니다. **여정 만들기**.

![데모](./images/aud20.png)

![데모](./images/aud21.png)

![데모](./images/aud22.png)

그리고 왼쪽 메뉴에서 **이벤트**, 선택 **세그먼트 자격** 여정으로 드래그합니다.

![데모](./images/aud23.png)

세그먼트에서 **편집** 세그먼트를 선택하려면 다음을 수행하십시오.

![데모](./images/aud24.png)

CJA에서 이전에 만든 대상자를 선택하고 을(를) 클릭합니다  **저장**.

![데모](./images/aud25.png)

준비! 여기에서 이 세그먼트에 대한 자격이 있는 고객을 위한 여정을 만들 수 있습니다.

[사용자 흐름 4로 돌아가기](./uc4.md)

[Voltar para todos os modulos](./../../overview.md)
