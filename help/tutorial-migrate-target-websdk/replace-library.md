---
title: 라이브러리 바꾸기 | Target을 at.js 2.x에서 Web SDK로 마이그레이션
description: Adobe Target 구현을 at.js 2.x에서 Adobe Experience Platform Web SDK로 마이그레이션하는 방법에 대해 알아봅니다. 주제에는 라이브러리 개요, 구현 차이점 및 기타 주목할 만한 설명선이 포함됩니다.
exl-id: dfafa132-376a-475d-a467-9bc2f0a414cf
source-git-commit: 07c3c5b3f45eeb02e94a25dbd164b7397cb7869d
workflow-type: tm+mt
source-wordcount: '1594'
ht-degree: 1%

---

# at.js 라이브러리를 Platform Web SDK로 바꾸기

페이지 내 Adobe Target 구현을 대체하여 at.js에서 Platform Web SDK로 마이그레이션하는 방법에 대해 알아봅니다. 기본 대체 는 다음 단계로 구성됩니다.

* Target 관리 설정을 검토하고 IMS 조직 ID를 메모하십시오
* at.js 라이브러리를 Platform Web SDK로 바꾸기
* 동기 라이브러리 구현을 위해 코드 조각 사전 숨김 업데이트
* Platform Web SDK 구성

>[!NOTE]
>
>제공된 예는 예시 목적으로 제공되며 실제 Target 구현은 다를 수 있습니다. 기존 Target 구현에서 Adobe의 데이터 수집 태그 관리자를 사용하는 경우 [Platform Web SDK Target 구현 자습서](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html)를 참조하여 추가 정보를 확인할 수도 있습니다.


## Target 관리 설정 검토

Target을 Platform Web SDK로 마이그레이션하는 첫 번째 단계는 Target 인터페이스의 **[!UICONTROL 관리]** 섹션에서 설정을 검토하는 것입니다.

### [!UICONTROL 구현]

#### [!UICONTROL 계정 세부 정보]

* **[!UICONTROL IMS 조직 ID]** - Platform Web SDK를 구성하는 데 필요하므로 이 값을 적어 두십시오.
* **[!UICONTROL 디바이스에서 의사 결정]** - 이 기능은 Platform Web SDK에서 지원되지 않습니다. 이 설정은 마이그레이션 후 비활성화할 수 있으며, 더 이상 웹 사이트에서 at.js를 사용하지 않거나 온디바이스 의사 결정에 대한 서버측 사용 사례가 없는 경우 가능합니다.

#### [!UICONTROL 구현 방법]

**[!UICONTROL 구현 메서드]** 섹션에서 편집 가능한 모든 설정은 at.js에만 적용됩니다. 이러한 설정은 구현을 위해 사용자 지정된 at.js 라이브러리를 생성하는 데 사용됩니다. 이러한 설정을 검토하여 사용자 지정 코드가 있는지 또는 도메인 간 사용 사례에 대한 자사 및 타사 쿠키를 설정하고 있는지 확인하십시오.

**[!UICONTROL 프로필 라이프타임]** 설정은 Adobe 고객 지원 센터에서만 변경할 수 있습니다. Target 방문자 프로필 라이프타임은 구현 접근 방식의 영향을 받지 않습니다. at.js와 Platform Web SDK는 모두 동일한 방문자 프로필 라이프타임을 사용합니다.

#### [!UICONTROL 개인정보 보호]

* **[!UICONTROL 방문자 IP 주소 난독화]** - 이 설정은 지리 기반의 타깃팅 기능에 영향을 줍니다. at.js와 Platform Web SDK는 모두 지리 기반의 타깃팅을 위해 동일한 백엔드 IP 난독화 설정을 사용합니다.

### [!UICONTROL 환경]

Platform Web SDK는 별도의 개발, 스테이징 및 프로덕션 데이터스트림에 대해 [!UICONTROL 환경 ID]를 명시적으로 정의할 수 있는 데이터스트림 구성을 사용합니다. 이 구성의 주요 사용 사례는 URL이 존재하지 않아 환경을 쉽게 구분할 수 있는 모바일 앱 구현용입니다. 이 설정은 선택 사항이지만 모든 요청이 지정된 환경과 제대로 연결되었는지 확인하는 데 사용할 수 있습니다. 도메인 및 호스트 그룹 규칙에 따라 Target 환경을 할당해야 하는 at.js 구현과 다릅니다.

>[!NOTE]
>
>데이터 스트림 구성에 환경 ID가 지정되지 않은 경우 Target은 **호스트** 섹션에 지정된 대로 도메인-환경 매핑을 사용합니다.

자세한 내용은 [데이터 스트림 구성](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target) 안내서 및 Target [호스트](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) 설명서를 참조하십시오.

## Platform Web SDK 배포

Target 기능은 at.js와 Platform Web SDK에서 모두 제공합니다. 두 라이브러리를 동시에 사용하면 렌더링 및 추적 문제가 발생할 수 있습니다. Platform Web SDK로 성공적으로 마이그레이션하기 위한 첫 번째 단계는 at.js를 제거하고 Platform Web SDK(alloy.js)로 바꾸는 것입니다.

at.js를 사용하는 간단한 Target 구현을 가정하십시오.

* 페이지 상단 근처에 있는 데이터 레이어는 Target 및 기타 애플리케이션에 대한 정보를 제공합니다
* 기능이 Target 활동에서 사용될 수 있는 하나 이상의 타사 도우미 라이브러리(예: jQuery)
* 깜박임을 완화하기 위한 코드 조각 사전 숨김
* Target at.js 라이브러리는 기본 설정을 사용하여 비동기식으로 로드되어 활동을 자동으로 요청하고 렌더링합니다.

HTML 페이지의 +++at.js 예제 구현

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>
  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>
  <!--prehiding snippet for Target with asynchronous deployment-->
  <script>
    ;(function(win, doc, style, timeout) {
      var STYLE_ID = 'at-body-style';

      function getParent() {
        return doc.getElementsByTagName('head')[0];
      }

      function addStyle(parent, id, def) {
        if (!parent) {
          return;
        }
        var style = doc.createElement('style');
        style.id = id;
        style.innerHTML = def;
        parent.appendChild(style);
      }

      function removeStyle(parent, id) {
        if (!parent) {
          return;
        }
        var style = doc.getElementById(id);
        if (!style) {
          return;
        }
        parent.removeChild(style);
      }
      addStyle(getParent(), STYLE_ID, style);
      setTimeout(function() {
        removeStyle(getParent(), STYLE_ID);
      }, timeout);
    }(window, document, "body {opacity: 0 !important}", 3000));
  </script>
  <!--Target at.js library loaded asynchonously-->
  <script src="/libraries/at.js" async></script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div>Homepage Hero Banner Content</div>
</body>
</html>
```

+++

Platform Web SDK를 사용하도록 Target을 업그레이드하려면 먼저 at.js를 제거합니다.

```HTML
<!--Target at.js library loaded asynchonously-->
<script src="/libraries/at.js" async></script>
```

alloy JavsScript 라이브러리 또는 태그 포함 코드 및 Adobe Experience Platform Web SDK 확장으로 대체합니다.

>[!BEGINTABS]

>[!TAB JavaScript]

```HTML
<!--Platform Web SDK base code-->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
<script src="https://cdn1.adoberesources.net/alloy/2.13.1/alloy.min.js" async></script>
```

>[!TAB 태그]

```HTML
<!--Tags Header Embed Code: REPLACE WITH THE INSTALL CODE FROM YOUR OWN ENVIRONMENT-->
<script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
```

태그 속성에서 Adobe Experience Platform Web SDK 확장을 추가합니다.

![Adobe Experience Platform 웹 SDK 확장 추가](assets/library-tags-addExtension.png){zoomable="yes"}


>[!ENDTABS]

미리 빌드된 독립 실행형 버전에는 alloy라는 글로벌 함수를 만드는 페이지에 직접 추가된 &quot;기본 코드&quot;가 필요합니다. 이 함수를 사용하여 SDK와 상호 작용합니다. 전역 함수의 이름을 다른 이름으로 지정하려면 `alloy` 이름을 변경하십시오.

자세한 내용 및 배포 옵션은 [Platform Web SDK 설치](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html) 설명서를 참조하십시오.


## 콘텐츠 사전 숨김 접근 방식 업데이트

Platform Web SDK 구현에는 라이브러리가 비동기적으로 로드되는지 아니면 동기적으로 로드되는지에 따라 코드 조각을 미리 숨기는 작업이 필요할 수 있습니다.

### 비동기 구현

at.js와 마찬가지로, Platform Web SDK 라이브러리가 비동기적으로 로드되면 Target이 콘텐츠 교환을 수행하기 전에 페이지에서 렌더링을 완료할 수 있습니다. 이 동작으로 인해 Target에서 지정한 개인화된 콘텐츠로 대체되기 전에 기본 콘텐츠가 잠깐 나타나는 &quot;깜박임&quot;이라고 하는 것이 나타날 수 있습니다. Adobe 이러한 깜박임을 방지하려면 비동기 Platform Web SDK 스크립트 참조 또는 태그 포함 코드 바로 앞에 특수 코드 조각 사전 숨김을 추가하는 것이 좋습니다.

위의 예처럼 구현이 비동기적이라면 at.js 코드 조각 사전 숨김을 Platform Web SDK와 호환되는 아래 버전으로 바꾸십시오.

```HTML
<!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
<script>
  !function(e,a,n,t){var i=e.head;if(i){
  if (a) return;
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("mboxEdit") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

코드 조각 사전 숨김은 선택한 항목의 CSS 정의가 있는 페이지 헤드에 스타일 태그를 만듭니다. 이 스타일 태그는 Target에서 응답을 받거나 시간 초과에 도달하면 제거됩니다.

사전 숨김 동작은 코드 조각의 맨 끝에서 두 가지 구성으로 제어됩니다.

* `body { opacity: 0 !important }`은(는) Target이 로드될 때까지 사전 숨김에 사용할 CSS 정의를 지정합니다. 기본적으로 전체 페이지가 숨겨집니다. 이 정의를 숨기려는 방법과 함께 미리 숨길 선택기로 업데이트할 수 있습니다. 이 값은 단순히 사전 숨김 스타일 태그에 삽입된 값이므로 여러 정의를 포함할 수 있습니다. 탐색 아래의 콘텐츠를 줄바꿈하는 쉽게 식별할 수 있는 컨테이너 요소가 있는 경우 이 설정을 사용하여 해당 컨테이너 요소로 사전 숨김을 제한할 수 있습니다.

* `3000`은(는) 사전 숨김에 대한 시간 제한(밀리초)을 지정합니다. 시간 초과 전에 Target에서 응답을 받지 못하면 스타일 태그 사전 숨김이 제거됩니다. 이 시간 제한에 도달하는 경우는 드뭅니다.

>[!IMPORTANT]
>
>Platform Web SDK는 다른 스타일 ID `alloy-prehiding`을(를) 사용하므로 올바른 코드 조각을 사용하십시오. at.js에 대한 코드 조각 사전 숨김을 사용하는 경우 제대로 작동하지 않을 수 있습니다.

### 동기식 구현

Adobe은 전반적인 페이지 성능을 최대화하기 위해 Platform Web SDK를 비동기식으로 구현할 것을 권장합니다. 그러나 alloy.js 라이브러리 또는 태그 포함 코드가 동기식으로 로드되면 코드 조각을 미리 숨길 필요가 없습니다. 대신 Platform 웹 SDK 구성에 사전 숨김 스타일이 지정됩니다.

동기 구현을 위한 미리 숨김 스타일은 [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#prehidingStyle) 옵션을 사용하여 구성할 수 있습니다. Platform Web SDK 구성에 대해서는 다음 섹션에서 다룹니다.

Platform Web SDK에서 플리커를 관리하는 방법에 대한 자세한 내용은 [개인화된 경험에 대한 플리커 관리](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/manage-flicker.html) 가이드 섹션을 참조하십시오.

## Platform Web SDK 구성

페이지를 로드할 때마다 Platform Web SDK를 구성해야 합니다. 다음 예제에서는 단일 배포에서 전체 사이트가 Platform Web SDK로 업그레이드되고 있다고 가정합니다.

>[!BEGINTABS]

>[!TAB JavaScript]

`configure` 명령은 항상 호출되는 첫 번째 SDK 명령이어야 합니다. `edgeConfigId`은(는) [!UICONTROL 데이터 스트림 ID]입니다.

```JavaScript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

>[!TAB 태그]

태그 구현에서 많은 필드가 자동으로 채워지거나 드롭다운 메뉴에서 선택할 수 있습니다. 각 환경에 대해 서로 다른 플랫폼 [!UICONTROL 샌드박스] 및 [!UICONTROL 데이터스트림]을 선택할 수 있습니다. 데이터 스트림은 게시 프로세스의 태그 라이브러리 상태에 따라 변경됩니다.

![웹 SDK 태그 확장 구성](assets/tags-config.png){zoomable="yes"}
>[!ENDTABS]

페이지별로 at.js에서 Platform Web SDK로 마이그레이션하려는 경우 다음 구성 옵션이 필요합니다.


>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled":true,
  "idMigrationEnabled":true
});
```

>[!TAB 태그]

![웹 SDK 태그 확장 마이그레이션 옵션 구성](assets/tags-config-migration.png){zoomable="yes"}

>[!ENDTABS]

Target과 관련된 주목할 만한 구성 옵션은 아래에 요약되어 있습니다.

| 옵션 | 설명 | 예제 값 |
| --- | --- | --- |
| `edgeConfigId` | 데이터 스트림 ID | `ebebf826-a01f-4458-8cec-ef61de241c93` |
| `orgId` | Adobe Experience Cloud 조직 ID | `ADB3LETTERSANDNUMBERS@AdobeOrg` |
| `targetMigrationEnabled` | 이 옵션을 사용하여 Web SDK가 at.js에서 사용하는 레거시 mbox 및 mboxEdgeCluster 쿠키를 읽고 쓸 수 있도록 설정합니다. 이렇게 하면 Web SDK를 사용하는 페이지에서 at.js 라이브러리를 사용하는 페이지로 이동하는 동안 방문자 프로필을 유지하는 데 도움이 됩니다. | `true` |
| `idMigrationEnabled` | true인 경우 SDK는 이전 AMCV 쿠키를 읽고 설정합니다. 이 옵션은 사이트의 일부 부분에서 여전히 Visitor.js를 사용할 수 있지만 Platform Web SDK를 사용하여 로 전환하는 데 도움이 됩니다. | `true` |
| `thirdPartyCookiesEnabled` | Adobe 서드파티 쿠키의 설정을 활성화합니다. SDK는 타사 컨텍스트에서 방문자 ID를 유지하여 사이트 간에 동일한 방문자 ID를 사용할 수 있습니다. 여러 사이트가 있는 경우 이 옵션을 사용하십시오. 하지만 개인 정보 보호를 위해 이 옵션을 사용하지 않는 경우도 있습니다. | `true` |
| `prehidingStyle` | 개인화된 콘텐츠가 서버에서 로드되는 동안 웹 페이지의 콘텐츠 영역을 숨기는 CSS 스타일 정의를 만드는 데 사용됩니다. SDK의 동기식 배포에서만 사용됩니다. | `body { opacity: 0 !important }` |

전체 옵션 목록은 [Platform Web SDK 구성](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html) 안내서를 참조하십시오.

## 구현 예

Platform Web SDK가 제대로 갖추어지면 예제 페이지가 다음과 같이 표시됩니다.

>[!BEGINTABS]

>[!TAB JavaScript]

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>

  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>

  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

  <!--Platform Web SDK base code-->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
  <script src="https://cdn1.adoberesources.net/alloy/2.13.1/alloy.min.js" async></script>
  
  <!--Configure Platform Web SDK-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
  </script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div id="homepage-hero">Homepage Hero Banner Content</div>
</body>
</html>
```

>[!TAB 태그]

페이지 코드:

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>

  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>

  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

    <!--Tags Header Embed Code: REPLACE WITH THE INSTALL CODE FROM YOUR OWN ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div id="homepage-hero">Homepage Hero Banner Content</div>
</body>
</html>
```

태그에서 Adobe Experience Platform 웹 SDK 확장을 추가합니다.

![Adobe Experience Platform 웹 SDK 확장 추가](assets/library-tags-addExtension.png){zoomable="yes"}

원하는 구성을 추가합니다.
![웹 SDK 태그 확장 마이그레이션 옵션 구성](assets/tags-config-migration.png){zoomable="yes"}


>[!ENDTABS]



위에서 보듯이 Platform Web SDK 라이브러리를 단순히 포함 및 구성해도 Adobe Edge 네트워크에 대한 네트워크 호출은 실행되지 않습니다.

다음으로, VEC 기반 활동을 [요청 및 적용](render-vec-activities.md)하는 방법에 대해 알아봅니다.

>[!NOTE]
>
>at.js에서 Web SDK로 Target을 성공적으로 마이그레이션할 수 있도록 지원하기 위해 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)에 게시하여 알려 주십시오.
