---
title: Microsoft Azure 이벤트 허브에 세그먼트 활성화 - 세그먼트 활성화
description: Microsoft Azure 이벤트 허브에 세그먼트 활성화 - 세그먼트 활성화
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 250f8536-b6bd-4c64-a552-80d5c6fb6358
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 2%

---

# 13.4 세그먼트 활성화

## 13.4.1 Azure 이벤트 허브 대상에 세그먼트 추가

이 연습에서는 세그먼트를 추가합니다 `--demoProfileLdap-- - Interest in Equipment` 아래와 같이 `--demoProfileLdap---aep-enablement` Azure 이벤트 허브 대상.

다음 URL로 이동하여 Adobe Experience Platform에 로그인합니다. [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

로그인하면 Adobe Experience Platform 홈 페이지가 표시됩니다.

![데이터 수집](../module2/images/home.png)

계속하기 전에 **샌드박스**. 선택할 샌드박스의 이름은 다음과 같습니다 ``--aepSandboxId--``. 이 작업은 텍스트를 클릭하여 수행할 수 있습니다 **[!UICONTROL 프로덕션 제품]** 화면 상단에 있는 파란색 줄에 표시됩니다. 적절한 샌드박스를 선택하면 화면 변경 사항이 표시되고 이제 전용 샌드박스에 있습니다.

![데이터 수집](../module2/images/sb1.png)

이동 **대상**&#x200B;를 클릭한 다음 **찾아보기**. 그러면 사용 가능한 모든 대상이 표시됩니다. 대상을 찾아 **+** 아래에 표시된 아이콘입니다.

![5-01-select-destination.png](./images/5-01-select-destination.png)

그러면 이게 보입니다. ldap를 사용하여 세그먼트를 검색하고 선택합니다. `--demoProfileLdap-- - Interest in Equipment` 세그먼트 목록 아래에 그룹화됩니다.

**다음**&#x200B;을 클릭합니다.

![5-04-select-segment.png](./images/5-04-select-segment.png)

Adobe Experience Platform 실시간 CDP는 세그먼트 대상 및 프로필 대상, 이렇게 두 가지 유형의 대상에 페이로드를 제공할 수 있습니다.

세그먼트 대상은 나중에 논의될 사전 정의된 세그먼트 자격 페이로드를 수신하게 됩니다. 이러한 페이로드는 을 포함합니다 **모두** 특정 프로필에 대한 세그먼트 자격. 대상이 아닌 세그먼트의 활성화 목록에 없는 세그먼트의 경우에도. 이러한 세그먼트 대상의 예는 다음과 같습니다 **Azure 이벤트 허브** 및 **AWS Kinesis**.

프로필 기반 대상을 사용하면 XDM 프로필 결합 스키마에서 속성(firstName, lastName, ...)을 선택하여 활성화 페이로드에 포함할 수 있습니다. 이러한 대상의 예는 입니다 **이메일 마케팅**.

Azure 이벤트 허브 대상이 **세그먼트** 대상, 필드 예를 들면 을 선택합니다 `--aepTenantId--.identification.core.ecid`.

클릭 **새 필드 추가**&#x200B;를 클릭하고 스키마 찾아보기 를 클릭한 다음 필드를 선택합니다 `--aepTenantId--identification.core.ecid` (자동으로 표시되는 다른 필드는 모두 삭제합니다.)

**다음**&#x200B;을 클릭합니다.

![5-05-select-attributes.png](./images/5-05-select-attributes.png)

**마침을 클릭합니다**.

![5-06-destination-finish.png](./images/5-06-destination-finish.png)

이제 세그먼트가 Microsoft 이벤트 허브 대상 방향으로 활성화됩니다.

![5-07-destination-segment-added.png](./images/5-07-destination-segment-added.png)

다음 단계: [13.5 Microsoft Azure 프로젝트 만들기](./ex5.md)

[모듈 13으로 돌아가기](./segment-activation-microsoft-azure-eventhub.md)

[모든 모듈로 돌아가기](./../../overview.md)
