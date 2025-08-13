---
title: Federated Audience Composition을 통해 크로스 채널 인사이트 잠금 해제
description: Federated Audience Composition은 데이터 설계자 및 데이터 엔지니어가 서드파티 데이터 웨어하우스에서 직접 대상을 구축하고 강화할 수 있는 강력한 기능입니다.
breadcrumb-title: 개요
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2025-08-11T00:00:00Z
exl-id: 9d5a2e40-6cda-4164-87db-1bfffe3438e3
source-git-commit: a3c8d8b03472d01f491bf787ed647a696d3a5524
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# 개요

Federated Audience Composition은 Adobe Real-Time Customer Data Platform(Real-Time CDP) 및 Adobe Journey Optimizer 환경에서 사용할 수 있는 강력한 기능입니다. 이를 통해 데이터 설계자와 데이터 엔지니어는 데이터를 Adobe Experience Platform에 복제하지 않고도 [지원](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"}되는 타사 데이터 웨어하우스에서 직접 대상을 구축하고 강화할 수 있습니다. 이 튜토리얼에서는 기술 사용자가 엔터프라이즈 데이터 웨어하우스를 연결하고 대상을 만들고 보강하며 개인화된 마케팅 경험을 위해 활성화할 수 있는 실습 지침을 제공합니다.

## 시각적 안내서

이 시각적 안내서는 비즈니스 시나리오의 다양한 측면을 지원하는 데 사용되는 각 활동의 단계를 보여 줍니다. 목표는 다음을 포함하여 환경에서 활용할 수 있는 활동을 제공하는 것입니다.

- Adobe Experience Platform을 엔터프라이즈 데이터 웨어하우스에 연결합니다.
- Federated Audience Composition을 사용하여 대상을 만들고 관리합니다.
- 페더레이션 대상을 Amazon S3와 같은 외부 대상에 매핑합니다.
- 페더레이션 데이터로 기존 대상을 보강합니다.
- &quot;즉각적인&quot; 개인화를 추진할 대상을 만듭니다.
- 페더레이션 대상 데이터를 사용하여 고객 여정을 작성합니다.

이 안내서는 Real-Time CDP 또는 Journey Optimizer과 함께 작업하는 데이터 설계자 및 데이터 엔지니어를 위해 설계되었습니다. Adobe Experience Platform 및 기본 데이터 웨어하우스 개념에 익숙하다고 가정합니다.

## 비즈니스 컨텍스트

SecurFinancial은 대표적인 금융 서비스 회사입니다. 다양한 소스에 걸쳐 풍부한 고객 데이터를 활용하여 다양한 세그먼트에 대한 오퍼와 캠페인을 개인화할 수 있습니다. 또한 기업은 Adobe의 애플리케이션을 사용하여 개인화된 고객 경험을 제공하는 동시에 기존 데이터 웨어하우스를 사용할 수 있는 Adobe Experience Platform의 Real-Time CDP Federated Audience Composition 기능을 사용할 계획입니다. 주요 이점은 다음과 같습니다.

- **웨어하우스 데이터에 액세스**: 데이터 복제 없이 지원되는 데이터 웨어하우스의 데이터 세트에서 고부가가치 대상을 만듭니다.
- **데이터 이동 최소화**: 웨어하우스에서 직접 데이터를 쿼리하여 중복을 줄이고 데이터 거버넌스를 유지합니다.
- **통합 경험 워크플로**: 크로스 채널 사용 사례를 위해 Adobe Experience Platform 내의 대상자를 큐레이션 및 활성화합니다.
- **향상된 개인화**: 웨어하우스 특성을 사용하여 프로필 및 대상자를 강화하여 실시간으로 트리거된 경험을 제공합니다.

## 비즈니스 시나리오

SecurFinancial은 양호한 크레딧을 기반으로 대출 자격이 주어지고 SecurFinancial 포트폴리오에 활성 대출이 없는 고객을 재타겟팅하기 위해 이메일 캠페인을 시작하려고 합니다. 온라인 행동 데이터를 실시간으로 섭취하는 동안 AEP에 신용 정보를 섭취하는 것이 제한되므로 고객 사전 자격을 식별하는 데 어려움을 겪습니다. 제한된 데이터를 이동하지 않고 자격이 있는 고객을 우대하기 위해 Federated Audience Composition을 사용하여 AEP 행동 대상을 보강합니다.

## 전제 조건

환경에서 유사한 활동을 수행하려면 다음을 수행해야 합니다.

- Real-Time CDP 또는 Journey Optimizer으로 프로비저닝된 Adobe Experience Platform 계정에 대한 액세스 권한.
- 시스템 관리자 권한 또는 권한을 구성할 수 있는 기능입니다.
- 스키마, 데이터 세트 및 대상자와 같은 Adobe Experience Platform 개념에 익숙합니다(권장: Experience League에서 [Adobe Experience Platform 재생 목록 소개](https://experienceleague.adobe.com/en/playlists/experience-platform-introduction?lang=en){target="_blank"}를 완료합니다).
- 지원되는 엔터프라이즈 데이터 웨어하우스(예: Amazon Redshift, Azure Synapse Analytics, Snowflake 또는 Google BigQuery)에 액세스합니다.
- 데이터 웨어하우스 쿼리를 위한 SQL에 대한 기본 지식.
- **샌드박스 환경**: 조직의 Real-Time CDP 인스턴스에서 샌드박스를 만들어 프로덕션 데이터에 영향을 주지 않고 안전하게 실험합니다.
- **Data Warehouse 연결**: 이 자습서에서는 Snowflake 연결을 사용하지만 [지원되는 클라우드 웨어하우스](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites)를 사용할 수 있습니다.

[Data Warehouse 연결](data-warehouse-connection.md)(으)로 시작하겠습니다.
