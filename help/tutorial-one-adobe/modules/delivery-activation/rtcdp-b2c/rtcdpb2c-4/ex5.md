---
title: Audience Activation에서 Microsoft Azure Event Hub로 - 대상 활성화
description: Audience Activation에서 Microsoft Azure Event Hub로 - 대상 활성화
kt: 5342
doc-type: tutorial
exl-id: e6bac0ce-4a1e-4458-af3e-3d6ac40b9cb5
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 3%

---

# 2.4.5 대상자 활성화

## Azure 이벤트 허브 대상에 대상 추가

이 연습에서는 대상 `--aepUserLdap-- - Interest in Plans`을(를) `--aepUserLdap---aep-enablement` Azure Event Hub 대상에 추가합니다.

URL [https://experience.adobe.com/platform](https://experience.adobe.com/platform)로 이동하여 Adobe Experience Platform에 로그인합니다.

로그인하면 Adobe Experience Platform 홈페이지에 접속하게 됩니다.

![데이터 수집](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

계속하려면 **샌드박스**&#x200B;를 선택해야 합니다. 선택할 샌드박스 이름이 ``--aepSandboxName--``입니다. 적절한 샌드박스를 선택하면 화면이 변경되고 이제 전용 샌드박스에 있습니다.

![데이터 수집](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

**대상**(으)로 이동한 다음 **찾아보기**&#x200B;를 클릭합니다. 그러면 사용 가능한 모든 대상을 볼 수 있습니다. 대상을 찾고 아래 표시된 대로 세 점**..**을 클릭한 다음 **대상 활성화**&#x200B;를 클릭합니다.

![5-01-select-destination.png](./images/501selectdestination.png)

그러면 이걸 보게 될 거야. LDAP를 사용하여 대상자를 검색하고 대상자 목록에서 `--aepUserLdap-- - Interest in Plans`을(를) 선택합니다.

**다음**&#x200B;을 클릭합니다.

![5-04-select-segment.png](./images/504selectsegment.png)

**새 필드 추가**&#x200B;를 클릭하고 스키마 찾아보기를 클릭한 다음 `--aepTenantId--identification.core.ecid` 필드를 선택합니다(자동으로 표시되는 다른 필드 삭제).

**다음**&#x200B;을 클릭합니다.

![5-05-select-attributes.png](./images/505selectattributes.png)

**마침을 클릭합니다**.

![5-06-destination-finish.png](./images/506destinationfinish.png)

이제 대상자가 Microsoft 이벤트 허브 대상에 대해 활성화됩니다.

![5-07-destination-segment-added.png](./images/507destinationsegmentadded.png)

## 다음 단계

[2.4.6 Microsoft Azure 프로젝트 만들기](./ex6.md){target="_blank"}(으)로 이동

[Real-Time CDP: Audience Activation에서 Microsoft Azure Event Hub로 이동](./segment-activation-microsoft-azure-eventhub.md){target="_blank"}

[모든 모듈](./../../../../overview.md){target="_blank"}(으)로 돌아가기
