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
source-git-commit: 0b13a4fa625cd29cc98c319b81fcb2a278b7b19a
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 9%

---

# 데이터 세트 만들기

<!--15min-->

이 단원에서는 데이터를 수신할 데이터 세트를 만듭니다. 이 자습서에서 가장 짧은 단원이 되는 것을 알게 되면 매우 기쁩니다!

Adobe Experience Platform에 성공적으로 수집된 모든 데이터는 데이터 세트로 데이터 레이크에 유지됩니다. 데이터 세트는 스키마(열) 및 필드(행)를 포함하는 데이터 수집을 위한 저장소 및 관리 구조입니다. 데이터 세트에는 저장하는 데이터의 다양한 측면을 설명하는 메타데이터도 포함됩니다.

**데이터 설계자** 은(는) 이 자습서 외부에 데이터 세트를 만들어야 합니다.

연습을 시작하기 전에 이 짧은 비디오를 통해 데이터 세트에 대해 자세히 알아보십시오.
>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)

## 권한 필요

다음에서 [권한 구성](configure-permissions.md) 단원, 이 단원을 완료하는 데 필요한 모든 액세스 제어를 설정합니다.

<!--
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## UI에서 데이터 세트 만들기

이 연습에서는 UI에 데이터 세트를 만듭니다. 충성도 데이터로 시작하겠습니다.

1. 다음으로 이동 **[!UICONTROL 데이터 세트]** Platform 사용자 인터페이스의 왼쪽 탐색
1. 다음 항목 선택 **[!UICONTROL 데이터 세트 만들기]** 단추
   ![데이터 세트 만들기](assets/datasets-createDataset.png)

1. 다음 화면에서 다음을 선택합니다. **스키마에서 데이터 세트 만들기**
1. 다음 화면에서 다음을 선택합니다 `Luma Loyalty Schema` 을(를) 선택한 다음 **[!UICONTROL 다음]** 단추
   ![데이터 세트 선택](assets/datasets-selectSchema.png)

1. 데이터 세트 이름 지정 `Luma Loyalty Dataset` 및 선택 **[!UICONTROL 완료]** 단추
   ![데이터 세트 이름 지정](assets/datasets-nameDataset.png)
1. 데이터 세트가 저장되면 다음과 같은 화면으로 이동합니다.
   ![데이터 세트 생성됨](assets/datasets-created.png)

됐습니다. 금방 될 거라고 했잖아 동일한 단계를 사용하여 이러한 다른 데이터 세트를 만듭니다.

1. `Luma Offline Purchase Events Dataset` 에 대한 `Luma Offline Purchase Events Schema`
1. `Luma Web Events Dataset` 에 대한 `Luma Web Events Schema`
1. `Luma Product Catalog Dataset` 에 대한 `Luma Product Catalog Schema`


## API를 사용하여 데이터 세트 만들기

이제 다음을 만듭니다. `Luma CRM Dataset` api 사용.

>[!NOTE]
>
>API 연습을 건너뛰고 다음을 만들려면 `Luma CRM Dataset` 사용자 인터페이스에서도 괜찮습니다. 이름 지정 `Luma CRM Dataset` 및 사용 `Luma CRM Schema`.

### 데이터 세트에 사용할 스키마 ID 가져오기

먼저 다음을 얻어야 합니다 `$id` / `Luma CRM Schema`:

1. 열기 [!DNL Postman]
1. 액세스 토큰이 없는 경우 요청을 엽니다 **[!DNL OAuth: Request Access Token]** 및 선택 **보내기** 에서 수행한 것과 같은 방식으로 새 액세스 토큰을 요청합니다. [!DNL Postman] 레슨.
1. 요청 열기 **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]**
1. 다음 항목 선택 **보내기** 단추
1. 200개의 응답을 받아야 합니다.
1. 다음에 대한 응답을 찾습니다. `Luma CRM Schema` 항목 및 복사 `$id` 값
   ![$id 복사](assets/dataset-crm-getSchemaId.png)

### 데이터 세트 만들기

이제 데이터 세트를 만들 수 있습니다.

1. 다운로드 [카탈로그 서비스 API.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Catalog%20Service%20API.postman_collection.json) (으)로 `Luma Tutorial Assets` 폴더를 삭제합니다.
1. 컬렉션 가져오기 [!DNL Postman]
1. 요청 선택 **[!DNL Catalog Service API > Datasets > Create a new dataset.]**
1. 다음을 로 붙여넣기 **본문** 요청 중, ***id 값을 자신의 id 값으로 바꾸기***:

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

1. 다음 항목 선택 **보내기** 단추
1. 새 데이터 세트의 ID가 포함된 201 Created 응답을 가져와야 합니다!
   ![본문에 사용된 사용자 정의 $id인 API로 만들어진 데이터 세트](assets/datasets-crm-created.png)

>[!TIP]
>
> 이 요청을 하는 일반적인 문제 및 수정 가능성:
>
> * `400: There was a problem retrieving xdm schema` 질문에 답합니다. 위 샘플의 id를 자신의 id로 교체한 적이 있는지 확인합니다 `Luma CRM Schema`
> * 인증 토큰 없음: 다음을 실행합니다 **OAuth: 액세스 토큰 요청** 새 토큰 생성 요청
> * `401: Not Authorized to PUT/POST/PATCH/DELETE for this path : /global/schemas/`: 를 업데이트합니다 **CONTAINER_ID** 의 환경 변수 `global` 끝 `tenant`
> * `403: PALM Access Denied. POST access is denied for this resource from access control`: Admin Console에서 사용자 권한 확인


다음으로 돌아갈 수 있습니다. **[!UICONTROL 데이터 세트]** platform 사용자 인터페이스의 화면에서 5개의 데이터 세트가 모두 성공적으로 생성되었는지 확인할 수 있습니다.
![5개 데이터 세트 완료](assets/datasets-allComplete.png)


## 추가 리소스

* [데이터 세트 설명서](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=ko)
* [데이터 세트 API(카탈로그 서비스의 일부) 참조](https://www.adobe.io/experience-platform-apis/references/catalog/#tag/Datasets)

이제 모든 스키마, ID 및 데이터 세트가 준비되었으므로 [실시간 고객 프로필에 대해 활성화](enable-profiles.md).
