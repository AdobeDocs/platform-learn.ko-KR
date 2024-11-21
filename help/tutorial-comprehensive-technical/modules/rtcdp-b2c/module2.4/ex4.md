---
title: Microsoft Azure Event Hub Audience Activation - 대상 만들기
description: Microsoft Azure Event Hub Audience Activation - 대상 만들기
kt: 5342
doc-type: tutorial
exl-id: 56f6a6dc-82aa-4b64-a3f6-b6f59c484ccb
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 2%

---

# 2.4.4 대상 만들기

## 소개

간단한 대상자를 만듭니다.

- 고객이 CitiSignal 데모 웹 사이트의 **계획** 페이지를 방문할 때 자격을 부여할 계획에 대한 **관심**.

### 알아 둘 사항

Real-Time CDP는 해당 대상의 활성화 목록에 속하는 대상에 대한 자격이 있을 때 대상에 대한 활성화를 트리거합니다. 이 경우 해당 대상으로 전송되는 대상 자격 페이로드에는 **고객 프로필이 자격을 갖는 모든 대상**&#x200B;이 포함됩니다.

이 모듈의 목표는 고객 프로필의 대상 자격이 거의 실시간으로 이벤트 허브 대상으로 전송되는 것을 보여 주는 것입니다.

### 대상 상태

Adobe Experience Platform의 대상 자격은 항상 **status** 속성을 가지며 다음 중 하나가 될 수 있습니다.

- **실현됨**: 새 대상 자격을 나타냅니다.
- **종료됨**: 프로필이 더 이상 대상에 적합하지 않음을 나타냅니다.

## 대상자 작성

URL [https://experience.adobe.com/platform](https://experience.adobe.com/platform)로 이동하여 Adobe Experience Platform에 로그인합니다.

로그인하면 Adobe Experience Platform 홈페이지에 접속하게 됩니다.

![데이터 수집](./../../../modules/datacollection/module1.2/images/home.png)

계속하려면 **샌드박스**&#x200B;를 선택해야 합니다. 선택할 샌드박스 이름이 ``--aepSandboxName--``입니다. 적절한 샌드박스를 선택하면 화면이 변경되고 이제 전용 샌드박스에 있습니다.

![데이터 수집](./../../../modules/datacollection/module1.2/images/sb1.png)

**대상**(으)로 이동합니다. **+ 대상자 만들기** 단추를 클릭합니다.

![데이터 수집](./images/seg.png)

**규칙 빌드**&#x200B;를 선택하고 **만들기**&#x200B;를 클릭합니다.

![데이터 수집](./images/seg1.png)

대상자의 이름을 `--aepUserLdap-- - Interest in Plans`로 지정하고 평가 메서드를 **Edge**(으)로 설정한 다음 경험 이벤트에서 페이지 이름을 추가하십시오.

**이벤트**&#x200B;를 클릭하고 **XDM ExperienceEvent > 웹 > 웹 페이지 세부 정보 > 이름**&#x200B;을(를) 끌어서 놓습니다. 값으로 **계획**&#x200B;을(를) 입력하십시오.

![4-05-create-ee-2.png](./images/405createee2.png)

**XDM ExperienceEvent > `--aepTenantId--` > demoEnvironment > brandName**&#x200B;을(를) 끌어서 놓습니다. `--aepUserLdap--`을(를) 값으로 입력하고 비교 매개 변수를 **포함**(으)로 설정한 다음 **Publish**&#x200B;을(를) 클릭합니다.

![4-05-create-ee-2-brand.png](./images/405createee2brand.png)

이제 대상자가 게시되었습니다.

![4-05-create-ee-2-brand.png](./images/405createee2brand1.png)

다음 단계: [2.4.5 대상 활성화](./ex5.md)

[모듈 2.4로 돌아가기](./segment-activation-microsoft-azure-eventhub.md)

[모든 모듈로 돌아가기](./../../../overview.md)
