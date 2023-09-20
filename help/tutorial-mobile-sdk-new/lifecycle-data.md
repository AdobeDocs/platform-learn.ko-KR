---
title: 라이프사이클 데이터 수집
description: 모바일 앱에서 라이프사이클 데이터를 수집하는 방법에 대해 알아봅니다.
hide: true
source-git-commit: 5f178f4bd30f78dff3243b3f5bd2f9d11c308045
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 3%

---

# 라이프사이클 데이터 수집

모바일 앱에서 라이프사이클 데이터를 수집하는 방법에 대해 알아봅니다.

Adobe Experience Platform 모바일 SDK 라이프사이클 확장을 사용하면 모바일 앱에서 수집 라이프사이클 데이터를 사용할 수 있습니다. Adobe Experience Platform Edge Network 확장은 이 라이프사이클 데이터를 Platform Edge Network로 보낸 다음 데이터스트림 구성에 따라 다른 애플리케이션 및 서비스로 전달합니다. 에 대해 자세히 알아보기 [라이프사이클 확장](https://developer.adobe.com/client-sdks/documentation/lifecycle-for-edge-network/) 를 참조하십시오.


## 전제 조건

* SDK가 설치 및 구성된 앱을 빌드하고 실행했습니다. 이 단원의 일부로 라이프사이클 모니터링을 이미 시작했습니다. 다음을 참조하십시오 [SDK 설치 - AppDelegate 업데이트](install-sdks.md#update-appdelegate) 검토해 보십시오.
* 에 설명된 대로 Assurance 확장을 등록했습니다 [이전 단원](install-sdks.md).

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

<!--
* Add lifecycle field group to the schema.
* -->
* 앱이 전경과 배경 사이를 이동할 때 올바르게 시작/일시 중지하여 정확한 라이프사이클 지표를 활성화합니다.
* 앱에서 Platform Edge Network로 데이터를 전송합니다.
* Assurance에서 유효성 검사

<!--
## Add lifecycle field group to schema

The Consumer Experience Event field group you added in the [previous lesson](create-schema.md) already contains the lifecycle fields, so you can skip this step. If you don't use Consumer Experience Event field group in your own app, you can add the lifecycle fields by doing the following:

1. Navigate to the schema interface as described in the [previous lesson](create-schema.md).
1. Open the **Luma Mobile App Event Schema** schema and select **[!UICONTROL Add]** next to Field groups.
    ![select add](assets/lifecycle-add.png)
1. In the search bar, enter "lifecycle".
1. Select the checkbox next to **[!UICONTROL AEP Mobile Lifecycle Details]**.
1. Select **[!UICONTROL Add field groups]**.
    ![add field group](assets/lifecycle-lifecycle-field-group.png)
1. Select **[!UICONTROL Save]**.
    ![save](assets/lifecycle-lifecycle-save.png)
-->

## 구현 변경 사항

이제 프로젝트를 업데이트하여 라이프사이클 이벤트를 등록할 수 있습니다.

1. 다음으로 이동 **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL SceneDelegate]** 를 입력합니다.

1. 앱을 시작할 때 앱이 백그라운드 상태에서 다시 시작되는 경우 iOS에서 `sceneWillEnterForeground:` delegate 메서드 및 여기서 라이프사이클 시작 이벤트를 트리거할 수 있습니다. 이 코드를 추가할 위치 `func sceneWillEnterForeground(_ scene: UIScene)`:

   ```swift
   // When in foreground start lifecycle data collection
   MobileCore.lifecycleStart(additionalContextData: nil)
   ```

1. 앱이 백그라운드로 전환되면 앱의 라이프사이클 데이터 수집을 일시 중지하려는 경우 `sceneDidEnterBackground:` 위임 메서드. 이 코드를 추가할 위치  `func sceneDidEnterBackground(_ scene: UIScene)`:

   ```swift
   // When in background pause lifecycle data collection
   MobileCore.lifecyclePause()
   }
   ```

## Assurance를 통해 유효성 검사

1. 리뷰 [설치 지침](assurance.md) 시뮬레이터 또는 장치를 Assurance에 연결하고 연결합니다.
1. 앱을 실행합니다.
1. 앱을 백그라운드로 보냅니다. 확인 **[!UICONTROL 라이프사이클 일시 중지]** 보증 UI의 이벤트.
1. 앱을 전경으로 가져옵니다. 확인 **[!UICONTROL 주기 다시 시작]** 보증 UI의 이벤트.
   ![라이프사이클 유효성 검사](assets/lifecycle-lifecycle-assurance.png)


## Platform Edge Network에 데이터 전달

이전 연습에서는 전경 및 배경 이벤트를 Adobe Experience Platform Mobile SDK에 전달했습니다. 이러한 이벤트를 Platform Edge Network에 전달하려면:

1. 선택 **[!UICONTROL 규칙]** (데이터 수집 UI)
   ![규칙 만들기](assets/rule-create.png)
1. 선택 **[!UICONTROL 초기 빌드]** 사용할 라이브러리로 사용됩니다.
1. **[!UICONTROL 새 규칙 만들기]**를 선택합니다.
   ![새 규칙 만들기](assets/rules-create-new.png)
1. 다음에서 **[!UICONTROL 규칙 만들기]** 화면, 입력 `Application Status` 대상 **[!UICONTROL 이름]**.
1. 선택 ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 추가]** 아래 **[!UICONTROL 이벤트]**.
   ![규칙 만들기 대화 상자](assets/rule-create-name.png)
1. 다음에서 **[!UICONTROL 이벤트 구성]** 단계:
   1. 선택 **[!UICONTROL 모바일 코어]** (으)로 **[!UICONTROL 확장]**.
   1. 선택 **[!UICONTROL 전경]** (으)로 **[!UICONTROL 이벤트 유형]**.
   1. **[!UICONTROL 변경사항 유지]**를 선택합니다.
      ![규칙 이벤트 구성](assets/rule-event-configuration.png)
1. 뒤로 이동 **[!UICONTROL 규칙 만들기]** 화면, 선택 ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 추가]** 다음에 **[!UICONTROL 모바일 코어 - 전경]**.
   ![다음 이벤트 구성](assets/rule-event-configuration-next.png)
1. 다음에서 **[!UICONTROL 이벤트 구성]** 단계:
   1. 선택 **[!UICONTROL 모바일 코어]** (으)로 **[!UICONTROL 확장]**.
   1. 선택 **[!UICONTROL 배경]** (으)로 **[!UICONTROL 이벤트 유형]**.
   1. **[!UICONTROL 변경사항 유지]**를 선택합니다.
      ![규칙 이벤트 구성](assets/rule-event-configuration-background.png)
1. 뒤로 이동 **[!UICONTROL 규칙 만들기]** 화면, 선택 ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 추가]** 아래 **[!UICONTROL 작업]**.
   ![규칙 추가 작업](assets/rule-action-button.png)
1. 다음에서 **[!UICONTROL 작업 구성]** 단계:
   1. 선택 **[!UICONTROL Experience Edge 네트워크 Adobe]** (으)로 **[!UICONTROL 확장]**.
   1. 선택 **[!UICONTROL Edge Network로 이벤트 전달]** (으)로 **[!UICONTROL 작업 유형]**.
   1. **[!UICONTROL 변경사항 유지]**를 선택합니다.
      ![규칙 작업 구성](assets/rule-action-configuration.png)
1. 선택 **[!UICONTROL 라이브러리에 저장]**.
   ![규칙 - 라이브러리에 저장](assets/rule-save-to-library.png)
1. 선택 **[!UICONTROL 빌드]** 라이브러리를 다시 빌드합니다.
   ![규칙 - 빌드](assets/rule-build.png)

속성을 성공적으로 빌드하면 이벤트가 Platform Edge Network로 전송되고 이벤트는 데이터 스트림 구성에 따라 다른 애플리케이션 및 서비스로 전달됩니다.

다음이 표시됩니다. **[!UICONTROL 애플리케이션 닫기(백그라운드)]** 및 **[!UICONTROL 애플리케이션 실행(전경)]** 보증의 XDM 데이터가 포함된 이벤트.

![platform Edge로 전송된 라이프사이클의 유효성 검사](assets/lifecycle-edge-assurance.png)

>[!SUCCESS]
>
>이제 응용 프로그램 상태(전경, 배경) 이벤트를 Adobe Experience Platform Edge Network와 데이터 스트림에 정의한 모든 서비스에 보내도록 앱을 설정했습니다.<br>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하려는 경우 또는 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

다음: **[이벤트 데이터 추적](events.md)**
