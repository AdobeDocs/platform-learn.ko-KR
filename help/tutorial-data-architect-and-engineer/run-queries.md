---
title: 쿼리 실행
seo-title: Run queries | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 쿼리 실행
description: 이 단원에서는 수집한 데이터의 유효성을 확인하기 위해 쿼리를 설정, 작성 및 실행하는 방법을 알아봅니다.
role: Data Architect, Data Engineer
feature: Queries
kt: 4348
thumbnail: 4348-run-queries.jpg
exl-id: a37531cb-96ad-4547-86af-84f7ed65f019
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 3%

---

# 쿼리 실행

<!-- 15 min-->
이 단원에서는 수집한 데이터의 유효성을 확인하기 위해 쿼리를 설정, 작성 및 실행하는 방법을 알아봅니다.

Adobe Experience Platform Query Service를 사용하면 표준 SQL을 사용하여 Platform에서 데이터를 쿼리할 수 있으므로 데이터를 이해할 수 있습니다. Query Service를 사용하여 데이터 레이크에서 모든 데이터 세트에 참여하고 쿼리 결과를 보고, 기계 학습 또는 실시간 고객 프로필에 수집하기 위한 새로운 데이터 세트로 캡처할 수 있습니다.

**데이터 설계자** 및 **데이터 엔지니어** 은 이 자습서의 외부에서 쿼리 서비스를 사용해야 합니다.

연습을 시작하기 전에 이 짧은 비디오에서 쿼리 서비스에 대해 자세히 알아보십시오.
>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## 필요한 권한

에서 [권한 구성](configure-permissions.md) 이 단원을 완료하는 데 필요한 모든 액세스 컨트롤을 설정합니다.

<!-- Settings > **[!UICONTROL Services]** > **[!UICONTROL Query Service]**
* Permission items Data Management > **[!UICONTROL View Datasets]** and  **[!UICONTROL Manage Datasets]**
* Permission item Sandboxes > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## 단순 쿼리

간단한 몇 가지 쿼리로 시작하십시오.

1. Platform 사용자 인터페이스에서 로 이동합니다. **쿼리** 왼쪽 탐색
1. 을(를) 선택합니다 **쿼리 만들기** 오른쪽 상단의 단추를 클릭하여 쿼리를 실행하고 실행할 텍스트 상자를 엽니다.
1. 편집기에서 다음 쿼리를 입력하고 Shift+Enter 또는 Shift+Return 키를 눌러 쿼리를 실행합니다.

   ```
   SHOW TABLES
   ```

1. 사용 가능한 테이블 목록이 표시됩니다

   ![테이블 쿼리 표시](assets/queries-showTables.png)


1. 이제 이 쿼리를 사용하여 `_techmarketingdemos` 를 사용 중이면 스키마에 표시되는 고유한 테넌트 네임스페이스가 있습니다.

   ```
   SELECT person.name.lastName,loyalty.tier
   FROM luma_loyalty_dataset
   WHERE loyalty.tier ='gold'
   ```

   ![충성도 데이터 세트에서 데이터 선택](assets/queries-loyaltySelect.png)

1. 오류가 발생하면 자세한 메시지는 **[!UICONTROL 콘솔]** 탭 - 아래 그림과 같이
   ![쿼리의 오류](assets/queries-error.png)

1. 성공적인 쿼리를 통해 **[!UICONTROL 이름]** it `Luma Gold Level Customers`
1. **[!UICONTROL 저장]** 버튼을 선택합니다
   ![쿼리 저장](assets/queries-loyaltySelect-save.png)


<!--SELECT COUNT(DISTINCT (_techmarketingdemos.systemIdentifier.loyaltyId)) FROM luma_loyalty_dataset 


SELECT _techmarketingdemos.systemIdentifier.loyaltyId, COUNT(_techmarketingdemos.systemIdentifier.loyaltyId)
FROM luma_loyalty_dataset 
GROUP BY _techmarketingdemos.systemIdentifier.loyaltyId
HAVING COUNT(_techmarketingdemos.systemIdentifier.loyaltyId) > 1;-->

## 추가 연습

나중에 추가 쿼리 서비스 연습이 자습서에 추가됩니다.
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

* [Query Service 설명서](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=ko)
* [쿼리 서비스 API 참조](https://www.adobe.io/experience-platform-apis/references/query-service/)

그리고 지금 마지막 실습 수업을 위해 [세그먼트 만들기](build-segments.md)!
