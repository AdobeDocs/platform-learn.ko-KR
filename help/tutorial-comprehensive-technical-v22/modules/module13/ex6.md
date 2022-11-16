---
title: Microsoft Azure 이벤트 허브에 세그먼트 활성화 - 작업
description: Microsoft Azure 이벤트 허브에 세그먼트 활성화 - 작업
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 989dd2e4-597b-4b80-8b17-41aa6929ed64
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# 13.6 엔드 투 엔드 시나리오

## 13.6.1 Azure 이벤트 허브 시작 트리거

세그먼트 자격 시 Adobe Experience Platform 실시간 CDP에서 Azure 이벤트 허브로 보내는 페이로드를 표시하려면 간단한 Azure 이벤트 허브 트리거 기능을 시작해야 합니다. 이 함수는 Visual Studio 코드에서 콘솔에 페이로드를 &quot;덤프&quot;합니다. 그러나 이 함수는 전용 API 및 프로토콜을 사용하여 모든 유형의 환경과 인터페이스로 확장될 수 있습니다.

### Visual Studio 코드 시작 및 프로젝트 시작

Visual Studio 코드 프로젝트를 열고 실행해야 합니다

Visual Studio 코드에서 Azure 함수를 시작/중지/다시 시작하려면 다음 연습을 참조하십시오.

- [연습 13.5.4 - Azure 프로젝트 시작](./ex5.md)
- [연습 13.5.5 - Azure 프로젝트 중지](./ex5.md)

Visual Studio 코드 **터미널** 다음과 유사한 것을 언급해야 합니다.

```code
[2022-02-23T05:03:41.429Z] Worker process started and initialized.
[2022-02-23T05:03:41.484Z] Debugger attached.
[2022-02-23T05:03:46.401Z] Host lock lease acquired by instance ID '000000000000000000000000D90C881B'.
```

![6-01-vsc-ready.png](./images/vsc31.png)

## 13.6.2 Luma 웹 사이트 로드

이동 [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Adobe ID으로 로그인하면 다음이 표시됩니다. 웹 사이트 프로젝트를 클릭하여 엽니다.

![DSN](../module0/images/web8.png)

이제 아래 흐름을 따라 웹 사이트에 액세스할 수 있습니다. 클릭 **통합**.

![DSN](../module0/images/web1.png)

설정 **통합** 페이지에서 연습 0.1에서 생성된 데이터 수집 속성을 선택해야 합니다.

![DSN](../module0/images/web2.png)

그러면 데모 웹 사이트가 열립니다. URL을 선택하고 클립보드에 복사합니다.

![DSN](../module0/images/web3.png)

새 시크릿 브라우저 창을 엽니다.

![DSN](../module0/images/web4.png)

이전 단계에서 복사한 데모 웹 사이트의 URL을 붙여넣습니다. 그런 다음 Adobe ID을 사용하여 로그인하라는 메시지가 표시됩니다.

![DSN](../module0/images/web5.png)

계정 유형을 선택하고 로그인 프로세스를 완료합니다.

![DSN](../module0/images/web6.png)

그러면 시크릿 브라우저 창에서 로드되는 웹 사이트가 표시됩니다. 모든 데모에서는 신선하고 시크릿 브라우저 창을 사용하여 데모 웹 사이트 URL을 로드해야 합니다.

![DSN](../module0/images/web7.png)

## 13.6.3 장비 세그먼트에 대한 관심 자격 부여

로 이동합니다 **장비** 한 번, 및 **다시 로드하거나 새로 고치지 않습니다**. 이 작업을 수행하면 `--demoProfileLdap-- - Interest in Equipment` 세그먼트.

![6-04-luma-telco-nav-sports.png](./images/luma1.png)

확인하려면 프로필 뷰어 패널을 엽니다. 이제 다음을 수행할 수 있습니다 `--demoProfileLdap-- - Interest in Equipment`. 세그먼트 멤버십이 프로필 뷰어 패널에서 아직 업데이트되지 않은 경우 다시 로드 단추를 클릭합니다.

![6-05-luma-telco-nav-broadband.png](./images/luma2.png)

Visual Studio 코드로 돌아가서 **터미널** 탭에서 특정 세그먼트의 목록을 볼 수 있습니다 **ECID**. 이 활성화 페이로드는 자격이 되는 즉시 이벤트 허브에 전달됩니다 `--demoProfileLdap-- - Interest in Equipment` 세그먼트.

세그먼트 페이로드를 자세히 보면 다음을 확인할 수 있습니다 `--demoProfileLdap-- - Interest in Equipment` 이(가) 상태입니다. **실현**.

의 세그먼트 상태 **실현** 은(는) 프로필이 방금 세그먼트에 들어갔음을 의미합니다. 반면에 **기존** 상태는 프로필이 세그먼트에 계속 있음을 의미합니다.

![6-06-vsc-activation-realized.png](./images/luma3.png)

## 13.6.4 두 번째로 장비 페이지 방문

하드 새로 고침 **장비** 페이지.

![6-07-back-to-sports.png](./images/luma1.png)

이제 Visual Studio 코드로 돌아가서 다음을 확인합니다 **터미널** 탭. 세그먼트가 여전히 있지만 현재 상태임을 알 수 있습니다 **기존** 즉, 프로필이 계속 세그먼트에 있을 것입니다.

![6-08-vsc-activation-existing.png](./images/luma4.png)

## 13.6.5 스포츠 페이지를 세 번째로 방문

만약 **스포츠** 세그먼트 POV에서 상태가 변경되지 않으므로 세 번째로 페이지가 활성화되지 않습니다.

세그먼트 활동은 세그먼트의 상태가 변경될 때만 발생합니다.

![6-09-segment-state-change.png](./images/6-09-segment-state-change.png)

다음 단계: [요약 및 이점](./summary.md)

[모듈 13으로 돌아가기](./segment-activation-microsoft-azure-eventhub.md)

[모든 모듈로 돌아가기](./../../overview.md)
