---
title: Bootcamp - 실시간 고객 프로필 - 세그먼트 만들기 - UI - 브라질
description: Bootcamp - 실시간 고객 프로필 - 세그먼트 만들기 - UI - 브라질
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 3%

---

# 1.3 세그먼트 만들기 - UI

이 연습에서는 Adobe Experience Platform의 세그먼트 빌더를 사용하여 세그먼트를 만듭니다.

## Story

이동 [Adobe Experience Platform](https://experience.adobe.com/platform). 로그인하면 Adobe Experience Platform 홈 페이지가 표시됩니다.

![데이터 수집](./images/home.png)

계속하기 전에 **샌드박스**. 선택할 샌드박스의 이름은 다음과 같습니다 ``Bootcamp``. 이 작업은 텍스트를 클릭하여 수행할 수 있습니다 **[!UICONTROL 프로덕션 제품]** 화면 상단에 있는 파란색 줄에 표시됩니다. 적절한 [!UICONTROL 샌드박스]이렇게 하면 화면 변경 사항이 표시되고 이제 전용 화면에 표시됩니다 [!UICONTROL 샌드박스].

![데이터 수집](./images/sb1.png)

왼쪽 메뉴에서 **세그먼트**. 이 페이지에서는 기존 모든 세그먼트에 대한 개요를 볼 수 있습니다. 을(를) 클릭합니다. **+ 세그먼트 만들기** 새 세그먼트 만들기를 시작하는 단추.

![세그먼테이션](./images/menuseg.png)

새 세그먼트 빌더에 있으면 즉시 **속성** 메뉴 옵션 및 **XDM 개별 프로필** 참조.

![세그먼테이션](./images/segmentationui.png)

XDM은 경험 비즈니스를 구동하는 언어이므로 XDM은 세그먼트 빌더의 기반이기도 합니다. 플랫폼에서 수집된 모든 데이터는 XDM에 대해 매핑해야 합니다. 따라서 모든 데이터는 해당 데이터의 위치와 관계없이 동일한 데이터 모델의 일부가 됩니다. 이렇게 하면 세그먼트를 작성할 때, 이 세그먼트 빌더 UI에서 처럼 동일한 워크플로우에서 모든 출처의 데이터를 결합할 수 있는 큰 이점이 있습니다. 세그먼트 빌더 내에 작성된 세그먼트는 활성화를 위해 Adobe Target, Adobe Campaign 및 Adobe Audience Manager과 같은 솔루션으로 보낼 수 있습니다.

이제 제품을 본 모든 고객의 세그먼트를 만들어야 합니다 **Real-Time CDP**.

이 세그먼트를 만들려면 경험 이벤트를 추가해야 합니다. 를 클릭하여 모든 경험 이벤트를 찾을 수 있습니다 **이벤트** 아이콘( **필드** 메뉴 모음

![세그먼테이션](./images/findee.png)

다음으로, 당신은 최고 수준을 볼 것입니다. **XDM ExperienceEvents** 노드 아래에 있어야 합니다. 클릭 **XDM ExperienceEvent**.

![세그먼테이션](./images/see.png)

이동 **제품 목록 항목**.

![세그먼테이션](./images/plitems.png)

선택 **이름** 끌어서 놓습니다. **이름** 왼쪽 메뉴에서 세그먼트 빌더 캔버스로 **이벤트** 섹션을 참조하십시오. 그러면 다음 내용이 표시됩니다.

![세그먼테이션](./images/eewebpdtlname.png)

비교 매개 변수는 **다음과 같음** 입력 필드에 을 입력합니다. **실시간 CDP**.

![세그먼테이션](./images/pv.png)

세그먼트 빌더에 요소를 추가할 때마다 **예상 새로 고침** 세그먼트의 모집단을 새로 추정하기 위한 단추.

![세그먼테이션](./images/refreshest.png)

로서의 **평가 방법**, 선택 **Edge**.

![세그먼테이션](./images/evedge.png)

마지막으로 세그먼트 이름을 지정하고 저장하겠습니다.

명명 규칙으로, 다음을 사용하십시오.

- `yourLastName - Interest in Real-Time CDP`

그런 다음 **저장 후 닫기** 세그먼트를 저장하는 버튼을 클릭합니다.

![세그먼테이션](./images/segmentname.png)

이제 세그먼트 개요 페이지로 돌아갑니다. 여기에서 세그먼트에 대한 자격이 있는 고객 프로필의 샘플 미리 보기를 볼 수 있습니다.

![세그먼테이션](./images/savedsegment.png)

이제 다음 연습으로 계속 이동하여 Adobe Target에서 세그먼트를 사용할 수 있습니다.

다음 단계: [1.4 조치 수행: Adobe Target에 세그먼트 보내기](./ex4.md)

[사용자 흐름 1로 돌아가기](./uc1.md)

[모든 모듈로 돌아가기](../../overview.md)
