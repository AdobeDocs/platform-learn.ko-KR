---
title: Bootcamp - 실시간 CDP - 세그먼트 구축 및 조치 수행 - Adobe Target에 세그먼트 보내기 - 브라질
description: Bootcamp - 실시간 CDP - 세그먼트 구축 및 조치 수행 - Adobe Target에 세그먼트 보내기 - 브라질
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 1%

---

# 1.4 조치 수행: Adobe Target에 세그먼트 보내기

이동 [Adobe Experience Platform](https://experience.adobe.com/platform). 로그인하면 Adobe Experience Platform 홈 페이지가 표시됩니다.

![데이터 수집](./images/home.png)

계속하기 전에 **샌드박스**. 선택할 샌드박스의 이름은 다음과 같습니다 ``Bootcamp``. 이 작업은 텍스트를 클릭하여 수행할 수 있습니다 **[!UICONTROL 프로덕션 제품]** 화면 상단에 있는 파란색 줄에 표시됩니다. 적절한 [!UICONTROL 샌드박스]이렇게 하면 화면 변경 사항이 표시되고 이제 전용 화면에 표시됩니다 [!UICONTROL 샌드박스].

![데이터 수집](./images/sb1.png)

## 1.4.1 Adobe Target 대상에 세그먼트 활성화

Adobe Target은 Real-Time CDP의 대상으로 사용할 수 있습니다. Adobe Target 통합을 설정하려면 다음 위치로 이동하십시오. **대상**&#x200B;에 대해 **카탈로그**.

클릭 **개인화** 에서 **카테고리** 메뉴 아래의 제품에서 사용할 수 있습니다. 그러면 **Adobe Target** 대상 카드. 클릭 **세그먼트 활성화**.

![AT](./images/atdest1.png)

대상을 선택합니다 ``Bootcamp Target`` 을(를) 클릭합니다. **다음**.

![AT](./images/atdest3.png)

사용 가능한 세그먼트 목록에서 만든 세그먼트를 선택합니다 [1.3 세그먼트 만들기](./ex3.md): `yourLastName - Interest in Real-Time CDP`. 그런 다음 **다음**.

![AT](./images/atdest8.png)

다음 페이지에서 **다음**.

![AT](./images/atdest9.png)

**마침을 클릭합니다**.

![AT](./images/atdest10.png)

이제 세그먼트가 Adobe Target에 대해 활성화됩니다.

![AT](./images/atdest11.png)

>[!IMPORTANT]
>
>Real-Time CDP에서 Adobe Target 대상을 방금 만든 경우 대상이 라이브로 전환되려면 최대 1시간이 걸릴 수 있습니다. 백엔드 구성 설정으로 인해 일회성 대기 시간입니다. 초기 1시간 대기 시간 및 백엔드 구성이 완료되면 Adobe Target 대상으로 전송되는 새로 추가된 Edge 세그먼트를 실시간으로 타깃팅할 수 있습니다.

## 1.4.2 Adobe Target 양식 기반 활동 구성

이제 Real-Time CDP 세그먼트가 Adobe Target으로 전송되도록 구성되었으므로 Adobe Target에서 경험 타깃팅 활동을 구성할 수 있습니다. 이 연습에서는 시각적 경험 작성기 기반 활동을 구성합니다.

이동하여 Adobe Experience Cloud 홈 페이지로 이동합니다. [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). 클릭 **Target** 열려고

![RTCDP](./images/excl.png)

설정 **Adobe Target** homepage에는 기존의 모든 활동이 표시됩니다.
클릭 **+ 활동 만들기** 새 활동을 만들려면

![RTCDP](./images/exclatov.png)

선택 **경험 타깃팅**.

![RTCDP](./images/exclatcrxt.png)

선택 **시각적** 그리고 **활동 URL** to `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`로 바꾸십시오.

>[!IMPORTANT]
>
>사용 중인 모든 사용자는 개별 웹 페이지를 사용하여 다양한 Adobe Target 경험의 충돌을 방지해야 합니다. 여기 로 이동하여 웹 페이지를 선택하고 URL을 찾을 수 있습니다. [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>모든 페이지는 동일한 기본 URL을 공유하고 참가자 수로 끝납니다.
>
>예를 들어 참가자 1은 URL을 사용해야 합니다 `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, 참가자 30은 URL을 사용해야 합니다. `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

작업 공간을 선택합니다 **AT Bootcamp**.

**다음**&#x200B;을 클릭합니다.

![RTCDP](./images/exclatcrxtdtlform.png)

이제 시각적 경험 작성기에 있습니다. 웹 사이트가 완전히 로드될 때까지 20~30초가 걸릴 수 있습니다.

![RTCDP](./images/atform1.png)

현재 기본 대상은 입니다 **모든 방문자**. 을(를) 클릭합니다. **세 점** 다음 **모든 방문자** 을(를) 클릭합니다. **대상 변경**.

![RTCDP](./images/atform3.png)

이제 사용 가능한 대상자 목록이 표시되고, 이전에 만들어서 Adobe Target으로 보낸 Adobe Experience Platform 세그먼트가 이제 이 목록에 포함됩니다. Adobe Experience Platform에서 이전에 만든 세그먼트를 선택합니다. 클릭 **대상 할당**.

![RTCDP](./images/exclatvecchaud.png)

이제 Adobe Experience Platform 세그먼트가 이 경험 타깃팅 활동의 일부입니다.

![RTCDP](./images/atform4.png)

대표 이미지를 변경하려면 먼저 을(를) 클릭해야 합니다 **모두 허용** ( 쿠키 배너 ) 아래에 그룹화됩니다.

이렇게 하려면 로 이동하십시오. **찾아보기**

![RTCDP](./images/cook1.png)

다음을 클릭합니다. **모두 허용**.

![RTCDP](./images/cook2.png)

다음으로 돌아갑니다. **작성**.

![RTCDP](./images/cook3.png)

이제 웹 사이트의 홈 페이지에서 영웅 이미지를 변경해 보겠습니다. 웹 사이트에서 기본 대표 이미지를 클릭하고 **컨텐츠 바꾸기** 그런 다음 **이미지**.

![RTCDP](./images/atform5.png)

이미지 파일을 검색합니다 **rtcdp.png**. 선택한 다음 을(를) 클릭합니다 **저장**.

![RTCDP](./images/atform6.png)

그러면 선택한 대상에 대해 새 이미지가 포함된 새 경험이 표시됩니다.

![RTCDP](./images/atform7.png)

왼쪽 위 모서리에 있는 활동의 제목을 클릭하여 이름을 변경합니다.

![RTCDP](./images/exclatvecname.png)

이름은 다음을 사용하십시오.

- `yourLastName - RTCDP - XT (VEC)`

**다음**&#x200B;을 클릭합니다.

![RTCDP](./images/atform8.png)

**다음**&#x200B;을 클릭합니다.

![RTCDP](./images/atform8a.png)

설정 **목표 및 설정** - 페이지, 이동 **목표 지표**.

![RTCDP](./images/atform9.png)

기본 목표를 다음으로 설정 **참여** - **사이트에서 보낸 시간**. **저장 및 닫기**&#x200B;를 클릭합니다.

![RTCDP](./images/vec3.png)

이제 **활동 개요** 페이지. 활동을 활성화해야 합니다.

![RTCDP](./images/atform10.png)

필드를 클릭합니다 **비활성** 을(를) 선택합니다. **활성화**.

![RTCDP](./images/atform11.png)

그러면 활동이 이제 라이브 상태가 된다는 시각적 확인이 제공됩니다.

![RTCDP](./images/atform12.png)

이제 활동이 활성 상태이며 Bootcamp 웹 사이트에서 테스트할 수 있습니다.

이제 데모 웹 사이트로 돌아가 제품 페이지를 **Real-Time CDP**&#x200B;만든 세그먼트에 대한 자격이 즉시 부여되고 홈 페이지에 Adobe Target 활동이 실시간으로 표시됩니다.

>[!IMPORTANT]
>
>사용 중인 모든 사용자는 개별 웹 페이지를 사용하여 다양한 Adobe Target 경험의 충돌을 방지해야 합니다. 여기 로 이동하여 웹 페이지를 선택하고 URL을 찾을 수 있습니다. [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>모든 페이지는 동일한 기본 URL을 공유하고 참가자 수로 끝납니다.
>
>예를 들어 참가자 1은 URL을 사용해야 합니다 `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, 참가자 30은 URL을 사용해야 합니다. `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

다음 단계: [1.5 조치 수행: facebook에 세그먼트 보내기](./ex5.md)

[사용자 흐름 1로 돌아가기](./uc1.md)

[모든 모듈로 돌아가기](../../overview.md)
