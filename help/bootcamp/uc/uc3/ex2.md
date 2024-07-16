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
source-wordcount: '457'
ht-degree: 0%

---

# 3.2 이벤트 만들기

[Adobe Journey Optimizer](https://experience.adobe.com)(으)로 이동하여 Adobe Experience Cloud에 로그인합니다. **Journey Optimizer**&#x200B;을(를) 클릭합니다.

![AOP](./images/acophome.png)

Journey Optimizer의 **Home** 보기로 리디렉션됩니다. 먼저 올바른 샌드박스를 사용하고 있는지 확인하십시오. 사용할 샌드박스를 `Bootcamp`이라고 합니다. 한 샌드박스에서 다른 샌드박스로 변경하려면 **Prod**&#x200B;를 클릭하고 목록에서 샌드박스를 선택합니다. 이 예제에서는 샌드박스 이름이 **Bootcamp2**&#x200B;입니다. 그러면 샌드박스 `Bootcamp`의 **홈** 보기에 있게 됩니다.

![AOP](./images/acoptriglp.png)

왼쪽 메뉴에서 아래로 스크롤하여 **구성**&#x200B;을 클릭합니다. 그런 다음 **이벤트**&#x200B;에서 **관리** 단추를 클릭합니다.

![AOP](./images/acopmenu.png)

그러면 사용 가능한 모든 이벤트의 개요가 표시됩니다. 나만의 이벤트를 만들려면 **이벤트 만들기**&#x200B;를 클릭하세요.

![AOP](./images/emptyevent.png)

그러면 비어 있는 새 이벤트 창이 나타납니다.

먼저 이벤트에 다음과 같은 이름(`yourLastNameBeaconEntryEvent`)을 지정하고 이 `Beacon Entry Event`과 같은 설명을 추가하십시오.

![AOP](./images/eventdescription.png)

그런 다음 **Type**&#x200B;이(가) **Unitary**(으)로 설정되어 있는지 확인하고, **이벤트 ID 유형** 선택에 대해 **시스템 생성**&#x200B;을 선택하십시오.

![AOP](./images/eventidtype.png)

다음은 스키마 선택 사항입니다. 이 연습을 위해 스키마가 준비되었습니다. 스키마 `Demo System - Event Schema for Mobile App (Global v1.1) v.1`을(를) 사용하십시오.

![AOP](./images/eventschema.png)

스키마를 선택하면 **필드** 섹션에서 여러 필드를 선택할 수 있습니다. 이제 **필드** 섹션 위로 마우스를 가져가면 3개의 아이콘 팝업이 표시됩니다. **편집** 아이콘을 클릭합니다.

![AOP](./images/eventpayload.png)

**필드** 창 팝업이 나타나며, 이 팝업에서 여정을 개인화하는 데 필요한 일부 필드를 선택해야 합니다.  나중에 Adobe Experience Platform에 이미 있는 데이터를 사용하여 다른 프로필 속성을 선택합니다.

![AOP](./images/eventfields.png)

개체 `Place context`이(가) 표시될 때까지 아래로 스크롤하고 확인란을 선택합니다. 이를 통해 고객 위치의 모든 컨텍스트를 여정이 사용할 수 있도록 합니다. 변경 내용을 저장하려면 **확인**&#x200B;을 클릭하세요.

![AOP](./images/eventpayloadbr.png)

그럼 이걸 보셔야죠 변경 내용을 저장하려면 **저장**&#x200B;을 다시 클릭하세요.

![AOP](./images/eventsave.png)

이제 이벤트가 구성 및 저장되었습니다.

![AOP](./images/eventdone.png)

이벤트를 다시 클릭하여 **이벤트 편집** 화면을 다시 엽니다. **필드** 위로 마우스를 다시 가져가면 3개의 아이콘이 표시됩니다. **보기** 아이콘을 클릭합니다.

![AOP](./images/viewevent.png)

이제 예상 페이로드의 예를 볼 수 있습니다.
이벤트에는 고유한 오케스트레이션 eventID가 있으며 `_experience.campaign.orchestration.eventID`이(가) 표시될 때까지 해당 페이로드에서 아래로 스크롤하여 찾을 수 있습니다.

![AOP](./images/payloadeventID.png)

이벤트 ID는 다음 연습 중 하나에서 빌드할 여정을 트리거하기 위해 Adobe Experience Platform에 전송해야 하는 ID입니다. 이 eventID는 나중에 필요할 수 있으므로 기억하십시오.
`"eventID": "e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5"`

**확인**&#x200B;을 클릭한 다음 **취소**&#x200B;을 클릭합니다.

이제 이 연습을 완료했습니다.

다음 단계: [3.3 여정 및 푸시 알림 만들기](./ex3.md)

[사용자 흐름으로 돌아가기 3](./uc3.md)

[모든 모듈로 돌아가기](../../overview.md)
