---
title: Bootcamp - Journey Optimizer 여정 및 이메일 메시지 만들기
description: Bootcamp - Journey Optimizer 여정 및 이메일 메시지 만들기
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: 138a70fa-fe50-4585-b47f-150db4770c3d
source-git-commit: f018e3aae714879de0cccb3a47b1f2242b57abc1
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 4%

---

# 2.3 여정 및 이메일 메시지 만들기

이 연습에서는 다른 사람이 데모 웹 사이트에서 계정을 만들 때 트리거해야 하는 여정을 구성합니다.

다음 위치로 이동하여 Adobe Journey Optimizer에 로그인합니다 [Adobe Experience Cloud](https://experience.adobe.com). 클릭 **Journey Optimizer**.

![ACOP](./images/acophome.png)

으로 리디렉션됩니다. **홈**  Journey Optimizer에서 보기. 먼저 올바른 샌드박스를 사용하고 있는지 확인하십시오. 사용할 샌드박스를 이라고 합니다 `Bootcamp`. 한 샌드박스에서 다른 샌드박스로 변경하려면 **Prod** 및 목록에서 샌드박스를 선택합니다. 이 예제에서 샌드박스의 이름은 다음과 같습니다 **Bootcamp**. 그러면 **홈** 샌드박스 보기 `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 2.3.1 여정 만들기

왼쪽 메뉴에서 **여정**. 다음을 클릭합니다. **여정 만들기** 새 여정을 만들려면

![ACOP](./images/createjourney.png)

그러면 빈 여정 화면이 표시됩니다.

![ACOP](./images/journeyempty.png)

이전 연습에서 새 **이벤트**. 이렇게 이름을 지으셨어요 `yourLastNameAccountCreationEvent` 교체 `yourLastName` 성 이벤트 생성 결과입니다.

![ACOP](./images/eventdone.png)

이제 이 여정의 시작으로 이 이벤트를 가져와야 합니다. 화면 왼쪽으로 이동하고 이벤트 목록에서 이벤트를 검색하여 이 작업을 수행할 수 있습니다.

![ACOP](./images/eventlist.png)

이벤트를 선택하고 여정 캔버스에 끌어다 놓습니다. 이제 여정 모습은 다음과 같습니다.

![ACOP](./images/journeyevent.png)

여정에서 두 번째 단계로 짧게 추가해야 합니다 **대기** 단계. 화면 왼쪽으로 이동하여 **오케스트레이션** 섹션을 참조하십시오. 프로필 속성을 사용하고, 이 속성이 실시간 고객 프로필에 채워졌는지 확인해야 합니다.

![ACOP](./images/journeywait.png)

이제 여정이 다음과 같습니다. 화면 오른쪽에서는 대기 시간을 구성해야 합니다. 1분으로 설정해주세요 이렇게 하면 이벤트가 실행된 후 프로필 속성을 사용할 수 있는 시간이 충분합니다.

![ACOP](./images/journeywait1.png)

클릭 **확인** 변경 사항을 저장하려면 을 클릭합니다.

여정에서 세 번째 단계로 다음을 추가해야 합니다 **이메일** 작업. 화면 왼쪽으로 이동하여 **작업**&#x200B;에서 을(를) 선택합니다. **이메일** 작업을 수행한 다음, 여정의 두 번째 노드에 끌어서 놓습니다. 이제 이게 보입니다.

![ACOP](./images/journeyactions.png)

설정 **카테고리** to **마케팅** 전자 메일을 보낼 수 있는 전자 메일 서피스를 선택합니다. 이 경우 선택할 이메일 표면은 다음과 같습니다 **이메일**. 에 대한 확인란이 **이메일 클릭 수** 및 **이메일 열기** 둘 다 활성화되어 있습니다.

![ACOP](./images/journeyactions1.png)

다음 단계는 메시지를 만드는 것입니다. 이렇게 하려면 **컨텐츠 편집**.

![ACOP](./images/journeyactions2.png)

## 2.3.2 메시지 만들기

메시지를 만들려면 **컨텐츠 편집**.

![ACOP](./images/journeyactions2.png)

이제 이게 보입니다.

![ACOP](./images/journeyactions3.png)

을(를) 클릭합니다. **제목 줄** 텍스트 필드.

![Journey Optimizer](./images/msg5.png)

텍스트 영역에서 쓰기 시작 **안녕**

![Journey Optimizer](./images/msg6.png)

제목란은 아직 끝나지 않았습니다. 다음으로, 필드에 대한 개인화 토큰을 가져와야 합니다 **이름** 다음 위치에 저장됩니다. `profile.person.name.firstName`. 왼쪽 메뉴에서 아래로 스크롤하여 **개인** 요소를 마우스로 가리킨 다음 화살표를 클릭하여 더 깊이 이동합니다.

![Journey Optimizer](./images/msg7.png)

이제 를 찾습니다. **전체 이름** 요소를 마우스로 가리킨 다음 화살표를 클릭하여 더 깊이 이동합니다.

![Journey Optimizer](./images/msg8.png)

마지막으로 **이름** 필드를 클릭하고 **+** 옆에 서명하십시오. 그러면 텍스트 필드에 개인화 토큰이 나타납니다.

![Journey Optimizer](./images/msg9.png)

그런 다음 텍스트를 추가합니다 **감사합니다!** 질문에 답합니다. **저장**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/msg10.png)

그럼 다시 오셔야 합니다 클릭 **이메일 디자이너** 전자 메일의 컨텐츠를 만들려면

![Journey Optimizer](./images/msg11.png)

다음 화면에서는 전자 메일의 컨텐츠를 제공하는 세 가지 다른 방법을 묻는 메시지가 표시됩니다.

- **처음부터 디자인**: 빈 캔버스로 시작하고 WYSIWYG-editor를 사용하여 구조 및 콘텐츠 구성 요소를 드래그하여 놓아 전자 메일의 컨텐츠를 시각적으로 구성합니다.
- **직접 코드 작성**: HTML을 사용하여 코딩하여 자신만의 이메일 템플릿을 만듭니다
- **가져오기 HTML**: 편집할 수 있는 기존 HTML 템플릿을 가져옵니다.

클릭 **가져오기 HTML**. 또는, **저장된 템플릿** 템플릿을 선택하고 **Bootcamp - 이메일 템플릿**.

![Journey Optimizer](./images/msg12.png)

선택한 경우 **가져오기 HTML**&#x200B;로 지정하는 경우 이제 파일을 끌어다 놓을 수 있습니다 **mailtemplatebootcamp.html**&#x200B;다운로드할 수 있는 [여기](../../assets/html/mailtemplatebootcamp.html.zip). 가져오기를 클릭합니다.

![Journey Optimizer](./images/msg13.png)

그러면 이 기본 이메일 템플릿이 표시됩니다.

![Journey Optimizer](./images/msg14.png)

이메일을 개인화하겠습니다. 텍스트 옆에 있는 를 클릭합니다 **안녕** 그런 다음 **개인화 추가** 아이콘.

![Journey Optimizer](./images/msg35.png)

다음으로, **이름** 에 저장된 개인화 토큰 `profile.person.name.firstName`. 메뉴에서 **개인** 요소, 드릴 다운 **전체 이름** 요소를 클릭한 다음 **+** 아이콘 을 클릭하여 표현식 편집기에 이름 필드를 추가합니다.

**저장**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/msg36.png)

이제 개인화 필드가 텍스트에 추가된 방식을 확인할 수 있습니다.

![Journey Optimizer](./images/msg37.png)

클릭 **저장** 메시지를 저장합니다.

![Journey Optimizer](./images/msg55.png)

을(를) 클릭하여 메시지 대시보드로 돌아갑니다 **화살표** 왼쪽 상단 모서리의 제목란 텍스트 옆에 있습니다.

![Journey Optimizer](./images/msg56.png)

이제 등록 전자 메일 만들기를 완료했습니다. 왼쪽 상단 모서리의 화살표를 클릭하여 여정으로 돌아갑니다.

![Journey Optimizer](./images/msg57.png)

클릭 **확인**.

![Journey Optimizer](./images/msg57a.png)

## 2.3.3 여정 게시

여정에 이름을 지정해야 합니다. 다음을 클릭하여 수행할 수 있습니다 **속성** 화면 오른쪽 상단의 아이콘을 클릭합니다.

![ACOP](./images/journeyname.png)

그런 다음 여기에 여정 이름을 입력할 수 있습니다. 사용 `yourLastName - Account Creation Journey`. 클릭 **확인** 변경 사항을 저장하려면 을 클릭합니다.

![ACOP](./images/journeyname1.png)

이제 을(를) 클릭하여 여정을 게시할 수 있습니다 **게시**.

![ACOP](./images/publishjourney.png)

클릭 **게시** 다시 한 번

![ACOP](./images/publish1.png)

이제 여정이 게시되었다는 녹색 확인 표시줄이 표시됩니다.

![ACOP](./images/published.png)

이제 이 운동을 끝마쳤습니다.

다음 단계: [2.4 여정 테스트](./ex4.md)

[사용자 흐름 2로 돌아가기](./uc2.md)

[모든 모듈로 돌아가기](../../overview.md)