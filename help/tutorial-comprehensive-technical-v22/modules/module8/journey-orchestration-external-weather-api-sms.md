---
title: Adobe Journey Optimizer - 외부 날씨 API, SMS 동작 등
description: Adobe Journey Optimizer - 외부 날씨 API, SMS 동작 등
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7f3d6dcb-845d-4ff1-97c3-8e93b8d2c624
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 2%

---

# 8. Adobe Journey Optimizer: 외부 데이터 소스 및 사용자 지정 작업

**작성자: [우터 반 겔루위](https://www.linkedin.com/in/woutervangeluwe/)**

이 모듈에서는 Adobe Journey Optimizer을 사용하여 온라인과 오프라인을 막론하고 고객 행동을 경청하고 지능적이고 상황에 맞는 실시간으로 반응합니다. 모듈 6에서 Adobe Journey Optimizer을 처음 경험해 보았습니다. 이 연습에서는 외부 데이터 소스를 여정의 일부로 사용하는 고급 사용 사례를 살펴봅니다.

## 학습 목표

- Adobe Journey Optimizer에서 이벤트, 외부 데이터 소스 및 여정을 만드는 방법을 알아봅니다
- Open Weather API에서 날씨 정보를 사용하는 방법을 알아봅니다
- Twilio 및 Adobe Journey Optimizer의 Slack과 같은 사용자 지정 작업 대상을 사용하는 방법을 알아봅니다

## 사전 요구 사항

- Adobe Experience Platform에 액세스: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Adobe Journey Optimizer 액세스
- Open Weather API에 대한 액세스

>[!IMPORTANT]
>
>이 자습서는 특정 워크숍 형식을 용이하게 하기 위해 만들어졌습니다. 액세스 권한이 없을 수 있는 특정 시스템 및 계정을 사용합니다. 액세스 권한이 없더라도 이 매우 자세한 내용을 통해 많은 것을 배울 수 있을 것입니다. 워크샵 중 하나에 참여하고 액세스 자격 증명이 필요한 경우 Adobe 담당자에게 연락하여 필요한 정보를 제공합니다.

## 아키텍처 개요

이 모듈에서 논의하고 사용할 구성 요소를 강조 표시하는 아래 아키텍처를 살펴보십시오.

![아키텍처 개요](../../assets/images/architecturem12.png)

## 비즈니스 컨텍스트

브랜드는 온라인 경험을 개인화하는 데 많은 투자를 했습니다. 이제 오프라인 경험에 대해 상황에 맞는 경험을 만들어야 합니다.
이 모듈에서는 오프라인 스토어에서 고객의 존재가 확인되면 매장 내에서 개인화된 경험을 제공할 수 있습니다. 따라서 매장 내 화면에 해당 고객에게 관련 컨텐츠를 표시하면서 동시에 해당 고객에게 개인화된 푸시 또는 SMS 메시지를 실시간으로 전달하려고 합니다.
브랜드에서는 컨텍스트가 고객의 관심사에 크게 영향을 주므로 해당 고객의 위치에 대한 현재 날씨 정보를 가져와서 표시할 컨텐츠 또는 프로모션을 결정하려고 합니다.

## 사용할 샌드박스

이 모듈의 경우 다음 샌드박스를 사용하십시오. `--aepSandboxId--`.

>[!NOTE]
>
>에서 참조한 대로 Chrome 확장 프로그램을 설치, 구성 및 사용하는 것을 잊지 마십시오 [0.1 - Experience League 설명서용 Chrome 확장 프로그램 설치](../module0/ex1.md)

## 연습

[8.1 이벤트 정의](./ex1.md)

Adobe Journey Optimizer을 사용하여 사용자 지정 이벤트를 정의하는 방법을 알아봅니다.

[8.2 외부 데이터 소스 정의](./ex2.md)

Adobe Journey Optimizer을 사용하여 외부 데이터 소스를 구성하는 방법을 알아봅니다.

[8.3 사용자 지정 작업 정의](./ex3.md)

Adobe Journey Optimizer을 사용하여 외부 작업을 정의하는 방법을 배웁니다.

[8.4 여정 및 메시지 만들기](./ex4.md)

이벤트, 데이터 소스 및 작업을 지능적이고 상황에 맞는 여정으로 결합할 수 있습니다.

[8.5 여정 트리거](./ex5.md)

특정 여정을 트리거합니다.

[요약 및 이점](./summary.md)

이 모듈의 요약 및 이점 개요

>[!NOTE]
>
>Adobe Experience Platform에 대해 알아야 할 모든 것을 배우는 데 시간을 투자해주셔서 감사합니다. 질문이 있는 경우 향후 컨텐츠에 대한 제안 사항이 있는 일반적인 피드백을 공유하려는 경우 Outlook Van Geluwe에게 이메일을 직접 보내주십시오 **vangeluw@adobe.com**.

[모든 모듈로 돌아가기](../../overview.md)
