---
title: 부트캠프 - Customer Journey Analytics - Customer Journey Analytics 101
description: 부트캠프 - Customer Journey Analytics - Customer Journey Analytics 101
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 587be8bc-8ebe-4f30-99d8-ba88ce40caf7
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 0%

---

# 4.1 Customer Journey Analytics 101

## 목표

- CJA 애플리케이션 서비스 이해
- CJA 포지셔닝 방법 알아보기
- 데이터 연결에서 통찰력에 이르기까지 CJA 워크플로 이해

## 4.1.1 Customer Journey Analytics 이란?

Customer Journey Analytics(CJA)은 크로스 채널 데이터(온라인 및 오프라인)의 결합 및 분석을 위한 비즈니스 인텔리전스 및 데이터 과학 팀에 툴킷을 제공합니다. CJA의 기능은 복잡한 다중 채널 고객 여정에 컨텍스트와 명확성을 제공합니다. 제공된 컨텍스트를 통해 고객 전환 프로세스에서 문제점을 제거하고 가장 중요한 순간에 대한 탁월한 경험을 설계 및 제공하는 데 대한 실용적인 통찰력을 얻을 수 있습니다.

CJA는 Analysis Workspace을 Adobe Experience Platform의 맨 위에 제공합니다. Adobe Experience Platform은 커뮤니케이션 및 오케스트레이션을 위한 두뇌이며 CJA와 함께 이제 브랜드가 모든 데이터를 컨텍스트화하고 시각화할 수 있으므로 비즈니스 및 인사이트 팀이 전체 온라인과 오프라인 고객 여정을 분석하여 이를 학습할 수 있습니다.

비즈니스 및 인사이트 팀은 Analysis Workspace의 드래그 앤 드롭, 포인트 앤 클릭 및 사용자 친화적인 UI를 통해 CJA와 이야기하고, 질문을 하고, 즉석에서 답변을 얻을 수 있습니다.

![데모](./images/cja-adv-analysis1.png)

## 4.1.2 주요 장점

고객에게 제공되는 3가지 주요 이점은 다음과 같습니다.

- 모든 사용자가 이용할 수 있는 통찰력을 만드는 기능(예: 데이터 액세스 민주화)
- 상황별 여정에서 고객을 볼 수 있는 기능(즉, 데이터는 온라인 및 오프라인 모두에서 여러 채널에 걸쳐 순차적으로 시각화될 수 있음)
- 필요 없이 데이터의 기능을 활용할 수 있는 기능(즉, 일반 사용자가 데이터를 사용하여 마케팅 활성화를 위한 심층적인 통찰력과 분석을 수행할 수 있도록 함)

## 4.1.3 Customer Journey Analytics을 선택하는 이유

CJA는 Power BI, Microstrategy, Locker 또는 Tableau와 같은 현재 BI 애플리케이션을 대체하기 위한 것이 아닙니다. 이러한 BI 애플리케이션은 데이터를 시각화하여 회사 대시보드를 생성함으로써 조직의 모든 사용자가 중요한 지표를 빠르게 볼 수 있도록 하기 위한 것입니다.\
CJA의 목표는 마케팅 및 비즈니스 팀을 이러한 담당자를 위한 &#39;필수&#39; 분석 도구로 만드는 분석력을 제공하는 것입니다.

전통적으로 BI 애플리케이션은 진정한 고객 인텔리전스를 실현할 수 없었습니다.

- 속성을 수행할 수 없고 고객 여정 분석을 수행할 수 없습니다.
- BI 애플리케이션은 사전에 질문을 알아야 합니다.
- 대화형 쿼리는 데이터베이스의 구조에 의해 제한됩니다
- SQL 스킬이 필요합니다.
- BI 애플리케이션은 어떤 일이 발생한 이유를 묻는 기능을 제공하지 않습니다.
- BI 애플리케이션은 고객 접점에 직접 연결되어 있지 않습니다.

이러한 이유로 비즈니스 사용자와 분석가는 거의 즉시 중단되어 많은 비용이 들고, 느리고, 유연성이 없으며, 작업 시스템과 연결이 끊겼습니다.

CJA에서는 인사이트 시간을 단축하고 비즈니스 사용자가 왜 일이 발생했는지 이해하고 이에 대응하는 방법을 독립적으로 이해할 수 있도록 하는 적절한 도구와 함께 오프라인 및 온라인 데이터를 사용하여 고객 여정을 360개까지 볼 수 있습니다.

![데모](./images/cja-use-case.png)

## 4.1.4 Customer Journey Analytics 워크플로 이해

다음 연습을 시작하기 전에 데이터를 시각화하고 심도 있는 통찰력을 얻기 위해 Adobe Experience Platform의 데이터를 CJA로 가져오는 데 필요한 단계를 이해하는 것이 중요합니다. CJA Workflow라고 합니다. 살펴보겠습니다.

![데모](./images/cja-work-flow.jpg)

위의 단계를 시작하기 전에 Adobe Experience Platform에서 사용할 수 있는 데이터를 이해하는 0단계를 잊지 마십시오.

**쓰레기가 들어오면, 쓰레기가 나와요.** 기억나니? 사용 가능한 데이터와 Adobe Experience Platform의 스키마가 구성되는 방식을 명확히 알고 있어야 합니다. Adobe Experience Platform에 있는 데이터를 이해하면 데이터 연결 부분뿐만 아니라 시각화를 구축하고 분석을 수행할 때도 작업이 더 쉬워집니다.

## 4.1.5 0단계: Adobe Experience Platform 스키마 및 데이터 세트 이해

다음 URL로 이동하여 Adobe Experience Platform에 로그인합니다. [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

로그인하면 Adobe Experience Platform 홈페이지에 접속하게 됩니다.

![데이터 수집](../uc1/images/home.png)

계속하기 전에 **샌드박스**. 선택할 샌드박스 이름이 로 지정됩니다. ``Bootcamp``. 텍스트를 클릭하여 이 작업을 수행할 수 있습니다 **[!UICONTROL Prod]** 을 클릭합니다. 적절한 샌드박스를 선택하면 화면이 변경되고 이제 전용 샌드박스에 있습니다.

![데이터 수집](../uc1/images/sb1.png)

Adobe Experience Platform에서 이러한 스키마 및 데이터 세트를 살펴보십시오.

| 데이터 세트 | 스키마 |
| ----------------- |-------------| 
| 데모 시스템 - 웹 사이트에 대한 이벤트 데이터 세트(전역 v1.1) | 데모 시스템 - 웹 사이트에 대한 이벤트 스키마(전역 v1.1) |
| 데모 시스템 - 콜 센터용 이벤트 데이터 세트(글로벌 v1.1) | 데모 시스템 - 콜 센터용 이벤트 스키마(글로벌 v1.1) |
| 데모 시스템 - Voice Assistant용 이벤트 데이터 세트(글로벌 v1.1) | 데모 시스템 - Voice Assistant용 이벤트 스키마(전역 v1.1) |

최소한 다음과 같은 사항을 확인해야 합니다.

- ID: CRMID, 전화번호, ECID, 이메일. 기본 식별자인 ID와 보조 식별자인 ID
스키마를 열고 개체를 보면 식별자를 찾을 수 있습니다 `_experienceplatform.identification.core`. 스키마 살펴보기 [데모 시스템 - 웹 사이트에 대한 이벤트 스키마(전역 v1.1)](https://experience.adobe.com/platform/schema).

![데모](./images/identity.png)

- 스키마 내의 상거래 개체 탐색 [데모 시스템 - 웹 사이트에 대한 이벤트 스키마(전역 v1.1)](https://experience.adobe.com/platform/schema).

![데모](./images/commerce.png)

- 모든 항목 미리 보기 [데이터 세트](https://experience.adobe.com/platform/dataset/browse?limit=50&amp;page=1&amp;sortDescending=1&amp;sortField=created) 데이터를 살펴보십시오.

이제 Customer Journey Analytics UI 사용을 시작할 준비가 되었습니다.

다음 단계: [4.2 Customer Journey Analytics에서 Adobe Experience Platform 데이터 세트 연결](./ex2.md)

[사용자 흐름으로 돌아가기 4](./uc4.md)

[모든 모듈로 돌아가기](../../overview.md)
