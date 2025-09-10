---
title: Platform Mobile SDK 구현에 대한 동의 구현
description: 모바일 앱에서 동의를 구현하는 방법을 알아봅니다.
feature: Mobile SDK,Consent
jira: KT-14629
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 1%

---

# 동의 구현

모바일 앱에서 동의를 구현하는 방법을 알아봅니다.

Adobe Experience Platform Consent 모바일 확장을 사용하면 Adobe Experience Platform Mobile SDK 및 Edge Network 확장을 사용할 때 모바일 앱에서 동의 환경 설정을 수집할 수 있습니다. 설명서에서 [동의 확장](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/)에 대해 자세히 알아보세요.

## 전제 조건

* SDK가 설치 및 구성된 앱을 빌드하고 실행했습니다.

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* 사용자에게 동의를 묻는 메시지를 표시합니다.
* 사용자 응답을 기반으로 확장을 업데이트합니다.
* 현재 동의 상태를 가져오는 방법을 알아봅니다.

## 동의 요청

처음부터 자습서를 따랐다면 동의 확장에 있는 기본 동의를 **[!UICONTROL 보류 중 - 사용자가 동의 환경 설정을 제공하기 전에 발생하는 큐 이벤트로 설정했음을 기억할 수 있습니다.]**

데이터 수집을 시작하려면 사용자의 동의를 받아야 합니다. 실제 앱에서는 지역에 대한 동의 모범 사례를 참조해야 합니다. 이 자습서에서는 경고를 사용하여 요청하기만 하면 사용자의 동의를 받습니다.

>[!BEGINTABS]

>[!TAB iOS]

1. 사용자에게 동의를 한 번만 요청하려고 합니다. Mobile SDK 동의와 Apple의 [앱 추적 투명도 프레임워크](https://developer.apple.com/documentation/apptrackingtransparency)를 사용하여 추적하는 데 필요한 권한을 결합합니다. 이 앱에서는 사용자가 추적 권한을 부여할 때 이벤트 수집에 동의한다고 가정합니다.

1. Xcode 프로젝트 탐색기에서 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]**(으)로 이동합니다.

   이 코드를 `updateConsent` 함수에 추가합니다.

   ```swift
   // Update consent
   let collectConsent = ["collect": ["val": value]]
   let currentConsents = ["consents": collectConsent]
   Consent.update(with: currentConsents)
   MobileCore.updateConfigurationWith(configDict: currentConsents)
   ```

1. Xcode의 프로젝트 탐색기에서 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL 면책조항 보기]**&#x200B;로 이동합니다. Xode의 Project navigator는 애플리케이션을 설치 또는 재설치하고 앱을 처음 시작한 후 표시되는 보기입니다. Apple의 [앱 추적 투명도 프레임워크](https://developer.apple.com/documentation/apptrackingtransparency)에 따라 추적을 승인하라는 메시지가 표시됩니다. 사용자가 권한을 부여하면 동의도 업데이트됩니다.

   `ATTrackingManager.requestTrackingAuthorization { status in` 닫기에 다음 코드를 추가합니다.

   ```swift
   // Add consent based on authorization
   if status == .authorized {
      // Set consent to yes
      MobileSDK.shared.updateConsent(value: "y")
   }
   else {
      // Set consent to yes
      MobileSDK.shared.updateConsent(value: "n")
   }
   ```

>[!TAB Android]

1. 사용자에게 동의를 한 번만 요청하려고 합니다. 이 앱에서는 사용자가 추적 권한을 부여할 때 이벤트 수집에 동의한다고 가정합니다.

1. Android Studio 탐색기에서 **[!UICONTROL 앱]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL 모델]** > **[!UICONTROL MobileSDK]**&#x200B;로 이동합니다.

   이 코드를 `updateConsent(value: String)` 함수에 추가합니다.

   ```kotlin
   // Update consent
   val collectConsent = mapOf("collect" to mapOf("val" to value))
   val currentConsents = mapOf("consents" to collectConsent)
   Consent.update(currentConsents)
   MobileCore.updateConfiguration(currentConsents)
   ```

1. Android Studio 탐색기에서 **[!UICONTROL 앱]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL 보기]** > **[!UICONTROL 면책조항 보기.kt]**&#x200B;로 이동합니다.

   `DisclaimerView(navController: NavController)` 및 `// Set content to yes` 아래의 `// Set content to no` 함수에 다음 코드를 추가합니다.

   ```kotlin
   // Add consent based on authorization
   if (status) {
      showPersonalizationWarning = false
   
      // Set consent to yes
      MobileSDK.shared.updateTrackingStatus(TrackingStatus.AUTHORIZED)
      MobileSDK.shared.updateConsent("y")
   } else {
      Toast.makeText(
            context,
            "You will not receive offers and location tracking will be disabled.",
            Toast.LENGTH_LONG
      ).show()
      showPersonalizationWarning = true
   
      // Set consent to no
      MobileSDK.shared.updateTrackingStatus(TrackingStatus.DENIED)
      MobileSDK.shared.updateConsent("n")
   }
   ```

>[!ENDTABS]

## 현재 동의 상태 가져오기

동의 모바일 확장은 현재 동의 값을 기반으로 추적을 자동으로 억제/보류/허용합니다. 현재 동의 상태에 직접 액세스할 수도 있습니다.

>[!BEGINTABS]

>[!TAB iOS]

1. Xcode의 Project 탐색기에서 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]**(으)로 이동합니다.

   `getConsents` 함수에 다음 코드를 추가합니다.

   ```swift
   // Get consents
   Consent.getConsents { consents, error in
      guard error == nil, let consents = consents else { return }
      guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
      guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
      Logger.aepMobileSDK.info("Consent getConsents: \(jsonStr)")
   }
   ```

2. Xcode의 Project 탐색기에서 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL HomeView]**(으)로 이동합니다.

   `.task` 한정자에 다음 코드를 추가합니다.

   ```swift
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

위의 예에서는 단순히 동의 상태를 Xcode의 콘솔에 로깅하는 것입니다. 실제 시나리오에서는 이를 사용하여 사용자에게 표시되는 메뉴나 옵션을 수정할 수 있습니다.

>[!TAB Android]

1. Android Studio 탐색기에서 **[!UICONTROL 앱]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL 모델]** > **[!UICONTROL MobileSDK]**&#x200B;로 이동합니다.

   `getConsents()` 함수에 다음 코드를 추가합니다.

   ```kotlin
   // Get consents
   Consent.getConsents { callback ->
      if (callback != null) {
            val jsonStr = JSONObject(callback).toString(4)
            Log.i("MobileSDK", "Consent getConsents: $jsonStr")
      }
   }
   ```

1. Android Studio 탐색기에서 **[!UICONTROL 앱]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL 보기]** > **[!UICONTROL HomeView.kt]**&#x200B;로 이동합니다.

   `LaunchedEffect(unit)`에 다음 코드를 추가하십시오.

   ```kotlin
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

위의 예에서는 단순히 Android Studio의 콘솔에 동의 상태를 기록하는 것입니다. 실제 시나리오에서는 이를 사용하여 사용자에게 표시되는 메뉴나 옵션을 수정할 수 있습니다.

>[!ENDTABS]

## Assurance를 사용한 유효성 검사

1. 장치 또는 시뮬레이터에서 애플리케이션을 삭제하여 추적을 재설정하고 올바르게 동의를 초기화합니다.
1. 시뮬레이터 또는 장치를 Assurance에 연결하려면 [설치 지침](assurance.md#connecting-to-a-session) 섹션을 검토하십시오.
1. 앱에서 **[!UICONTROL 홈]** 화면에서 **[!UICONTROL 제품]** 화면으로 이동하고 **[!UICONTROL 홈]** 화면으로 다시 이동하면 Assurance UI에 **[!UICONTROL 동의 가져오기]** 이벤트가 표시됩니다.
   ![동의 유효성 검사](assets/consent-update.png){zoomable="yes"}


>[!SUCCESS]
>
>이제 앱을 활성화하여 설치(또는 재설치) 후 초기 시작 시 사용자에게 Adobe Experience Platform Mobile SDK 사용에 동의하라는 메시지를 표시합니다.
>
>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하고 싶거나 향후 콘텐츠에 대한 제안이 있는 경우 이 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)에서 공유하십시오.

다음: **[라이프사이클 데이터 수집](lifecycle-data.md)**
