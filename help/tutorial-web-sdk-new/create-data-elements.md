---
title: 데이터 요소 만들기
description: XDM 개체를 만들고 데이터 요소를 태그에 매핑하는 방법에 대해 알아봅니다. 이 단원은 Web SDK를 사용하여 Adobe Experience Cloud 구현 자습서의 일부입니다.
feature: Tags
source-git-commit: 695c12ab66df33af00baacabc3b69eaac7ada231
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 1%

---

# 데이터 요소 만들기

Experience Platform Web SDK를 사용하여 데이터를 캡처하는 데 필요한 필수 데이터 요소를 만드는 방법을 알아봅니다. 에서 컨텐츠 및 ID 데이터 캡처 [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html). XDM 개체라는 새 데이터 요소 유형을 통해 Platform Web SDK를 사용하여 데이터를 수집하기 위해 이전에 만든 XDM 스키마를 사용하는 방법에 대해 알아봅니다.

>[!NOTE]
>
> 데모 목적으로 이 단원의 연습은 다음 기간 동안 사용된 예를 기반으로 합니다. [스키마 구성](configure-schemas.md) 단계; 본 컨텐츠 및 의 사용자 ID를 캡처하는 예제 XDM 개체 만들기 [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html).

>[!IMPORTANT]
>
>이 단원의 데이터는 `[!UICONTROL digitalData]` Luma 사이트의 데이터 레이어 데이터 레이어를 보려면 개발자 콘솔을 열고 을 입력합니다. `[!UICONTROL digitalData]` 전체 데이터 레이어를 확인할 수 있습니다.![digitalData 데이터 레이어](assets/data-element-data-layer.png)


Platform Web SDK에 관계없이, 데이터 레이어, HTML 속성 또는 기타 속성과 같이, 웹 사이트의 데이터 수집 변수에 매핑되는 태그 속성 내에 데이터 요소를 계속 만들어야 합니다. 이러한 데이터 요소를 만든 후에는 다음 작업 중에 만든 XDM 스키마에 매핑해야 합니다. [스키마 구성](configure-schemas.md) 레슨. 이를 위해 Platform 웹 SDK 확장은 XDM 개체라는 새 데이터 요소 유형을 사용할 수 있도록 합니다. 따라서 데이터 요소 만들기는 두 가지 작업으로 구성됩니다.

1. 웹 사이트 변수를 데이터 요소에 매핑 및
1. 이러한 데이터 요소를 XDM 개체에 매핑

1단계의 경우 코어 태그 확장의 데이터 요소 유형을 사용하여 현재 데이터 레이어와 동일한 방식으로 데이터 요소를 계속 매핑합니다. 2단계의 경우 Platform Web SDK 확장은 이전에 사용할 수 없었던 일련의 새로운 데이터 요소 유형을 만듭니다.

* 이벤트 병합 ID
* ID 맵
* XDM 개체

이 단원에서는 XDM 개체 및 ID 맵 데이터 요소 유형에 중점을 둡니다. Luma 방문자의 활동 및 인증 상태를 캡처하는 XDM 개체를 만듭니다.

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* 데이터 요소를 만들어 콘텐츠 및 사용자 로그인 ID 데이터 캡처
* ID 맵 데이터 요소 만들기
* 데이터 요소를 XDM 개체 데이터 요소에 매핑


## 전제 조건

데이터 계층이 무엇인지 이해하고 있으며 [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} 데이터 레이어 및 태그의 데이터 요소를 참조하는 방법을 알아봅니다. 자습서에서 다음 이전 단계를 완료해야 합니다

* [권한 구성](configure-permissions.md)
* [XDM 스키마 구성](configure-schemas.md)
* [ID 네임스페이스 구성](configure-identities.md)
* [데이터스트림 구성](configure-datastream.md)
* [태그 속성에 설치된 Web SDK 확장](install-web-sdk.md)

>[!IMPORTANT]
>
>다음 [Experience Cloud ID 서비스 확장](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) ID 서비스 기능이 Platform Web SDK에 내장되어 있으므로 Adobe Experience Platform Web SDK를 구현할 때에는 이 필요하지 않습니다.

## 데이터 요소를 만들어 데이터 레이어 캡처

XDM 개체 만들기를 시작하기 전에 [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} 데이터 계층:

1. 다음으로 이동 **[!UICONTROL 데이터 요소]** 및 선택 **[!UICONTROL 데이터 요소 추가]** (또는 **[!UICONTROL 새 데이터 요소 만들기]** 태그 속성에 기존 데이터 요소가 없는 경우)

   ![데이터 요소 만들기](assets/data-element-create.jpg)

1. 데이터 요소에 이름을 지정합니다 `page.pageInfo.pageName`
1. 사용 **[!UICONTROL JavaScript 변수]** **[!UICONTROL 데이터 요소 유형]** luma의 데이터 레이어에 있는 값을 가리키려면 다음을 수행합니다. `digitalData.page.pageInfo.pageName`

1. 다음 확인란을 선택합니다. **[!UICONTROL 소문자 강제 적용 값]** 및 **[!UICONTROL 텍스트 정리]** 케이스를 표준화하고 외부 공백을 제거하려면

1. 나가기 `None` (으)로 **[!UICONTROL 저장 기간]** 이 값은 모든 페이지에서 다르므로 설정

1. 선택 **[!UICONTROL 저장]**

   ![페이지 이름 데이터 요소](assets/data-element-pageName.jpg)

다음 네 가지 추가 데이터 요소를 만들려면 동일한 단계를 따르십시오.

* **`page.pageInfo.server`**  매핑됨
  `digitalData.page.pageInfo.server`

* **`page.pageInfo.hierarchie1`**  매핑됨
  `digitalData.page.pageInfo.hierarchie1`

* **`user.profile.attributes.username`**  매핑됨
  `digitalData.user.0.profile.0.attributes.username`

* **`user.profile.attributes.loggedIn`** 매핑됨
  `digitalData.user.0.profile.0.attributes.loggedIn`

* **`cart.orderId`** 매핑됨 `digitalData.cart.orderId` (다음 기간 동안 이 옵션을 사용합니다. [Analytics 설정](setup-analytics.md) 단원)


>[!CAUTION]
>
>다음 [!UICONTROL JavaScript 변수] 데이터 요소 유형은 배열 참조를 대괄호 대신 점으로 처리하므로 사용자 이름 데이터 요소를 로 참조합니다. `digitalData.user[0].profile[0].attributes.username` **작동하지 않음**.

## ID 맵 데이터 요소 만들기

다음으로 ID 맵 데이터 요소를 만들 수 있습니다.

1. 다음으로 이동 **[!UICONTROL 데이터 요소]** 및 선택 **[!UICONTROL 데이터 요소 추가]**

1. **[!UICONTROL 이름]** 데이터 요소 `identityMap.loginID`

1. 다음으로: **[!UICONTROL 확장]**, 선택 `Adobe Experience Platform Web SDK`

1. 다음으로: **[!UICONTROL 데이터 요소 유형]**, 선택 `Identity map`

1. 이렇게 하면 내에서 오른쪽에 화면 영역이 표시됩니다. **[!UICONTROL 데이터 수집 인터페이스]** id를 구성할 수 있도록 다음을 수행합니다.

   ![데이터 수집 인터페이스](assets/identity-identityMap-setup.png)

1. 다음으로:  **[!UICONTROL 네임스페이스]**&#x200B;를 선택하고 `Luma CRM Id` 이전에 만든 네임스페이스 [ID 구성](configure-identities.md) 레슨.

   >[!NOTE]
   >
   >    다음 항목이 표시되지 않으면 `Luma CRM Id` 네임스페이스에서 기본 프로덕션 샌드박스에서도 생성했는지 확인합니다. 기본 프로덕션 샌드박스에서 생성된 네임스페이스만 현재 네임스페이스 드롭다운에 표시됩니다.

1. 다음 이후 **[!UICONTROL 네임스페이스]** 을(를) 선택한 경우 ID를 설정해야 합니다. 다음 항목 선택 `user.profile.attributes.username` 사용자가 Luma 사이트에 로그인하면 ID를 캡처하는 이 단원의 앞부분에서 만든 데이터 요소입니다.

<!--  >[!TIP]
   >
   >You can verify the **[!UICONTROL Luma CRM ID]** is collected in a data element on the web property by going to the [Luma Demo site](https://luma.enablementadobe.com/content/luma/us/en.html), logging in, [switching the tag environment](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) to your own, and typing `_satellite.getVar("user.profile.attributes.username")` in the web browser developer console.
   >
   >   ![Data Element  ID ](assets/identity-data-element-customer-id.png)
-->

1. 다음으로: **[!UICONTROL 인증 상태]**, 선택 **[!UICONTROL 인증됨]**
1. 선택 **[!UICONTROL 기본]**

1. 선택 **[!UICONTROL 저장]**

   ![데이터 수집 인터페이스](assets/identity-id-namespace.png)

>[!TIP]
>
> Adobe은 다음과 같이 개인을 나타내는 ID를 전송할 것을 권장합니다. `Luma CRM Id`를 로 사용 [!UICONTROL 기본] 신원.
>
> ID 맵에 개인 식별자가 포함된 경우(예: `Luma CRM Id`)를 입력하면 개인 식별자가 [!UICONTROL 기본] 신원. 그렇지 않으면, `ECID` 이(가) [!UICONTROL 기본] 신원.





<!--
1. Once the data element is configured in **[!UICONTROL Data Collection interface]**, it can be tested on the Luma web property like any other Data Element. Enter the following script in the browser developer console
   
   
   ```
   _satellite.getVar('identityMap.loginID')
   ```  

   ![Data Collection interface](assets/identity-consoleIdentityDataElement.png)
   
   >[!NOTE]
   >
   >ECID identifier will NOT populate in the Data Element, as this is configured already with Platform Web SDK.   
-->

## XDM 개체에 데이터 요소 매핑

만드는 모든 데이터 요소는 XDM 개체에 매핑해야 합니다. 이 개체는 다음 작업 중에 만든 XDM 스키마를 준수해야 합니다. [스키마 구성](configure-schemas.md) 레슨.

데이터 요소를 XDM 개체 필드에 매핑하는 방법에는 여러 가지가 있습니다. 데이터 요소가 XDM 개체에 있는 정확한 키-값 쌍 스키마와 일치하는 경우 개별 데이터 요소를 개별 XDM 필드에 매핑하거나 데이터 요소를 전체 XDM 개체에 매핑할 수 있습니다. 이 단원에서는 캡처하여 개별 필드에 매핑하여 컨텐츠 데이터를 캡처합니다. 다음 방법을 배울 수 있습니다. [전체 XDM 개체에 데이터 요소 매핑](setup-analytics.md#Map-an-entire-array-to-an-XDM-Object) 다음에서 [Analytics 설정](setup-analytics.md) 레슨.

콘텐츠 데이터를 캡처할 XDM 개체 만들기:

1. 왼쪽 탐색에서 을 선택합니다. **[!UICONTROL 데이터 요소]**
1. 선택 **[!UICONTROL 데이터 요소 추가]**
1. **[!UICONTROL 이름]** 데이터 요소 **`xdm.content`**
1. 다음으로: **[!UICONTROL 확장]** 선택 `Adobe Experience Platform Web SDK`
1. 다음으로: **[!UICONTROL 데이터 요소 유형]** 선택 `XDM object`
1. 플랫폼 선택 **[!UICONTROL 샌드박스]** 에서 를 수행하는 동안 XDM 스키마를 만든 경우 [XDM 스키마 구성](configure-schemas.md) 단원, 이 예에서 `DEVELOPMENT Mobile and Web SDK Courses`
1. 다음으로: **[!UICONTROL 스키마]**&#x200B;을(를) 선택합니다 `Luma Web Event Data` 스키마:

   ![XDM 개체](assets/data-element-xdm.content-fields.png)

   >[!NOTE]
   >
   >샌드박스는 스키마를 만든 Experience Platform 샌드박스에 해당합니다. Experience Platform 인스턴스에는 여러 개의 샌드박스가 있을 수 있으므로 올바른 샌드박스를 선택해야 합니다. 항상 개발 작업을 먼저 수행한 다음 프로덕션을 수행합니다.

1. 에 도달할 때까지 아래로 스크롤합니다. **`web`** 오브젝트
1. 열려면 선택하십시오.

   ![웹 개체](assets/data-element-pageviews-xdm-object.png)


1. 다음 웹 XDM 변수를 데이터 요소에 매핑

   * **`web.webPageDetials.name`** 끝 `%page.pageInfo.pageName%`
   * **`web.webPageDetials.server`** 끝 `%page.pageInfo.server%`
   * **`web.webPageDetials.siteSection`** 끝 `%page.pageInfo.hierarchie1%`

   ![XDM 개체](assets/data-element-xdm.content.png)

1. 그런 다음 `identityMap` 스키마의 객체를 선택하고

1. 에 매핑 `identityMap.loginID` 데이터 요소

1. 선택 **[!UICONTROL 저장]**

   ![데이터 수집 인터페이스](assets/identity-dataElements-xdmContent-LumaSchema-identityMapSelect3.png)




이러한 단계를 마치면 다음 데이터 요소를 만들어야 합니다.

| 코어 확장 데이터 요소 | Platform Web SDK 데이터 요소 |
-----------------------------|-------------------------------
| `cart.orderId` | `identityMap.loginID` |
| `page.pageInfo.hierarchie1` | `xdm.content` |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |

이러한 데이터 요소가 준비되면 태그에 규칙을 만들어 XDM 개체를 통해 Platform Edge Network에 데이터를 전송할 준비가 되었습니다.

[다음: ](create-tag-rule.md)

>[!NOTE]
>
>Adobe Experience Platform Web SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하려는 경우 또는 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
