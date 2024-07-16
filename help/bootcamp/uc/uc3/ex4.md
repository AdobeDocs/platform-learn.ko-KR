---
title: Bootcamp - 물리적 및 디지털 혼합 - 여정 테스트
description: Bootcamp - 물리적 및 디지털 혼합 - 여정 테스트
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 45c77177-9ea9-4c3d-a40e-c04a747938eb
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# 3.4 여정 테스트

여정을 테스트하려면 연습 3.2에서 만든 이벤트의 이벤트 ID를 사용해야 합니다. 이 ID는 다음과 같습니다.

![AOP](./images/payloadeventID.png)

여정 ID는 이벤트를 트리거하기 위해 Adobe Experience Platform에 전송해야 하는 ID입니다. 이 예제에서 eventID는 다음과 같습니다.
`e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5`.

모바일 앱을 열고 홈페이지로 이동합니다. **설정** 아이콘을 클릭합니다.

![DSN](./images/appsett.png)

**Beacon EventID** 필드에 eventID를 붙여 넣고 **저장**&#x200B;을 클릭합니다.

![DSN](./images/beacon1.png)

계속하기 전에 컴퓨터에서 이 웹 페이지를 여십시오. [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

그러면 다음과 같은 결과가 표시됩니다.

![DSN](./images/screen1.png)

다음으로 홈 페이지로 돌아갑니다. **beacon** 아이콘을 클릭합니다.

![DSN](./images/app23.png)

그러면 이걸 보게 될 거야. 먼저 **Bootcamp 화면 비콘**&#x200B;을 선택한 다음 **시작** 단추를 클릭합니다. 이렇게 하면 비콘 항목을 시뮬레이션할 수 있습니다.

![DSN](./images/app21.png)

이제 매장 화면을 살펴보세요. 5초 이내에 마지막으로 본 제품이 표시됩니다.

![DSN](./images/beacon3.png)

푸시 알림도 수신하게 됩니다.

![DSN](./images/beacon2.png)

이제 이 연습을 완료했습니다.

[사용자 흐름으로 돌아가기 3](./uc3.md)

[모든 모듈로 돌아가기](../../overview.md)
