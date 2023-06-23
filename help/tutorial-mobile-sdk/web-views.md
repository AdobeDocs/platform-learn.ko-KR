---
title: 웹 보기 처리
description: 모바일 앱에서 WebViews를 사용하여 데이터 수집을 처리하는 방법에 대해 알아봅니다.
jira: KT-6987
exl-id: 9b3c96fa-a1b8-49d2-83fc-ece390b9231c
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 1%

---

# 웹 보기 처리

모바일 앱에서 WebViews를 사용하여 데이터 수집을 처리하는 방법에 대해 알아봅니다.

## 사전 요구 사항

* SDK가 설치 및 구성된 앱을 빌드하고 실행했습니다.

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* WebViews에 대해 특별히 고려해야 하는 이유를 이해합니다.
* 추적 문제를 방지하는 데 필요한 코드를 이해합니다.

## 잠재적 추적 문제

앱의 기본 부분과 WebView에서 데이터를 전송하는 경우, 각 사용자는 고유한 Experience Cloud ID(ECID)를 생성합니다. 이렇게 되면 히트 수가 끊기고 방문/방문자 데이터가 부풀려집니다. ECID에 대한 자세한 내용은 [ECID 개요](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en).

이러한 바람직하지 않은 상황을 해결하려면 사용자의 ECID를 기본 부분에서 WebView로 전달하는 것이 중요합니다.

WebView의 Experience Cloud ID 서비스 JavaScript 확장은 새 ID에 대한 요청을 Adobe에게 보내는 대신 URL에서 ECID를 추출합니다. ID 서비스는 이 ECID를 사용하여 방문자를 추적합니다.

## 구현

Luma 샘플 앱에서 다음을 찾습니다. `TermsOfService.swift` 파일(위치: `Intro-Login_SignUp` folder)를 클릭하고 다음 코드를 찾습니다.

```swift
// Show tou.html
let url = Bundle.main.url(forResource: "tou", withExtension: "html")
let myRequest = URLRequest(url: url!)
self.webView.load(myRequest)
```

WebView를 로드하는 간단한 방법입니다. 이 경우 로컬 파일이지만 원격 페이지에도 동일한 개념이 적용됩니다.

아래 표시된 대로 Webview 코드를 리팩터링합니다.

```swift
let url = Bundle.main.url(forResource: "tou", withExtension: "html")
if var urlString = url?.absoluteString {
    // Adobe Experience Platform - Handle Web View
    AEPEdgeIdentity.Identity.getUrlVariables {(urlVariables, error) in
        if let error = error {
            self.simpleAlert("\(error.localizedDescription)")
            return;
        }

        if let urlVariables: String = urlVariables {
            urlString.append("?" + urlVariables)
        }

        DispatchQueue.main.async {
            self.webView.load(URLRequest(url: URL(string: urlString)!))
        }
        print("Successfully retrieved urlVariables for WebView, final URL: \(urlString)")
    }
} else {
    self.simpleAlert("Failed to create URL for webView")
}
```

다음에 대해 자세히 알아볼 수 있습니다. `Identity.getUrlVariables` 의 API [Edge Network 확장 API 참조 안내서를 위한 ID](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables).

## 유효성 검사

검토 후 [설치 지침](assurance.md) 섹션 및 시뮬레이터나 장치를 Assurance에 연결하고 WebView를 로드한 다음 `Edge Identity Response URL Variables` 다음에서 이벤트 발생 `com.adobe.griffon.mobile` 공급업체.

WebView를 로드하려면 Luma 앱의 홈 화면으로 이동하여 &quot;계정&quot; 아이콘을 선택한 다음, 바닥글에 &quot;사용 약관&quot;을 선택합니다.

WebView를 로드한 후 이벤트를 선택하고 `urlvariables` 의 필드 `ACPExtensionEventData` 다음 매개 변수가 URL에 있는지 확인하는 개체입니다. `adobe_mc`, `mcmid`, 및 `mcorgid`.

![webview 유효성 검사](assets/mobile-webview-validation.png)

샘플 `urvariables` 필드는 아래에서 볼 수 있습니다.

```html
// Original (with escaped characters)
adobe_mc=TS%3D1636526122%7CMCMID%3D79076670946787530005526183384271520749%7CMCORGID%3D7ABB3E6A5A7491460A495D61%40AdobeOrg

// Beautified
adobe_mc=TS=1636526122|MCMID=79076670946787530005526183384271520749|MCORGID=7ABB3E6A5A7491460A495D61@AdobeOrg
```

>[!NOTE]
>
>이러한 URL 매개 변수를 통한 방문자 결합은 현재 Platform Web SDK(버전 2.11.0 이상)에서 지원됩니다. `VisitorAPI.js`.


다음: **[신원](identity.md)**

>[!NOTE]
>
>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나, 일반적인 피드백을 공유하거나, 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오. [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)