---
title: 푸시 메시지로 여정 구성
description: 푸시 메시지로 여정 구성
kt: 5342
doc-type: tutorial
source-git-commit: 203590e3289d2e5342085bf8b6b4e3cd11859539
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 1%

---

# 3.3.2 푸시 메시지로 여정 구성


## 3.4.4.6 새 이벤트 만들기

**Journey Optimizer**(으)로 이동합니다. 왼쪽 메뉴에서 **구성**(으)로 이동한 다음 **이벤트**&#x200B;에서 **관리**&#x200B;를 클릭합니다.

![AOP](./images/acopmenu.png)

**이벤트** 화면에 다음과 유사한 보기가 표시됩니다. **이벤트 만들기**&#x200B;를 클릭합니다.

![AOP](./images/add.png)

그러면 빈 이벤트 구성이 표시됩니다.
먼저 이벤트에 다음과 같은 이름(`--aepUserLdap--StoreEntryEvent`)을 지정하고 설명을 `Store Entry Event`(으)로 설정하십시오.
다음은 **이벤트 유형** 선택입니다. **단일**&#x200B;을(를) 선택합니다.
다음은 **이벤트 ID 유형** 선택 항목입니다. **시스템 생성**&#x200B;을 선택하십시오.

![AOP](./images/eventname.png)

다음은 스키마 선택 사항입니다. 이 연습을 위해 스키마가 준비되었습니다. 스키마 `Demo System - Event Schema for Mobile App (Global v1.1) v.1`을(를) 사용하십시오.

스키마를 선택하면 **페이로드** 섹션에서 여러 필드를 선택할 수 있습니다. 이제 이벤트가 완전히 구성되었습니다.

**저장**&#x200B;을 클릭합니다.

![AOP](./images/eventschema.png)

이제 이벤트가 구성 및 저장되었습니다. 이벤트를 다시 클릭하여 **이벤트 편집** 화면을 다시 엽니다.

![AOP](./images/eventdone.png)

**페이로드** 필드 위로 마우스를 가져간 후 **페이로드 보기** 아이콘을 클릭합니다.

![AOP](./images/hover.png)

이제 예상 페이로드의 예를 볼 수 있습니다.

이벤트에는 고유한 오케스트레이션 eventID가 있으며 `_experience.campaign.orchestration.eventID`이(가) 표시될 때까지 해당 페이로드에서 아래로 스크롤하여 찾을 수 있습니다.

![AOP](./images/payloadeventID.png)

이벤트 ID는 다음 단계에서 빌드할 여정을 트리거하기 위해 Adobe Experience Platform에 전송해야 하는 ID입니다. 다음 단계에서 필요하므로 이 eventID를 기록하십시오.
`"eventID": "89acd341ec2b7d1130c9a73535029debf2ac35f486bc99236b1a5091d6f4bc68"`

**확인**, **취소**&#x200B;를 차례로 클릭합니다.

## 3.4.4.7 여정 만들기

메뉴에서 **여정**(으)로 이동하여 **여정 만들기**&#x200B;를 클릭합니다.

![DSN](./images/sjourney1.png)

그러면 이걸 보게 될 거야. 여정 이름을 지정합니다. `--aepUserLdap-- - Store Entry journey` 사용. **저장**&#x200B;을 클릭합니다.

![DSN](./images/sjourney3.png)

먼저 이벤트를 여정 시작점으로 추가해야 합니다. `--aepUserLdap--StoreEntryEvent` 이벤트를 검색하여 캔버스에 끌어서 놓습니다. **저장**&#x200B;을 클릭합니다.

![DSN](./images/sjourney4.png)

그런 다음 **Actions**&#x200B;에서 **Push** 작업을 검색합니다. **Push** 작업을 캔버스로 끌어서 놓습니다.

**카테고리**&#x200B;을(를) **마케팅**(으)로 설정하고 푸시 알림을 보낼 수 있는 푸시 표면을 선택하십시오. 이 경우 선택할 전자 메일 표면은 **Push-iOS-Android**&#x200B;입니다.

>[!NOTE]
>
>이전에 검토한 대로 **앱 표면**&#x200B;을(를) 사용하는 Journey Optimizer 채널이 있어야 합니다.

![AOP](./images/journeyactions1push.png)

다음 단계는 메시지를 만드는 것입니다. 이렇게 하려면 **콘텐츠 편집**&#x200B;을 클릭하세요.

![AOP](./images/journeyactions2push.png)

그러면 이걸 보게 될 거야. **제목** 필드에 대한 **개인화** 아이콘을 클릭합니다.

![푸시](./images/bp5.png)

그러면 이걸 보게 될 거야. 이제 실시간 고객 프로필에서 프로필 속성을 직접 선택할 수 있습니다.

**이름** 필드를 검색한 다음 **이름** 필드 옆에 있는 **+** 아이콘을 클릭합니다. 그러면 이름 **{{profile.person.name.firstName}}**&#x200B;에 대한 개인화 토큰이 추가됩니다.

![푸시](./images/bp9.png)

**텍스트를 추가합니다. 스토어에 오신 것을 환영합니다!** 뒤에 **{{profile.person.name.firstName}}**&#x200B;이(가) 있습니다.

**저장**&#x200B;을 클릭합니다.

![푸시](./images/bp10.png)

이제 이걸 가지셨네요. **본문** 필드에 대한 **개인화** 아이콘을 클릭합니다.

![푸시](./images/bp11.png)

이 텍스트를 입력하십시오. **오늘 구입하면 10% 할인을 받으려면 여기를 클릭하세요!**&#x200B;을(를) 클릭하고 **저장**&#x200B;을(를) 클릭합니다.

![푸시](./images/bp12.png)

그럼 이걸로 드셔보세요 왼쪽 상단 모서리의 화살표를 클릭하여 여정으로 돌아갑니다.

![Journey Optimizer](./images/bp12a.png)

푸시 작업을 닫으려면 **저장**&#x200B;을 클릭하세요.

![DSN](./images/sjourney8.png)

**게시**&#x200B;를 클릭합니다.

![DSN](./images/sjourney10.png)

**게시**&#x200B;를 다시 클릭합니다.

![DSN](./images/sjourney10a.png)

이제 여정이 게시되었습니다.

![DSN](./images/sjourney11.png)

## 3.4.4.8 여정 및 푸시 메시지 테스트

DX 데모 2.0 모바일 응용 프로그램에서 **설정** 화면으로 이동합니다. **항목 저장** 단추를 클릭합니다.

>[!NOTE]
>
>**스토어 항목** 단추가 현재 구현되고 있습니다. 앱에서 아직 찾을 수 없습니다.

![DSN](./images/demo1b.png)

**스토어 시작** 아이콘을 클릭한 후 바로 앱을 닫아야 합니다. 그렇지 않으면 푸시 메시지가 표시되지 않습니다.

몇 초 후에 메시지가 나타납니다.

![DSN](./images/demo2.png)

이 연습을 완료했습니다.

## 다음 단계

[3.3.3으로 이동 인앱 메시지로 캠페인 구성](./ex3.md){target="_blank"}

[Adobe Journey Optimizer: 푸시 및 인앱 메시지](ajopushinapp.md){target="_blank"}(으)로 돌아가기

[모든 모듈](./../../../../overview.md){target="_blank"}(으)로 돌아가기
