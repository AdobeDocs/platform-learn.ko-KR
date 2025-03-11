---
title: SDK 교체 - 모바일 앱의 Adobe Target 구현을 Adobe Journey Optimizer - Decisioning 확장 프로그램으로 마이그레이션합니다.
description: Adobe Target에서 SDK - Decisioning Mobile 확장 기능으로 마이그레이션할 때 Adobe Journey Optimizer을 교체하는 방법을 알아봅니다.
exl-id: f1b77cad-792b-4a80-acff-e1a2f29250e1
source-git-commit: d2da62ed2d36f73af1c8053be5af27feea32cb14
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 2%

---

# Target SDK을 Optimize SDK으로 바꾸기

모바일 구현에서 Adobe Target SDK를 Optimize SDK로 바꾸는 방법을 알아봅니다. 기본 대체 는 다음 단계로 구성됩니다.

* Podfile 또는 `build.gradle` 파일의 종속성 업데이트
* 가져오기 업데이트
* 애플리케이션 코드 업데이트


>[!INFO]
>
>Adobe Experience Platform Mobile SDK 생태계 내에서 확장은 다른 이름을 가질 수 있는 애플리케이션에 가져온 SDK에 의해 구현됩니다.
>
> * **Target SDK**&#x200B;이(가) **Adobe Target 확장**&#x200B;을 구현함
> * **SDK 최적화**&#x200B;에서 **Adobe Journey Optimizer - Decisioning 확장 기능**&#x200B;을 구현합니다.

## 종속성 업데이트

+++Android 예

>[!BEGINTABS]

>[!TAB SDK 최적화]

마이그레이션 후 종속성 `build.gradle`개

```Java
implementation platform('com.adobe.marketing.mobile:sdk-bom:3.+')
implementation 'com.adobe.marketing.mobile:core'
implementation 'com.adobe.marketing.mobile:edgeidentity'
implementation 'com.adobe.marketing.mobile:edge'
implementation 'com.adobe.marketing.mobile:optimize'
```


>[!TAB SDK 타깃팅]

마이그레이션 전 종속성 `build.gradle`개

```Java
implementation platform('com.adobe.marketing.mobile:sdk-bom:3.+')
implementation 'com.adobe.marketing.mobile:analytics'
implementation 'com.adobe.marketing.mobile:target'
implementation 'com.adobe.marketing.mobile:core'
implementation 'com.adobe.marketing.mobile:identity'
implementation 'com.adobe.marketing.mobile:lifecycle'
implementation 'com.adobe.marketing.mobile:signal'
implementation 'com.adobe.marketing.mobile:userprofile'
```


>[!ENDTABS]

+++

+++ iOS 예

>[!BEGINTABS]


>[!TAB SDK 최적화]

마이그레이션 후 종속성 `Podfile`개

```Swift
use_frameworks!
target 'YourAppTarget' do
    pod 'AEPCore', '~> 5.0'
    pod 'AEPEdge', '~> 5.0'
    pod 'AEPEdgeIdentity', '~> 5.0'
    pod 'AEPOptimize', '~> 5.0'
end
```

>[!TAB SDK 타깃팅]

마이그레이션 전 종속성 `Podfile`개

```Swift
use_frameworks!
pod 'AEPAnalytics', '~> 5.0'
pod 'AEPTarget', '~> 5.0'
pod 'AEPCore', '~> 5.0'
pod 'AEPIdentity', '~> 5.0'
pod 'AEPSignal', '~>5.0'
pod 'AEPLifecycle', '~>5.0'
pod 'AEPUserProfile', '~> 5.0'
```

>[!ENDTABS]

+++

## 가져오기 및 코드 업데이트

+++ Android 예

>[!BEGINTABS]

>[!TAB SDK 최적화]

마이그레이션 후 Java 초기화 코드

```Java
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Edge;
import com.adobe.marketing.mobile.edge.identity.Identity;
import com.adobe.marketing.mobile.optimize.Optimize;
import com.adobe.marketing.mobile.AdobeCallback;
 
public class MainApp extends Application {
 
  private final String ENVIRONMENT_FILE_ID = "YOUR_APP_ENVIRONMENT_ID";
 
    @Override
    public void onCreate() {
        super.onCreate();
 
        MobileCore.setApplication(this);
        MobileCore.configureWithAppID(ENVIRONMENT_FILE_ID);
 
        MobileCore.registerExtensions(
            Arrays.asList(Edge.EXTENSION, Identity.EXTENSION, Optimize.EXTENSION),
            o -> Log.d("MainApp", "Adobe Journey Optimizer - Decisioning Mobile SDK was initialized.")
        );
    }
}
```

>[!TAB SDK 타깃팅]

마이그레이션 전 Java 초기화 코드

```Java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.Analytics;
import com.adobe.marketing.mobile.Extension;
import com.adobe.marketing.mobile.Identity;
import com.adobe.marketing.mobile.Lifecycle;
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Signal;
import com.adobe.marketing.mobile.Target;
import com.adobe.marketing.mobile.UserProfile;
import java.util.Arrays;
import java.util.List;
...
import android.app.Application;
...
public class MainApp extends Application {
...
    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);
        MobileCore.setLogLevel(LoggingMode.DEBUG);
        ...
        List<Class<? extends Extension>> extensions = Arrays.asList(
            Analytics.EXTENSION,
            Target.EXTENSION,
            Identity.EXTENSION,
            Lifecycle.EXTENSION,
            Signal.EXTENSION,
            UserProfile.EXTENSION
        );
 
 
        MobileCore.registerExtensions(extensions, new AdobeCallback () {
            @Override
            public void call(Object o) {
                MobileCore.configureWithAppID(<Environment File ID>);
            }
        });
    }
}
```

>[!ENDTABS]

+++

+++ iOS

>[!BEGINTABS]

>[!TAB SDK 최적화]

마이그레이션 후 Swift 초기화 코드

```Swift
import AEPCore
import AEPEdge
import AEPEdgeIdentity
import AEPOptimize
 
@UIApplicationMain
final class AppDelegate: UIResponder, UIApplicationDelegate {
  var window: UIWindow?
 
  func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]? = nil) -> Bool {
 
      // register the extensions
      MobileCore.registerExtensions([Edge.self, AEPEdgeIdentity.Identity.self, Optimize.self]) {
        MobileCore.configureWith(appId: <YOUR_ENVIRONMENT_FILE_ID>) // Replace <YOUR_ENVIRONMENT_FILE_ID> with a String containing your own ID.
      }
 
      return true
  }
}
```

>[!TAB SDK 타깃팅]

마이그레이션 전 Swift 초기화 코드

```Swift
import AEPCore
import AEPAnalytics
import AEPTarget
import AEPIdentity
import AEPLifecycle
import AEPSignal
import AEPServices
import AEPUserProfile
...
@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        MobileCore.setLogLevel(.debug)
        let appState = application.applicationState
        ...
        let extensions = [
            Analytics.self,
            Target.self,
            Identity.self,
            Lifecycle.self,
            Signal.self,
            UserProfile.self
        ]
        MobileCore.registerExtensions(extensions, {
        MobileCore.configureWith(<Environment File ID>)
        if appState != .background {
            MobileCore.lifecycleStart(additionalContextData: ["contextDataKey": "contextDataVal"])
            }
        })
        ...
        return true
    }
}
```

>[!ENDTABS]

+++

## API 비교

많은 Target 확장 API에는 아래 표에 설명된 Decisioning 확장을 사용하는 동일한 접근 방식이 있습니다. [함수](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/api-reference/)에 대한 자세한 내용은 API 참조를 참조하십시오.

| Target 확장 | Decisioning 확장 | 참고 |
| --- | --- | --- | 
| [prefetchContent](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#prefetchcontent){target=_blank} | [updatePropositions](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/api-reference/#updatepropositionswithcompletionhandlerandtimeout){target=_blank} |  |
| [retrieveLocationContent](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#retrievelocationcontent){target=_blank} | [getPropositions](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/api-reference/#getpropositionswithtimeout){target=_blank} | `getPropositions` API를 사용할 때 SDK에서 캐시되지 않은 범위를 가져오기 위한 원격 호출이 수행되지 않습니다. |
| [displayedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#retrievelocationcontent){target=_blank} | [오퍼 -> 표시됨()](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} | 또한 `generateDisplayInteractionXdm` Offer 메서드를 사용하여 항목 표시용 XDM을 생성할 수 있습니다. 그런 다음 Edge 네트워크 SDK의 sendEvent API를 사용하여 추가 XDM, 자유 형식 데이터를 첨부하고 경험 이벤트를 원격으로 전송할 수 있습니다. |
| [clickedLocation](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#clickedlocation){target=_blank} | [오퍼 -> 탭()](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} | 또한 `generateTapInteractionXdm` 오퍼 메서드를 사용하여 항목 탭용 XDM을 생성할 수 있습니다. 그런 다음 Edge 네트워크 SDK의 sendEvent API를 사용하여 추가 XDM, 자유 형식 데이터를 첨부하고 경험 이벤트를 원격으로 전송할 수 있습니다. |
| [clearPrefetchCache](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#clickedlocation){target=_blank} | [clearCachedPropositions](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} |  |
| [resetExperience](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#resetexperience){target=_blank} | 해당 사항 없음 | SDK용 Edge Network 확장 ID의 [removeIdentity](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity){target=_blank} API를 사용하여 방문자 ID를 Edge 네트워크로 보내는 것을 중지합니다. 자세한 내용은 [removeIdentity API 설명서](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity)를 참조하세요. <br><br>참고: Mobile Core의 `resetIdentities` API는 ECID(Experience Cloud ID)를 포함하여 SDK에 저장된 모든 ID를 지웁니다. 드물게 사용해야 합니다! |
| [getSessionId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#getsessionid){target=_blank} | 해당 사항 없음 | `state:store` 응답 핸들은 세션 관련 정보를 전달합니다. Edge 네트워크 확장은 만료되지 않은 상태 저장소 항목을 후속 요청에 연결하여 관리하는 데 도움이 됩니다. |
| [setSessionId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#setsessionid){target=_blank} | 해당 사항 없음 | `state:store` 응답 핸들은 세션 관련 정보를 전달합니다. Edge 네트워크 확장은 만료되지 않은 상태 저장소 항목을 후속 요청에 연결하여 관리하는 데 도움이 됩니다. |
| [getThirdPartyId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#getthirdpartyid){target=_blank} | 해당 사항 없음 | Edge Network 확장에 대한 ID의 updateIdentities API를 사용하여 타사 ID 값을 제공합니다. 그런 다음 데이터 스트림에서 타사 ID 네임스페이스를 구성합니다. 자세한 내용은 [Target 타사 ID 모바일 설명서](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id)를 참조하십시오. |
| [setThirdPartyId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#setthirdpartyid){target=_blank} | 해당 사항 없음 | Edge Network 확장에 대한 ID의 updateIdentities API를 사용하여 타사 ID 값을 제공합니다. 그런 다음 데이터 스트림에서 타사 ID 네임스페이스를 구성합니다. 자세한 내용은 [Target 타사 ID 모바일 설명서](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id)를 참조하십시오. |
| [getTntId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#gettntid){target=_blank} | 해당 사항 없음 | `locationHint:result` 응답 핸들은 Target 위치 힌트 정보를 전달합니다. Target Edge가 Experience Edge과 함께 위치한다고 가정합니다. <br> <br>Edge 네트워크 확장은 EdgeNetwork 위치 힌트를 사용하여 요청을 보낼 Edge 네트워크 클러스터를 결정합니다. SDK(하이브리드 앱)에서 Edge 네트워크 위치 힌트를 공유하려면 Edge Network 확장의 `getLocationHint` 및 `setLocationHint` API를 사용합니다. 자세한 내용은 [`getLocationHint` API 설명서](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint)를 참조하십시오. |
| [setTntId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#gettntid){target=_blank} | 해당 사항 없음 | [locationHint:result](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#setlocationhint){target=_blank} 응답 핸들은 Target 위치 힌트 정보를 전달합니다. Target Edge가 Experience Edge과 함께 위치한다고 가정합니다. <br> <br>Edge 네트워크 확장은 EdgeNetwork 위치 힌트를 사용하여 요청을 보낼 Edge 네트워크 클러스터를 결정합니다. SDK(하이브리드 앱)에서 Edge 네트워크 위치 힌트를 공유하려면 Edge Network 확장의 `getLocationHint` 및 `setLocationHint` API를 사용합니다. 자세한 내용은 [`getLocationHint` API 설명서](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint)를 참조하십시오. |


다음으로 페이지에 [활동을 요청 및 렌더링](retrieve-activities.md)하는 방법에 대해 알아봅니다.

>[!NOTE]
>
>Target 확장에서 Decisioning 확장으로 모바일 Target을 성공적으로 마이그레이션할 수 있도록 지원하기 위해 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)에 게시하여 알려 주십시오.
