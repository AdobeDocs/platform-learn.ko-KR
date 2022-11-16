---
title: 콜 센터에서 실시간 고객 프로필 활용 사례 보기
description: 콜 센터에서 실시간 고객 프로필 활용 사례 보기
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 457347ca-1ce5-4699-bd30-735abdc7b450
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 3%

---

# 3.6 콜 센터에서 실시간 고객 프로필 활용 사례 보기

이 연습에서 목표는 고객 여정을 살펴보고 실제 고객처럼 행동하도록 하는 것입니다.

이 웹 사이트에서 Adobe Experience Platform을 구현했습니다. 모든 작업은 경험 이벤트로 간주되며 실시간 고객 프로필을 수화하여 Adobe Experience Platform으로 실시간으로 전송됩니다.

이전에 연습에서는 사이트를 탐색하는 익명의 고객으로 시작했다가 두 가지 단계를 거친 후 알려진 고객이 되었습니다.

같은 고객이 결국 전화를 걸어 콜 센터에 전화하면 다른 채널의 정보를 즉시 사용할 수 있으므로 콜 센터 경험이 연관성 있고 개인화할 수 있습니다.

## 3.6.1 CX 앱 사용

데모 시스템의 일부로 콜 센터 환경을 시뮬레이션하는 데 사용할 수 있는 CX 앱 템플릿을 만들었습니다. 이러한 CX 앱 프로젝트를 생성하려면 다음 단계를 수행합니다.

이동 [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). 클릭 **새 프로젝트**.

그러면 CX 앱 프로젝트가 표시됩니다. 프로젝트를 클릭하여 엽니다.

![데모](./images/cxapp3.png)

CX 앱 프로젝트에서 다음 위치로 이동합니다. **통합**. 모듈 0에서 만든 Adobe Experience Platform 데이터 수집 속성을 선택합니다. 이 있는 속성을 선택해야 합니다 **(지원)** 이름으로. 그런 다음 **실행**.

![데모](./images/cxapp4.png)

그러면 이게 보입니다.

![데모](./images/cxapp5.png)

프로필 뷰어 패널에서는 ID 및 네임스페이스의 조합을 볼 수 있습니다.

![고객 프로필](./images/identities.png)

| 신원 | 네임스페이스 |
|:-------------:| :---------------:|
| ECID(Experience Cloud ID) | 12507560687324495704459439363261812234 |
| 이메일 ID | woutervangeluwe+06022022-01@gmail.com |
| 모바일 번호 ID | +32473622044+06022022-01 |

고객이 콜 센터에 전화하면 전화 번호를 사용하여 고객을 식별할 수 있습니다. 따라서 이 연습에서는 전화 번호를 사용하여 CX 앱에서 고객의 프로필을 검색합니다.

선택 **전화 번호** 드롭다운에서 웹 사이트에서 사용한 전화 번호를 입력합니다. 히트 **Enter 키**.

![데모](./images/19.png)

이제 콜 센터에 이상적으로 표시되는 정보를 볼 수 있으므로, 콜 센터 직원들은 고객과 상담할 때 즉시 모든 관련 정보를 이용할 수 있습니다.

![데모](./images/20.png)

다음 단계: [요약 및 이점](./summary.md)

[모듈 3으로 돌아가기](./real-time-customer-profile.md)

[모든 모듈로 돌아가기](../../overview.md)
