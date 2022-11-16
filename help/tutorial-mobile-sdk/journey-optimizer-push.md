---
title: Adobe Journey Optimizer 푸시 메시지
description: Platform Mobile SDK 및 Adobe Journey Optimizer을 사용하여 모바일 앱에 푸시 메시지를 만드는 방법을 알아봅니다.
exl-id: e8e920d5-fd36-48b7-9185-a34231c0d336
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 2%

---

# Adobe Journey Optimizer 푸시 메시지

Platform Mobile SDK 및 Adobe Journey Optimizer을 사용하여 모바일 앱용 푸시 메시지를 만드는 방법을 알아봅니다.

Journey Optimizer을 사용하면 여정을 만들고 타겟팅된 대상자에게 메시지를 전송할 수 있습니다. Journey Optimizer에서 푸시 알림을 전송하기 전에 올바른 구성 및 통합이 있는지 확인해야 합니다. Adobe Journey Optimizer의 푸시 알림 데이터 흐름을 이해하려면 다음을 참조하십시오 [설명서](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-gs.html).

>[!NOTE]
>
>이 단원은 선택 사항이며 푸시 메시지를 전송하려는 Adobe Journey Optimizer 사용자만 적용됩니다.


## 전제 조건

* SDK가 설치 및 구성된 앱을 성공적으로 빌드하고 실행합니다.
* 설명된 대로 Adobe Journey Optimizer 및 충분한 권한에 대한 액세스 [여기](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). 또한 다음 Adobe Journey Optimizer 기능에 대한 충분한 권한이 필요합니다.
   * 앱 서피스를 만듭니다.
   * 여정 만들기
   * 메시지 만들기.
   * 메시지 사전 설정 만들기.
* 인증서, 식별자 및 키를 만들 수 있는 충분한 액세스 권한이 있는 유료 Apple 개발자 계정.
* 테스트를 위한 실제 iOS 장치.

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* APN(Apple 푸시 알림 서비스)에 앱 ID를 등록합니다.
* 만들기 **[!UICONTROL 앱 서피스]** AJO에서.
* 업데이트 **[!UICONTROL 스키마]** 푸시 메시지 필드를 포함하도록 업데이트되고 수정되었습니다.
* 설치 및 구성 **[!UICONTROL Adobe Journey Optimizer]** 태그 확장.
* AJO 태그 확장을 포함하도록 앱을 업데이트합니다.
* Assurance에서 설정의 유효성을 확인합니다.
* 테스트 메시지를 보냅니다.


## APN에 앱 ID 등록

다음 단계는 Adobe Experience Cloud에만 국한되지 않으며 APN 구성을 안내하도록 설계되었습니다.

### 만들기 `.p8` 개인 키

1. Apple 개발자 포털에서 **[!UICONTROL 키]**.
1. + 아이콘을 선택하여 키를 만듭니다.
   ![새 키 만들기](assets/mobile-push-apple-dev-new-key.png)

1. 다음을 제공합니다. **[!UICONTROL 키 이름]**.
1. 을(를) 선택합니다 **[!UICONTROL APN]** 확인란을 선택합니다.
1. 선택 **[!UICONTROL 계속]**.
   ![새 키 구성](assets/mobile-push-apple-dev-config-key.png)
1. 구성 검토 및 선택 **[!UICONTROL 등록]**.
1. 다운로드 `.p8` 개인 키. 앱 서피스 구성에서 사용됩니다.
1. 다음 사항에 주의하십시오. **[!UICONTROL 키 ID]**. 앱 서피스 구성에서 사용됩니다.

추가 설명서는 [여기에서](https://help.apple.com/developer-account/#/devcdfbb56a3).

### Apple 개발자 팀 ID 검색

1. Apple 개발자 포털에서 **[!UICONTROL 멤버십]**.
1. 사용자 **[!UICONTROL 팀 ID]** 다른 멤버십 정보와 함께 나열됩니다. 앱 서피스 구성에서 사용됩니다.

## 데이터 수집에 앱 푸시 자격 증명 추가

1. 에서 [데이터 수집 인터페이스](https://experience.adobe.com/data-collection/)왼쪽 패널에서 앱 서피스 탭을 선택합니다.
1. 선택 **[!UICONTROL 앱 서피스 만들기]** 구성을 만들려면
   ![앱 표면 홈](assets/mobile-push-app-surface.png)
1. 을(를) 입력합니다. **[!UICONTROL 이름]** 예를 들어, `Luma App Tutorial`  .
1. 모바일 애플리케이션 구성에서 을 선택합니다. **[!UICONTROL Apple iOS]**.
1. 앱 ID(iOS 번들 ID) 필드에 모바일 앱 번들 ID를 입력합니다. Luma 앱과 함께 를 따르는 경우 이 값은 다음과 같습니다. `com.adobe.luma.tutorial`.
1. 켜기 **[!UICONTROL 푸시 자격 증명]** 단추를 클릭하여 자격 증명을 추가합니다.
1. 끌어서 놓기 `.p8` **Apple 푸시 알림 인증 키** 파일.
1. 을 만드는 동안 지정된 10자 문자열인 키 ID를 제공합니다 `p8` 인증 키. 의 키 탭에서 찾을 수 있습니다 **인증서, 식별자 및 프로필** 페이지.
1. 팀 ID를 제공합니다. 이 값은 **멤버십** 탭.
1. **[!UICONTROL 저장]**을 선택합니다.
   ![앱 서피스 구성](assets/mobile-push-app-surface-config.png)

## Adobe Journey Optimizer 태그 확장 설치

1. 다음으로 이동 [!UICONTROL 태그] > [!UICONTROL 확장] > [!UICONTROL 카탈로그], 및에서 **[!UICONTROL Adobe Journey Optimizer]** 확장.
1. 확장을 설치합니다.
   ![ajo 확장 설치](assets/mobile-push-tags-install.png)
1. 선택 `CJM Push Tracking Experience Event Dataset` Adobe Experience Platform 데이터 세트.
   ![AJO 확장 설정](assets/mobile-push-tags-ajo.png)
1. 선택 **[!UICONTROL 라이브러리 및 빌드에 저장]**.

>[!NOTE]
>옵션으로 &quot;CJM 푸시 추적 경험 이벤트 데이터 세트&quot;가 표시되지 않는 경우 고객 지원 센터에 문의하십시오.

## 앱에서 Adobe Journey Optimizer 구현

이전 단원에서 설명한 대로 모바일 태그 확장을 설치하면 구성만 제공됩니다. 다음으로 메시징 SDK를 설치하고 등록해야 합니다. 이 단계를 명확하지 않은 경우 [SDK 설치](install-sdks.md) 섹션을 참조하십시오.

>[!NOTE]
>
>을(를) 완료한 경우 [SDK 설치](install-sdks.md) 섹션에 있는 경우 SDK가 이미 설치되어 있으므로 단계를 건너뛸 수 #7.

1. 다음 문서를 엽니다. `Podfile` 다음 줄을 추가하고 파일을 저장합니다.

   `pod 'AEPMessaging', '~>1'`
1. 터미널을 열고 을 포함하는 폴더로 이동합니다 `Podfile`.
1. 명령을 실행하여 SDK 설치 `pod install`.
   ![동의 유효성 검사](assets/mobile-push-terminal-install.png)
1. XCode를 열고 다음 위치로 이동합니다. `AppDelegate.swift`.
1. 가져오기 목록에 다음을 추가합니다.

   `import AEPMessaging`
1. 추가 `Messaging.self` 등록할 확장의 배열에 추가합니다.
1. 파일에 다음 함수를 추가합니다.

   ```swift
   func application(_: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
       MobileCore.setPushIdentifier(deviceToken)
   }
   ```

   이 함수는 앱이 설치된 장치에 고유한 장치 토큰을 검색하고 푸시 메시지 전송을 위해 Adobe/Apple으로 보냅니다.

## 테스트 푸시 메시지를 전송하여 유효성 검사

1. 를 검토합니다. [설정 지침](assurance.md) 섹션을 참조하십시오.
1. 실제 장치에 앱을 설치합니다.
1. Assurance 생성 URL을 사용하여 앱을 시작합니다.
1. 앱을 백그라운드로 보냅니다.
1. Assurance UI에서 **[!UICONTROL 구성]**.
   ![click 구성](assets/mobile-push-validate-config.png)
1. 을(를) 선택합니다 **[!UICONTROL +]** 다음 단추 **[!UICONTROL 푸시 디버그]**.
1. **[!UICONTROL 저장]**을 선택합니다.
   ![저장](assets/mobile-push-validate-save.png)
1. 선택 **[!UICONTROL 푸시 디버그]** 왼쪽 탐색에서 를 클릭합니다.
1. 에서 장치를 선택합니다 **[!UICONTROL 클라이언트 목록]**.
1. 오류가 발생하지 않는지 확인합니다.
   ![유효성 검사](assets/mobile-push-validate-confirm.png)
1. 아래로 스크롤하여 선택합니다. **[!UICONTROL 테스트 푸시 알림 보내기]**.
1. 및 오류를 받지 않고 장치에서 메시지를 수신하는지 확인합니다.
   ![테스트 푸시 보내기](assets/mobile-push-validate-send-test.png)

다음: **[결론 및 다음 단계](conclusion.md)**

>[!NOTE]
>
>Adobe Experience Platform Mobile SDK에 대한 학습에 시간을 내주셔서 감사합니다. 질문이 있거나 일반 피드백을 공유하거나 향후 컨텐츠에 대한 제안 사항이 있는 경우 해당 정보를 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)