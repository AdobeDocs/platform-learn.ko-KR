---
title: 제품 페이지에서 데이터 레이어 구현
description: 제품 페이지에서 데이터 레이어 구현
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: a72011a5-ea9c-45df-a0f3-5eb40bc99d3f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# 제품 페이지에서 데이터 레이어 구현

이 자습서에서는 일반적인 전자 상거래 웹 사이트용 Adobe 클라이언트 데이터 계층을 구현합니다. 아직 하지 않았다면, [Adobe 클라이언트 데이터 레이어를 사용하는 방법](how-to-use-the-adobe-client-data-layer.md) 먼저 Adobe 클라이언트 데이터 레이어가 작동하는 방식을 이해합니다.

사용자가 제품을 찾아보고 폼 롤러를 클릭한다고 가정해 보겠습니다. 사용자가 폼 롤러 제품 세부 사항 페이지에 도달합니다.

다음은 간단한 제품 세부 사항 페이지에 대한 HTML입니다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Product Page</title>
    <script>
      // Code will go here.
    </script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button">Add to cart</button>
    <a href="https://example.com/download">Download the app</a>
  </body>
</html>
```

아시다시피, `<head>` 태그 `<script>` 태그에 가깝게 포함했습니다. 여기서 JavaScript 코드를 배치합니다. 이 파일을 작성할 필요는 없습니다 `<script>` 태그 내 `<head>`를 채울 수 있지만 가능한 한 빨리 데이터를 데이터 레이어에 푸시하는 것은 마케터가 사용자가 페이지를 떠나기 전에 Adobe Experience Platform에 데이터를 보낼 수 있도록 하는 데 도움이 됩니다.

내부 `<script>` 태그로 시작하면 `adobeDataLayer` 어레이를 구성한 다음 적절한 이벤트 및 데이터 정보를 어레이에 푸시합니다. 데이터는 XDM 스키마를 따릅니다 [이전에 만든](../configure-the-server/create-a-schema.md).

```js
window.adobeDataLayer = window.adobeDataLayer || [];
window.adobeDataLayer.push({
  "event": "pageViewed",
  "web": {
    "webPageDetails": {
      "name": "Foam Roller",
      "siteSection": "Equipment"
    },
  }
});
window.adobeDataLayer.push({
  "event": "productViewed",
  "productListItems": [
    {
      "SKU": "eqfr08",
      "currencyCode": "USD",
      "name": "Foam Roller",
      "priceTotal": 18.95
    }
  ]
});
```

이 예제에서는 2개의 푸시를 데이터 레이어에 적용했으며 각 푸시에는 `event` 키. 다음 포함 `event` 키는 페이지에서 발생한 이벤트를 알리는 데 그치지 않고, 마케터가 Adobe Experience Platform 태그 내에 적절한 규칙을 만드는 것을 더 간단하게 만들 수 있습니다.

데이터 계층에 대한 첫 번째 푸시는 사용자가 페이지를 열람했음을 수신자(태그 규칙)에게 알립니다. 또한 페이지 이름과 사이트 섹션이 데이터 레이어에 추가됩니다.

데이터 계층에 대한 두 번째 푸시는 사용자가 제품을 보았음을 수신자(태그 규칙)에게 알립니다. 또한 데이터 계층에 제품 정보를 추가합니다.

## 장바구니에 추가

사용자가 를 클릭하는 시점을 추적할 수도 있습니다 [!UICONTROL 장바구니에 추가] 버튼을 클릭합니다.

이렇게 하려면 사용자가 [!UICONTROL 장바구니에 추가] 버튼을 클릭합니다.

```js
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
```

이 함수를 호출하면 먼저 사용자에 대해 장바구니가 이미 있는지 확인합니다. 일반적으로 특정 쿠키나 변수가 있는지 여부를 확인하여 수행합니다. 장바구니가 없는 경우 `cartOpened` 이벤트를 데이터 계층에 추가합니다. 그 후에 `productAddedToCart` 이벤트를 데이터 계층에 추가합니다. 제품 정보가 데이터 계층에 이미 있으므로 다시 추가할 필요가 없습니다.

추가 `onclick` 속성을 [!UICONTROL 장바구니에 추가] 새 `onAddToCartClick` 함수 위에 있어야 합니다.

HTML 페이지의 결과는 다음과 같습니다.

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
    </script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download">Download the app</a>
  </body>
</html>
```

## 앱 다운로드

마지막으로 수행할 작업은 사용자가 _[!UICONTROL 앱 다운로드]_ 링크를 클릭합니다.

이렇게 하려면 사용자가 _[!UICONTROL 앱 다운로드]_ 링크를 클릭합니다.

```js
window.onDownloadAppClick = function(event) {
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
```

이 경우 링크에 대한 정보는 `eventInfo` 키. 에서 설명한 대로 [Adobe 클라이언트 데이터 레이어를 사용하는 방법](how-to-use-the-adobe-client-data-layer.md)이렇게 하면 데이터 레이어에게 이벤트와 함께 이 데이터를 전달하지만, _not_ 데이터 레이어 내에서 데이터를 유지합니다. 링크 클릭의 경우, 클릭된 링크에 대한 정보를 추가해도 유용하지 않습니다. 이 링크는 페이지 전체에는 속하지 않으며, 발생할 수 있는 다른 이벤트에는 적용할 수 없기 때문입니다.

추가 `onclick` 속성을 [!UICONTROL 앱 다운로드] 새 링크를 호출하는 링크 `onDownloadAppClick` 함수 위에 있어야 합니다.

HTML 페이지의 결과는 다음과 같습니다.

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
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download" onclick="onDownloadAppClick()">Download the app</a>
  </body>
</html>
```
