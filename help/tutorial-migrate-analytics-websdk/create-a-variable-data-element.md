---
title: 변수 데이터 요소 만들기
description: 여러 규칙에 빌드될 데이터 요소를 추가한 다음 Edge Network으로 보내고 Adobe Analytics으로 전달합니다.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16759
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# 변수 데이터 요소 만들기

여러 규칙에 빌드된 다음 Edge Network으로 전송되고 Adobe Analytics으로 전달되는 데이터 요소를 추가합니다.

이 데이터 요소는 &quot;Data&quot; 개체를 만듭니다. 이 개체는 Adobe Analytics 변수(props, eVar, event 등)를 다시 Adobe Analytics 및 Adobe Target에 전달하는 데 사용됩니다. 따라서 Analytics의 AppMeasurement 구현에서 &quot;s 개체&quot;를 작성하는 것과 마찬가지로, 여러 규칙에서 액세스하고 업데이트할 변수 개체라는 이 유형을 작성하고 이 유형을 사용하여 prop 및 eVar를 Analytics에 채울 수 있습니다.

1. 데이터 수집 인터페이스의 왼쪽 탐색에서 **데이터 요소**&#x200B;를 클릭합니다.

   기존 데이터 요소를 모두 볼 수 있는 데이터 요소 랜딩 페이지로 이동합니다. 마이그레이션을 용이하게 하는 새로운 데이터 요소를 만들어야 합니다. **데이터 요소 추가**&#x200B;를 클릭합니다.

   ![데이터 요소 추가](assets/add-new-data-alement.jpg)

1. 데이터 요소를 구성합니다.
   1. 원하는 대로 데이터 요소에 이름을 지정합니다. 이렇게 하면 페이지에서 데이터를 작성하고 이것이 &quot;변수&quot; 유형이 된다는 것을 기억하는 데 도움이 됩니다. 이 자습서에서는 이 자습서를 **페이지 보기 데이터 변수**&#x200B;라고 합니다.
   1. 확장 드롭다운에서 **Adobe Experience Platform Web SDK**&#x200B;을(를) 선택합니다.
   1. **데이터 요소 유형** 드롭다운에서 **변수**&#x200B;을(를) 선택합니다.
   1. 오른쪽 패널에서 **데이터** 라디오 단추를 선택합니다.
   1. **Adobe Analytics** 솔루션과 마이그레이션 중인 다른 솔루션(예: 이 스크린샷에 표시되는 **Adobe Target**)을 확인하십시오.
1. **저장**&#x200B;을 클릭합니다.

   ![변수 데이터 요소 구성](assets/configure-variable-data-element.jpg)
