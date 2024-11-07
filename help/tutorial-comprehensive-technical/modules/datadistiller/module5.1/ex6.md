---
title: 쿼리 서비스 - Tableau를 사용하여 데이터 세트 살펴보기
description: 쿼리 서비스 - Tableau를 사용하여 데이터 세트 살펴보기
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 5.1.6 쿼리 서비스 및 타블로

타블로를 엽니다.

![start-tableau.png](./images/start-tableau.png)

**서버에 연결**&#x200B;에서 **PostgreSQL**&#x200B;을(를) 선택합니다.

![tableau-connect-postgress.png](./images/tableau-connect-postgress.png)

Adobe Experience Platform, **쿼리** 및 **자격 증명**(으)로 이동합니다.

![query-service-credentials.png](./images/query-service-credentials.png)

Adobe Experience Platform의 **자격 증명** 페이지에서 **호스트**&#x200B;를 복사하여 **서버** 필드에 붙여 넣고, **데이터베이스**&#x200B;를 복사하여 Tableau의 **데이터베이스** 필드에 붙여 넣고, **포트**&#x200B;를 복사하여 Tableau의 **포트**&#x200B;필드에 붙여 넣고, **사용자 이름** 및 **암호**&#x200B;에 대해서도 동일하게 수행합니다. **로그인**&#x200B;을 클릭합니다.

로그인:

![tableau-connection-dialog.png](./images/tableau-connection-dialog.png)

검색(1)을 클릭하고 검색 필드에 **ldap**&#x200B;을(를) 입력한 다음, 결과 집합에서 테이블을 식별하고 (3) **테이블을 여기로 드래그하십시오**. 완료되면 **시트 1**(3)을 클릭합니다.

![tableau-drag-table.png](./images/tableau-drag-table.png)

지도에서 데이터를 시각화하려면 경도와 위도를 차원으로 변환해야 합니다. **측정 단위**&#x200B;에서 **위도**(1)를 선택하고 필드의 드롭다운을 연 다음 **Dimension으로 전환**(2)을 선택합니다. **경도** 측정값에 대해서도 동일한 작업을 수행합니다.

![tableau-convert-dimension.png](./images/tableau-convert-dimension.png)

**경도** 측정값을 **열**, **위도** 측정값을 **행**(으)로 드래그합니다. 자동으로 **벨기에**&#x200B;의 지도가 표시되며, 데이터 집합의 도시를 나타내는 작은 점이 표시됩니다.

![tableau-drag-lon-lat.png](./images/tableau-drag-lon-lat.png)

**측정값 이름**(1)을 선택하고 드롭다운을 연 다음 **시트에 추가**(2)를 선택합니다.

![tableau-select-measure-names.png](./images/tableau-select-measure-names.png)

이제 다양한 크기의 점이 있는 지도가 제공됩니다. 크기는 해당 도시에 대한 콜센터 상호 작용 수를 나타냅니다. 점의 크기를 변경하려면 오른쪽 패널로 이동하여 **측정값**&#x200B;을 엽니다(드롭다운 아이콘 사용). 드롭다운 목록에서 **크기 편집**&#x200B;을 선택합니다. 다양한 크기로 놀아보세요.

![tableau-vary-size-dots.png](./images/tableau-vary-size-dots.png)

**통화 주제**&#x200B;별 데이터를 더 표시하려면 **통화 주제** 차원을 **페이지**(으)로 끌어서 놓습니다. 화면 오른쪽의 **통화 주제**(2)를 사용하여 다른 **통화 주제**&#x200B;를 탐색합니다.

![tableau-call-topic-navigation.png](./images/tableau-call-topic-navigation.png)

이제 이 연습을 완료했습니다.

다음 단계: [5.1.7 쿼리 서비스 API](./ex7.md)

[모듈 5.1로 돌아가기](./query-service.md)

[모든 모듈로 돌아가기](../../../overview.md)
