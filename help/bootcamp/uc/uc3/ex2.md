---
title: Bootcamp - 물리 및 디지털 혼합 - Journey Optimizer 이벤트 만들기
description: Bootcamp - 물리 및 디지털 혼합 - Journey Optimizer 이벤트 만들기
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 3d47c686-c2d8-4961-a05b-0990025392fa
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# 3.2 이벤트 만들기

다음으로 이동하여 Adobe Journey Optimizer에 로그인 [Adobe Experience Cloud](https://experience.adobe.com). 클릭 **Journey Optimizer**.

![ACOP](./images/acophome.png)

다음 페이지로 리디렉션됩니다. **홈**  Journey Optimizer에서 봅니다. 먼저 올바른 샌드박스를 사용하고 있는지 확인하십시오. 사용할 샌드박스는 이라고 합니다. `Bootcamp`. 한 샌드박스에서 다른 샌드박스로 변경하려면 를 클릭합니다. **Prod** 목록에서 샌드박스를 선택합니다. 이 예에서 샌드박스는 다음과 같이 이름이 지정됩니다. **Bootcamp2**. 그러면 다음 위치에 있게 됩니다. **홈** 샌드박스 보기 `Bootcamp`.

![ACOP](./images/acoptriglp.png)

왼쪽 메뉴에서 아래로 스크롤하고 을 클릭합니다. **구성**. 그런 다음 **관리** 아래에 있는 단추 **이벤트**.

![ACOP](./images/acopmenu.png)

그러면 사용 가능한 모든 이벤트의 개요가 표시됩니다. 클릭 **이벤트 만들기** 을 클릭하여 나만의 이벤트를 만듭니다.

![ACOP](./images/emptyevent.png)

그러면 비어 있는 새 이벤트 창이 나타납니다.

먼저 이벤트에 다음과 같은 이름을 지정합니다. `yourLastNameBeaconEntryEvent` 다음과 같은 설명 추가 `Beacon Entry Event`.

![ACOP](./images/eventdescription.png)

그런 다음 **유형** 이(가) (으)로 설정됨 **단일**, 및 **이벤트 ID 유형** 선택, 선택 **시스템 생성됨**.

![ACOP](./images/eventidtype.png)

다음은 스키마 선택 사항입니다. 이 연습을 위해 스키마가 준비되었습니다. 스키마를 사용하십시오. `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

스키마를 선택하면 **필드** 섹션. 이제 마우스를 위에 놓으십시오. **필드** 섹션으로 이동하면 3개의 아이콘 팝업이 표시됩니다. 을(를) 클릭합니다 **편집** 아이콘.

![ACOP](./images/eventpayload.png)

다음이 표시됩니다. **필드** 여정을 개인화하는 데 필요한 일부 필드를 선택해야 하는 창 팝업입니다.  나중에 Adobe Experience Platform에 이미 있는 데이터를 사용하여 다른 프로필 속성을 선택합니다.

![ACOP](./images/eventfields.png)

개체가 표시될 때까지 아래로 스크롤합니다 `Place context` 확인란을 선택합니다. 이를 통해 고객 위치의 모든 컨텍스트를 여정이 사용할 수 있도록 합니다. 클릭 **확인** 변경 사항을 저장합니다.

![ACOP](./images/eventpayloadbr.png)

그럼 이걸 보셔야죠 클릭 **저장** 변경 사항을 저장하려면 한 번 더 하십시오.

![ACOP](./images/eventsave.png)

이제 이벤트가 구성 및 저장되었습니다.

![ACOP](./images/eventdone.png)

이벤트를 다시 클릭하여 **이벤트 편집** 화면을 다시 표시합니다. 마우스로 가리키기 **필드** 다시 3개의 아이콘을 표시합니다. 을(를) 클릭합니다 **보기** 아이콘.

![ACOP](./images/viewevent.png)

이제 예상 페이로드의 예를 볼 수 있습니다.
이벤트에는 고유한 오케스트레이션 eventID가 있으며, 이 ID는 표시될 때까지 해당 페이로드에서 아래로 스크롤하여 찾을 수 있습니다 `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

이벤트 ID는 다음 연습 중 하나에서 빌드할 여정을 트리거하기 위해 Adobe Experience Platform에 전송해야 하는 ID입니다. 이 eventID는 나중에 필요할 수 있으므로 기억하십시오.
`"eventID": "e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5"`

클릭 **확인**, 클릭 후 **취소**.

이제 이 연습을 완료했습니다.

다음 단계: [3.3 여정 및 푸시 알림 만들기](./ex3.md)

[사용자 흐름으로 돌아가기 3](./uc3.md)

[모든 모듈로 돌아가기](../../overview.md)
