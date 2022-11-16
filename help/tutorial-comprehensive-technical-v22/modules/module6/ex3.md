---
title: 실시간 CDP - 세그먼트 구축 및 작업 수행 - 세그먼트를 DV360으로 보내기
description: 실시간 CDP - 세그먼트 구축 및 작업 수행 - 세그먼트를 DV360으로 보내기
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7a78260f-cd25-4ed0-801b-87174babaffe
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 2%

---

# 6.3 조치 수행: 세그먼트를 DV360으로 보내기

이동 [Adobe Experience Platform](https://experience.adobe.com/platform). 로그인하면 Adobe Experience Platform 홈 페이지가 표시됩니다.

![데이터 수집](../module2/images/home.png)

계속하기 전에 **샌드박스**. 선택할 샌드박스의 이름은 다음과 같습니다 ``--aepSandboxId--``. 이 작업은 텍스트를 클릭하여 수행할 수 있습니다 **[!UICONTROL 프로덕션 제품]** 화면 상단에 있는 파란색 줄에 표시됩니다. 적절한 [!UICONTROL 샌드박스]이렇게 하면 화면 변경 사항이 표시되고 이제 전용 화면에 표시됩니다 [!UICONTROL 샌드박스].

![데이터 수집](../module2/images/sb1.png)

왼쪽 메뉴에서 **대상**, 그런 다음 **카탈로그**. 그러면 **대상 카탈로그**.

![RTCDP](./images/rtcdpmenudest.png)

in **대상**&#x200B;를 클릭하고 **세그먼트 활성화** on **Google 디스플레이 및 비디오 360** 카드.

![RTCDP](./images/rtcdpgoogleseg.png)

대상을 선택하고 을(를) 클릭합니다 **다음**.

![RTCDP](./images/rtcdpcreatedest2.png)

사용 가능한 세그먼트 목록에서 이전 연습에서 만든 세그먼트를 선택합니다. **다음**&#x200B;을 클릭합니다.

![RTCDP](./images/rtcdpcreatedest3.png)

설정 **세그먼트 예약** 페이지를 클릭한 다음 **다음**.

![RTCDP](./images/rtcdpcreatedest4.png)

마지막으로, **검토** 페이지를 클릭한 다음 **완료**.

![RTCDP](./images/rtcdpcreatedest5.png)

이제 세그먼트가 Google DV360에 연결됩니다. 고객이 이 세그먼트를 사용할 수 있을 때마다 Google DV360의 Audience에 해당 고객을 포함하도록 신호가 Google DV360으로 전송됩니다.

다음 단계: [6.4 조치 수행: S3 대상에 세그먼트 보내기](./ex4.md)

[모듈 6으로 돌아가기](./real-time-cdp-build-a-segment-take-action.md)

[모든 모듈로 돌아가기](../../overview.md)
