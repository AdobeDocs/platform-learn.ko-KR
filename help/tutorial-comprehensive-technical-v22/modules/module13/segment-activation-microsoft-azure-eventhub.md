---
title: Microsoft Azure 이벤트 허브에 세그먼트 활성화
description: Microsoft Azure 이벤트 허브에 세그먼트 활성화
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 73c2576d-0a69-4d56-a671-9ae1f75580b9
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 1%

---

# 13. Real-Time CDP: Microsoft Azure 이벤트 허브에 세그먼트 활성화

**작성자: [마크 메위스](https://www.linkedin.com/in/marcmeewis/), [우터 반 겔루위](https://www.linkedin.com/in/woutervangeluwe/)**

이 단원에서는 Adobe Experience Platform 실시간 CDP를 위한 실시간 대상으로 Microsoft Azure EventHub 대상을 설정합니다. 또한 Adobe Experience Platform에서 Azure EventHub 대상으로 세그먼트 페이로드를 전달할 때마다 실시간으로 트리거되는 Azure 함수를 설정 및 배포합니다. 트리거할 Azure 함수는 Adobe Experience Platform 실시간 CDP의 활성화 기능 메커니즘을 보여줍니다.

또한 이 모듈의 일부로, 특정 대상에 페이로드를 실제로 제공하기 위해 실시간 CDP를 트리거하는 항목을 알아봅니다. 또한 세그먼트 자격의 상태 및 활성화 방법에 대해서도 설명합니다.

Adobe Experience Platform 실시간 CDP는 스트리밍 클라우드 스토리지 대상에 대한 데이터 활성화를 지원하므로 대상 데이터 및 이벤트를 JSON 형식으로 이러한 대상으로 실시간으로 내보낼 수 있습니다. 그런 다음 대상에서 이러한 이벤트 위에 비즈니스 논리를 설명할 수 있습니다

Microsoft Azure 이벤트 허브는 간단하고 신뢰할 수 있으며 확장 가능한 완전히 관리되는 실시간 데이터 수집 서비스입니다. 소스에서 초당 수백만 개의 이벤트를 스트리밍하여 다이내믹 데이터 파이프라인을 구축하고 비즈니스 문제에 즉시 대처할 수 있습니다.

## 학습 목표

- Microsoft Azure 이벤트 허브에 익숙해지십시오
- Microsoft Azure 이벤트 허브에 RTCDP 대상 설정
- 실시간 CDP가 활성화되는 시점과 활성화 페이로드가 어떻게 표시되는지 이해합니다
- Azure 프로젝트를 개발, 테스트 및 배포하려면 Visual Studio 코드를 설정하십시오
- RTCDP에서 실시간으로 제공되는 세그먼트 자격을 사용하는 Azure 함수를 만들고 배포합니다

## 전제 조건

- 액세스 권한 [Adobe Experience Platform](https://experience.adobe.com/platform)
- AEP 데모 웹 사이트 환경에 익숙함
- Adobe Experience Platform에서 스트리밍 세그먼트를 정의, 사용 및 활성화하는 방법을 이해합니다

>[!IMPORTANT]
>
>이 자습서는 특정 워크숍 형식을 용이하게 하기 위해 만들어졌습니다. 액세스 권한이 없을 수 있는 특정 시스템 및 계정을 사용합니다. 액세스 권한이 없더라도 이 매우 자세한 내용을 통해 많은 것을 배울 수 있을 것입니다. 워크샵 중 하나에 참여하고 액세스 자격 증명이 필요한 경우 Adobe 담당자에게 연락하여 필요한 정보를 제공합니다.

## 아키텍처 개요

이 모듈에서 논의하고 사용할 구성 요소를 강조 표시하는 아래 아키텍처를 살펴보십시오.

![아키텍처 개요](../../assets/images/architecturem18.png)

## 사용할 샌드박스

이 모듈의 경우 다음 샌드박스를 사용하십시오. `--module18sandbox--`.

>[!NOTE]
>
>에서 참조한 대로 Chrome 확장 프로그램을 설치, 구성 및 사용하는 것을 잊지 마십시오 [0.1 - Experience League 설명서용 Chrome 확장 프로그램 설치](../module0/ex1.md)

## 연습

[13.0 환경 구성](./ex0.md)

이 연습에서는 Microsoft Azure 환경을 설정합니다.

[13.1 Microsoft Azure EventHub 환경 구성](./ex1.md)

이 연습에서는 Microsoft Azure EventHub 환경을 설정합니다.

[13.2 Adobe Experience Platform에서 Azure 이벤트 허브 대상 구성](./ex2.md)

이 연습에서는 이전 연습에서 구성한 EventHub에 세그먼트를 실시간으로 전달하는 실시간 CDP 대상 연결을 설정합니다.

[13.3 세그먼트 만들기](./ex3.md)

이 연습에서는 Adobe Experience Platform에서 스트리밍 세그먼트를 만듭니다

[13.4 세그먼트 활성화](./ex4.md)

이 연습에서는 스트리밍 세그먼트를 실시간 CDP EventHub 대상으로 활성화합니다.

[13.5 Microsoft Azure 프로젝트 만들기](./ex5.md)

이 연습에서는 Adobe Experience Platform이 해당 Azure 이벤트 허브 대상에 대한 세그먼트 자격을 활성화하면 실시간으로 트리거되는 Azure 함수를 만듭니다.

[13.6 엔드 투 엔드 시나리오](./ex6.md)

이 시점에서 모든 것이 설정됩니다. 이제 AEP 데모 웹 사이트에서 일부 탐색을 수행하고 Microsoft Azure EventHub 트리거 함수로 제공되는 세그먼트 자격을 가져올 수 있습니다.

[요약 및 이점](./summary.md)

이 모듈의 요약 및 이점 개요

>[!NOTE]
>
>Adobe Experience Platform에 대해 알아야 할 모든 것을 배우는 데 시간을 투자해주셔서 감사합니다. 질문이 있는 경우 향후 컨텐츠에 대한 제안 사항이 있는 일반적인 피드백을 공유하려는 경우 Outlook Van Geluwe에게 이메일을 직접 보내주십시오 **vangeluw@adobe.com**.

[모든 모듈로 돌아가기](../../overview.md)
