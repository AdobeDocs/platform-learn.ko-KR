---
title: Bootcamp - Journey Optimizer 여정 만들기
description: Bootcamp - Journey Optimizer 여정 만들기
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: e4464502-60c8-4fba-a429-169b7a4516c8
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 2%

---

# 2.4 여정 테스트

## 고객 여정 흐름

새롭고 깔끔한 시크릿 브라우저 창을 열고 다음으로 이동 [https://bootcamp.aepdemo.net](https://bootcamp.aepdemo.net). 클릭 **모두 허용**. 이전 사용자 흐름의 탐색 동작을 기반으로 웹 사이트의 홈페이지에서 개인화가 발생하는 것을 볼 수 있습니다.

![DSN](./images/web8a.png)

다음을 클릭합니다. **프로필** 아이콘 을 클릭하여 표시할 수 있습니다.

![데모](./images/web8b.png)

클릭 **계정 만들기**.

![데모](./images/pv5.png)

양식의 모든 필드를 채웁니다. 이메일 및 SMS 게재를 위한 이후 연습에서 사용되므로 이메일 주소 및 전화번호 값은 실제 값을 사용합니다.

![데모](./images/pv7a.png)

아래로 스크롤합니다. 이제 연습 2.2에서 만든 사용자 지정 이벤트의 eventID를 입력해야 합니다. 여기에서 찾을 수 있습니다.

![ACOP](./images/payloadeventID.png)

여정 ID는 빌드한 이벤트를 트리거하기 위해 Adobe Experience Platform으로 전송해야 하는 ID입니다. 이 예제의 eventID는 다음과 같습니다. `19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f`

필드에 eventID 입력 **계정 생성 이벤트 ID** 및 클릭 **등록**.

![데모](./images/pv8a.png)

그러면 이걸 보게 될 거야.

![데모](./images/pv9.png)

또한 이 연습의 일부로 직접 만든 이메일인 이 이메일을 받게 됩니다.

![데모](./images/pv10a.png)

이제 이 연습을 완료했습니다.

다음 단계: [2.5 모바일 앱 설치 및 사용](./ex5.md)

[사용자 흐름 2로 돌아가기](./uc2.md)

[모든 모듈로 돌아가기](../../overview.md)
