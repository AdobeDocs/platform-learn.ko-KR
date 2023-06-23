---
title: 데이터 구조화
description: 데이터 구조화
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: d300429a-5a66-4b61-97cb-b934fc8e8291
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# 데이터 구조화

기업은 자신의 도메인에 대해 소통하기 위한 고유한 언어를 가지고 있습니다. 자동차 대리점은 제조사, 모형, 실린더 등을 취급한다. 항공사는 항공편 번호, 서비스 등급, 좌석 배정 업무를 처리합니다. 이러한 용어 중 일부는 특정 회사에 고유하며 일부는 수직 산업 간에 공유되고 일부는 거의 모든 비즈니스에서 공유됩니다. 업계 카테고리 또는 더 광범위한 카테고리 간에 공유되는 용어의 경우 이러한 용어의 이름을 지정하고 공통된 방식으로 구성할 때 데이터를 사용하여 강력한 작업을 시작할 수 있습니다.

예를 들어, 많은 사업체들이 주문을 처리합니다. 만약 이 사업체들이 비슷한 방법으로 주문을 모형화하기로 결정했다면 어땠을까. 예를 들어 데이터 모델이 `priceTotal` 주문의 총 가격을 나타내는 속성입니다. 개체에 라는 속성도 있으면 어떻게 합니까? `currencyCode` 및 `purchaseOrderNumber`. 주문 개체에 이름이 인 속성이 포함되어 있을 수 있습니다. `payments` 그러면 결제 객체의 배열이 됩니다. 각 개체는 주문에 대한 결제를 나타냅니다. 예를 들어 고객이 주문의 일부를 상품권으로 결제하고 나머지는 신용카드로 결제했을 수도 있다. 다음과 같은 모델을 만들 수 있습니다.

```json
{
  "order": {
    "priceTotal": 89.50,
    "currencyCode": "EUR",
    "purchaseOrderNumber": "JWN20192388410012",
    "payments": [
      {
        "paymentType": "gift_card",
        "paymentAmount": 50
      },
      {
        "paymentType": "credit_card",
        "paymentAmount": 39.50
      }
    ]
  }
}
```

주문을 처리하는 모든 기업이 업계에서 흔히 볼 수 있는 용어에 대해 일관된 방식으로 주문 데이터를 모델링하기로 결정했다면 마법 같은 일이 벌어지기 시작할 수 있다. 데이터(prop 및 evar, 누구나?)를 지속적으로 해석하고 번역하는 대신 조직 내외부에서 정보를 보다 유연하게 교환할 수 있습니다. 머신 러닝을 통해 귀하의 데이터를 보다 쉽게 이해할 수 있습니다 _수단_ 실행 가능한 통찰력을 제공합니다. 관련 데이터를 표시하기 위한 사용자 인터페이스가 보다 직관적이 될 수 있습니다. 동일한 모델링을 따르는 파트너 및 공급업체와 데이터를 원활하게 통합할 수 있습니다.

## XDM

이것이 Adobe의 목표입니다. [경험 데이터 모델](https://business.adobe.com/products/experience-platform/experience-data-model.html). XDM은 산업에서 일반적인 데이터에 대한 규범적 모델링을 제공하는 동시에 특정 요구 사항에 맞게 모델을 확장할 수도 있습니다. Adobe Experience Platform은 XDM을 중심으로 빌드되므로 Experience Platform에 전송된 데이터는 XDM에 있어야 합니다. 데이터를 Experience Platform으로 보내기 전에 현재 데이터 모델을 XDM으로 변환할 수 있는 위치와 방법을 생각하기보다 조직 전체에 XDM을 보다 광범위하게 채택하여 번역을 거의 수행하지 않아도 되도록 하십시오.
