---
title: Bootcamp - 물리적 및 디지털 혼합 - Journey Optimizer 여정 및 푸시 만들기 - 브라일로 알림
description: Bootcamp - 물리적 및 디지털 혼합 - Journey Optimizer 여정 및 푸시 만들기 - 브라일로 알림
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 2%

---

# 3.3 여정 및 푸시 알림 만들기

이 연습에서는 다른 사람이 모바일 앱을 사용하여 비콘을 입력할 때 트리거해야 하는 여정 및 메시지를 구성합니다.

다음 위치로 이동하여 Adobe Journey Optimizer에 로그인합니다 [Adobe Experience Cloud](https://experience.adobe.com). 클릭 **Journey Optimizer**.

![ACOP](./images/acophome.png)

으로 리디렉션됩니다. **홈**  Journey Optimizer에서 보기. 먼저 올바른 샌드박스를 사용하고 있는지 확인하십시오. 사용할 샌드박스를 이라고 합니다 `Bootcamp`. 한 샌드박스에서 다른 샌드박스로 변경하려면 **Prod** 및 목록에서 샌드박스를 선택합니다. 이 예제에서 샌드박스의 이름은 다음과 같습니다 **Bootcamp**. 그러면 **홈** 샌드박스 보기 `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 여정 만들기

왼쪽 메뉴에서 **여정**. 다음을 클릭합니다. **여정 만들기** 새 여정을 만들려면

![ACOP](./images/createjourney.png)

그러면 빈 여정 화면이 표시됩니다.

![ACOP](./images/journeyempty.png)

이전 연습에서 새 **이벤트**. 이렇게 이름을 지으셨어요 `yourLastNameBeaconEntryEvent` 교체 `yourLastName` 성 이벤트 생성 결과입니다.

![ACOP](./images/eventdone.png)

이제 이 여정의 시작으로 이 이벤트를 가져와야 합니다. 화면 왼쪽으로 이동하고 이벤트 목록에서 이벤트를 검색하여 이 작업을 수행할 수 있습니다.

![ACOP](./images/eventlist.png)

이벤트를 선택하고 여정 캔버스에 끌어다 놓습니다. 이제 여정이 다음과 같습니다. 클릭 **확인** 변경 사항을 저장하려면 을 클릭합니다.

![ACOP](./images/journeyevent.png)

여정에서 두 번째 단계로 다음을 추가해야 합니다 **푸시** 작업. 화면 왼쪽으로 이동하여 **작업**&#x200B;에서 을(를) 선택합니다. **푸시** 작업을 수행한 다음, 여정의 두 번째 노드에 끌어서 놓습니다.

![ACOP](./images/journeyactions.png)

화면 오른쪽에서 푸시 알림을 만들어야 합니다.

설정 **카테고리** to **마케팅** 푸시 알림을 전송할 수 있는 푸시 면을 선택합니다. 이 경우 선택할 푸시 서피스는 다음과 같습니다 **miewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 메시지 만들기

클릭 **컨텐츠 편집**.

![ACOP](./images/emptymsg.png)

그러면 다음 내용이 표시됩니다.

![ACOP](./images/emailmsglist.png)

푸시 알림의 내용을 정의하겠습니다.

을(를) 클릭합니다. **제목** 텍스트 필드.

![Journey Optimizer](./images/msg5.png)

텍스트 영역에서 쓰기 시작 **안녕**. 개인화 아이콘을 클릭합니다.

![Journey Optimizer](./images/msg6.png)

이제 필드에 대한 개인화 토큰을 가져와야 합니다 **이름** 다음 위치에 저장됩니다. `profile.person.name.firstName`. 왼쪽 메뉴에서 **프로필 속성**&#x200B;를 차례로 클릭하거나 아래로 스크롤하여 **개인** 요소를 마우스로 가리킨 다음 화살표를 클릭하여 필드에 도달할 때까지 더 깊이 이동합니다 `profile.person.name.firstName`. 을(를) 클릭합니다. **+** 아이콘을 클릭하여 필드를 캔버스에 추가합니다. **저장**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/msg7.png)

그럼 다시 오셔야 합니다 필드 옆에 있는 개인화 아이콘을 클릭합니다 **본문**.

![Journey Optimizer](./images/msg11.png)

텍스트 영역에서 `Welcome at the `.

![Journey Optimizer](./images/msg12.png)

다음을 클릭합니다. **상황별 속성** 그리고 **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

클릭 **이벤트**.

![ACOP](./images/jomsg4.png)

다음과 같이 표시되는 이벤트 이름을 클릭합니다. **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

클릭 **컨텍스트 배치**.

![ACOP](./images/jomsg6.png)

클릭 **POI 상호 작용**.

![ACOP](./images/jomsg7.png)

클릭 **POI 세부 사항**.

![ACOP](./images/jomsg8.png)

을(를) 클릭합니다. **+** 아이콘 켜짐 **POI 이름**.
그러면 이게 보입니다. **저장**&#x200B;을 클릭합니다.

![ACOP](./images/jomsg9.png)

이제 메시지를 사용할 수 있습니다. 왼쪽 상단 모서리의 화살표를 클릭하여 여정으로 돌아갑니다.

![ACOP](./images/jomsg11.png)

클릭 **확인**.

![ACOP](./images/jomsg14.png)

## 3.3.2 화면으로 메시지 보내기

여정에서 세 번째 단계로 다음을 추가해야 합니다 **sendMessageToScreen** 작업. 화면 왼쪽으로 이동하여 **작업**&#x200B;에서 을(를) 선택합니다. **sendMessageToScreen** 작업을 수행한 다음, 여정의 세 번째 노드에 끌어서 놓습니다. 그러면 이게 보입니다.

![ACOP](./images/jomsg15.png)

다음 **sendMessageToScreen** 작업은 저장 내 디스플레이에서 사용하는 엔드포인트에 메시지를 게시하는 사용자 지정 작업입니다. 다음 **sendMessageToScreen** 작업을 위해서는 많은 변수를 정의해야 합니다. 이 변수들을 보려면 아래로 스크롤하여 **작업 매개 변수**.

![ACOP](./images/jomsg16.png)

이제 모든 작업 매개 변수에 대한 값을 설정해야 합니다. 이 표를 따라 필요한 값을 파악합니다.

| 매개 변수 | 값 |
|:-------------:| :---------------:|
| 배달 | `'image'` |
| ECID | `@{yourLastNameBeaconEntryEvent._experienceplatform.identification.core.ecid}` |
| 이름 | `#{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName}` |
| EVENTSUBJECT | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first().name}` |
| EVENTSUBJECTURL | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first()._experienceplatform.core.imageURL}` |
| 샌드박스 | `'bootcamp'` |
| CONTAINERID | `''` |
| ACTIVITYID | `''` |
| PLACEMENTID | `''` |

{style=&quot;table-layout:auto&quot;}

이러한 값을 설정하려면 **편집** 아이콘.

![ACOP](./images/jomsg17.png)

다음 을 선택합니다. **고급 모드**.

![ACOP](./images/jomsg18.png)

그런 다음 위의 표를 기준으로 값을 붙여넣습니다. 클릭 **확인**.

![ACOP](./images/jomsg19.png)

이 프로세스를 반복하여 각 필드에 값을 추가합니다.

>[!IMPORTANT]
>
>ECID 필드에 이벤트에 대한 참조가 있습니다 `yourLastNameBeaconEntryEvent`. 바꾸십시오 `yourLastName` 성.

최종 결과는 다음과 같습니다.

![ACOP](./images/jomsg20.png)

위로 스크롤하여 클릭 **확인**.

![ACOP](./images/jomsg21.png)

여정에 이름을 지정해야 합니다. 다음을 클릭하여 수행할 수 있습니다 **속성** 화면 오른쪽 상단의 아이콘을 클릭합니다.

![ACOP](./images/journeyname.png)

그런 다음 여기에 여정 이름을 입력할 수 있습니다. 사용 `yourLastName - Beacon Entry Journey`. 클릭 **확인** 변경 사항을 저장하려면 을 클릭합니다.

![ACOP](./images/journeyname1.png)

이제 을(를) 클릭하여 여정을 게시할 수 있습니다 **게시**.

![ACOP](./images/publishjourney.png)

클릭 **게시** 다시 한 번

![ACOP](./images/publish1.png)

이제 여정이 게시되었다는 녹색 확인 표시줄이 표시됩니다.

![ACOP](./images/published.png)

이제 여정이 라이브로 트리거될 수 있습니다.

이제 이 운동을 끝마쳤습니다.

다음 단계: [3.4 여정 테스트](./ex4.md)

[사용자 흐름 3으로 돌아가기](./uc3.md)

[모든 모듈로 돌아가기](../../overview.md)
