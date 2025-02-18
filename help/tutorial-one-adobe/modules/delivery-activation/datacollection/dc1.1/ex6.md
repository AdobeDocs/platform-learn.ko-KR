---
title: 기초 - Adobe Experience Platform 데이터 수집 및 웹 SDK 확장 설정 - Adobe Target 구현
description: 기초 - Adobe Experience Platform 데이터 수집 및 웹 SDK 확장 설정 - Adobe Target 구현
kt: 5342
doc-type: tutorial
exl-id: 31cdde2f-011d-442d-8e47-15a318a6c89d
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 2%

---

# 1.1.6 Adobe Target 구현

## Adobe Target을 사용하도록 데이터 스트림 업데이트

웹 SDK에서 수집한 데이터를 Adobe Target으로 보내고 모든 고객을 위한 개인화된 경험으로 Adobe Target에서 응답을 받으려면 다음 단계를 따르십시오.

[https://experience.adobe.com/launch/](https://experience.adobe.com/launch/)(으)로 이동한 다음 **데이터스트림**(으)로 이동합니다.

화면 오른쪽 상단에서 샌드박스 이름을 선택합니다. 이름은 `--aepSandboxName--`이어야 합니다. 이름이 `--aepUserLdap-- - Demo System Datastream`인 특정 데이터 스트림을 엽니다.

![왼쪽 탐색에서 Edge 구성 아이콘을 클릭합니다](./images/edgeconfig1b.png)

그러면 이걸 보게 될 거야. Adobe Target을 사용하려면 **서비스 추가**&#x200B;를 클릭하세요.

![AEP 디버거](./images/aa2.png)

그러면 이걸 보게 될 거야. **Adobe Target** 서비스를 선택한 후 선택적으로 추가 정보를 제공할 수 있습니다. **저장**&#x200B;을 클릭합니다.

![AEP 디버거](./images/at1.png)

## 다음 단계

Adobe Experience Platform의 [1.1.7 XDM 스키마 요구 사항으로 이동](./ex7.md){target="_blank"}

[Adobe Experience Platform 데이터 수집 및 웹 SDK 태그 확장 설정으로 돌아가기](./data-ingestion-launch-web-sdk.md){target="_blank"}

[모든 모듈](./../../../../overview.md){target="_blank"}(으)로 돌아가기
