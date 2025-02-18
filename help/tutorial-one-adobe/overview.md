---
title: 개요 - 포괄적인 기술 튜토리얼 - One Adobe
description: 포괄적인 기술 튜토리얼 - One Adobe
doc-type: multipage-overview
exl-id: 5bc0d621-0662-4d94-80a0-b6c173c0ac9e
source-git-commit: 9169b0f9be7f192fd7e16ddcc2ae32f6a8cca92c
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 2%

---

# 포괄적인 기술 튜토리얼 - One Adobe

![기술 내부자](./assets/images/techinsiders.png){width="50px" align="left"}

## 개요

이 튜토리얼은 매우 다양하며 다음 애플리케이션에 대한 명확한 통찰력을 제공합니다.

- Adobe Firefly 서비스
- Adobe Photoshop
- Adobe Workfront 및 Adobe Workfront Fusion
- Adobe Experience Manager Cloud Service, Sites, Assets 및 Edge Delivery Services
- Adobe Experience Platform
- Adobe Real-Time CDP
- Adobe Journey Optimizer


이 튜토리얼은 Adobe 애플리케이션에만 중점을 두지 않고 브랜드가 작동하는 광범위한 에코시스템을 고려합니다. 이를 위해 일부 단원에서는 Adobe이 아닌 애플리케이션을 Adobe 애플리케이션과 통합하는 방법에 중점을 두고 있습니다. 따라서 다음 애플리케이션이 Adobe Experience Platform과 함께 작동하는 방식을 깊이 이해할 수 있습니다.

- Amazon AWS
- Google Cloud 플랫폼
- Microsoft Azure
- Postman
- Snowflake
- ...

## 전제 조건

고유한 Adobe Experience Cloud 인스턴스를 사용하여 이 자습서를 수행하려면 인스턴스에서 다음 애플리케이션을 프로비저닝하고 액세스할 수 있어야 합니다.

- Adobe Firefly [https://firefly.adobe.com/](https://firefly.adobe.com/){target="_blank"}
- Adobe Photoshop
- Adobe Workfront
- Adobe Workfront Fusion [https://fusion.adobe.com/](https://fusion.adobe.com/){target="_blank"}
- Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform){target="_blank"}
- Adobe Experience Platform 데이터 수집: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/){target="_blank"}
- 데모 시스템 액세스: [https://dsn.adobe.com/](https://dsn.adobe.com/){target="_blank"}

## 완료 및 인증

이 튜토리얼은 Adobe 인증 교육 과정의 일부입니다. [https://certification.adobe.com](https://certification.adobe.com)&#x200B;(으)로 이동하여 이 자습서와 함께 과정에 등록할 수 있습니다.

아래 자습서를 사용하여 완료하는 모든 모듈에 대해 [여기](./completion.md)에 표시된 대로 완료 증명을 제출해야 합니다.

## 컨텐츠 상태

아래 콘텐츠의 상태를 확인하려면 [상태 페이지](./status.md){target="_blank"}(으)로 이동하세요.

### 시작하기

[시작](./modules/getting-started/gettingstarted/getting-started.md){target="_blank"}

이 기본 모듈에서는 데모 환경에 액세스하고 사용할 수 있도록 모든 것을 준비합니다.

### 1. 워크플로 및 계획

### 2. 제작 및 제작

[1.1 Adobe Firefly 서비스](./modules/creation-production/module1.1/firefly-services.md){target="_blank"}

이 모듈에서는 Adobe Firefly Services API, Photoshop API 및 Microsoft Azure Storage Services를 사용하여 이미지를 생성하고 프로그래밍 방식으로 저장합니다.

Workfront Fusion을 사용한 [1.2 Creative Workflow Automation](./modules/creation-production/module1.2/automation.md){target="_blank"}

이 기본 모듈에서는 Adobe Workfront Fusion을 사용하여 콘텐츠 제작 워크플로를 자동화하고 확장하게 됩니다.

### 3. 자산 관리

[1.1 Adobe Experience Manager Cloud Service 및 Edge Delivery Services](./modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}

이 기본 모듈에서는 Adobe Experience Manager Cloud Service 프로그램, 사이트 및 Assets 저장소를 설정합니다.

Adobe Workfront을 사용한 [1.2 워크플로 관리](./modules/asset-mgmt/module2.2/workfront.md){target="_blank"}

이 기본 모듈에서는 Adobe Workfront을 구성 및 사용하여 승인 흐름을 관리하고 Adobe Experience Manager Assets, 유니버설 편집기, Photoshop 등과의 통합을 사용합니다.

### 4. 배달 및 활성화

#### 데이터 수집

[1.1 Foundation - Adobe Experience Platform 데이터 수집 및 웹 SDK 설정](./modules/delivery-activation/datacollection/dc1.1/data-ingestion-launch-web-sdk.md)

이 기본 모듈에서는 Adobe Experience Platform 데이터 수집 및 새로운 웹 SDK 확장에 대해 알아봅니다.

[1.2 Foundation - 데이터 수집](./modules/delivery-activation/datacollection/dc1.2/data-ingestion.md)

이 기본 모듈에서는 다양한 소스의 데이터를 Adobe Experience Platform으로 수집합니다

[1.3 페더레이션 대상 구성](./modules/delivery-activation/datacollection/dc1.3/fac.md)

이 모듈에서는 Federated Audiences 모델을 설정하고 Federated Data를 사용하여 대상을 생성하는 방법에 대해 알아봅니다.

#### Real-Time CDP

[2.1 Foundation - 실시간 고객 프로필](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-1/real-time-customer-profile.md)

이 기본 모듈에서는 UI 및 API를 사용하여 Adobe Experience Platform의 실시간 고객 프로필을 살펴봅니다.

[2.2 지능형 서비스](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-2/intelligent-services.md)

이 모듈에서는 Adobe Experience Platform Intelligent Services를 설정, 구성 및 사용하는 방법을 배웁니다.

[2.3 Real-Time CDP - 대상 구축 및 조치](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-3/real-time-cdp-build-a-segment-take-action.md)

이 모듈에서는 대상을 구성하고 Google DV360, Adobe Target 및 AWS S3을 포함한 여러 대상에 대상을 활성화합니다.

[2.4 Real-Time CDP: Audience Activation에서 Microsoft Azure Event Hub로](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-4/segment-activation-microsoft-azure-eventhub.md)

이 모듈에서는 Microsoft Azure EventHub 대상을 Adobe Experience Platform Real-time CDP의 실시간 대상으로 설정합니다.

[2.5 Real-Time CDP 연결: 이벤트 전달](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-5/aep-data-collection-ssf.md)

이 모듈에서는 서버측에서 Google Cloud Platform Pub/Sub 및 AWS Kinesis와 같은 여러 엔드포인트로 데이터를 전달합니다.

[2.6 Apache Kafka에서 Real-Time CDP으로 데이터 스트리밍](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-6/aep-apache-kafka.md)

이 모듈에서는 고유한 Apache Kafka 클러스터를 설정하고 데이터를 Adobe Experience Platform에 스트리밍하는 방법에 대해 알아봅니다.

#### Adobe Journey Optimizer

[3.1 Adobe Journey Optimizer: 오케스트레이션](./modules/delivery-activation/ajo-b2c/ajob2c-1/journey-orchestration-create-account.md)

이 모듈에서는 Adobe Journey Optimizer을 사용하여 트리거 기반 여정을 빌드합니다.

[3.2 Adobe Journey Optimizer: 외부 데이터 소스 및 사용자 지정 작업](./modules/delivery-activation/ajo-b2c/ajob2c-2/journey-orchestration-external-weather-api-sms.md)

이 모듈에서는 Adobe Journey Optimizer을 사용하여 온라인과 오프라인 모두에서 고객 행동을 청취하고 다양한 채널을 통해 지능적이고 상황에 맞는 실시간 방식으로 응답합니다.

[3.3 Adobe Journey Optimizer: Offer Decisioning](./modules/delivery-activation/ajo-b2c/ajob2c-3/offer-decisioning.md)

이 모듈에서는 Adobe Journey Optimizer을 사용하여 개인화된 오퍼와 나만의 오퍼 의사 결정을 구성합니다.

[3.4 Adobe Journey Optimizer: 이벤트 기반 여정](./modules/delivery-activation/ajo-b2c/ajob2c-4/journeyoptimizer.md)

이 모듈에서는 기업이 고객에게 연관성 있고 상황에 맞는 개인화된 경험을 디자인하고 제공하는 데 도움이 되는 Journey Optimizer에 대해 알아야 할 모든 사항을 알아봅니다.

[3.5 Adobe Journey Optimizer: 번역 서비스](./modules/delivery-activation/ajo-b2c/ajob2c-5/ajotranslationsvcs.md)

이 모듈에서는 Adobe Journey Optimizer 내에서 번역 서비스를 설정하고 사용하여 고객에게 메시지를 현지화하는 방법에 대해 알아봅니다.

### 5. 보고 및 통찰력

#### Adobe Customer Journey Analytics

[1.1 Customer Journey Analytics: Adobe Experience Platform 맨 위에서 Analysis Workspace을 사용하여 대시보드 빌드](./modules/reporting-insights/cja-b2c/cjab2c-1/customer-journey-analytics-build-a-dashboard.md)

이 모듈에서는 옴니채널 데이터가 포함된 대시보드를 구성하여 오프라인 통찰력을 얻을 수 있습니다.

[1.2 Customer Journey Analytics: BigQuery Source 커넥터를 사용하여 Adobe Experience Platform에서 Google Analytics 데이터 수집 및 분석](./modules/reporting-insights/cja-b2c/cjab2c-2/customer-journey-analytics-bigquery-gcp.md)

이 모듈에서는 고유한 Google Cloud Platform 인스턴스를 설정하고 Google Cloud Platform에서 데모 데이터를 로드한 다음 BigQuery Source 커넥터를 사용하여 해당 데이터를 Google Cloud Platform에서 Adobe Experience Platform으로 수집합니다.

#### Data Distiller

[2.1 쿼리 서비스](./modules/reporting-insights/datadistiller/dd-1/query-service.md)

이 모듈에서는 Adobe Experience Platform 쿼리 서비스를 사용하는 방법을 알아봅니다.

![기술 내부자](./assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>질문이 있는 경우 향후 콘텐츠에 대한 제안 사항에 대한 일반적인 피드백을 공유하려면 기술 인사이더에게 **techinsiders@adobe.com**&#x200B;로 전자 메일을 보내 직접 문의하십시오.
