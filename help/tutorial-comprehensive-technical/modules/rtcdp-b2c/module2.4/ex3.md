---
title: Microsoft Azure 이벤트 허브에 대한 세그먼트 활성화 - 스트리밍 세그먼트 만들기
description: Microsoft Azure 이벤트 허브에 대한 세그먼트 활성화 - 스트리밍 세그먼트 만들기
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---

# 2.4.3 세그먼트 만들기

## 2.4.3.1 소개

간단한 세그먼트를 만듭니다.

- Luma 데모 웹 사이트의 **장비** 페이지를 방문할 때 고객 프로필이 자격을 부여할 장비에 대한 **관심**.

### 알아 둘 사항

Real-Time CDP는 해당 대상의 활성화 목록에 포함된 세그먼트에 대한 자격이 있을 때 대상에 대한 활성화를 트리거합니다. 이 경우 해당 대상으로 전송되는 세그먼트 자격 페이로드에는 **프로필이 자격을 갖는 모든 세그먼트**&#x200B;가 포함됩니다.

이 모듈의 목표는 고객 프로필의 세그먼트 자격이 **내** 이벤트 허브 대상으로 실시간으로 전송됨을 보여 주는 것입니다.

### 세그먼트 상태

Adobe Experience Platform의 세그먼트 자격은 항상 **status** 속성을 가지며 다음 중 하나일 수 있습니다.

- **실현됨**: 새 세그먼트 자격을 나타냅니다.
- **기존**: 기존 세그먼트 자격을 나타냅니다.
- **종료됨**: 프로필이 더 이상 세그먼트에 적합하지 않음을 나타냅니다.

## 2.4.3.2 세그먼트 빌드

세그먼트 만들기는 [모듈 2.3](./../../../modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md)에 자세히 설명되어 있습니다.

### 세그먼트 만들기

URL [https://experience.adobe.com/platform](https://experience.adobe.com/platform)로 이동하여 Adobe Experience Platform에 로그인합니다.

로그인하면 Adobe Experience Platform 홈페이지에 접속하게 됩니다.

![데이터 수집](./../../../modules/datacollection/module1.2/images/home.png)

계속하려면 **샌드박스**&#x200B;를 선택해야 합니다. 선택할 샌드박스 이름이 ``--aepSandboxName--``입니다. 화면 상단의 파란색 선에 있는 텍스트 **[!UICONTROL 프로덕션]**&#x200B;을(를) 클릭하면 됩니다. 적절한 샌드박스를 선택하면 화면이 변경되고 이제 전용 샌드박스에 있습니다.

![데이터 수집](./../../../modules/datacollection/module1.2/images/sb1.png)

**세그먼트**(으)로 이동합니다. **+ 세그먼트 만들기** 단추를 클릭합니다.

![데이터 수집](./images/seg.png)

세그먼트 이름을 `--aepUserLdap-- - Interest in Equipment`로 지정하고 페이지 이름 경험 이벤트를 추가합니다.

**이벤트**&#x200B;를 클릭하고 **XDM ExperienceEvent > 웹 > 웹 페이지 세부 정보 > 이름**&#x200B;을(를) 끌어서 놓습니다. 값으로 **equipment**&#x200B;을(를) 입력하십시오.

![4-05-create-ee-2.png](./images/4-05-create-ee-2.png)

**XDM ExperienceEvent > `--aepTenantId--` > demoEnvironment > brandName**&#x200B;을(를) 끌어서 놓습니다. `--aepUserLdap--`을(를) 값으로 입력하고 비교 매개 변수를 **contains**(으)로 설정한 다음 **저장**&#x200B;을(를) 클릭합니다.

![4-05-create-ee-2-brand.png](./images/4-05-create-ee-2-brand.png)

### PQL 정의

세그먼트의 PQL은 다음과 같습니다.

```code
CHAIN(xEvent, timestamp, [C0: WHAT(web.webPageDetails.name.equals("equipment", false) and _experienceplatform.demoEnvironment.brandName.contains("--aepUserLdap--", false))])
```

다음 단계: [2.4.4 세그먼트 활성화](./ex4.md)

[모듈 2.4로 돌아가기](./segment-activation-microsoft-azure-eventhub.md)

[모든 모듈로 돌아가기](./../../../overview.md)
