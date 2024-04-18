---
title: 태그 규칙 만들기
description: 태그 규칙을 사용하여 XDM 오브젝트와 함께 이벤트를 Platform Edge Network에 보내는 방법에 대해 알아봅니다. 이 단원은 Web SDK를 사용하여 Adobe Experience Cloud 구현 자습서의 일부입니다.
feature: Tags
exl-id: e06bad06-3ee3-475f-9b10-f0825a48a312
source-git-commit: 15bc08bdbdcb19f5b086267a6d94615cbfe1bac7
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 3%

---

# 태그 규칙 만들기


>[!CAUTION]
>
>2024년 4월 23일 화요일에 이 자습서에 대한 주요 변경 사항을 게시하겠습니다. 이 시점 이후에는 많은 연습이 변경되며 모든 단원을 완료하려면 튜토리얼을 처음부터 다시 시작해야 할 수 있습니다.

태그 규칙을 사용하여 XDM 오브젝트와 함께 이벤트를 Platform Edge Network에 보내는 방법에 대해 알아봅니다. 태그 규칙은 태그 속성에 작업을 수행하도록 지시하는 이벤트, 조건 및 작업의 조합입니다.

>[!NOTE]
>
> 데모 목적으로 이 단원의 연습은 다음 기간 동안 사용한 예를 기반으로 합니다. [데이터 요소 만들기](create-data-elements.md) 단계; XDM 이벤트 작업을 전송하여 의 사용자로부터 콘텐츠 및 ID 캡처 [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html).


## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* 태그 내 규칙 관리에 명명 규칙 사용
* XDM 이벤트를 전송하는 태그 규칙 만들기
* 개발 라이브러리에 태그 규칙 게시


## 전제 조건

데이터 수집 태그 및 [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html), 그리고 자습서에서 다음 이전 단원을 완료해야 합니다.

* [권한 구성](configure-permissions.md)
* [XDM 스키마 구성](configure-schemas.md)
* [ID 네임스페이스 구성](configure-identities.md)
* [데이터스트림 구성](configure-datastream.md)
* [태그 속성에 설치된 Web SDK 확장](install-web-sdk.md)
* [데이터 요소 만들기](create-data-elements.md)

## 이름 지정 규칙

태그의 규칙을 더 잘 관리하려면 표준 명명 규칙을 따르는 것이 좋습니다. 이 튜토리얼에서는 세 부분으로 구성된 명명 규칙을 사용합니다.

* [위치] - [이벤트] - [도구]

다음의 경우

1. 위치는 규칙이 실행되는 사이트의 페이지입니다
1. event 는 비콘을 실행하는 트리거입니다.
1. 도구는 해당 규칙의 작업 단계에서 사용되는 특정 응용 프로그램입니다


## 태그 규칙 만들기

태그에서 규칙은 다양한 조건에서 작업(호출 실행)을 실행하는 데 사용됩니다. Edge Network 이 첫 번째 규칙을 사용하여 Web SDK의 [!UICONTROL 이벤트 보내기] 작업. 이 자습서의 뒷부분에서는 방문자가 켜져 있는 페이지 유형에 따라 서로 다른 버전의 XDM 개체를 보냅니다. 이러한 이유로 규칙 조건을 사용하여 다른 유형의 페이지를 제외합니다.

태그 규칙을 만들려면 다음을 수행하십시오.

1. 이 자습서에서 사용하는 태그 속성을 엽니다
1. 다음으로 이동 **[!UICONTROL 규칙]** 왼쪽 탐색
1. 다음 항목 선택 **[!UICONTROL 새 규칙 만들기]** 단추
   ![규칙 만들기](assets/rules-create.png)
1. 규칙 이름을 지정합니다 `all pages - library load - AA & AT`

   >[!NOTE]
   >
   > 이 규칙은 향후 단원에서 Adobe Analytics 및 Target에 의해 특정 방식으로 사용됩니다. 이 때문에 `AA & AT` 는 이름의 끝에 사용됩니다.

1. 다음에서 **[!UICONTROL 이벤트]** 섹션, 선택 **[!UICONTROL 추가]**
   ![규칙에 이름 지정 및 이벤트 추가](assets/rule-name.png)
1. 사용 **[!UICONTROL 코어 확장]** 및 선택 `Library Loaded (Page Top)` (으)로 **[!UICONTROL 이벤트 유형]**.

   이 설정은 태그 라이브러리가 페이지에 로드될 때마다 규칙이 실행됨을 의미합니다.
1. 선택 **[!UICONTROL 변경 내용 유지]** 기본 규칙 화면으로 돌아가기
   ![Library Loaded 이벤트 추가](assets/rule-event-pagetop.png)
1. 다음에서 **[!UICONTROL 조건]** 섹션에서 **[!UICONTROL 추가]** 단추
   ![조건 추가](assets/rules-add-conditions.png)
1. 선택 **[!UICONTROL 논리 유형]** `Exception`, **[!UICONTROL 확장]** `Core`, 및 **[!UICONTROL 조건 유형]** `Path Without Query String`
1. URL 경로 입력 `/content/luma/us/en/user/cart.html` 다음에서 **[!UICONTROL 경로가 다음과 같음]** 필드 및 **[!UICONTROL 이름]** it `Core - cart page`
1. 선택 **[!UICONTROL 변경 내용 유지]**
   ![조건 추가](assets/rule-condition-exception.png)
1. 다음 URL 경로에 대해 세 가지 예외를 더 추가합니다

   * **`Core - checkout page`** for `/content/luma/us/en/user/checkout.html`
   * **`Core - thank you page`** for `/content/luma/us/en/user/checkout/order/thank-you.html`
   * **`Core - product page`** 대상 `/products/` Regex 스위치가 켜진 상태에서

   ![조건 추가](assets/rule-condition-exception-all.png)

1. 다음에서 **[!UICONTROL 작업]** 섹션, 선택 **[!UICONTROL 추가]**
1. 선택 **[!UICONTROL Adobe Experience Platform 웹 SDK]** (으)로 **[!UICONTROL 확장]**
1. 선택 **[!UICONTROL 이벤트 보내기]** (으)로 **[!UICONTROL 작업 유형]**
1. 선택 **[!UICONTROL web.webpagedetails.pageViews]** (으)로 **[!UICONTROL 유형]**.

   >[!WARNING]
   >
   > 이 드롭다운은 **`xdm.eventType`** 변수를 채우는 방법에 따라 페이지를 순서대로 표시합니다. 이 필드에는 자유 형식 레이블을 입력할 수도 있지만, 반드시 입력하는 것이 좋습니다 **금지** Platform에는 역효과가 있기 때문입니다.

1. 다음으로: **[!UICONTROL XDM 데이터]**&#x200B;를 선택하고 `xdm.content` 이전 단원에서 만든 데이터 요소
1. 선택 **[!UICONTROL 변경 내용 유지]** 기본 규칙 화면으로 돌아가기

   ![이벤트 보내기 작업 추가](assets/rule-set-action-xdm.png)
1. 선택 **[!UICONTROL 저장]** 규칙을 저장하려면

   ![규칙 저장](assets/rule-save.png)

## 라이브러리에 규칙 게시

그런 다음 규칙이 작동하는지 확인할 수 있도록 개발 환경에 규칙을 게시합니다.

라이브러리를 만들려면 다음 작업을 수행하십시오.

1. 다음으로 이동 **[!UICONTROL 게시 플로우]** 왼쪽 탐색
1. 선택 **[!UICONTROL 라이브러리 추가]**

   ![라이브러리 추가 를 선택합니다](assets/rule-publish-library.png)
1. 의 경우 **[!UICONTROL 이름]**, 입력 `Luma Web SDK Tutorial`
1. 의 경우 **[!UICONTROL 환경]**, 선택 `Development`
1. 선택  **[!UICONTROL 변경된 모든 리소스 추가]**

   >[!NOTE]
   >
   >    Adobe Experience Platform 웹 SDK 확장 및 `all pages - library load - AA & AT` 규칙: 이전 단원에서 만든 태그 구성 요소가 표시됩니다. 코어 확장에는 모든 웹 태그 속성에 필요한 기본 JavaScript가 포함되어 있습니다.

1. 선택 **[!UICONTROL 개발을 위한 저장 및 구축]**

   ![라이브러리 만들기 및 빌드](assets/rule-publish-add-all-changes.png)

라이브러리를 빌드하는 데 몇 분 정도 소요될 수 있으며 완료되면 라이브러리 이름 왼쪽에 녹색 점이 표시됩니다.

![빌드 완료](assets/rule-publish-success.png)

에서 볼 수 있듯이 [!UICONTROL 게시 플로우] 화면, 게시 프로세스에는 이 자습서의 범위를 벗어나는 많은 내용이 있습니다. 이 자습서에서는 개발 환경의 단일 라이브러리를 사용합니다.

이제 Adobe Experience Platform Debugger을 사용하여 요청에 있는 데이터의 유효성을 검사할 준비가 되었습니다.

[다음 ](validate-with-debugger.md)

>[!NOTE]
>
>Adobe Experience Platform Web SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하려는 경우 또는 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
