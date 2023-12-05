---
title: Platform Mobile SDK 구현에 대한 동의 구현
description: 모바일 앱에서 동의를 구현하는 방법을 알아봅니다.
feature: Mobile SDK,Consent
jira: KT-14629
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# 동의 구현

모바일 앱에서 동의를 구현하는 방법을 알아봅니다.

Adobe Experience Platform Consent 모바일 확장을 사용하면 Adobe Experience Platform Mobile SDK 및 Edge Network 확장을 사용할 때 모바일 앱에서 동의 환경 설정을 수집할 수 있습니다. 에 대해 자세히 알아보기 [동의 확장](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/) 설명서에서 참조하십시오.

## 전제 조건

* SDK가 설치 및 구성된 앱을 빌드하고 실행했습니다.

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* 사용자에게 동의를 묻는 메시지를 표시합니다.
* 사용자 응답을 기반으로 확장을 업데이트합니다.
* 현재 동의 상태를 가져오는 방법을 알아봅니다.

## 동의 요청

처음부터 자습서를 따랐다면 동의 확장에서 기본 동의를 로 설정했음을 기억할 수 있습니다 **[!UICONTROL 보류 중 - 사용자가 동의 환경 설정을 제공하기 전에 발생하는 이벤트를 큐에 추가합니다.]**

데이터 수집을 시작하려면 사용자의 동의를 받아야 합니다. 실제 앱에서는 지역에 대한 동의 모범 사례를 참조해야 합니다. 이 자습서에서는 경고를 사용하여 요청하기만 하면 사용자의 동의를 받습니다.

1. 사용자에게 동의를 한 번만 요청하려고 합니다. 이렇게 하려면 Mobile SDK 동의와 Apple을 사용한 추적에 필요한 인증을 결합하면 됩니다. [앱 추적 투명도 프레임워크](https://developer.apple.com/documentation/apptrackingtransparency). 이 앱에서는 사용자가 추적 권한을 부여할 때 이벤트 수집에 동의한다고 가정합니다.

1. 다음으로 이동 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** 를 입력합니다.

   에 이 코드 추가 `updateConsent` 함수.

   ```swift
   // Update consent
   let collectConsent = ["collect": ["val": value]]
   let currentConsents = ["consents": collectConsent]
   Consent.update(with: currentConsents)
   MobileCore.updateConfigurationWith(configDict: currentConsents)
   ```

1. 다음으로 이동 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL 면책조항 보기]** 응용 프로그램을 설치 또는 다시 설치하고 앱을 처음 시작한 후에 표시되는 보기인 Xcode의 Project navigator에 있습니다. Apple에 따라 추적을 승인하라는 메시지가 표시됩니다. [앱 추적 투명도 프레임워크](https://developer.apple.com/documentation/apptrackingtransparency). 사용자가 권한을 부여하면 동의도 업데이트됩니다.

   에 다음 코드를 추가합니다 `ATTrackingManager.requestTrackingAuthorization { status in` 종료.

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

## 현재 동의 상태 가져오기

동의 모바일 확장은 현재 동의 값을 기반으로 추적을 자동으로 억제/보류/허용합니다. 현재 동의 상태에 직접 액세스할 수도 있습니다.

1. 다음으로 이동 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** Xcode의 Project navigator에서.

   에 다음 코드를 추가합니다 `getConsents` 함수:

   ```swift
   // Get consents
   Consent.getConsents { consents, error in
      guard error == nil, let consents = consents else { return }
      guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
      guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
      Logger.aepMobileSDK.info("Consent getConsents: \(jsonStr)")
   }
   ```

2. 다음으로 이동 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL HomeView]** Xcode의 Project navigator에서.

   에 다음 코드를 추가합니다 `.task` 수정자:

   ```swift
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

위의 예에서는 단순히 동의 상태를 Xcode의 콘솔에 로깅하는 것입니다. 실제 시나리오에서는 이를 사용하여 사용자에게 표시되는 메뉴나 옵션을 수정할 수 있습니다.

## Assurance를 통해 유효성 검사

1. 장치 또는 시뮬레이터에서 애플리케이션을 삭제하여 추적 및 동의를 올바르게 재설정하고 초기화합니다.
1. 시뮬레이터 또는 장치를 Assurance에 연결하려면 다음을 검토하십시오. [설치 지침](assurance.md#connecting-to-a-session) 섹션.
1. 에서 앱으로 이동할 때 **[!UICONTROL 홈]** 화면 대상 **[!UICONTROL 제품]** 화면으로 돌아가기 **[!UICONTROL 홈]** 화면에 다음이 표시됩니다. **[!UICONTROL 동의 응답 받기]** 이벤트를 추가합니다.
   ![동의 확인](assets/consent-update.png)


>[!SUCCESS]
>
>이제 Adobe Experience Platform Mobile SDK를 사용하여 설치(또는 재설치) 후 초기 시작 시 사용자에게 동의를 묻는 메시지를 표시하도록 앱을 활성화했습니다.
>
>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하려는 경우 또는 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

다음: **[라이프사이클 데이터 수집](lifecycle-data.md)**
