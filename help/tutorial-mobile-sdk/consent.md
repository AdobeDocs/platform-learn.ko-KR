---
title: 동의
description: 모바일 앱에서 동의를 구현하는 방법을 알아봅니다.
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 3%

---

# 동의

모바일 앱에서 동의를 구현하는 방법을 알아봅니다.

Adobe Experience Platform Consent 모바일 확장을 사용하면 Adobe Experience Platform Mobile SDK 및 Edge Network 확장을 사용할 때 모바일 앱에서 동의 환경 설정 수집을 사용할 수 있습니다. 추가 정보 [동의 확장](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network)를 입력합니다.

## 전제 조건

* SDK가 설치 및 구성된 앱을 성공적으로 빌드하고 실행합니다.

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* 사용자에게 동의를 요청합니다.
* 사용자 응답을 기반으로 확장을 업데이트합니다.
* 현재 동의 상태를 가져오는 방법을 알아봅니다.

## 동의 요청

자습서를 처음부터 따랐으면 **[!UICONTROL 기본 동의 수준]** &quot;보류 중&quot;으로 설정됩니다. 데이터 수집을 시작하려면 사용자의 동의를 받아야 합니다. 이 자습서에서는 지역에 대한 동의 우수 사례를 참조할 실제 앱에서 경고로 간단히 동의를 얻습니다.

1. 사용자에게 한 번만 요청할 수 있습니다. 이를 관리하는 한 가지 간단한 방법은 `UserDefaults`.
1. 다음으로 이동 `Home.swift`.
1. 다음 코드를 `viewDidLoad()`.

   ```swift
   let defaults = UserDefaults.standard
   let consentKey = "askForConsentYet"
   let hidePopUp = defaults.bool(forKey: consentKey)
   ```

1. 사용자가 이전에 경고를 본 적이 없다면 경고를 표시하고 응답을 기반으로 동의를 업데이트합니다. 다음 코드를 `viewDidLoad()`.

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

동의 모바일 확장은 현재 동의 값을 기반으로 추적을 자동으로 억제/일시 중지/허용합니다. 현재 동의 상태에 직접 액세스할 수도 있습니다.

1. 다음으로 이동 `Home.swift`.
1. 다음 코드를 `viewDidLoad()`.

```swift
Consent.getConsents{ consents, error in
    guard error == nil, let consents = consents else { return }
    guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
    guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
    print("Consent getConsents: ",jsonStr)
}
```

위의 예에서는 콘솔에 동의 상태를 인쇄하는 것입니다. 실제 시나리오에서는 이 기능을 사용하여 사용자에게 표시되는 메뉴 또는 옵션을 수정할 수 있습니다.

## 보증으로 유효성 검사

1. 를 검토합니다. [보증](assurance.md) 단원.
1. 앱을 설치하십시오.
1. Assurance 생성 URL을 사용하여 앱을 시작합니다.
1. 위의 코드를 올바르게 추가한 경우 동의하라는 메시지가 표시됩니다. 선택 **예**.
   ![동의 팝업](assets/mobile-consent-validate.png)
1. 다음 항목이 표시됩니다. **[!UICONTROL 동의 기본 설정 업데이트됨]** 확인 UI의 이벤트입니다.
   ![동의 유효성 검사](assets/mobile-consent-update.png)

다음: **[라이프사이클 데이터 수집](lifecycle-data.md)**

>[!NOTE]
>
>Adobe Experience Platform Mobile SDK에 대한 학습에 시간을 내주셔서 감사합니다. 질문이 있거나 일반 피드백을 공유하거나 향후 컨텐츠에 대한 제안 사항이 있는 경우 해당 정보를 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)