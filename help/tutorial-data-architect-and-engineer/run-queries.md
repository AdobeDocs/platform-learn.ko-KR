---
title: 쿼리 실행
seo-title: Run queries | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 쿼리 실행
description: 이 단원에서는 수집한 데이터의 유효성을 확인하기 위해 쿼리를 설정, 쓰기 및 실행하는 방법에 대해 알아봅니다.
role: Data Architect, Data Engineer
feature: Queries
jira: KT-4348
thumbnail: 4348-run-queries.jpg
exl-id: a37531cb-96ad-4547-86af-84f7ed65f019
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 4%

---

# 쿼리 실행

<!-- 15 min-->
이 단원에서는 수집한 데이터의 유효성을 확인하기 위해 쿼리를 설정, 쓰기 및 실행하는 방법에 대해 알아봅니다.

Adobe Experience Platform Query Service를 사용하면 표준 SQL을 사용하여 Platform에서 데이터를 쿼리할 수 있으므로 데이터를 이해할 수 있습니다. 쿼리 서비스를 사용하면 데이터 레이크에서 모든 데이터 세트에 참여하고 쿼리 결과를 보고, 머신 러닝에 사용하거나 실시간 고객 프로필에 수집하기 위한 새 데이터 세트로 캡처할 수 있습니다.

**데이터 설계자** 및 **데이터 엔지니어** 은(는) 이 자습서 외부에서 쿼리 서비스를 사용해야 합니다.

연습을 시작하기 전에 이 짧은 비디오를 시청하여 쿼리 서비스에 대해 자세히 알아보십시오.
>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## 권한 필요

다음에서 [권한 구성](configure-permissions.md) 단원, 이 단원을 완료하는 데 필요한 모든 액세스 제어를 설정합니다.

<!-- Settings > **[!UICONTROL Services]** > **[!UICONTROL Query Service]**
* Permission items Data Management > **[!UICONTROL View Datasets]** and  **[!UICONTROL Manage Datasets]**
* Permission item Sandboxes > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## 단순 쿼리

간단한 쿼리부터 시작하겠습니다.

1. Platform 사용자 인터페이스에서 **쿼리** 왼쪽 탐색
1. 다음 항목 선택 **쿼리 만들기** 쿼리를 실행하고 실행할 텍스트 상자를 여는 오른쪽 상단 단추
1. 편집기에서 다음 쿼리를 입력하고 Shift+Enter 또는 Shift+Return을 눌러 쿼리를 실행합니다.

   ```
   SHOW TABLES
   ```

1. 사용 가능한 테이블 목록을 표시합니다.

   ![테이블 쿼리 표시](assets/queries-showTables.png)


1. 이제 이 쿼리를 시도하고 을(를) 대체하십시오. `_techmarketingdemos` 를 호출하면 스키마에 표시되는 자체 테넌트 네임스페이스가 있습니다.

   ```
   SELECT person.name.lastName,loyalty.tier
   FROM luma_loyalty_dataset
   WHERE loyalty.tier ='gold'
   ```

   ![충성도 데이터 세트에서 데이터 선택](assets/queries-loyaltySelect.png)

1. 오류가 있으면 자세한 메시지가에 표시됩니다. **[!UICONTROL 콘솔]** 아래 그림과 같은 탭
   ![쿼리 오류](assets/queries-error.png)

1. 쿼리가 성공하면 **[!UICONTROL 이름]** it `Luma Gold Level Customers`
1. **[!UICONTROL 저장]** 버튼을 선택합니다
   ![쿼리 저장 중](assets/queries-loyaltySelect-save.png)


<!--SELECT COUNT(DISTINCT (_techmarketingdemos.systemIdentifier.loyaltyId)) FROM luma_loyalty_dataset 


SELECT _techmarketingdemos.systemIdentifier.loyaltyId, COUNT(_techmarketingdemos.systemIdentifier.loyaltyId)
FROM luma_loyalty_dataset 
GROUP BY _techmarketingdemos.systemIdentifier.loyaltyId
HAVING COUNT(_techmarketingdemos.systemIdentifier.loyaltyId) > 1;-->

## 추가 연습

추가적인 쿼리 서비스 연습이 나중에 자습서에 추가됩니다.
<!--
## Join Datasets

In this exercise, we will join two datasets `Luma Loyalty Dataset` and `Luma Offline Purchase` to get list of gold customers who have spend over $500 dollars in one purchase.

1. Create a new query
1. Copy and paste following query in query editor and execute, again replacing `_techmarketingdemos` with your own tenant namespace
    
    ```
    SELECT DISTINCT lopd.commerce.order.purchaseID as PurchaseId ,
        lld.person.name.firstName as LastName ,
        lld.person.name.lastName as LastName ,
        lopd.personalEmail.address as email,
        lopd.commerce.order.priceTotal as Total

    FROM luma_loyalty_dataset lld
    JOIN luma_offline_purchase_event_dataset lopd
    ON lopd._techmarketingdemos.systemIdentifier.loyaltyId = lld._techmarketingdemos.systemIdentifier.loyaltyId

    WHERE lld._techmarketingdemos.loyalty.level ='gold' AND lopd.commerce.order.priceTotal >500;
    ```

1. You should get list of Gold Customers who have spend over $500 in single purchase.

## Output datasets

1. Select on Output Dataset button
1. Provide name and description to the dataset
1. Save.
1. Go to **Datasets** under **Data Management** to find new dataset created.

-->
<!--Add content for Adobe Defined Functions-->

## 추가 리소스

* [쿼리 서비스 설명서](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=ko)
* [쿼리 서비스 API 참조](https://www.adobe.io/experience-platform-apis/references/query-service/)

그리고 마지막 실습 수업을 위해 [세그먼트 만들기](build-segments.md)!
