---
title: Audience Activation에서 Microsoft Azure Event Hub로 - 요약 및 이점
description: Audience Activation에서 Microsoft Azure Event Hub로 - 요약 및 이점
kt: 5342
doc-type: tutorial
exl-id: f081af11-3ea0-47cc-ae74-24a0e0231d66
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 1%

---

# 요약 및 이점

Microsoft Azure Event Hub 및 Adobe Experience Platform에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다!
이 모듈에서는 Azure Event Hub 인스턴스를 설정하는 방법과 이를 Adobe Experience Platform에 연결하는 방법을 배웠습니다.

## 이점

Adobe Experience Platform과 Microsoft Azure Event Hub 통합의 이점을 강조하겠습니다.

- Microsoft Azure Event Hubs as a Adobe Experience Platform Destination을 사용하면 대상 자격을 실시간으로 캡처하고 Azure Event Hub 기능을 사용하여 처리할 수 있습니다. 이러한 Azure Event Hub 함수를 사용하여 모든 종류의 사용자 지정 대상 활성화 핸들러를 빌드하고 모든 종류의 타사 대상을 통합할 수 있습니다.

- 대상은 지정된 대상자에 의해서만 트리거되지만, 활성화 페이로드에는 지정된 프로필이 자격을 갖는 모든 대상자가 포함됩니다.

- 대상은 상태가 변경될 때만 활성화를 트리거합니다. 예를 들어 3개월 동안 대상에 대해 4번 자격을 부여하는 프로필의 경우 처음 두 개만 활성화됩니다. 첫 번째 변경 사항은 **실현됨**(으)로의 상태 변경이며 두 번째 변경 사항은 **실현됨**&#x200B;에서 **기존**(으)로의 상태 변경에 의해 트리거됩니다.

- 알려진 프로필에 대해 대상을 활성화하면 전체 ID 맵이 활성화 페이로드에 포함됩니다. Azure 함수는 애플리케이션의 고객 식별자를 사용하는 동안 사용 가능한 ID 중 하나를 사용하여 대상을 타사 애플리케이션에서 관리되는 프로필에 매핑할 수 있습니다.

- 이 모듈에서는 이벤트 허브 함수가 로컬로 배포되어 많은 문제 해결 및 디버그 옵션을 제공합니다(Visual Studio 코드의 디버그 모드).

## 이 항목 확인

- N/A

## 다음 단계

[Real-Time CDP: Audience Activation에서 Microsoft Azure Event Hub로 이동](./segment-activation-microsoft-azure-eventhub.md){target="_blank"}

[모든 모듈](./../../../../overview.md){target="_blank"}(으)로 돌아가기
