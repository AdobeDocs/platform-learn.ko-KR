---
title: Real-Time CDP - 세그먼트 구축 및 조치
description: Real-Time CDP - 세그먼트 구축 및 조치
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 147d9153-5742-4857-aae1-0ec434a1e626
source-git-commit: 5c4d00879be343e7a6cd6a773b383bad1a24e349
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 1%

---

# 2.3 Real-time CDP - 대상 구축 및 조치

이 모듈에서는 스트리밍 세그먼트를 구성하고 대상을 여러 대상에 활성화합니다.

## 학습 목표

- 대상자를 빌드하고 스트리밍에 사용할 수 있도록 하는 방법에 대해 알아봅니다.
- Adobe Experience Platform UI를 사용하여 광고 대상을 구성하는 방법을 알아봅니다.
- 대상을 대상에 연결하고 활성화하는 방법을 알아봅니다.

## 전제 조건

- Adobe Experience Platform 액세스: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Adobe Target 액세스
- AWS S3에 액세스

>[!NOTE]
>
>[Experience League 설명서용 Chrome 확장 설치](../../gettingstarted/gettingstarted/ex1.md)에서 참조한 대로 Chrome 확장 기능을 설치, 구성 및 사용하는 것을 잊지 마십시오

## 연습

[2.3.1 대상자 만들기](./ex1.md)

대상자를 만드는 방법을 알아봅니다.

[2.3.2 대상을 사용하여 DV360 대상을 구성하는 방법 검토](./ex2.md)

Real-Time CDP UI를 사용하여 광고 대상을 구성하는 방법을 알아봅니다.

[2.3.3 조치 취하기: 대상자를 DV360으로 보내기](./ex3.md)

빌드한 대상을 대상 DV360에 연결합니다.

[2.3.4 조치 취하기: 대상자를 S3-destination으로 보내기](./ex4.md)

만든 대상을 사용하여 S3 대상으로 보냅니다(일반적으로 이메일 마케팅 대상에 사용됨).

[2.3.5 조치 취하기: 대상자를 Adobe Target으로 보내기](./ex5.md)

만든 대상을 사용하여 Adobe Target에서 경험 타깃팅 활동을 구성합니다.

[2.3.6 대상 SDK](./ex6.md)

대상 SDK을 사용하여 고유한 대상을 구성합니다.

[요약 및 이점](./summary.md)

이 단원의 요약 및 이점 개요

![기술 내부자](./../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Adobe Experience Platform과 애플리케이션에 대해 알아야 할 모든 것을 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있는 경우 향후 콘텐츠에 대한 제안 사항에 대한 일반적인 피드백을 공유하려면 기술 인사이더에게 **techinsiders@adobe.com**&#x200B;로 전자 메일을 보내 직접 문의하십시오.

[모든 모듈로 돌아가기](../../../overview.md)
