---
title: Bootcamp - 물리 및 디지털 혼합 - Journey Optimizer 여정 및 푸시 알림 만들기
description: Bootcamp - 물리 및 디지털 혼합 - Journey Optimizer 여정 및 푸시 알림 만들기
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: be8c23ec-c5f8-4abc-849f-994446072a84
source-git-commit: cd59a41f4533f18a54d80298ee9faf3a8ba3c6e7
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# 3.3 여정 및 푸시 알림 만들기

이 연습에서는 모바일 앱을 사용하여 다른 사람이 비콘에 들어갈 때 트리거해야 하는 여정 및 메시지를 구성합니다.

다음으로 이동하여 Adobe Journey Optimizer에 로그인 [Adobe Experience Cloud](https://experience.adobe.com). 클릭 **Journey Optimizer**.

![ACOP](./images/acophome.png)

다음 페이지로 리디렉션됩니다. **홈**  Journey Optimizer에서 봅니다. 먼저 올바른 샌드박스를 사용하고 있는지 확인하십시오. 사용할 샌드박스는 이라고 합니다. `Bootcamp`. 한 샌드박스에서 다른 샌드박스로 변경하려면 를 클릭합니다. **Prod** 목록에서 샌드박스를 선택합니다. 이 예에서 샌드박스는 다음과 같이 이름이 지정됩니다. **부트캠프**. 그러면 다음 위치에 있게 됩니다. **홈** 샌드박스 보기 `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 여정 만들기

왼쪽 메뉴에서 **여정**. 그런 다음 을 클릭합니다. **여정 만들기** 새 여정 만들기

![ACOP](./images/createjourney.png)

그러면 빈 여정 화면이 표시됩니다.

![ACOP](./images/journeyempty.png)

이전 연습에서는 새 를 만들었습니다 **이벤트**. 이름을 이렇게 지으셨어요 `yourLastNameBeaconEntryEvent` 및 대체됨 `yourLastName` 성을 입력합니다. 이는 이벤트 생성의 결과였습니다.

![ACOP](./images/eventdone.png)

이제 이 이벤트를 이 여정의 시작으로 간주해야 합니다. 이렇게 하려면 화면 왼쪽으로 이동하여 이벤트 목록에서 이벤트를 검색할 수 있습니다.

![ACOP](./images/eventlist.png)

이벤트를 선택하고 여정 캔버스에 끌어서 놓습니다. 이제 여정은 다음과 같습니다. 클릭 **확인** 변경 사항을 저장합니다.

![ACOP](./images/journeyevent.png)

여정의 두 번째 단계로 **푸시** 작업. 화면 왼쪽으로 이동한 다음 **작업**&#x200B;를 선택하고 **푸시** 작업을 수행한 다음 여정의 두 번째 노드로 끌어서 놓습니다.

![ACOP](./images/journeyactions.png)

이제 화면 오른쪽에서 푸시 알림을 만들어야 합니다.

설정 **범주** 끝 **마케팅** 푸시 알림을 전송할 수 있는 푸시 표면을 선택합니다. 이 경우 선택할 푸시 표면은 입니다. **meeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 메시지 만들기

클릭 **콘텐츠 편집**.

![ACOP](./images/emptymsg.png)

그러면 다음과 같은 결과가 표시됩니다.

![ACOP](./images/emailmsglist.png)

푸시 알림의 콘텐츠를 정의하겠습니다.

다음을 클릭합니다. **제목** 텍스트 필드.

![Journey Optimizer](./images/msg5.png)

텍스트 영역에서 작성을 시작합니다. **안녕하세요.**. 개인화 아이콘을 클릭합니다.

![Journey Optimizer](./images/msg6.png)

이제 필드에 대한 개인화 토큰을 가져와야 합니다 **이름** 아래에 저장됨 `profile.person.name.firstName`. 왼쪽 메뉴에서 다음을 선택합니다. **프로필 속성**, 아래로 스크롤/이동하여 **개인** 요소를 선택하고 화살표를 클릭하여 필드에 도달할 때까지 더 깊은 레벨로 이동합니다 `profile.person.name.firstName`. 다음을 클릭합니다. **+** 아이콘을 클릭하여 필드를 캔버스에 추가합니다. **저장**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/msg7.png)

그럼 다시 여기로 오십시오. 필드 옆에 있는 개인화 아이콘을 클릭합니다 **본문**.

![Journey Optimizer](./images/msg11.png)

텍스트 영역에 을 입력합니다. `Welcome at the `.

![Journey Optimizer](./images/msg12.png)

그런 다음 을 클릭합니다. **컨텍스트 속성** 그런 다음 **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

클릭 **이벤트**.

![ACOP](./images/jomsg4.png)

다음과 같이 표시되는 이벤트의 이름을 클릭합니다. **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

클릭 **위치 컨텍스트**.

![ACOP](./images/jomsg6.png)

클릭 **POI 인터랙션**.

![ACOP](./images/jomsg7.png)

클릭 **POI 세부 정보**.

![ACOP](./images/jomsg8.png)

다음을 클릭합니다. **+** 아이콘 **POI 이름**.
그러면 이걸 보게 될 거야. **저장**&#x200B;을 클릭합니다.

![ACOP](./images/jomsg9.png)

이제 메시지가 준비되었습니다. 왼쪽 상단 모서리의 화살표를 클릭하여 여정으로 돌아갑니다.

![ACOP](./images/jomsg11.png)

클릭 **확인**.

![ACOP](./images/jomsg14.png)

## 3.3.2 화면으로 메시지 보내기

여정의 세 번째 단계로 **sendMessageToScreen** 작업. 화면 왼쪽으로 이동한 다음 **작업**&#x200B;를 선택하고 **sendMessageToScreen** 작업을 수행한 다음 여정의 세 번째 노드로 끌어서 놓습니다. 그러면 이걸 보게 될 거야.

![ACOP](./images/jomsg15.png)

다음 **sendMessageToScreen** 작업은 매장 디스플레이에서 사용하는 끝점에 메시지를 게시하는 사용자 지정 작업입니다. 다음 **sendMessageToScreen** 작업에서는 여러 변수가 정의되어야 합니다. 표시될 때까지 아래로 스크롤하여 해당 변수를 볼 수 있습니다 **작업 매개 변수**.

![ACOP](./images/jomsg16.png)

이제 모든 작업 매개 변수에 대한 값을 설정해야 합니다. 이 표를 따라 필요한 위치에 대한 값을 이해합니다.

| 매개변수 | value |
|:-------------:| :---------------:|
| 게재 | `'image'` |
| ECID | `@{yourLastNameBeaconEntryEvent._experienceplatform.identification.core.ecid}` |
| 이름 | `#{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName}` |
| 이벤트 주제 | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first().name}` |
| EVENTSUBJECT | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first()._experienceplatform.core.imageURL}` |
| 샌드박스 | `'bootcamp'` |
| CONTAINERID | `''` |
| 활동 ID | `''` |
| PLACEMENTID | `''` |

{style="table-layout:auto"}

이러한 값을 설정하려면 **편집** 아이콘.

![ACOP](./images/jomsg17.png)

그런 다음 을 선택합니다. **고급 모드**.

![ACOP](./images/jomsg18.png)

그런 다음 위의 표를 기준으로 값을 붙여넣습니다. 클릭 **확인**.

![ACOP](./images/jomsg19.png)

각 필드에 값을 추가하려면 이 프로세스를 반복합니다.

>[!IMPORTANT]
>
>필드 ECID에 이벤트에 대한 참조가 있습니다 `yourLastNameBeaconEntryEvent`. 다음을 교체하십시오. `yourLastName` 성씨로요.

최종 결과는 다음과 같아야 합니다.

![ACOP](./images/jomsg20.png)

위로 스크롤하고 클릭 **확인**.

![ACOP](./images/jomsg21.png)

여정 이름을 계속 지정해야 합니다. 다음을 클릭하면 됩니다. **연필** 아이콘 을 클릭하여 표시할 수 있습니다.

![ACOP](./images/journeyname.png)

그런 다음 여기에 여정 이름을 입력할 수 있습니다. 다음을 사용하십시오. `yourLastName - Beacon Entry Journey`. 클릭 **확인** 변경 사항을 저장합니다.

![ACOP](./images/journeyname1.png)

이제 을(를) 클릭하여 여정을 게시할 수 있습니다. **게시**.

![ACOP](./images/publishjourney.png)

클릭 **게시** 다시.

![ACOP](./images/publish1.png)

그러면 이제 여정이 게시되었다는 녹색 확인 표시줄이 표시됩니다.

![ACOP](./images/published.png)

이제 여정이 라이브되며 트리거될 수 있습니다.

이제 이 연습을 완료했습니다.

다음 단계: [3.4 여정 테스트](./ex4.md)

[사용자 흐름으로 돌아가기 3](./uc3.md)

[모든 모듈로 돌아가기](../../overview.md)
