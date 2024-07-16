---
title: Target 및 Platform Mobile SDK를 사용하여 모바일 앱에서 A/B 테스트 수행
description: Platform Mobile SDK 및 Adobe Target과 함께 모바일 앱에서 Target A/B 테스트를 사용하는 방법을 알아봅니다.
solution: Data Collection,Target
feature-set: Target
feature: A/B Tests
jira: KT-14641
exl-id: 87546baa-2d8a-4cce-b531-bec3782d2e90
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '1745'
ht-degree: 1%

---

# Adobe Target을 사용하여 최적화 및 개인화

Platform Mobile SDK 및 Adobe Target을 사용하여 모바일 앱에서 경험을 최적화하고 개인화하는 방법을 알아봅니다.

Target은 고객의 경험을 조정하고 개인화해야 하는 모든 기능을 제공합니다. Target을 사용하면 웹 및 모바일 사이트, 앱, 소셜 미디어 및 기타 디지털 채널에서 매출을 극대화할 수 있습니다. Target은 A/B 테스트, 다변량 테스트, 제품 및 콘텐츠 추천, 콘텐츠 타겟팅, AI를 통한 콘텐츠 자동 개인화 등을 수행할 수 있습니다. 이 단원에서는 Target의 A/B 테스트 기능에 초점을 둡니다. 자세한 내용은 [A/B 테스트 개요](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=en)를 참조하십시오.

![아키텍쳐](assets/architecture-at.png)

Target에서 A/B 테스트를 수행하려면 먼저 적절한 구성 및 통합이 있는지 확인해야 합니다.

>[!NOTE]
>
>이 단원은 선택 사항이며 A/B 테스트를 수행하려는 Adobe Target 사용자에게만 적용됩니다.


## 전제 조건

* SDK가 설치 및 구성된 앱을 빌드하고 실행했습니다.
* [여기](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=ko-KR)에서 설명한 대로 사용 권한, 올바르게 구성된 역할, 작업 공간 및 속성을 사용하여 Adobe Target에 액세스합니다.


## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* Target 통합을 위해 데이터 스트림을 업데이트합니다.
* Journey Optimizer - Decisioning 확장을 사용하여 태그 속성을 업데이트합니다.
* 스키마를 업데이트하여 제안 이벤트를 캡처합니다.
* Assurance에서 설정의 유효성을 검사합니다.
* Target에서 간단한 A/B 테스트를 만듭니다.
* 앱을 업데이트하여 Optimizer 확장을 등록합니다.
* 앱에서 A/B 테스트를 구현합니다.
* Assurance에서 구현의 유효성을 검사합니다.


## 설정

>[!TIP]
>
>[Journey Optimizer 오퍼](journey-optimizer-offers.md) 단원의 일부로 앱을 이미 설정한 경우 이 설정 섹션의 일부 단계를 이미 수행했을 수 있습니다.

### 데이터 스트림 구성 업데이트

#### Adobe Target

모바일 앱에서 Experience Platform Edge Network으로 전송된 데이터가 Adobe Target으로 전달되도록 하려면 데이터 스트림 구성을 업데이트해야 합니다.

1. 데이터 수집 UI에서 **[!UICONTROL 데이터스트림]**&#x200B;을(를) 선택하고 데이터스트림(예: **[!DNL Luma Mobile App]**)을 선택합니다.
1. **[!UICONTROL 서비스 추가]**&#x200B;를 선택하고 **[!UICONTROL 서비스]** 목록에서 **[!UICONTROL Adobe Target]**&#x200B;을(를) 선택합니다.
1. Target Premium 고객이 속성 토큰을 사용하려는 경우 이 통합에 사용할 Target **[!UICONTROL 속성 토큰]** 값을 입력하십시오. Target Standard 사용자는 이 단계를 건너뛸 수 있습니다.

   Target UI의 **[!UICONTROL 관리]** > **[!UICONTROL 속성]**&#x200B;에서 속성을 찾을 수 있습니다. 사용할 속성에 대한 속성 토큰을 표시하려면 ![Code](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg)을(를) 선택하십시오. 속성 토큰에 `"at_property": "xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"`과(와) 같은 형식이 있습니다. `xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx` 값만 입력해야 합니다.

   필요한 경우 Target 환경 ID를 지정할 수 있습니다. Target은 환경을 사용하여 사이트와 사전 프로덕션 환경을 구성하여 손쉽게 관리하고 별도의 보고를 수행합니다. 사전 설정된 환경에는 프로덕션, 스테이징 및 개발이 포함됩니다. 자세한 내용은 [환경](https://experienceleague.adobe.com/docs/target/using/administer/environments.html?lang=en) 및 [대상 환경 ID](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html?lang=en#target-environment-id)를 참조하십시오.

   원할 경우 ID 네임스페이스(예: CRM ID)에서 프로필 동기화를 지원하도록 Target 타사 ID 네임스페이스를 지정할 수 있습니다. 자세한 내용은 [Target 타사 ID 네임스페이스](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html?lang=en#target-third-party-id-namespace)를 참조하십시오.

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

   ![데이터 스트림에 대상 추가](assets/edge-datastream-target.png)


#### Adobe Journey Optimizer

모바일 앱에서 Edge Network으로 전송된 데이터가 의사 결정 관리인 Journey Optimizer으로 전달되도록 하려면 데이터스트림 구성을 업데이트합니다.

1. 데이터 수집 UI에서 **[!UICONTROL 데이터스트림]**&#x200B;을(를) 선택하고 데이터스트림(예: **[!DNL Luma Mobile App]**)을 선택합니다.
1. **[!UICONTROL Experience Platform]**&#x200B;에 대해 ![자세히](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg)를 선택하고 상황에 맞는 메뉴에서 ![편집](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL 편집]**&#x200B;을 선택합니다.
1. **[!UICONTROL 데이터스트림]** > ![폴더](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) > **[!UICONTROL Adobe Experience Platform]** 화면에서 **[!UICONTROL Offer decisioning]**, **[!UICONTROL Edge 세분화]** 및 **[!UICONTROL Personalization 대상]**&#x200B;이 선택되어 있는지 확인하십시오. Journey Optimizer 단원을 따르는 경우 **[!UICONTROL Adobe Journey Optimizer]**&#x200B;을(를) 선택합니다. 자세한 내용은 [Adobe Experience Platform 설정](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#aep)을 참조하세요.
1. 데이터스트림 구성을 저장하려면 **[!UICONTROL 저장]** 을 선택합니다.

   ![AEP 데이터스트림 구성](assets/datastream-aep-configuration-target.png)


### Adobe Journey Optimizer - Decisioning 태그 확장 설치

1. **[!UICONTROL 태그]**(으)로 이동하여 모바일 태그 속성을 찾은 다음 속성을 엽니다.
1. **[!UICONTROL 확장]**&#x200B;을 선택하십시오.
1. **[!UICONTROL 카탈로그]**&#x200B;를 선택하십시오.
1. **[!UICONTROL Adobe Journey Optimizer - Decisioning]** 확장을 검색합니다.
1. 확장을 설치합니다. 확장은 추가 구성이 필요하지 않습니다.

   ![의사 결정 확장 추가](assets/tag-add-decisioning-extension.png)


### 스키마 업데이트

1. 데이터 수집 인터페이스로 이동하여 왼쪽 레일에서 **[!UICONTROL 스키마]**&#x200B;를 선택합니다.
1. 상단 표시줄에서 **[!UICONTROL 찾아보기]**&#x200B;를 선택합니다.
1. 스키마를 선택하여 엽니다.
1. 스키마 편집기에서 **[!UICONTROL 필드 그룹]** 옆에 있는 ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 추가]**&#x200B;을(를) 선택합니다.
1. **[!UICONTROL 필드 그룹 추가]** 대화 상자에서 `proposition`을(를) 검색하고 **[!UICONTROL 경험 이벤트 - 제안 상호 작용]**&#x200B;을 선택하고 **[!UICONTROL 필드 그룹 추가]**를 선택합니다.
   ![제안](assets/schema-fieldgroup-proposition.png)
1. 스키마에 변경 내용을 저장하려면 **[!UICONTROL 저장]**&#x200B;을 선택합니다.


### Assurance에서 설정 확인

Assurance에서 설정을 확인하려면:

1. Assurance UI로 이동합니다.
1. 왼쪽 레일에서 **[!UICONTROL 구성]**&#x200B;을 선택하고 **[!UICONTROL ADOBE JOURNEY OPTIMIZER DECISIONING]** 아래의 **[!UICONTROL 설정 유효성 검사]** 옆에 있는 ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg)을 선택합니다.
1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.
1. 왼쪽 레일에서 **[!UICONTROL 설정 유효성 검사]**를 선택합니다. 데이터 스트림 설정과 SDK 설정이 모두 애플리케이션에서 검증되었습니다.
   ![AJO 의사 결정 유효성 검사](assets/ajo-decisioning-validation.png)

## A/B 테스트 만들기

소개에서 언급한 대로 Adobe Target에서 만들고 모바일 앱에서 구현할 수 있는 다양한 유형의 활동이 있습니다. 이 단원에서는 A/B 테스트를 구현합니다.

1. Target UI의 상단 표시줄에서 **[!UICONTROL 활동]**&#x200B;을 선택합니다.
1. 컨텍스트 메뉴에서 **[!UICONTROL 활동 만들기]** 및 **[!UICONTROL A/B 테스트]**&#x200B;를 선택합니다.
1. Target Premium 고객이 데이터스트림에 속성 토큰을 지정한 경우 **[!UICONTROL A/B 테스트 활동 만들기]** 대화 상자에서 **[!UICONTROL Mobile]**&#x200B;을 **[!UICONTROL 유형]**(으)로 선택하고, **[!UICONTROL Workspace 선택]** 목록에서 작업 영역을 선택하고, **[!UICONTROL 속성 선택]** 목록에서 속성을 선택합니다.
1. **[!UICONTROL 만들기]**를 선택합니다.
   ![대상 활동 만들기](assets/target-create-activity1.png)

1. **[!UICONTROL 제목 없는 활동]** 화면의 **[!UICONTROL 경험]** 단계에서 다음을 수행합니다.

   1. **[!UICONTROL 위치 1]** 아래의 **[!UICONTROL 위치 선택]**&#x200B;에 `luma-mobileapp-abtest`을(를) 입력하십시오. 이 위치 이름(mbox라고도 함)은 앱 구현에서 나중에 사용됩니다.
   1. **[!UICONTROL 기본 콘텐츠]** 옆에 있는 ![Chrevron down](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg)을 선택하고 상황에 맞는 메뉴에서 **[!UICONTROL JSON 오퍼 만들기]**&#x200B;를 선택합니다.
   1. 다음 JSON을 **[!UICONTROL 올바른 JSON 개체를 입력하십시오]**.

      ```json
      { 
          "title": "Luma Anaolog Watch",
          "text": "Designed to stand up to your active lifestyle, this women's Luma Analog Watch features a tasteful brushed chrome finish and a stainless steel, water-resistant construction for lasting durability.", 
          "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/gear/watches/Luma_Analog_Watch.jpg" 
      }
      ```

   1. **[!UICONTROL + 경험 추가]**&#x200B;를 선택합니다.

      ![경험 A](assets/target-create-activity-experienceA.png)

   1. 경험 B에 대해 b단계와 c단계를 반복하되 대신 다음 JSON을 사용하십시오.

      ```json
      { 
          "title": "Aim Analog Watch",
          "text": "The flexible, rubberized strap is contoured to conform to the shape of your wrist for a comfortable all-day fit. The face features three illuminated hands, a digital read-out of the current time, and stopwatch functions.", 
          "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/gear/watches/Aim_Watch.jpg" 
      }
      ```

   1. **[!UICONTROL 다음]**&#x200B;을 선택합니다.

      ![경험 B](assets/target-create-activity-experienceB.png)

1. **[!DNL Targeting]** 단계에서 A/B 테스트 설정을 검토합니다. 기본적으로 두 오퍼는 모두 모든 방문자에게 동일하게 할당됩니다. 계속하려면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

   ![타깃팅](assets/taget-targeting.png)

1. **[!UICONTROL 목표 및 설정]** 단계:

   1. 제목 없는 활동의 이름을 `Luma Mobile SDK Tutorial - A/B Test Example`(으)로 변경합니다.
   1. A/B 테스트의 **[!UICONTROL 목표]**&#x200B;를 입력하십시오(예: `A/B Test for Luma mobile app tutorial`).
   1. **[!UICONTROL 목표 지표]** > **[!UICONTROL 내 기본 목표]** 타일에서 **[!UICONTROL 전환]**, **[!UICONTROL mbox 확인함]**&#x200B;을(를) 선택하고 위치(mbox) 이름(예: `luma-mobileapp-abtest`)을 입력하십시오.
   1. **[!UICONTROL 저장 및 닫기]**&#x200B;를 선택합니다.

      ![목표 설정](assets/target-goals.png)

1. **[!UICONTROL 모든 활동]** 화면으로 돌아가기:

   1. 활동에서 ![자세히](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg)을(를) 선택합니다.
   1. A/B 테스트를 활성화하려면 ![재생](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg) **[!UICONTROL 활성화]**&#x200B;를 선택하십시오.

   ![활성화](assets/target-activate.png)


## 앱에서 Target 구현

이전 단원에서 설명한 대로 모바일 태그 확장을 설치하면 구성만 제공됩니다. 그런 다음 Optimize SDK를 설치하고 등록해야 합니다. 이 단계가 명확하지 않으면 [SDK 설치](install-sdks.md) 섹션을 검토하십시오.

>[!NOTE]
>
>[SDK 설치](install-sdks.md) 섹션을 완료한 경우 SDK가 이미 설치되어 있으므로 이 단계를 건너뛸 수 있습니다.
>

1. Xcode에서 패키지 종속 항목의 패키지 목록에 [AEP 최적화](https://github.com/adobe/aepsdk-messaging-ios)가 추가되었는지 확인하십시오. [Swift 패키지 관리자](install-sdks.md#swift-package-manager)를 참조하세요.
1. Xcode 프로젝트 탐색기에서 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL AppDelegate]**(으)로 이동합니다.
1. `AEPOptimize`이(가) 가져오기 목록의 일부인지 확인하십시오.

   `import AEPOptimize`

1. `Optimize.self`이(가) 등록 중인 확장 배열의 일부인지 확인하십시오.

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

1. Xcode 프로젝트 탐색기에서 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!DNL MobileSDK]**(으)로 이동합니다. ` func updatePropositionAT(ecid: String, location: String) async` 함수를 찾습니다. 다음 코드를 추가합니다.

   ```swift
   // set up the XDM dictionary, define decision scope and call update proposition API
   Task {
       let ecid = ["ECID" : ["id" : ecid, "primary" : true] as [String : Any]]
       let identityMap = ["identityMap" : ecid]
       let xdmData = ["xdm" : identityMap]
       let decisionScope = DecisionScope(name: location)
       Optimize.clearCachedPropositions()
       Optimize.updatePropositions(for: [decisionScope], withXdm: xdmData)
   }
   ```

   이 함수:

   * A/B 테스트를 표시해야 하는 프로필을 식별하기 위해 ECID가 포함된 XDM 사전 `xdmData`을(를) 설정합니다.
   * A/B 테스트를 표시할 위치의 배열인 `decisionScope`을(를) 정의합니다.

   그런 다음 함수는 [`Optimize.clearCachedPropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#clearpropositions) 및 [`Optimize.updatePropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#updatepropositions) API를 호출합니다. 이러한 함수는 캐시된 모든 제안을 지우고 이 프로필에 대한 제안을 업데이트합니다. 이 컨텍스트에서 제안은 Target 활동(A/B 테스트)에서 선택되고 [A/B 테스트 만들기](#create-an-ab-test)에서 정의한 경험(오퍼)입니다.

1. Xcode 프로젝트 탐색기에서 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Personalization]** > **[!DNL TargetOffersView]**(으)로 이동합니다. `func onPropositionsUpdateAT(location: String) async {` 함수를 찾아 이 함수의 코드를 검사합니다. 이 함수에서 가장 중요한 부분은 [`Optimize.onPropositionsUpdate`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#onpropositionsupdate) API 호출입니다.
   * 결정 범위(A/B 테스트에서 정의한 위치)를 기반으로 현재 프로필에 대한 제안을 검색합니다.
   * 제안에서 오퍼를 검색합니다.
   * 앱에서 제대로 표시될 수 있도록 오퍼의 콘텐츠를 래핑 해제합니다.
   * 오퍼에 대한 `displayed()` 작업을 트리거하여 오퍼가 표시되었음을 알리는 이벤트를 Platform Edge Network에 다시 보냅니다.

1. **[!DNL TargetOffersView]**&#x200B;에서 `.onFirstAppear` 한정자에 다음 코드를 추가하십시오. 이 코드는 오퍼를 업데이트하기 위한 콜백이 한 번만 등록되도록 합니다.

   ```swift
   // Invoke callback for offer updates
   Task {
       await self.onPropositionsUpdateAT(location: location)
   }
   ```

1. **[!DNL TargetOffersView]**&#x200B;에서 `.task` 한정자에 다음 코드를 추가하십시오. 이 코드는 보기를 새로 고칠 때 오퍼를 업데이트합니다.

   ```swift
   // Clear and update offers
   await self.updatePropositionsAT(ecid: currentEcid, location: location)
   ```

[`Optimize.updatePropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#updatepropositions) API를 호출할 때 데이터 사전에 추가하여 개인화 쿼리 요청에서 추가 Target 매개 변수(예: mbox, 프로필, 제품 또는 주문 매개 변수)를 Experience Edge 네트워크에 보낼 수 있습니다. 자세한 내용은 [Target 매개 변수](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/#target-parameters)를 참조하십시오.


## 앱을 사용하여 유효성 검사

1. ![재생](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg)을 사용하여 시뮬레이터나 Xcode의 실제 장치에서 앱을 다시 빌드하고 실행합니다.

1. **[!UICONTROL 개인화]** 탭으로 이동합니다.

1. 아래쪽으로 스크롤하면 A/B 테스트에서 정의한 두 오퍼 중 하나가 **[!UICONTROL TARGET]** 타일에 표시됩니다.

   <img src="assets/target-app-offer.png" width="300">


## Assurance에서 구현 유효성 검사

Assurance에서 A/B 테스트를 확인하려면 다음을 수행하십시오.

1. [설치 지침](assurance.md#connecting-to-a-session) 섹션을 검토하여 시뮬레이터 또는 장치를 Assurance에 연결하십시오.
1. 왼쪽 레일에서 **[!UICONTROL 구성]**&#x200B;을 선택하고 **[!UICONTROL ADOBE JOURNEY OPTIMIZER DECISIONING]** 아래의 **[!UICONTROL 검토 및 시뮬레이션]** 옆에 있는 ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg)을 선택합니다.
1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.
1. 왼쪽 레일에서 **[!UICONTROL 검토 및 시뮬레이션]**&#x200B;을 선택합니다. 데이터 스트림 설정과 SDK 설정이 모두 애플리케이션에서 검증되었습니다.
1. 상단 표시줄에서 **[!UICONTROL 요청]**&#x200B;을(를) 선택합니다. **[!DNL Target]** 요청이 표시됩니다.
   ![AJO 의사 결정 유효성 검사](assets/assurance-decisioning-requests.png)

1. Target 오퍼에 대한 설정을 확인하는 추가 기능을 위해 **[!UICONTROL 시뮬레이션]** 및 **[!UICONTROL 이벤트 목록]** 탭을 탐색할 수 있습니다.

## 다음 단계

관련성이 있고 적용 가능한 경우 더 많은 A/B 테스트 또는 기타 Target 활동(예: 경험 타기팅, 다변량 테스트)을 앱에 추가하기 시작할 수 있는 모든 도구가 있어야 합니다. [GitHub 저장소 for the Optimize extension](https://github.com/adobe/aepsdk-optimize-ios)에서 Adobe Target 오퍼를 추적하는 방법에 대한 전용 [자습서](https://opensource.adobe.com/aepsdk-optimize-ios/#/tutorials/README)에 대한 링크를 찾을 수 있는 자세한 정보를 확인할 수 있습니다.

>[!SUCCESS]
>
>A/B 테스트용 앱을 활성화하고 Adobe Target 및 Adobe Experience Platform Mobile SDK용 Adobe Journey Optimizer - Decisioning 확장을 사용한 A/B 테스트의 결과를 표시했습니다.
>
>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하고 싶거나 향후 콘텐츠에 대한 제안이 있는 경우 이 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)에서 공유하십시오.

다음: **[결론 및 다음 단계](conclusion.md)**
