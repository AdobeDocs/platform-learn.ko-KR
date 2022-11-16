---
title: 기초 - 실시간 고객 프로필 - 세그먼트 만들기 - UI
description: 기초 - 실시간 고객 프로필 - 세그먼트 만들기 - UI
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 2462addc-6123-44e6-991c-0e5c21256448
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 3%

---

# 3.4 세그먼트 만들기 - UI

이 연습에서는 Adobe Experience Platform의 세그먼트 빌더를 사용하여 세그먼트를 만듭니다.

## Story

이동 [Adobe Experience Platform](https://experience.adobe.com/platform). 로그인하면 Adobe Experience Platform 홈 페이지가 표시됩니다.

![데이터 수집](../module2/images/home.png)

계속하기 전에 **샌드박스**. 선택할 샌드박스의 이름은 다음과 같습니다 ``--aepSandboxId--``. 이 작업은 텍스트를 클릭하여 수행할 수 있습니다 **[!UICONTROL 프로덕션 제품]** 화면 상단에 있는 파란색 줄에 표시됩니다. 적절한 [!UICONTROL 샌드박스]이렇게 하면 화면 변경 사항이 표시되고 이제 전용 화면에 표시됩니다 [!UICONTROL 샌드박스].

![데이터 수집](../module2/images/sb1.png)

왼쪽 메뉴에서 **세그먼트**. 이 페이지에서는 기존 모든 세그먼트에 대한 개요를 볼 수 있습니다. 을(를) 클릭합니다. **+ 세그먼트 만들기** 새 세그먼트 만들기를 시작하는 단추.

![세그먼테이션](./images/menuseg.png)

새 세그먼트 빌더에 있으면 즉시 **속성** 메뉴 옵션 및 **XDM 개별 프로필** 참조.

![세그먼테이션](./images/segmentationui.png)

XDM은 경험 비즈니스를 구동하는 언어이므로 XDM은 세그먼트 빌더의 기반이기도 합니다. 플랫폼에서 수집된 모든 데이터는 XDM에 대해 매핑해야 합니다. 따라서 모든 데이터는 해당 데이터의 위치와 관계없이 동일한 데이터 모델의 일부가 됩니다. 이렇게 하면 세그먼트를 작성할 때, 이 세그먼트 빌더 UI에서 처럼 동일한 워크플로우에서 모든 출처의 데이터를 결합할 수 있는 큰 이점이 있습니다. 세그먼트 빌더 내에 작성된 세그먼트는 활성화를 위해 Adobe Target, Adobe Campaign 및 Adobe Audience Manager과 같은 솔루션으로 보낼 수 있습니다.

모든 세그먼트를 포함하는 세그먼트를 만들겠습니다 **남성** 고객.

gender 속성에 접근하려면 XDM을 이해하고 알고 있어야 합니다.

Gender는 Person의 속성이며 Attributes 아래에 찾을 수 있습니다. 따라서 먼저 을 클릭하여 **XDM 개별 프로필**. 그러면 이게 보입니다. 에서 **XDM 개별 프로필** 창, 선택 **개인**.

![세그먼테이션](./images/person.png)

그러면 이게 보입니다. in **개인**&#x200B;를 찾으면 **성별** 속성을 사용합니다. 성별 속성을 세그먼트 빌더로 드래그합니다.

![세그먼테이션](./images/gender.png)

이제 미리 채워진 옵션 중에서 특정 성별을 선택할 수 있습니다. 이 경우 **남성**.

![세그먼테이션](./images/genderselection.png)

선택 후 **남성**&#x200B;를 눌러 세그먼트의 모집단을 예측할 수 있습니다 **예상 새로 고침** 버튼을 클릭합니다. 이 기능은 비즈니스 사용자에게 매우 유용하며, 따라서 특정 속성이 결과 세그먼트 크기에 미치는 영향을 볼 수 있습니다.

![세그먼테이션](./images/segmentpreview.png)

그러면 다음과 같은 추정이 표시됩니다.

![세그먼테이션](./images/segmentpreviewest.png)

다음으로, 세그먼트를 약간 세분화해야 합니다. 제품을 본 모든 남성 고객으로 구성된 세그먼트를 만들어야 합니다 **Proteus Fitness Jackshirt(주황색)**.

이 세그먼트를 만들려면 경험 이벤트를 추가해야 합니다. 를 클릭하여 모든 경험 이벤트를 찾을 수 있습니다 **이벤트** 아이콘( **필드** 메뉴 모음

![세그먼테이션](./images/findee.png)

다음으로, 당신은 최고 수준을 볼 것입니다. **XDM ExperienceEvents** 노드 아래에 있어야 합니다. 클릭 **XDM ExperienceEvent**.

![세그먼테이션](./images/see.png)

이동 **제품 목록 항목**.

![세그먼테이션](./images/plitems.png)

선택 **이름** 끌어서 놓습니다. **이름** 왼쪽 메뉴에서 세그먼트 빌더 캔버스로 **이벤트** 섹션을 참조하십시오.

![세그먼테이션](./images/eeweb.png)

그러면 다음 내용이 표시됩니다.

![세그먼테이션](./images/eewebpdtlname.png)

비교 매개 변수는 **다음과 같음** 입력 필드에 을 입력합니다. **몬태나 윈드 재킷**.

![세그먼테이션](./images/pv.png)

세그먼트 빌더에 요소를 추가할 때마다 **예상 새로 고침** 세그먼트의 모집단을 새로 추정하기 위한 단추.

지금까지 UI를 사용하여 세그먼트를 작성했지만, 세그먼트를 만드는 코드 옵션도 있습니다.

세그먼트를 작성할 때 실제로 PQL(프로필 쿼리 언어) 쿼리를 작성하는 것입니다. PQL 코드를 시각화하려면 **코드 보기** 세그먼트 빌더의 오른쪽 위 모서리에 있는 전환기.

![세그먼테이션](./images/codeview.png)

이제 전체 PQL 문을 볼 수 있습니다.

```sql
person.gender in ["male"] and CHAIN(xEvent, timestamp, [C0: WHAT(productListItems.exists(name.equals("MONTANA WIND JACKET", false)))])
```

을 클릭하여 이 세그먼트에 속하는 고객 프로필의 샘플을 미리 볼 수도 있습니다 **프로필 보기**.

![세그먼테이션](./images/previewprofiles.png)

![세그먼테이션](./images/previewprofilesdtl.png)

마지막으로 세그먼트 이름을 지정하고 저장하겠습니다.

명명 규칙으로, 다음을 사용하십시오.

- `--demoProfileLdap-- - Male customers with interest in Montana Wind Jacket`

![세그먼테이션](./images/segmentname.png)

그런 다음 **저장 후 닫기** 세그먼트를 저장할 단추를 클릭하면 세그먼트 개요 페이지로 돌아갑니다.

![세그먼테이션](./images/savedsegment.png)

이제 다음 연습을 계속 진행하고 API를 통해 세그먼트를 만들 수 있습니다.

다음 단계: [3.5 세그먼트 만들기 - API](./ex5.md)

[모듈 3으로 돌아가기](./real-time-customer-profile.md)

[모든 모듈로 돌아가기](../../overview.md)
