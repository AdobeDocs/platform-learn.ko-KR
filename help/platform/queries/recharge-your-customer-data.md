---
title: 고객 데이터를 재충전하여 매력적인 경험 전달
description: 저품질 데이터의 영향을 줄이고, 가치 창출 시간을 단축하며, 다수의 사용 사례에 대해 동일한 데이터를 사용하여 ROI를 높이는 방법을 알아봅니다.
role: Data Engineer, Data Architect, Developer
feature: Queries
kt: 10323
thumbnail: 342533.jpeg
exl-id: 30574cc5-66fa-4ab8-83ed-7af710294dbf
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 3%

---

# 고객 데이터를 재충전하여 매력적인 경험 전달

옴니채널 데이터는 마케터가 활성화 오케스트레이션 및 결과 고객 여정을 측정하는 데 사용하는 실행 가능한 고객 프로필을 수행하는 데 중요한 요소입니다. 그러나 조직은 이러한 데이터의 품질, 규모 및 다양성을 관리해야 하는 어려움에 직면해 있습니다. 이 솔루션은 저품질 데이터의 영향을 줄이고, 가치 창출 시간을 단축하며, 다양한 사용 사례에 대해 동일한 데이터를 사용하여 ROI를 증대하기 위해 간소화된 솔루션이 필요합니다.

이 비디오에서는 다음을 설명합니다.

* 활용할 수 있는 Adobe Experience Platform 데이터 준비 기능
* Adobe Real-Time CDP, Adobe Journey Optimizer 및 Customer Journey Analytics에서 ROI 향상

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## SQL 예

```sql
INSERT INTO summit_adv_data_prep_dataset
SELECT STRUCT(
customerId AS crmCustomerId, struct(sku AS sku, price AS sku_price, abandonTS AS abandonTS) AS abandonBrowse) AS _pfreportingonprod
FROM
(SELECT
B.personKey.sourceID AS customerId,
A.productListItems[0].SKU AS sku,
max(A.timestamp) AS abandonTS,
max(C._pfreportingonprod.price) AS price
FROM summit_adobe_analytics_dataset A,profile_attribute_14adf268_2a20_4dee_bee6_a6b0e34616a9 B,summit_product_dataset C
WHERE A._experience.analytics.customDimensions.eVars.eVar1 = B.personKey.sourceID
AND A.productListItems[0].sku = C._pfreportingonprod.sku
AND A.web.webpagedetails.URL NOT LIKE '%orderconfirmation%'
AND timestamp > current_date - interval '4 day'
GROUP BY customerId,sku
order by price desc)D;
```

자세한 내용은 [Query Service 설명서](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=ko).

>[!NOTE]
>
>이 비디오는 Adobe Summit 2020 세션에서 발췌한 것입니다 *[경험을 위한 옴니채널 데이터 충전](https://business.adobe.com/summit/2022/sessions/recharging-omnichannel-data-for-electrifying-exper-s409.html)*.
