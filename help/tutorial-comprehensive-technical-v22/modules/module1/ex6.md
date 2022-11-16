---
title: Foundation - Adobe Experience Platform 데이터 수집 및 웹 SDK 확장 설정 - Adobe Target 구현
description: Foundation - Adobe Experience Platform 데이터 수집 및 웹 SDK 확장 설정 - Adobe Target 구현
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 4aee8ae2-38ca-49a3-8f1b-57713d16f5b5
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# 1.6 Adobe Target 구현

## 1.6. Adobe Target을 사용하도록 데이터 스트림을 업데이트합니다

Web SDK로 수집한 데이터를 Adobe Target에 보내고 모든 고객을 위한 개인화된 경험과 함께 Adobe Target의 응답을 받으려면 다음 단계를 따르십시오.

이동 [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) 그리고 **데이터 스트림**.

화면의 오른쪽 상단 모서리에서 샌드박스 이름을 선택합니다. 샌드박스 이름은 다음과 같습니다. `--aepSandboxId--`. 이름이 인 특정 데이터 스트림을 엽니다 `--demoProfileLdap-- - Demo System Datastream`.

![왼쪽 탐색에서 Edge Configuration 아이콘을 클릭합니다](./images/edgeconfig1b.png)

그러면 이게 보입니다. Adobe Target을 활성화하려면 **+서비스 추가**.

![AEP Debugger](./images/aa2.png)

그러면 이게 보입니다. 서비스를 선택합니다 **Adobe Target**&#x200B;를 입력하면 추가 정보를 선택적으로 제공할 수 있습니다. 지금은 저장할 필요가 없으므로 **취소**.

![AEP Debugger](./images/at1.png)

다음 단계: [Adobe Experience Platform의 1.7 XDM 스키마 요구 사항](./ex7.md)

[모듈 1로 돌아가기](./data-ingestion-launch-web-sdk.md)

[모든 모듈로 돌아가기](./../../overview.md)
