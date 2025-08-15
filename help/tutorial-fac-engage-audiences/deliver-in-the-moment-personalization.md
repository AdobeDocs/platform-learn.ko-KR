---
title: Edge Network을 사용하여 "즉각적인" 개인화 제공
seo-title: Deliver "in-the moment" personalization using Edge Network | Engage with audiences directly from your data warehouse using Federated Audience Composition
breadcrumb-title: Edge Network을 사용하여 "즉각적인" 개인화 제공
description: 이 연습에서는 즉각적인 "즉시" 재타겟팅을 위해 Edge에서 페더레이션 대상을 평가합니다.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-drive-in-the-moment-personalization.jpg
exl-id: 20bfafb1-1d1b-48d8-84eb-97d4c9e03b76
source-git-commit: 93b787112134919444150974c7149dc10c2d0ca6
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 0%

---

# Edge Network을 사용하여 &quot;즉각적인&quot; 개인화 제공

Federated Audience Composition을 사용하면 Enterprise Data Warehouse에서 페더레이션된 구성된 대상 데이터를 활용하여 Adobe Experience Platform(AEP)의 기존 대상을 강화할 수 있습니다. 이 데이터는 Adobe Experience Platform에서 유지되지 않지만 [이벤트 전달](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/event-forwarding/overview){target="_blank"} 기능을 사용하여 이 데이터를 데이터 웨어하우스로 바로 보낼 수 있습니다.

이 연습에서는 신용 점수 및 대출 활동으로 쿼리된 연합 대상을 사용하여 대출 애플리케이션 웹 페이지 방문자의 행동 대상을 보강합니다.

Edge에서 이 대상자를 평가하면 사전 승인된 대출 신청 페이지 방문자를 즉시 재타겟팅하여 사이트에 개인화된 오퍼를 제공합니다.

![edge-audience-enrich](assets/edge-audience-enrich.png)

## 단계

1. 페더레이션 대상 구성을 **저장하고 시작**&#x200B;합니다. 컴포지션이 실행되면 페더레이션 대상이 대상 포털에 표시됩니다.
2. 프로필 서비스의 프로필 특성 및 경험 이벤트를 사용하여 **대상 규칙을 구축**&#x200B;하고 페더레이션 대상을 통합합니다.

이 작업은 [학습 요약 및 최종 준비](conclusion.md)로 마무리하겠습니다!
