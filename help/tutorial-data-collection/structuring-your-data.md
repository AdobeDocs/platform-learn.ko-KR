---
title: 데이터 구조화
description: 데이터 구조화
exl-id: 8d176389-25a4-4718-afff-efd2f87204ed
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# 데이터 구조화

기업은 자신의 도메인에 대해 소통하는 고유한 언어를 가지고 있습니다. 자동차 대리점들은 자동차 제조, 모델, 실린더를 취급한다. 항공사들은 항공편 번호, 서비스 등급, 좌석 배정 등을 처리합니다. 이러한 용어 중 일부는 특정 회사에 고유하며, 일부는 업계 카테고리 간에 공유되며 일부는 거의 모든 회사에서 공유됩니다. 업계 카테고리 또는 보다 광범위한 간에 공유되는 용어는 공통 방식으로 이러한 용어를 지정하고 구성할 때 데이터로 강력한 작업을 시작할 수 있습니다.

예를 들어, 많은 기업들이 주문을 처리하고 있습니다. 이런 기업들이 비슷한 방식으로 주문을 외우기로 했다면 어떨까. 예를 들어, 데이터 모델이 `priceTotal` 주문의 총 가격을 나타내는 속성? 해당 객체에 이름이 지정된 속성도 있는 경우 `currencyCode` 및 `purchaseOrderNumber`? 순서 개체에 이름이 지정된 속성이 있을 수 있습니다. `payments` 그것은 지불물들의 배열일 것입니다. 각 객체는 주문에 대한 지급을 나타냅니다. 예를 들어, 한 고객이 상품권으로 주문의 일부 대금을 결제하고 나머지 대금을 신용 카드로 결제할 수 있습니다. 다음과 같은 모양의 모델을 구성할 수 있습니다.

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

주문을 처리하는 모든 기업이 업계에서 흔히 볼 수 있는 조건에 일관된 방식으로 주문 데이터를 모델링하기로 결정한다면, 마법 같은 일들이 일어날 수 있습니다. 데이터(prop 및 evar 등)를 지속적으로 해석하고 번역하지 않고 조직 내외부에서 정보를 보다 유동적으로 교환할 수 있습니다. 머신 러닝을 통해 데이터 파악 _수단_ 유용한 통찰력을 제공합니다. 관련 데이터를 표시하기 위한 사용자 인터페이스가 보다 직관적이 될 수 있습니다. 데이터는 동일한 모델링을 수행하는 파트너 및 공급업체와 원활하게 통합될 수 있습니다.

## XDM

이것이 Adobe의 목표이다 [경험 데이터 모델](https://business.adobe.com/products/experience-platform/experience-data-model.html). XDM은 업계에서 일반적으로 사용되는 데이터에 대한 규범적인 모델링을 제공하는 동시에 특정 요구 사항에 맞게 모델을 확장할 수 있습니다. Adobe Experience Platform은 XDM을 기반으로 구축되며, 따라서 Experience Platform으로 전송된 데이터는 XDM에 있어야 합니다. 데이터를 Experience Platform에 보내기 전에 현재 데이터 모델을 XDM으로 변환할 수 있는 위치와 방법을 계산하지 않고 조직 전반에 걸쳐 XDM을 더욱 유연하게 채택하여 번역을 거의 수행할 필요가 없습니다.

[다음: ](configure-the-server/create-a-schema.md)

>[!NOTE]
>
>데이터 수집에 시간을 내어 주셔서 감사합니다. 질문이 있거나 일반 피드백을 공유하거나 향후 컨텐츠에 대한 제안 사항이 있는 경우 해당 정보를 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
