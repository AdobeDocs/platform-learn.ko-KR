---
title: 페더레이션 데이터를 사용하여 Experience Platform 대상 강화
seo-title: Enrich Experience Platform audiences with federated data | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: 페더레이션 데이터를 사용하여 Experience Platform 대상 강화
description: 이 단원에서는 페더레이션 데이터를 사용하여 Experience Platform 대상을 보강합니다.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-enrich-audience-with-federated-data.jpg
hide: true
source-git-commit: a5ae2695763bc3d6dce786861dcbc15f3422c035
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 5%

---


# 페더레이션된 대상자 컴포지션

Federated Audience Composition을 사용하면 Enterprise Data Warehouse에서 페더레이션된 구성된 대상 데이터를 활용하여 Adobe Experience Platform(AEP)의 기존 대상을 강화할 수 있습니다. 이 데이터는 Adobe Experience Platform 고객 프로필에 유지되지 않습니다.

## 페더레이션 대상 컴포지션을 보강하는 방법

페더레이션 대상 구성을 보강하는 두 가지 기본 방법이 있습니다.

### &#x200B;1. 연합된 컴포지션에서 AEP 대상 읽기

이 첫 번째 예에서는 AEP의 프로필 서비스에 저장된 **SecurFinancial Loan 응용 프로그램 페이지 방문자** 대상을 사용하여 통합 구성을 시작합니다. Snowflake의 페더레이션 데이터를 사용하여 대상자를 보강하여 신용 점수 및 대출 활동에 따라 사전 승인을 결정합니다.

![federated-composition-example](assets/snowflake-preapproval.png)

1. **AEP 대상을 Federated 대상 구성 대상에 매핑**&#x200B;합니다.
2. 매핑된 대상을 읽기 대상으로 하여 **컴포지션을 빌드**&#x200B;합니다.
3. 페더레이션 데이터에 참여하려면 읽기 대상의 **ID를 조정**&#x200B;하십시오.

![federated-method-1-1](assets/federated-method-1-1.png)

![federated-method-1-2](assets/federated-method-1-2.png)

### &#x200B;2. 연결된 대상을 사용하여 Experience Platform 대상 규칙 강화

두 번째 예에서는 신용 점수 및 대출 활동으로 쿼리된 연합 대상 을 사용하여 대출 애플리케이션 웹 페이지 방문자의 행동 대상을 보강합니다.

Edge에서 이 대상자를 평가하면 사전 승인된 대출 신청서 페이지 방문자를 사이트에서 개인화된 오퍼로 즉시 재타겟팅할 수 있습니다.

![edge-audience-enrich](assets/edge-audience-enrich.png)

1. 페더레이션 대상 구성을 **저장하고 시작**&#x200B;합니다. 컴포지션이 실행되면 연결된 대상이 대상 포털에 표시됩니다.
2. 프로필 서비스의 프로필 특성 및 경험 이벤트를 사용하여 **대상 규칙을 구축**&#x200B;하고 페더레이션 대상을 통합합니다.

이 작업은 [학습 요약 및 최종 준비](conclusion.md)로 마무리하겠습니다!
