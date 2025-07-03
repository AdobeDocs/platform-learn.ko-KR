---
title: Experience Decisioning - Experience Decisioning 101
description: Experience Decisioning - Experience Decisioning 101
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
source-git-commit: 13d790855601fa6f36c1afa0f2d5faad5fc07eb0
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 1%

---

# 3.7.1 Experience Decisioning 101

## 3.7.1.1 용어

Experience Decisioning에 대한 이해를 높이려면 Offer Decisioning 응용 프로그램 서비스가 Adobe Experience Platform에서 작동하는 방식에 대한 [개요](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=en)를 읽는 것이 좋습니다.

Offer Decisioning을 사용하여 작업하려면 다음 개념을 이해해야 합니다.

| 용어 | 설명 |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **오퍼** | 오퍼는 오퍼를 볼 자격이 있는 사람을 지정하는 규칙과 관련된 마케팅 메시지입니다. 오퍼의 상태는 초안, 승인됨 또는 보관됨입니다. |
| **배치** | 최종 사용자를 위한 오퍼가 표시되는 위치(또는 채널 유형)와 컨텍스트(또는 컨텐츠 유형)의 조합입니다. 효과적으로 텍스트, HTML, 이미지, 모바일, 웹, 소셜, 인스턴트 메시징 및 비디지털 채널의 JSON 조합입니다. |
| **규칙** | 오퍼에 대한 최종 사용자의 자격을 정의하고 제어하는 논리입니다. |
| **개인 맞춤화된 오퍼** | 자격 규칙 및 제약 조건을 기반으로 한 사용자 지정 가능한 마케팅 메시지입니다. |
| **대체 오퍼** | 최종 사용자가 사용된 컬렉션에 있는 오퍼에 대한 자격이 없을 때 표시되는 기본 오퍼입니다. |
| **최대 가용량** | 오퍼를 총 몇 번이나 특정 사용자에게 제시할 수 있는지 정의하는 데 오퍼 정의에 사용됩니다. |
| **우선 순위** | 수준 : 오퍼의 결과 세트에서 우선 순위 등급을 결정합니다. |
| **컬렉션** | Offer Decisioning 프로세스 속도를 높이기 위해 개인화된 오퍼 목록에서 오퍼의 하위 세트를 필터링하는 데 사용됩니다. |
| **결정** | 마케터는 의사 결정 엔진에서 최상의 오퍼를 제공하도록 오퍼, 배치 및 프로필 세트의 조합입니다. |
| **AEM Assets Essentials** | Adobe Experience Cloud 솔루션 및 Adobe Experience Platform에서 자산을 저장, 검색 및 선택할 수 있는 범용 및 중앙 집중식 경험입니다. |

{style="table-layout:auto"}

## 3.7.1.2 경험 의사 결정

[Adobe Journey Optimizer](https://experience.adobe.com)&#x200B;(으)로 이동하여 Adobe Experience Cloud에 로그인합니다. **Journey Optimizer**&#x200B;을(를) 클릭합니다.

![ExD](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Journey Optimizer의 **Home** 보기로 리디렉션됩니다. 먼저 올바른 샌드박스를 사용하고 있는지 확인하십시오. 사용할 샌드박스를 `--aepSandboxName--`이라고 합니다. 그러면 샌드박스 **의**&#x200B;홈`--aepSandboxName--` 보기에 있게 됩니다.

![ExD](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

다음 연습에서는 오퍼 및 결정을 직접 구성합니다.

## 다음 단계

[3.7.2 오퍼 및 의사 결정 구성](./ex2.md){target="_blank"}(으)로 이동

[경험 의사 결정](ajo-decisioning.md){target="_blank"}(으)로 돌아가기

[모든 모듈](./../../../../overview.md){target="_blank"}(으)로 돌아가기
