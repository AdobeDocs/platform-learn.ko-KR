---
title: 대상자 만들기
seo-title: Create an audience | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: 대상자 만들기
description: 이 단원에서는 Federated Audience 구성을 활성화하기 위해 Adobe Experience Platform과 Enterprise Data Warehouse 간의 연결을 구성합니다.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
hide: true
source-git-commit: a5ae2695763bc3d6dce786861dcbc15f3422c035
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 3%

---


# 대상자 만들기 연습

이 연습에서는 Federated Audience Composition을 사용하여 Data Warehouse에서 대상을 만드는 과정을 안내합니다. SecurFinancial 고객의 신용 점수가 650점 이상이고 현재 SecurFinancial 포트폴리오에 대출이 없는 고객을 검증하기 위해 대상을 구성합니다.

## 단계

1. **고객 > 대상** 포털에서 **통합 구성** 탭을 클릭합니다.
2. **컴포지션 만들기**&#x200B;를 클릭합니다.

   ![create-composition](assets/create-composition.png)

3. 컴포지션에 `SecurFinancial Customers - No Loans, Good Credit + [your lab user ID]` 레이블을 지정합니다. **만들기**&#x200B;를 클릭합니다.

4. 캔버스에서 **+** 단추를 클릭하고 **대상자 빌드**&#x200B;를 선택합니다. 오른쪽 레일이 표시됩니다.

5. **스키마 선택**&#x200B;을 클릭하고 **FSI_CRM** 스키마를 선택한 다음 **확인**&#x200B;을 클릭합니다.

6. **계속**&#x200B;을 클릭합니다. 쿼리 빌더 창에서 **+** 단추를 클릭한 다음 **사용자 지정 조건**&#x200B;을 클릭합니다. 다음 조건을 만듭니다.
   - `CURRENTPRODUCTS does not contain loan`
   - `AND`
   - `CREDITSCORE greater than or equal to 650`
   - 당사는 마케팅 환경 설정 데이터를 사용하여 이메일을 선택한 고객을 선호하는 커뮤니케이션 채널로 분류합니다.
   - `AND`
   - `CONSENTSMARKETINGPREFERRED equal to email`

   **참고:** 값 필드는 대/소문자를 구분합니다.

   이제 쿼리는 다음과 같아야 합니다.

   ![query-builder](assets/query-builder.png)

7. 다음 **+** 단추를 클릭한 다음 **대상자 저장**&#x200B;을 클릭합니다.

   이 단계의 레이블을 `SecurFinancial Customers - No Loans, Good Credit + [your lab user ID]`(으)로 지정합니다. 대상 레이블과 동일한 값을 사용합니다.

8. 다음 대상 매핑을 추가합니다.
   - **Source 대상 필드:** 전자 메일
   - **Source 대상 필드:** CURRENTPRODUCTS
   - **Source 대상 필드:** 이름

9. 프로필에 사용할 기본 ID 및 네임스페이스 선택:
   - **기본 ID 필드:** 전자 메일
   - **ID 네임스페이스:** 전자 메일

10. **저장**&#x200B;을 클릭한 다음 **시작**&#x200B;을 클릭하여 방금 작성한 컴포지션의 쿼리를 실행합니다.

**참고:** 정품 인증을 위해 다운스트림 플랫폼으로 신용 점수와 같은 중요한 데이터를 이동하지 않은 대상을 만들기 위해 제품 및 신용 정보를 사용했습니다.

대상 구성에 대한 자세한 내용을 보려면 [Experience League](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/compositions/create-composition/create-composition){target="_blank"}을(를) 방문하세요.

페더레이션 대상이 생성되었으므로 [S3 계정에 매핑](map-federated-audience-to-s3.md)을 사용하여 진행하겠습니다.
