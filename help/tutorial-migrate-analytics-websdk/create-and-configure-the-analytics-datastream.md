---
title: 데이터 스트림 만들기 및 구성
description: 웹 사이트 데이터를 Adobe Analytics으로 라우팅할 수 있도록 새 데이터 스트림을 만들고 구성하는 방법에 대해 알아봅니다.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16757
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---


# 데이터 스트림 만들기 및 구성

웹 사이트 데이터를 Adobe Analytics으로 라우팅할 수 있도록 새 데이터 스트림을 만들고 구성하는 방법에 대해 알아봅니다.

이 단원에서는 데이터가 웹 사이트에서 Adobe Edge으로 이동한 다음 여기에서 Adobe Analytics으로 라우팅되도록 시스템을 만들고 구성하는 방법에 대해 알아봅니다.

![아키텍처 다이어그램](assets/architecture_diagram.jpg)

## 새 개발 데이터스트림 만들기

1. Adobe 데이터 수집 인터페이스 열기
   1. 브라우저에서 https://experience.adobe.com 로 이동합니다.
   1. 페이지 맨 위에서 올바른 조직이 선택되었는지 확인합니다(예: 아래 이미지에서 Adobe 프로덕션 - 기술 마케팅 데모).
   1. &quot;9개 점&quot;(응용 프로그램 전환기)을 클릭하고 **데이터 수집**&#x200B;을 선택합니다.

      ![데이터 수집으로 이동](assets/navigate-to-data-collection.jpg)

1. 왼쪽 탐색 영역에서 **[!UICONTROL 데이터스트림]**(으)로 이동
1. **[!UICONTROL 새 데이터 스트림]** 선택
1. 원하는 **[!UICONTROL 이름]**&#x200B;을(를) 입력하고 이 이름을 웹 SDK 개발 환경에 사용한다는 표시기를 포함하십시오. 예를 들어, 아래 표시된 대로 사이트 뒤에 이 이름을 지정할 수 있습니다. 이 이름은 나중에 태그 속성에서 웹 SDK 확장을 구성할 때 참조되므로 기록해 둡니다. 원하는 경우 설명을 입력합니다.

   >[!NOTE]
   >
   >[데이터 수집을 위한 데이터 준비](https://experienceleague.adobe.com/ko/docs/platform-learn/data-collection/edge-network/data-prep) 기능을 사용하는 경우 스키마를 선택하기만 하면 됩니다. 이 작업은 이 자습서에서는 수행하지 않습니다. 자세한 내용은 링크를 참조하십시오.

1. **[!UICONTROL 저장]** 선택

   ![데이터 스트림 만들기](assets/create-new-datastream.jpg)

1. 데이터 스트림을 저장하면 아직 구성된 서비스가 없음을 알리는 새 화면이 표시됩니다. 즉, 데이터가 Edge 서버로 전송되지만 서비스를 추가할 때까지 애플리케이션에 전송되지 않습니다. 이제 Adobe Analytics으로 데이터를 전송하도록 데이터 스트림을 구성하겠습니다. **[!UICONTROL 서비스 추가]**&#x200B;를 클릭합니다.
   ![서비스 추가](assets/datastream-add-service.jpg)
1. 서비스 드롭다운 메뉴에서 **[!UICONTROL Adobe Analytics]**&#x200B;을(를) 선택합니다.
1. 보고서 세트 ID 필드에 [유효성 검사 보고서 세트 만들기](create-a-validation-report-suite.md) 활동에서 만든 유효성 검사 보고서 세트의 ID(제목이 아니라 보고서 세트 ID)를 입력합니다. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

## 스테이징 및 프로덕션 데이터스트림

이제 두 번 더 **동일한 단계를 다시**&#x200B;하려고 합니다. 스테이징 환경에서 한 번, 프로덕션 환경에서 한 번. 다음은 이러한 두 개의 데이터 스트림을 추가로 설정할 때 참조할 수 있는 몇 가지 사항입니다.

### 스테이징 데이터 스트림

* 데이터 스트림의 이름을 지정할 때(및 설명을 추가할 때) &quot;development&quot; 대신 &quot;staging&quot;을 추가하는 차이점을 사용하여 동일한 이름을 가질 수/있어야 합니다.
* 이전과 마찬가지로 Adobe Analytics 서비스를 추가하고 보고서 세트를 동일한 개발 보고서 세트로 설정합니다.
* Adobe Analytics 보고서에서 스테이징 숫자를 찾기 위한 환경을 더 깔끔하게 정리하려면, 스테이징용으로만 새 보고서 세트를 만든 다음 이 데이터스트림의 Analytics 서비스에서 해당 보고서 세트를 가리키는지 확인할 수 있습니다.

### 프로덕션 데이터스트림

* 데이터스트림의 이름을 지정할 때(및 설명을 추가할 때) &quot;development&quot; 대신 &quot;production&quot;을 추가하는 차이점을 사용하여 동일한 이름을 가질 수/있어야 합니다.
* 데이터를 매핑할 보고서 세트를 선택할 때 개발 보고서 세트나 새 보고서 세트를 선택하는 대신 이 데이터 스트림을 AppMeasurement 구현에서 제공하는 **current** 프로덕션 보고서 세트에 매핑할 수 있습니다. 이러한 방식으로 마이그레이션을 완료하고 테스트하여 숫자가 만족스러우면 이전 AppMeasurement 코드를 제거하고 태그 라이브러리를 프로덕션으로 보내면 새 프로덕션 데이터를 동일한 프로덕션 보고서 세트에 제공할 수 있으므로 이전 구현과 새 구현 간에 연속성을 갖게 됩니다.
