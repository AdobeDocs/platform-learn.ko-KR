---
title: BigQuery Source Connector를 사용하여 Adobe Experience Platform에서 Google Analytics 데이터 수집 및 분석
description: BigQuery Source Connector를 사용하여 Adobe Experience Platform에서 Google Analytics 데이터 수집 및 분석
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: c9c28b5a-d158-49fa-9533-1a295876f6c4
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 3%

---

# 12. BigQuery 소스 커넥터를 사용하여 Adobe Experience Platform에서 Google Analytics 데이터를 수집 및 분석

**작성자: [빅터 드 라 이글레시아](https://www.linkedin.com/in/victordelaiglesia/), [우터 반 겔루위](https://www.linkedin.com/in/woutervangeluwe/)**

이 모듈에서는 고유한 Google 클라우드 플랫폼 인스턴스를 설정하고, Google Cloud Platform에 샘플 데이터를 로드한 다음 BigQuery Source Connector를 사용하여 Google Cloud Platform의 해당 데이터를 Adobe Experience Platform으로 수집합니다. 마지막으로 Customer Journey Analytics을 사용하여 데이터를 시각화합니다.

Adobe Experience Platform의 소스 커넥터를 사용하면 데이터를 Adobe Experience Platform에 쉽게 가져올 수 있습니다. Google BigQuery는 이미 사용 가능한 커넥터 중 하나입니다. Adobe Experience Platform과 BigQuery Source Connector 덕분에 이제 Customer Journey Analytics에서 Analysis Workspace으로 Google Analytics 데이터를 가져올 수 있습니다.

또한 Customer Journey Analytics 내의 CRM, 콜 센터 또는 충성도 데이터와 같은 다른 데이터 소스와 연결하여 해당 Google Analytics 데이터를 보강할 수 있습니다.

## 학습 목표

- Google Cloud Platform 및 BigQuery 사용자 인터페이스에 익숙해지십시오
- Google Analytics 데이터를 Adobe Experience Platform으로 수집
- Customer Journey Analytics을 사용하여 Google Analytics 데이터 분석 수행
- 오프라인 데이터로 Google Analytics 데이터 보강

## 전제 조건

- Customer Journey Analytics에 익숙하지만 필수는 아닙니다
- Adobe Experience Platform 액세스: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Customer Journey Analytics에 액세스
- Google Cloud Platform 및 Google BigQuery 액세스
- **다음 자산 다운로드**:
   - [JSON - 샘플 데이터: 충성도 데이터](./../../assets/json/bqLoyalty.json)

>[!IMPORTANT]
>
>이 자습서는 특정 워크숍 형식을 용이하게 하기 위해 만들어졌습니다. 액세스 권한이 없을 수 있는 특정 시스템 및 계정을 사용합니다. 액세스 권한이 없더라도 이 매우 자세한 내용을 통해 많은 것을 배울 수 있을 것입니다. 워크샵 중 하나에 참여하고 액세스 자격 증명이 필요한 경우 Adobe 담당자에게 연락하여 필요한 정보를 제공합니다.

## 아키텍처 개요

이 모듈에서 논의하고 사용할 구성 요소를 강조 표시하는 아래 아키텍처를 살펴보십시오.

![아키텍처 개요](../../assets/images/architecturem16.png)

## 사용할 샌드박스

이 모듈의 경우 다음 샌드박스를 사용하십시오. `--aepSandboxId--`.

>[!NOTE]
>
>에서 참조한 대로 Chrome 확장 프로그램을 설치, 구성 및 사용하는 것을 잊지 마십시오 [0.1 - Experience League 설명서용 Chrome 확장 프로그램 설치](../module0/ex1.md)

## 연습

[12.1 Google Cloud Platform 계정 만들기](./ex1.md)

Google Cloud Platform 계정을 만듭니다.

[12.2 BigQuery에서 첫 번째 쿼리 만들기](./ex2.md)

BigQuery를 사용하여 Platform에 로드할 데이터를 준비하는 방법을 배웁니다.

[12.3 GCP 및 BigQuery를 Adobe Experience Platform에 연결](./ex3.md)

Adobe Experience Platform에서 소스 커넥터를 설정하는 방법을 알아봅니다.

[12.4 BigQuery에서 Adobe Experience Platform으로 데이터 로드](./ex4.md)

Adobe Experience Platform에서 BigQuery 소스 커넥터를 구성하여 Google Analytics 데이터를 수집하는 방법을 알아봅니다.

[12.5 Customer Journey Analytics을 사용하여 Google Analytics 데이터 분석](./ex5.md)

Customer Journey Analytics에서 Google Analytics 데이터를 분석하고 충성도 데이터와 결합하는 방법을 알아봅니다.

[요약 및 이점](./summary.md)

이 모듈의 요약 및 이점 개요

>[!NOTE]
>
>Adobe Experience Platform에 대해 알아야 할 모든 것을 배우는 데 시간을 투자해주셔서 감사합니다. 질문이 있는 경우 향후 컨텐츠에 대한 제안 사항이 있는 일반적인 피드백을 공유하려는 경우 Outlook Van Geluwe에게 이메일을 직접 보내주십시오 **vangeluw@adobe.com**.

[모든 모듈로 돌아가기](../../overview.md)
