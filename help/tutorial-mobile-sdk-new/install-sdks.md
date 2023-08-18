---
title: Adobe Experience Platform Mobile SDK 설치
description: 모바일 앱에서 Adobe Experience Platform Mobile SDK를 구현하는 방법을 알아봅니다.
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 1%

---

# Adobe Experience Platform Mobile SDK 설치

모바일 앱에서 Adobe Experience Platform Mobile SDK를 구현하는 방법을 알아봅니다.

## 전제 조건

* 에 설명된 확장을 사용하여 태그 라이브러리를 성공적으로 빌드했습니다. [이전 단원](configure-tags.md).
* 의 개발 환경 파일 ID [모바일 설치 지침](configure-tags.md#generate-sdk-install-instructions).
* 다운로드됨, 비어 있음 [샘플 앱](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App{target="_blank"}).
* 경험 [XCode](https://developer.apple.com/xcode/{target="_blank"}).

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* Swift 패키지 관리자를 사용하여 필요한 SDK를 프로젝트에 추가합니다.
* 확장 등록.

>[!NOTE]
>
>모바일 앱 구현에서 &quot;확장&quot; 및 &quot;SDK&quot;라는 용어는 거의 상호 교환 가능합니다.

## Swift 패키지 관리자

CocoaPod를 사용하지 않고 Pod 파일을 사용합니다(모바일 설치 지침에 설명된 대로). [SDK 설치 지침 생성](./configure-tags.md#generate-sdk-install-instructions))에서는 Xcode의 기본 Swift 패키지 관리자를 사용하여 개별 패키지를 추가합니다.

Xcode에서 다음을 사용합니다. **[!UICONTROL 파일]** > **[!UICONTROL 패키지 추가...]** 아래 표에 나열된 모든 패키지를 설치합니다. 특정 패키지에 대한 전체 URL을 얻으려면 테이블에서 패키지의 링크를 선택하십시오.

| 패키지 | 설명 |
|---|---|
| [AEP 코어](https://github.com/adobe/aepsdk-core-ios.git) | 다음 `AEPCore`, `AEPServices`, 및 `AEPIdentity` 확장은 Adobe Experience Platform SDK의 기반을 나타냅니다. SDK를 사용하는 모든 앱에는 확장이 포함되어야 합니다. 이러한 모듈에는 모든 SDK 확장에 필요한 일반적인 기능 및 서비스 세트가 포함되어 있습니다.<br/>`AEPCore` 이벤트 허브의 구현을 포함합니다. 이벤트 허브는 앱과 SDK 간에 이벤트를 전달하는 데 사용되는 메커니즘입니다. 이벤트 허브는 확장 간에 데이터를 공유하는 데에도 사용됩니다.<br/>`AEPServices` 는 네트워킹, 디스크 액세스 및 데이터베이스 관리를 포함하여 플랫폼 지원에 필요한 몇 가지 재사용 가능한 구현을 제공합니다.<br/>`AEPIdentity` 는 Adobe Experience Platform ID 서비스와의 통합을 구현합니다.<br/>`AEPSignal` 마케터가 앱에 &quot;신호&quot;를 전송하여 데이터를 외부 대상으로 보내거나 URL을 열 수 있는 Adobe Experience Platform SDK의 신호 확장을 나타냅니다.<br/>`AEPLifecycle` 는 애플리케이션 설치 또는 업그레이드 정보, 애플리케이션 실행 및 세션 정보, 디바이스 정보 및 애플리케이션 개발자가 제공하는 추가 컨텍스트 데이터와 같은 애플리케이션 라이프사이클 지표를 수집하는 데 도움이 되는 Adobe Experience Platform SDK의 라이프사이클 확장을 나타냅니다. |
| [AEP Edge](https://github.com/adobe/aepsdk-edge-ios.git) | Adobe Experience Platform Edge Network 모바일 확장을 사용하면 모바일 애플리케이션에서 Adobe Edge Network로 데이터를 전송할 수 있습니다. 이 확장을 사용하면 보다 강력한 방식으로 Adobe Experience Cloud 기능을 구현하고, 하나의 네트워크 호출을 통해 여러 Adobe 솔루션을 제공하고, 동시에 이 정보를 Adobe Experience Platform에 전달할 수 있습니다.<br/>Edge Network 모바일 확장은 Adobe Experience Platform SDK용 확장으로, `AEPCore` 및 `AEPServices` 이벤트 처리를 위한 확장 및 `AEPEdgeIdentity` id 검색을 위한 확장(예: ECID) |
| [AEP Edge ID](https://github.com/adobe/aepsdk-edgeidentity-ios.git) | AEP Edge Identity 모바일 확장을 사용하면 Adobe Experience Platform SDK 및 Edge Network 확장을 사용할 때 모바일 애플리케이션에서 사용자 ID 데이터를 처리할 수 있습니다. |
| [AEP Edge 동의](https://github.com/adobe/aepsdk-edgeconsent-ios.git) | AEP 동의 수집 모바일 확장을 사용하면 Adobe Experience Platform SDK 및 Edge Network 확장을 사용할 때 모바일 애플리케이션에서 동의 환경 설정을 수집할 수 있습니다. |
| [AEP 사용자 프로필](https://github.com/adobe/aepsdk-userprofile-ios.git) | Adobe Experience Platform 사용자 프로필 모바일 확장 기능은 Adobe Experience Platform SDK에 대한 사용자 프로필을 관리하기 위한 확장 기능입니다. |
| [AEP Places](https://github.com/adobe/aepsdk-places-ios) | Adobe Experience Platform Places 확장은 Adobe Experience Platform Swift SDK용 확장입니다. AEPPlaces 확장을 사용하면 위치 UI 및 Adobe Adobe 실행 규칙에 정의된 대로 지리적 위치 이벤트를 추적할 수 있습니다. |
| [AEP 메시징](https://github.com/adobe/aepsdk-messaging-ios.git) | AEP 메시징 확장은 Adobe Experience Platform Swift SDK용 확장입니다. AEP 메시징 확장을 사용하면 푸시 알림 토큰과 푸시 알림 클릭스루 피드백을 Adobe Experience Platform에 보낼 수 있습니다. |
| [AEP 최적화](https://github.com/adobe/aepsdk-optimize-ios) | AEP 최적화 확장은 Adobe Target 또는 Adobe Journey Optimizer Offer decisioning을 사용하여 Adobe Experience Platform Mobile SDK에서 실시간 개인화 워크플로우를 가능하게 하는 API를 제공합니다. 이를 위해서는 `AEPCore` 및 `AEPEdge` experience Edge 네트워크에 개인화 쿼리 이벤트를 전송하는 확장입니다. |
| [AEP 보증](https://github.com/adobe/aepsdk-assurance-ios.git) | Assurance(프로젝트 그리폰)는 모바일 앱에서 데이터를 수집하거나 경험을 제공하는 방법을 검사, 증명, 시뮬레이션 및 확인하는 데 도움이 되는 새롭고 혁신적인 제품입니다. |


모든 패키지를 설치한 후 Xcode **[!UICONTROL 패키지 종속성]** 화면은 다음과 같아야 합니다.

![Xcode 패키지 종속성](assets/xcode-package-dependencies.png)


## 확장 가져오기

소스의 Xcode에서 **[!UICONTROL AppDelegate]** 및 **[!UICONTROL MobileSDK]**, 다음 가져오기를 추가합니다.

```swift
import AEPCore
import AEPServices
import AEPIdentity
import AEPSignal
import AEPLifecycle
import AEPEdge
import AEPEdgeIdentity
import AEPEdgeConsent
import AEPUserProfile
import AEPPlaces
import AEPMessaging
import AEPOptimize
import AEPAssurance
```

## AppDelegate 업데이트

위치 **AppDelegate**,

1. 설정 `@AppStorage` 값 `environmentFileId` 의 6단계에서 태그에서 검색한 개발 환경 파일 ID 값으로 [SDK 설치 지침 생성](configure-tags.md#generate-sdk-install-instructions).

   ```swift
   @AppStorage("environmentFileId") private var environmentFileId = "b5cbd1a1220e/1857ef6cacb5/launch-2594f26b23cd-development"
   ```

1. 다음 강조 표시된 코드를 `application(_, didFinishLaunchingWithOptions)` 함수.

   ```swift {highlight="10-39"}
   func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
   
       UNUserNotificationCenter.current().delegate = self
   
       // step-init-start
       MobileCore.setLogLevel(.trace)
       let appState = application.applicationState;
   
       let extensions = [
           AEPIdentity.Identity.self,
           Lifecycle.self,
           Signal.self,
           Edge.self,
           AEPEdgeIdentity.Identity.self,
           Consent.self,
           UserProfile.self,
           Places.self,
           Messaging.self,
           Optimize.self,
           Assurance.self
       ]
   
       MobileCore.registerExtensions(extensions, {
           // Use the environment file id assigned to this application via Adobe Experience Platform Data Collection
           Logger.aepMobileSDK.info("Luma - using mobile config: \(self.environmentFileId)")
           MobileCore.configureWith(appId: self.environmentFileId)
   
           // set this to false or comment it when deploying to TestFlight (default is false),
           // set this to true when testing on your device.
           MobileCore.updateConfigurationWith(configDict: ["messaging.useSandbox": true])
           if appState != .background {
               // only start lifecycle if the application is not in the background
               MobileCore.lifecycleStart(additionalContextData: nil)
           }
   
           // assume unknown, adapt to your needs.
           MobileCore.setPrivacyStatus(.unknown)
   
           // update version and build
           Logger.configuration.info("Luma - Updating version and build number...")
           SettingsBundleHelper.setVersionAndBuildNumber()
       })
   
       // register push notification
       registerForPushNotifications(application: application)
   
       // set up core location
       let locationManager = LocationManager()
       locationManager.requestAuthorisation()
   
       return true
   }
   ```

위의 코드는 다음을 수행합니다.

1. 필요한 확장을 등록합니다.
1. 태그 속성 구성을 사용하도록 MobileCore 및 기타 확장을 구성합니다.
1. 디버그 로깅을 활성화합니다. 자세한 내용 및 옵션은 [Adobe Experience Platform Mobile SDK 설명서](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).

>[!IMPORTANT]
>
>다음을 업데이트했는지 확인 `MobileCore.configureWith(appId: self.environmentFileId)` (으)로 `appId` 를 기반으로 함 `environmentFileId` 개발, 스테이징 또는 프로덕션용으로 빌드하고 있는 태그 환경에서.
>

>[!SUCCESS]
>
>이제 자습서의 나머지 부분에서 사용할 필수 Adobe Experience Platform Mobile SDK 확장을 올바르게 등록하기 위해 필요한 패키지를 설치하고 프로젝트를 업데이트했습니다.<br/>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하려는 경우 또는 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

다음: **[보증 설정](assurance.md)**
