---
title: 실시간 CDP - 세그먼트 구축 및 조치 수행
description: 실시간 CDP - 세그먼트 구축 및 조치 수행
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 147d9153-5742-4857-aae1-0ec434a1e626
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 2%

---

# 6. 실시간 CDP - 세그먼트 구축 및 조치 수행

**작성자: [우터 반 겔루위](https://www.linkedin.com/in/woutervangeluwe/), [알베르토 드 카로](https://www.linkedin.com/in/albertodecaro/), [베네딕트 웨데니크](https://www.linkedin.com/in/benedikt-wedenik/)**

이 단원에서는 스트리밍 세그먼트를 구성하고 세그먼트를 여러 대상에 활성화합니다.

## 학습 목표

- 세그먼트를 만들고 스트리밍에 사용하도록 설정하는 방법을 알아봅니다.
- Adobe Experience Platform UI를 사용하여 광고 대상을 구성하는 방법을 알아봅니다.
- 세그먼트를 대상에 연결하고 활성화하는 방법을 알아봅니다.
- 양방향 세그먼트 공유를 통해 Adobe Audience Manager에서 Adobe Experience Platform 세그먼트를 사용하는 방법과 Adobe Experience Platform에서 Adobe Audience Manager 세그먼트를 사용하는 방법을 알아봅니다.

## 사전 요구 사항

- Adobe Experience Platform에 액세스: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Adobe Target 액세스
- AWS S3에 액세스

>[!IMPORTANT]
>
>이 자습서는 특정 워크숍 형식을 용이하게 하기 위해 만들어졌습니다. 액세스 권한이 없을 수 있는 특정 시스템 및 계정을 사용합니다. 액세스 권한이 없더라도 이 매우 자세한 내용을 통해 많은 것을 배울 수 있을 것입니다. 워크샵 중 하나에 참여하고 액세스 자격 증명이 필요한 경우 Adobe 담당자에게 연락하여 필요한 정보를 제공합니다.

## 아키텍처 개요

이 모듈에서 논의하고 사용할 구성 요소를 강조 표시하는 아래 아키텍처를 살펴보십시오.

![아키텍처 개요](../../assets/images/architecturem11.png)

## 사용할 샌드박스

이 모듈의 경우 다음 샌드박스를 사용하십시오. `--module11sandbox--`.

>[!NOTE]
>
>에서 참조한 대로 Chrome 확장 프로그램을 설치, 구성 및 사용하는 것을 잊지 마십시오 [0.1 - Experience League 설명서용 Chrome 확장 프로그램 설치](../module0/ex1.md)

## 연습

[6.1 세그먼트 만들기](./ex1.md)

세그먼트를 만드는 방법을 알아봅니다.

[6.2 대상을 사용하여 DV360 대상을 구성하는 방법 검토](./ex2.md)

Real-Time CDP UI를 사용하여 광고 대상을 구성하는 방법을 알아봅니다.

[6.3 조치 수행: 세그먼트를 DV360으로 보내기](./ex3.md)

연습 6.1에서 작성한 세그먼트를 대상 DV360에 연결합니다.

[6.4 조치 수행: S3 대상에 세그먼트 보내기](./ex4.md)

experience 6.1에서 작성한 세그먼트를 사용하여 S3 대상에 전송하며 일반적으로 이메일 마케팅 대상에 사용됩니다.

[6.5 조치 수행: Adobe Target에 세그먼트 보내기](./ex5.md)

연습 6.1에서 작성한 세그먼트를 사용하여 Adobe Target에서 경험 타깃팅 활동을 구성합니다.

[6.6 외부 대상](./ex6.md)

외부 소스 시스템의 대상을 Adobe Experience Platform으로 가져옵니다.

[6.7 대상 SDK](./ex7.md)

대상 SDK를 사용하여 고유한 대상을 구성합니다.

[요약 및 이점](./summary.md)

이 모듈의 요약 및 이점 개요

>[!NOTE]
>
>Adobe Experience Platform에 대해 알아야 할 모든 것을 배우는 데 시간을 투자해주셔서 감사합니다. 질문이 있는 경우 향후 컨텐츠에 대한 제안 사항이 있는 일반적인 피드백을 공유하려는 경우 Outlook Van Geluwe에게 이메일을 직접 보내주십시오 **vangeluw@adobe.com**.

[모든 모듈로 돌아가기](../../overview.md)
