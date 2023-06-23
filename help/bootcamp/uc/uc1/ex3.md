---
title: 부트캠프 - 실시간 고객 프로필 - 세그먼트 만들기 - UI
description: 부트캠프 - 실시간 고객 프로필 - 세그먼트 만들기 - UI
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 37d4a5e8-e2bc-4c8c-a74f-09f74ea79962
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 3%

---

# 1.3 세그먼트 만들기 - UI

이 연습에서는 Adobe Experience Platform의 세그먼트 빌더를 사용하여 세그먼트를 만듭니다.

## 스토리

다음으로 이동 [Adobe Experience Platform](https://experience.adobe.com/platform). 로그인하면 Adobe Experience Platform 홈페이지에 접속하게 됩니다.

![데이터 수집](./images/home.png)

계속하기 전에 **샌드박스**. 선택할 샌드박스 이름이 로 지정됩니다. ``Bootcamp``. 텍스트를 클릭하여 이 작업을 수행할 수 있습니다 **[!UICONTROL 프로덕션 프로덕션]** 화면 상단의 파란색 선. 적절한 을(를) 선택한 후 [!UICONTROL 샌드박스], 화면 변경 사항이 표시되며 이제 전용 모드로 전환됩니다. [!UICONTROL 샌드박스].

![데이터 수집](./images/sb1.png)

왼쪽에 있는 메뉴에서 **세그먼트**. 이 페이지에서는 기존의 모든 세그먼트에 대한 개요를 볼 수 있습니다. 을(를) 클릭합니다 **+ 세그먼트 만들기** 단추를 클릭하여 새 세그먼트 만들기를 시작합니다.

![세그먼테이션](./images/menuseg.png)

새 세그먼트 빌더에 로그인하면 **속성** 메뉴 옵션 및 **XDM 개별 프로필** 참조.

![세그먼테이션](./images/segmentationui.png)

XDM은 경험 비즈니스를 지원하는 언어이므로 XDM은 세그먼트 빌더를 위한 기반이기도 합니다. Platform에서 수집되는 모든 데이터는 XDM에 대해 매핑되어야 하며, 따라서 모든 데이터는 해당 데이터의 출처에 관계없이 동일한 데이터 모델의 일부가 됩니다. 이렇게 하면 세그먼트를 작성할 때 이 하나의 세그먼트 빌더 UI에서 동일한 워크플로우의 모든 원본의 데이터를 결합할 수 있으므로 큰 이점이 있습니다. 세그먼트 빌더 내에 빌드된 세그먼트는 활성화를 위해 Adobe Target, Adobe Campaign 및 Adobe Audience Manager과 같은 솔루션으로 보낼 수 있습니다.

이제 제품을 본 모든 고객의 세그먼트를 만들어야 합니다 **Real-Time CDP**.

이 세그먼트를 작성하려면 경험 이벤트를 추가해야 합니다. 다음을 클릭하여 모든 경험 이벤트를 찾을 수 있습니다. **이벤트** 아이콘 **필드** 메뉴 모음

![세그먼테이션](./images/findee.png)

다음으로, 당신은 최고 수준을 볼 것입니다, **XDM 경험 이벤트** 노드. 클릭 **XDM ExperienceEvent**.

![세그먼테이션](./images/see.png)

다음으로 이동 **제품 목록 항목**.

![세그먼테이션](./images/plitems.png)

선택 **이름** 을(를) 끌어서 놓습니다. **이름** 왼쪽 메뉴에서 세그먼트 빌더 캔버스로 **이벤트** 섹션. 그러면 다음과 같은 결과가 표시됩니다.

![세그먼테이션](./images/eewebpdtlname.png)

비교 매개 변수는 다음과 같아야 합니다. **다음과 같음** 입력 필드에 을 입력합니다. **Real-time CDP**.

![세그먼테이션](./images/pv.png)

세그먼트 빌더에 요소를 추가할 때마다 **예상 새로 고침** 단추를 클릭하여 세그먼트의 모집단에 대한 새 예상을 가져옵니다.

![세그먼테이션](./images/refreshest.png)

다음으로: **평가 방법**, 선택 **Edge**.

![세그먼테이션](./images/evedge.png)

마지막으로 세그먼트 이름을 지정하고 저장하겠습니다.

명명 규칙으로 다음을 사용합니다.

- `yourLastName - Interest in Real-Time CDP`

그런 다음 **저장 및 닫기** 버튼을 클릭하여 세그먼트를 저장합니다.

![세그먼테이션](./images/segmentname.png)

이제 세그먼트 개요 페이지로 돌아갑니다. 그러면 세그먼트에 적합한 고객 프로필의 샘플 미리보기가 표시됩니다.

![세그먼테이션](./images/savedsegment.png)

이제 다음 연습을 계속하여 Adobe Target에서 세그먼트를 사용할 수 있습니다.

다음 단계: [1.4 조치 취하기: 세그먼트를 Adobe Target에 보내기](./ex4.md)

[사용자 흐름 1로 돌아가기](./uc1.md)

[모든 모듈로 돌아가기](../../overview.md)
