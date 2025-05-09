---
title: BigQuery Source 커넥터를 사용하여 Adobe Experience Platform에서 Google Analytics 데이터 수집 및 분석
description: BigQuery Source 커넥터를 사용하여 Adobe Experience Platform에서 Google Analytics 데이터 수집 및 분석
kt: 5342
doc-type: tutorial
exl-id: 19266ac3-7c93-4cdb-8b65-75ce5c38649c
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# 1.2 BigQuery Source 커넥터를 사용하여 Adobe Experience Platform에서 Google Analytics 데이터 수집 및 분석

이 모듈에서는 고유한 Google Cloud Platform 인스턴스를 설정하고 Google Cloud Platform에서 샘플 데이터를 로드한 다음 BigQuery Source 커넥터를 사용하여 해당 데이터를 Google Cloud Platform에서 Adobe Experience Platform으로 수집합니다. 마지막으로 Customer Journey Analytics을 사용하여 해당 데이터를 시각화합니다.

Adobe Experience Platform의 Source 커넥터를 사용하면 데이터를 Adobe Experience Platform으로 쉽게 가져올 수 있습니다. Google BigQuery는 이미 사용 가능한 커넥터 중 하나입니다. Adobe Experience Platform 및 BigQuery Source 커넥터 덕분에 이제 Google Analytics 데이터를 Customer Journey Analytics의 Analysis Workspace으로 가져올 수 있습니다.

또한 Customer Journey Analytics 내의 CRM, 콜 센터 또는 로열티 데이터와 같은 다른 데이터 소스와 결합하여 Google Analytics 데이터를 강화할 수 있습니다.

## 학습 목표

- Google 클라우드 플랫폼 및 BigQuery 사용자 인터페이스에 익숙해지기
- Google Analytics 데이터를 Adobe Experience Platform에 수집
- Customer Journey Analytics을 사용하여 Google Analytics 데이터 분석 수행
- 오프라인 데이터로 Google Analytics 데이터 강화

## 전제 조건

- Customer Journey Analytics에 익숙해지는 것이 선호되지만 필수는 아닙니다
- Adobe Experience Platform 액세스: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Customer Journey Analytics 액세스
- Google 클라우드 플랫폼 및 Google BigQuery에 액세스
- **이 에셋 다운로드**:
   - [JSON - 샘플 데이터: 충성도 데이터](./../../../../assets/json/bqLoyalty.json)

>[!NOTE]
>
>[Chrome 설명서용 Chrome 확장 설치](../../../getting-started/gettingstarted/ex1.md)에서 참조한 대로 Experience League 확장 기능을 설치, 구성 및 사용하는 것을 잊지 마십시오

## 연습

[1.2.1 Google Cloud Platform 사용 시작](./ex1.md)

Google Cloud Platform 환경 사용을 시작합니다.

[1.2.2 BigQuery에서 첫 번째 쿼리 만들기](./ex2.md)

BigQuery를 사용하여 데이터를 플랫폼으로 로드하는 방법에 대해 알아봅니다.

[1.2.3 GCP 및 BigQuery를 Adobe Experience Platform에 연결](./ex3.md)

Adobe Experience Platform에서 소스 커넥터를 설정하는 방법을 알아봅니다.

[1.2.4 BigQuery에서 Adobe Experience Platform으로 데이터 로드](./ex4.md)

Adobe Experience Platform에서 BigQuery 소스 커넥터를 구성하여 Google Analytics 데이터를 수집하는 방법을 알아봅니다.

[1.2.5 Customer Journey Analytics을 사용하여 Google Analytics 데이터 분석](./ex5.md)

Customer Journey Analytics에서 Google Analytics 데이터를 분석하고 충성도 데이터와 결합하는 방법에 대해 알아봅니다.

[요약 및 이점](./summary.md)

이 단원의 요약 및 이점 개요

![기술 내부자](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Adobe Experience Platform과 애플리케이션에 대해 알아야 할 모든 것을 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있는 경우 향후 콘텐츠에 대한 제안 사항에 대한 일반적인 피드백을 공유하려면 기술 인사이더에게 **techinsiders@adobe.com**&#x200B;로 전자 메일을 보내 직접 문의하십시오.

[모든 모듈로 돌아가기](./../../../../overview.md)
