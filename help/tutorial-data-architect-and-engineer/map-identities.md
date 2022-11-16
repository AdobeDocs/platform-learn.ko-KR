---
title: ID 매핑
seo-title: Map identities | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: ID 매핑
description: 이 단원에서는 ID 네임스페이스를 만들고 스키마에 ID 필드를 추가합니다.
role: Data Architect
feature: Profiles
kt: 4348
thumbnail: 4348-map-identities.jpg
exl-id: e17ffabc-049c-42ff-bf0a-8cc31d665dfa
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 3%

---

# ID 매핑

<!-- 30 min-->

이 단원에서는 ID 네임스페이스를 만들고 스키마에 ID 필드를 추가합니다. 그런 다음 이전 단원에서 스키마 관계를 완료할 수 있습니다.

Adobe Experience Platform Identity Service를 사용하면 장치 및 시스템 전반에서 ID를 브리징하여 고객 및 행동을 더 잘 파악할 수 있으므로 효과적이고 개인화된 디지털 경험을 실시간으로 제공할 수 있습니다. ID 필드와 네임스페이스는 서로 다른 데이터 소스를 결합하여 360도 실시간 고객 프로필을 만드는 접착제입니다.

**데이터 설계자** 는 이 자습서의 외부에서 ID를 매핑해야 합니다.

연습을 시작하기 전에 이 짧은 비디오에서 Adobe Experience Platform의 ID에 대해 자세히 알아보십시오.
>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

>[!NOTE]
>
>ID 필드는 실시간 고객 프로필을 빌드하는 경우에만 필요합니다. 데이터 레이크로 데이터만 수집하는 경우에는 필요하지 않습니다.

<!--explain identity maps-->
<!--explain the strategy behind the identity selection, how these identities will join all the data together-->

## 필요한 권한

에서 [권한 구성](configure-permissions.md) 이 단원을 완료하는 데 필요한 모든 액세스 컨트롤을 설정합니다.

<!--
* Permission items **[!UICONTROL Identity Management]** > **[!UICONTROL View Identity Namespaces]** and **[!UICONTROL Manage Identity Namespaces]**
* Permission item **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## ID 네임스페이스 만들기

이 연습에서는 Luma의 사용자 지정 ID 필드에 대한 ID 네임스페이스를 만듭니다. `loyaltyId`, `crmId`, 및 `productSku`. 동일한 네임스페이스에 있는 두 개의 일치 값을 사용하면 두 데이터 소스가 ID 그래프를 형성할 수 있으므로 ID 네임스페이스는 실시간 고객 프로필을 작성하는 데 중요한 역할을 합니다.


### UI에서 네임스페이스 만들기

먼저 Luma 충성도 스키마의 네임스페이스를 만듭니다.

1. Platform 사용자 인터페이스에서 로 이동합니다. **[!UICONTROL ID]** 왼쪽 탐색
1. 사용 가능한 기본 ID 네임스페이스가 여러 개 있습니다. 을(를) 선택합니다 **[!UICONTROL ID 네임스페이스 만들기]** 버튼
1. 다음과 같이 세부 정보를 제공합니다

   | 필드 | 값 |
   |---------------|-----------|
   | 디스플레이 이름 | Luma 충성도 Id |
   | ID 기호 | luma충성도Id |
   | 유형 | 크로스 디바이스 |

1. **[!UICONTROL 만들기]**&#x200B;를 선택합니다

   ![네임스페이스 만들기](assets/identity-createNamespace.png)

이제 다음 세부 사항으로 Luma 제품 카탈로그 스키마에 대한 다른 네임스페이스를 설정합니다.

| 필드 | 값 |
|---------------|-----------|
| 디스플레이 이름 | Luma 제품 SKU |
| ID 기호 | lumaProductSKU |
| 유형 | 비사용자 식별자 |



## API를 사용하여 ID 네임스페이스 만들기

API를 통해 CRM 네임스페이스를 만듭니다.

>[!NOTE]
>
>API 연습을 건너뛰려면 다음 세부 정보와 함께 사용한 사용자 인터페이스 메서드를 통해 자유롭게 CRM 네임스페이스를 만드십시오.
>
> 1. 로서의 **[!UICONTROL 표시 이름]**, 사용 `Luma CRM Id`
> 1. 로서의 **[!UICONTROL ID 기호]**, 사용 `lumaCrmId`
> 1. 로서의 **[!UICONTROL 유형]**, 교차 장치 사용


ID 네임스페이스를 만들겠습니다 `Luma CRM Id`:

1. 다운로드 [Identity Service.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Identity%20Service.postman_collection.json) 아래와 같이 `Luma Tutorial Assets` 폴더
1. 컬렉션 가져오기 [!DNL Postman]
1. 지난 24시간 동안 요청을 하지 않은 경우 인증 토큰이 만료되었을 수 있습니다. 요청을 엽니다. **[!DNL Adobe I/O Access Token Generation > Local Signing (Non-production use-only) > IMS: JWT Generate + Auth via User Token]**, 을(를) 선택하고 을(를) 선택합니다. **보내기** 새 JWT 및 액세스 토큰을 요청하려면 다음을 수행하십시오.
1. 요청을 선택합니다 **[!UICONTROL ID 서비스] > [!UICONTROL ID 네임스페이스] > [!UICONTROL 새 ID 네임스페이스 만들기].**
1. 다음 내용을 [!DNL Body] 요청:

   ```json
   {
       "name": "Luma CRM Id",
       "code": "lumaCrmId",
       "idType": "Cross_device"
   }
   ```

1. 누르기 **보내기** 버튼을 누르면 **200 OK** 응답:

   ![ID 네임스페이스](assets/identity-createUsingApi.png)

사용자 인터페이스로 돌아가면 이제 세 개의 새 사용자 지정 네임스페이스가 표시됩니다.
![ID 네임스페이스 ](assets/identity-newIdentities.png)


## 스키마의 ID 필드에 레이블 지정

네임스페이스가 있으므로 다음 단계는 스키마를 업데이트하여 ID 필드에 레이블을 지정하는 것입니다.


### 기본 Id에 대한 Xdm 필드에 레이블 지정

실시간 고객 프로필과 함께 사용되는 각 스키마에는 기본 ID가 지정되어 있어야 합니다. 그리고 수집된 각 레코드에는 해당 필드에 대한 값이 있어야 합니다.

기본 ID를 `Luma Loyalty Schema`:

1. 를 엽니다. `Luma Loyalty Schema`
1. 을(를) 선택합니다 `Luma Identity profile field group`
1. 을(를) 선택합니다 `loyaltyId` 필드
1. 을(를) 확인합니다. **[!UICONTROL ID]** 상자
1. 을(를) 확인합니다. **[!UICONTROL 기본 ID]** 상자도
1. 을(를) 선택합니다 `Luma Loyalty Id` 네임스페이스 **[!UICONTROL ID 네임스페이스]** 드롭다운
1. 선택 **[!UICONTROL 적용]**
1. **[!UICONTROL 저장]**&#x200B;을 선택합니다

   ![기본 ID ](assets/identity-loyalty-primary.png)

다른 일부 스키마에 대해 프로세스를 반복합니다.

1. 에서 `Luma CRM Schema`, 레이블 지정 `crmId` 필드를 `Luma CRM Id` namespace
1. 에서 `Luma Offline Purchase Events Schema`, 레이블 지정 `loyaltyId` 필드를 `Luma Loyalty Id` namespace
1. 에서 `Luma Product Catalog Schema`, 레이블 지정 `productSku` 필드를 `Luma Product SKU` namespace

>[!NOTE]
>
>웹 SDK로 수집한 데이터는 스키마의 ID 필드에 레이블을 지정하는 일반적인 방법의 예외입니다. 웹 SDK는 ID 맵을 사용하여 ID에 레이블을 지정합니다 *구현 측에서* 따라서 우리는 `Luma Web Events Schema` luma 웹 사이트에서 웹 SDK를 구현하는 경우입니다. 이 후 단원에서는 Experience Cloud 방문자 ID(ECID)를 기본 ID로, crmId는 보조 ID로 수집합니다.

우리의 1차 ID의 선택을 통해, 어떻게 `Luma CRM Schema` 에 연결할 수 있습니다. `Luma Offline Purchase Events Schema` 둘 다 `loyaltyId` 를 식별자로 사용합니다. 그러나 오프라인 구매를 온라인 행동과 어떻게 연결시킬 수 있을까요? 제품 카탈로그와 함께 구매한 제품을 분류하려면 어떻게 해야 합니까? 추가적인 ID 필드와 스키마 관계를 사용할 것입니다.

<!--use a visual-->

### 보조 Id에 대한 Xdm 필드에 레이블 지정

스키마에 여러 ID 필드를 추가할 수 있습니다. 기본 ID가 아닌 ID를 보조 ID라고 합니다. 오프라인 구매를 온라인 동작에 연결하기 위해 crmId를 Adobe에 보조 식별자로 추가합니다 `Luma Loyalty Schema` 및 나중에 웹 이벤트 데이터를 참조하십시오. 업데이트 `Luma Loyalty Schema`:

1. 를 엽니다. `Luma Loyalty Schema`
1. 선택 `Luma Identity Profile Field group`
1. 선택 `crmId` 필드
1. 을(를) 확인합니다. **[!UICONTROL ID]** 상자
1. 을(를) 선택합니다 `Luma CRM Id` 네임스페이스 **[!UICONTROL ID 네임스페이스]** 드롭다운
1. 선택 **[!UICONTROL 적용]** 그런 다음 **[!UICONTROL 저장]** 변경 사항을 저장하는 단추

   ![보조 ID](assets/identity-loyalty-secondaryId.png)

## 스키마 관계 완료

이제 ID 필드가 레이블이 지정되었으므로 Luma의 제품 카탈로그와 이벤트 스키마 간의 스키마 관계 설정을 완료할 수 있습니다.

1. 를 엽니다. `Luma Offline Purchase Events Schema`
1. 선택 **[!UICONTROL 상거래 세부 사항]** 필드 그룹
1. 선택 **[!UICONTROL productListItems]** > **[!UICONTROL SKU]** 필드
1. 을(를) 확인합니다. **[!UICONTROL 관계]** 상자
1. 선택 `Luma Product Catalog Schema` 로서의 **[!UICONTROL 참조 스키마]**
1. `Luma Product SKU` 는 **[!UICONTROL 참조 ID 네임스페이스]**
1. 선택 **[!UICONTROL 적용]**
1. **[!UICONTROL 저장]**&#x200B;을 선택합니다

   ![참조 필드](assets/identity-offlinePurchase-relationship.png)

이 프로세스를 반복하여 `Luma Web Events Schema` 그리고 `Luma Product Catalog Schema`.

관계를 정의한 후에는 두 모두에 표시됩니다 **[!UICONTROL 조성물]** 및 **[!UICONTROL 구조]** 스키마 편집기의 섹션.

![스키마 편집기의 관계 시각화](assets/identity-webEvents-relationship.png)

<!--need to verify that the relationship schema works-->

## 추가 리소스

* [Identity Service 설명서](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=ko)
* [ID 서비스 API](https://www.adobe.io/experience-platform-apis/references/identity-service/)

이제 우리의 정체성이 제자리에 있으니 [데이터 세트 만들기](create-datasets.md)!
