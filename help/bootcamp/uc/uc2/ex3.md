---
title: Bootcamp - Journey Optimizer 여정 및 이메일 메시지 만들기
description: Bootcamp - Journey Optimizer 여정 및 이메일 메시지 만들기
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Journeys
exl-id: 138a70fa-fe50-4585-b47f-150db4770c3d
source-git-commit: cd59a41f4533f18a54d80298ee9faf3a8ba3c6e7
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# 2.3 여정 및 이메일 메시지 만들기

이 연습에서는 누군가 데모 웹 사이트에서 여정을 만들 때 트리거해야 하는 계정을 구성합니다.

[Adobe Journey Optimizer](https://experience.adobe.com)(으)로 이동하여 Adobe Experience Cloud에 로그인합니다. **Journey Optimizer**&#x200B;을(를) 클릭합니다.

![AOP](./images/acophome.png)

Journey Optimizer의 **Home** 보기로 리디렉션됩니다. 먼저 올바른 샌드박스를 사용하고 있는지 확인하십시오. 사용할 샌드박스를 `Bootcamp`이라고 합니다. 한 샌드박스에서 다른 샌드박스로 변경하려면 **Prod**&#x200B;를 클릭하고 목록에서 샌드박스를 선택합니다. 이 예제에서는 샌드박스 이름이 **Bootcamp**&#x200B;입니다. 그러면 샌드박스 `Bootcamp`의 **홈** 보기에 있게 됩니다.

![AOP](./images/acoptriglp.png)

## 2.3.1 여정 만들기

왼쪽 메뉴에서 **여정**&#x200B;을 클릭합니다. 그런 다음 **여정 만들기**&#x200B;를 클릭하여 새 여정을 만듭니다.

![AOP](./images/createjourney.png)

그러면 빈 여정 화면이 표시됩니다.

![AOP](./images/journeyempty.png)

이전 연습에서는 새 **이벤트**&#x200B;를 만들었습니다. 이 `yourLastNameAccountCreationEvent`과(와) 같이 이름을 지정하고 `yourLastName`을(를) 성으로 바꾸었습니다. 이는 이벤트 생성의 결과였습니다.

![AOP](./images/eventdone.png)

이제 이 이벤트를 이 여정의 시작으로 간주해야 합니다. 이렇게 하려면 화면 왼쪽으로 이동하여 이벤트 목록에서 이벤트를 검색할 수 있습니다.

![AOP](./images/eventlist.png)

이벤트를 선택하고 여정 캔버스에 끌어서 놓습니다. 이제 여정은 다음과 같습니다.

![AOP](./images/journeyevent.png)

여정의 두 번째 단계로 **대기** 단계를 짧게 추가해야 합니다. 화면의 왼쪽으로 이동하여 **오케스트레이션** 섹션을 찾습니다. 프로필 속성을 사용하게 되며 이러한 속성이 실시간 고객 프로필에 채워져 있는지 확인해야 합니다.

![AOP](./images/journeywait.png)

이제 여정은 다음과 같습니다. 화면 오른쪽에서 대기 시간을 구성해야 합니다. 1분으로 설정합니다. 이렇게 하면 이벤트가 실행된 후에 프로필 속성을 사용할 수 있는 충분한 시간이 제공됩니다.

![AOP](./images/journeywait1.png)

변경 내용을 저장하려면 **확인**&#x200B;을 클릭하세요.

여정의 세 번째 단계로 **전자 메일** 작업을 추가해야 합니다. 화면의 왼쪽으로 이동하여 **작업**&#x200B;을(를) 선택하고 **전자 메일** 작업을 선택한 다음 여정의 두 번째 노드에 끌어서 놓습니다. 이제 이 항목을 볼 수 있습니다.

![AOP](./images/journeyactions.png)

**카테고리**&#x200B;을(를) **마케팅**(으)로 설정하고 전자 메일을 보낼 수 있는 전자 메일 표면을 선택합니다. 이 경우 선택할 전자 메일 표면은 **전자 메일**&#x200B;입니다. **이메일 클릭 수** 및 **이메일 열기**&#x200B;에 대한 확인란이 모두 활성화되어 있는지 확인하십시오.

![AOP](./images/journeyactions1.png)

다음 단계는 메시지를 만드는 것입니다. 이렇게 하려면 **콘텐츠 편집**&#x200B;을 클릭하세요.

![AOP](./images/journeyactions2.png)

## 2.3.2 메시지 만들기

메시지를 만들려면 **콘텐츠 편집**&#x200B;을 클릭하세요.

![AOP](./images/journeyactions2.png)

이제 이 항목을 볼 수 있습니다.

![AOP](./images/journeyactions3.png)

**제목 줄** 텍스트 필드를 클릭합니다.

![Journey Optimizer](./images/msg5.png)

텍스트 영역에서 **안녕하세요** 쓰기를 시작합니다.

![Journey Optimizer](./images/msg6.png)

제목란은 아직 완성되지 않았습니다. 다음으로 `profile.person.name.firstName` 아래에 저장된 필드 **이름**&#x200B;에 대한 개인화 토큰을 가져와야 합니다. 왼쪽 메뉴에서 아래로 스크롤하여 **Person** 요소를 찾은 다음 화살표를 클릭하여 더 깊은 레벨로 이동합니다.

![Journey Optimizer](./images/msg7.png)

이제 **전체 이름** 요소를 찾아 화살표를 클릭하면 더 깊은 레벨로 이동합니다.

![Journey Optimizer](./images/msg8.png)

마지막으로 **이름** 필드를 찾은 다음 옆에 있는 **+** 기호를 클릭합니다. 그러면 개인화 토큰이 텍스트 필드에 표시되는 것을 볼 수 있습니다.

![Journey Optimizer](./images/msg9.png)

다음으로 **텍스트를 추가하십시오. 등록해 주셔서 감사합니다!** 질문에 답합니다. **저장**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/msg10.png)

그럼 다시 여기로 오십시오. 전자 메일 콘텐츠를 만들려면 **전자 메일 Designer**&#x200B;을(를) 클릭합니다.

![Journey Optimizer](./images/msg11.png)

다음 화면에서는 전자 메일 콘텐츠를 제공하는 3가지 방법이 표시됩니다.

- **처음부터 디자인**: 빈 캔버스로 시작하고 WYSIWYG 편집기를 사용하여 구조 및 콘텐츠 구성 요소를 끌어서 놓아 전자 메일의 콘텐츠를 시각적으로 빌드합니다.
- **직접 코딩하기**: HTML을 사용하여 코딩하여 전자 메일 템플릿을 만드십시오.
- **HTML 가져오기**: 편집할 수 있는 기존 HTML 템플릿을 가져옵니다.

**HTML 가져오기**&#x200B;를 클릭합니다. 또는 **저장된 템플릿**&#x200B;을 클릭하고 템플릿 **Bootcamp - 전자 메일 템플릿**&#x200B;을 선택할 수 있습니다.

![Journey Optimizer](./images/msg12.png)

**HTML 가져오기**&#x200B;를 선택한 경우 이제 **mailtemplatebootcamp.html** 파일을 끌어서 놓을 수 있습니다. [여기](../../assets/html/mailtemplatebootcamp.html.zip)에서 다운로드할 수 있습니다. 가져오기를 클릭합니다.

![Journey Optimizer](./images/msg13.png)

그러면 이 기본 이메일 템플릿이 표시됩니다.

![Journey Optimizer](./images/msg14.png)

이메일을 개인화하겠습니다. **안녕하세요** 텍스트 옆에 있는 아이콘을 클릭한 다음 **Personalization 추가** 아이콘을 클릭합니다.

![Journey Optimizer](./images/msg35.png)

`profile.person.name.firstName`에 저장된 **이름** 개인화 토큰을 가져와야 합니다. 메뉴에서 **Person** 요소를 찾아 **전체 이름** 요소로 드릴다운한 다음 **+** 아이콘을 클릭하여 이름 필드를 식 편집기에 추가합니다.

**저장**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/msg36.png)

이제 개인화 필드가 텍스트에 추가된 방식을 알 수 있습니다.

![Journey Optimizer](./images/msg37.png)

메시지를 저장하려면 **저장**&#x200B;을 클릭하세요.

![Journey Optimizer](./images/msg55.png)

왼쪽 상단 모서리의 제목 줄 텍스트 옆에 있는 **화살표**&#x200B;를 클릭하여 메시지 대시보드로 돌아갑니다.

![Journey Optimizer](./images/msg56.png)

이제 등록 이메일 작성을 완료했습니다. 왼쪽 상단 모서리의 화살표를 클릭하여 여정으로 돌아갑니다.

![Journey Optimizer](./images/msg57.png)

**확인**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/msg57a.png)

## 2.3.3 Publish 사용자 여정

여정 이름을 계속 지정해야 합니다. 화면 왼쪽 상단의 **연필** 아이콘을 클릭하면 됩니다.

![AOP](./images/journeyname.png)

그런 다음 여기에 여정 이름을 입력할 수 있습니다. `yourLastName - Account Creation Journey`을(를) 사용하십시오. 변경 내용을 저장하려면 **확인**&#x200B;을 클릭하세요.

![AOP](./images/journeyname1.png)

이제 **Publish**&#x200B;을(를) 클릭하여 여정을 게시할 수 있습니다.

![AOP](./images/publishjourney.png)

**Publish**&#x200B;을 다시 클릭합니다.

![AOP](./images/publish1.png)

그러면 이제 여정이 게시되었다는 녹색 확인 표시줄이 표시됩니다.

![AOP](./images/published.png)

이제 이 연습을 완료했습니다.

다음 단계: [2.4 여정 테스트](./ex4.md)

[사용자 흐름 2로 돌아가기](./uc2.md)

[모든 모듈로 돌아가기](../../overview.md)