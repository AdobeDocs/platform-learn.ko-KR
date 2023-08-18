---
title: Adobe Journey Optimizer 푸시 메시지
description: Platform Mobile SDK 및 Adobe Journey Optimizer을 사용하여 모바일 앱에 푸시 메시지를 만드는 방법을 알아봅니다.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Push
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 2%

---

# Adobe Journey Optimizer 푸시 메시지

Platform Mobile SDK 및 Adobe Journey Optimizer을 사용하여 모바일 앱용 푸시 메시지를 만드는 방법을 알아봅니다.

Journey Optimizer을 사용하면 여정을 만들고 타겟팅된 대상자에게 메시지를 보낼 수 있습니다. Journey Optimizer을 사용하여 푸시 알림을 전송하기 전에 적절한 구성 및 통합이 있는지 확인해야 합니다. Adobe Journey Optimizer의 푸시 알림 데이터 흐름을 이해하려면 다음을 참조하십시오. [설명서](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-gs.html).

>[!NOTE]
>
>이 단원은 선택 사항이며 푸시 메시지를 전송하려는 Adobe Journey Optimizer 사용자에게만 적용됩니다.


## 전제 조건

* SDK가 설치 및 구성된 앱을 빌드하고 실행했습니다.
* Adobe Journey Optimizer에 대한 액세스 및 설명된 대로 충분한 권한 [여기](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). 또한 다음 Adobe Journey Optimizer 기능에 대한 충분한 권한이 필요합니다.
   * 앱 표면을 만듭니다.
   * 여정 만들기
   * 메시지 만들기.
   * 메시지 사전 설정 만들기.
* 인증서, 식별자 및 키를 만들 수 있는 충분한 액세스 권한이 있는 유료 Apple 개발자 계정입니다.
* 테스트를 위한 물리적 iOS 장치.

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* APN(Apple 푸시 알림 서비스)에 앱 ID를 등록합니다.
* 만들기 **[!UICONTROL 앱 표면]** AJO에서.
* 업데이트 **[!UICONTROL 스키마]** 푸시 메시지 필드를 포함합니다.
* 설치 및 구성 **[!UICONTROL Adobe Journey Optimizer]** 태그 확장.
* AJO 태그 확장을 포함하도록 앱을 업데이트합니다.
* Assurance에서 설정의 유효성을 검사합니다.
* 테스트 메시지를 보냅니다.


## APN에 앱 ID 등록

다음 단계는 Adobe Experience Cloud 전용이 아니며 APN 구성을 안내하도록 설계되었습니다.

### 개인 키 만들기

1. Apple 개발자 포털에서 **[!UICONTROL 키]**.
1. 키를 만들려면 다음을 선택합니다. **[!UICONTROL +]**.
   ![새 키 만들기](assets/mobile-push-apple-dev-new-key.png)

1. 다음을 제공합니다. **[!UICONTROL 키 이름]**.
1. 다음 항목 선택 **[!UICONTROL APN]** 확인란.
1. 선택 **[!UICONTROL 계속]**.
   ![새 키 구성](assets/mobile-push-apple-dev-config-key.png)
1. 구성 검토 및 선택 **[!UICONTROL 등록]**.
1. 다운로드 `.p8` 개인 키. 앱 표면 구성에서 사용됩니다.
1. 다음을 기록해 둡니다. [!UICONTROL 키 ID]. 앱 표면 구성에서 사용됩니다.
1. 다음을 기록해 둡니다. [!UICONTROL 팀 ID]. 앱 표면 구성에서 사용됩니다.
   ![주요 세부 정보](assets/push-apple-dev-key-details.png)

추가 설명서는 다음과 같습니다. [여기에서 찾음](https://help.apple.com/developer-account/#/devcdfbb56a3).

## 데이터 수집에서 앱 푸시 자격 증명 추가

1. 다음에서 [데이터 수집 인터페이스](https://experience.adobe.com/data-collection/), 선택 **[!UICONTROL 앱 표면]** 왼쪽 패널에서
1. 구성을 만들려면 다음을 선택합니다 **[!UICONTROL 앱 표면 만들기]**.
   ![앱 표면 홈](assets/push-app-surface.png)
1. 입력 **[!UICONTROL 이름]** 예를 들어 구성의 경우 `Luma App Tutorial`  .
1. 모바일 애플리케이션 구성에서 을 선택합니다. **[!UICONTROL Apple iOS]**.
1. 앱 ID(iOS 번들 ID) 필드에 모바일 앱 번들 ID를 입력합니다. Luma 앱과 함께 다음을 수행하는 경우 해당 값은 다음과 같습니다. `com.adobe.luma.tutorial.swiftui`.
1. 전환 **[!UICONTROL 푸시 자격 증명]** 자격 증명을 추가하는 버튼입니다.
1. 을(를) 끌어다 놓기 `.p8` **Apple 푸시 알림 인증 키** 파일.
1. 다음을 제공합니다 **[!UICONTROL 키 ID]**&#x200B;를 만드는 동안 할당된 10자 문자열 `p8` 인증 키. 다음에서 찾을 수 있습니다 **[!UICONTROL 키]** 의 탭 **인증서, 식별자 및 프로필** Apple 개발자 포털 페이지의 페이지입니다.
1. 다음을 제공합니다 **[!UICONTROL 팀 ID]**. 팀 ID는 **멤버십** 또는 Apple 개발자 포털 페이지 상단에 있는 탭입니다.
1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

   ![앱 표면 구성](assets/push-app-surface-config.png)

## Adobe Journey Optimizer 태그 확장 설치

1. 다음으로 이동 **[!UICONTROL 태그]** > **[!UICONTROL 확장]** > **[!UICONTROL 카탈로그]**,
1. 속성을 엽니다. 예 **[!UICONTROL Luma 모바일 앱 튜토리얼]**.
1. 선택 **[!UICONTROL 카탈로그]**.
1. 검색 **[!UICONTROL Adobe Journey Optimizer]** 확장명.
1. 확장을 설치합니다.
1. 다음에서 **[!UICONTROL 확장 설치]** 대화 상자
   1. 환경 선택(예: ) **[!UICONTROL 개발]**.
   1. 다음 항목 선택 **[!UICONTROL AJO 푸시 추적 경험 이벤트 데이터 세트]** 데이터 세트 **[!UICONTROL 이벤트 데이터 세트]** 드롭다운 목록입니다.
      ![AJO 확장 설정](assets/push-tags-ajo.png)
   1. 선택 **[!UICONTROL 라이브러리 및 빌드에 저장]**.

>[!NOTE]
>
>표시되지 않으면 `AJO Push Tracking Experience Event Dataset` 선택 사항으로 고객 지원 센터에 문의하십시오.
>

## 앱에서 Adobe Journey Optimizer 구현

이전 단원에서 설명한 대로 모바일 태그 확장을 설치하면 구성만 제공됩니다. 그런 다음 메시징 SDK를 설치하고 등록해야 합니다. 이러한 단계가 명확하지 않으면 다음을 검토하십시오. [SDK 설치](install-sdks.md) 섹션.

>[!NOTE]
>
>을(를) 완료한 경우 [SDK 설치](install-sdks.md) 섹션에서 SDK가 이미 설치되어 있는 경우 #7단계로 건너뛸 수 있습니다.
>

1. Xcode에서 다음을 확인합니다 [AEP 메시징](https://github.com/adobe/aepsdk-messaging-ios.git) 패키지 종속 항목의 패키지 목록에 추가됩니다. 다음을 참조하십시오 [Swift 패키지 관리자](install-sdks.md#swift-package-manager).
1. Xcode를 열고 다음으로 이동 **[!UICONTROL AppDelegate]**.
1. 확인 `AEPMessaging` 는 가져오기 목록의 일부입니다.

   `import AEPMessaging`

1. 확인 `Messaging.self` 는 등록 중인 확장 배열의 일부입니다.

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

1. 추가 `MobileCore.setPushIdentifier` (으)로 `application(_, didRegisterForRemoteNotificationsWithDeviceToken)` 함수.

   ```swift {highlight="7"}
   func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
       // Required to log the token
       let tokenParts = deviceToken.map { data in String(format: "%02.2hhx", data) }
       let token = tokenParts.joined()
       Logger.notifications.info("didRegisterForRemoteNotificationsWithDeviceToken - device token: \(token)")
   
       // Send push token to Experience Platform
       MobileCore.setPushIdentifier(deviceToken)
       currentDeviceToken = token
   }
   ```

   이 함수는 앱이 설치된 장치에 고유한 장치 토큰을 검색하고 푸시 메시지 전달을 위해 토큰을 Adobe Apple으로 보냅니다.

## 테스트 푸시 메시지를 보내 유효성 확인

1. 리뷰 [설치 지침](assurance.md) 섹션.
1. 물리적 장치 또는 시뮬레이터에 앱을 설치합니다.
1. 보증 생성 URL을 사용하여 앱을 실행합니다.
1. Assurance UI에서 **[!UICONTROL 구성]**.
   ![구성 클릭](assets/push-validate-config.png)
1. 다음 항목 선택 ![플러스](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) 단추 옆에 있음 **[!UICONTROL 푸시 디버그]**.
1. **[!UICONTROL 저장]**을 선택합니다.
   ![저장](assets/push-validate-save.png)
1. 선택 **[!UICONTROL 푸시 디버그]** 왼쪽 탐색에서.
1. 다음 항목 선택 **[!UICONTROL 설정 유효성 검사]** 탭.
1. 에서 장치 선택 **[!UICONTROL 클라이언트]** 목록을 표시합니다.
1. 오류가 발생하지 않는지 확인합니다.
   ![유효성 검사](assets/push-validate-confirm.png)
1. 다음 항목 선택 **[!UICONTROL 테스트 푸시 보내기]** 탭.
1. (선택 사항) 의 기본 세부 정보 변경 **[!UICONTROL 제목]** 및 **[!UICONTROL 본문]**
1. 선택 ![버그](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bug_18_N.svg) **[!UICONTROL 테스트 푸시 알림 보내기]**.
1. 다음 확인: **[!UICONTROL 테스트 결과]**.
1. 앱에 푸시 알림이 표시됩니다.

   <img src="assets/luma-app-push.png" width="300" />


>[!SUCCESS]
>
>이제 Adobe Experience Platform Mobile SDK용 Adobe Journey Optimizer 확장을 사용하여 푸시 알림에 대한 앱을 활성화했습니다.<br/>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하려는 경우 또는 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

다음: **[결론 및 다음 단계](conclusion.md)**
