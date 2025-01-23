---
title: Adobe Journey Optimizer - 외부 날씨 API, SMS 동작 등
description: Adobe Journey Optimizer - 외부 날씨 API, SMS 동작 등
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7f3d6dcb-845d-4ff1-97c3-8e93b8d2c624
source-git-commit: bd46be455f88007174f7e6be9a1ce5f508edc09b
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# 3.2 Adobe Journey Optimizer: 외부 데이터 소스 및 사용자 지정 작업

이 모듈에서는 Adobe Journey Optimizer을 사용하여 온라인과 오프라인 모두에서 고객 행동을 청취하고 지능적이고 상황에 맞는 실시간 방식으로 대응합니다. 이미 모듈 6에서 Adobe Journey Optimizer을 처음 사용해 본 경험이 있습니다. 이 연습에서는 외부 데이터 소스를 여정의 일부로 사용하는 고급 사용 사례에 대해 알아봅니다.

## 학습 목표

- Adobe Journey Optimizer에서 이벤트, 외부 데이터 소스 및 여정을 만드는 방법을 알아봅니다
- 개방형 날씨 API에서 날씨 정보를 사용하는 방법을 알아봅니다
- Adobe Journey Optimizer에서 Twilio 및 Slack과 같은 사용자 지정 작업 대상을 사용하는 방법을 알아봅니다

## 전제 조건

- Adobe Experience Platform 액세스: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Adobe Journey Optimizer 액세스
- 개방형 날씨 API에 액세스

## 비즈니스 컨텍스트

브랜드로서는 온라인 경험을 개인화하는 데 많은 투자를 했습니다. 이제 오프라인 경험에 상황에 맞게 관련성을 갖추어야 합니다.
이 모듈에서는 오프라인 스토어에서 고객의 현재 상태를 사용하여 매장 내 화면에서 해당 고객에게 관련 콘텐츠를 표시함으로써 매장 내에 개인화된 환경을 제공하고, 동시에 동일한 고객에게 개인화된 푸시 또는 SMS 메시지를 실시간으로 전달하려고 합니다.
브랜드로서는 컨텍스트가 고객의 관심에 크게 영향을 미친다는 사실을 이해하므로 해당 고객 위치의 현재 날씨 정보를 가져와서 표시할 콘텐츠 또는 프로모션을 결정하려고 합니다.

>[!NOTE]
>
>[Experience League 설명서용 Chrome 확장 설치](../../gettingstarted/gettingstarted/ex1.md)에서 참조한 대로 Chrome 확장 기능을 설치, 구성 및 사용하는 것을 잊지 마십시오

## 연습

[3.2.1 이벤트 정의](./ex1.md)

Adobe Journey Optimizer을 사용하여 사용자 지정 이벤트를 정의하는 방법을 알아봅니다.

[3.2.2 외부 데이터 소스 정의](./ex2.md)

Adobe Journey Optimizer을 사용하여 외부 데이터 소스를 구성하는 방법에 대해 알아봅니다.

[3.2.3 사용자 지정 작업 정의](./ex3.md)

Adobe Journey Optimizer을 사용하여 외부 작업을 정의하는 방법을 알아봅니다.

[3.2.4 여정 및 메시지 만들기](./ex4.md)

이벤트, 데이터 소스 및 작업을 지능적이고 상황에 맞는 여정으로 결합합니다.

[3.2.5 여정 트리거](./ex5.md)

특정 여정을 트리거합니다.

[요약 및 이점](./summary.md)

이 단원의 요약 및 이점 개요

![기술 내부자](./../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Adobe Experience Platform과 애플리케이션에 대해 알아야 할 모든 것을 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있는 경우 향후 콘텐츠에 대한 제안 사항에 대한 일반적인 피드백을 공유하려면 기술 인사이더에게 **techinsiders@adobe.com**&#x200B;로 전자 메일을 보내 직접 문의하십시오.

[모든 모듈로 돌아가기](../../../overview.md)
