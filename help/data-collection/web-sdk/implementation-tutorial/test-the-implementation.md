---
title: 구현 테스트
description: 구현 테스트
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: e2213c23-d395-4c57-8c6c-0319cd0fb0ac
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 2%

---

# 구현 테스트

이제 웹 페이지를 설정하고 Adobe Experience Platform 태그 라이브러리를 배포했으므로 구현을 테스트할 차례입니다.

브라우저에서 제품 페이지를 엽니다. 다음을 클릭하여 수행할 수 있습니다. _파일_ 그러면 _파일 열기..._ 또는 브라우저에서 웹 서버에 페이지를 호스팅하고 적절한 URL을 입력할 수 있습니다.

페이지가 로드되면 다음과 같은 메시지가 표시됩니다.

![웹 페이지](../../assets/implementation-strategy/webpage.png)

예쁘지는 않지만, 그 일을 해낼 거예요.

## 페이지 보기 및 제품 보기 이벤트 Inspect

브라우저에서 개발자 도구를 열고 네트워크 패널을 클릭합니다. 페이지를 새로 고칩니다.

이 시점에서 다음 네 가지 요청이 표시됩니다.

1. product.html - 웹 페이지입니다.
2. launch-##########-development.js - Launch 라이브러리.
3. interact - 서버로 전송되는 페이지 보기 이벤트입니다.
4. interact - 서버로 전송되는 제품 보기 이벤트입니다.

각 요청의 페이로드를 언제든지 검사하십시오. 첫 번째 `interact` 요청하십시오. 페이로드가 과 함께 전송되는 것을 볼 수 있습니다. `eventType` / `web.webpagedetails.pageViews`.

![페이지 보기 요청 검사](../../assets/implementation-strategy/webpage-page-viewed-inspection.png)

다음 기간 동안 `interact` 요청하십시오. 페이로드가 과 함께 전송되는 것을 볼 수 있습니다. `eventType` / `commerce.productViews`.

![제품 보기 요청 검사](../../assets/implementation-strategy/webpage-product-view-inspection.png)

제품 정보를 포함하여 전송되는 나머지 데이터를 자유롭게 살펴보십시오.

## 장바구니 열기 및 장바구니에 추가 이벤트 Inspect

이제 _장바구니에 추가_ 단추를 클릭합니다.

첫 번째에 `eventType` / `commerce.productListOpens` (새 장바구니 열기) 및 `eventType` / `commerce.productListAdds` (제품을 장바구니에 추가).

## Inspect 앱 링크 다운로드 클릭 이벤트

브라우저에 따라 현재 페이지에서 멀리 이동하는 링크를 클릭하면 네트워크 패널이 지워질 수 있습니다. 페이지에서 나가기 직전에 발생하는 링크 클릭 이벤트에 대한 네트워크 요청을 검사하려면 페이지 간 네트워크 로그를 유지하도록 브라우저를 구성해야 합니다. 다음 중 하나를 선택하여 이 작업을 수행합니다. _로그 유지_ 네트워크 패널(Chrome, Safari, Edge)에서 확인란을 선택하거나 톱니바퀴 아이콘을 클릭하고 _로그 유지_ 표시된 메뉴의 항목(Firefox)입니다.

이제 _앱 다운로드_ 링크를 클릭합니다.

하나 더 보셔야겠네요 `interact` 네트워크 패널에 요청이 표시됩니다. 요청을 검사하면 다음을 찾을 수 있습니다. `eventType` / `web.webinteraction.linkClicks` 클릭된 링크에 대한 세부 정보도 제공합니다.

## 데이터가 Adobe Experience Platform 데이터 세트에 도착하는지 확인

이제 요청이 전송되므로, 만든 Adobe Experience Platform 데이터 세트에 데이터가 안전하게 도착하는지 여부도 확인할 수 있습니다. 다음 위치로 이동하여 시작 [!UICONTROL 데이터 세트] Adobe Experience Platform 내에서 보기.

이전에 만든 데이터 세트를 선택합니다.

몇 분 정도 기다려야 할 수 있지만, 곧 데이터 세트에 처리 및 삽입되는 데이터의 표시가 표시됩니다. 처리가 성공했는지 아니면 실패했는지도 확인해야 합니다. 실패했다면 왜 실패했는지 알 수 있습니다. 일반적으로 실패는 보내는 데이터가 스키마와 일치하지 않기 때문에 발생하며 그에 따라 데이터나 스키마를 조정해야 합니다.

![데이터 세트 수집](../../assets/implementation-strategy/dataset-ingestion.png)

## Adobe Experience Platform Debugger 확장 사용

브라우저와 Adobe 서버 모두에서 구현이 어떻게 작동하는지 자세히 알아보려면 Adobe Experience Platform Debugger 브라우저 확장 기능을 확인하십시오!

[Chrome용 Adobe Experience Platform Debugger 확장 기능](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

[Firefox용 Adobe Experience Platform Debugger 확장](https://addons.mozilla.org/ko-KR/firefox/addon/adobe-experience-platform-dbg/)
