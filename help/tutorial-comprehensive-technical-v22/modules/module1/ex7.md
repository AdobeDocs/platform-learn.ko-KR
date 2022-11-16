---
title: Foundation - Adobe Experience Platform 데이터 수집 및 웹 SDK 확장 설정 - Adobe Experience Platform의 XDM 스키마 요구 사항
description: Foundation - Adobe Experience Platform 데이터 수집 및 웹 SDK 확장 설정 - Adobe Experience Platform의 XDM 스키마 요구 사항
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 8e17129c-633d-45bd-aa70-78cc3d3a2108
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# Adobe Experience Platform의 1.7 XDM 스키마 요구 사항

Web SDK 및 alloy.js에서 데이터를 Adobe Experience Platform에 수집할 수 있도록 Adobe Experience Platform에서 XDM 스키마의 일부로 특정 XDM Mixin이 포함되어야 합니다.

이동 [https://experience.adobe.com/platform](https://experience.adobe.com/platform) 로그인하고

![AEP Debugger](./images/exp1.png)

로그인한 후 텍스트를 클릭하여 적절한 샌드박스를 선택합니다 **프로덕션 제품** 화면 상단에 있는 파란색 줄에 표시됩니다. 샌드박스 선택 `--aepSandboxId--`.

샌드박스를 선택하면 화면 변경 사항이 표시되고 이제 샌드박스에 있습니다.

![AEP Debugger](./images/exp2.png)

왼쪽 메뉴에서 **스키마** 그리고 **데모 시스템 - 웹 사이트용 이벤트 스키마(글로벌 v1.1)** 스키마.

![AEP Debugger](./images/exp3.png)

해당 스키마에서 필드 그룹이 표시됩니다 **AEP 웹 SDK ExperienceEvent Mixin** 이 추가되었습니다. 이 필드 그룹은 스키마에 최소 필수 필드를 모두 추가합니다. 웹 SDK에서 사용할 Adobe Experience Platform의 모든 경험 이벤트 스키마에서는 항상 해당 필드 그룹이 스키마의 일부가 되어야 합니다.

![AEP Debugger](./images/exp4.png)

in [모듈 2](./../module2/data-ingestion.md) 스키마에 필드 그룹을 추가하는 방법을 알아봅니다.

다음 단계: [요약 및 이점](./summary.md)

[모듈 1로 돌아가기](./data-ingestion-launch-web-sdk.md)

[모든 모듈로 돌아가기](./../../overview.md)
