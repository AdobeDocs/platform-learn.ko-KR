---
title: 태그를 사용하여 웹 사이트에서 Experience Cloud 구현
description: 태그를 사용하여 웹 사이트에서 Experience Cloud을 구현하는 것은 웹 사이트에서 Adobe Experience Cloud 솔루션을 구현하는 방법을 배우고자 하는 프런트엔드 개발자나 기술 마케터에게 완벽한 시작점입니다.
recommendations: catalog, noDisplay
exl-id: 1b95f0b2-3062-49d1-9b0b-e6824a54008f
source-git-commit: 2483409b52562e13a4f557fe5bdec75b5afb4716
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 36%

---

# 개요

_태그를 사용하여 웹 사이트에서 Experience Cloud 구현_&#x200B;은 웹 사이트에서 Adobe Experience Cloud 솔루션을 구현하는 방법을 배우고자 하는 프런트 엔드 개발자나 기술 마케터에게 완벽한 시작점입니다.

각 단원에는 Experience Cloud를 구현하고 그 가치를 이해하는 데 도움이 되는 방법 연습 및 기본 정보가 포함되어 있습니다. 데모 사이트는 자습서를 완료하기 위해 제공되므로 안전한 환경에서 기본 기술을 배울 수 있습니다. 이 자습서를 완료한 후에는 자체 웹 사이트에서 태그를 통해 모든 마케팅 솔루션 구현을 시작할 준비가 되어 있어야 합니다.

>[!INFO]
>
>이 자습서에서는 애플리케이션별 확장 및 라이브러리(Adobe Analytics의 경우 AppMeasurement.js, Adobe Target의 경우 at.js)를 사용합니다. Adobe Experience Platform Web SDK를 구현하려면 [Web SDK를 사용하여 Adobe Experience Cloud 구현](/help/tutorial-web-sdk/overview.md) 자습서를 참조하십시오.


이 단원을 완료하면 다음 작업을 수행할 수 있습니다.

* 태그 속성 만들기

* 웹 사이트에 태그 속성 설치

* 다음 Adobe Experience Cloud 솔루션 추가:
   * **[Adobe Experience Platform Identity 서비스](id-service.md)**
   * **[Adobe Target](target.md)**
   * **[Adobe Analytics](analytics.md)**
   * **[Adobe Audience Manager](audience-manager.md)**

* 규칙과 데이터 요소를 만들어 Adobe 솔루션에 데이터 보내기

* Adobe Experience Cloud Debugger를 사용하여 구현의 유효성 검사

* Publish은 개발, 스테이징 및 프로덕션 환경을 통해 변경됩니다

>[!NOTE]
>
>Adobe Experience Platform Launch은 데이터 수집 기술군으로 Adobe Experience Platform에 통합되고 있습니다. 이 콘텐츠를 사용하는 동안 알아야 하는 몇 가지 용어 변경 사항이 인터페이스에 롤아웃되었습니다.
>
> * Platform launch(Client Side)가 이제 **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ko)**&#x200B;입니다.
> * 이제 platform launch 서버측이 **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=ko)**&#x200B;입니다.
> * 이제 Edge 구성이 **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=ko)**&#x200B;입니다.

>[!NOTE]
>
>[Web SDK](../tutorial-web-sdk/overview.md) 및 [Mobile SDK](../tutorial-mobile-sdk/overview.md)에도 유사한 다중 솔루션 자습서가 있습니다.

## 전제 조건

이 단원들에서는 사용자에게 Adobe ID와 연습을 완료하는 데 필요한 권한이 있다고 가정합니다. 없을 경우 액세스 권한을 요청하려면 Experience Cloud 관리자에게 문의해야 할 수 있습니다.

* 태그의 경우 개발, 승인, Publish, 확장 관리 및 환경 관리 권한이 있어야 합니다. 태그 사용자 권한에 대한 자세한 내용은 [설명서](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=ko)를 참조하세요.
* Adobe Analytics의 경우 이 자습서를 완료하는 데 사용할 보고서 세트와 추적 서버를 알고 있어야 합니다.
* Audience Manager의 경우 Audience Manager 하위 도메인(&quot;파트너 이름&quot; &quot;파트너 ID&quot; 또는 &quot;파트너 하위 도메인&quot;이라고도 함)을 알고 있어야 합니다

또한 HTML 및 JavaScript와 같은 프런트 엔드 개발 언어를 잘 알고 있다고 가정합니다. 이러한 언어를 통달하지 않아도 단원을 완료할 수 있지만, 코드를 읽고 이해할 수 있으면 단원을 최대한 활용할 수 있습니다.

## 태그 기본 정보

Adobe Experience Platform의 태그 기능은 Adobe의 차세대 웹 사이트 태그 및 모바일 SDK 관리 기능입니다. 태그를 통해 관련 고객 환경을 향상하는 데 필요한 모든 분석, 마케팅 및 광고 솔루션을 배포하고 관리하는 간단한 방법을 고객에게 제공합니다. 태그에 대한 추가 요금은 없습니다. 모든 Adobe Experience Cloud 고객이 이용할 수 있습니다.

웹 사이트용 태그를 사용하면 데스크탑 및 모바일 사이트에서 사용되는 분석, 마케팅 및 광고 솔루션과 관련된 모든 JavaScript을 중앙에서 관리할 수 있습니다. 예를 들어 Adobe Analytics을 배포하는 경우 태그는 AppMeasurement JavaScript 라이브러리를 관리하고, 변수를 채우고, 요청을 실행합니다.

사용자 지정 코드를 포함하여 컨테이너의 컨텐츠가 축소됩니다. 모든 것은 모듈식입니다. 항목이 필요하지 않으면 라이브러리에 포함되지 않습니다. 따라서 빠르고 컴팩트하게 구현됩니다.

태그는 또한 서드파티 공급업체가 태그를 통해 솔루션을 쉽게 배포할 수 있도록 확장을 만들 수 있는 플랫폼입니다. 확장은 태그 인터페이스와 클라이언트 기능을 확장하는 코드 패키지(JavaScript, HTML 및 CSS)입니다. 태그는 운영 체제로 생각할 수 있으며 확장은 작업을 수행하기 위해 사용하는 앱입니다.

## 단원 정보

이 단원들에서는 Luma라는 가짜 소매 웹 사이트에 Adobe Experience Cloud를 구현하게 됩니다. [Luma 사이트](https://luma.enablementadobe.com/content/luma/us/en.html)에는 사실적인 구현을 만들 수 있는 풍부한 데이터 레이어와 기능이 있습니다. 고유한 Experience Cloud 조직에서 고유한 태그 속성을 빌드하고, Experience Cloud Debugger을 사용하여 호스팅된 Luma 사이트에 매핑합니다.

[![Luma 웹 사이트](images/overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)

## 도구 가져오기

1. 브라우저 전용 확장을 사용할 예정이므로 [Chrome 웹 브라우저](https://www.google.com/chrome/)를 사용하여 자습서를 완료해 주십시오
1. Chrome 브라우저에 [Adobe Experience Platform Debugger](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) 확장 추가
1. 샘플 html 페이지 코드 복사

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

1. 샘플 html 페이지를 변경할 수 있는 텍스트 편집기를 가져옵니다. (텍스트 편집기가 없다면 [Brackets](https://brackets.io/)를 추천합니다.)
1. [Luma 사이트](https://luma.enablementadobe.com/content/luma/us/en.html)에 책갈피를 지정합니다.

>[!NOTE]
>
>다른 브라우저에서 이 자습서를 읽고 데이터 수집 인터페이스 단계를 완료하는 동안 Chrome에서 Luma 사이트를 열면 이 자습서를 보다 쉽게 완료할 수 있습니다.

그럼 시작해 보겠습니다!

[다음 &quot;태그 속성 만들기&quot; >](create-a-property.md)
