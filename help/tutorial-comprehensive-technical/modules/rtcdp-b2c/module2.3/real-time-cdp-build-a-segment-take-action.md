---
title: Real-Time CDP - 세그먼트 구축 및 조치
description: Real-Time CDP - 세그먼트 구축 및 조치
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 147d9153-5742-4857-aae1-0ec434a1e626
source-git-commit: f4b3463ce9464c96378790bf8070504fc90cb2ff
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 1%

---

# 2.3 Real-time CDP - 세그먼트 구축 및 조치

**작성자: [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/), [Alberto De Caro](https://www.linkedin.com/in/albertodecaro/), [Benedikt Wedenik](https://www.linkedin.com/in/benedikt-wedenik/)**

이 모듈에서는 스트리밍 세그먼트를 구성하고 여러 대상에 대한 세그먼트를 활성화합니다.

## 학습 목표

- 세그먼트를 작성하고 스트리밍에 사용할 수 있도록 설정하는 방법에 대해 알아봅니다.
- Adobe Experience Platform UI를 사용하여 광고 대상을 구성하는 방법을 알아봅니다.
- 세그먼트를 대상에 연결하고 활성화하는 방법에 대해 알아봅니다.
- 양방향 세그먼트 공유 덕분에 Adobe Audience Manager에서 Adobe Experience Platform 세그먼트를 사용하는 방법과 Adobe Experience Platform에서 Adobe Audience Manager 세그먼트를 사용하는 방법을 알아봅니다.

## 전제 조건

- Adobe Experience Platform 액세스: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Adobe Target 액세스
- AWS S3에 액세스

>[!NOTE]
>
>[Experience League 설명서용 Chrome 확장 설치](../../gettingstarted/gettingstarted/ex1.md)에서 참조한 대로 Chrome 확장 기능을 설치, 구성 및 사용하는 것을 잊지 마십시오

## 연습

[2.3.1 세그먼트 만들기](./ex1.md)

세그먼트를 만드는 방법을 알아봅니다.

[2.3.2 대상을 사용하여 DV360 대상을 구성하는 방법 검토](./ex2.md)

Real-Time CDP UI를 사용하여 광고 대상을 구성하는 방법을 알아봅니다.

[2.3.3 조치 취하기: 세그먼트를 DV360으로 보내기](./ex3.md)

연습 6.1에서 작성한 세그먼트를 대상 DV360에 연결합니다.

[2.3.4 조치 취하기: 세그먼트를 S3 대상으로 보내기](./ex4.md)

연습 6.1에서 작성한 세그먼트를 사용하여 일반적으로 이메일 마케팅 대상에 사용되는 S3 대상으로 보냅니다.

[2.3.5 조치 취하기: 세그먼트를 Adobe Target에 보내기](./ex5.md)

연습 6.1에서 작성한 세그먼트를 사용하여 Adobe Target에서 경험 타깃팅 활동을 구성합니다.

[2.3.6 외부 대상](./ex6.md)

외부 소스 시스템의 대상을 Adobe Experience Platform으로 가져옵니다.

[2.3.7 대상 SDK](./ex7.md)

대상 SDK를 사용하여 고유한 대상을 구성합니다.

[요약 및 이점](./summary.md)

이 단원의 요약 및 이점 개요

>[!NOTE]
>
>Adobe Experience Platform과 애플리케이션에 대해 알아야 할 모든 것을 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있는 경우 향후 콘텐츠에 대한 제안 사항에 대한 일반적인 피드백을 공유하려면 기술 인사이더에게 **techinsiders@adobe.com**&#x200B;로 전자 메일을 보내 직접 문의하십시오.

[모든 모듈로 돌아가기](../../../overview.md)
