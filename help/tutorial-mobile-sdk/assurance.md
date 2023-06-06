---
title: 보증 설정
description: 모바일 앱에서 Assurance 확장을 구현하는 방법을 알아봅니다.
exl-id: e15774b2-2f52-400f-9313-bb4338a88918
source-git-commit: b2e1bf08d9fb145ba63263dfa078c96258342708
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 2%

---

# 보증

모바일 앱에서 Adobe Experience Platform Assurance를 설정하는 방법을 알아봅니다.

Assurance는 정식적으로 프로젝트 그리폰이라고 하며, 모바일 앱에서 데이터를 수집하거나 경험을 제공하는 방법을 검사, 증명, 시뮬레이션 및 확인하는 데 도움이 되도록 설계되었습니다.

보증은 Adobe Experience Platform Mobile SDK에서 생성한 원시 SDK 이벤트를 검사하는 데 도움이 됩니다. SDK에서 수집한 모든 이벤트를 검사할 수 있습니다. SDK 이벤트는 시간별로 정렬된 목록 보기에 로드됩니다. 각 이벤트에는 추가 세부 정보를 제공하는 세부 보기가 있습니다. SDK 구성, 데이터 요소, 공유 상태 및 SDK 확장 버전을 검색할 수 있는 추가 보기도 제공됩니다. 에 대해 자세히 알아보기 [보증](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html) 를 참조하십시오.


## 사전 요구 사항

* SDK가 설치 및 구성된 샘플 앱을 빌드하고 실행했습니다.

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* 조직에 액세스 권한이 있는지 확인합니다(없는 경우 요청).
* 기본 URL을 설정합니다.
* 필요한 iOS 관련 코드를 추가합니다.
* 세션에 연결합니다.

## 액세스 확인

다음 단계를 완료하여 조직에서 Assurance에 액세스할 수 있는지 확인하십시오.

1. 방문 [https://experience.adobe.com/#/assurance](https://experience.adobe.com/griffon){target="_blank"}
1. Experience Cloud에 대해 Adobe ID 자격 증명을 사용하여 로그인합니다.
1. 다음으로 데리고 가면 **[!UICONTROL 세션]** 그런 다음 액세스 권한을 갖습니다. Beta 액세스 페이지로 이동하면 **[!UICONTROL 등록]**.

## 구현

일반에 더해서 [SDK 설치](install-sdks.md) 이전 단원에서 을(를) 완료했습니다. iOS에도 다음 추가 기능이 필요합니다. 다음 코드를 `AppDelegate.swift` 파일에 추가합니다.

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey: Any] = [:]) -> Bool {
    Assurance.startSession(url: url)
    return true
}
```

이 자습서에 제공된 샘플 Luma는 iOS 12.0을 사용합니다. iOS 13 이상을 사용하여 자신의 장면 기반 애플리케이션과 함께 다음을 수행하는 경우 `UISceneDelegate's scene(_:openURLContexts:)` 메서드를 다음과 같이 바꿉니다.

```swift
func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>) {
    // Called when the app in background is opened with a deep link.
    if let deepLinkURL = URLContexts.first?.url {
        Assurance.startSession(url: deepLinkURL)
    }
}
```

추가 정보를 찾을 수 있음 [여기](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/api-reference/){target="_blank"}.

## 기본 URL 설정

1. XCode를 열고 프로젝트 이름을 선택합니다.
1. 다음 위치로 이동 **정보** 탭.
1. 아래로 스크롤하여 **URL 유형** 및 선택 **+** 단추를 클릭하여 새 단추를 추가합니다.
1. 설정 **식별자** 및 **URL 체계** &quot;lumadeeplink&quot;에 매핑됩니다.
1. 앱을 빌드하고 실행합니다.

![보증 url](assets/mobile-assurance-url-type.png)

iOS의 URL 체계에 대해 자세히 알아보려면 을 검토하십시오. [Apple 설명서](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target="_blank"}.

보증은 브라우저 또는 QR 코드를 통해 해당 URL이 앱을 열고 추가 매개 변수를 포함하는 기본 URL로 시작하는 URL을 열어 작동합니다. 이러한 고유한 매개 변수는 세션을 연결하는 데 사용됩니다.

## 세션에 연결

1. 다음 위치로 이동 [보증 UI](https://experience.adobe.com/griffon){target="_blank"}.
1. 선택 **[!UICONTROL 세션 만들기]**.
1. 제공 **[!UICONTROL 세션 이름]** 과 같은 `Luma App QA` 및 **[!UICONTROL 기본 URL]** `lumadeeplink://default`
1. **[!UICONTROL 다음]**을 선택합니다.
   ![보증 생성 세션](assets/mobile-assurance-create-session.png)
1. **[!UICONTROL QR 코드 스캔]** 물리적 디바이스를 사용하는 경우 시뮬레이터를 사용하고 있다면 **[!UICONTROL 링크 복사]** 시뮬레이터에서 Safari를 사용하여 엽니다.
   ![보증 qa 코드](assets/mobile-assurance-qr-code.png)
1. 앱이 로드되면 이전 단계에서 PIN을 입력하라는 모달이 표시됩니다.
   ![보증 pin 입력](assets/mobile-assurance-enter-pin.png)
1. 연결에 성공하면 Assurance 웹 UI에 이벤트가 표시되고 앱에 부동 Assurance 아이콘이 표시됩니다.
   * 보증 아이콘 부동.
      ![보증 양식](assets/mobile-assurance-modal.png)
   * 웹 UI에서 전달되는 Experience Cloud 이벤트.
      ![보증 이벤트](assets/mobile-assurance-events.png)

문제가 발생하는 경우 다음을 검토하십시오. [기술](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/){target="_blank"} and [general documentation](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html){target="_blank"}.

다음: **[동의](consent.md)**

>[!NOTE]
>
>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나, 일반적인 피드백을 공유하거나, 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오. [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
