---
title: Real-Time CDP - 세그먼트 작성 및 작업 수행 - 세그먼트 작성
description: Real-Time CDP - 세그먼트 작성 및 작업 수행 - 세그먼트 작성
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 2%

---

# 2.3.1 세그먼트 만들기

이 연습에서는 Adobe Experience Platform의 세그먼트 빌더를 사용하여 세그먼트를 만듭니다.

## 2.3.1.1 컨텍스트

오늘날의 세계에서 고객의 행동에 대응하는 것은 실시간으로 이루어질 필요가 있습니다. 실시간으로 고객 행동에 대응하는 방법 중 하나는 세그먼트가 실시간으로 자격을 얻는다는 조건으로 세그먼트를 사용하는 것입니다. 이 연습에서는 사용 중인 웹 사이트의 실제 활동을 고려하여 세그먼트를 작성해야 합니다.

## 2.3.1.2 반응할 동작 식별

[https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects)(으)로 이동합니다. Adobe ID으로 로그인하면 이 메시지가 표시됩니다. 웹 사이트 프로젝트를 클릭하여 엽니다.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

이제 아래 흐름을 따라 웹 사이트에 액세스할 수 있습니다. **통합**&#x200B;을 클릭합니다.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web1.png)

**통합** 페이지에서 연습 0.1에서 만든 데이터 수집 속성을 선택해야 합니다.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web2.png)

그러면 데모 웹 사이트가 열리는 것을 볼 수 있습니다. URL을 선택하고 클립보드에 복사합니다.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web3.png)

새 시크릿 브라우저 창을 엽니다.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web4.png)

이전 단계에서 복사한 데모 웹 사이트의 URL을 붙여 넣습니다. 그런 다음 Adobe ID을 사용하여 로그인하라는 메시지가 표시됩니다.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web5.png)

계정 유형을 선택하고 로그인 프로세스를 완료합니다.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web6.png)

그러면 웹 사이트가 시크릿 브라우저 창에 로드되는 것을 볼 수 있습니다. 모든 데모에 대해 새로운 시크릿 브라우저 창을 사용하여 데모 웹 사이트 URL을 로드해야 합니다.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web7.png)

이 예에서는 특정 제품을 보는 특정 고객에게 응답하려고 합니다.
**Luma** 홈페이지에서 **Men**(으)로 이동하여 제품 **PROTEUS FITNESS JACKSHIRT**&#x200B;을(를) 클릭하십시오.

![데이터 수집](./images/homenadia.png)

따라서 누군가가 **PROTEUS FITNESS JACKSHIRT**&#x200B;에 대한 제품 페이지를 방문하면 조치를 취할 수 있습니다. 조치를 취하기 위해 가장 먼저 해야 할 일은 세그먼트를 정의하는 것입니다.

![데이터 수집](./images/homenadiapp.png)

## 2.3.1.3 세그먼트 만들기

[Adobe Experience Platform](https://experience.adobe.com/platform)(으)로 이동합니다. 로그인하면 Adobe Experience Platform 홈페이지에 접속하게 됩니다.

![데이터 수집](./../../../modules/datacollection/module1.2/images/home.png)

계속하려면 **샌드박스**&#x200B;를 선택해야 합니다. 선택할 샌드박스 이름이 ``--aepSandboxName--``입니다. 화면 상단의 파란색 선에 있는 텍스트 **[!UICONTROL 프로덕션]**&#x200B;을(를) 클릭하면 됩니다. 적절한 [!UICONTROL 샌드박스]를 선택하면 화면이 변경되고 이제 전용 [!UICONTROL 샌드박스]에 있게 됩니다.

![데이터 수집](./../../../modules/datacollection/module1.2/images/sb1.png)

왼쪽의 메뉴에서 **세그먼트**(으)로 이동한 다음 기존의 모든 세그먼트에 대한 개요를 볼 수 있는 **찾아보기**(으)로 이동합니다. **세그먼트 만들기** 단추를 클릭하여 새 세그먼트를 만듭니다.

![세그먼테이션](./images/menuseg.png)

위에서 언급했듯이 **PROTEUS FITNESS JACKSHIRT** 제품을 본 모든 고객으로부터 세그먼트를 만들어야 합니다.

이 세그먼트를 작성하려면 이벤트를 추가해야 합니다. **세그먼트** 메뉴 모음의 **이벤트** 아이콘을 클릭하면 모든 이벤트를 찾을 수 있습니다.

상위 수준 **XDM ExperienceEvent** 노드가 표시됩니다.

**PROTEUS FITNESS JACKSHIRT** 제품을 방문한 고객을 찾으려면 **XDM ExperienceEvent**&#x200B;를 클릭하세요.

![세그먼테이션](./images/findee.png)

**제품 목록 항목**(으)로 아래로 스크롤하여 클릭합니다.

![세그먼테이션](./images/see.png)

**이름**&#x200B;을(를) 선택하고 왼쪽 **제품 목록 항목** 메뉴에서 **이름** 개체를 세그먼트 빌더 캔버스로 **이벤트** 섹션으로 끌어서 놓습니다.

![세그먼테이션](./images/eewebpdtlname1.png)

비교 매개 변수는 **equals**&#x200B;이어야 하며 입력 필드에 `PROTEUS FITNESS JACKSHIRT`을(를) 입력하십시오.

![세그먼테이션](./images/pv.png)

**이벤트 규칙**&#x200B;은(는) 이제 다음과 같습니다. 세그먼트 빌더에 요소를 추가할 때마다 **예상 새로 고침** 단추를 클릭하여 세그먼트에 있는 모집단의 새 예상 값을 가져올 수 있습니다.

![세그먼테이션](./images/ldap4.png)

마지막으로 세그먼트 이름을 지정하고 저장하겠습니다.

명명 규칙으로 다음을 사용합니다.

- `--aepUserLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`

세그먼트 이름은 다음과 같아야 합니다.
`vangeluw - Interest in PROTEUS FITNESS JACKSHIRT`

그런 다음 **저장 후 닫기** 단추를 클릭하여 세그먼트를 저장합니다.

![세그먼테이션](./images/segmentname.png)

이제 세그먼트 개요 페이지로 돌아갑니다.

![세그먼테이션](./images/savedsegment.png)

다음 단계: [2.3.2 대상을 사용하여 DV360 대상을 구성하는 방법 검토](./ex2.md)

[모듈 2.3으로 돌아가기](./real-time-cdp-build-a-segment-take-action.md)

[모든 모듈로 돌아가기](../../../overview.md)
