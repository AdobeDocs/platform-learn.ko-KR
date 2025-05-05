---
title: ID 매핑
seo-title: Map identities | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: ID 매핑
description: 이 단원에서는 ID 네임스페이스를 만들고 스키마에 ID 필드를 추가합니다.
role: Data Architect
feature: Profiles
jira: KT-4348
thumbnail: 4348-map-identities.jpg
exl-id: e17ffabc-049c-42ff-bf0a-8cc31d665dfa
source-git-commit: 73645b8b088cfdfe6f256c187b3c510dcc2386fc
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 6%

---

# ID 매핑

<!-- 30 min-->

이 단원에서는 ID 네임스페이스를 만들고 스키마에 ID 필드를 추가합니다. 그렇게 하면 이전 단원에서 스키마 관계도 완성할 수 있습니다.

Adobe Experience Platform Identity Service를 사용하면 디바이스와 시스템 간에 ID를 연결하여 고객과 고객의 행동을 더 잘 볼 수 있으므로 효과적인 개인 디지털 경험을 실시간으로 제공할 수 있습니다. ID 필드와 네임스페이스는 서로 다른 데이터 소스를 함께 연결하여 360도 실시간 고객 프로필을 만드는 접착제입니다.

**데이터 설계자**&#x200B;는 이 자습서 외부에서 ID를 매핑해야 합니다.

연습을 시작하기 전에 이 짧은 비디오를 통해 Adobe Experience Platform의 ID에 대해 자세히 알아보십시오.
>[!VIDEO](https://video.tv.adobe.com/v/3422775?learn=on&enablevpops&captions=kor)

>[!NOTE]
>
>ID 필드는 실시간 고객 프로필을 작성하는 경우에만 필요합니다. 데이터 레이크로만 데이터를 수집하는 경우에는 필요하지 않습니다.

<!--explain identity maps-->
<!--explain the strategy behind the identity selection, how these identities will join all the data together-->

## 권한 필요

[권한 구성](configure-permissions.md) 단원에서 이 단원을 완료하는 데 필요한 모든 액세스 제어를 설정합니다.

<!--
* Permission items **[!UICONTROL Identity Management]** > **[!UICONTROL View Identity Namespaces]** and **[!UICONTROL Manage Identity Namespaces]**
* Permission item **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## ID 네임스페이스 만들기

이 연습에서는 Luma의 사용자 지정 ID 필드 `loyaltyId`, `crmId` 및 `productSku`에 대한 ID 네임스페이스를 만듭니다. 동일한 네임스페이스 내에 일치하는 두 값이 있으면 두 개의 데이터 소스가 하나의 ID 그래프를 구성할 수 있기 때문에 ID 네임스페이스는 실시간 고객 프로필을 작성하는 데 중요한 역할을 합니다.


### UI에서 네임스페이스 만들기

Luma 충성도 스키마에 대한 네임스페이스를 만들어 보겠습니다.

1. Platform 사용자 인터페이스에서 왼쪽 탐색 메뉴의 **[!UICONTROL ID]**(으)로 이동합니다.
1. 사용할 수 있는 기본 ID 네임스페이스가 여러 개 있습니다. **[!UICONTROL ID 네임스페이스 만들기]** 단추를 선택합니다.
1. 다음과 같이 세부 정보를 제공합니다

   | 필드 | 값 |
   |---------------|-----------|
   | 표시 이름 | Luma 충성도 Id |
   | ID 심볼 | lumaLoyaltyId |
   | 유형 | 크로스 디바이스 |

1. **[!UICONTROL 만들기]** 선택

   ![네임스페이스 만들기](assets/identity-createNamespace.png)

이제 다음 세부 정보를 사용하여 Luma 제품 카탈로그 스키마에 대한 다른 네임스페이스를 설정합니다.

| 필드 | 값 |
|---------------|-----------|
| 표시 이름 | Luma 제품 SKU |
| ID 심볼 | lumaProductSKU |
| 유형 | 비개인 식별자 |



## API를 사용하여 ID 네임스페이스 만들기

API를 통해 CRM 네임스페이스를 만듭니다.

>[!NOTE]
>
>API 연습을 건너뛰려면 다음 세부 정보와 함께 사용한 사용자 인터페이스 메서드를 통해 자유롭게 CRM 네임스페이스를 만드십시오.
>
> 1. **[!UICONTROL 표시 이름]**(으)로 `Luma CRM Id`을(를) 사용합니다.
> 1. **[!UICONTROL ID 기호]**(으)로 `lumaCrmId` 사용
> 1. **[!UICONTROL Type]**(으)로 Cross-Device 사용

ID 네임스페이스 `Luma CRM Id`을(를) 만들어 보겠습니다.

1. `Luma Tutorial Assets` 폴더에 [Identity Service.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Identity%20Service.postman_collection.json) 다운로드
1. 컬렉션을 [!DNL Postman]&#x200B;(으)로 가져오기
1. 액세스 토큰이 없는 경우 **[!DNL OAuth: Request Access Token]** 요청을 열고 **보내기**&#x200B;를 선택하여 새 액세스 토큰을 요청하세요.
1. 요청 **[!UICONTROL ID 서비스] > [!UICONTROL ID 네임스페이스] > [!UICONTROL 새 ID 네임스페이스 만들기]를 선택합니다.**
1. 다음을 요청의 [!DNL Body]&#x200B;(으)로 붙여 넣습니다.

   ```json
   {
       "name": "Luma CRM Id",
       "code": "lumaCrmId",
       "idType": "Cross_device"
   }
   ```

1. **보내기** 단추를 누르면 **200 OK** 응답이 나타납니다.

   ![ID 네임스페이스](assets/identity-createUsingApi.png)

이제 사용자 인터페이스로 돌아가면 세 개의 새 사용자 정의 네임스페이스가 표시됩니다.
![ID 네임스페이스 ](assets/identity-newIdentities.png)


## 스키마의 레이블 ID 필드

이제 네임스페이스가 있으므로 다음 단계는 스키마를 업데이트하여 ID 필드에 레이블을 지정하는 것입니다.


### 기본 Id에 대한 레이블 XDM 필드

실시간 고객 프로필과 함께 사용되는 각 스키마에는 기본 ID가 지정되어야 합니다. 그리고 수집된 각 레코드에는 해당 필드의 값이 있어야 합니다.

`Luma Loyalty Schema`에 기본 ID를 추가하겠습니다.

1. `Luma Loyalty Schema` 열기
1. `Luma Identity profile field group` 선택
1. `loyaltyId` 필드 선택
1. **[!UICONTROL ID]** 상자를 선택합니다.
1. **[!UICONTROL 기본 ID]** 상자도 확인
1. **[!UICONTROL ID 네임스페이스]** 드롭다운에서 `Luma Loyalty Id` 네임스페이스를 선택합니다.
1. **[!UICONTROL 적용]** 선택
1. **[!UICONTROL 저장]** 선택

   ![기본 ID ](assets/identity-loyalty-primary.png)

다른 스키마 일부에 대해 다음 프로세스를 반복합니다.

1. `Luma CRM Schema`에서 `Luma CRM Id` 네임스페이스를 사용하여 `crmId` 필드에 기본 ID로 레이블을 지정합니다.
1. `Luma Offline Purchase Events Schema`에서 `Luma Loyalty Id` 네임스페이스를 사용하여 `loyaltyId` 필드에 기본 ID로 레이블을 지정합니다.
1. `Luma Product Catalog Schema`에서 `Luma Product SKU` 네임스페이스를 사용하여 `productSku` 필드에 기본 ID로 레이블을 지정합니다.

>[!NOTE]
>
>웹 SDK으로 수집된 데이터는 스키마에서 ID 필드에 레이블을 지정하는 일반적인 방법에 대한 예외입니다. Web SDK은 ID 맵을 사용하여 구현 측면에 *의 ID에 레이블을 지정합니다*. 따라서 Luma 웹 사이트에서 Web SDK을 구현할 때 `Luma Web Events Schema`의 ID를 결정합니다. 이후 단원에서는 기본 ID로 Experience Cloud 방문자 ID(ECID)를 수집하고 보조 ID로 crmId를 수집합니다.

기본 ID를 선택하면 `Luma Loyalty Schema`이(가) loyaltyId를 식별자로 사용하므로 `Luma Offline Purchase Events Schema`에 연결할 수 있는 방법을 알 수 있습니다. 그러나 CRM을 오프라인 구매 이벤트에 연결하는 방법은 무엇입니까? 오프라인 구매를 온라인 비헤이비어와 어떻게 연결할 수 있습니까? 그리고 우리 제품 카탈로그로 구매한 제품을 어떻게 분류할 수 있을까? 추가 ID 필드 및 스키마 관계를 사용합니다.

<!--use a visual-->

### 보조 ID에 대한 레이블 XDM 필드

여러 ID 필드를 스키마에 추가할 수 있습니다. 기본이 아닌 ID를 종종 보조 ID라고 합니다. 오프라인 구매를 온라인 동작에 연결하기 위해 crmId를 `Luma Loyalty Schema` 및 이후 웹 이벤트 데이터에 보조 식별자로 추가합니다. `Luma Loyalty Schema`을(를) 업데이트하겠습니다.

1. `Luma Loyalty Schema` 열기
1. `Luma Identity Profile Field group` 선택
1. `crmId` 필드 선택
1. **[!UICONTROL ID]** 상자를 선택합니다.
1. **[!UICONTROL ID 네임스페이스]** 드롭다운에서 `Luma CRM Id` 네임스페이스를 선택합니다.
1. **[!UICONTROL 적용]**&#x200B;을 선택한 다음 **[!UICONTROL 저장]** 단추를 선택하여 변경 내용을 저장합니다.

   ![보조 ID](assets/identity-loyalty-secondaryId.png)

## 스키마 관계 완료

이제 ID 필드에 레이블이 지정되었으므로 Luma의 제품 카탈로그와 이벤트 스키마 간의 스키마 관계 설정을 완료할 수 있습니다.

1. `Luma Offline Purchase Events Schema` 열기
1. **[!UICONTROL Commerce 세부 정보]** 필드 그룹 선택
1. **[!UICONTROL productListItems]** > **[!UICONTROL SKU]** 필드 선택
1. **[!UICONTROL 관계]** 상자를 선택합니다.
1. `Luma Product Catalog Schema`을(를) **[!UICONTROL 참조 스키마]**(으)로 선택
1. `Luma Product SKU`은(는) 자동으로 **[!UICONTROL 참조 ID 네임스페이스]**(으)로 채워집니다.
1. **[!UICONTROL 적용]** 선택
1. **[!UICONTROL 저장]** 선택

   ![참조 필드](assets/identity-offlinePurchase-relationship.png)

이 프로세스를 반복하여 `Luma Web Events Schema`과(와) `Luma Product Catalog Schema` 사이의 관계를 만듭니다.

관계를 정의하면 스키마 편집기의 **[!UICONTROL 컴포지션]** 및 **[!UICONTROL 구조]** 섹션에 모두 표시됩니다.

![스키마 편집기의 관계 시각화](assets/identity-webEvents-relationship.png)

<!--need to verify that the relationship schema works-->

## 추가 리소스

* [ID 서비스 설명서](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=ko-KR)
* [ID 서비스 API](https://www.adobe.io/experience-platform-apis/references/identity-service/)

이제 ID가 준비되었으므로 [데이터 세트를 만들 수 있습니다](create-datasets.md)!
