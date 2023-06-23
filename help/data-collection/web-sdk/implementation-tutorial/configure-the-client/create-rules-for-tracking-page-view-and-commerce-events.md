---
title: 페이지 보기 및 상거래 이벤트를 추적하기 위한 규칙 만들기
description: 페이지 보기 및 상거래 이벤트를 추적하기 위한 규칙 만들기
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 2dd02462-ddb5-4f67-8b0f-4a5bf5f7d655
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 2%

---

# 페이지 보기 및 상거래 이벤트를 추적하기 위한 규칙 만들기

사용자가 제품 페이지를 보았는지 추적하려면 Adobe Experience Platform 태그 내에 규칙을 만듭니다. 다음을 수행합니다. [!UICONTROL 규칙] 왼쪽 메뉴에서 [!UICONTROL 규칙 추가].

규칙 이름에 을 입력합니다. _페이지 조회함_.

## 이벤트 추가

다음을 클릭합니다. [!UICONTROL 추가] 아래에 있는 단추 [!UICONTROL 이벤트]. 이제 이벤트 보기에 가 표시됩니다. 의 경우 [!UICONTROL 확장] 필드, 선택 [!UICONTROL Adobe 클라이언트 데이터 레이어]. 의 경우 [!UICONTROL 이벤트 유형] 필드, 선택 [!UICONTROL 데이터 푸시됨].

왜냐하면 다음과 같은 경우에만 이 규칙이 트리거되도록 하기 때문입니다. `pageViewed` 이벤트가 데이터 레이어로 푸시되고 [!UICONTROL 특정 이벤트] 아래에 [!UICONTROL 들어보기] 및 유형 _페이지 조회수_ 대상: [!UICONTROL 등록할 이벤트/키] 텍스트 필드.

![페이지 조회수 이벤트](../../../assets/implementation-strategy/page-viewed-event.png)

[!UICONTROL 변경사항 유지]를 클릭합니다.

## 작업 추가

이제 규칙 보기로 돌아왔으므로 [!UICONTROL 추가] 아래에 있는 단추 [!UICONTROL 작업]. 이제 작업 보기에 있어야 합니다. 의 경우 [!UICONTROL 확장] 필드, 선택 [!UICONTROL Adobe Experience Platform 웹 SDK]. 의 경우 [!UICONTROL 작업 유형] 필드, 선택 [!UICONTROL 이벤트 보내기]. 이 작업을 통해 Adobe Experience Platform Edge Network에 경험 이벤트를 보낼 수 있습니다.

화면 오른쪽에서 [!UICONTROL 유형] 필드 및 선택 `web.webpagedetails.pageViews`. Adobe Experience Platform에서 즉시 제공하는 표준 경험 이벤트 유형 중 하나입니다. 페이지 보기를 나타냅니다.

의 경우 [!UICONTROL XDM 데이터] 필드, 입력 `%event.fullState%`. 이는 규칙이 트리거될 때 캡처되는 데이터 레이어의 계산된 상태(전체 상태라고도 함)를 경험 이벤트의 일부로 전송해야 함을 나타냅니다.

![페이지 조회수 작업](../../../assets/implementation-strategy/page-viewed-action.png)

웹 사이트에서 데이터 레이어로 푸시한 데이터가 XDM 스키마를 따르지 않았거나 데이터 레이어의 계산된 상태 일부만 전송하려는 경우 [!UICONTROL XDM 개체] 데이터 요소 유형(Adobe Experience Platform Web SDK 확장에서 제공)을 사용하여 스키마와 일치하는 적절한 개체를 작성합니다.

다음을 클릭합니다. [!UICONTROL 변경 내용 유지] 단추를 클릭합니다.

## 규칙을 저장합니다

이제 규칙을 완료해야 합니다.

![페이지 조회수 규칙](../../../assets/implementation-strategy/page-viewed-rule.png)

을(를) 클릭하여 규칙 저장 [!UICONTROL 저장].

## 프로세스 반복

위에 설명된 프로세스를 반복하여 제품을 보고, 장바구니를 열고, 제품을 장바구니에 추가할 때 규칙을 만듭니다. 규칙 간의 유일한 차이는 규칙 이름, 에 입력한 값입니다. [!UICONTROL 등록할 이벤트/키] 의 필드 [!UICONTROL 데이터 푸시됨] 이벤트 및 [!UICONTROL 유형] 의 필드 [!UICONTROL 이벤트 보내기] 작업. 각 규칙의 값은 다음과 같습니다.

제품 보기 규칙:

* **규칙 이름**: _제품 조회함_
* **등록할 이벤트/키** 다음 범위 내 [!UICONTROL 데이터 푸시됨] 이벤트: `productViewed`
* **유형** 다음 범위 내 [!UICONTROL 이벤트 보내기] 작업: `commerce.productViews`

장바구니 열림 규칙:

* **규칙 이름**: _장바구니 열림_
* **등록할 이벤트/키** 다음 범위 내 [!UICONTROL 데이터 푸시됨] 이벤트: `cartOpened`
* **유형** 다음 범위 내 [!UICONTROL 이벤트 보내기] 작업: `commerce.productListOpens`

장바구니에 추가된 제품:

* **규칙 이름**: _장바구니에 추가된 제품_
* **등록할 이벤트/키** 다음 범위 내 [!UICONTROL 데이터 푸시됨] 이벤트: `productAddedToCart`
* **유형** 다음 범위 내 [!UICONTROL 이벤트 보내기] 작업: `commerce.productListAdds`

다음으로, 의 추적 클릭을 처리합니다. [!UICONTROL 앱 다운로드] 링크를 클릭합니다.
