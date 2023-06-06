---
title: Adobe Experience Platform Mobile SDK 설치
description: 모바일 앱에서 Adobe Experience Platform Mobile SDK를 구현하는 방법을 알아봅니다.
exl-id: 98d6f59e-b8a3-4c63-ae7c-8aa11e948f59
source-git-commit: b2e1bf08d9fb145ba63263dfa078c96258342708
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 1%

---

# Adobe Experience Platform Mobile SDK 설치

모바일 앱에서 Adobe Experience Platform Mobile SDK를 구현하는 방법을 알아봅니다.

## 사전 요구 사항

* 에 설명된 확장을 사용하여 태그 라이브러리를 성공적으로 빌드했습니다. [이전 단원](configure-tags.md).
* 의 개발 환경 파일 ID [모바일 설치 지침](configure-tags.md#generate-sdk-install-instructions).
* 다운로드됨, 비어 있음 [샘플 앱](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}.
* 경험 [XCode](https://developer.apple.com/xcode/){target="_blank"}.
* 기본 [명령줄](https://en.wikipedia.org/wiki/Command-line_interface){target="_blank"} 지식.

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* CocoaPod 파일을 업데이트합니다.
* 필요한 SDK를 가져옵니다.
* 확장 등록.

>[!NOTE]
>
>모바일 앱 구현에서 &quot;확장&quot; 및 &quot;SDK&quot;라는 용어는 거의 상호 교환 가능합니다.


## PodFile 업데이트

>[!NOTE]
>
> CocoaPods에 익숙하지 않은 경우 관계자를 검토하십시오. [시작 안내서](https://guides.cocoapods.org/using/getting-started.html).

설치는 일반적으로 간단한 sudo 명령입니다.

```console
sudo gem install cocoapods
```

CocoaPod를 설치한 후 Podfile을 엽니다.

![초기 podfile](assets/mobile-install-initial-podfile.png)

다음 Pod를 포함하도록 파일을 업데이트합니다.

```swift
pod 'AEPCore', '~> 3'
pod 'AEPEdge', '~> 1'
pod 'AEPUserProfile', '~> 3'
pod 'AEPAssurance', '~> 3'
pod 'AEPServices', '~> 3'
pod 'AEPEdgeConsent', '~> 1'
pod 'AEPLifecycle', '~>3'
pod 'AEPMessaging', '~>1'
pod 'AEPEdgeIdentity', '~>1'
pod 'AEPSignal', '~>3'
```

>[!NOTE]
>
> `AEPMessaging` Adobe Journey Optimizer을 사용하여 푸시 메시지를 구현할 계획인 경우에만 필요합니다. 다음에 대한 자습서를 읽어 보십시오. [Adobe Journey Optimizer을 사용하여 푸시 메시지 구현](journey-optimizer-push.md) 추가 정보.

Podfile에 변경 사항을 저장한 후 프로젝트가 있는 폴더로 이동하고 `pod install` 명령을 실행하여 변경 사항을 설치합니다.

![pod install](assets/mobile-install-podfile-install.png)

>[!NOTE]
>
> 프로젝트 디렉터리에 &quot;Podfile 없음&quot;이 표시된다면 오류입니다. 터미널이 잘못된 폴더에 있습니다. 업데이트한 Podfile이 있는 폴더로 이동하고 다시 시도하십시오.

최신 버전으로 업그레이드하려면 `pod update` 명령입니다.

>[!INFO]
>
>자신의 앱에서 CocoaPod을 사용할 수 없는 경우 다른 앱에 대해 알아볼 수 있습니다 [지원되는 구현](https://github.com/adobe/aepsdk-core-ios#binaries) (GitHub 프로젝트에서).

## CocoaPod 빌드

CocoaPod를 만들려면 `Luma.xcworkspace`, 및 선택 **제품**, 그 다음 **폴더 정리**.

>[!NOTE]
>
> 다음을 설정해야 합니다. **활성 아키텍처만 빌드** 끝 **아니요**. 이렇게 하려면 프로젝트 탐색기에서 Pod 프로젝트를 선택하고 **빌드 설정**, 및 설정 **활성 아키텍처 구축** 끝 **아니요**.

이제 프로젝트를 빌드하고 실행할 수 있습니다.

![빌드 설정](assets/mobile-install-build-settings.png)

>[!NOTE]
>
>Luma 프로젝트는 M1 칩셋의 Xcode v12.5로 구축되었으며 iOS 시뮬레이터에서 실행됩니다. 다른 설정을 사용 중인 경우 아키텍처를 반영하도록 빌드 설정을 변경해야 할 수 있습니다.
>
>빌드가 성공하지 못한 경우 을(를) 되돌려 보십시오. **활성 아키텍처 구축** > **디버그** 로 다시 설정 **예**.
>
>이 자습서를 작성하는 동안 시뮬레이터 구성 &quot;iPod touch (7th generation)&quot;이 사용되었습니다.

## 확장 가져오기

각 항목 `.swift` 파일에서 다음 가져오기를 추가합니다. 에 추가하여 시작 `AppDelegate.swift`.

```swift
import AEPUserProfile
import AEPAssurance
import AEPEdge
import AEPCore
import AEPEdgeIdentity
import AEPEdgeConsent
import AEPLifecycle
import AEPMessaging //Optional, used for AJO push messaging
import AEPSignal
import AEPServices
```

## AppDelegate 업데이트

다음에서 `AppDelegate.swift` 파일에 다음 코드를 추가합니다 `didFinishLaunchingWithOptions`. currentAppId를 의 태그에서 검색한 개발 환경 파일 ID 값으로 바꾸기 [이전 단원](configure-tags.md).

```swift
let currentAppId = "b5cbd1a1220e/bae66382cce8/launch-88492c6dcb6e-development"

let extensions = [Edge.self, Assurance.self, Lifecycle.self, UserProfile.self, Consent.self, AEPEdgeIdentity.Identity.self, Messaging.self]

MobileCore.setLogLevel(.trace)

MobileCore.registerExtensions(extensions, {
    MobileCore.configureWith(appId: currentAppId)
})
```

`Messaging.self` 에 설명된 대로 Adobe Journey Optimizer을 통해 푸시 메시지를 구현할 경우에만 필요합니다 [여기](journey-optimizer-push.md).

위의 코드는 다음을 수행합니다.

* 필요한 확장을 등록합니다.
* 태그 속성 구성을 사용하도록 MobileCore 및 기타 확장을 구성합니다.
* 디버그 로깅을 활성화합니다. 자세한 내용 및 옵션은 [Mobile SDK 설명서](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).

>[!IMPORTANT]
>프로덕션 앱에서는 현재 환경(dev/stag/prod)을 기반으로 AppId를 전환해야 합니다.

다음: **[보증 설정](assurance.md)**

>[!NOTE]
>
>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나, 일반적인 피드백을 공유하거나, 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오. [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)