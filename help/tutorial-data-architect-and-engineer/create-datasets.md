---
title: 데이터 세트 만들기
seo-title: Create datasets | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 데이터 세트 만들기
description: 이 단원에서는 데이터를 수신할 데이터 세트를 만듭니다.
role: Data Architect, Data Engineer
feature: Data Management
kt: 4348
thumbnail: 4348-create-datasets.jpg
exl-id: 80227af7-4976-4fd2-b1d4-b26bc4626fa0
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 8%

---

# 데이터 세트 만들기

<!--15min-->

이 단원에서는 데이터를 수신할 데이터 세트를 만듭니다. 자습서에서 이것이 가장 짧은 수업이라는 것을 알게 되면 흥분될 것입니다!

Adobe Experience Platform에 성공적으로 수집된 모든 데이터는 데이터 세트로 데이터 레이크에서 유지됩니다. 데이터 세트는 스키마(열) 및 필드(행)를 포함하는 데이터 수집을 위한 저장소 및 관리 구조입니다. 데이터 세트에는 저장하는 데이터의 다양한 측면을 설명하는 메타데이터도 포함됩니다.

**데이터 설계자** 은 이 자습서를 제외하고 데이터 세트를 만들어야 합니다.

연습을 시작하기 전에 이 짧은 비디오에서 데이터 세트에 대해 자세히 알아보십시오.
>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)

## 필요한 권한

에서 [권한 구성](configure-permissions.md) 이 단원을 완료하는 데 필요한 모든 액세스 컨트롤을 설정합니다.

<!--
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## UI에서 데이터 세트 만들기

이 연습에서는 UI에 데이터 세트를 만듭니다. 충성도 데이터로 시작합니다.

1. 이동 **[!UICONTROL 데이터 세트]** 플랫폼 사용자 인터페이스의 왼쪽 탐색
1. 을(를) 선택합니다 **[!UICONTROL 데이터 집합 만들기]** 버튼
   ![데이터 집합 만들기](assets/datasets-createDataset.png)

1. 다음 화면에서 을 선택합니다. **스키마에서 데이터 집합 만들기**
1. 다음 화면에서 `Luma Loyalty Schema` 그런 다음 **[!UICONTROL 다음]** 버튼
   ![데이터 세트를 선택합니다](assets/datasets-selectSchema.png)

1. 데이터 세트에 이름을 지정합니다 `Luma Loyalty Dataset` 을(를) 선택하고 을(를) 선택합니다. **[!UICONTROL 완료]** 버튼
   ![데이터 세트에 이름을 지정합니다](assets/datasets-nameDataset.png)
1. 데이터 세트가 저장되면 다음과 같은 화면으로 이동합니다.
   ![생성된 데이터 세트](assets/datasets-created.png)

됐습니다. 빨리 할 거라고 했잖아요 동일한 단계를 사용하여 이러한 다른 데이터 세트를 만듭니다.

1. `Luma Offline Purchase Events Dataset` 에 대해 `Luma Offline Purchase Events Schema`
1. `Luma Web Events Dataset` 에 대해 `Luma Web Events Schema`
1. `Luma Product Catalog Dataset` 에 대해 `Luma Product Catalog Schema`


## API를 사용하여 데이터 세트 만들기

이제 을(를) 만듭니다 `Luma CRM Dataset` api 사용.

>[!NOTE]
>
>API 연습을 건너뛰고 를 만들려면 `Luma CRM Dataset` 사용자 인터페이스에 표시됩니다. 이름을 지정합니다 `Luma CRM Dataset` 그리고 `Luma CRM Schema`.

### 데이터 집합에 사용할 스키마의 ID 가져오기

먼저 `$id` 의 `Luma CRM Schema`:

1. 열기 [!DNL Postman]
1. 지난 24시간 동안 요청을 하지 않은 경우 인증 토큰이 만료되었을 수 있습니다. 요청을 엽니다. **[!DNL Adobe I/O Access Token Generation > Local Signing (Non-production use-only) > IMS: JWT Generate + Auth via User Token]** 을(를) 선택합니다. **보내기** 새 JWT 및 액세스 토큰을 요청하려면 [!DNL Postman] 단원.
1. 요청을 엽니다. **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]**
1. 을(를) 선택합니다 **보내기** 버튼
1. 200개의 응답이 있어야 합니다
1. 에 대한 응답을 찾습니다. `Luma CRM Schema` 항목 및 복사 `$id` value
   ![$id 복사](assets/dataset-crm-getSchemaId.png)

### 데이터 세트 만들기

이제 데이터 세트를 만들 수 있습니다.

1. 다운로드 [카탈로그 서비스 API.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Catalog%20Service%20API.postman_collection.json) 아래와 같이 `Luma Tutorial Assets` 폴더를 입력합니다.
1. 컬렉션 가져오기 [!DNL Postman]
1. 요청을 선택합니다 **[!DNL Catalog Service API > Datasets > Create a new dataset.]**
1. 다음 내용을 **본문** 요청해서 ***id 값을 고유한 로 바꾸기***:

   ```json
   {
       "name": "Luma CRM Dataset",
   
       "schemaRef": {
           "id": "REPLACE_WITH_YOUR_OWN_ID",
           "contentType": "application/vnd.adobe.xed-full+json;version=1"
       },
       "fileDescription": {
           "persisted": true,
           "containerFormat": "parquet",
           "format": "parquet"
       }
   }
   ```

1. 을(를) 선택합니다 **보내기** 버튼
1. 새 데이터 세트의 ID가 포함된 201 생성 응답이 있어야 합니다!
   ![API로 생성된 데이터 세트, 본문에 사용된 사용자 지정 $id](assets/datasets-crm-created.png)

>[!TIP]
>
> 이 요청을 수행하는 일반적인 문제 및 가능한 수정 사항:
>
> * `400: There was a problem retrieving xdm schema` 질문에 답합니다. 위의 샘플에서 ID를 고유한 ID로 대체했는지 확인하십시오 `Luma CRM Schema`
> * 인증 토큰이 없습니다. 를 실행합니다. **IMS: 사용자 토큰을 통한 JWT 생성 + 인증** 새 토큰을 생성하기 위해 호출
> * `401: Not Authorized to PUT/POST/PATCH/DELETE for this path : /global/schemas/`: 업데이트 **CONTAINER_ID** 환경 변수 `global` to `tenant`
> * `403: PALM Access Denied. POST access is denied for this resource from access control`: Admin Console에서 사용자 권한 확인



로 돌아갈 수 있습니다. **[!UICONTROL 데이터 세트]** 플랫폼 사용자 인터페이스의 화면에서 5개의 데이터 세트를 모두 성공적으로 만들 수 있습니다.
![데이터 세트 5개 완료](assets/datasets-allComplete.png)


## 추가 리소스

* [데이터 세트 설명서](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=ko)
* [데이터 세트 API(카탈로그 서비스의 일부) 참조](https://www.adobe.io/experience-platform-apis/references/catalog/#tag/Datasets)

모든 스키마, ID 및 데이터 세트가 준비되었으므로 [실시간 고객 프로필에 대해 활성화](enable-profiles.md).
