---
title: 인텔리전트 서비스
description: 인텔리전트 서비스
kt: 5342
audience: Data Engineer, Data Architect, Data Scientist
doc-type: tutorial
activity: develop
exl-id: 99b56722-95bf-4c51-b4d6-8b5a8e5fd936
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 4%

---

# 5. Intelligent Services

**작성자: [디프티만 바다제나](https://www.linkedin.com/in/diptiman-badajena-1b178019/), [우터 반 겔루위](https://www.linkedin.com/in/woutervangeluwe/)**

이 단원에서는 Adobe Experience Platform Intelligent Services를 설정, 구성 및 사용하는 방법을 배웁니다.

## 학습 목표

- Adobe Experience Platform에 익숙해지십시오
- Intelligent Services에서 사용할 스키마/데이터 세트 구성
- 새 Customer AI 인스턴스 만들기
- 점수 대시보드 및 세그멘테이션

## 사전 요구 사항

- Adobe Experience Platform에 액세스: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)

>[!IMPORTANT]
>
>이 자습서는 특정 워크숍 형식을 용이하게 하기 위해 만들어졌습니다. 액세스 권한이 없을 수 있는 특정 시스템 및 계정을 사용합니다. 액세스 권한이 없더라도 이 매우 자세한 내용을 통해 많은 것을 배울 수 있을 것입니다. 워크샵 중 하나에 참여하고 액세스 자격 증명이 필요한 경우 Adobe 담당자에게 연락하여 필요한 정보를 제공합니다.

## 아키텍처 개요

이 모듈에서 논의하고 사용할 구성 요소를 강조 표시하는 아래 아키텍처를 살펴보십시오.

![아키텍처 개요](../../assets/images/architecturem5.png)

## 사용할 샌드박스

이 모듈의 경우 다음 샌드박스를 사용하십시오. `--module10sandbox--`.

>[!NOTE]
>
>에서 참조한 대로 Chrome 확장 프로그램을 설치, 구성 및 사용하는 것을 잊지 마십시오 [0.1 - Experience League 설명서용 Chrome 확장 프로그램 설치](../module0/ex1.md)

## 연습

[5.1 Customer AI - 데이터 준비(수집)](./ex1.md)

고객 데이터는 Adobe Experience Platform의 XDM(Experience Data Model)으로 수집 및 변형됩니다. 특히, Intelligent Services에서 사용되는 모든 데이터 세트는 CEE(Consumer ExperienceEvent) XDM 스키마를 준수해야 합니다.

[5.2 Customer AI - 새 인스턴스 만들기(구성)](./ex2.md)

마케팅 분석가는 비즈니스 규칙을 지정하고 관련 데이터를 식별하여 원하는 예측을 구성합니다. 모델을 구성한 후 실행 일정을 예약하고 점수를 검토합니다.

[5.3 Customer AI - 점수 대시보드 및 세그멘테이션(예측 및 수행)](./ex3.md)

모델이 교육과 점수를 마치면 점수가 다시 플랫폼으로 작성됩니다. 세그먼트 정의, 사용자 정의 대시보드 만들기 등과 같이 예측에 사용할 작업을 결정할 수 있습니다.

>[!NOTE]
>
>Adobe Experience Platform에 대해 알아야 할 모든 것을 배우는 데 시간을 투자해주셔서 감사합니다. 질문이 있는 경우 향후 컨텐츠에 대한 제안 사항이 있는 일반적인 피드백을 공유하려는 경우 Outlook Van Geluwe에게 이메일을 직접 보내주십시오 **vangeluw@adobe.com**.

[모든 모듈로 돌아가기](../../overview.md)
