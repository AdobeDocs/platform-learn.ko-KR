---
title: Foundation - 실시간 고객 프로필
description: Foundation - 실시간 고객 프로필
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 050e5d99-544d-4a86-a7f6-9f103381dca5
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 1%

---

# 3. 기초 - 실시간 고객 프로필

**작성자: [우터 반 겔루위](https://www.linkedin.com/in/woutervangeluwe/)**

이 단원에서는 Adobe Experience Platform의 실시간 고객 프로필 및 ID 기능에 대해 자세히 살펴봅니다. 대상을 정의하는 방법, ID 서비스 및 Experience Cloud ID의 역할, 세그먼트 빌더 쿼리를 정의하여 고유한 세그먼트를 정의하는 방법을 알아봅니다.

## 학습 목표

- Adobe Experience Platform의 UI를 통해 고객의 실시간 고객 프로필을 시각화하는 방법을 알아봅니다
- Adobe Experience Platform의 세그먼트 빌더를 사용하여 세그먼트를 만드는 방법을 알아봅니다
- Adobe Experience Platform API를 사용하여 세그먼트를 만들고 세그먼트의 결과를 데이터 세트에 저장하는 방법을 알아봅니다
- 오프라인 환경에서 실시간 동작을 포함하여 전체 고객 프로필에 액세스할 수 있는 영향에 대해 알아봅니다

## 전제 조건

- 액세스 권한 [Adobe Experience Platform](https://experience.adobe.com/platform)
- 액세스 권한 [https://public.aepdemo.net](https://public.aepdemo.net)
- **다음 자산 다운로드**:
   - [Postman 컬렉션](./../../assets/postman/postman_profile.zip)

>[!IMPORTANT]
>
>이 자습서는 특정 워크숍 형식을 용이하게 하기 위해 만들어졌습니다. 액세스 권한이 없을 수 있는 특정 시스템 및 계정을 사용합니다. 액세스 권한이 없더라도 이 매우 자세한 내용을 통해 많은 것을 배울 수 있을 것입니다. 워크샵 중 하나에 참여하고 액세스 자격 증명이 필요한 경우 Adobe 담당자에게 연락하여 필요한 정보를 제공합니다.

## 아키텍처 개요

이 모듈에서 논의하고 사용할 구성 요소를 강조 표시하는 아래 아키텍처를 살펴보십시오.

![아키텍처 개요](../../assets/images/architecturem3.png)

## 사용할 샌드박스

이 모듈의 경우 다음 샌드박스를 사용하십시오. `--aepSandboxId--`.

>[!NOTE]
>
>에서 참조한 대로 Chrome 확장 프로그램을 설치, 구성 및 사용하는 것을 잊지 마십시오 [0.1 - Experience League 설명서용 Chrome 확장 프로그램 설치](../module0/ex1.md)

## 연습

[3.1 웹 사이트 방문](./ex1.md)

이 연습에서는 스크립트를 따라 웹 사이트를 살펴봅니다.

[3.2 실시간 고객 프로필 시각화 - UI](./ex2.md)

이 연습에서는 Adobe Experience Platform에 로그인하고 UI에서 고유한 실시간 고객 프로필을 보게 됩니다.

[3.3 실시간 고객 프로필 시각화 - API](./ex3.md)

이 연습에서는 Adobe Experience Platform의 API를 사용하여 Postman 및 Adobe I/O을 사용하여 실시간 고객 프로필을 봅니다.

[3.4 세그먼트 만들기 - UI](./ex4.md)

이 연습에서는 Adobe Experience Platform의 세그먼트 빌더를 사용하여 세그먼트를 만듭니다.

[3.5 세그먼트 만들기 - API](./ex5.md)

이 연습에서는 Adobe Experience Platform의 API를 사용하여 Postman 및 Adobe I/O을 사용하여 세그먼트를 만들고 해당 세그먼트의 결과를 데이터 세트로 저장합니다.

[3.6 콜 센터에서 실시간 고객 프로필 활용 사례 보기](./ex6.md)

이 연습에서는 고객으로부터 전화를 받는 콜 센터 직원을 가장하게 됩니다. 이 고객의 경험에 실제로 영향을 주려면 사용 가능한 모든 정보에 실시간으로 액세스해야 합니다.

[요약 및 이점](./summary.md)

이 모듈의 요약 및 이점 개요

>[!NOTE]
>
>Adobe Experience Platform에 대해 알아야 할 모든 것을 배우는 데 시간을 투자해주셔서 감사합니다. 질문이 있는 경우 향후 컨텐츠에 대한 제안 사항이 있는 일반적인 피드백을 공유하려는 경우 Outlook Van Geluwe에게 이메일을 직접 보내주십시오 **vangeluw@adobe.com**.

[모든 모듈로 돌아가기](../../overview.md)
