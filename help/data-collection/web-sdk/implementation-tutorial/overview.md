---
title: 개요
description: 개요
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 8ffa258b-6ff7-4413-aead-21b106668c65
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---

# 개요

사용자의 브라우저에서 발생하는 이벤트에 대한 데이터 수집은 마케팅 전략의 기본 팁입니다. Adobe은 이 데이터를 관리하는 데 도움이 되는 몇 가지 도구를 제공했습니다. 이 자습서에서는 이러한 각 도구를 개별적으로 익숙하게 할 수 있지만, 이러한 각 도구가 수행하는 작업과 이러한 도구를 함께 사용하여 공통 목표를 달성하는 방법에 대한 광범위한 보기를 제공하려고 합니다.

이 자습서에서는 (1) Adobe Experience Platform 내에서 데이터를 구조화하고 유지하는 전략, (2) 브라우저에서 데이터를 관리하고 특정 이벤트가 발생했음을 알리는 전략, (3) 관련 데이터를 Adobe Experience Platform에 보내 이러한 이벤트에 대응하는 전략에 대해 설명합니다.

이 자습서에서는 Adobe 클라이언트 데이터 레이어, Adobe Experience Platform Web SDK 및 태그 기능을 사용하여 보다 처방적이고 매끄러운 구현을 제공하지만 이러한 도구를 타사 또는 사내 도구와 혼합하여 사용할 수도 있으므로 유연성을 극대화할 수 있습니다.

## 예시 상황

이 자습서에서는 전자 상거래 사이트의 간단한 제품 페이지에 대한 데이터 수집을 구현하고 있다고 가정합니다. 제품 페이지가 브라우저에 로드됩니다. 여기에서 사용자가 제품을 보았는지 추적합니다. 사용자는 제품을 구매하기로 결정하므로 버튼을 클릭하여 제품을 장바구니에 추가합니다. 여기서는 사용자가 Adobe Experience Platform에 경험 이벤트를 전송하여 새 장바구니를 열고 제품을 장바구니에 추가했음을 추적합니다. 마지막으로 사용자가 _앱 다운로드_ 모바일 앱에 관심이 있기 때문에 연결합니다. 사용자가 링크를 클릭했는지 추적합니다.
