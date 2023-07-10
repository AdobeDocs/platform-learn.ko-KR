---
title: 동의
description: 모바일 앱에서 동의를 구현하는 방법을 알아봅니다.
feature: Mobile SDK,Consent
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: adbe8f4476340abddebbf9231e3dde44ba328063
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 3%

---

# 동의

모바일 앱에서 동의를 구현하는 방법을 알아봅니다.

Adobe Experience Platform Consent 모바일 확장을 사용하면 Adobe Experience Platform Mobile SDK 및 Edge Network 확장을 사용할 때 모바일 앱에서 동의 환경 설정을 수집할 수 있습니다. 에 대해 자세히 알아보기 [동의 확장](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/)을 참조하십시오.

## 사전 요구 사항

* SDK가 설치 및 구성된 앱을 빌드하고 실행했습니다.

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* 사용자에게 동의를 묻는 메시지를 표시합니다.
* 사용자 응답을 기반으로 확장을 업데이트합니다.
* 현재 동의 상태를 가져오는 방법을 알아봅니다.

## 동의 요청

튜토리얼을 처음부터 따랐다면 **[!UICONTROL 기본 동의 수준]** &quot;보류 중&quot;으로 변경되었습니다. 데이터 수집을 시작하려면 사용자의 동의를 받아야 합니다. 이 자습서에서는 지역에 대한 동의 모범 사례를 참조하려는 실제 앱에서 경고를 사용하여 요청하기만 하면 동의를 얻습니다.

1. 사용자에게 한 번만 묻습니다. 이를 관리하는 한 가지 간단한 방법은 `UserDefaults`.
1. 다음으로 이동 `Home.swift`.
1. 에 다음 코드를 추가합니다 `viewDidLoad()`.

   ```swift
   let defaults = UserDefaults.standard
   let consentKey = "askForConsentYet"
   let hidePopUp = defaults.bool(forKey: consentKey)
   ```

1. 사용자가 이전에 경고를 보지 않은 경우 경고를 표시하고 응답을 기반으로 동의를 업데이트합니다. 에 다음 코드를 추가합니다 `viewDidLoad()`.

   ```swift
   if(hidePopUp == false){
       //Consent Alert
       let alert = UIAlertController(title: "Allow Data Collection?", message: "Selecting Yes will begin data collection", preferredStyle: .alert)
       alert.addAction(UIAlertAction(title: "Yes", style: .default, handler: { action in
           //Update Consent -> "yes"
           let collectConsent = ["collect": ["val": "y"]]
           let currentConsents = ["consents": collectConsent]
           Consent.update(with: currentConsents)
           defaults.set(true, forKey: consentKey)
       }))
       alert.addAction(UIAlertAction(title: "No", style: .cancel, handler: { action in
           //Update Consent -> "no"
           let collectConsent = ["collect": ["val": "n"]]
           let currentConsents = ["consents": collectConsent]
           Consent.update(with: currentConsents)
           defaults.set(true, forKey: consentKey)
       }))
       self.present(alert, animated: true)
   }
   ```


## 현재 동의 상태 가져오기

동의 모바일 확장은 현재 동의 값을 기반으로 추적을 자동으로 억제/보류/허용합니다. 현재 동의 상태에 직접 액세스할 수도 있습니다.

1. 다음으로 이동 `Home.swift`.
1. 에 다음 코드를 추가합니다 `viewDidLoad()`.

```swift
Consent.getConsents{ consents, error in
    guard error == nil, let consents = consents else { return }
    guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
    guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
    print("Consent getConsents: ",jsonStr)
}
```

위의 예에서는 단순히 동의 상태를 콘솔에 인쇄하는 것입니다. 실제 시나리오에서는 이를 사용하여 사용자에게 표시되는 메뉴나 옵션을 수정할 수 있습니다.

## Assurance를 통해 유효성 검사

1. 리뷰 [보증](assurance.md) 레슨.
1. 앱을 설치하십시오.
1. 보증 생성 URL을 사용하여 앱을 실행합니다.
1. 위의 코드를 올바르게 추가한 경우 동의를 입력하라는 메시지가 표시됩니다. 선택 **예**.
   ![동의 팝업](assets/mobile-consent-validate.png)
1. 다음이 표시됩니다. **[!UICONTROL 동의 환경 설정 업데이트됨]** 이벤트를 추가합니다.
   ![동의 확인](assets/mobile-consent-update.png)

다음: **[라이프사이클 데이터 수집](lifecycle-data.md)**

>[!NOTE]
>
>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나, 일반적인 피드백을 공유하거나, 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오. [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)