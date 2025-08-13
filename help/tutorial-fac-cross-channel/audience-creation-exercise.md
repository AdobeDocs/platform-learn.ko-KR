---
title: 페더레이션 대상 만들기
seo-title: Create a federated audience | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: 페더레이션 대상 만들기
description: 이 시각적 연습에서는 Federated Audience Composition을 활성화하기 위해 Adobe Experience Platform과 Enterprise Data Warehouse 간의 연결을 구성합니다.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
exl-id: a507cab5-dba9-4bf7-a043-d7c967e9e07d
source-git-commit: 15619a8419f608da6a77745fabf72c356a2ac4b4
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# 페더레이션 대상 만들기

다음으로, Federated Audience Composition을 사용하여 Data Warehouse에서 대상을 만드는 과정을 안내합니다. 대상은 신용 점수가 650점 이상이고 현재 SecurFinancial 포트폴리오에 대출이 없는 SecurFinancial 고객으로 구성됩니다.

## 단계

1. **고객 > 대상** 포털에서 **통합 구성** 탭을 클릭합니다.
2. **컴포지션 만들기**&#x200B;를 클릭합니다.

   ![create-composition](assets/create-composition.png)

3. 컴포지션에 레이블을 지정합니다. 이 예제에서는 `SecurFinancial Customers - No Loans, Good Credit`을(를) 사용합니다. **만들기**&#x200B;를 클릭합니다.

4. 캔버스에서 **+** 단추를 클릭하고 **대상자 빌드**&#x200B;를 선택합니다. 오른쪽 레일이 나타납니다.

5. **스키마 선택**&#x200B;을 클릭하고 적절한 스키마를 선택한 다음 **확인**&#x200B;을 클릭합니다.

6. **계속**&#x200B;을 클릭합니다. 쿼리 빌더 창에서 **+** 단추를 클릭한 다음 **사용자 지정 조건**&#x200B;을 클릭합니다. 조건을 작성하십시오. 이 예제에서는 다음을 사용합니다.

   `CURRENTPRODUCTS does not contain loan`
   `AND`
   `CREDITSCORE greater than or equal to 650`
   `AND`
   `CONSENTSMARKETINGPREFERRED equal to email`

   *마지막 조건은 마케팅 환경 설정 데이터가 이메일을 선호하는 커뮤니케이션 채널로 선택한 고객을 세그먼트화하는 데 사용되도록 합니다*.

   **참고:** 값 필드는 대/소문자를 구분합니다.

   ![query-builder](assets/query-builder.png)

7. 다음 **+** 단추를 클릭한 다음 **대상자 저장**&#x200B;을 클릭합니다. 이 단계에 레이블을 지정합니다. 이 예제에서는 `SecurFinancial Customers - No Loans, Good Credit`(으)로 레이블을 지정합니다.

8. 관련 대상 매핑을 추가합니다. 이 예제에서는

   - **Source 대상 필드:** 전자 메일
   - **Source 대상 필드:** CURRENTPRODUCTS
   - **Source 대상 필드:** 이름

9. 프로필에 사용할 기본 ID 및 네임스페이스를 선택합니다. 다음은 데이터에 사용되는 ID 및 필드입니다.

   - **기본 ID 필드:** 전자 메일
   - **ID 네임스페이스:** 전자 메일

10. **저장**&#x200B;을 클릭한 다음 **시작**&#x200B;을 클릭하여 컴포지션 쿼리를 실행합니다.

>[**요약**]
>
> 이 예에서는 제품 및 신용 정보를 사용하여 Adobe Experience Platform의 사본을 만들지 않고 Snowflake에서 엔터프라이즈 데이터에 직접 액세스하여 대상자를 빌드했습니다. 외부 시스템이 쿼리를 처리하고 나면 관련 이메일, 현재 제품 및 이름 값만 다운스트림 활성화를 위해 대상 정의로 가져옵니다. 이는 RTCDP이 지원하는 모든 대상에 적용됩니다.

대상 구성에 대한 자세한 내용을 보려면 [Experience League](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/compositions/create-composition/create-composition){target="_blank"}을(를) 방문하세요.

페더레이션 대상이 만들어졌으므로 [S3 계정에 매핑](map-federated-audience-to-s3.md)합니다.
