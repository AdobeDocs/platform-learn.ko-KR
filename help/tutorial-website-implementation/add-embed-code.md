---
title: 포함 코드 추가
description: 태그 속성의 포함 코드를 가져와 웹 사이트에서 구현하는 방법을 알아봅니다. 이 단원은 웹 사이트에 Experience Cloud 구현 자습서의 일부입니다.
exl-id: a2959553-2d6a-4c94-a7df-f62b720fd230
source-git-commit: 277f5f2c07bb5818e8c5cc129bef1ec93411c90d
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 43%

---

# 포함 코드 추가

이 단원에서는 태그 속성의 개발 환경에 대한 비동기 포함 코드를 구현합니다. 이 과정에서 태그의 두 가지 주요 개념인 환경과 포함 코드에 대해 알아봅니다.

>[!NOTE]
>
>Adobe Experience Platform Launch은 데이터 수집 기술군으로 Adobe Experience Platform에 통합되고 있습니다. 이 콘텐츠를 사용하는 동안 알아야 하는 몇 가지 용어 변경 사항이 인터페이스에 롤아웃되었습니다.
>
> * Platform launch(Client Side)가 이제 **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ko)**&#x200B;입니다.
> * 이제 platform launch 서버측이 **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=ko)**&#x200B;입니다.
> * 이제 Edge 구성이 **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=ko)**&#x200B;입니다.

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* 태그 속성에 대한 포함 코드 가져오기
* 개발, 스테이징 및 프로덕션 환경의 차이점 이해
* html 문서에 태그 포함 코드 추가
* html 문서의 `<head>`에서 다른 코드와 관련이 있는 태그 포함 코드의 최적 위치 설명

## 포함 코드 복사

포함 코드는 태그에서 빌드하는 논리를 로드 및 실행하기 위해 웹 페이지에서 지정하는 `<script>` 태그입니다. 라이브러리를 비동기식으로 로드하는 경우 브라우저에서 페이지를 계속 로드하고 태그 라이브러리를 검색하여 병렬로 실행합니다. 이 경우 `<head>`에 지정하는 포함 코드가 한 개만 있습니다. 태그가 동기적으로 배포되면 두 개의 포함 코드가 있습니다. 하나는 `<head>`에 지정하고 다른 하나는 `</body>` 앞에 지정합니다.

속성 개요 화면에서 왼쪽 탐색의 **[!UICONTROL 환경]**&#x200B;을 클릭하여 환경 페이지로 이동합니다. 개발, 스테이징 및 프로덕션 환경은 사용자를 위해 사전에 만들어졌습니다.

![위쪽 탐색에서 Environments 클릭](images/launch-environments.png)

개발, 스테이징 및 프로덕션 환경은 코드 개발 및 릴리스 프로세스에서 일반적인 환경에 해당합니다. 코드는 개발 환경에서 개발자가 처음 작성합니다. 개발자가 코드 작업을 마치면 QA 및 다른 팀이 검토할 수 있도록 스테이징 환경으로 보냅니다. QA와 다른 팀이 만족하면 코드가 프로덕션 환경에 게시됩니다. 이 환경은 방문자가 웹 사이트를 방문할 때 경험하는 공개 환경입니다.

태그는 추가 개발 환경을 허용하므로 여러 개발자가 동시에 서로 다른 프로젝트에서 작업하는 대기업에서 유용합니다.

이러한 환경은 자습서를 완료하는 데 필요한 유일한 환경입니다. 환경에서는 다른 URL에서 호스팅되는 태그 라이브러리의 다른 작업 버전을 사용할 수 있으므로 새로운 기능을 안전하게 추가하여 적합한 사용자(예: 개발자, QA 엔지니어, 대중 등)에게 제공할 수 있습니다. 제공할 수 있습니다.

이제 포함 코드를 복사하겠습니다.

1. **[!UICONTROL Development]** 행에서 Install 아이콘 ![Install 아이콘](images/launch-installIcon.png)을 클릭하여 모달을 엽니다.

1. 태그는 기본적으로 비동기 포함 코드로 설정됩니다

1. 복사 아이콘 ![Copy 아이콘](images/launch-copyIcon.png)을 클릭하여 포함 코드를 클립보드에 복사합니다.

1. **[!UICONTROL 닫기]**&#x200B;를 클릭하여 모달을 닫습니다.

   ![Install 아이콘](images/launch-copyInstallCode.png)

## 샘플 HTML 페이지의 `<head>`에서 포함 코드 구현

포함 코드는 속성을 공유할 모든 HTML 페이지의 `<head>` 요소에 구현해야 합니다. 사이트에서 전체적으로 `<head>`을(를) 제어하는 템플릿 파일이 한 개 또는 여러 개 있을 수 있으므로 태그를 추가하는 프로세스를 간단하게 만들 수 있습니다.

샘플 html 페이지 코드를 복사하여 코드 편집기에 붙여 넣습니다. [Brackets](https://brackets.io/)는 무료 오픈 소스 편집기입니다. 하나 필요하다면 다운로드하십시오.

+++샘플 html 페이지 코드

```html
<!doctype html>
<html lang="en">
<head>
    <title>Tags: Sample HTML Page</title>
    <!--Preconnect and DNS-Prefetch to improve page load time. REPLACE "techmarketingdemos" WITH YOUR OWN AAM PARTNER ID, TARGET CLIENT CODE, AND ANALYTICS TRACKING SERVER-->
    <link rel="preconnect" href="//dpm.demdex.net">
    <link rel="preconnect" href="//fast.techmarketingdemos.demdex.net">
    <link rel="preconnect" href="//techmarketingdemos.demdex.net">
    <link rel="preconnect" href="//cm.everesttech.net">
    <link rel="preconnect" href="//techmarketingdemos.tt.omtrdc.net">
    <link rel="preconnect" href="//techmarketingdemos.sc.omtrdc.net">
    <link rel="dns-prefetch" href="//dpm.demdex.net">
    <link rel="dns-prefetch" href="//fast.techmarketingdemos.demdex.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.demdex.net">
    <link rel="dns-prefetch" href="//cm.everesttech.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.tt.omtrdc.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.sc.omtrdc.net">
    <!--/Preconnect and DNS-Prefetch-->
    <!--Data Layer to enable rich data collection and targeting-->
    <script>
    var digitalData = {
        "page": {
            "pageInfo" : {
                "pageName": "Home"
                }
            }
    };
    </script>
    <!--/Data Layer-->
    <!--jQuery or other helper libraries-->
    <script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
    <!--/jQuery-->
    <!--Tags Header Embed Code: REPLACE THE NEXT LINE WITH THE EMBED CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
    <!--/Tags Header Embed Code-->
</head>
<body>
    <h1>Tags: Sample HTML Page</h1>
    <p>This is a very simple page to demonstrate basic implementation concepts of Tags</p>
    <p>See <a href="https://docs.adobe.com/content/help/ko-KR/experience-cloud/implementing-in-websites-with-launch/index.html">Implementing the Experience Cloud in Websites with Tags</a> for the complete tutorial</p>
</body>
</html>
```

+++

34행 또는 그 전후에 있는 기존 포함 코드를 클립보드에 있는 포함 코드로 바꾸고 페이지를 저장합니다. 이제 웹 브라우저에서 페이지를 엽니다. `file://` 프로토콜을 사용하여 페이지를 로드하는 경우 코드 편집기에서 포함 코드 URL의 시작 부분에 &quot;https:&quot;를 추가해야 합니다. 샘플 페이지의 33~36라인은 다음과 비슷합니다.

```html
    <!--Tags Header Embed Code: REPLACE LINE 39 WITH THE EMBED CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="https://assets.adobedtm.com/launch-ENa21cfed3f06f4ddf9690de8077b39e81-development.min.js" async></script>
    <!--/Tags Header Embed Code-->
```

웹 브라우저의 개발자 도구를 열고 네트워크 탭으로 이동합니다. 이 시점에서 태그 환경 URL에 대한 404 오류가 표시됩니다.
![404 오류](images/samplepage-404.png)

이 태그 환경에 라이브러리를 아직 빌드하지 않았기 때문에 404 오류가 발생할 수 있습니다. 다음 단원에서 이 작업을 수행합니다. 404 오류 대신 &quot;failed&quot; 메시지가 표시되는 경우 포함 코드에 `https://` 프로토콜을 추가하는 것을 잊어버렸을 수 있습니다. 즉, `file://` 프로토콜을 사용하여 샘플 페이지를 로드하는 경우에만 `https://` 프로토콜을 지정해야 합니다. 404 오류가 나타날 때까지 페이지를 변경하고 다시 로드합니다.

## 태그 구현 우수 사례

샘플 페이지에 나와 있는 태그 구현 모범 사례 중 일부를 잠시 살펴보겠습니다.

* **데이터 레이어**:

   * Analytics, Target 및 기타 마케팅 솔루션에서 변수를 채우는 데 필요한 모든 특성이 들어 있는 데이터 계층을 사이트에 만들 것을 *강력하게*&#x200B;권장합니다. 이 샘플 페이지에는 매우 간단한 데이터 계층만 들어 있지만, 실제 데이터 계층에는 페이지, 방문자, 장바구니 세부 사항 등에 대한 여러 가지 자세한 내용이 들어 있을 수 있습니다. 데이터 계층에 대한 자세한 내용은 [Customer Experience 디지털 데이터 계층 1.0](https://www.w3.org/2013/12/ceddl-201312.pdf)을 참조하십시오.

   * Experience Cloud 솔루션으로 수행할 수 있는 작업을 극대화하려면 태그 포함 코드 앞에 데이터 레이어를 정의하십시오.

* **JavaScript 도우미 라이브러리**: JQuery와 같은 라이브러리를 페이지의 `<head>`에서 이미 구현한 경우에는 태그 및 Target에서 해당 구문을 활용하기 위해 태그 앞에 로드하십시오

* **HTML5 doctype**: HTML5 doctype은 Target에 필요합니다.

* **preconnect and dns-prefetch**: preconnect 및 dns-prefetch를 사용하여 페이지 로드 시간을 개선합니다. 참고 항목: [https://w3c.github.io/resource-hints/](https://w3c.github.io/resource-hints/)

* **비동기 Target 구현을 위한 사전 숨김 코드 조각**: Target 단원에서 이에 대해 자세히 알아보겠지만, Target이 비동기 태그 포함 코드를 통해 배포되면 태그 포함 코드 앞에 페이지에 사전 숨김 코드 조각을 하드코딩하여 콘텐츠 깜박임을 관리해야 합니다

다음은 이러한 모범 사례의 상태를 제안된 순서로 보여주는 요약 내용입니다. 계정별 세부 사항에 대한 자리 표시자가 일부 있습니다.

```html
<!doctype html>
<html lang="en">
<head>
    <title>Basic Demo</title>
    <!--Preconnect and DNS-Prefetch to improve page load time. REPLACE "techmarketingdemos" WITH YOUR OWN AAM PARTNER ID, TARGET CLIENT CODE, AND ANALYTICS TRACKING SERVER-->
    <link rel="preconnect" href="//dpm.demdex.net">
    <link rel="preconnect" href="//fast.techmarketingdemos.demdex.net">
    <link rel="preconnect" href="//techmarketingdemos.demdex.net">
    <link rel="preconnect" href="//cm.everesttech.net">
    <link rel="preconnect" href="//techmarketingdemos.tt.omtrdc.net">
    <link rel="preconnect" href="//techmarketingdemos.sc.omtrdc.net">
    <link rel="dns-prefetch" href="//dpm.demdex.net">
    <link rel="dns-prefetch" href="//fast.techmarketingdemos.demdex.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.demdex.net">
    <link rel="dns-prefetch" href="//cm.everesttech.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.tt.omtrdc.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.sc.omtrdc.net">
    <!--/Preconnect and DNS-Prefetch-->
    <!--Data Layer to enable rich data collection and targeting-->
    <script>
    var digitalData = {
        "page": {
            "pageInfo" : {
                "pageName": "Home"
                }
            }
    };
    </script>
    <!--/Data Layer-->
    <!--jQuery or other helper libraries-->
    <script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
    <!--/jQuery-->
    <!--prehiding snippet for Adobe Target with asynchronous tags deployment-->
    <script>
        (function(g,b,d,f){(function(a,c,d){if(a){var e=b.createElement("style");e.id=c;e.innerHTML=d;a.appendChild(e)}})(b.getElementsByTagName("head")[0],"at-body-style",d);setTimeout(function(){var a=b.getElementsByTagName("head")[0];if(a){var c=b.getElementById("at-body-style");c&&a.removeChild(c)}},f)})(window,document,"body {opacity: 0 !important}",3E3);
    </script>
    <!--/prehiding snippet for Adobe Target with asynchronous tags deployment-->
    <!--Tags Header Embed Code: REPLACE LINE 39 WITH THE INSTALL CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
    <!--/Tags Header Embed Code-->
</head>
<body>
    <h1>Tags Basic Demo</h1>
    <p>This is a very simple page to demonstrate basic concepts of tags</p>
</body>
</html>
```

이제 사이트에 태그 포함 코드를 추가하는 방법을 알 수 있습니다.

[다음 &quot;데이터 요소, 규칙 및 라이브러리 추가&quot; >](add-data-elements-rules.md)
