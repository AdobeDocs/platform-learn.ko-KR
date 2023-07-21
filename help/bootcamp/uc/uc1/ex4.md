---
title: Bootcamp - Real-time CDP - 세그먼트 구축 및 조치 - 세그먼트를 Adobe Target으로 전송
description: Bootcamp - Real-time CDP - 세그먼트 구축 및 조치 - 세그먼트를 Adobe Target으로 전송
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
solution: Experience Platform, Target
feature: Segments, Integrations
exl-id: 6a76c2ab-96b7-4626-a6d3-afd555220b1e
source-git-commit: ee5c0af17c12f1d90774a3a4150c9788e2368e39
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 1%

---

# 1.4 조치 취하기: 세그먼트를 Adobe Target에 보내기

다음으로 이동 [Adobe Experience Platform](https://experience.adobe.com/platform). 로그인하면 Adobe Experience Platform 홈페이지에 접속하게 됩니다.

![데이터 수집](./images/home.png)

계속하기 전에 **샌드박스**. 선택할 샌드박스 이름이 로 지정됩니다. ``Bootcamp``. 텍스트를 클릭하여 이 작업을 수행할 수 있습니다 **[!UICONTROL 프로덕션 프로덕션]** 화면 상단의 파란색 선. 적절한 을(를) 선택한 후 [!UICONTROL 샌드박스], 화면 변경 사항이 표시되며 이제 전용 모드로 전환됩니다. [!UICONTROL 샌드박스].

![데이터 수집](./images/sb1.png)

## 1.4.1 Adobe Target 대상에 대한 세그먼트 활성화

Adobe Target은 Real-Time CDP에서 대상으로 사용할 수 있습니다. Adobe Target 통합을 설정하려면 **대상**, 대상 **카탈로그**.

클릭 **개인화** 다음에서 **카테고리** 메뉴 아래의 제품에서 사용할 수 있습니다. 그러면 다음을 볼 수 있습니다. **Adobe Target** 대상 카드. 클릭 **세그먼트 활성화**.

![위치](./images/atdest1.png)

대상 선택 ``Bootcamp Target`` 및 클릭 **다음**.

![위치](./images/atdest3.png)

사용 가능한 세그먼트 목록에서 만든 세그먼트를 선택합니다 [1.3 세그먼트 만들기](./ex3.md), 이름이 지정됨 `yourLastName - Interest in Real-Time CDP`. 그런 다음 을 클릭합니다. **다음**.

![위치](./images/atdest8.png)

다음 페이지에서 를 클릭합니다. **다음**.

![위치](./images/atdest9.png)

**마침을 클릭합니다**.

![위치](./images/atdest10.png)

이제 세그먼트가 Adobe Target을 향해 활성화됩니다.

![위치](./images/atdest11.png)

>[!IMPORTANT]
>
>Real-Time CDP에서 Adobe Target 대상을 방금 만든 경우 대상이 활성 상태가 되는 데 최대 1시간이 걸릴 수 있습니다. 백엔드 구성 설정으로 인한 일회성 대기 시간입니다. 초기 1시간 대기 시간 및 백엔드 구성이 완료되면 Adobe Target 대상으로 전송되는 새로 추가된 Edge 세그먼트를 실시간으로 타겟팅할 수 있습니다.

## 1.4.2 Adobe Target 양식 기반 활동 구성

이제 Real-Time CDP 세그먼트가 Adobe Target으로 전송되도록 구성되었으므로 Adobe Target에서 경험 타깃팅 활동을 구성할 수 있습니다. 이 연습에서는 시각적 경험 작성기 기반 활동을 구성합니다.

로 이동하여 Adobe Experience Cloud 홈페이지로 이동합니다. [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). 클릭 **Target** 열려고.

![RTCDP](./images/excl.png)

다음에서 **Adobe Target** 홈 페이지, 모든 기존 활동이 표시됩니다.
클릭 **+ 활동 만들기** 새 활동을 만듭니다.

![RTCDP](./images/exclatov.png)

선택 **경험 타기팅**.

![RTCDP](./images/exclatcrxt.png)

선택 **비주얼** 및 설정 **활동 URL** 끝 `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`를 채우기 전에 XX를 01에서 30 사이의 숫자로 바꾸십시오.

>[!IMPORTANT]
>
>활성화의 모든 참가자는 다양한 Adobe Target 경험의 충돌을 방지하기 위해 별도의 웹 페이지를 사용해야 합니다. 웹 페이지를 선택하고 다음 위치로 이동하여 URL을 찾을 수 있습니다. [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>페이지는 모두 동일한 기본 URL을 공유하며 참가자 수로 끝납니다.
>
>예를 들어 참가자 1은 URL을 사용해야 합니다 `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, 참가자 30은 URL을 사용해야 합니다. `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

작업 영역 선택 **부트캠프에서**.

**다음**&#x200B;을 클릭합니다.

![RTCDP](./images/exclatcrxtdtlform.png)

이제 시각적 경험 작성기에 있습니다. 웹 사이트가 완전히 로드될 때까지 20~30초 정도 소요될 수 있습니다.

![RTCDP](./images/atform1.png)

기본 대상은 현재 입니다. **모든 방문자**. 을(를) 클릭합니다 **점 3개** 다음에 **모든 방문자** 및 클릭 **대상 변경**.

![RTCDP](./images/atform3.png)

이제 사용 가능한 대상 목록이 표시되며, 이전에 만들어 Adobe Target에 보낸 Adobe Experience Platform 세그먼트는 이제 이 목록의 일부입니다. 이전에 Adobe Experience Platform에서 만든 세그먼트를 선택합니다. 클릭 **대상자 할당**.

![RTCDP](./images/exclatvecchaud.png)

이제 Adobe Experience Platform 세그먼트는 이 경험 타깃팅 활동의 일부입니다.

![RTCDP](./images/atform4.png)

영웅 이미지를 변경하려면 먼저 **모두 허용** 쿠키 배너에서.

이렇게 하려면 다음으로 이동합니다. **찾아보기**

![RTCDP](./images/cook1.png)

그런 다음 을 클릭합니다. **모두 허용**.

![RTCDP](./images/cook2.png)

다음으로 돌아가기: **작성**.

![RTCDP](./images/cook3.png)

이제 홈페이지 홈페이지의 영웅 이미지를 바꾸겠습니다. 웹 사이트에서 기본 영웅 이미지를 클릭하고 **컨텐츠 바꾸기** 다음을 선택합니다. **이미지**.

![RTCDP](./images/atform5.png)

이미지 파일 검색 **rtcdp.png**. 선택한 다음 을(를) 클릭합니다 **저장**.

![RTCDP](./images/atform6.png)

그러면 선택한 대상에 대한 새 이미지에 새 경험이 표시됩니다.

![RTCDP](./images/atform7.png)

왼쪽 위 모서리에서 활동 제목을 클릭하여 이름을 변경합니다.

![RTCDP](./images/exclatvecname.png)

이름은 다음을 사용하십시오.

- `yourLastName - RTCDP - XT (VEC)`

**다음**&#x200B;을 클릭합니다.

![RTCDP](./images/atform8.png)

**다음**&#x200B;을 클릭합니다.

![RTCDP](./images/atform8a.png)

다음에서 **목표 및 설정** - 페이지, 이동 **목표 지표**.

![RTCDP](./images/atform9.png)

기본 목표 설정 **참여** - **사이트에서 보낸 시간**. **저장 및 닫기**&#x200B;를 클릭합니다.

![RTCDP](./images/vec3.png)

이제 다음 작업을 수행합니다. **활동 개요** 페이지를 가리키도록 업데이트하는 중입니다. 활동을 활성화해야 합니다.

![RTCDP](./images/atform10.png)

필드 클릭 **비활성** 및 선택 **활성화**.

![RTCDP](./images/atform11.png)

그런 다음 활동이 현재 라이브 상태임을 시각적으로 확인할 수 있습니다.

![RTCDP](./images/atform12.png)

이제 활동이 라이브 상태이며 부트캠프 웹 사이트에서 테스트할 수 있습니다.

이제 데모 웹 사이트로 돌아가 의 제품 페이지를 방문하십시오. **Real-Time CDP**&#x200B;만든 세그먼트를 바로 사용할 수 있으며, 그러면 홈 페이지에 실시간으로 Adobe Target 활동이 표시되는 것을 볼 수 있습니다.

>[!IMPORTANT]
>
>활성화의 모든 참가자는 다양한 Adobe Target 경험의 충돌을 방지하기 위해 별도의 웹 페이지를 사용해야 합니다. 웹 페이지를 선택하고 다음 위치로 이동하여 URL을 찾을 수 있습니다. [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>페이지는 모두 동일한 기본 URL을 공유하며 참가자 수로 끝납니다.
>
>예를 들어 참가자 1은 URL을 사용해야 합니다 `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, 참가자 30은 URL을 사용해야 합니다. `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

다음 단계: [1.5 조치 취하기: 세그먼트를 Facebook에 보내기](./ex5.md)

[사용자 흐름 1로 돌아가기](./uc1.md)

[모든 모듈로 돌아가기](../../overview.md)
