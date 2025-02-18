---
title: 기초 - 실시간 고객 프로필 - 대상 만들기 - UI
description: 기초 - 실시간 고객 프로필 - 대상 만들기 - UI
kt: 5342
doc-type: tutorial
exl-id: 4870ea42-810b-400b-8285-ab1f89c6a018
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 3%

---

# 2.1.4 대상 만들기 - UI

이 연습에서는 Adobe Experience Platform의 대상 빌더를 사용하여 대상을 만듭니다.

[Adobe Experience Platform](https://experience.adobe.com/platform)(으)로 이동합니다. 로그인하면 Adobe Experience Platform 홈페이지에 접속하게 됩니다.

![데이터 수집](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

계속하려면 **샌드박스**&#x200B;를 선택해야 합니다. 선택할 샌드박스 이름이 ``--aepSandboxName--``입니다. 적절한 [!UICONTROL 샌드박스]를 선택하면 화면이 변경되고 이제 전용 [!UICONTROL 샌드박스]에 있게 됩니다.

![데이터 수집](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

왼쪽에 있는 메뉴에서 **대상**(으)로 이동합니다. 이 페이지에서는 모든 기존 대상에 대한 개요를 볼 수 있습니다. 새 대상을 만들려면 **+ 대상 만들기** 단추를 클릭하십시오.

![세그먼테이션](./images/menuseg.png)

**규칙 빌드**&#x200B;를 선택하고 **만들기**&#x200B;를 클릭합니다.

![세그먼테이션](./images/menusegbr.png)

새 대상 빌더에 로그인하면 **특성** 메뉴 옵션과 **XDM 개별 프로필** 참조가 즉시 표시됩니다.

![세그먼테이션](./images/segmentationui.png)

XDM은 경험 비즈니스를 지원하는 언어이므로 XDM은 대상 빌더의 기반이기도 합니다. Platform에서 수집되는 모든 데이터는 XDM에 대해 매핑되어야 하며, 따라서 모든 데이터는 해당 데이터의 출처에 관계없이 동일한 데이터 모델의 일부가 됩니다. 이렇게 하면 대상을 작성할 때 이 하나의 대상 빌더 UI에서 동일한 워크플로우의 모든 원본의 데이터를 결합할 수 있으므로 큰 이점이 있습니다. Audience Builder 내에 빌드된 대상은 활성화를 위해 Adobe Target, Adobe Campaign 및 Adobe Audience Manager과 같은 솔루션으로 보낼 수 있습니다.

모든 **남성** 고객을 포함하는 대상을 만들겠습니다.

젠더 속성에 접근하려면 XDM을 이해하고 알아야 합니다.

성별은 개인의 속성이며 속성에서 찾을 수 있습니다. 먼저 **XDM 개인 프로필**&#x200B;을 클릭하세요. 그러면 이걸 보게 될 거야. **XDM 개인 프로필** 창에서 **개인**&#x200B;을(를) 선택하십시오.

![세그먼테이션](./images/person.png)

그러면 이걸 보게 될 거야. **사용자**&#x200B;에서 **성별** 특성을 찾을 수 있습니다. Gender 속성을 대상 빌더로 드래그합니다.

![세그먼테이션](./images/gender.png)

이제 미리 채워진 옵션 중에서 특정 성별을 선택할 수 있습니다. 이 경우 **남성**&#x200B;을 선택하세요.

![세그먼테이션](./images/genderselection.png)

**남성**&#x200B;을(를) 선택한 후 **예상 새로 고침** 단추를 눌러 대상자의 모집단을 예상할 수 있습니다. 이는 비즈니스 사용자에게 매우 유용하므로 특정 속성이 결과 대상자 크기에 미치는 영향을 볼 수 있습니다.

![세그먼테이션](./images/segmentpreview.png)

그러면 아래와 같은 추정이 표시됩니다.

![세그먼테이션](./images/segmentpreviewest.png)

다음으로 대상을 조금 더 세분화해야 합니다. **iPhone 15 Pro** 제품을 본 모든 남성 고객의 대상을 구성해야 합니다.

이 대상을 빌드하려면 경험 이벤트를 추가해야 합니다. **필드** 메뉴 모음에서 **이벤트** 아이콘을 클릭하여 모든 경험 이벤트를 찾을 수 있습니다. 이제 최상위 수준인 **XDM ExperienceEvents** 노드가 표시됩니다. **XDM ExperienceEvent**&#x200B;을 클릭합니다.

![세그먼테이션](./images/findee.png)

**제품 목록 항목**(으)로 이동합니다.

![세그먼테이션](./images/plitems.png)

**이름**&#x200B;을(를) 선택하고 왼쪽 메뉴에서 **이름** 개체를 대상 빌더 캔버스로 **이벤트** 섹션으로 끌어서 놓습니다.

![세그먼테이션](./images/eeweb.png)

그러면 다음과 같은 결과가 표시됩니다.

![세그먼테이션](./images/eewebpdtlname.png)

비교 매개 변수는 **equals**&#x200B;이어야 하며 입력 필드에 **iPhone 15 Pro**&#x200B;을(를) 입력하십시오.

![세그먼테이션](./images/pv.png)

대상 빌더에 요소를 추가할 때마다 **예상 새로 고침** 단추를 클릭하여 대상에 있는 모집단의 새 예상 값을 가져올 수 있습니다.

지금까지 UI를 사용하여 대상자를 빌드했지만 대상자를 빌드하는 코드 옵션도 있습니다.

대상을 작성할 때 실제로 Profile Query Language(PQL) 쿼리를 작성합니다. PQL 코드를 시각화하려면 대상 빌더의 오른쪽 위 모서리에 있는 **코드 보기** 전환기를 클릭합니다.

![세그먼테이션](./images/codeview.png)

이제 전체 PQL 문을 볼 수 있습니다.

```sql
person.gender in ["male"] and CHAIN(xEvent, timestamp, [C0: WHAT(productListItems.exists(name.equals("iPhone 15 Pro", false)))])
```

**프로필 보기**&#x200B;를 클릭하여 이 대상자에 속하는 고객 프로필 샘플을 미리 볼 수도 있습니다.

![세그먼테이션](./images/previewprofilesdtl.png)

마지막으로, 청중에게 이름을 알려 주십시오.
**평가 메서드**&#x200B;을(를) **스트리밍**(으)로 설정하고 **게시**&#x200B;를 클릭합니다.

명명 규칙으로 다음을 사용합니다.

- `--aepUserLdap-- - Male customers with interest in iPhone 15 Pro`

![세그먼테이션](./images/segmentname.png)

대상 개요 페이지로 돌아갑니다.

![세그먼테이션](./images/savedsegment.png)

## 다음 단계

[2.1.5로 이동 콜센터에서 실시간 고객 프로필 확인](./ex5.md){target="_blank"}

[실시간 고객 프로필](./real-time-customer-profile.md){target="_blank"}(으)로 돌아가기

[모든 모듈](./../../../../overview.md){target="_blank"}(으)로 돌아가기
