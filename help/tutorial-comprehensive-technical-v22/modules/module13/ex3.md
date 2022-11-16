---
title: Microsoft Azure 이벤트 허브에 세그먼트 활성화 - 스트리밍 세그먼트 만들기
description: Microsoft Azure 이벤트 허브에 세그먼트 활성화 - 스트리밍 세그먼트 만들기
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: de3824bd-553c-4281-8edf-29abcc28a8e7
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 1%

---

# 13.3 세그먼트 만들기

## 13.3.1 소개

간단한 세그먼트를 만듭니다.

- **장비에 대한 관심** 방문할 때 자격을 부여하는 고객 프로필의 **장비** Luma 데모 웹 사이트의 페이지입니다.

### 잘 알고 있습니다

실시간 CDP는 해당 대상의 활성화 목록에 포함된 세그먼트에 대한 자격이 있는 경우 대상에 대한 활성화를 트리거합니다. 이 경우 해당 대상으로 전송할 세그먼트 자격 페이로드에는 다음이 포함됩니다 **프로필이 자격을 주는 모든 세그먼트**.

이 모듈의 목표는 고객 프로필의 세그먼트 자격이 로 전송되었음을 표시하는 것입니다 **your** 이벤트 허브 대상을 실시간으로 표시합니다.

### 세그먼트 상태

Adobe Experience Platform의 세그먼트 자격에는 항상 가 있습니다 **상태**-property 및 는 다음 중 하나일 수 있습니다.

- **실현**: 이는 새 세그먼트 자격을 나타냅니다
- **기존**: 기존 세그먼트 자격을 나타냅니다
- **종료한**: 이는 프로필이 더 이상 세그먼트에 적합하지 않음을 나타냅니다

## 13.3.2 세그먼트 작성

세그먼트 빌드는 [모듈 6](../module6/real-time-cdp-build-a-segment-take-action.md).

### 세그먼트 만들기

다음 URL로 이동하여 Adobe Experience Platform에 로그인합니다. [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

로그인하면 Adobe Experience Platform 홈 페이지가 표시됩니다.

![데이터 수집](../module2/images/home.png)

계속하기 전에 **샌드박스**. 선택할 샌드박스의 이름은 다음과 같습니다 ``--aepSandboxId--``. 이 작업은 텍스트를 클릭하여 수행할 수 있습니다 **[!UICONTROL 프로덕션 제품]** 화면 상단에 있는 파란색 줄에 표시됩니다. 적절한 샌드박스를 선택하면 화면 변경 사항이 표시되고 이제 전용 샌드박스에 있습니다.

![데이터 수집](../module2/images/sb1.png)

이동 **세그먼트**. 을(를) 클릭합니다. **+ 세그먼트 만들기** 버튼을 클릭합니다.

![데이터 수집](./images/seg.png)

세그먼트 이름을 지정합니다 `--demoProfileLdap-- - Interest in Equipment` 그리고 페이지 이름 경험 이벤트를 추가합니다.

클릭 **이벤트**, 드래그 앤 드롭 **XDM ExperienceEvent > 웹 > 웹 페이지 세부 사항 > 이름**. Enter 키 **장비** 로서의 값:

![4-05-create-ee-2.png](./images/4-05-create-ee-2.png)

드래그 앤 드롭 **XDM ExperienceEvent > `--aepTenantIdSchema--` > demoEnvironment > brandName**. Enter 키 `--demoProfileLdap--` 비교 매개 변수를 값으로 설정합니다. **다음 포함** 을(를) 클릭합니다. **저장**:

![4-05-create-ee-2-brand.png](./images/4-05-create-ee-2-brand.png)

### PQL 정의

세그먼트의 PQL은 다음과 같습니다.

```code
CHAIN(xEvent, timestamp, [C0: WHAT(web.webPageDetails.name.equals("equipment", false) and _experienceplatform.demoEnvironment.brandName.contains("--demoProfileLdap--", false))])
```

다음 단계: [13.4 세그먼트 활성화](./ex4.md)

[모듈 13으로 돌아가기](./segment-activation-microsoft-azure-eventhub.md)

[모든 모듈로 돌아가기](./../../overview.md)
