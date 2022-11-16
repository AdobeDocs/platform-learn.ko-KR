---
title: 실시간 CDP - 세그먼트 구축 및 조치 수행 - 세그먼트 구축
description: 실시간 CDP - 세그먼트 구축 및 조치 수행 - 세그먼트 구축
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: c0778e81-4282-433d-9e02-37e32bf370ef
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 2%

---

# 6.1 세그먼트 만들기

이 연습에서는 Adobe Experience Platform의 세그먼트 빌더를 사용하여 세그먼트를 만듭니다.

## 6.1.1 컨텍스트

오늘날 세계 각국에서 고객의 행동에 반응하는 것은 실시간이어야 합니다. 실시간으로 고객 행동에 응답하는 방법 중 하나는 세그먼트가 실시간으로 적격인 상황에서 세그먼트를 사용하는 것입니다. 이 연습에서는 사용하고 있는 웹 사이트의 실제 활동을 고려하여 세그먼트를 만들어야 합니다.

## 6.1.2 반응할 동작을 식별합니다

이동 [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Adobe ID으로 로그인하면 다음이 표시됩니다. 웹 사이트 프로젝트를 클릭하여 엽니다.

![DSN](../module0/images/web8.png)

이제 아래 흐름을 따라 웹 사이트에 액세스할 수 있습니다. 클릭 **통합**.

![DSN](../module0/images/web1.png)

설정 **통합** 페이지에서 연습 0.1에서 생성된 데이터 수집 속성을 선택해야 합니다.

![DSN](../module0/images/web2.png)

그러면 데모 웹 사이트가 열립니다. URL을 선택하고 클립보드에 복사합니다.

![DSN](../module0/images/web3.png)

새 시크릿 브라우저 창을 엽니다.

![DSN](../module0/images/web4.png)

이전 단계에서 복사한 데모 웹 사이트의 URL을 붙여넣습니다. 그런 다음 Adobe ID을 사용하여 로그인하라는 메시지가 표시됩니다.

![DSN](../module0/images/web5.png)

계정 유형을 선택하고 로그인 프로세스를 완료합니다.

![DSN](../module0/images/web6.png)

그러면 시크릿 브라우저 창에서 로드되는 웹 사이트가 표시됩니다. 모든 데모에서는 신선하고 시크릿 브라우저 창을 사용하여 데모 웹 사이트 URL을 로드해야 합니다.

![DSN](../module0/images/web7.png)

이 예에서는 특정 제품을 보는 특정 고객에 응답하려고 합니다.
에서 **루마** homepage, **남성**&#x200B;를 클릭하고 제품을 클릭합니다. **프로테우스 피트니스 자크셔츠**.

![데이터 수집](./images/homenadia.png)

따라서 누군가 다음에 대한 제품 페이지를 방문할 때 **프로테우스 피트니스 자크셔츠**, 작업을 수행할 수 있어야 합니다. 작업을 수행하기 위해 가장 먼저 하는 일은 세그먼트를 정의하는 것입니다.

![데이터 수집](./images/homenadiapp.png)

## 6.1.3 세그먼트 만들기

이동 [Adobe Experience Platform](https://experience.adobe.com/platform). 로그인하면 Adobe Experience Platform 홈 페이지가 표시됩니다.

![데이터 수집](../module2/images/home.png)

계속하기 전에 **샌드박스**. 선택할 샌드박스의 이름은 다음과 같습니다 ``--aepSandboxId--``. 이 작업은 텍스트를 클릭하여 수행할 수 있습니다 **[!UICONTROL 프로덕션 제품]** 화면 상단에 있는 파란색 줄에 표시됩니다. 적절한 [!UICONTROL 샌드박스]이렇게 하면 화면 변경 사항이 표시되고 이제 전용 화면에 표시됩니다 [!UICONTROL 샌드박스].

![데이터 수집](../module2/images/sb1.png)

왼쪽 메뉴에서 **세그먼트** 그리고 나서 **찾아보기** 모든 기존 세그먼트에 대한 개요를 볼 수 있는 곳입니다. 을(를) 클릭합니다. **세그먼트 만들기** 새 세그먼트 만들기를 시작하는 단추.

![세그먼테이션](./images/menuseg.png)

위에서 언급했듯이 제품을 본 모든 고객으로부터 세그먼트를 만들어야 합니다 **프로테우스 피트니스 자크셔츠**.

이 세그먼트를 만들려면 이벤트를 추가해야 합니다. 를 클릭하여 모든 이벤트를 찾을 수 있습니다 **이벤트** 아이콘( **세그먼트** 메뉴 모음

다음으로, 상위 수준을 볼 수 있습니다 **XDM ExperienceEvent** 노드 아래에 있어야 합니다.

를 방문한 고객을 찾으려면 **프로테우스 피트니스 자크셔츠** product, **XDM ExperienceEvent**.

![세그먼테이션](./images/findee.png)

아래로 스크롤하여 **제품 목록 항목** 클릭하여 선택합니다.

![세그먼테이션](./images/see.png)

선택 **이름** 끌어서 놓습니다. **이름** 왼쪽의 개체 **제품 목록 항목** 메뉴 아래의 세그먼트 빌더 캔버스에 **이벤트** 섹션을 참조하십시오.

![세그먼테이션](./images/eewebpdtlname1.png)

비교 매개 변수는 **다음과 같음** 입력 필드에 을 입력합니다. `PROTEUS FITNESS JACKSHIRT`.

![세그먼테이션](./images/pv.png)

사용자 **이벤트 규칙** 이제 이런 모습이어야 합니다. 세그먼트 빌더에 요소를 추가할 때마다 **예상 새로 고침** 세그먼트의 모집단을 새로 추정하기 위한 단추.

![세그먼테이션](./images/ldap4.png)

마지막으로 세그먼트 이름을 지정하고 저장하겠습니다.

명명 규칙으로, 다음을 사용하십시오.

- `--demoProfileLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`

세그먼트 이름은 다음과 같습니다.
`vangeluw - Interest in PROTEUS FITNESS JACKSHIRT`

그런 다음 **저장 후 닫기** 세그먼트를 저장하는 버튼을 클릭합니다.

![세그먼테이션](./images/segmentname.png)

이제 세그먼트 개요 페이지로 돌아갑니다.

![세그먼테이션](./images/savedsegment.png)

다음 단계: [6.2 대상을 사용하여 DV360 대상을 구성하는 방법 검토](./ex2.md)

[모듈 11로 돌아가기](./real-time-cdp-build-a-segment-take-action.md)

[모든 모듈로 돌아가기](../../overview.md)
