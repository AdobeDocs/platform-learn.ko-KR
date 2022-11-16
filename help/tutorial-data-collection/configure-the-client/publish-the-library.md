---
title: 라이브러리 게시
description: 라이브러리 게시
exl-id: b2657835-f320-4d58-b99b-f88aad660259
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 3%

---

# 라이브러리 게시

이제 웹 사이트에 태그 라이브러리를 배포할 차례입니다.

## 라이브러리 만들기

먼저 만든 확장, 규칙 및 데이터 요소를 포함하는 라이브러리를 만들어야 합니다.

1. 라이브러리를 만들려면 을(를) 선택합니다 **[!UICONTROL 게시 흐름]** 왼쪽 메뉴에 있습니다.
1. 선택 **[!UICONTROL 라이브러리 추가]**. 라이브러리 만들기 보기가 표시됩니다.
   ![태그 라이브러리 만들기](../assets/tags-library-creation.png)

1. 라이브러리에 다음과 같은 이름을 지정합니다. **_데모_**.
1. 선택 **[!UICONTROL 개발]** 에서 [!UICONTROL 환경] 드롭다운.
1. 다음을 클릭합니다. **[!UICONTROL 변경된 모든 리소스 추가]**.
이제 아래에 모든 확장, 규칙 및 데이터 요소가 표시됩니다 [!UICONTROL 리소스 변경 사항].
1. 클릭 **[!UICONTROL 개발에 저장 및 구축]**.

## HTML에 포함 코드 추가

이제 새로 빌드된 태그 라이브러리를 로드하는 제품 페이지 HTML에 스크립트 태그를 추가해야 합니다.

1. 다음을 클릭하여 시작합니다 **[!UICONTROL 환경]** 왼쪽 메뉴에 있습니다. 나열된 세 가지 다른 환경이 표시됩니다.
   ![태그 환경](../assets/tags-environments.png)
1. 에서 패키지 아이콘을 클릭합니다. **[!UICONTROL 개발]** 아래의 환경 행 _설치_ 열. 페이지에 Launch 라이브러리 스크립트를 설치하는 지침이 표시됩니다.
   ![태그 설치 지침](../assets/tags-installation-instructions.png)
1. 스크립트 태그를 복사합니다(편의를 위해 클립보드로 복사 단추가 있음).
1. 제품 페이지 HTML을 열고 앞에 스크립트 태그를 삽입합니다. `</head>` 태그에 가깝게 포함했습니다. 최종 HTML은 다음과 같습니다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Product Page</title>
    <script>
      window.adobeDataLayer = window.adobeDataLayer || [];
      window.adobeDataLayer.push({
        "event": "pageViewed",
        "web": {
          "webPageDetails": {
            "name": "Foam Roller",
            "siteSection": "Equipment"
          },
        },
        "productListItems": [
          {
            "SKU": "eqfr08",
            "currencyCode": "USD",
            "name": "Foam Roller",
            "priceTotal": 18.95
          }
        ]
      });
      window.adobeDataLayer.push({
        "event": "productViewed"
      });
      window.onAddToCartClick = function() {
        // In a real implementation, you would change this condition to 
        // only pass if a cart doesn't already exist. You would typically 
        // do this by checking a cookie or variable value.
        if (true) {
          window.adobeDataLayer.push({
            "event": "cartOpened",
          });
        }
        window.adobeDataLayer.push({
          "event": "productAddedToCart"
        });
      };
      window.onDownloadAppClick = function() {
        window.adobeDataLayer.push({
          "event": "downloadAppClicked",
          "eventInfo": {
            "web": {
              "webInteraction": {
                "URL": "https://example.com/download",
                "name": "App Download",
                "type": "download"
              }
            }
          }
        });
      };
    </script>
    <!--Swap this script tag with your own-->
    <script src="https://assets.adobedtm.com/xxxxxxxxxxxx/xxxxxxxxxxxx/launch-xxxxxxxxxxxx-development.min.js" async></script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download" onclick="onDownloadAppClick()">Download the app</a>
  </body>
</html>
```

다음을 확인하십시오 [태그에 대한 설명서 게시](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html?lang=ko-KR) 게시 프로세스에 대해 자세히 알아보려면.

다음으로, 새 구현을 테스트합니다!

[다음: ](../test-the-implementation.md)

>[!NOTE]
>
>데이터 수집에 시간을 내어 주셔서 감사합니다. 질문이 있거나 일반 피드백을 공유하거나 향후 컨텐츠에 대한 제안 사항이 있는 경우 해당 정보를 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
