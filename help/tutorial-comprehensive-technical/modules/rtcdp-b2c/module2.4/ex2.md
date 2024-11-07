---
title: Microsoft Azure 이벤트 허브에 대한 세그먼트 활성화 - Adobe Experience Platform에서 이벤트 허브 RTCDP 대상 설정
description: Microsoft Azure 이벤트 허브에 대한 세그먼트 활성화 - Adobe Experience Platform에서 이벤트 허브 RTCDP 대상 설정
kt: 5342
doc-type: tutorial
source-git-commit: c6ba1f751f18afe39fb6b746a62bc848fa8ec9bf
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---

# 2.4.2 Adobe Experience Platform에서 Azure Event Hub 대상 구성

## 2.4.2.1 필요한 Azure 연결 매개 변수 식별

Adobe Experience Platform에서 이벤트 허브 대상을 정의하려면 다음을 수행해야 합니다.

- 이벤트 허브 네임스페이스
- 이벤트 허브
- Azure SAS 키 이름
- Azure SAS 키

이전 연습에서 이벤트 허브 및 EventHub 네임스페이스를 정의했습니다. [연습 1 - Azure에서 이벤트 허브 설정](./ex1.md)

### 이벤트 허브 네임스페이스

Azure 포털에서 위의 정보를 조회하려면 [https://portal.azure.com/#home](https://portal.azure.com/#home)(으)로 이동합니다. 올바른 Azure 계정을 사용하고 있는지 확인하세요.

Azure 포털에서 **모든 리소스** 선택:

![2-01-azure-all-resources.png](./images/2-01-azure-all-resources.png)

### 이벤트 허브

리소스 유형이 **이벤트 허브 네임스페이스**&#x200B;인 리소스를 찾으십시오. 이전 연습에서 사용된 명명 규칙을 따랐으면 이벤트 허브 네임스페이스는 `--demoProfileLdap---aep-enablement`이(가) 됩니다. 기록해 두십시오. 다음 연습에서 필요할 것입니다.

![2-02-select-event-hubs-namespace.png](./images/2-02-select-event-hubs-namespace.png)

이벤트 허브 네임스페이스 이름을 클릭하여 자세한 내용을 확인합니다.

![2-03-select-event-hub.png](./images/2-03-select-event-hub.png)

**이벤트 허브**&#x200B;를 선택하여 이벤트 허브 네임스페이스에 정의된 이벤트 허브 목록을 가져옵니다. 이전 연습에서 사용한 이름 지정 규칙을 따랐으면 `--demoProfileLdap---aep-enablement-event-hub`(이)라는 이벤트 허브를 찾을 수 있습니다. 기록해 두십시오. 다음 연습에서 필요할 것입니다.

![2-04-event-hub-selected.png](./images/2-04-event-hub-selected.png)

### SAS 키 이름

**이벤트 허브 네임스페이스**&#x200B;에 대해 **공유 액세스 정책**&#x200B;을(를) 선택하십시오.

![2-05-select-sas.png](./images/2-05-select-sas.png)

공유 액세스 정책 목록이 표시됩니다. 찾고 있는 SAS 키는 **RootManageSharedAccessKey**&#x200B;입니다. SAS 키 이름입니다. 적어 주세요.

![2-06-sas-overview.png](./images/2-06-sas-overview.png)

### SAS 키 값

SAS 키 값을 가져오려면 **RootManageSharedAccessKey**&#x200B;을(를) 클릭합니다. **클립보드에 복사** 아이콘을 눌러 **기본 키**&#x200B;를 복사합니다.

![2-07-sas-key-value.png](./images/2-07-sas-key-value.png)

### 대상 값 요약

이 시점에서 Adobe Experience Platform Real-time CDP에서 Azure Event Hub 대상을 정의하는 데 필요한 모든 값을 식별했어야 합니다.

| 대상 속성 이름 | 대상 속성 값 | 예제 값 |
|---|---|---|
| sasKeyName | SAS 키 이름 | RootManageSharedAccessKey |
| sasKey | SAS 키 값 | srREx9ShJG1Rv7f/... |
| 네임스페이스 | 이벤트 허브 네임스페이스 | `--demoProfileLdap---aep-enablement` |
| 이벤트 허브 이름 | 이벤트 허브 | `--demoProfileLdap---aep-enablement-event-hub` |

## 2.4.2.2 Adobe Experience Platform에서 Azure Event Hub 대상 만들기

URL [https://experience.adobe.com/platform](https://experience.adobe.com/platform)로 이동하여 Adobe Experience Platform에 로그인합니다.

로그인하면 Adobe Experience Platform 홈페이지에 접속하게 됩니다.

![데이터 수집](./../../../modules/datacollection/module1.2/images/home.png)

계속하려면 **샌드박스**&#x200B;를 선택해야 합니다. 선택할 샌드박스 이름이 ``--aepSandboxId--``입니다. 화면 상단의 파란색 선에 있는 텍스트 **[!UICONTROL 프로덕션]**&#x200B;을(를) 클릭하면 됩니다. 적절한 샌드박스를 선택하면 화면이 변경되고 이제 전용 샌드박스에 있습니다.

![데이터 수집](./../../../modules/datacollection/module1.2/images/sb1.png)

**대상**(으)로 이동한 다음 **카탈로그**(으)로 이동합니다.

![데이터 수집](./images/sb2a.png)

**클라우드 저장소**&#x200B;를 선택하고 **Azure Event Hubs**(으)로 이동한 다음 **설정** 또는 **구성**&#x200B;을 클릭합니다.

![2-08-list-destinations.png](./images/2-08-list-destinations.png)

이전 연습에서 수집한 대상 값을 입력합니다. **대상에 연결**&#x200B;을 클릭합니다.

![2-09-destination-values.png](./images/2-09-destination-values.png)

자격 증명이 올바르면 **연결됨**&#x200B;이 표시됩니다.

![2-09-destination-values.png](./images/2-09-destination-valuesa.png)

이제 `--demoProfileLdap---aep-enablement` 형식으로 이름과 설명을 입력해야 합니다. **eventHubName**&#x200B;을(를) 입력하고(이전 연습 참조, `--demoProfileLdap---aep-enablement-event-hub` 모양) **다음**&#x200B;을(를) 클릭합니다.

![2-10-create-destination.png](./images/2-10-create-destination.png)

**저장 및 종료**&#x200B;를 클릭합니다.

![2-11-save-exit-activation.png](./images/2-11-save-exit-activation.png)

이제 대상이 만들어지고 Adobe Experience Platform에서 사용할 수 있습니다.

![2-12-destination-created.png](./images/2-12-destination-created.png)

다음 단계: [2.4.3 세그먼트 만들기](./ex3.md)

[모듈 2.4로 돌아가기](./segment-activation-microsoft-azure-eventhub.md)

[모든 모듈로 돌아가기](./../../../overview.md)
