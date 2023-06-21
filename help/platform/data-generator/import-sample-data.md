---
title: Adobe Experience Platform으로 샘플 데이터 가져오기
description: 일부 샘플 데이터를 사용하여 Experience Platform 샌드박스 환경을 설정하는 방법에 대해 알아봅니다.
role: Developer
feature: API
kt: 7349
thumbnail: 7349.jpg
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: da94f4bd-0686-4d6a-a158-506f2e401b4e
source-git-commit: 60f509ef55ce121f572466a8f13953dba982a0ce
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 5%

---

# Adobe Experience Platform으로 샘플 데이터 가져오기

샘플 데이터를 사용하여 Experience Platform 샌드박스 환경을 설정하는 방법에 대해 알아봅니다. Postman 컬렉션을 사용하여 필드 그룹, 스키마, 데이터 세트를 만든 다음 샘플 데이터를 Experience Platform으로 가져올 수 있습니다.

## 샘플 데이터 사용 사례

Experience Platform 비즈니스 사용자는 Experience Platform이 제공하는 마케팅 기능을 탐색하기 전에 필드 그룹 식별, 스키마 만들기, 데이터 준비, 데이터 세트 만들기 및 데이터 수집을 포함하는 일련의 단계를 거쳐야 하는 경우가 많습니다. 이 자습서는 일부 단계를 자동화하여 데이터를 Platform 샌드박스로 최대한 빨리 가져올 수 있습니다.

이 튜토리얼은 Luma라는 가상의 소매 브랜드에 중점을 둡니다. 이들은 Adobe Experience Platform에 투자하여 충성도, CRM, 제품 카탈로그 및 오프라인 구매 데이터를 실시간 고객 프로필에 결합하고 이러한 프로필을 활성화하여 마케팅을 한 차원 더 발전시킵니다. Luma에 대한 샘플 데이터를 생성했으며 이 자습서의 나머지 부분에서 이 데이터를 Experience Platform 샌드박스 환경 중 하나로 가져옵니다.

>[!NOTE]
>
>이 자습서의 최종 결과는 과 유사한 데이터가 포함된 샌드박스입니다. [데이터 설계자 및 데이터 엔지니어를 위한 Adobe Experience Platform 시작하기 자습서](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html). 을 지원하도록 2023년 4월에 업데이트되었습니다. [Journey Optimizer 과제](https://experienceleague.adobe.com/docs/journey-optimizer-learn/challenges/introduction-and-prerequisites.html?lang=ko). 인증 방법을 OAuth로 전환하도록 2023년 6월에 업데이트했습니다.


## 사전 요구 사항

* Experience Platform API에 대한 액세스 권한이 있으며 인증 방법을 알고 있습니다. 그렇지 않은 경우 다음을 검토하십시오. [튜토리얼](https://experienceleague.adobe.com/docs/platform-learn/tutorials/platform-api-authentication.html?lang=ko).
* Experience Platform 개발 샌드박스에 액세스할 수 있습니다.
* Experience Platform 테넌트 ID를 알고 있습니다. 를 인증하여 가져올 수 있습니다 [API 요청](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/getting-started.html?lang=en#know-your-tenant_id)
또는 Platform 계정에 로그인할 때 URL에서 추출하여 사용할 수 있습니다. 예를 들어 다음 URL에서 테넌트는 &quot;입니다`techmarketingdemos`&quot; `https://experience.adobe.com/#/@techmarketingdemos/sname:prod/platform/home`.

## 사용 [!DNL Postman] {#postman}

### 환경 변수 설정

단계를 따르려면 먼저 를 다운로드했는지 확인합니다. [Postman](https://www.postman.com/downloads/) 응용 프로그램. 그럼 시작해 보겠습니다!

1. 다운로드 [platform-utils-main.zip](../assets/data-generator/platform-utils-main.zip) 이 자습서에 필요한 모든 파일이 포함된 파일입니다.

   >[!NOTE]
   >
   >에 포함된 사용자 데이터 [platform-utils-main.zip](../assets/data-generator/platform-utils-main.zip) 파일은 가상 파일이며 데모용으로만 사용됩니다.

1. 다운로드 폴더의 `platform-utils-main.zip` 파일을 컴퓨터에서 원하는 위치로 옮긴 다음 압축을 풉니다.
1. 다음에서 `luma-data` 폴더, 모든 폴더 열기 `json` 텍스트 편집기의 파일 및 `_yourTenantId` 자신의 테넌트 id를 사용하고, 앞에 밑줄이 그어집니다.
1. 열기 `luma-offline-purchases.json`, `luma-inventory-events.json`, 및 `luma-web-events.json` 텍스트 편집기에서 이벤트가 지난 달에 발생하도록 모든 타임스탬프를 업데이트합니다(예: 검색 `"timestamp":"2022-11` 및 연도 및 월 대체)
1. 나중에 를 설정할 때 필요하므로 압축 해제된 폴더의 위치를 확인합니다. `FILE_PATH` [!DNL Postman] 환경 변수:

   >[!NOTE]
   > Mac에서 파일 경로를 얻으려면 `platform-utils-main` 폴더를 마우스 오른쪽 단추로 클릭하고 **정보 가져오기** 옵션을 선택합니다.
   >
   > ![MAC 파일 경로](../assets/data-generator/images/mac-file-path.png)

   >[!NOTE]
   > 창에서 파일 경로를 얻으려면 를 클릭하여 원하는 폴더의 위치를 연 다음, 주소 표시줄의 경로 오른쪽을 마우스 오른쪽 단추로 클릭합니다. 주소를 복사하여 파일 경로를 가져옵니다.
   > 
   > ![Windows 파일 경로](../assets/data-generator/images/windows-file-path.png)

1. 열기 [!DNL Postman] 및 를 사용하여 작업 공간을 **작업 공간** 드롭다운 메뉴:\
   ![작업 영역 만들기](../assets/data-generator/images/create-workspace.png)
1. 입력 **이름** 및 선택 사항 **요약** 을 클릭하여 작업 영역을 확인하십시오. **작업 영역 만들기**. [!DNL Postman] 새 작업 영역을 만들 때 이 작업 영역으로 전환됩니다.
   ![작업 영역 저장](../assets/data-generator/images/save-workspace.png)
1. 이제 몇 가지 설정을 조정하여 [!DNL Postman] 이 작업 공간의 컬렉션입니다. 의 머리글에서 [!DNL Postman], 톱니바퀴 아이콘 을 클릭하고 **설정** 를 클릭하여 설정 모달을 엽니다. 키보드 단축키 (CMD/CTRL + ,)를 사용하여 모달을 열 수도 있습니다.
1. 아래 `General` 탭, ms 단위의 요청 시간 초과를 다음으로 업데이트 `5000 ms` 및 활성화 `allow reading file outside this directory`
   ![설정](../assets/data-generator/images/settings.png)

   >[!NOTE]
   > 작업 디렉터리 내에서 파일이 로드되는 경우 동일한 파일이 다른 장치에 저장되어 있으면 여러 장치에서 원활하게 실행됩니다. 그러나 작업 디렉터리 외부에서 파일을 실행하려면 설정을 켜야 동일한 의도를 나타낼 수 있습니다. 다음의 경우 `FILE_PATH` 은(는) 과(와) 같지 않습니다. [!DNL Postman]의 작업 디렉토리 경로입니다. 이 옵션을 활성화해야 합니다.

1. 닫기 **설정** 패널.
1. 다음 항목 선택 **환경** 다음을 선택합니다. **가져오기**:
   ![환경 가져오기](../assets/data-generator/images/env-import.png)
1. 다운로드한 json 환경 파일 가져오기, `DataInExperiencePlatform.postman_environment`
1. Postman의 오른쪽 상단 드롭다운에서 환경을 선택하고 눈 모양 아이콘을 클릭하여 환경 변수를 봅니다.
   ![환경 선택](../assets/data-generator/images/env-selection.png)

1. 다음 환경 변수가 채워져 있는지 확인합니다. 환경 변수의 값을 가져오는 방법을 알아보려면 [Experience Platform API 인증](/help/platform/authentication/platform-api-authentication.md) 단계별 지침을 위한 자습서입니다.

   * `CLIENT_SECRET`
   * `API_KEY`—`Client ID` Adobe Developer 콘솔에서
   * `SCOPES`
   * `TECHNICAL_ACCOUNT_ID`
   * `IMS`
   * `IMS_ORG`—`Organization ID` Adobe Developer 콘솔에서
   * `SANDBOX_NAME`
   * `TENANT_ID`—밑줄로 이끌어야 합니다(예: ). `_techmarketingdemos`
   * `CONTAINER_ID`
   * `platform_end_point`
   * `FILE_PATH`- 압축을 푼 로컬 폴더 경로를 사용합니다. `platform-utils-main.zip` 파일. 폴더 이름이 포함되어 있는지 확인합니다(예: ). `/Users/dwright/Desktop/platform-utils-main`

1. **저장** 업데이트된 환경

### Postman 컬렉션 가져오기

그런 다음 컬렉션을 Postman으로 가져와야 합니다.

1. 선택 **컬렉션** 그런 다음 가져오기 옵션을 선택합니다.

   ![컬렉션](../assets/data-generator/images/collections.png)

1. 다음 컬렉션을 가져옵니다.

   * `0-Authentication.postman_collection.json`
   * `1-Luma-Loyalty-Data.postman_collection.json`
   * `2-Luma-CRM-Data.postman_collection.json`
   * `3-Luma-Product-Catalog.postman_collection.json`
   * `4-Luma-Offline-Purchase-Events.postman_collection.json`
   * `5-Luma-Product-Inventory-Events.postman_collection.json`
   * `6-Luma-Test-Profiles.postman_collection.json`
   * `7-Luma-Web-Events.postman_collection.json`

   ![컬렉션 가져오기](../assets/data-generator/images/collection-files.png)

### 인증

다음으로 사용자 토큰을 인증하고 생성해야 합니다. 이 자습서에서 사용되는 토큰 생성 방법은 비프로덕션 전용에 적합합니다. 로컬 서명은 타사 호스트에서 JavaScript 라이브러리를 로드하고 원격 서명은 개인 키를 Adobe이 소유하고 운영하는 웹 서비스로 전송합니다. Adobe은 이 개인 키를 저장하지 않지만 프로덕션 키는 누구와도 공유하면 안 됩니다.

1. 를 엽니다. `0-Authentication` 콜렉션에서 `OAuth: Request Access Token` 요청 및 클릭 `SEND` 액세스 토큰을 인증하고 가져옵니다.

   ![컬렉션 가져오기](../assets/data-generator/images/authentication.png)

1. 환경 변수를 검토하고 `ACCESS_TOKEN` 이제 가 채워집니다.

### 데이터 가져오기

이제 데이터를 준비하고 Platform 샌드박스로 가져올 수 있습니다. 가져온 Postman 컬렉션이 모든 힘든 작업을 수행합니다!

1. 를 엽니다. `1-Luma-Loyalty-Data` 컬렉션 및 클릭 **실행** 개요 탭에서 컬렉션 실행기를 시작합니다.

   ![컬렉션 가져오기](../assets/data-generator/images/loyalty.png)

1. Collection Runner 창의 드롭다운에서 환경을 선택하고 **지연** 끝 `4000ms`을(를) 선택합니다. **응답 저장** 옵션이 추가되고 실행 순서가 올바른지 확인합니다. 다음을 클릭합니다. **Luma 충성도 데이터 실행** 단추

   ![컬렉션 가져오기](../assets/data-generator/images/loyalty-run.png)

   >[!NOTE]
   >
   >**1-Luma-Loyalty-Data** 고객 충성도 데이터를 위한 스키마를 만듭니다. 스키마는 XDM 개인 프로필 클래스, 표준 필드 그룹, 사용자 지정 필드 그룹 및 데이터를 기반으로 합니다. 컬렉션은 스키마를 사용하여 데이터 세트를 만들고 샘플 고객 충성도 데이터를 Adobe Experience Platform에 업로드합니다.

   >[!NOTE]
   >
   >Postman 컬렉션 실행기 중에 컬렉션 요청이 실패한 경우 실행을 중지하고 컬렉션 요청을 하나씩 실행합니다.

1. 모든 것이 잘 진행되면 `Luma-Loyalty-Data` 컬렉션이 전달됩니다.

   ![충성도 결과](../assets/data-generator/images/loyalty-result.png)

1. 이제 다음으로 로그인하겠습니다. [Adobe Experience Platform 인터페이스](https://platform.adobe.com/) 데이터 세트로 이동합니다.
1. 를 엽니다. `Luma Loyalty Dataset` 데이터 세트 및 데이터 세트 활동 창에서 1,000개의 레코드를 수집한 성공적인 배치 실행을 볼 수 있습니다. 데이터 세트 미리 보기 옵션을 클릭하여 수집된 레코드를 확인할 수도 있습니다. 1000을 확인하려면 몇 분 정도 기다려야 할 수 있습니다 [!UICONTROL 새 프로필 조각] 이(가) 만들어졌습니다.
   ![충성도 데이터 세트](../assets/data-generator/images/loyalty-dataset.png)
1. 1-3단계를 반복하여 다른 컬렉션을 실행합니다.
   * `2-Luma-CRM-Data.postman_collection.json` 는 고객의 CRM 데이터에 대한 스키마 및 채워진 데이터 세트를 만듭니다. 스키마는 인구 통계 세부 정보, 개인 연락처 세부 정보, 환경 설정 세부 정보 및 사용자 지정 ID 필드 그룹을 구성하는 XDM 개인 프로필 클래스를 기반으로 합니다.
   * `3-Luma-Product-Catalog.postman_collection.json` 는 제품 카탈로그 정보에 대한 스키마 및 채워진 데이터 세트를 만듭니다. 스키마는 사용자 정의 제품 카탈로그 클래스를 기반으로 하며 사용자 정의 제품 카탈로그 필드 그룹을 사용합니다.
   * `4-Luma-Offline-Purchase-Events.postman_collection.json` 는 고객의 오프라인 구매 이벤트 데이터에 대한 스키마와 채워진 데이터 세트를 만듭니다. 스키마는 XDM ExperienceEvent 클래스를 기반으로 하며 사용자 지정 ID 및 상거래 세부 사항 필드 그룹으로 구성됩니다.
   * `5-Luma-Product-Inventory-Events.postman_collection.json` 시작 및 종료 제품과 관련된 이벤트에 대한 스키마 및 채워진 데이터 세트를 만듭니다. 스키마는 사용자 정의 비즈니스 이벤트 클래스 및 사용자 정의 필드 그룹을 기반으로 합니다.
   * `6-Luma-Test-Profiles.postman_collection.json` Adobe Journey Optimizer에서 사용할 스키마 및 테스트 프로필로 채워진 데이터 세트 만들기
   * `7-Luma-Web-Events.postman_collection.json` 는 간단한 내역 웹 데이터로 스키마와 채워진 데이터 세트를 만듭니다.


## 유효성 검사

샘플 데이터는 컬렉션이 실행될 때 여러 시스템의 데이터를 결합하는 실시간 고객 프로필을 빌드하도록 설계되었습니다. 충성도, CRM 및 오프라인 구매 데이터 세트의 첫 번째 기록이 좋은 예입니다. 해당 프로필을 조회하여 데이터가 수집되었는지 확인합니다. 다음에서 [Adobe Experience Platform 인터페이스](https://experience.adobe.com/platform/):

1. 다음으로 이동 **[!UICONTROL 프로필]** > **[!UICONTROL 찾아보기]**
1. 선택 `Luma Loyalty Id` (으)로 **[!UICONTROL ID 네임스페이스]**
1. 검색 대상 `5625458` (으)로 **[!UICONTROL ID 값]**
1. 를 엽니다. `Daniel Wright` 프로필

>[!TIP]
>
>프로필이 표시되지 않으면 다음을 확인하십시오. [!UICONTROL 데이터 세트] 모든 데이터 세트가 성공적으로 생성되고 수집되었는지 확인하는 페이지입니다. 정상적으로 보이는 경우 15분 동안 기다렸다가 뷰어에서 프로필이 사용 가능한지 확인하십시오.  데이터 수집에 문제가 있는 경우 오류 메시지를 확인하여 문제를 찾으십시오. 또한에 대한 오류 진단을 활성화할 수 있습니다. [!UICONTROL 데이터 세트] json 데이터 파일을 페이지에 넣고 드래그 앤 드롭하여 데이터를 다시 수집합니다.


![프로필 열기](../assets/data-generator/images/validation-profile-open.png)

에서 데이터를 검색하여 **[!UICONTROL 속성]** 및 **[!UICONTROL 이벤트]** 탭에서는 프로필에 다양한 데이터 파일의 데이터가 포함되어 있음을 확인해야 합니다.
![오프라인 구매 이벤트 파일의 이벤트 데이터](../assets/data-generator/images/validation-profile-events.png)

## 다음 단계

Adobe Journey Optimizer에 대해 알아보려면 이 샌드박스에는 [Journey Optimizer 과제](https://experienceleague.adobe.com/docs/journey-optimizer-learn/challenges/introduction-and-prerequisites.html?lang=ko)

병합 정책, 데이터 거버넌스, 쿼리 서비스 및 세그먼트 빌더에 대해 알아보려면 로 이동하십시오. [데이터 설계자 및 데이터 엔지니어를 위한 시작하기 자습서의 11단원](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/create-merge-policies.html?lang=en). 이 다른 자습서의 이전 단원을 통해 이러한 Postman 컬렉션에서 방금 채운 모든 항목을 수동으로 빌드할 수 있습니다. 바로 시작할 수 있습니다.

이 샌드박스에 연결되는 샘플 웹 SDK 구현을 빌드하려면 다음을 수행하십시오.
[Web SDK 튜토리얼을 사용하여 Adobe Experience Cloud 구현](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=ko-KR). 웹 SDK 자습서의 &quot;초기 구성&quot;, &quot;태그 구성&quot; 및 &quot;Experience Platform 설정&quot; 단원을 설정한 후에 의 처음 10개 이메일 주소를 사용하여 Luma 웹 사이트에 로그인합니다. `luma-crm.json` 암호를 사용하는 파일 `test` 이 자습서에서 업로드한 데이터와 프로필 조각을 병합하는 방법을 살펴봅니다.

이 샌드박스에 연결되는 샘플 Mobile SDK 구현을 빌드하려면 다음을 수행하십시오.
[모바일 앱에서 Adobe Experience Cloud 구현 자습서](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html?lang=ko). 웹 SDK 자습서의 &quot;초기 구성&quot;, &quot;앱 구현&quot; 및 &quot;Experience Platform&quot; 단원을 설정한 후에 의 첫 번째 이메일 주소를 사용하여 Luma 웹 사이트에 로그인합니다. `luma-crm.json` 이 자습서에서 업로드한 데이터와 프로필 조각을 병합하는 방법을 볼 수 있는 파일입니다.

## 샌드박스 환경 재설정 {#reset-sandbox}

비프로덕션 샌드박스를 재설정하면 샌드박스의 이름과 관련 권한을 유지하면서 해당 샌드박스(스키마, 데이터 세트 등)와 관련된 모든 리소스가 삭제됩니다. 이 &quot;클린&quot; 샌드박스는 액세스 권한이 있는 사용자가 동일한 이름으로 계속 사용할 수 있습니다.

다음 단계 [여기](https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html?lang=en#reset-a-sandbox) 샌드박스 환경을 재설정합니다.
