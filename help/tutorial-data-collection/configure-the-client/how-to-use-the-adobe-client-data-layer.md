---
title: Adobe 클라이언트 데이터 레이어를 사용하는 방법
description: Adobe 클라이언트 데이터 레이어를 사용하는 방법
exl-id: b5af9e72-aa6c-4cd7-80dd-b2de762a7523
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 0%

---

# Adobe 클라이언트 데이터 레이어를 사용하는 방법

in [데이터 계층이란 무엇입니까?](whats-a-data-layer.md)에서는 데이터 계층에 대해 논의할 때 고려해야 할 두 가지 사항이 있습니다. 컨테이너 및 컨텐츠. 다음 [Adobe 클라이언트 데이터 레이어](https://github.com/adobe/adobe-client-data-layer) 는 컨테이너입니다. 네가 어떻게 하든 상관없다 [데이터 구조](../structuring-your-data.md) 또는 데이터에 어떤 정보를 입력할지 선택합니다. 데이터는 다음과 같이 구조화할 수 있습니다. [XDM](../structuring-your-data.md#xdm)아래의 예와 같이 또는 고유한 구조를 완전히 구축할 수 있습니다.

가장 좋은 방법은 회사의 엔지니어링 팀이 페이지 내 코드를 통해 데이터 레이어에 필요한 데이터를 푸시할 수 있다는 것입니다. 그런 다음 마케팅 팀은 데이터 계층에서 데이터를 검색합니다. 바람직하게는 이전에 Launch라고 했던 Adobe Experience Platform의 태그 기능을 사용합니다.

## 데이터 레이어에 데이터 푸싱

Adobe 클라이언트 데이터 계층은 JavaScript 배열입니다. 클라이언트 데이터 Adobe 레이어를 만들면 빈 상태로 시작됩니다.

```js
window.adobeDataLayer = window.adobeDataLayer || [];
```

데이터를 데이터 계층에 배치하려면 `push` 데이터 레이어 배열의 메서드:

```js
window.adobeDataLayer.push({
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile"
  }
});
```

를 호출하여 언제든지 데이터 레이어에 추가 데이터를 푸시할 수 있습니다 `push` 다시 한 번

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

이전 두 개를 구현한 경우 `push` 를 호출하면 데이터 레이어 배열에 두 개의 항목이 표시됩니다. 데이터 계층은 이 상태에서 유용하지 않습니다. 일반적으로 데이터 레이어의 병합된 상태에 액세스하거나, 다시 말해 데이터 레이어에 푸시한 모든 데이터의 결합 결과인 단일 개체를 액세스하려고 합니다. 나중에 자습서에서 병합된 이 상태에 액세스하는 방법을 알아봅니다. 현재 두 데이터 계층 다음의 계산된 상태를 이해하는 것으로 충분합니다 `push` 호출은 다음과 같습니다.

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

## 데이터 제거

경우에 따라 데이터 레이어에서 데이터 조각을 제거해야 합니다. 사용자가 한 보기에서 다음 보기로 이동할 때 단일 페이지 애플리케이션에서 일반적으로 사용됩니다. 예를 들어 사용자가 제품 보기에서 연락처 보기로 이동하는 경우 활성 뷰와 더 이상 관련이 없으므로 데이터 계층에서 제품 데이터를 지우는 것이 적절할 수 있습니다.

값을 눌러 데이터 조각을 제거할 수 있습니다 `undefined` 을 클릭합니다. 제거하려면 이전 예제에 빌드합니다. `status` 데이터 계층에서 코드는 다음과 같습니다.

```js
window.adobeDataLayer.push({
  "claims": {
    "status": undefined
  }
});
```

데이터 계층의 계산된 상태는 더 이상 포함되지 않습니다 `status`:

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

## 이벤트를 데이터 계층에 푸시하기

Adobe 클라이언트 데이터 계층은 데이터를 저장할 뿐만 아니라 페이지에서 발생하는 이벤트를 전달하는 데에도 사용됩니다. 실제로 일반적으로 데이터를 데이터 레이어에 푸시합니다 _결과로_ 이벤트에서 다른 이벤트를 발생시키지 않습니다. 이러한 이벤트에는 채팅 보트 열기 또는 검색 창에 검색어 입력 또는 (2) 광고 노출 또는 웹 페이지 성능 계산 완료와 같은 비상호 작용 이벤트 등의 (1) 상호 작용 이벤트가 포함됩니다.

페이지에서 이벤트가 발생했음을 알려면 다음을 포함합니다 `event` 키를 누릅니다. 예를 들어 사용자가 검색 쿼리를 검색 필드에 입력했음을 알릴 수 있습니다.

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered"
});
```

<!--Later, you'll learn how to trigger rules within Adobe Experience Platform Tags when a particular event is pushed to the data layer.--> Also note that the `event` key is not included in the computed state. It receives special treatment by the data layer.


## 이벤트 및 데이터를 데이터 레이어에 푸싱

사용자가 검색 쿼리를 입력했음을 수신자에게 알리는 것이 유용하지만, 이벤트에 대한 추가 정보를 제공하려면 어떻게 해야 합니까? 예를 들어 사용자의 검색 쿼리를 포함하려는 경우 다음 두 가지 방법 중 하나로 이 데이터를 제공할 수 있습니다.

1. 데이터를 제공하도록 제공 **보존됨** 데이터 레이어의 계산된 상태의 일부로 데이터 레이어에서 사용할 수 있습니다.
1. 데이터를 제공하도록 제공 **보존되지 않음** 데이터 레이어의 계산된 상태의 일부로 데이터 레이어에서 사용할 수 있습니다.

일반적으로 데이터 계층에 데이터를 유지할지 여부는 사용자가 페이지에 있는 동안 해당 데이터를 참조할 계획인지에 따라 다릅니다. 그렇지 않으면 데이터 레이어 내의 데이터를 유지하면 데이터 레이어가 복잡해집니다.

다음은 추가적인 데이터를 사용하여 이벤트를 푸시하는 예입니다 **보존됨** 데이터 레이어:

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

이후 `push` 제자리에 `siteKnowledge` 페이지가 언로드될 때까지(의도적으로 제거하거나 재정의하지 않는 경우) 항상 데이터 계층의 계산 상태에 표시됩니다 `siteKnowledge`).

이와 대조적으로, 다음은 추가적인 데이터로 이벤트를 푸시하는 예입니다 **보존되지 않음** 데이터 레이어:

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

이 예에서 `siteKnowledge` 내부에 래핑됨 `eventInfo`. 다음 `eventInfo` 키는 데이터 계층에서 특별 처리를 받습니다. 이 데이터는 데이터 계층에 이 데이터를 알려줍니다 _다음과 같이 하십시오._ 수신자에게 전송되는 이벤트에 포함되지만 _다음을 해서는 안 됩니다_ 데이터 레이어 내에서 유지됩니다. 수신자(태그 관리자 등)가 이벤트에 대한 알림을 받으면 이 데이터가 무시됩니다. 다음 `siteKnowledge` 키가 데이터 계층의 계산된 상태 내에 표시되지 않습니다.

호출할 때마다 `push`로 지정하는 경우 Adobe 클라이언트 데이터 계층은 수신자에게 모든 알림을 보냅니다. 나중에 이러한 알림을 수신하는 방법을 배웁니다 <!--from Adobe Experience Platform Tags--> 및 그에 따라 규칙을 트리거합니다.

[다음: ](implement-product-page-data-layer.md)

>[!NOTE]
>
>데이터 수집에 시간을 내어 주셔서 감사합니다. 질문이 있거나 일반 피드백을 공유하거나 향후 컨텐츠에 대한 제안 사항이 있는 경우 해당 정보를 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
