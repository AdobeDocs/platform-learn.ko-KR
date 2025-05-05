---
title: Platform Mobile SDK를 사용하여 WebViews 처리
description: 모바일 앱에서 WebViews를 사용하여 데이터 수집을 처리하는 방법에 대해 알아봅니다.
jira: KT-14632
exl-id: 9b3c96fa-a1b8-49d2-83fc-ece390b9231c
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# 웹 보기 처리

모바일 앱에서 WebViews를 사용하여 데이터 수집을 처리하는 방법에 대해 알아봅니다.

## 전제 조건

* SDK가 설치 및 구성된 앱을 빌드하고 실행했습니다.

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* 앱에서 WebViews에 대해 특별히 고려해야 하는 이유를 이해합니다.
* 추적 문제를 방지하는 데 필요한 코드를 이해합니다.

## 잠재적 추적 문제

앱의 기본 부분과 앱 내의 WebView에서 데이터를 전송하는 경우 각각은 고유한 Experience Cloud ID(ECID)를 생성하므로 히트가 끊기고 방문/방문자 데이터가 부풀려집니다. ECID에 대한 자세한 내용은 [ECID 개요](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=ko)를 참조하십시오.

이러한 바람직하지 않은 상황을 해결하려면 사용자의 ECID를 앱의 기본 부분에서 앱에서 사용할 WebView로 전달하는 것이 중요합니다.

WebView 내에서 사용된 AEP Edge Identity 확장은 새 ID에 대한 Adobe 요청을 보내는 대신 현재 ECID를 수집하여 URL에 추가합니다. 그런 다음 구현은 이 ECID를 사용하여 URL을 요청합니다.

## 구현

**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Info]** > **[!DNL TermsOfServiceSheet]**(으)로 이동하여 `final class SwiftUIWebViewModel: ObservableObject` 클래스에서 `func loadUrl()` 함수를 찾습니다. 웹 보기를 처리하기 위해 다음 호출을 추가합니다.

```swift
// Handle web view
AEPEdgeIdentity.Identity.getUrlVariables {(urlVariables, error) in
    if let error = error {
        print("Error with Webview", error)
        return;
    }
    
    if let urlVariables: String = urlVariables {
        urlString.append("?" + urlVariables)
        guard let url = URL(string: urlString) else {
            return
        }
        DispatchQueue.main.async {
            self.webView.load(URLRequest(url: url))
        }
    }
    Logger.aepMobileSDK.info("Successfully retrieved urlVariables for WebView, final URL: \(urlString)")
}
```

[`AEPEdgeIdentity.Identity.getUrlVariables`](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) API는 URL에 대해 ECID 등과 같은 모든 관련 정보를 포함하도록 변수를 설정합니다. 이 예에서는 로컬 파일을 사용하고 있지만 원격 페이지에도 동일한 개념이 적용됩니다.

[Edge Network 확장 API 참조 안내서](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables)에서 `Identity.getUrlVariables` API에 대해 자세히 알아볼 수 있습니다.

## 유효성 검사

코드를 실행하려면:

1. [설치 지침](assurance.md#connecting-to-a-session) 섹션을 검토하여 시뮬레이터 또는 장치를 Assurance에 연결하십시오.
1. 앱의 **[!UICONTROL 설정]**(으)로 이동
1. **[!DNL View...]** 단추를 탭하여 **[!DNL Terms of Use]**&#x200B;을(를) 표시합니다.

   <img src="./assets/tou1.png" width="300" /> <img src="./assets/tou2.png" width="300" />

1. Assurance UI에서 **[!UICONTROL com.adobe.grifcon.mobile]** 공급업체에서 **[!UICONTROL Edge ID 응답 URL 변수]** 이벤트를 찾습니다.
1. 이벤트를 선택하고 **[!UICONTROL ACPExtensionEventData]** 개체에서 **[!UICONTROL urlvariable]** 필드를 검토하여 다음 매개 변수가 URL에 있는지 확인합니다. `adobe_mc`, `mcmid` 및 `mcorgid`.

   ![웹 보기 유효성 검사](assets/webview-validation.png)

   샘플 `urvariables` 필드는 아래에서 볼 수 있습니다.

   * 원본(이스케이프 처리된 문자 포함)

     ```html
     adobe_mc=TS%3D1636526122%7CMCMID%3D79076670946787530005526183384271520749%7CMCORGID%3D7ABB3E6A5A7491460A495D61%40AdobeOrg
     ```

   * 미화

     ```html
     adobe_mc=TS=1636526122|MCMID=79076670946787530005526183384271520749|MCORGID=7ABB3E6A5A7491460A495D61@AdobeOrg
     ```

죄송합니다. 웹 세션 디버깅은 제한됩니다. 예를 들어 브라우저의 Adobe Experience Platform Debugger을 사용하여 Webview 세션을 계속 디버깅할 수는 없습니다.

>[!NOTE]
>
>이러한 URL 매개 변수를 통한 방문자 결합은 Platform Web SDK(버전 2.11.0 이상) 및 `VisitorAPI.js` 사용 시 지원됩니다.


>[!SUCCESS]
>
>이제 Adobe Experience Platform Mobile SDK에서 이미 발급한 ECID와 동일한 ECID를 사용하여 웹 보기에서 URL을 기반으로 콘텐츠를 표시하도록 앱을 설정했습니다.
>
>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하고 싶거나 향후 콘텐츠에 대한 제안이 있는 경우 이 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=ko)에서 공유하십시오.

다음: **[ID](identity.md)**
