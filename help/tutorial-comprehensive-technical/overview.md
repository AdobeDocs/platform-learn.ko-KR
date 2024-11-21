---
title: 개요
description: 데이터 엔지니어, 데이터 분석가, 데이터 설계자, 데이터 과학자, 오케스트레이션 엔지니어 및 마케터가 Adobe Experience Platform 및 모든 애플리케이션 서비스의 비즈니스 가치를 완전히 이해할 수 있는 시작점입니다.
doc-type: multipage-overview
hide: false
exl-id: 88c19383-c185-40f0-b118-6cb82db0ce0e
source-git-commit: b6c98ca773ba46205c467321a7796c29b614e75c
workflow-type: tm+mt
source-wordcount: '1511'
ht-degree: 2%

---

# Adobe Experience Platform을 위한 포괄적인 기술 튜토리얼

## 개요

이 자습서는 데이터 엔지니어, 데이터 분석가, 데이터 설계자, 데이터 과학자, 오케스트레이션 엔지니어 및 마케터가 Adobe Experience Platform 및 모든 애플리케이션 서비스의 비즈니스 가치를 완전히 이해할 수 있는 완벽한 시작점입니다. 각 단원에서는 오늘날의 복잡한 개인화 생태계에서 직면한 진정한 도전을 중점적으로 다룹니다. 다양한 실습 위주의 연습에서 Experience Platform이 이러한 도전을 해결하는 방법을 분류합니다.

이 튜토리얼은 매우 다양하며 다음 애플리케이션에 대한 명확한 통찰력을 제공합니다.

- Adobe Experience Platform
- Adobe Experience Platform 데이터 수집
- 실시간 CDP
- Adobe Journey Optimizer
- Customer Journey Analytics

이 튜토리얼은 Adobe 애플리케이션에만 중점을 두지 않고 브랜드가 작동하는 광범위한 에코시스템을 고려합니다. 이를 위해 일부 단원에서는 _Adobe이 아닌_ 응용 프로그램을 Adobe Experience Platform과 통합하는 방법에 중점을 두고 있습니다. 따라서 다음 애플리케이션이 Adobe Experience Platform과 함께 작동하는 방식을 깊이 이해할 수 있습니다.

- Amazon: AWS 람다, AWS S3, AWS Kinesis
- Google: Google Cloud Platform, Google BigQuery, Google Display&amp;Video 360, Google AdWords
- Microsoft: Power BI, Azure EventHub, Azure Blob 저장소
- Salesforce: 타블로
- 아파치 카프카
- Postman
- ...

이 자습서의 연습을 완료하면 다음 작업을 수행할 수 있습니다.

- 스키마, 필드 그룹, 데이터 세트 및 ID 구성
- Adobe Experience Platform 데이터 수집 속성 구성 및 Adobe Experience Platform 데이터 수집에서 새 Web SDK 확장 설정
- Adobe Experience Platform 데이터 수집을 사용하여 실시간으로 Adobe Experience Platform에 데이터 스트리밍
- 워크플로우를 사용하거나 추출, 변환, 로드(ETL) 애플리케이션을 사용하여 데이터를 Adobe Experience Platform에 일괄 처리 수집
- Adobe Experience Platform에서 실시간 고객 프로필 시각화 및 사용
- 대상자 만들기
- 여러 Adobe Experience Platform API 사용
- SQL을 사용하여 Adobe Experience Platform에서 데이터 쿼리
- 트리거 기반의 실시간 여정 구성 및 실행
- Real-Time CDP를 사용하여 대상을 다양한 대상으로 활성화함으로써 조치를 취할 수 있습니다
- Customer Journey Analytics을 사용하여 Google BigQuery를 비롯한 다양한 소스의 옴니채널 고객 데이터에 대해 보고합니다

## 전제 조건

- Adobe Experience Platform 액세스: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Adobe Experience Platform 데이터 수집에 액세스: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- 데모 시스템 액세스: [https://dsn.adobe.com/](https://dsn.adobe.com/)

## 비디오

기술 아카데미 웨비나, 부트캠프 등에서 흥미로운 동영상을 [Experience Makers 커뮤니티 YouTube 채널](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw)에서 많이 볼 수 있습니다.

## 콘텐츠

[0. 시작하기](./modules/gettingstarted/gettingstarted/getting-started.md)

- **대상:** Adobe Experience Platform을 위한 포괄적인 기술 자습서의 모든 참가자
- **필수 구성 요소:** 다음 데모 시스템, Adobe Experience Platform 및 Adobe Experience Platform 데이터 수집에 액세스합니다.
- **설명:** 이 기본 모듈에서는 데모 환경에 액세스하고 사용할 수 있도록 모든 기능을 설정합니다.
- **시간 투자:** 30분

### 1. 데이터 수집

[1.1 Foundation - Adobe Experience Platform 데이터 수집 및 웹 SDK 설정](./modules/datacollection/module1.1/data-ingestion-launch-web-sdk.md)

- **대상:** 데이터 엔지니어, 데이터 설계자
- **필수 구성 요소:** Adobe Experience Platform 및 Adobe Experience Platform 데이터 수집에 대한 액세스 권한.
- **설명:** 이 기본 모듈에서는 Adobe Experience Platform 데이터 수집 및 새 Web SDK 확장에 대해 알아봅니다.
- **시간 투자:** 30분

[1.2 Foundation - 데이터 수집](./modules/datacollection/module1.2/data-ingestion.md)

- **대상:** 데이터 엔지니어, 데이터 설계자
- **필수 구성 요소:** Adobe Experience Platform 및 Adobe Experience Platform 데이터 수집에 대한 액세스 권한.
- **설명:** 이 기본 모듈에서는 웹 사이트의 데이터를 플랫폼으로 수집합니다.
- **시간 투자:** 120분

[1.3 페더레이션 대상 구성](./modules/datacollection/module1.3/fac.md)

- **대상:** 데이터 분석가, 데이터 엔지니어, 데이터 설계자
- Adobe Experience Platform에 대한 **필수 구성 요소:** 액세스
- **설명:** 이 모듈에서는 Kafka Connect용 Adobe Experience Platform 싱크 커넥터를 사용하여 Apache Kafka 클러스터를 설정하고, 주제, 제작자 및 소비자를 정의하고, Adobe Experience Platform에 데이터를 스트리밍하는 방법에 대해 알아봅니다.
- **시간 투자:** 90분

### 2. Real-Time CDP B2C

[2.1 Foundation - 실시간 고객 프로필](./modules/rtcdp-b2c/module2.1/real-time-customer-profile.md)

- **대상:** 데이터 엔지니어, 데이터 설계자, 마케터
- **필수 구성 요소:** Adobe Experience Platform 및 Postman 액세스
- **설명:** 이 기본 모듈에서는 UI와 API를 사용하여 Adobe Experience Platform의 실시간 고객 프로필을 살펴봅니다.
- **시간 투자:** 90분
- **이 에셋 다운로드**:
   - [Postman 컬렉션](./assets/postman/postman_profile.zip)

[2.2 지능형 서비스](./modules/rtcdp-b2c/module2.2/intelligent-services.md)

- **대상:** 데이터 엔지니어, 데이터 설계자, 데이터 과학자
- **필수 구성 요소:** Adobe Experience Platform, Intelligent Services 액세스
- **설명:** 이 모듈에서는 Adobe Experience Platform Intelligent Services를 설정, 구성 및 사용하는 방법을 배웁니다.
- **시간 투자:** 60분

[2.3 Real-Time CDP - 대상 구축 및 조치](./modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md)

- **대상:** 데이터 설계자, 오케스트레이션 엔지니어, 마케터
- **사전 요구 사항:** Adobe Experience Platform, Real-Time CDP, Adobe Audience Manager, Adobe Target, AWS S3에 액세스
- **설명:** 이 모듈에서는 대상을 구성하고 Google DV360, Adobe Target 및 AWS S3 등 여러 대상에 대상을 활성화합니다.
- **시간 투자:** 90분

[2.4 Real-Time CDP: Microsoft Azure Event Hub Audience Activation](./modules/rtcdp-b2c/module2.4/segment-activation-microsoft-azure-eventhub.md)

- **대상:** 데이터 엔지니어, 데이터 설계자, 데이터 분석가
- **사전 요구 사항:** Adobe Experience Platform, Real-time CDP 및 Microsoft Azure에 대한 액세스 권한
- **설명:** 이 모듈에서는 Microsoft Azure EventHub 대상을 Adobe Experience Platform Real-time CDP의 실시간 대상으로 설정합니다. 또한 Adobe Experience Platform이 대상 페이로드를 Azure EventHub 대상에 전달할 때마다 실시간으로 트리거되는 Azure 기능을 설정하고 배포합니다. 트리거할 Azure 기능은 Adobe Experience Platform Real-time CDP의 활성화 기능의 메커니즘을 보여 줍니다.
또한 이 모듈의 일부로 Real-Time CDP를 트리거하여 실제로 페이로드를 지정된 대상에 전달하는 방법에 대해 이해할 수 있습니다. 또한 대상 자격 상태와 작동 방식에 대해서도 설명합니다.
- **시간 투자:** 90분

[2.5 Real-Time CDP 연결: 이벤트 전달](./modules/rtcdp-b2c/module2.5/aep-data-collection-ssf.md)

- **대상:** 데이터 엔지니어, 데이터 설계자, 데이터 분석가
- **필수 구성 요소:** Real-Time CDP 연결, 태그 및 이벤트 전달 속성에 대한 액세스
- **설명:** 이 모듈에서는 이전에 구성한 데이터 세트, 스키마 및 Adobe Experience Platform 데이터 수집 속성을 사용하여 데이터를 수집한 다음 해당 데이터 서버측을 원하는 끝점으로 전달합니다.
- **시간 투자:** 90분

[2.6 Apache Kafka에서 Real-Time CDP으로 데이터 스트리밍](./modules/rtcdp-b2c/module2.6/aep-apache-kafka.md)

- **대상:** 데이터 분석가, 데이터 엔지니어, 데이터 설계자
- Adobe Experience Platform에 대한 **필수 구성 요소:** 액세스
- **설명:** 이 모듈에서는 Kafka Connect용 Adobe Experience Platform 싱크 커넥터를 사용하여 Apache Kafka 클러스터를 설정하고, 주제, 제작자 및 소비자를 정의하고, Adobe Experience Platform에 데이터를 스트리밍하는 방법에 대해 알아봅니다.
- **시간 투자:** 90분

### 3. Adobe Journey Optimizer B2C

[3.1 Adobe Journey Optimizer: 오케스트레이션](./modules/ajo-b2c/module3.1/journey-orchestration-create-account.md)

- **대상:** 데이터 엔지니어, 데이터 설계자, 오케스트레이션 엔지니어
- **필수 구성 요소:** Adobe Experience Platform 및 Adobe Journey Optimizer 액세스
- **설명:** 이 모듈에서는 Adobe Journey Optimizer을 사용하여 트리거 기반 여정을 빌드합니다.
- **시간 투자:** 60분

[3.2 Adobe Journey Optimizer: 외부 데이터 소스 및 사용자 지정 작업](./modules/ajo-b2c/module3.2/journey-orchestration-external-weather-api-sms.md)

- **대상:** 데이터 엔지니어, 데이터 설계자, 오케스트레이션 엔지니어, 마케터
- **사전 요구 사항:** Adobe Experience Platform, Adobe Journey Optimizer, Open Weather API, Twilio 액세스
- **설명:** 이 모듈에서는 Adobe Journey Optimizer을 사용하여 온라인과 오프라인 모두에서 고객 행동을 청취하고 다양한 채널을 통해 지능적이고 상황에 맞는 실시간 방식으로 응답합니다.
- **시간 투자:** 90분

[3.3 Adobe Journey Optimizer: Offer decisioning](./modules/ajo-b2c/module3.3/offer-decisioning.md)

- **대상:** 데이터 엔지니어, 데이터 설계자, 오케스트레이션 엔지니어, 마케터
- **필수 구성 요소:** Adobe Experience Platform 및 Offer decisioning 액세스
- **설명:** 이 단원에서는 Adobe Experience Platform - Offers/Decisioning 응용 프로그램 서비스를 직접 사용하여 개인화된 오퍼 및 고유한 오퍼 활동을 구성합니다.
- **시간 투자:** 120분

[3.4 Adobe Journey Optimizer: 이벤트 기반 여정](./modules/ajo-b2c/module3.4/journeyoptimizer.md)

- **대상:** 전자 메일 마케터, 오케스트레이션 전문가, 데이터 엔지니어, 데이터 설계자, 데이터 분석가
- **필수 구성 요소:** Adobe Experience Platform 및 Journey Optimizer 액세스
- **설명:** 이 모듈에서는 기업이 고객에게 연관성 있고 상황에 맞는 개인화된 경험을 디자인하고 제공하는 데 도움이 되는 Journey Optimizer에 대해 알아야 할 모든 사항을 알아봅니다.
- **시간 투자:** 120분

### 4. Adobe Customer Journey Analytics

[4.1 Customer Journey Analytics: Adobe Experience Platform 맨 위에서 Analysis Workspace을 사용하여 대시보드 빌드](./modules/cja-b2c/module4.1/customer-journey-analytics-build-a-dashboard.md)

- **대상:** 데이터 엔지니어, 데이터 설계자, 데이터 분석가
- **필수 구성 요소:** Adobe Experience Platform 및 Customer Journey Analytics 액세스
- **설명:** 이 모듈에서는 웹 사이트 상호 작용, 모바일 앱 상호 작용, 콜 센터 상호 작용, 매장 내 상호 작용 등과 같은 옴니채널 데이터가 포함된 대시보드를 구성하여 오프라인 인사이트에 대한 온라인 인사이트를 얻을 수 있습니다.
- **시간 투자:** 120분

[4.2 Customer Journey Analytics: BigQuery Source 커넥터를 사용하여 Adobe Experience Platform에서 Google Analytics 데이터 수집 및 분석](./modules/cja-b2c/module4.2/customer-journey-analytics-bigquery-gcp.md)

- **대상:** 데이터 엔지니어, 데이터 설계자, 데이터 분석가
- **사전 요구 사항:** Adobe Experience Platform, Customer Journey Analytics, Google Cloud Platform, Google BigQuery에 액세스
- **설명:** 이 모듈에서는 고유한 Google Cloud Platform 인스턴스를 설정하고 Google Cloud Platform에서 데모 데이터를 로드한 다음 BigQuery Source 커넥터를 사용하여 Google Cloud Platform에서 Adobe Experience Platform으로 해당 데이터를 수집합니다. 마지막으로 Customer Journey Analytics을 사용하여 해당 데이터를 시각화합니다.
- **시간 투자:** 120분
- **이 에셋 다운로드**:
   - [JSON - 샘플 데이터: 데모 - 충성도 데이터](./assets/json/bqLoyalty.json)

### 5. 데이터 Distiller

[5.1 쿼리 서비스](./modules/datadistiller/module5.1/query-service.md)

- **대상:** 데이터 엔지니어, 데이터 설계자, 데이터 분석가, BI 전문가
- **필수 구성 요소:** Adobe Experience Platform, 쿼리 서비스, Power BI 또는 타블로에 액세스
- **설명:** 이 모듈에서는 Adobe Experience Platform 쿼리 서비스를 사용하는 방법을 배웁니다.
- **시간 투자:** 90분
- **이 에셋 다운로드**:
   - [JSON - 샘플 데이터: 데모 시스템 - 웹 사이트용 이벤트 데이터 세트](./assets/json/ee.json)
   - [JSON - 샘플 데이터: 데모 시스템 - 콜 센터용 이벤트 데이터 세트](./assets/json/callcenter.json)
   - [JSON - 샘플 데이터: 데모 시스템 - 충성도를 위한 프로필 데이터 세트](./assets/json/loyalty.json)





