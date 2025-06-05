---
title: 일괄 처리 데이터 수집
seo-title: Ingest batch data | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 일괄 처리 데이터 수집
description: 이 단원에서는 다양한 방법을 사용하여 배치 데이터를 Experience Platform에 수집합니다.
role: Data Engineer
feature: Data Ingestion
jira: KT-4348
thumbnail: 4348-ingest-batch-data.jpg
exl-id: fc7db637-e191-4cc7-9eec-29f4922ae127
source-git-commit: d73f9b3eafb327783d6bfacaf4d57cf8881479f7
workflow-type: tm+mt
source-wordcount: '2446'
ht-degree: 0%

---

# 일괄 처리 데이터 수집

<!-- 1hr-->
이 단원에서는 다양한 방법을 사용하여 배치 데이터를 Experience Platform에 수집합니다.

일괄 데이터 수집을 사용하면 한 번에 많은 양의 데이터를 Adobe Experience Platform으로 수집할 수 있습니다. Platform의 인터페이스 내에서 또는 API를 사용하여 일괄 데이터를 한 번에 업로드할 수 있습니다. Source 커넥터를 사용하여 클라우드 스토리지 서비스와 같은 서드파티 서비스에서 정기적으로 예약된 일괄 업로드를 구성할 수도 있습니다.

**데이터 엔지니어**&#x200B;는 이 자습서 외부에서 일괄 데이터를 수집해야 합니다.

연습을 시작하기 전에 이 짧은 비디오를 시청하여 데이터 수집에 대해 자세히 알아보십시오.

>[!VIDEO](https://video.tv.adobe.com/v/27106?learn=on&enablevpops)


## 권한 필요

[권한 구성](configure-permissions.md) 단원에서 이 단원을 완료하는 데 필요한 모든 액세스 제어를 설정합니다.

<!--
* Permission item **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]**, **[!UICONTROL Manage Datasets]** and **[!UICONTROL Data Monitoring]**
* Permission items **[!UICONTROL Data Ingestion]** > **[!UICONTROL View Sources]** and **[!UICONTROL Manage Sources]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

소스 연습을 수행하려면 (S)FTP 서버 또는 클라우드 스토리지 솔루션에 액세스해야 합니다. 없는 경우 해결 방법이 있습니다.

## Platform 사용자 인터페이스를 사용하여 데이터 배치 수집

데이터는 JSON 및 Parquet 형식으로 데이터 세트 화면의 데이터 세트에 직접 업로드할 수 있습니다. 이는 을(를) 만든 후 일부 데이터의 수집을 테스트하는 좋은 방법입니다

### 데이터 다운로드 및 준비

먼저 샘플 데이터를 가져와 테넌트에 맞게 사용자 지정합니다.

>[!NOTE]
>
>[luma-data.zip](assets/luma-data.zip) 파일에 포함된 데이터는 가상 데이터이며 데모용으로만 사용됩니다.

1. **Luma 튜토리얼 Assets** 폴더에 [luma-data.zip](assets/luma-data.zip)을(를) 다운로드합니다.
1. 파일의 압축을 풀고 이 단원에서 사용할 4개의 데이터 파일이 포함된 `luma-data` 폴더를 만듭니다.
1. 텍스트 편집기에서 `luma-loyalty.json`을(를) 열고 `_techmarketingdemos`의 모든 인스턴스를 고유한 스키마에 표시된 대로 고유한 밑줄 테넌트 ID로 바꿉니다.
   ![밑줄 테넌트 ID](assets/ingestion-underscoreTenant.png)

1. 업데이트된 파일 저장

### 데이터 수집

1. Platform 사용자 인터페이스의 왼쪽 탐색에서 **[!UICONTROL 데이터 세트]**&#x200B;를 선택합니다
1. `Luma Loyalty Dataset` 열기
1. 오른쪽 열에 **[!UICONTROL 데이터 추가]** 섹션이 표시될 때까지 아래로 스크롤합니다.
1. `luma-loyalty.json` 파일을 업로드합니다.
1. 파일이 업로드되면 배치에 대한 행이 나타납니다
1. 몇 분 후 페이지를 다시 로드하면 1000개의 레코드와 1000개의 프로필 조각과 함께 배치가 성공적으로 업로드된 것을 볼 수 있습니다.

   ![수집](assets/ingestion-loyalty-uploadJson.png)
   <!--do i need to explain error diagnostics and partial ingestion-->

>[!NOTE]
>
>이 단원의 다양한 화면에서 볼 수 있는 몇 가지 옵션인 **[!UICONTROL 오류 진단]** 및 **[!UICONTROL 부분 수집]**&#x200B;이 있습니다. 이러한 옵션은 자습서에서 다루지 않습니다. 몇 가지 빠른 정보:
>
>* 오류 진단을 활성화하면 데이터 수집에 대한 데이터가 생성되고 이 데이터는 Data Access API를 사용하여 검토할 수 있습니다. 자세한 내용은 [설명서](https://experienceleague.adobe.com/docs/experience-platform/data-access/home.html)를 참조하세요.
>* 부분 수집을 사용하면 지정 가능한 특정 임계값까지, 오류가 포함된 데이터를 수집할 수 있습니다. 자세한 내용은 [설명서](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/partial.html)를 참조하세요.

### 데이터 유효성 검사

데이터가 성공적으로 수집되었는지 확인하는 방법에는 몇 가지가 있습니다.

#### Platform 사용자 인터페이스에서 유효성 검사

데이터가 데이터 세트에 수집되었는지 확인하려면:

1. 데이터를 수집한 페이지에서 오른쪽 상단의 **[!UICONTROL 데이터 집합 미리 보기]** 단추를 선택합니다.
1. **미리 보기** 단추를 선택하면 수집된 데이터 중 일부를 볼 수 있습니다.

   ![성공한 데이터 집합 미리 보기](assets/ingestion-loyalty-preview.png)


데이터가 프로필에 도달했는지 확인하려면(데이터가 도착하는 데 몇 분 정도 걸릴 수 있음):

1. 왼쪽 탐색에서 **[!UICONTROL 프로필]**(으)로 이동
1. **[!UICONTROL ID 네임스페이스 선택]** 필드 옆의 아이콘을 선택하여 모달을 엽니다.
1. `Luma Loyalty Id` 네임스페이스 선택
1. 그런 다음 데이터 집합 `5625458`에서 `loyaltyId` 값 중 하나를 입력하십시오.
1. **[!UICONTROL 보기]** 선택
   ![데이터 집합에서 프로필 확인](assets/ingestion-loyalty-profile.png)

#### 데이터 수집 이벤트로 유효성 검사

이전 단원에서 데이터 수집 이벤트를 구독한 경우 고유한 webhook.site URL을 확인합니다. 세 개의 요청이 다음 순서로 표시되고 그 사이에 시간이 좀 걸리며 다음 `eventCode` 값이 표시됩니다.

1. `ing_load_success`—수집된 일괄 처리
1. `ig_load_success` - 배치가 id 그래프로 수집되었습니다.
1. `ps_load_success` - 배치가 프로필 서비스에 수집되었습니다.

![데이터 수집 Webhook](assets/ingestion-loyalty-webhook.png)

알림에 대한 자세한 내용은 [설명서](https://experienceleague.adobe.com/docs/experience-platform/ingestion/quality/subscribe-events.html#available-status-notification-events)를 참조하세요.

## Platform API를 사용하여 데이터 배치 수집

이제 API를 사용하여 데이터를 업로드하겠습니다.

>[!NOTE]
>
>데이터 설계자는 사용자 인터페이스 메서드를 통해 CRM 데이터를 자유롭게 업로드할 수 있습니다.

### 데이터 다운로드 및 준비

1. `Luma Tutorial Assets` 폴더에 [luma-data.zip](assets/luma-data.zip)을(를) 이미 다운로드하고 압축 해제했어야 합니다.
2. 텍스트 편집기에서 `luma-crm.json`을(를) 열고 스키마에 표시된 대로 `_techmarketingdemos`의 모든 인스턴스를 고유한 밑줄 테넌트 ID로 바꾸십시오.
3. 업데이트된 파일 저장

### 데이터 세트 ID 가져오기

먼저 데이터를 수집할 데이터 세트의 데이터 세트 ID를 가져옵니다.

1. [!DNL Postman] 열기
1. 액세스 토큰이 없는 경우 [!DNL Postman] 단원에서 수행한 것처럼 **[!DNL OAuth: Request Access Token]** 요청을 열고 **보내기**&#x200B;를 선택하여 새 액세스 토큰을 요청합니다.
1. 환경 변수를 열고 **CONTAINER_ID**&#x200B;의 값이 여전히 `tenant`인지 확인하십시오
1. **[!DNL Catalog Service API > Datasets > Retrieve a list of datasets.]** 요청을 열고 **보내기**&#x200B;를 선택합니다.
1. `200 OK` 응답을 받아야 합니다.
1. 응답 본문에서 `Luma CRM Dataset`의 ID 복사
   ![데이터 세트 ID 가져오기](assets/ingestion-crm-getDatasetId.png)

### 일괄 처리 만들기

이제 데이터 세트에 일괄 처리를 만들 수 있습니다.

1. `Luma Tutorial Assets` 폴더에 [데이터 수집 API.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Data%20Ingestion%20API.postman_collection.json) 다운로드
1. 컬렉션을 [!DNL Postman]&#x200B;(으)로 가져오기
1. **[!DNL Data Ingestion API > Batch Ingestion > Create a new batch in Catalog Service.]** 요청 선택
1. 다음을 요청의 **본문**(으)로 붙여 넣습니다. ***datasetId 값을 자신의 값으로 바꾸기***:

   ```json
   {
       "datasetId":"REPLACE_WITH_YOUR_OWN_DATASETID",
       "inputFormat": {
           "format": "json"
       }
   }
   ```

1. **보내기** 단추 선택
1. 새 일괄 처리의 ID가 포함된 201 Created 응답을 가져와야 합니다!
1. 새 일괄 처리의 `id` 복사
   ![일괄 처리 생성됨](assets/ingestion-crm-createBatch.png)

### 데이터 수집

이제 데이터를 배치에 업로드할 수 있습니다.

1. **[!DNL Data Ingestion API > Batch Ingestion > Upload a file to a dataset in a batch.]** 요청 선택
1. **매개 변수** 탭에서 각 필드에 데이터 세트 ID와 배치 ID를 입력합니다
1. **매개 변수** 탭에서 **filePath**(으)로 `luma-crm.json`을(를) 입력하십시오.
1. **본문** 탭에서 **이진** 옵션을 선택합니다.
1. 로컬 `Luma Tutorial Assets` 폴더에서 다운로드한 `luma-crm.json` 선택
1. **보내기**&#x200B;를 선택하면 응답 본문에 &#39;1&#39;이 있는 200 OK 응답을 받게 됩니다.

   ![데이터 업로드됨](assets/ingestion-crm-uploadFile.png)

이때 Platform 사용자 인터페이스에서 일괄 처리를 보면 일괄 처리가 &quot;[!UICONTROL 로드 중]&quot; 상태임을 알 수 있습니다.
![일괄 로드](assets/ingestion-crm-loading.png)

일괄 처리 API는 여러 파일을 업로드하는 데 자주 사용되므로 일괄 처리가 완료되면 플랫폼에게 알려 주어야 합니다. 이 작업은 다음 단계에서 수행합니다.

### 일괄 처리 완료

배치를 완료하려면

1. **[!DNL Data Ingestion API > Batch Ingestion > Finish uploading a file to a dataset in a batch.]** 요청 선택
1. **매개 변수** 탭에서 **작업**(으)로 `COMPLETE`을(를) 입력하십시오.
1. **매개 변수** 탭에서 배치 ID를 입력합니다. 데이터 세트 ID 또는 filePath가 있는 경우 걱정하지 마십시오.
1. 게시물의 URL이 `https://platform.adobe.io/data/foundation/import/batches/:batchId?action=COMPLETE`이고 `datasetId` 또는 `filePath`에 대한 불필요한 참조가 없는지 확인하십시오
1. **보내기**&#x200B;를 선택하면 응답 본문에 &#39;1&#39;이 있는 200 OK 응답을 받게 됩니다.

   ![일괄 처리 완료](assets/ingestion-crm-complete.png)

### 데이터 유효성 검사

#### Platform 사용자 인터페이스에서 유효성 검사

충성도 데이터 세트에 대해 수행한 것처럼 데이터가 Platform 사용자 인터페이스에 포함되었는지 확인합니다.

먼저, 배치가 1000개의 레코드가 수집되었음을 확인합니다.

![일괄 처리 성공](assets/ingestion-crm-success.png)

그런 다음 미리 보기 데이터 세트를 사용하여 일괄 처리를 확인합니다.

![일괄 처리 미리 보기](assets/ingestion-crm-preview.png)

마지막으로, `Luma CRM Id` 네임스페이스(예: `b642b4217b34b1e8d3bd915fc65c4452`)별로 프로필 중 하나를 조회하여 프로필 중 하나가 생성되었는지 확인합니다

![수집된 프로필](assets/ingestion-crm-profile.png)

방금 일어났던 한 가지 흥미로운 사실을 지적하고 싶다. `Danny Wright` 프로필을 엽니다. 프로필에 `Lumacrmid`과(와) `Lumaloyaltyid`이(가) 모두 있습니다. `Luma Loyalty Schema`에 Luma 충성도 ID와 CRM ID라는 두 개의 ID 필드가 포함되어 있음을 기억하십시오. 이제 두 데이터 세트를 모두 업로드했으므로 하나의 프로필로 병합되었습니다. 충성도 데이터의 이름은 `Daniel`이고 홈 주소는 &quot;New York City&quot;이며 CRM 데이터의 이름은 `Danny`이고 충성도 ID가 동일한 고객의 홈 주소는 `Portland`입니다. 병합 정책에 대한 단원에서 이름이 `Danny`을(를) 표시하는 이유를 다시 살펴봅니다.

축하합니다. 방금 프로필을 병합했습니다!

![병합된 프로필 ](assets/ingestion-crm-profileLinkedIdentities.png)

#### 데이터 수집 이벤트로 유효성 검사

이전 단원에서 데이터 수집 이벤트를 구독한 경우 고유한 webhook.site URL을 확인합니다. 충성도 데이터와 마찬가지로 다음 세 가지 요청이 들어오는 것을 볼 수 있습니다.

![데이터 수집 Webhook](assets/ingestion-crm-webhook.png)

알림에 대한 자세한 내용은 [설명서](https://experienceleague.adobe.com/docs/experience-platform/ingestion/quality/subscribe-events.html#available-status-notification-events)를 참조하세요.

## 워크플로우를 사용하여 데이터 수집

데이터를 업로드하는 다른 방법에 대해 살펴보겠습니다. 워크플로우 기능을 사용하면 XDM에서 아직 모델링되지 않은 CSV 데이터를 수집할 수 있습니다.

### 데이터 다운로드 및 준비

1. `Luma Tutorial Assets` 폴더에 [luma-data.zip](assets/luma-data.zip)을(를) 이미 다운로드하고 압축 해제했어야 합니다.
1. `luma-products.csv`이(가) 있는지 확인

### 워크플로 만들기

이제 워크플로우를 설정하겠습니다.

1. 왼쪽 탐색에서 **[!UICONTROL 워크플로]**(으)로 이동
1. **[!UICONTROL XDM 스키마에 CSV 매핑]**&#x200B;을 선택하고 **[!UICONTROL 시작]** 단추를 선택합니다.
   ![워크플로우 시작](assets/ingestion-products-launchWorkflow.png)
1. `Luma Product Catalog Dataset`을(를) 선택하고 **[!UICONTROL 다음]** 단추를 선택하세요.
   ![데이터 세트 선택](assets/ingestion-products-selectDataset.png)
1. 다운로드한 `luma-products.csv` 파일을 추가하고 **[!UICONTROL 다음]** 단추를 선택합니다.
   ![데이터 세트 선택](assets/ingestion-products-selectData.png)
1. 이제 소스 데이터(`luma-products.csv` 파일의 열 이름 중 하나)의 필드를 대상 스키마의 XDM 필드에 매핑할 수 있는 매퍼 인터페이스에 있습니다. 이 예제에서 열 이름은 매퍼가 올바른 매핑을 자동으로 감지할 수 있을 만큼 스키마 필드 이름에 가깝습니다. 매퍼가 오른쪽 필드를 자동 감지할 수 없는 경우 대상 필드 오른쪽에 있는 아이콘을 선택하여 올바른 XDM 필드를 선택합니다. 또한 CSV에서 열 중 하나를 수집하지 않으려는 경우 매퍼에서 행을 삭제할 수 있습니다. 매퍼의 작동 방식을 이해하려면 자유롭게 재생하고 `luma-products.csv`의 열 머리글을 변경하십시오.
1. **[!UICONTROL 완료]** 단추 선택
   ![데이터 세트 선택](assets/ingestion-products-mapper.png)

### 데이터 유효성 검사

배치가 업로드되면 데이터 세트를 미리 보고 업로드를 확인합니다.

`Luma Product SKU`은(는) 비사용자 네임스페이스이므로 제품 sku에 대한 프로필이 표시되지 않습니다.

웹후크에 대한 세 개의 히트를 볼 수 있습니다.

## 소스를 사용하여 데이터 수집

그래, 넌 힘든 일을 했어. 이제 _자동화된_ 일괄 처리 수집이 약속된 땅으로 이동해 보겠습니다! 내가 &quot;설정해!&quot; 라고 하면 &quot;잊어 버려!&quot; &quot;설정해!&quot; &quot;됐어!&quot; &quot;설정해!&quot; &quot;됐어!&quot; 농담이야, 넌 절대 그런 짓 안 할 거야! 좋아, 일하러 가 거의 다 됐어

소스 카탈로그를 열려면 왼쪽 탐색에서 **[!UICONTROL 소스]**(으)로 이동하십시오. 업계 최고의 데이터 및 스토리지 공급업체와의 다양한 기본 통합을 살펴볼 수 있습니다.

![Source 카탈로그](assets/ingestion-offline-sourceCatalog.png)

좋습니다. 소스 커넥터를 사용하여 데이터를 수집하겠습니다.

이 연습은 나만의 모험 스타일로 할 것입니다. FTP 소스 커넥터를 사용하는 워크플로우를 표시하려고 합니다. 회사에서 사용하는 다른 클라우드 스토리지 소스 커넥터를 사용하거나 충성도 데이터를 사용한 것과 같은 데이터 세트 사용자 인터페이스를 사용하여 json 파일을 업로드할 수 있습니다.

대부분의 소스에는 다음과 같은 유사한 구성 워크플로가 있습니다.

1. 인증 세부 정보 입력
1. 수집할 데이터 선택
1. 수집할 Platform 데이터 세트를 선택합니다
1. 필드를 XDM 스키마에 매핑
1. 해당 위치에서 데이터를 수집할 빈도를 선택합니다

>[!NOTE]
>
>이 연습에서 사용할 오프라인 구매 데이터에는 날짜/시간 데이터가 포함되어 있습니다. 날짜/시간 데이터는 [ISO 8061 형식의 문자열](https://www.iso.org/iso-8601-date-and-time-format.html)&#x200B;(&quot;2018-07-10T15:05:59.000-08:00&quot;) 또는 밀리초 형식의 Unix 시간(1531263959000)이어야 하며 수집 시간에 대상 XDM 유형으로 변환됩니다. 데이터 변환 및 기타 제약 조건에 대한 자세한 내용은 [일괄 처리 수집 API 설명서](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/api-overview.html#types)를 참조하십시오.

### 원하는 클라우드 스토리지 공급업체에 데이터 다운로드, 준비 및 업로드

1. `Luma Tutorial Assets` 폴더에 [luma-data.zip](assets/luma-data.zip)을(를) 이미 다운로드하고 압축 해제했어야 합니다.
1. 텍스트 편집기에서 `luma-offline-purchases.json`을(를) 열고 스키마에 표시된 대로 `_techmarketingdemos`의 모든 인스턴스를 고유한 밑줄 테넌트 ID로 바꾸십시오.
1. 이벤트가 지난 달에 발생하도록 모든 타임스탬프를 업데이트합니다(예: `"timestamp":"2022-06`을(를) 검색하고 연도 및 월을 대체).
1. 선호하는 클라우드 저장소 공급자를 선택하여 [!UICONTROL 원본] 카탈로그에서 사용할 수 있는지 확인하세요.
1. 선호하는 클라우드 저장소 공급자의 위치에 `luma-offline-purchases.json` 업로드

### 데이터를 원하는 클라우드 스토리지 위치로 수집

1. Platform 사용자 인터페이스에서 [!UICONTROL 소스] 카탈로그를 **[!UICONTROL 클라우드 저장소]**(으)로 필터링합니다.
1. `...` 아래에 설명서에 대한 편리한 링크가 있습니다.
1. 기본 클라우드 스토리지 공급업체의 상자에서 **[!UICONTROL 구성]** 단추를 선택합니다.
   ![구성 선택](assets/ingestion-offline-selectFTP.png)
1. **[!UICONTROL 인증]**&#x200B;이 첫 번째 단계입니다. 계정 이름(예: `Luma's FTP Account`)과 인증 세부 정보를 입력하십시오. 필드가 약간 다를 수 있지만 이 단계는 모든 클라우드 스토리지 소스의 경우와 상당히 유사해야 합니다. 계정에 대한 인증 세부 정보를 입력하면 동일한 계정의 다른 파일과 다른 일정에 따라 다른 데이터를 전송할 수 있는 다른 소스 연결에 이를 다시 사용할 수 있습니다
1. **[!UICONTROL 원본에 연결 단추]** 선택
1. 플랫폼이 Source에 연결되면 **[!UICONTROL 다음]** 단추를 선택합니다.
   ![소스에 인증](assets/ingestion-offline-authentication.png)

1. **[!UICONTROL 데이터 선택]** 단계에서 사용자 인터페이스는 자격 증명을 사용하여 클라우드 저장소 솔루션에서 폴더를 엽니다
1. 수집할 파일 선택(예: `luma-offline-purchases.json`)
1. **[!UICONTROL 데이터 형식]**(으)로 `XDM JSON`을(를) 선택합니다.
1. 그런 다음 JSON 구조 및 파일의 샘플 데이터를 미리 볼 수 있습니다
1. **[!UICONTROL 다음]** 단추 선택
   ![데이터 파일 선택](assets/ingestion-offline-selectData.png)

1. **[!UICONTROL 매핑]** 단계에서 `Luma Offline Purchase Events Dataset`을(를) 선택하고 **[!UICONTROL 다음]** 단추를 선택합니다. 수집하는 데이터가 JSON 파일이므로 소스 필드를 타겟 필드에 매핑하는 매핑 단계가 없다는 메시지에 주의하십시오. JSON 데이터는 이미 XDM에 있어야 합니다. CSV를 수집하는 경우 이 단계에서 전체 매핑 사용자 인터페이스가 표시됩니다.
   ![데이터 세트 선택](assets/ingestion-offline-mapping.png)
1. **[!UICONTROL 예약]** 단계에서는 Source에서 데이터를 수집할 빈도를 선택합니다. 잠시 옵션을 살펴보십시오. 일회성 수집만 수행하려 하므로 **[!UICONTROL 한 번]**&#x200B;에 **[!UICONTROL 빈도]**&#x200B;을(를) 두고 **[!UICONTROL 다음]** 단추를 선택하세요.
   ![데이터 흐름 예약](assets/ingestion-offline-scheduling.png)
1. **[!UICONTROL 데이터 흐름 세부 정보]** 단계에서 데이터 흐름의 이름을 선택하고, 선택적 설명을 입력하고, 오류 진단을 켜고, 부분 수집을 할 수 있습니다. 설정을 그대로 두고 **[!UICONTROL 다음]** 단추를 선택합니다.
   ![데이터 흐름의 세부 정보 편집](assets/ingestion-offline-detail.png)
1. **[!UICONTROL 검토]** 단계에서 모든 설정을 함께 검토하고 편집하거나 **[!UICONTROL 완료]** 단추를 선택할 수 있습니다
1. 저장한 후 다음과 같은 화면에 랜딩합니다.
   ![완료](assets/ingestion-offline-complete.png)

### 데이터 유효성 검사

배치가 업로드되면 데이터 세트를 미리 보고 업로드를 확인합니다.

웹후크에 대한 세 개의 히트를 볼 수 있습니다.

`loyaltyId` 네임스페이스에 값이 `5625458`인 프로필을 다시 검색하여 프로필에 구매 이벤트가 있는지 확인하십시오. 한 번 구매하시는 게 보일 겁니다. **[!UICONTROL JSON 보기]**&#x200B;를 선택하여 구매 세부 정보를 살펴볼 수 있습니다.

![프로필의 구매 이벤트](assets/ingestion-offline-eventInProfile.png)

## ETL 도구

Adobe은 여러 ETL 공급업체와 협력하여 Experience Platform으로의 데이터 수집을 지원합니다. 다양한 서드파티 공급업체로 인해 ETL은 이 자습서에서 다루지 않지만, 다음 리소스 중 일부를 검토할 수 있습니다.

* [Adobe Experience Platform을 위한 ETL 통합 개발](https://experienceleague.adobe.com/docs/experience-platform/etl/home.html)
* [[!DNL Snaplogic] Adobe Experience Platform 스냅 팩](https://www.snaplogic.com/resources/videos/august-2020-aep)

## 추가 리소스

* [일괄 처리 수집 설명서](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html)
* [일괄 처리 수집 API 참조](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)

이제 웹 SDK을 사용하여 데이터를 [스트리밍](ingest-streaming-data.md)하겠습니다.
