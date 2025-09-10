---
title: Platform Mobile SDK으로 인앱 메시지 만들기 및 보내기
description: Platform Mobile SDK 및 Adobe Journey Optimizer을 사용하여 인앱 메시지를 만들고 모바일 앱으로 전송하는 방법에 대해 알아봅니다.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: In App
jira: KT-14639
exl-id: 6cb4d031-6172-4a84-b717-e3a1f5dc7d5d
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '1786'
ht-degree: 1%

---

# 인앱 메시지 만들기 및 보내기

Experience Platform Mobile SDK 및 Journey Optimizer을 사용하여 모바일 앱용 인앱 메시지를 만드는 방법을 알아봅니다.

Journey Optimizer을 사용하면 캠페인을 만들어 타깃팅된 대상자에게 인앱 메시지를 보낼 수 있습니다. Journey Optimizer의 캠페인은 다양한 채널을 사용하여 특정 대상에게 일회성 콘텐츠를 전달하는 데 사용됩니다. 캠페인을 사용하면 작업을 동시에 즉시 또는 지정된 일정에 따라 수행합니다. 여정([Journey Optimizer 푸시 알림](journey-optimizer-push.md) 단원 참조)를 사용하면 작업이 순서대로 실행됩니다.

![아키텍쳐](assets/architecture-ajo.png){zoomable="yes"}

Journey Optimizer을 사용하여 인앱 메시지를 보내기 전에 적절한 구성 및 통합이 제대로 되어 있는지 확인해야 합니다. Journey Optimizer의 인앱 메시지 데이터 흐름을 이해하려면 [설명서](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/in-app/inapp-configuration)를 참조하세요.

>[!NOTE]
>
>이 단원은 선택 사항이며 인앱 메시지를 전송하려는 Journey Optimizer 사용자에게만 적용됩니다.


## 전제 조건

* SDK가 설치 및 구성된 앱을 빌드하고 실행했습니다.
* Adobe Experience Platform용 앱을 설정합니다.
* Journey Optimizer 및 [푸시 알림에 대한 충분한 권한](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/push/push-config/push-configuration)에 액세스할 수 있습니다. 또한 다음 Journey Optimizer 기능에 대한 충분한 권한이 필요합니다.
   * 캠페인을 관리합니다.
* 테스트를 위한 물리적 iOS 장치 또는 시뮬레이터.


## 학습 목표

이 단원에서는 다음과 같은 작업을 수행합니다

* Journey Optimizer에서 채널 구성을 만듭니다.
* Journey Optimizer 태그 확장 설치 및 구성
* 앱을 업데이트하여 Journey Optimizer 태그 확장을 등록합니다.
* Assurance에서 설정의 유효성을 검사합니다.
* Journey Optimizer에서 나만의 캠페인 및 인앱 메시지 경험을 정의합니다.
* 앱 내에서 고유한 인앱 메시지를 보냅니다.

## 설정

>[!TIP]
>
>[Journey Optimizer 푸시 메시지](journey-optimizer-push.md) 단원의 일부로 환경을 이미 설정한 경우 이 설정 섹션의 일부 단계를 이미 수행했을 수 있습니다.


### 채널 구성 만들기

시작하려면 Journey Optimizer에서 앱 메시지 알림을 보낼 수 있도록 채널 구성을 만들어야 합니다.

1. Journey Optimizer 인터페이스에서 **[!UICONTROL 채널]** > **[!UICONTROL 일반 설정]** > **[!UICONTROL 채널 구성]** 메뉴를 연 다음 **[!UICONTROL 채널 구성 만들기]**&#x200B;를 선택합니다.

1. 구성의 이름 및 설명(선택 사항)을 입력합니다. 예: `LumaInAppMessaging` 및 `Channel for in-app messaging`.

   >[!NOTE]
   >
   > 이름은 문자(A-Z)로 시작해야 합니다. 영숫자만 포함할 수 있습니다. 밑줄 `_`, 점 `.`, 하이픈 `-`도 사용할 수 있습니다.

1. 구성에 사용자 지정 또는 핵심 데이터 사용 레이블을 할당하려면 **[!UICONTROL 액세스 관리]**&#x200B;를 선택할 수 있습니다. [OLAC(개체 수준 액세스 제어)에 대해 자세히 알아보세요](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/access-control/object-based-access).

1. **인앱 메시지** 채널을 선택하십시오.

1. 이 구성을 사용하여 동의 정책을 메시지와 연결하려면 **[!UICONTROL 마케팅 액션]**&#x200B;을(를) 선택하십시오. 마케팅 액션과 관련된 모든 동의 정책은 고객의 선호도를 존중하도록 활용됩니다. [마케팅 액션에 대해 자세히 알아보기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/privacy/consent/consent#surface-marketing-actions). 예: 푸시 타깃팅.

1. 설정을 정의할 플랫폼을 선택합니다. 이 설정을 사용하면 각 플랫폼에 대한 대상 앱을 지정할 수 있으며, 여러 플랫폼에서 일관되게 콘텐츠를 게재할 수 있습니다.

   >[!NOTE]
   >
   >iOS 및 Android 플랫폼의 경우 게재는 앱 ID만을 기반으로 합니다. 두 앱이 동일한 앱 ID를 공유하는 경우 **[!UICONTROL 채널 구성]**&#x200B;에서 선택한 플랫폼에 관계없이 콘텐츠가 두 앱 모두에 전달됩니다.

1. 지원하려는 플랫폼의 앱 ID를 입력합니다.

   ![채널 구성 만들기](assets/in-app-messaging-config.png){zoomable="yes"}

1. 변경 내용을 저장하려면 **[!UICONTROL 제출]**&#x200B;을 선택하십시오.

### 데이터 스트림 구성 업데이트

모바일 앱에서 Edge Network으로 전송된 데이터가 Journey Optimizer으로 전달되도록 하려면 Experience Edge 구성을 업데이트하십시오.



1. 데이터 수집 UI에서 **[!UICONTROL 데이터스트림]**&#x200B;을(를) 선택하고 데이터스트림(예: **[!DNL Luma Mobile App]**)을 선택합니다.
1. ![Experience Platform](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg)에 대해 **[!UICONTROL 자세히]**&#x200B;를 선택하고 상황에 맞는 메뉴에서 ![편집](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL 편집]**&#x200B;을 선택합니다.
1. **[!UICONTROL 데이터스트림]** > ![폴더](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) > **[!UICONTROL Adobe Experience Platform]** 화면에서 **[!UICONTROL Adobe Journey Optimizer]**&#x200B;을(를) 선택했는지 확인하십시오. 자세한 내용은 [Adobe Experience Platform 설정](https://experienceleague.adobe.com/ko/docs/experience-platform/datastreams/configure)을 참조하세요.
1. 데이터스트림 구성을 저장하려면 **[!UICONTROL 저장]**&#x200B;을 선택합니다.


   ![AEP 데이터스트림 구성](assets/datastream-ajo-inapp-configuration.png){zoomable="yes"}


### Journey Optimizer 태그 확장 설치

앱이 Journey Optimizer에서 작동하려면 태그 속성을 업데이트해야 합니다.

1. **[!UICONTROL 태그]** > **[!UICONTROL 확장]** > **[!UICONTROL 카탈로그]**(으)로 이동합니다.
1. 속성을 엽니다(예: **[!DNL Luma Mobile App Tutorial]**).
1. **[!UICONTROL 카탈로그]**&#x200B;를 선택하십시오.
1. **[!UICONTROL Adobe Journey Optimizer]** 확장을 검색합니다.
1. 확장을 설치합니다.

앱에서 인앱 메시지를 사용하는 경우 *only*, **[!UICONTROL 확장 설치]** 또는 **[!UICONTROL 확장 구성]**&#x200B;에서는 아무것도 구성할 필요가 없습니다. 자습서에서 [푸시 알림](journey-optimizer-push.md) 단원을 이미 따랐다면 **[!UICONTROL 개발]** 환경의 경우 **[!UICONTROL AJO 푸시 추적 경험 이벤트 데이터 세트]** 데이터 세트가 **[!UICONTROL 이벤트 데이터 세트]** 목록에서 선택되었음을 알 수 있습니다.


### 앱에서 Journey Optimizer 구현

이전 단원에서 설명한 대로 모바일 태그 확장을 설치하면 구성만 제공됩니다. 그런 다음 메시징 SDK을 설치하고 등록해야 합니다. 이 단계가 명확하지 않으면 [SDK 설치](install-sdks.md) 섹션을 검토하십시오.

>[!NOTE]
>
>[SDK 설치](install-sdks.md) 섹션을 완료한 경우 SDK이 이미 설치되어 있으므로 이 단계를 건너뛸 수 있습니다.
>

>[!BEGINTABS]

>[!TAB iOS]

1. Xcode에서 [AEP Messaging](https://github.com/adobe/aepsdk-messaging-ios)이(가) 패키지 종속 항목의 패키지 목록에 추가되어 있는지 확인하십시오. [Swift 패키지 관리자](install-sdks.md#swift-package-manager)를 참조하세요.
1. Xcode 프로젝트 탐색기에서 **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]**(으)로 이동합니다.
1. `AEPMessaging`이(가) 가져오기 목록의 일부인지 확인하십시오.

   `import AEPMessaging`

1. `Messaging.self`이(가) 등록 중인 확장 배열의 일부인지 확인하십시오.

   ```swift
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
   ```

>[!TAB Android]

1. Android Studio에서 [aepsdk-messaging-android](https://github.com/adobe/aepsdk-messaging-android)이(가) **[!UICONTROL Android]** **[!UICONTROL V자 전환]** > ![Gradle Scripts](/help/assets/icons/ChevronDown.svg)의 **[!UICONTROL build.gradle.kts]**&#x200B;에 있는 종속성의 일부인지 확인하십시오. [Gradle](install-sdks.md#gradle)을(를) 참조하세요.
1. Android Studio 프로젝트 탐색기에서 **[!UICONTROL Android]** ![VDown](/help/assets/icons/ChevronDown.svg) **[!DNL app]** > **[!DNL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL LumaApplication]**&#x200B;으로 이동합니다.
1. `com.adobe.marketing.mobile.Messaging`이(가) 가져오기 목록의 일부인지 확인하십시오.

   `import import com.adobe.marketing.mobile.Messaging`

1. `Messaging.EXTENSION`이(가) 등록 중인 확장 배열의 일부인지 확인하십시오.

   ```kotlin
   val extensions = listOf(
       Identity.EXTENSION,
       Lifecycle.EXTENSION,
       Signal.EXTENSION,
       Edge.EXTENSION,
       Consent.EXTENSION,
       UserProfile.EXTENSION,
       Places.EXTENSION,
       Messaging.EXTENSION,
       Optimize.EXTENSION,
       Assurance.EXTENSION
   )
   ```

>[!ENDTABS]

## Assurance으로 설정 유효성 검사

1. [설치 지침](assurance.md#connecting-to-a-session) 섹션을 검토하여 시뮬레이터 또는 장치를 Assurance에 연결하십시오.
1. Assurance UI에서 **[!UICONTROL 구성]**&#x200B;을 선택합니다.
   ![클릭 구성](assets/push-validate-config.png){zoomable="yes"}
1. ![인앱 메시지](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) 옆에 있는 **[!UICONTROL Plus]** 단추를 선택하세요.
1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.
   ![저장](assets/assurance-in-app-config.png){zoomable="yes"}
1. 왼쪽 탐색에서 **[!UICONTROL 인앱 메시지]**&#x200B;를 선택합니다.
1. **[!UICONTROL 유효성 검사]** 탭을 선택합니다. 오류가 발생하지 않는지 확인합니다.

   ![인앱 유효성 검사](assets/assurance-in-app-validate.png){zoomable="yes"}


## 고유한 인앱 메시지 만들기

고유한 인앱 메시지를 만들려면 발생하는 이벤트를 기반으로 인앱 메시지를 트리거하는 캠페인을 Journey Optimizer에서 정의해야 합니다. 이러한 이벤트는 다음과 같을 수 있습니다.

* Adobe Experience Platform으로 전송된 데이터,
* 모바일 코어 일반 API를 통한 작업, 상태 또는 PII 데이터 수집과 같은 코어 추적 이벤트
* 시작, 설치, 업그레이드, 닫기 또는 충돌과 같은 애플리케이션 라이프사이클 이벤트
* 관심 영역 입력 또는 종료와 같은 지리적 위치 이벤트.

이 자습서에서는 Mobile Core 일반 및 확장 독립적인 API([Mobile Core 일반 API](https://developer.adobe.com/client-sdks/documentation/mobile-core/#mobile-core-generic-apis) 참조)를 사용하여 사용자 화면, 작업 및 PII 데이터의 이벤트 추적을 용이하게 합니다. 이러한 API에 의해 생성된 이벤트는 SDK 이벤트 허브에 게시되며 확장에서 사용할 수 있습니다. SDK 이벤트 허브는 모든 Mobile Platform SDK 확장에 연결된 핵심 데이터 구조를 제공합니다. 이벤트 허브는 등록된 확장 및 내부 모듈 목록, 등록된 이벤트 리스너 목록 및 공유 상태 데이터베이스를 유지 관리합니다.

SDK 이벤트 허브는 등록된 확장에서 이벤트 데이터를 게시하고 수신하여 Adobe 및 서드파티 솔루션과의 통합을 단순화합니다. 예를 들어 최적화 확장이 설치되면 이벤트 허브는 Journey Optimizer - 의사 결정 관리 오퍼 엔진과의 모든 요청 및 상호 작용을 처리합니다.

1. Journey Optimizer UI의 왼쪽 레일에서 **[!UICONTROL 캠페인]**&#x200B;을 선택합니다.
1. **[!UICONTROL 캠페인 만들기]**&#x200B;를 선택합니다.
1. **[!UICONTROL 캠페인 만들기]** 대화 상자에서 ![시계](/help/assets/icons/Clock.svg) **[!UICONTROL 예약 - 마케팅]**&#x200B;을 선택하고 **[!UICONTROL 확인]**&#x200B;을 선택합니다.
1. **[!UICONTROL Campaign - *YYYY-MM-DD HH:MM:SS UTC+XX:XX*]**&#x200B;화면에서:

   1. **[!UICONTROL 속성]** 탭에서:

      1. 캠페인 이름(예: `Luma Mobile In-App Campaign`)을 입력하십시오.
      1. 원할 경우 설명을 추가합니다.


   1. **[!UICONTROL 작업]** 탭을 선택합니다.

      1. **[!UICONTROL 메시지 표시 조건]** 아래에서 ![추가](/help/assets/icons/Add.svg) **[!UICONTROL 작업 추가]**&#x200B;를 선택합니다. 드롭다운 메뉴에서 **[!UICONTROL 인앱 메시지]**&#x200B;를 선택합니다.
      1. **[!UICONTROL 인앱 메시지 구성]** 드롭다운 메뉴에서 구성을 선택합니다. 예: **[!UICONTROL LumaInAppMessaging]**.
      1. ![편집](/help/assets/icons/Edit.svg) **[!UICONTROL 트리거 편집]**&#x200B;을(를) 선택하십시오.
      1. **[!UICONTROL 인앱 메시지 트리거]** 대화 상자에서:

         1. **[!UICONTROL 응용 프로그램 시작]**&#x200B;을 선택하고 드롭다운 메뉴에서 **[!UICONTROL 작업 추적]**&#x200B;을 선택합니다.
         1. ![AddCircle](/help/assets/icons/AddCircle.svg) **[!UICONTROL 조건 추가]**&#x200B;를 선택합니다.
         1. 드롭다운 메뉴에서 **[!UICONTROL 작업]** 및 **[!UICONTROL 같음]**&#x200B;을 선택하십시오.
         1. `in-app` 입력.
         1. ![AddCircle](/help/assets/icons/AddCircle.svg) **[!UICONTROL 조건 추가]**&#x200B;를 선택합니다.
         1. 드롭다운 메뉴에서 **[!UICONTROL 컨텍스트 데이터]**&#x200B;을(를) 선택하고 `showMessage`을(를) 입력하십시오.
         1. 드롭다운 메뉴에서 **[!UICONTROL equals]**&#x200B;을(를) 선택하고 `true`을(를) 입력합니다.

            ![트리거 편집](assets/edit-triggers.png){zoomable="yes"}
         1. **[!UICONTROL 완료]**&#x200B;를 선택합니다.

   1. 기본 캠페인 정의 화면으로 돌아가서 **[!UICONTROL 콘텐츠]** 탭을 선택합니다.

      1. **[!UICONTROL 고급 서식 설정]**&#x200B;을 사용합니다.
      1. **[!UICONTROL 모달]**&#x200B;을(를) **[!UICONTROL 메시징 레이아웃]**(으)로 선택합니다. **[!UICONTROL 레이아웃 전환]** 대화 상자에서 **[!UICONTROL 레이아웃 변경]**&#x200B;을 선택합니다.
      1. **[!UICONTROL 콘텐츠]** 탭에서.
         1. `https://luma.enablementadobe.com/content/dam/luma/en/logos/Luma_Logo.png`미디어 URL **[!UICONTROL 에 대해]**&#x200B;을(를) 입력하십시오.
         1. **[!UICONTROL 머리글]**(예: `Welcome to this Luma In-App Message`)을 입력하고 **[!UICONTROL 본문]**(예: `Triggered by pushing that button in the app...`)을 입력하십시오.

         ![인앱 메시지 콘텐츠](assets/in-app-message-content.png){zoomable="yes"}

      1. **[!UICONTROL 설정]** 탭을 선택하십시오.
         1. **[!UICONTROL 메시지]**&#x200B;에서 **[!UICONTROL 크기 사용자 지정]**&#x200B;을(를) 선택하십시오.
         1. **[!UICONTROL 콘텐츠에 맞춤]**&#x200B;을 사용하지 않도록 설정합니다.
         1. **[!UICONTROL 높이]**&#x200B;을(를) **[!UICONTROL 75%]**(으)로 설정합니다.

         ![인앱 메시지 설정](assets/in-app-message-settings.png){zoomable="yes"}

1. **[!UICONTROL 활성화하려면 검토]**&#x200B;를 선택하십시오. **[!UICONTROL 콘텐츠]**, **[!UICONTROL 속성]**, **[!UICONTROL 작업]** 이상의 구성을 선택적으로 편집하려면 ![편집](/help/assets/icons/Edit.svg)을 선택하세요.
1. **[!UICONTROL 활성화 검토(*캠페인 이름*)]** 화면에서 **[!UICONTROL 활성화]**&#x200B;를 선택합니다.
1. 잠시 후 **_캠페인_** 목록에 상태가 **[!UICONTROL 라이브]**&#x200B;인 **[!UICONTROL 캠페인 이름]**&#x200B;이 표시됩니다.
   ![캠페인 목록](assets/ajo-campaign-list.png){zoomable="yes"}


## 인앱 메시지 트리거

인앱 메시지를 보낼 수 있는 모든 구성 요소가 준비되었습니다. 남은 것은 앱에서 이 인앱 메시지를 트리거하는 방법입니다.

>[!BEGINTABS]

>[!TAB iOS]

1. Xcode 프로젝트 탐색기에서 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]**(으)로 이동합니다. `func sendTrackAction(action: String, data: [String: Any]?)` 함수를 찾고 [`MobileCore.track` 및 ](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction) 매개 변수를 기반으로 `action` `data` 함수를 호출하는 다음 코드를 추가합니다.


   ```swift
   // Send trackAction event
   MobileCore.track(action: action, data: data)
   ```

1. Xcode Project Navigator에서 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL ConfigView]**(으)로 이동합니다. 인앱 메시지 단추에 대한 코드를 찾아 다음 코드를 추가합니다.

   ```swift
   // Setting parameters and calling function to send in-app message
   Task {
       MobileSDK.shared.sendTrackAction(action: "in-app", data: ["showMessage": "true"])
   }
   ```

>[!TAB Android]

1. Android Studio 탐색기에서 **[!UICONTROL Android]** ![VDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!DNL models]** > **[!UICONTROL MobileSDK]**(으)로 이동합니다. `fun sendTrackAction(action: String, data: Map<String, String>?)` 함수를 찾고 [`MobileCore.track` 및 ](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction) 매개 변수를 기반으로 `action` `data` 함수를 호출하는 다음 코드를 추가합니다.


   ```kotlin
   // Send trackAction event
   MobileCore.track(action, data)
   ```

1. Android Studio 탐색기에서 **[!UICONTROL Android]** ![VDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.androi]** > **[!DNL views]** > **[!UICONTROL ConfigView.kt]**(으)로 이동합니다. `onInAppMessageClick` 처리기 단추의 코드를 찾아 다음 코드를 추가합니다.

   ```kotlin
   // Setting parameters and calling function to send in-app message
   MobileSDK.shared.sendTrackAction(
       "in-app",
       mapOf("showMessage" to "true")
   )
   ```

>[!ENDTABS]

## 앱을 사용하여 유효성 검사

앱 자체 내에서 인앱 메시지의 유효성을 검사할 수 있습니다.

>[!BEGINTABS]

>[!TAB iOS]

1. ![재생](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg)을 사용하여 시뮬레이터나 Xcode의 실제 장치에서 앱을 다시 빌드하고 실행합니다.

1. **[!UICONTROL 설정]** 탭으로 이동합니다.

1. **[!UICONTROL 인앱 메시지]**&#x200B;를 탭합니다. 인앱 메시지가 앱에 표시되는 것을 볼 수 있습니다.

   <img src="assets/ajo-in-app-message.png" width="300" />


>[!TAB Android]

1. ![재생](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg)을 사용하여 시뮬레이터 또는 Android Studio의 실제 장치에서 앱을 다시 빌드하고 실행합니다.

1. **[!UICONTROL 설정]** 탭으로 이동합니다.

1. **[!UICONTROL 인앱 메시지]**&#x200B;를 탭합니다. 인앱 메시지가 앱에 표시되는 것을 볼 수 있습니다.

   <img src="assets/ajo-in-app-message-android.png" width="300" />


>[!ENDTABS]


## Assurance에서 구현의 유효성 검사

Assurance UI에서 인앱 메시지의 유효성을 검사할 수 있습니다.

1. [설치 지침](assurance.md#connecting-to-a-session) 섹션을 검토하여 시뮬레이터 또는 장치를 Assurance에 연결하십시오.
1. **[!UICONTROL 인앱 메시지]**&#x200B;를 선택합니다.
1. **[!UICONTROL 이벤트 목록]**&#x200B;을 선택하세요.
1. **[!UICONTROL 메시지 표시]** 항목을 선택하십시오.
1. 원본 이벤트, 특히 인앱 메시지의 전체 레이아웃과 콘텐츠가 포함된 `html`을(를) 검사합니다.
   ![Assurance 인앱 메시지](assets/assurance-in-app-display-message.png){zoomable="yes"}


## 다음 단계

관련 있고 적용 가능한 경우 인앱 메시지 추가를 시작할 수 있는 모든 도구가 있어야 합니다. 예를 들어 앱에서 추적 중인 특정 상호 작용을 기반으로 제품을 홍보할 수 있습니다.

>[!SUCCESS]
>
>Journey Optimizer 및 Experience Platform Mobile SDK용 Journey Optimizer 확장을 사용하여 인앱 메시지를 활성화하고 인앱 메시지 캠페인을 추가했습니다.
>
>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하고 싶거나 향후 콘텐츠에 대한 제안이 있는 경우 이 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=ko)에서 공유하십시오.

다음: **[오퍼 만들기 및 표시](journey-optimizer-offers.md)**
