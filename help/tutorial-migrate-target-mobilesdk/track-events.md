---
title: 전환 이벤트 추적 - 모바일 앱의 Adobe Target 구현을 Adobe Journey Optimizer - Decisioning 확장으로 마이그레이션합니다.
description: Adobe Journey Optimizer - Decisioning Mobile 확장을 사용하여 Adobe Target 전환 이벤트를 추적하는 방법에 대해 알아봅니다
exl-id: 7b53aab1-0922-4d9f-8bf0-f5cf98ac04c4
source-git-commit: d2da62ed2d36f73af1c8053be5af27feea32cb14
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# Decisioning 모바일 확장을 사용하여 Target 전환 이벤트 추적

대부분의 Target 활동의 목표는 구매, 등록, 클릭 수 등과 같은 중요한 사용자 작업을 애플리케이션에서 수행하는 것입니다. Target 구현은 일반적으로 사용자 지정 전환 이벤트를 사용하여 이러한 작업을 추적하며, 종종 전환에 대한 추가 세부 사항이 포함됩니다. Target에 대한 전환 이벤트는 Target SDK과 유사한 SDK 최적화 를 사용하여 추적할 수 있습니다. 아래 표와 같이 전환 이벤트를 추적하려면 특정 API를 호출해야 합니다.

| 활동 목표 | Target 확장 | Decisioning 확장 |
|---|---|---|
| mbox 위치(범위)에 대한 보기 전환 이벤트 추적 | mbox 위치를 볼 때 [displayedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} API를 호출합니다. | mbox 위치에 대한 오퍼를 볼 때 [displayed](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} API를 호출합니다. 이렇게 하면 이벤트 유형 decisioning.propositionDisplay가 있는 이벤트가 Experience Edge 네트워크로 전송됩니다. **이 작업은 Target 활동에서 방문자를 늘리는 데 필수적이며 일반 Target 오퍼와 기본 Target 오퍼를 모두 제공할 때 수행해야 합니다.** |
| mbox 위치(범위)에 대한 클릭 전환 이벤트 추적 | mbox 위치를 클릭하면 [clickedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} API를 호출합니다. | mbox 위치에 대한 오퍼를 클릭하면 [taped](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} API를 호출합니다. 이렇게 하면 이벤트 유형 decisioning.propositionInteract가 있는 이벤트가 Experience Edge 네트워크로 전송됩니다. |
| Target 프로필 매개 변수 및 순서 세부 사항과 같은 추가 데이터를 포함할 수 있는 사용자 지정 전환 이벤트를 추적합니다 | [displayedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} 및 [clickedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} API에서 제공하는 TargetParameters 필드에 추가 데이터를 전달합니다. | mbox 위치의 오퍼에서 사용할 수 있는 공용 메서드 [generateDisplayInteractionXdm](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-edge-extension-api){target=_blank} 및 [generateTapInteractionXdm](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-edge-extension-api){target=_blank} API를 사용하여 각각 보기 및 클릭에 대한 XDM 형식의 데이터를 생성합니다. 그런 다음 Edge SDK [sendEvent](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#sendevent){target=_blank} API를 호출하여 추가적인 XDM 및 자유 형식 데이터와 함께 이 추적 XDM 데이터를 Experience Edge 네트워크에 보냅니다. |


다음으로 Decisioning 확장과의 호환성을 보장하기 위해 [대상 및 프로필 스크립트를 업데이트](update-audiences.md)하는 방법을 알아봅니다.

>[!NOTE]
>
>Target 확장에서 Decisioning 확장으로 모바일 Target을 성공적으로 마이그레이션할 수 있도록 지원하기 위해 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=ko#M463)에 게시하여 알려 주십시오.
