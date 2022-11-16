---
title: Microsoft Azure 이벤트 허브에 세그먼트 활성화 - 요약 및 이점
description: Microsoft Azure 이벤트 허브에 세그먼트 활성화 - 요약 및 이점
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 2174ac52-b5dd-4bc8-ab5f-4d84ae9ef19b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 1%

---

# 요약 및 이점

Microsoft Azure Event Hub 및 Adobe Experience Platform에 대해 학습하는 데 시간을 할애해 주셔서 감사합니다!
이 단원에서는 Azure 이벤트 허브 인스턴스를 설정하는 방법과 Adobe Experience Platform에 연결하는 방법을 배웁니다.

## 이점

Adobe Experience Platform과 Microsoft Azure 이벤트 허브를 통합함으로써 얻을 수 있는 이점을 강조하겠습니다.

- Microsoft Azure 이벤트 허브를 Adobe Experience Platform 대상으로 사용하면 실시간으로 세그먼트 자격을 캡처하고 Azure 이벤트 허브 함수를 사용하여 처리할 수 있습니다. 이러한 Azure 이벤트 허브 기능을 사용하면 모든 종류의 사용자 지정 세그먼트 활성화 핸들러를 빌드하고 이러한 종류의 타사 대상을 통합할 수 있습니다.

- 대상은 지정된 세그먼트에서만 트리거되지만 활성화 페이로드에는 해당 프로필이 자격을 주는 모든 세그먼트가 포함됩니다.

- 세그먼트는 상태가 변경될 때만 활성화를 트리거합니다. 예를 들어 3개월 동안 한 세그먼트에 대해 4번 자격을 부여하는 프로필은 처음 두 개만 활성화됩니다. 첫 번째는 에서 로 상태 변경 **실현**&#x200B;두 번째 변수는 의 상태 변경에 의해 트리거됩니다. **실현** to **기존**.

- 알려진 프로필에 대해 세그먼트를 활성화하면 전체 ID 맵이 활성화 페이로드에 포함됩니다. Azure 함수는 응용 프로그램의 고객 식별자를 사용하는 동안 사용 가능한 ID를 사용하여 세그먼트를 타사 애플리케이션에서 관리하는 프로필에 매핑할 수 있습니다.

- 이 모듈에서 이벤트 허브 함수를 로컬로 배포하여(Visual Studio 코드의 디버그 모드) 많은 문제 해결 및 디버그 옵션을 제공합니다.

## 체크 아웃

- 해당 없음

[모듈 13으로 돌아가기](./segment-activation-microsoft-azure-eventhub.md)

[모든 모듈로 돌아가기](./../../overview.md)
