---
title: Microsoft Azure 이벤트 허브에 대한 세그먼트 활성화 - 세그먼트 활성화
description: Microsoft Azure 이벤트 허브에 대한 세그먼트 활성화 - 세그먼트 활성화
kt: 5342
doc-type: tutorial
source-git-commit: cd603fdcbac6cc77b00d50be888805329f014443
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 1%

---

# 2.4.4 세그먼트 활성화

## 2.4.4.1 Azure 이벤트 허브 대상에 세그먼트 추가

이 연습에서는 `--demoProfileLdap-- - Interest in Equipment` 세그먼트를 `--demoProfileLdap---aep-enablement` Azure Event Hub 대상에 추가합니다.

URL [https://experience.adobe.com/platform](https://experience.adobe.com/platform)로 이동하여 Adobe Experience Platform에 로그인합니다.

로그인하면 Adobe Experience Platform 홈페이지에 접속하게 됩니다.

![데이터 수집](./../../../modules/datacollection/module1.2/images/home.png)

계속하려면 **샌드박스**&#x200B;를 선택해야 합니다. 선택할 샌드박스 이름이 ``--aepSandboxId--``입니다. 화면 상단의 파란색 선에 있는 텍스트 **[!UICONTROL 프로덕션]**&#x200B;을(를) 클릭하면 됩니다. 적절한 샌드박스를 선택하면 화면이 변경되고 이제 전용 샌드박스에 있습니다.

![데이터 수집](./../../../modules/datacollection/module1.2/images/sb1.png)

**대상**(으)로 이동한 다음 **찾아보기**&#x200B;를 클릭합니다. 그러면 사용 가능한 모든 대상을 볼 수 있습니다. 대상을 찾고 아래 표시된 대로 **+** 아이콘을 클릭합니다.

![5-01-select-destination.png](./images/5-01-select-destination.png)

그러면 이걸 보게 될 거야. ldap를 사용하여 세그먼트를 검색하고 세그먼트 목록에서 `--demoProfileLdap-- - Interest in Equipment`을(를) 선택합니다.

**다음**&#x200B;을 클릭합니다.

![5-04-select-segment.png](./images/5-04-select-segment.png)

Adobe Experience Platform Real-time CDP는 두 가지 유형의 대상, 세그먼트 대상 및 프로필 대상에 페이로드를 제공할 수 있습니다.

세그먼트 대상은 나중에 설명하는 사전 정의된 세그먼트 자격 페이로드를 받습니다. 이러한 페이로드에는 특정 프로필에 대한 세그먼트 자격 **모두**&#x200B;이(가) 포함되어 있습니다. 대상 의 활성화 목록에 없는 세그먼트의 경우에도 마찬가지입니다. 이러한 세그먼트 대상의 예로는 **Azure Event Hubs** 및 **AWS Kinesis**&#x200B;이 있습니다.

프로필 기반 대상을 사용하면 XDM 프로필 통합 스키마에서 속성(firstName, lastName, ...)을 선택하여 활성화 페이로드에 포함할 수 있습니다. 이러한 대상의 예로는 **이메일 마케팅**&#x200B;이 있습니다.

Azure Event Hub 대상이 **세그먼트** 대상이므로 필드 `--aepTenantId--.identification.core.ecid`을(를) 선택하십시오.

**새 필드 추가**&#x200B;를 클릭하고 스키마 찾아보기를 클릭한 다음 `--aepTenantId--identification.core.ecid` 필드를 선택합니다(자동으로 표시되는 다른 필드 삭제).

**다음**&#x200B;을 클릭합니다.

![5-05-select-attributes.png](./images/5-05-select-attributes.png)

**마침을 클릭합니다**.

![5-06-destination-finish.png](./images/5-06-destination-finish.png)

이제 세그먼트가 Microsoft 이벤트 허브 대상에 대해 활성화됩니다.

![5-07-destination-segment-added.png](./images/5-07-destination-segment-added.png)

다음 단계: [2.4.5 Microsoft Azure 프로젝트 만들기](./ex5.md)

[모듈 2.4로 돌아가기](./segment-activation-microsoft-azure-eventhub.md)

[모든 모듈로 돌아가기](./../../../overview.md)
