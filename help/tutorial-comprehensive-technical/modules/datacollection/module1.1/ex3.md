---
title: 기초 - Adobe Experience Platform 데이터 수집 및 Web SDK 확장 설정 - Adobe Experience Platform 데이터 수집 소개
description: 기초 - Adobe Experience Platform 데이터 수집 및 Web SDK 확장 설정 - Adobe Experience Platform 데이터 수집 소개
kt: 5342
doc-type: tutorial
exl-id: 391c79d6-9c42-465e-bce8-60fa6474979c
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 9%

---

# 1.1.3 - Adobe Experience Platform 데이터 수집 소개

## 컨텍스트

이제 Adobe Experience Platform 데이터 수집의 기본 구성 요소를 자세히 살펴보고 데모 웹 사이트에 설치된 항목을 파악해 보겠습니다. Adobe Experience Platform 웹 SDK 확장을 자세히 살펴보고 데이터 요소와 규칙을 구성하고 라이브러리를 게시하는 방법을 알아봅니다.

## 1.1.3.1 - Adobe Experience Platform 웹 SDK 확장

확장은 Adobe Experience Platform 데이터 수집 인터페이스와 라이브러리 기능을 확장하는 패키지화된 코드 세트입니다. Adobe Experience Platform 데이터 수집은 플랫폼이며 확장은 플랫폼에서 실행되는 앱과 같습니다. 자습서에서 사용되는 모든 확장은 Adobe에서 만들고 관리하지만 서드파티는 고유한 확장을 만들어 Adobe Experience Platform 데이터 수집 사용자가 관리해야 하는 사용자 지정 코드의 양을 제한할 수 있습니다.

[Adobe Experience Platform 데이터 수집](https://experience.adobe.com/launch/)(으)로 이동하여 **태그**&#x200B;를 선택합니다.

이전에 보았던 Adobe Experience Platform 데이터 수집 속성 페이지입니다.

![속성 페이지](./images/launch1.png)

**시작하기**&#x200B;에서 데모 시스템은 웹 사이트용 클라이언트 속성과 모바일 앱용 클라이언트 속성 두 개를 만들었습니다. **[!UICONTROL 검색]** 상자에서 `--aepUserLdap--`을(를) 검색하여 찾으십시오.
**Web** 속성을 열려면 클릭하세요.

![검색 상자](./images/property6.png)



그러면 속성 개요 페이지가 표시됩니다. 왼쪽 레일에서 **[!UICONTROL 확장]**&#x200B;을 클릭한 다음 **Adobe Experience Platform Web SDK**&#x200B;를 클릭한 다음 **[!UICONTROL 구성]**&#x200B;을 클릭합니다.

![속성 개요 페이지](./images/property7.png)

Adobe Experience Platform 웹 SDK를 시작합니다! [시작](./../../../modules/gettingstarted/gettingstarted/ex2.md)에서 만든 데이터 스트림과 고급 구성으로 확장을 구성할 수 있습니다.

기본 Edge 도메인은 항상 **edge.adobedc.net**&#x200B;입니다. Adobe Experience Cloud 또는 Adobe Experience Platform 환경에서 CNAME 구성을 구현한 경우 **[!UICONTROL Edge 도메인]**&#x200B;을 업데이트해야 합니다.

인스턴스의 Edge 도메인이 기본 도메인과 다른 경우 여기에서 Edge 도메인을 업데이트하십시오. 확실하지 않은 경우 기본 도메인을 사용합니다. Edge 도메인을 사용하면 자사 추적 서버를 구성한 다음 백엔드에서 CNAME 구성을 사용하여 데이터를 Adobe에 수집할 수 있습니다.

![확장 홈](./images/property9edgedomain.png)

**[!UICONTROL 데이터스트림]**&#x200B;에서 이미 **시작하기** 섹션에서 데이터스트림을 선택했습니다. 각 환경에 대해 **[!UICONTROL 데이터 스트림]** 상자의 목록에서 이 데이터 스트림 `--aepUserLdap-- - Demo System Datastream`을(를) 선택했습니다.

확장 보기로 돌아가려면 **[!UICONTROL 저장]**&#x200B;을 클릭하세요.

![확장 홈](./images/property9edge.png)

## 1.1.3.2 데이터 요소

데이터 요소는 데이터 사전(또는 데이터 맵)의 기본 구성단위입니다. 데이터 요소를 사용하여 마케팅 및 광고 기술 전반에서 데이터를 수집, 구성 및 전달합니다.

단일 데이터 요소는 쿼리 문자열, URL, 쿠키 값, JavaScript 변수 등에 값을 매핑할 수 있는 변수입니다. Adobe Experience Platform 데이터 수집 전체에서 해당 변수 이름으로 이 값을 참조할 수 있습니다. 이 데이터 요소 컬렉션은 규칙(이벤트, 조건 및 작업)을 작성하는 데 사용할 수 있는 정의된 데이터 사전이 됩니다. 이 데이터 사전은 속성에 추가한 확장에 사용하기 위해 모든 Adobe Experience Platform 데이터 수집에서 공유됩니다.

이제 기존 데이터 요소를 Web SDK에 친숙한 형식으로 편집하려고 합니다.

왼쪽 레일에서 데이터 요소 를 클릭하여 데이터 요소 페이지로 이동합니다.

![데이터 요소 홈 페이지](./images/dataelement1.png)

>[!NOTE]
>
>이 연습에서는 데이터 요소만 편집하고 있지만 이 페이지에서 데이터 사전에 새 변수를 추가하는 데 사용되는 **[!UICONTROL 데이터 요소 추가]** 단추가 표시됩니다. 그런 다음 Adobe Experience Platform 데이터 수집 전체에서 사용할 수 있습니다. 이미 존재하는 다른 데이터 요소 중 일부를 자유롭게 살펴볼 수 있으며, 대부분 로컬 저장소를 데이터 소스로 사용합니다.

검색 창에서 **XDM - 제품 보기**&#x200B;를 입력하고 반환되는 데이터 요소를 클릭합니다.

![ruleArticlePages 검색](./images/dataelement2.png)

이 화면에서는 편집할 XDM 개체를 보여 줍니다. XDM(Experience Data Model)은 이 기술 자습서 전체에서 훨씬 더 자세히 살펴볼 개념이지만 지금은 Adobe Experience Platform 웹 SDK에 필요한 형식으로 이해하는 것으로 충분합니다. 데모 웹 사이트의 문서 페이지에 수집된 데이터에 추가 정보를 추가합니다.

트리의 맨 아래에 있는 **web** 옆에 있는 더하기 단추를 클릭합니다.

**webPageDetails** 옆에 있는 더하기 단추를 클릭합니다.

**siteSection**&#x200B;을 클릭합니다. 이제 **siteSection**&#x200B;이(가) 아직 데이터 요소에 연결되어 있지 않습니다. 그걸 바꿀게요.

![사이트 섹션으로 이동](./images/dataelement3.png)

위로 스크롤하여 `%Product Category%` 텍스트를 입력합니다. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

![저장](./images/dataelement4.png)

이 시점에서 Adobe Experience Platform 웹 SDK 확장이 설치되고 XDM 구조에 대한 데이터를 수집하도록 데이터 요소를 업데이트했습니다. 다음으로, 데이터를 올바른 시간에 전송할 규칙을 확인해 보겠습니다.

## 1.1.3.3 규칙

Adobe Experience Platform 데이터 수집은 규칙 기반 시스템입니다. 사용자 상호 작용과 관련 데이터를 찾습니다. 규칙에 요약된 기준이 충족되면, 규칙이 정의한 확장, 스크립트 또는 클라이언트측 코드를 트리거합니다.

서로 다른 제품을 하나의 솔루션으로 통합하는 마케팅 및 광고 기술에 대한 데이터와 기능을 통합하는 규칙을 빌드합니다.

문서 페이지에서 데이터를 보내는 규칙을 분류해 보겠습니다.

왼쪽 레일에서 **[!UICONTROL 규칙]**&#x200B;을 클릭합니다.

`Product View`에 대해 **[!UICONTROL 검색]**&#x200B;합니다.

반환되는 규칙을 클릭합니다.

![미디어 - 문서 페이지 규칙 검색](./images/rule1.png)

이 규칙을 구성하는 개별 요소를 살펴보자.

모든 규칙: 지정된 **[!UICONTROL Event]**&#x200B;이 발생하면 **[!UICONTROL Conditions]**&#x200B;이 평가되고 필요한 경우 지정된 **[!UICONTROL Actions]**&#x200B;이(가) 수행됩니다.

![미디어 - 문서 페이지 규칙](./images/rule2.png)

이벤트 **코어 - 사용자 지정 이벤트**&#x200B;를 클릭합니다. 이 뷰는 로드됩니다.

**이벤트 유형** 드롭다운을 클릭합니다.

조건이 true인 경우 Adobe Experience Platform 데이터 수집에 신호를 보내 작업을 실행할 수 있는 몇 가지 표준 상호 작용이 나열됩니다.

![이벤트](./images/rule3.png)

규칙으로 돌아가려면 **[!UICONTROL 취소]**&#x200B;를 클릭하십시오.

**제품 보기 경험 이벤트 보내기** 작업을 클릭합니다.

![이벤트 보내기 작업](./images/rule5a.png)

여기에서 Adobe Experience Platform 웹 SDK에서 Edge로 전송하는 데이터를 볼 수 있습니다. 특히 웹 SDK의 **alloy** **[!UICONTROL 인스턴스]**&#x200B;를 사용합니다. 이벤트 **[!UICONTROL Type]**&#x200B;이(가) **Commerce 제품(장바구니) 보기**(으)로 설정되어 있으며, 보내는 XDM 데이터는 이전에 변경한 **XDM - 제품 보기** 데이터 요소입니다.

![이벤트 보내기 작업](./images/rule5.png)

이제 규칙을 살펴보았으므로, Adobe Experience Platform 데이터 수집에서 모든 변경 사항을 게시할 수 있습니다.

## 라이브러리의 1.1.3.4 Publish

마지막으로, 방금 업데이트한 규칙 및 데이터 요소의 유효성을 검사하려면 속성에 편집된 항목이 들어 있는 라이브러리를 게시해야 합니다. Adobe Experience Platform 데이터 수집의 **[!UICONTROL 게시]** 섹션에서 수행해야 하는 몇 가지 빠른 단계가 있습니다.

왼쪽 탐색에서 **[!UICONTROL 게시 흐름]**&#x200B;을 클릭합니다

**Main**(이)라는 기존 라이브러리를 클릭합니다.

![라이브러리 액세스](./images/publish1.png)

**변경된 모든 리소스 추가** 단추를 클릭합니다. 다음,
**개발을 위한 저장 및 빌드** 단추를 클릭합니다.

![라이브러리 액세스](./images/publish1a.png)

라이브러리를 빌드하는 데 몇 분 정도 걸릴 수 있으며 완료되면 라이브러리 이름 왼쪽에 녹색 점이 표시됩니다.

![컨텐츠 라이브러리](./images/publish2.png)

게시 플로우 화면에서 볼 수 있듯이 Adobe Experience Platform 데이터 수집에는 이 자습서의 범위를 벗어나는 게시 프로세스가 많습니다. 개발 환경에서 단일 라이브러리를 사용할 예정입니다.

다음 단계: [1.1.4 클라이언트측 웹 데이터 수집](./ex4.md)

[모듈 1.1로 돌아가기](./data-ingestion-launch-web-sdk.md)

[모든 모듈로 돌아가기](./../../../overview.md)
