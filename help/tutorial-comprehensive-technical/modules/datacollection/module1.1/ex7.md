---
title: 기초 - Adobe Experience Platform 데이터 수집 및 웹 SDK 확장 설정 - Adobe Experience Platform의 XDM 스키마 요구 사항
description: 기초 - Adobe Experience Platform 데이터 수집 및 웹 SDK 확장 설정 - Adobe Experience Platform의 XDM 스키마 요구 사항
kt: 5342
doc-type: tutorial
exl-id: 3fc4a1d6-4130-464e-98c0-5b9cac8051a0
source-git-commit: 1526661a80b4d551627dfca42a7e97c9498dd1f2
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# Adobe Experience Platform의 1.1.7 XDM 스키마 요구 사항

웹 SDK에서 Adobe Experience Platform으로 데이터를 수집할 수 있도록 하려면 Adobe Experience Platform에서 특정 XDM mixin이 XDM 스키마의 일부가 되어야 합니다.

[https://experience.adobe.com/platform](https://experience.adobe.com/platform)(으)로 이동하여 로그인합니다.

![AEP 디버거](./images/exp1.png)

로그인 후 화면 상단의 파란색 선에 있는 텍스트 **프로덕션**&#x200B;을(를) 클릭하여 적절한 샌드박스를 선택합니다. 샌드박스 `--aepSandboxName--`을(를) 선택하십시오.

샌드박스를 선택하면 화면이 변경되고 이제 샌드박스에 있습니다.

![AEP 디버거](./images/exp2.png)

왼쪽 메뉴에서 **스키마**(으)로 이동하여 **데모 시스템 - 웹 사이트에 대한 이벤트 스키마(전역 v1.1)** 스키마를 엽니다.

![AEP 디버거](./images/exp3.png)

해당 스키마에서 필드 그룹 **AEP 웹 SDK ExperienceEvent** 필드 그룹이 추가되었습니다. 이 필드 그룹은 스키마에 최소 필수 필드를 모두 추가합니다. Web SDK에서 사용할 Adobe Experience Platform의 모든 경험 이벤트 스키마에서는 항상 해당 필드 그룹이 스키마의 일부가 되어야 합니다.

![AEP 디버거](./images/exp4.png)

[모듈 1.2](./../module1.2/data-ingestion.md)에서 스키마에 필드 그룹을 추가하는 방법을 배웁니다.

다음 단계: [요약 및 이점](./summary.md)

[모듈 1.1로 돌아가기](./data-ingestion-launch-web-sdk.md)

[모든 모듈로 돌아가기](./../../../overview.md)
