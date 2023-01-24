---
title: Bootcamp - 실제 및 디지털 혼합 - Journey Optimizer 이벤트 만들기 - 브라질
description: Bootcamp - 실제 및 디지털 혼합 - Journey Optimizer 이벤트 만들기 - 브라질
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# 3.2 이벤트 만들기

다음 위치로 이동하여 Adobe Journey Optimizer에 로그인합니다 [Adobe Experience Cloud](https://experience.adobe.com). 클릭 **Journey Optimizer**.

![ACOP](./images/acophome.png)

으로 리디렉션됩니다. **홈**  Journey Optimizer에서 보기. 먼저 올바른 샌드박스를 사용하고 있는지 확인하십시오. 사용할 샌드박스를 이라고 합니다 `Bootcamp`. 한 샌드박스에서 다른 샌드박스로 변경하려면 **Prod** 및 목록에서 샌드박스를 선택합니다. 이 예제에서 샌드박스의 이름은 다음과 같습니다 **Bootcamp2**. 그러면 **홈** 샌드박스 보기 `Bootcamp`.

![ACOP](./images/acoptriglp.png)

왼쪽 메뉴에서 아래로 스크롤하여 **구성**. 그런 다음 **관리** 버튼 아래 **이벤트**.

![ACOP](./images/acopmenu.png)

사용 가능한 모든 이벤트에 대한 개요를 볼 수 있습니다. 클릭 **이벤트 만들기** 을 클릭하여 고유한 이벤트 만들기를 시작합니다.

![ACOP](./images/emptyevent.png)

그러면 빈 이벤트 창이 새로 나타납니다.

먼저 다음과 같은 이름을 이벤트에 지정합니다. `yourLastNameBeaconEntryEvent` 다음과 같은 설명을 추가합니다 `Beacon Entry Event`.

![ACOP](./images/eventdescription.png)

다음으로, **유형** 가 로 설정되어 있습니다. **단일**, 및에 대해 **이벤트 ID 유형** 선택 **시스템 생성**.

![ACOP](./images/eventidtype.png)

다음은 스키마 선택입니다. 이 연습에 대한 스키마가 준비되었습니다. 스키마를 사용하십시오 `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

스키마를 선택하면 **필드** 섹션을 참조하십시오. 이제 다음을 마우스로 가리키면 됩니다 **필드** 섹션을 클릭하면 3개의 아이콘 팝업이 표시됩니다. 을(를) 클릭합니다. **편집** 아이콘.

![ACOP](./images/eventpayload.png)

다음 항목이 표시됩니다. **필드** 창 팝업. 여정을 개인화하는 데 필요한 필드 중 일부를 선택해야 합니다.  Adobe Experience Platform에 이미 있는 데이터를 사용하여 나중에 다른 프로필 속성을 선택합니다.

![ACOP](./images/eventfields.png)

개체가 표시될 때까지 아래로 스크롤합니다. `Place context` 확인란을 선택합니다. 이를 통해 고객 위치의 모든 컨텍스트를 여정이 사용할 수 있습니다. 클릭 **확인** 변경 사항을 저장하려면 을 클릭합니다.

![ACOP](./images/eventpayloadbr.png)

그러면 이게 보입니다. 클릭 **저장** 변경 사항을 저장하려면 한 번 더 클릭합니다.

![ACOP](./images/eventsave.png)

이제 이벤트가 구성 및 저장됩니다.

![ACOP](./images/eventdone.png)

이벤트를 다시 클릭하여 **이벤트 편집** 다시 화면 표시 마우스로 가리키기 **필드** 를 다시 클릭하여 3개의 아이콘을 확인합니다. 을(를) 클릭합니다. **보기** 아이콘.

![ACOP](./images/viewevent.png)

이제 예상 페이로드의 예를 볼 수 있습니다.
이벤트에는 고유한 오케스트레이션 eventID가 있으며, 이 ID는 표시될 때까지 해당 페이로드에서 아래로 스크롤하여 찾을 수 있습니다 `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

이벤트 ID는 다음 연습 중 하나에서 빌드할 여정을 트리거하기 위해 Adobe Experience Platform으로 전송해야 하는 것입니다. 이 eventID는 나중에 필요할 수 있으므로 기억하십시오.
`"eventID": "e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5"`

클릭 **확인**, 그 다음에 를 클릭합니다. **취소**.

이제 이 운동을 끝마쳤습니다.

다음 단계: [3.3 여정 및 푸시 알림 만들기](./ex3.md)

[사용자 흐름 3으로 돌아가기](./uc3.md)

[모든 모듈로 돌아가기](../../overview.md)
