---
title: 웨어하우스 데이터로 대상자 강화
seo-title: Enrich Audiences with warehouse data | Engage with audiences directly from your data warehouse using Federated Audience Composition
breadcrumb-title: 웨어하우스 데이터로 대상자 강화
description: 이 연습에서는 Experience Platform 대상이 웨어하우스 데이터로 보강됩니다.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-enrich-audience-with-federated-data.jpg
exl-id: 3f6aa121-0dbd-4ad9-b136-d1455eed03ca
source-git-commit: 93b787112134919444150974c7149dc10c2d0ca6
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 7%

---

# 웨어하우스 데이터로 대상자 강화

Federated Audience Composition을 사용하면 Enterprise Data Warehouse에서 페더레이션된 구성된 대상 데이터를 활용하여 Adobe Experience Platform(AEP)의 기존 대상을 강화할 수 있습니다. 이 데이터는 Adobe Experience Platform 고객 프로필에 유지되지 않습니다.

## Federated Composition 내의 대상자 읽기

이 연습에서는 Experience Platform의 프로필 서비스에 저장된 **SecurFinancial Loan 응용 프로그램 페이지 방문자** 대상을 사용하여 통합 구성을 시작합니다. Snowflake의 페더레이션 데이터를 사용하여 신용 점수 및 대출 활동을 기반으로 사전 승인을 결정합니다.

![federated-composition-example](assets/snowflake-preapproval.png)

### 단계

1. **AEP 대상을 Federated 대상 구성 대상에 매핑**&#x200B;합니다.
2. 매핑된 대상을 읽기 대상으로 하여 **컴포지션을 빌드**&#x200B;합니다.
3. 페더레이션 데이터에 참여하려면 읽기 대상의 **ID를 조정**&#x200B;하십시오.

![federated-method-1-1](assets/federated-method-1-1.png)

![federated-method-1-2](assets/federated-method-1-2.png)

[현재 개인화 지원](deliver-in-the-moment-personalization.md)을 위해 페더레이션 데이터를 사용하는 다른 예를 살펴보겠습니다.
