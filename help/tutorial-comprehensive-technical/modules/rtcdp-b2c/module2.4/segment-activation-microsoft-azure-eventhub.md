---
title: Microsoft Azure 이벤트 허브에 대한 세그먼트 활성화
description: Microsoft Azure 이벤트 허브에 대한 세그먼트 활성화
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 2.4 Real-Time CDP: Microsoft Azure 이벤트 허브에 대한 세그먼트 활성화

**작성자: [Marc Meewis](https://www.linkedin.com/in/marcmeewis/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

이 모듈에서는 Microsoft Azure EventHub 대상을 Adobe Experience Platform Real-time CDP의 실시간 대상으로 설정합니다. 또한 Adobe Experience Platform이 세그먼트 페이로드를 Azure EventHub 대상에 전달할 때마다 실시간으로 트리거되는 Azure 기능을 설정하고 배포합니다. 트리거할 Azure 기능은 Adobe Experience Platform Real-time CDP의 활성화 기능의 메커니즘을 보여 줍니다.

또한 이 모듈의 일부로 Real-Time CDP를 트리거하여 실제로 페이로드를 지정된 대상에 전달하는 방법에 대해 이해할 수 있습니다. 또한 세그먼트 자격 상태와 활성화와 어떤 관련이 있는지에 대해서도 설명합니다.

Adobe Experience Platform Real-time CDP는 스트리밍 클라우드 스토리지 대상에 대한 데이터 활성화를 지원하므로 대상 데이터 및 이벤트를 JSON 형식으로 이러한 대상으로 실시간으로 내보낼 수 있습니다. 그런 다음 대상의 이러한 이벤트 위에 비즈니스 논리를 설명할 수 있습니다

Microsoft Azure Event Hubs는 단순하고 신뢰할 수 있으며 확장 가능한 전체 관리 실시간 데이터 수집 서비스입니다. 모든 소스에서 초당 수백만 개의 이벤트를 스트리밍하여 동적 데이터 파이프라인을 구축하고 비즈니스 문제에 즉시 대응할 수 있습니다.

## 학습 목표

- Microsoft Azure 이벤트 허브에 익숙해지십시오.
- Microsoft Azure 이벤트 허브에 RTCDP 대상 설정
- Real-Time CDP가 활성화되는 시기와 활성화 페이로드의 모습을 이해합니다
- Azure 프로젝트를 개발, 테스트 및 배포하려면 Visual Studio 코드를 설정합니다.
- RTCDP에서 실시간으로 제공되는 세그먼트 자격을 사용하는 Azure 함수 만들기 및 배포

## 전제 조건

- [Adobe Experience Platform](https://experience.adobe.com/platform)에 액세스
- AEP 데모 웹 사이트 환경에 익숙함
- Adobe Experience Platform에서 스트리밍 세그먼트를 정의, 사용 및 활성화하는 방법을 이해할 수 있습니다

>[!NOTE]
>
>[0.1 - Experience League 설명서용 Chrome 확장 설치](../../gettingstarted/gettingstarted/ex1.md)에서 참조한 대로 Chrome 확장 기능을 설치, 구성 및 사용하는 것을 잊지 마십시오.

## 연습

[2.4.0 환경 구성](./ex0.md)

이 연습에서는 Microsoft Azure 환경을 설정합니다.

[2.4.1 Microsoft Azure EventHub 환경 구성](./ex1.md)

이 연습에서는 Microsoft Azure EventHub 환경을 설정합니다.

[2.4.2 Adobe Experience Platform에서 Azure Event Hub 대상 구성](./ex2.md)

이 연습에서는 이전 연습에서 구성한 EventHub에 실시간으로 세그먼트를 전달하는 실시간 CDP 대상 연결을 설정합니다.

[2.4.3 세그먼트 만들기](./ex3.md)

이 연습에서는 Adobe Experience Platform에서 스트리밍 세그먼트를 만듭니다.

[2.4.4 세그먼트 활성화](./ex4.md)

이 연습에서는 Real-time CDP EventHub 대상에 대한 스트리밍 세그먼트를 활성화합니다.

[2.4.5 Microsoft Azure 프로젝트 만들기](./ex5.md)

이 연습에서는 Adobe Experience Platform이 해당 Azure Event Hub 대상에 대한 세그먼트 자격을 활성화할 때 실시간으로 트리거되는 Azure 기능을 만듭니다.

[2.4.6 전체 시나리오](./ex6.md)

이 시점에서 모든 설정이 이루어집니다. 이제 AEP 데모 웹 사이트에서 일부 검색을 수행하고 Microsoft Azure EventHub 트리거 기능에 세그먼트 자격을 제공할 수 있습니다.

[요약 및 이점](./summary.md)

이 단원의 요약 및 이점 개요

>[!NOTE]
>
>Adobe Experience Platform과 애플리케이션에 대해 알아야 할 모든 것을 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있는 경우 향후 콘텐츠에 대한 제안 사항에 대한 일반적인 피드백을 공유하려면 기술 인사이더에게 **techinsiders@adobe.com**&#x200B;로 전자 메일을 보내 직접 문의하십시오.

[모든 모듈로 돌아가기](../../../overview.md)
