---
title: Experience Platform 보증을 사용하여 웹 SDK 구현 유효성 검사
description: Adobe Experience Platform Assurance를 사용하여 Platform Web SDK 구현의 유효성을 검사하는 방법을 알아봅니다. 이 단원은 Web SDK를 사용하여 Adobe Experience Cloud 구현 자습서의 일부입니다.
feature: Web SDK,Tags,Assurance
source-git-commit: 4361d8e688ff2c2f3b5472f2cfff246efa627c7f
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---

# Experience Platform 보증을 사용하여 웹 SDK 구현 유효성 검사


## 보증 세션 시작

Adobe Experience Platform Assurance는 데이터를 수집하거나 경험을 제공하는 방법을 검사, 증명, 시뮬레이션 및 확인하는 데 도움이 되는 Adobe Experience Cloud의 제품입니다.

자세한 내용 [Adobe 보증](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html?lang=en).

Edge Trace를 활성화할 때마다 백그라운드에서 Assurance 세션이 시작됩니다.

보증 세션을 보려면

1. Edge Trace 가 활성화된 경우 맨 위에 발신 링크 아이콘이 표시됩니다. Assurance를 열려면 아이콘을 선택합니다. 브라우저에서 새 탭이 열립니다.

   ![보증 세션 시작](assets/validate-debugger-start-assurnance.png)

1. Adobe 응답 핸들이라는 이벤트가 있는 행을 선택합니다.
1. 메뉴가 오른쪽에 표시됩니다. 다음 항목 선택 `+` 다음 옆에 서명 `[!UICONTROL ACPExtensionEvent]`
1. 을 선택하여 드릴다운 `[!UICONTROL payload > 0 > payload > 0 > namespace]`. 마지막 항목 아래에 표시된 ID `0` 다음에 해당 `ECID`. 아래에 표시되는 값으로 알 수 있습니다. `namespace` 일치 `ECID`

   ![보증 유효성 확인 ECID](assets/validate-assurance-ecid.png)

   >[!CAUTION]
   >
   >창의 너비로 인해 잘린 ECID 값이 표시될 수 있습니다. 인터페이스에서 핸들 막대를 선택하고 왼쪽으로 드래그하여 전체 ECID를 표시하면 됩니다.

향후 단원에서는 Assurance를 사용하여 데이터 스트림에서 활성화된 Adobe 애플리케이션에 도달하기 위해 완전히 처리된 페이로드를 확인합니다.

이제 페이지에서 실행되는 XDM 개체와 데이터 수집의 유효성을 검사하는 방법에 대한 지식이 있으면 Platform Web SDK를 사용하여 개별 Adobe 애플리케이션을 설정할 수 있습니다.