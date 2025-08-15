---
title: Federated Audience Composition 높은 수준의 아키텍처 및 플로우
seo-title: Federated Audience Composition high-level architecture & flow | Engage with audiences directly from your data warehouse using Federated Audience Composition
breadcrumb-title: 높은 수준의 아키텍처 및 흐름으로 통합 대상 구성
description: 높은 수준의 아키텍처 및 Federated Audience Composition의 흐름에 대한 개요입니다.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-high-level-architecture.jpg
exl-id: 4cb0b730-4206-476b-93d9-776dfbd464ff
source-git-commit: 0564f516cfba7ea09ac9da19d94f46d984e9e00a
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---


# 높은 수준의 아키텍처 및 흐름으로 통합 대상 구성

SecurFinancial의 비즈니스 시나리오를 지원하기 위한 단계를 살펴보기 전에 이 구성 가능한 CDP 접근 방식에 대한 높은 수준의 아키텍처와 흐름을 검토하겠습니다.

Adobe Experience Platform의 Federated Audience Composition 모듈은 기본 데이터를 복사하지 않고 Data Warehouse 데이터 세트에 대한 액세스를 확장하여 데이터 이동 및 복제를 최소화합니다.

또한 웨어하우스에서 필요한 데이터 관리 작업을 이미 완료하고 Adobe Experience Platform이 참여 엔진이 되는 제로 복사 패턴을 사용하려는 조직에게 필요한 구성 가능한 아키텍처를 제공합니다.

따라서 기업은 하나 이상의 데이터 웨어하우스에 저장된 정보를 신속하게 처리할 수 있습니다. Adobe 환경으로 데이터를 수집할 필요가 없습니다. 또한 엔터프라이즈 데이터 웨어하우스에 있지만 지금까지 고객 경험 워크플로우에서 액세스할 수 없었던 새로운 데이터 세트에 대한 액세스를 제공합니다. 고객 참여를 위해 집계된 대상 수준에서 유용하게 사용할 수 있는 과거 거래 또는 개인 데이터가 이러한 예에 포함될 수 있습니다.

![fac-architecture](assets/fac-architecture.png)

이제 [Data Warehouse 연결](data-warehouse-connection.md)을 만드는 단계로 넘어갑니다.
