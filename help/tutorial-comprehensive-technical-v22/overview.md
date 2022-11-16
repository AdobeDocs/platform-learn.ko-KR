---
title: 개요
description: 데이터 엔지니어, 데이터 분석가, 데이터 설계자, 데이터 과학자, 오케스트레이션 엔지니어 및 마케터가 Adobe Experience Platform과 모든 애플리케이션 서비스의 비즈니스 가치를 완벽하게 이해할 수 있도록 지원합니다.
doc-type: multipage-overview
hide: false
exl-id: 88c19383-c185-40f0-b118-6cb82db0ce0e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1869'
ht-degree: 2%

---

# Adobe Experience Platform을 위한 포괄적인 기술 튜토리얼

## 개요

이 자습서는 데이터 엔지니어, 데이터 분석가, 데이터 설계자, 데이터 과학자, 오케스트레이션 엔지니어 및 마케터가 Adobe Experience Platform과 모든 애플리케이션 서비스의 비즈니스 가치를 완벽하게 이해할 수 있는 완벽한 시작점입니다. 각 단원은 오늘날의 복잡한 개인화 생태계에서 기업이 직면하고 있는 실제 문제에 초점을 맞추고 다양한 실습 위주의 연습에서 Experience Platform이 이러한 문제를 해결하는 방법을 설명합니다. 이 비디오를 보고 Adobe Experience Platform에서 해결에 도움이 되는 문제를 이해하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/344237?quality=12&enable=on)

이 자습서는 매우 다양하며 다음 애플리케이션에서 명확한 통찰력을 제공합니다.

- Adobe Experience Platform
- Adobe Experience Platform 데이터 수집
- 실시간 CDP
- Adobe Journey Optimizer
- Customer Journey Analytics
- Offer Decisioning

이 자습서는 Adobe 애플리케이션에만 초점을 두지 않고 브랜드가 작동하는 광범위한 에코시스템을 고려합니다. 그것을 하기 위해서, 어떤 교훈에서는 어떻게 해야 하는지에 초점이 있습니다 _비Adobe_ 애플리케이션은 Adobe Experience Platform과 통합됩니다. 따라서 다음 애플리케이션이 Adobe Experience Platform과 함께 작동하는 방식을 깊이 이해할 수 있습니다.

- Amazon: AWS Lambda, AWS S3, AWS Kinesis
- Google: Google Cloud Platform, Google BigQuery, Google Display&amp;Video 360, Google AdWords
- Microsoft: Power BI, Azure EventHub, Azure Blob 저장소
- Salesforce: 타블로
- Apache Kafka
- Postman
- ...

이 자습서를 완료하면 다음 작업을 수행할 수 있습니다.

- 스키마, Mixin, 데이터 세트 및 ID 구성
- Adobe Experience Platform 데이터 수집에서 Adobe Experience Platform 데이터 수집 속성을 구성하고 새 웹 SDK 확장을 설정합니다
- Adobe Experience Platform 데이터 수집, Google 태그 관리자 또는 Amazon Alexa을 사용하여 데이터를 실시간으로 Adobe Experience Platform으로 스트리밍
- 워크플로우를 사용하거나 추출, 변환, 로드(ETL) 애플리케이션을 사용하여 데이터를 Adobe Experience Platform에 일괄적으로 수집
- Adobe Experience Platform에서 실시간 고객 프로필 시각화 및 사용
- 세그먼트 만들기
- 여러 Adobe Experience Platform API 사용
- SQL을 사용하여 Adobe Experience Platform에서 데이터를 쿼리합니다.
- Adobe Experience Platform에서 기계 학습 모델 구성, 교육 및 점수 책정
- Journey Orchestration을 사용하여 실시간 트리거 기반 여정 구성
- 실시간 CDP를 사용하여 세그먼트를 다양한 대상으로 활성화하여 조치를 취할 수 있습니다
- Customer Journey Analytics을 사용하여 Google BigQuery를 비롯한 다양한 소스의 옴니채널 고객 데이터에 대해 보고합니다

## 사전 요구 사항

- Adobe Experience Platform에 액세스: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Adobe Experience Platform 데이터 수집에 대한 액세스: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- 데모 시스템에 액세스: [https://dashboard.adobedemo.com/](https://dashboard.adobedemo.com/)

>[!IMPORTANT]
>
>이 자습서는 특정 워크숍 형식을 용이하게 하기 위해 만들어졌습니다. 액세스 권한이 없을 수 있는 특정 시스템 및 계정을 사용합니다. 액세스 권한이 없더라도 이 매우 자세한 내용을 통해 많은 것을 배울 수 있을 것입니다. 워크샵 중 하나에 참여하고 액세스 자격 증명이 필요한 경우 Adobe 담당자에게 연락하여 필요한 정보를 제공합니다.

## 이 자습서 정보

이 단원들에서는 여러 산업을 지원하는 데모 웹 사이트를 사용하여 Adobe Experience Platform 및 애플리케이션 서비스를 구현합니다. 데모 웹 사이트 및 모바일 앱에는 사실적인 구현을 만들 수 있는 풍부한 데이터 레이어와 기능이 있습니다. 다음과 같은 데모 브랜드에 액세스할 수 있습니다. **루마**, **시티신호**, **EXP 뉴스**, **MUTUAL365**, **카벨로** 그리고 다른 몇 가지. 고유한 Experience Cloud 조직에서 고유한 Adobe Experience Platform 데이터 수집 클라이언트 속성을 빌드하여 데모 웹 사이트에 매핑합니다. 그러면 자체 Adobe Experience Platform 인스턴스로 전송되는 데이터가 생성됩니다.

## 아키텍처

실습 위주의 연습에서 시작하기 전에 이 자습서의 뒷부분에 있는 아키텍처를 살펴보십시오. 위의 개요에서 볼 수 있듯이 이 자습서에서는 Adobe Experience Platform의 다양한 기능과 성능에 대해 자세히 설명하지만 다양한 소스 및 대상 간의 여러 통합에 대해서도 설명합니다. 이 자습서의 아키텍처와 Adobe Experience Platform의 전체 위치를 엔터프라이즈 에코시스템에 제대로 이해하려면 아키텍처 비디오 및 다이어그램을 검토하십시오.

이동 [아키텍처](./architecture.md).


## 비디오

![비디오](./assets/images/yt.jpeg)

당신은 우리의 기술 아카데미 행사, 부트캠프 등에서 많은 흥미로운 비디오를 찾을 수 있습니다 [Experience Makers 커뮤니티 YouTube 채널](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw).

Adobe Experience Platform과 Adobe이 아닌 애플리케이션 간의 지원 및 강력한 통합 요소를 보여주는 여러 비디오가 생성되었습니다. 아래 링크를 클릭하여 해당 비디오에 대한 개요를 확인합니다.

이동 [비디오](./videos.md).



## Adobe Experience Platform에 대한 포괄적인 기술 자습서 작성 기능은 어떻게 측정됩니까?

이 자습서에 Adobe 파트너 또는 Adobe 직원으로 참여하는 경우 모든 지원 모듈을 완료한 후 진행 상황을 제출해야 합니다.

여기에서 완료 실행을 위한 요구 사항 및 프로세스를 찾을 수 있습니다. [측정 완료](./completion.md)

## 콘텐츠

[0. 시작하기](./modules/module0/getting-started.md)

- **대상:** Adobe Experience Platform을 위한 포괄적인 기술 자습서의 모든 참가자
- **전제 조건:** 다음 데모 시스템 액세스, Adobe Experience Platform 및 Adobe Experience Platform 데이터 수집 Adobe Experience Platform 환경의 기본 구성 ID에 액세스합니다.
- **설명:** 이 기본 모듈에서는 데모 환경에 액세스하고 사용할 수 있도록 모든 것을 설정합니다.
- **시간 투자:** 30분

[1. 기초 - Adobe Experience Platform 데이터 수집 및 웹 SDK 설정](./modules/module1/data-ingestion-launch-web-sdk.md)

- **대상:** 데이터 엔지니어, 데이터 설계자
- **전제 조건:** Adobe Experience Platform 및 Adobe Experience Platform 데이터 수집에 대한 액세스.
- **설명:** 이 기본 모듈에서는 Adobe Experience Platform 데이터 수집 및 새 웹 SDK 확장에 대해 알아봅니다.
- **시간 투자:** 30분

[2. 기초 - 데이터 수집](./modules/module2/data-ingestion.md)

- **대상:** 데이터 엔지니어, 데이터 설계자
- **전제 조건:** Adobe Experience Platform 및 Adobe Experience Platform 데이터 수집에 대한 액세스.
- **설명:** 이 기본 모듈에서는 웹 사이트의 데이터를 플랫폼으로 수집합니다
- **시간 투자:** 120분

[3. 기초 - 실시간 고객 프로필](./modules/module3/real-time-customer-profile.md)

- **대상:** 데이터 엔지니어, 데이터 설계자, 마케터
- **전제 조건:** Adobe Experience Platform 및 Postman 액세스
- **설명:** 이 기본 모듈에서는 UI 및 API를 사용하여 Adobe Experience Platform의 실시간 고객 프로필을 탐색합니다.
- **시간 투자:** 90분
- **다음 자산 다운로드**:
   - [Postman 컬렉션](./assets/postman/postman_profile.zip)

[4. 쿼리 서비스](./modules/module4/query-service.md)

- **대상:** 데이터 엔지니어, Data Architect, Data Analyst, BI Expert
- **전제 조건:** Adobe Experience Platform, 쿼리 서비스, Power BI 또는 타블로에 대한 액세스
- **설명:** 이 단원에서는 Adobe Experience Platform Query Service 사용 방법을 배웁니다.
- **시간 투자:** 90분
- **다음 자산 다운로드**:
   - [JSON - 샘플 데이터: 데모 시스템 - 웹 사이트용 이벤트 데이터 세트](./assets/json/ee.json)
   - [JSON - 샘플 데이터: 데모 시스템 - 콜 센터용 이벤트 데이터 세트](./assets/json/callcenter.json)
   - [JSON - 샘플 데이터: 데모 시스템 - 충성도 프로필 데이터 세트](./assets/json/loyalty.json)

[5. Intelligent Services](./modules/module5/intelligent-services.md)

- **대상:** 데이터 엔지니어, 데이터 설계자, 데이터 과학자
- **전제 조건:** Adobe Experience Platform, Intelligent Services 액세스
- **설명:** 이 단원에서는 Adobe Experience Platform Intelligent Services를 설정, 구성 및 사용하는 방법을 배웁니다.
- **시간 투자:** 60분

[6. Real-Time CDP - 세그먼트 작성 및 작업 수행](./modules/module6/real-time-cdp-build-a-segment-take-action.md)

- **대상:** Data Architect, Orchestration 엔지니어, 마케터
- **전제 조건:** Adobe Experience Platform, 실시간 CDP, Adobe Audience Manager, Adobe Target, AWS S3에 대한 액세스
- **설명:** 이 모듈에서는 세그먼트를 구성하고, 스트리밍 세그먼테이션에 사용하도록 설정하고, Google DV360, Google AdWords, Adobe Audience Manager, Adobe Target 및 Salesforce Marketing Cloud과 같은 S3 대상을 포함한 여러 대상으로 세그먼트를 활성화합니다.
- **시간 투자:** 90분

[7. Adobe Journey Optimizer: 오케스트레이션](./modules/module7/journey-orchestration-create-account.md)

- **대상:** 데이터 엔지니어, 데이터 설계자, 오케스트레이션 엔지니어
- **전제 조건:** Adobe Experience Platform 및 Adobe Journey Optimizer 액세스
- **설명:** 이 모듈에서는 Adobe Journey Optimizer을 사용하여 트리거 기반 여정을 만듭니다.
- **시간 투자:** 60분

[8. Adobe Journey Optimizer: 외부 데이터 소스 및 사용자 지정 작업](./modules/module8/journey-orchestration-external-weather-api-sms.md)

- **대상:** 데이터 엔지니어, 데이터 설계자, 오케스트레이션 엔지니어, 마케터
- **전제 조건:** Adobe Experience Platform, Adobe Journey Optimizer, Open Weather API, Twilio 액세스
- **설명:** 이 모듈에서는 Adobe Journey Optimizer을 사용하여 온라인과 오프라인을 막론하고 고객 행동을 경청하고 다양한 채널을 통해 지능적이고 상황에 맞는 실시간으로 응답할 수 있습니다.
- **시간 투자:** 90분

[9. Adobe Journey Optimizer: offer decisioning](./modules/module9/offer-decisioning.md)

- **대상:** 데이터 엔지니어, 데이터 설계자, 오케스트레이션 엔지니어, 마케터
- **전제 조건:** Adobe Experience Platform 및 Offer decisioning 액세스
- **설명:** 이 단원에서는 Adobe Experience Platform - Offers/Decisioning 애플리케이션 서비스를 양방향 사용하여 개인화된 오퍼와 고유한 오퍼 활동을 구성합니다.
- **시간 투자:** 120분

[10. Adobe Journey Optimizer: 이벤트 기반 여정](./modules/module10/journeyoptimizer.md)

- **대상:** 이메일 마케터, 오케스트레이션 전문가, 데이터 엔지니어, 데이터 설계자, 데이터 분석가
- **전제 조건:** Adobe Experience Platform 및 Journey Optimizer 액세스
- **설명:** 이 모듈에서는 회사가 고객에게 연결되고 상황에 맞는 개인화된 경험을 디자인하고 제공하는 데 도움이 되는 Journey Optimizer에 대해 알고 있는 모든 것을 알아봅니다.
- **시간 투자:** 120분

[11. Customer Journey Analytics: Adobe Experience Platform 맨 위에서 Analysis Workspace을 사용하여 대시보드 만들기](./modules/module11/customer-journey-analytics-build-a-dashboard.md)

- **대상:** 데이터 엔지니어, 데이터 설계자, 데이터 분석가
- **전제 조건:** Adobe Experience Platform 및 Customer Journey Analytics 액세스
- **설명:** 이 모듈에서는 웹 사이트 상호 작용, 모바일 앱 상호 작용, 콜 센터 상호 작용, 매장 내 상호 작용 등과 같은 옴니채널 데이터가 포함된 대시보드를 구성하여 온라인으로 오프라인 인사이트를 얻을 수 있습니다.
- **시간 투자:** 120분

[12. Customer Journey Analytics BigQuery Source Connector를 사용하여 Adobe Experience Platform에서 Google Analytics 데이터 수집 및 분석](./modules/module12/customer-journey-analytics-bigquery-gcp.md)

- **대상:** 데이터 엔지니어, 데이터 설계자, 데이터 분석가
- **전제 조건:** Adobe Experience Platform, Customer Journey Analytics, Google Cloud Platform, Google BigQuery에 대한 액세스
- **설명:** 이 모듈에서는 고유한 Google 클라우드 플랫폼 인스턴스를 설정하고, Google Cloud Platform에 데모 데이터를 로드한 다음 BigQuery Source Connector를 사용하여 Google Cloud Platform의 해당 데이터를 Adobe Experience Platform으로 수집합니다. 마지막으로 Customer Journey Analytics을 사용하여 데이터를 시각화합니다.
- **시간 투자:** 120분
- **다음 자산 다운로드**:
   - [JSON - 샘플 데이터: 데모 - 충성도 데이터](./assets/json/bqLoyalty.json)

[13. Real-Time CDP: Microsoft Azure 이벤트 허브에 세그먼트 활성화](./modules/module13/segment-activation-microsoft-azure-eventhub.md)

- **대상:** 데이터 엔지니어, 데이터 설계자, 데이터 분석가
- **전제 조건:** Adobe Experience Platform, 실시간 CDP 및 Microsoft Azure에 액세스
- **설명:** 이 단원에서는 Adobe Experience Platform 실시간 CDP를 위한 실시간 대상으로 Microsoft Azure EventHub 대상을 설정합니다. 또한 Adobe Experience Platform에서 Azure EventHub 대상으로 세그먼트 페이로드를 전달할 때마다 실시간으로 트리거되는 Azure 함수를 설정 및 배포합니다. 트리거할 Azure 함수는 Adobe Experience Platform 실시간 CDP의 활성화 기능 메커니즘을 보여줍니다.
또한 이 모듈의 일부로, 특정 대상에 페이로드를 실제로 제공하기 위해 실시간 CDP를 트리거하는 항목을 알아봅니다. 또한 세그먼트 자격의 상태 및 활성화 방법에 대해서도 설명합니다.
- **시간 투자:** 90분

[14. Real-Time CDP 연결: 이벤트 전달](./modules/module14/aep-data-collection-ssf.md)

- **대상:** 데이터 엔지니어, 데이터 설계자, 데이터 분석가
- **전제 조건:** Real-Time CDP 연결, 태그 및 이벤트 전달 속성에 대한 액세스
- **설명:** 이 모듈에서는 이전에 구성한 데이터 세트, 스키마 및 Adobe Experience Platform 데이터 수집 속성을 사용하여 데이터를 수집한 다음 해당 데이터 서버측을 선택한 종단점으로 전달합니다.
- **시간 투자:** 90분

[15. Apache Kafka에서 Real-Time CDP으로 스트림 데이터](./modules/module15/aep-apache-kafka.md)

- **대상:** Data Analyst, 데이터 엔지니어, Data Architect
- **전제 조건:** Adobe Experience Platform 액세스
- **설명:** 이 모듈에서는 Kafka Connect용 Adobe Experience Platform 싱크 커넥터를 사용하여 Apache Kafka 클러스터를 설정하고, 주제, 생산자 및 소비자를 정의하고, 데이터를 Adobe Experience Platform으로 스트리밍하는 방법을 알아봅니다.
- **시간 투자:** 90분

>[!NOTE]
>
>Adobe Experience Platform에 대해 알아야 할 모든 것을 배우는 데 시간을 투자해주셔서 감사합니다. 질문이 있는 경우 향후 컨텐츠에 대한 제안 사항이 있는 일반적인 피드백을 공유하려는 경우 Outlook Van Geluwe에게 이메일을 직접 보내주십시오 **vangeluw@adobe.com**.
