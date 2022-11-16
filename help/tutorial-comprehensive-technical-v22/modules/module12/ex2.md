---
title: BigQuery Source Connector를 사용하여 Adobe Experience Platform에서 Google Analytics 데이터를 수집 및 분석 - BigQuery에서 첫 번째 쿼리를 만듭니다
description: BigQuery Source Connector를 사용하여 Adobe Experience Platform에서 Google Analytics 데이터를 수집 및 분석 - BigQuery에서 첫 번째 쿼리를 만듭니다
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 73154afc-c3e3-420c-9471-5bb106dbfd02
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 1%

---

# 12.2 BigQuery에서 첫 번째 쿼리 만들기

## 목표

- BigQuery UI 살펴보기
- BigQuery에서 SQL 쿼리 만들기
- BigQuery 내의 데이터 집합에 SQL 쿼리 결과를 저장합니다.

## 컨텍스트

Google Analytics 데이터가 BigQuery에 있으면 차원, 지표 및 기타 변수가 모두 중첩됩니다. 또한 Google Analytics 데이터는 매일 다른 테이블에 로드됩니다. 즉, BigQuery 내의 Google Analytics 테이블을 Adobe Experience Platform에 직접 연결하는 것은 매우 어렵고 좋은 생각이 아닙니다.

이 문제의 해결 방법은 Google Analytics 데이터를 읽기 가능한 형식으로 변환하여 Adobe Experience Platform으로 쉽게 수집하는 것입니다.

## 12.2.1 새 BigQuery 테이블을 저장할 데이터 세트 만들기

로 이동합니다. [BigQuery 콘솔](https://console.cloud.google.com/bigquery).

![데모](./images/ex3/1.png)

in **탐색기**, 프로젝트 ID가 표시됩니다. 프로젝트 ID를 클릭합니다(를 클릭하지 않음). **bigquery-public-data** 데이터 세트)만 로드하는 것입니다.

![데모](./images/ex3/2.png)

데이터 세트가 아직 없음을 알 수 있으므로 지금 만들어 보겠습니다.
클릭 **데이터 집합 만들기**.

![데모](./images/ex3/4.png)

화면 오른쪽에는 **데이터 집합 만들기** 메뉴 아래의 제품에서 사용할 수 있습니다.

![데모](./images/ex3/5.png)

대상 **데이터 세트 ID**&#x200B;를 채울 때는 아래 명명 규칙을 사용하십시오. 다른 필드의 경우 기본 설정을 그대로 둡니다.

| 이름 지정 | 예 |
| ----------------- | ------------- | 
| `--demoProfileLdap--_BigQueryDataSets` | vangeluw_BigQueryDataSets |

![데모](./images/ex3/6.png)

다음을 클릭합니다. **데이터 집합 만들기**.

![데모](./images/ex3/7.png)

그런 다음 데이터 세트를 만든 BigQuery 콘솔로 돌아갑니다.

![데모](./images/ex3/8.png)

## 12.2.2 첫 번째 SQL BigQuery 만들기

다음으로, BigQuery에서 첫 번째 쿼리를 만듭니다. 이 쿼리의 목적은 Google Analytics 샘플 데이터를 가져와서 Adobe Experience Platform에서 수집할 수 있도록 변환하는 것입니다. 로 이동합니다. **편집자** 탭.

![데모](./images/ex3/9.png)

다음 SQL 쿼리를 복사하여 해당 쿼리 편집기에 붙여 넣으십시오. 자유롭게 쿼리를 읽고 Google Analytics BigQuery 구문을 이해할 수 있습니다.


```sql
SELECT
  CONCAT(fullVisitorId, CAST(hitTime AS String), '-', hitNumber) AS _id,
  TIMESTAMP(DATETIME(Year_Current, Month_Current, Day_Current, Hour, Minutes, Seconds)) AS timeStamp,
  fullVisitorId as GA_ID,
  -- Fake CUSTOMER ID
  CONCAT('3E-D4-',fullVisitorId, '-1W-93F' ) as customerID,
  Page,
  Landing_Page,
  Exit_Page,
  Device,
  Browser,
  MarketingChannel,
  TrafficSource,
  TrafficMedium,
  -- Enhanced Ecommerce
  TransactionID,
  CASE
      WHEN EcommerceActionType = '2' THEN 'Product_Detail_Views'
      WHEN EcommerceActionType = '3' THEN 'Adds_To_Cart'
      WHEN EcommerceActionType = '4' THEN 'Product_Removes_From_Cart'
      WHEN EcommerceActionType = '5' THEN 'Product_Checkouts'
      WHEN EcommerceActionType = '6' THEN 'Product_Refunds'
    ELSE
    NULL
  END
     AS Ecommerce_Action_Type,
  -- Entrances (metric)
  SUM(CASE
      WHEN isEntrance = TRUE THEN 1
    ELSE
    0
  END
    ) AS Entries,
    
--Pageviews (metric)
    COUNT(*) AS Pageviews,
    
 -- Exits 
    SUM(
    IF
      (isExit IS NOT NULL,
        1,
        0)) AS Exits,
        
 --Bounces
   SUM(CASE
      WHEN isExit = TRUE AND isEntrance = TRUE THEN 1
    ELSE
    0
  END
    ) AS Bounces,
        
  -- Unique Purchases (metric)
  COUNT(DISTINCT TransactionID) AS Unique_Purchases,
  -- Product Detail Views (metric)
  COUNT(CASE
      WHEN EcommerceActionType = '2' THEN fullVisitorId
    ELSE
    NULL
  END
    ) AS Product_Detail_Views,
  -- Product Adds To Cart (metric)
  COUNT(CASE
      WHEN EcommerceActionType = '3' THEN fullVisitorId
    ELSE
    NULL
  END
    ) AS Adds_To_Cart,
  -- Product Removes From Cart (metric)
  COUNT(CASE
      WHEN EcommerceActionType = '4' THEN fullVisitorId
    ELSE
    NULL
  END
    ) AS Product_Removes_From_Cart,
  -- Product Checkouts (metric)
  COUNT(CASE
      WHEN EcommerceActionType = '5' THEN fullVisitorId
    ELSE
    NULL
  END
    ) AS Product_Checkouts,
  -- Product Refunds (metric)
  COUNT(CASE
      WHEN EcommerceActionType = '7' THEN fullVisitorId
    ELSE
    NULL
  END
    ) AS Product_Refunds
  FROM (
  SELECT
    -- Landing Page (dimension)
    CASE
      WHEN hits.isEntrance = TRUE THEN hits.page.pageTitle
    ELSE NULL
  END
    AS Landing_page,
    
        -- Exit Page (dimension)
    CASE
      WHEN hits.isExit = TRUE THEN hits.page.pageTitle
    ELSE
    NULL
  END
    AS Exit_page,
    
    hits.page.pageTitle AS Page,
    hits.isEntrance,
    hits.isExit,
    hits.hitNumber as hitNumber,
    hits.time as hitTime,
    date as Fecha,
    fullVisitorId,
    visitStartTime,
    device.deviceCategory AS Device,
    device.browser AS Browser,
    channelGrouping AS MarketingChannel,
    trafficSource.source AS TrafficSource,
    trafficSource.medium AS TrafficMedium,
    hits.transaction.transactionId AS TransactionID,
    CAST(EXTRACT(YEAR FROM CURRENT_DATE()) AS INT64) AS Year_Current,
    CAST(EXTRACT(MONTH FROM CURRENT_DATE()) AS INT64) AS Month_Current,
     CAST(EXTRACT(DAY FROM CURRENT_DATE()) AS INT64) AS Day_Current,
    CAST(EXTRACT(DAY FROM DATE_SUB(CURRENT_DATE(),INTERVAL 1 DAY)) AS INT64) AS Day_Current_Before,
    CAST(FORMAT_DATE('%Y', PARSE_DATE("%Y%m%d", date)) AS INT64) AS Year,
  CAST(FORMAT_DATE('%m', PARSE_DATE("%Y%m%d",date)) AS INT64) AS Month,
  CAST(FORMAT_DATE('%d', PARSE_DATE("%Y%m%d",date)) AS INT64) AS Day,
    CAST(EXTRACT (hour FROM TIMESTAMP_SECONDS(hits.time)) AS INT64) AS Hour,
  CAST(EXTRACT (minute FROM TIMESTAMP_SECONDS(hits.time)) AS INT64) AS Minutes,
  CAST(EXTRACT (second FROM TIMESTAMP_SECONDS(hits.time)) AS INT64) AS SecondS,
    hits.eCommerceAction.action_type AS EcommerceActionType
  
  FROM
    `bigquery-public-data.google_analytics_sample.ga_sessions_*`,
     UNNEST(hits) AS hits
  WHERE
    _table_suffix BETWEEN '20170101'
    AND '20170331'
    AND totals.visits = 1
    AND hits.type = 'PAGE'
    )
    
GROUP BY
  1,
  2,
  3,
  4,
  5,
  6,
  7,
  8,
  9,
  10,
  11,
  12,
  13,
  14
    
  ORDER BY 2 DESC
```

준비가 되면 을(를) 클릭합니다. **실행** 쿼리를 실행하려면

![데모](./images/ex3/10.png)

쿼리를 실행하는 데 2분 정도 걸릴 수 있습니다.

쿼리 실행이 끝나면, **쿼리 결과**.

![데모](./images/ex3/12.png)

## 12.2.3 BigQuery SQL 쿼리 결과 저장

다음 단계는 **결과 저장** 버튼을 클릭합니다.

![데모](./images/ex3/13.png)

출력의 위치로 를 선택합니다 **BigQuery 테이블**.

![데모](./images/ex3/14.png)

그러면 새 팝업이 표시됩니다. 여기서 **프로젝트 이름** 및 **데이터 집합 이름** 는 미리 채워집니다. 데이터 집합 이름은 이 연습 시작 시 만든 데이터 집합이어야 하며 다음 명명 규칙을 사용합니다.

| 이름 지정 | 예 |
| ----------------- | ------------- | 
| `--demoProfileLdap--_BigQueryDataSets` | `vangeluw_BigQueryDataSets` |

이제 테이블 이름을 입력해야 합니다. 다음 명명 규칙을 사용하십시오.

| 이름 지정 | 예 |
| ----------------- |------------- | 
| `--demoProfileLdap--_GAdataTableBigQuery` | `vangeluw_GAdataTableBigQuery` |

![데모](./images/ex3/16.png)

**저장**&#x200B;을 클릭합니다.

만든 표에 데이터가 준비될 때까지 시간이 걸릴 수 있습니다. 몇 분 후에 브라우저를 새로 고칩니다. 그러면 데이터 세트 내에 이 표시됩니다 `--demoProfileLdap--_GAdataTableBigquery` 테이블 아래 **탐색기** BigQuery 프로젝트 내부에서

![데모](./images/ex3/19.png)

이제 다음 연습을 계속 진행합니다. 여기서 이 테이블을 Adobe Experience Platform에 연결합니다.

다음 단계: [12.3 GCP 및 BigQuery를 Adobe Experience Platform에 연결](./ex3.md)

[모듈 12로 돌아가기](./customer-journey-analytics-bigquery-gcp.md)

[모든 모듈로 돌아가기](./../../overview.md)
