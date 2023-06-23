---
title: Adobe 클라이언트 데이터 레이어 사용 방법
description: Adobe 클라이언트 데이터 레이어 사용 방법
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 33a5db8c-e49b-4073-b4d7-4abe19537fcb
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---

# Adobe 클라이언트 데이터 레이어 사용 방법

위치 [데이터 레이어란 무엇입니까?](whats-a-data-layer.md)에서는 데이터 레이어에 대해 논의할 때 고려해야 할 두 가지 부분, 즉 컨테이너와 컨텐츠가 있다는 것을 배웠습니다. Adobe 클라이언트 데이터 레이어 는 컨테이너입니다. 네가 어떻게 되든 상관 없어 [데이터 구조](../structuring-your-data.md) 또는 데이터에 어떤 정보를 입력할지 선택할 수 있습니다. 데이터는 다음과 같이 구조화할 수 있습니다. [XDM](../structuring-your-data.md#xdm)아래 예제에 나와 있는 대로 또는 완전히 고유한 구조를 만들 수 있습니다.

이상적으로 회사의 엔지니어링 팀은 페이지 내 코드를 통해 필요한 데이터를 데이터 레이어로 푸시할 책임이 있습니다. 그런 다음 마케팅 팀은 데이터 레이어에서 데이터를 검색합니다(가급적 Adobe Experience Platform 태그 사용).

## 데이터 레이어로 데이터 푸시

Adobe 클라이언트 데이터 레이어는 JavaScript 배열입니다. Adobe 클라이언트 데이터 레이어를 만들면 비어 있는 상태로 시작됩니다.

```js
window.adobeDataLayer = window.adobeDataLayer || [];
```

데이터 레이어에 데이터를 배치하려면 `push` 데이터 레이어 배열의 메서드:

```js
window.adobeDataLayer.push({
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile"
  }
});
```

를 호출하여 언제든지 추가 데이터를 데이터 레이어에 푸시할 수 있습니다. `push` 다시.

```js
window.adobeDataLayer.push({
  "claims": {
    "status": "approved",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
});
```

## 푸시된 데이터 파악

이전 두 가지를 구현한 경우 `push` 를 호출하면 데이터 레이어 배열에 두 개의 항목이 표시됩니다. 이 상태에서는 데이터 레이어가 특별히 유용하지 않습니다. 일반적으로 데이터 레이어의 병합 상태, 즉 데이터 레이어로 푸시한 모든 데이터의 결합 결과인 단일 개체에 액세스하려고 합니다. 이 병합된 상태에 액세스하는 방법은 이 자습서의 뒷부분에서 알아봅니다. 지금은 데이터 레이어의 계산된 상태가 두 번째 이후의 것임을 이해하는 것으로 충분합니다 `push` 호출은 다음과 같습니다.

```json
{
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile",
    "status": "approved",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
}
```

## 데이터 제거 중

경우에 따라 데이터 레이어에서 데이터 일부를 제거해야 합니다. 이는 사용자가 한 보기에서 다음 보기로 이동할 때 특히 단일 페이지 애플리케이션에서 일반적입니다. 예를 들어 사용자가 제품 보기에서 연락처 보기로 이동하는 경우 데이터 레이어는 활성 보기와 더 이상 관련이 없으므로 데이터 레이어에서 제품 데이터를 지우는 것이 적절할 수 있습니다.

값을 푸시하여 데이터 일부를 제거할 수 있습니다. `undefined` 을(를) 클릭하여 제거할 키를 지정합니다. 을(를) 제거하려면 이전 예제를 기반으로 합니다. `status` 데이터 레이어에서 코드는 다음과 같습니다.

```js
window.adobeDataLayer.push({
  "claims": {
    "status": undefined
  }
});
```

데이터 레이어의 계산된 상태에 더 이상 포함되지 않음 `status`:

```json
{
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
}
```

## 이벤트를 데이터 레이어로 푸시

Adobe 클라이언트 데이터 레이어는 데이터를 저장할 뿐만 아니라 페이지에서 발생하는 이벤트를 통신하는 데에도 사용됩니다. 실제로 일반적으로 데이터를 데이터 레이어에 푸시합니다 _결과적으로_ 페이지에서 발생하는 이벤트. 이러한 이벤트에는 (1) 채팅 봇 열기 또는 검색어에 검색어 입력 등의 상호 작용 이벤트 또는 (2) 광고 노출 또는 웹 페이지 성능 계산 완료와 같은 비상호 작용 이벤트가 포함됩니다.

페이지에서 이벤트가 발생했음을 알려면 다음을 포함합니다. `event` 데이터 레이어로 푸시하는 개체의 키입니다. 예를 들어, 사용자가 검색 필드에 검색 쿼리를 입력했음을 알려 줄 수 있습니다.

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered"
});
```

나중에 특정 이벤트가 데이터 레이어에 푸시될 때 Adobe Experience Platform 태그 내에서 규칙을 트리거하는 방법을 알아봅니다. 또한 `event` 키: _아님_ 계산된 상태에 포함됩니다. 데이터 계층에 의해 특별한 처리가 처리됩니다.

## 이벤트 및 데이터를 데이터 레이어로 푸시

리스너에 사용자가 검색 쿼리를 입력했음을 알리는 것이 도움이 되지만, 이벤트에 대한 추가 정보를 제공하려면 어떻게 해야 합니까? 예를 들어 사용자의 검색 쿼리를 포함할 수 있습니다. 다음 두 가지 방법 중 하나로 이 데이터를 제공할 수 있습니다.

1. 다음과 같이 데이터 제공 **유지됨** 데이터 계층의 계산된 상태 일부로서 데이터 계층에서 입니다.
2. 다음과 같이 데이터 제공 **유지되지 않음** 데이터 계층의 계산된 상태 일부로서 데이터 계층에서 입니다.

일반적으로 데이터 레이어에서 데이터를 유지할지 여부는 페이지에 있는 사용자의 기간 동안 해당 데이터를 참조할지 여부에 따라 달라집니다. 그렇지 않은 경우 데이터 레이어 내부에 데이터를 유지하면 데이터 레이어가 복잡해질 수 있습니다.

다음은 추가 데이터가 있는 이벤트를 푸시하는 예입니다. **유지됨** 데이터 레이어에서:

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered",
  "siteKnowledge": {
    "supportSiteSearch": {
      "term": "roller",
      "locationInPage": "topSearchBar"
    }
  }
});
```

이후 `push` 일어나면, `siteKnowledge` 은 페이지가 언로드될 때까지(의도적으로 제거하거나 재정의하지 않는 한) 항상 데이터 레이어의 계산된 상태에 표시됩니다 `siteKnowledge`).

이와 달리, 다음은 추가 데이터가 있는 이벤트를 푸시하는 예입니다. **유지되지 않음** 데이터 레이어에서:

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered",
  "eventInfo": {
    "siteKnowledge": {
      "supportSiteSearch": {
        "term": "roller",
        "locationInPage": "topSearchBar"
      }
    }
  }
});
```

이 예제에서 주목해야 할 사항은 다음과 같습니다. `siteKnowledge` 안에 래핑 `eventInfo`. 다음 `eventInfo` key는 데이터 계층에 의해 특별한 대우를 받습니다. 이 데이터는 데이터 레이어에 표시됩니다 _다음과 같아야 함_ 수신자에게 전송되는 이벤트에 포함되지만, _하지 말아야 함_ 는 데이터 레이어 내부에 유지됩니다. 리스너(예: Adobe Experience Platform 태그)에게 이벤트가 통지되면 이 데이터는 기본적으로 잊혀집니다. 다음 `siteKnowledge` 키가 데이터 레이어의 계산된 상태 내에 표시되지 않습니다.

호출할 때마다 `push`: Adobe 클라이언트 데이터 레이어는 모든 리스너에 알립니다. 나중에 Adobe Experience Platform 태그에서 이러한 알림을 수신하고 그에 따라 규칙을 트리거하는 방법을 알아봅니다.
