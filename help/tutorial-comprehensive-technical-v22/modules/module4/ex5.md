---
title: 쿼리 서비스 - Power BI을 사용하여 데이터 집합 탐색
description: 쿼리 서비스 - Power BI을 사용하여 데이터 집합 탐색
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 0f9e6719-056b-4858-8c86-04b3beaa950e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# 4.5 쿼리 서비스 및 Power BI

Microsoft Power BI Desktop을 엽니다.

![start-power-bi.png](./images/start-power-bi.png)

클릭 **데이터 가져오기**.

![power-bi-get-data.png](./images/power-bi-get-data.png)

검색 대상 **postgres** (1), 을(를) 선택합니다. **Postgres** (2) 목록에서 **Connect** (3).

![power-bi-connect-progress.png](./images/power-bi-connect-progress.png)

Adobe Experience Platform으로 이동하여 **쿼리** 및 **자격 증명**.

![query-service-credentials.png](./images/query-service-credentials.png)

에서 **자격 증명** Adobe Experience Platform에서 페이지를 복사합니다. **호스트** 여기에 붙여넣습니다 **서버** 필드를 작성하고 **데이터베이스** 여기에 붙여넣습니다 **데이터베이스** PowerBI의 필드를 클릭한 다음 확인(2)을 클릭합니다.

>[!IMPORTANT]
>
>포트를 포함해야 합니다. **0:80** 현재 Query Service가 기본 PostgreSQL 포트 5432를 사용하지 않으므로 서버 값 끝에 있습니다.

![power-bi-connect-server.png](./images/power-bi-connect-server.png)

다음 대화 상자에서 사용자 이름과 암호를 **자격 증명** Adobe Experience Platform의 쿼리

![query-service-credentials.png](./images/query-service-credentials.png)

네비게이터 대화 상자에서 **LDAP** 검색 필드(1)에서 CTAS 데이터 세트를 찾고 각 (2) 옆에 있는 상자를 선택합니다. 그런 다음 로드(3)를 클릭합니다.

![power-bi-load-churn-data.png](./images/power-bi-load-churn-data.png)

다음을 확인합니다. **보고서** 탭(1)이 선택되어 있습니다.

![power-bi-report-tab.png](./images/power-bi-report-tab.png)

맵(1)을 선택하고 보고 캔버스에 추가한 후 맵(2)을 확대합니다.

![power-bi-select-map.png](./images/power-bi-select-map.png)

그런 다음 측정값과 차원을 정의해야 합니다. 이렇게 하려면 **필드** 해당 자리 표시자( 아래에 있음) **시각화**)에 사용할 수 있습니다.

![power-bi-drag-lat-lon.png](./images/power-bi-drag-lat-lon.png)

측정으로는 **customerId**. 을(를) 드래그합니다. **crmid** 필드의 필드 **필드** 섹션에 **크기** 자리 표시자:

![power-bi-drag-crmid.png](./images/power-bi-drag-crmid.png)

마지막으로, **callTopic** 분석, **callTopic** 에 대한 필드 **페이지 수준 필터** 자리 표시자(다음을 스크롤해야 할 수 있음 **시각화** 섹션)

![power-bi-drag-calltopic.png](./images/power-bi-drag-calltopic.png)

선택/선택 취소 **callTopics** 다음을 조사합니다.

![power-bi-report-select-calltopic.png](./images/power-bi-report-select-calltopic.png)

이제 이 운동을 끝마쳤습니다.

다음 단계: [4.7 Query Service API](./ex7.md)

[모듈 4로 돌아가기](./query-service.md)

[모든 모듈로 돌아가기](../../overview.md)
