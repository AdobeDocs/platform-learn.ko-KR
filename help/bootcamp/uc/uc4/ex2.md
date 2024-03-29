---
title: Bootcamp - Customer Journey Analytics - Customer Journey Analytics에서 Adobe Experience Platform 데이터 세트 연결
description: Bootcamp - Customer Journey Analytics - Customer Journey Analytics에서 Adobe Experience Platform 데이터 세트 연결
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Connections
exl-id: 47e02021-019c-4ea4-a7a8-003deef7c9e5
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 3%

---

# 4.2 Customer Journey Analytics에서 Adobe Experience Platform 데이터 세트 연결

## 목표

- 데이터 연결 UI 이해
- Adobe Experience Platform 데이터를 CJA로 가져오기
- 개인 ID 및 데이터 결합 이해
- Customer Journey Analytics에서의 데이터 스트리밍에 대한 개념 알아보기

## 4.2.1 연결

다음으로 이동 [analytics.adobe.com](https://analytics.adobe.com) Customer Journey Analytics 액세스.

Customer Journey Analytics-홈페이지에서 **연결**.

![데모](./images/cja2.png)

여기에서 CJA와 Platform 간에 이루어진 다양한 연결을 모두 볼 수 있습니다. 이러한 연결은 Adobe Analytics의 보고서 세트와 동일한 목표를 가집니다. 그러나 데이터 수집은 완전히 다릅니다. 모든 데이터는 Adobe Experience Platform 데이터 세트에서 가져옵니다.

첫 번째 연결을 만들어 보겠습니다. **새 연결 만들기**&#x200B;를 클릭합니다.

![데모](./images/cja4.png)

그러면 다음을 볼 수 있습니다. **연결 만들기** UI.

![데모](./images/cja5.png)

이제 연결에 이름을 지정할 수 있습니다.

이 명명 규칙을 사용하십시오. `yourLastName – Omnichannel Data Connection`.

예: `vangeluw - Omnichannel Data Connection`

사용할 올바른 샌드박스를 선택해야 합니다. 샌드박스 메뉴에서 샌드박스를 선택합니다. `Bootcamp`. 이 예에서 사용할 샌드박스는 다음과 같습니다. **부트캠프**. 또한 다음을 설정해야 합니다. **일일 평균 이벤트 수** 끝 **백만 미만**.

![데모](./images/cjasb.png)

샌드박스를 선택한 후 이 연결에 데이터 세트를 추가할 수 있습니다. 클릭 **데이터 세트 추가**.

![데모](./images/cjasb1.png)

## 4.2.2 Adobe Experience Platform 데이터 세트 선택

데이터 세트 검색 `Demo System - Event Dataset for Website (Global v1.1)`. 클릭 **+** 을 클릭하여 데이터 세트를 이 연결에 추가합니다.

![데모](./images/cja7.png)

이제 확인란을 검색하여 선택하십시오. `Demo System - Profile Dataset for Loyalty (Global v1.1)` 및 `Demo System - Event Dataset for Call Center (Global v1.1)`.

그럼 이걸로 드셔보세요 **다음**&#x200B;을 클릭합니다.

![데모](./images/cja9.png)

## 4.2.3 개인 ID 및 데이터 결합

### 개인 ID

이제 이러한 데이터 세트에 결합하는 것이 목표입니다. 선택한 모든 데이터 세트에 대해 라는 필드가 표시됩니다. **개인 ID**. 각 데이터 세트에는 고유한 개인 ID 필드가 있습니다.

![데모](./images/cja11.png)

보시는 것처럼 대부분 개인 ID가 자동으로 선택됩니다. Adobe Experience Platform의 모든 스키마에서 기본 식별자가 선택되기 때문입니다. 예를 들어 다음 스키마는 `Demo System - Event Schema for Call Center (Global v1.1)`: 기본 ID가 로 설정되었음을 확인할 수 있습니다. `phoneNumber`.

![데모](./images/cja13.png)

그러나 연결을 위해 데이터 세트를 결합하는 데 사용할 식별자에 영향을 줄 수 있습니다. 데이터 세트에 연결된 스키마에 구성된 모든 식별자를 사용할 수 있습니다. 드롭다운을 클릭하여 각 데이터 세트에서 사용할 수 있는 ID를 탐색합니다.

![데모](./images/cja14.png)

위에서 언급했듯이 각 데이터 세트에 대해 서로 다른 개인 ID를 설정할 수 있습니다. 이를 통해 여러 출처의 다양한 데이터 세트를 CJA에 함께 가져올 수 있습니다. 컨텍스트와 어떤 일이 왜 일어났는지 이해하는 데 매우 흥미롭고 도움이 될 수 있는 NPS 또는 설문 조사 데이터를 가져온다고 상상해 보십시오.

개인 ID 필드의 값이 일치하는 경우 개인 ID 필드의 이름은 중요하지 않습니다. 예를 들어 개인 ID가 `email` 하나의 데이터 세트 및 `emailAddress` 다른 차원으로 `dnb-bootcamp@adobe.com` 는 두 데이터 세트의 개인 ID 필드에 대한 동일한 값이며 CJA가 데이터를 결합할 수 있습니다.

현재 익명 동작을 알려짐 과 같은 몇 가지 다른 제한 사항이 있습니다. 다음 FAQ를 검토하십시오. [FAQ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html?lang=ko-KR).

### 개인 ID를 사용하여 데이터 결합

개인 ID를 사용하여 데이터 세트를 결합하는 개념을 이해했으므로 다음을 선택하겠습니다 `email` 를 각 데이터 세트의 개인 ID로 사용하십시오.

![데모](./images/cja15.png)

각 데이터 세트로 이동하여 개인 ID를 업데이트합니다.

![데모](./images/cja12a.png)

이제 다음을 선택하여 필드 개인 ID를 채웁니다. `email` 드롭다운 목록에서 다음을 수행합니다.

![데모](./images/cja17.png)

세 개의 데이터 세트를 결합했으면 계속 진행할 준비가 되었습니다.

| 데이터 세트 | 개인 ID |
| ----------------- |-------------| 
| 데모 시스템 - 웹 사이트에 대한 이벤트 데이터 세트(전역 v1.1) | 이메일 |
| 데모 시스템 - 충성도에 대한 프로필 데이터 세트(글로벌 v1.1) | 이메일 |
| 데모 시스템 - 콜 센터용 이벤트 데이터 세트(글로벌 v1.1) | 이메일 |

또한 모든 데이터 세트에 대해 다음 옵션이 활성화되어 있는지 확인해야 합니다.

- 새 데이터 모두 가져오기
- 기존 데이터 모두 채우기

클릭 **데이터 세트 추가**.

![데모](./images/cja16.png)

클릭 **저장** 다음 연습으로 이동하십시오.
을(를) 만든 후 **연결** cja에서 데이터를 사용할 수 있으려면 몇 시간이 걸릴 수 있습니다.

![데모](./images/cja20.png)

다음 단계: [4.3 데이터 보기 만들기](./ex3.md)

[사용자 흐름으로 돌아가기 4](./uc4.md)

[모든 모듈로 돌아가기](./../../overview.md)
