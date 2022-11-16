---
title: 태그 속성 만들기
description: 데이터 수집 인터페이스에 로그인하고 태그 속성을 만드는 방법을 알아봅니다. 이 단원은 웹 사이트에서 Experience Cloud 구현 자습서의 일부입니다.
exl-id: f83d374a-a831-4598-b9d3-6f183224b589
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 55%

---

# 태그 속성 만들기

이 단원에서는 첫 번째 태그 속성을 만듭니다.

속성은 사이트에 태그를 배포할 때 기본적으로 확장, 규칙, 데이터 요소 및 라이브러리로 채우는 컨테이너입니다.

## 전제 조건

다음 몇 가지 단원을 마치려면 태그에서 개발, 승인, 게시, 확장 관리 및 환경 관리 권한이 있어야 합니다. 사용자 인터페이스 옵션을 사용할 수 없어서 이러한 단계를 완료할 수 없는 경우 Experience Cloud 관리자에게 연락하여 액세스 권한을 요청하십시오. 태그 사용자 권한에 대한 자세한 내용은 [설명서](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html).

>[!NOTE]
>
>Adobe Experience Platform Launch은 데이터 수집 기술 세트로 Adobe Experience Platform에 통합되고 있습니다. 인터페이스에서 이 컨텐츠를 사용하는 동안 알고 있어야 하는 몇 가지 용어 변경 사항이 롤아웃되었습니다.
>
> * 이제 platform launch(클라이언트측)가 **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)**
> * 이제 platform launch 서버 측 **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * 이제 Edge 구성이 제공됩니다. **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)**


## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* 데이터 수집 사용자 인터페이스에 로그인
* 새 태그 속성 만들기
* 태그 속성 구성

## Data Collection 인터페이스로 이동합니다

**데이터 수집에 액세스하려면**

1. [Adobe Experience Cloud](https://experiencecloud.adobe.com)에 로그인합니다.

1. 을(를) 클릭합니다. ![솔루션 전환기 아이콘](images/launch-solutionSwitcher.png) 아이콘 을 클릭하여 앱 전환기를 엽니다.

1. 선택 **[!UICONTROL 시작/데이터 수집]** 메뉴에서 ![아이콘을 사용하여 솔루션 전환기를 열고 Launch/Data Collection 을 클릭합니다.](images/launch-solutionSwitcherActivation.png)

이제 `Tags Properties` 화면이 표시됩니다. 계정에서 속성을 만들지 않은 경우 이 화면이 비어 있을 수 있습니다.

![속성 화면](images/launch-propertiesScreen.png)

## 속성 만들기

속성은 사이트에 태그를 배포할 때 기본적으로 확장, 규칙, 데이터 요소 및 라이브러리로 채우는 컨테이너입니다. 속성은 하나 이상의 도메인과 하위 도메인을 그룹화한 것일 수 있습니다. 이 자산들은 유사하게 관리 및 추적할 수 있습니다. 예를 들어 하나의 템플릿을 기반으로 한 여러 개의 웹 사이트가 있고 이러한 웹 사이트 모두에서 동일한 자산을 추적하려 하는 경우, 여러 도메인에 하나의 속성을 적용할 수 있습니다. 속성 만들기에 대한 자세한 내용은 제품 설명서의 [&quot;회사 및 속성&quot;](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html)을 참조하십시오.

**속성을 만들려면**

1. **[!UICONTROL New Property]** 단추를 클릭합니다.

   ![New Property 클릭](images/launch-addNewProperty.png)

1. 속성에 이름을 지정합니다(예: `Luma Tutorial` 또는 `Luma Tutorial - Daniel`).
1. `enablementadobe.com`이 Luma 데모 사이트가 호스팅되는 도메인이므로 도메인으로는 이 도메인을 입력합니다. 도메인 필드가 필요하지만 태그 속성은 태그 속성이 구현된 모든 도메인에서 작동합니다. 이 필드의 주 목적은 규칙 빌더에서 메뉴 옵션을 미리 채우는 것입니다.
1. 를 확장합니다. **[!UICONTROL 고급 옵션]** 섹션을 클릭하고 다음 확인란을 선택합니다. **[!UICONTROL 규칙 구성 요소를 순서대로 실행]**
1. **[!UICONTROL Save]** 단추를 클릭합니다.

   ![새 속성 만들기](images/launch-newProperty.png)

새 속성이 속성 페이지에 표시됩니다. 속성 이름 옆에 있는 상자를 선택하면 속성에 대한 **[!UICONTROL Configure]** 또는 **[!UICONTROL Delete]** 옵션이 속성 목록 위에 표시됩니다. 속성 이름(예: `Luma Tutorial`)을 클릭하여 `Overview` 화면을 엽니다.
![속성 이름을 클릭하여 열기](images/launch-openProperty.png)

[다음 &quot; 포함 코드 추가&quot; >](add-embed-code.md)
