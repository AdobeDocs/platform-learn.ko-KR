---
title: Microsoft Azure 이벤트 허브에 대한 세그먼트 활성화 - 작업
description: Microsoft Azure 이벤트 허브에 대한 세그먼트 활성화 - 작업
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# 2.4.6 전체 시나리오

## 2.4.6.1 Azure 이벤트 허브 트리거 시작

세그먼트 자격 조건 시 Adobe Experience Platform Real-time CDP에서 Azure Event Hub로 보내는 페이로드를 표시하려면 간단한 Azure Event Hub 트리거 기능을 시작해야 합니다. 이 함수는 Visual Studio 코드의 콘솔에 페이로드를 &quot;덤프&quot;합니다. 그러나 이 함수는 전용 API 및 프로토콜을 사용하여 모든 종류의 환경과 상호 작용할 수 있도록 어떤 방식으로든 확장할 수 있습니다.

### Visual Studio 코드를 시작하고 프로젝트를 시작합니다.

Visual Studio 코드 프로젝트가 열려 있고 실행 중인지 확인합니다.

Visual Studio 코드에서 Azure 함수를 시작/중지/다시 시작하려면 다음 연습을 참조하십시오.

- [연습 13.5.4 - Azure 프로젝트 시작](./ex5.md)
- [연습 13.5.5 - Azure 프로젝트 중지](./ex5.md)

Visual Studio 코드의 **터미널**&#x200B;에서는 다음과 유사한 내용을 언급해야 합니다.

```code
[2022-02-23T05:03:41.429Z] Worker process started and initialized.
[2022-02-23T05:03:41.484Z] Debugger attached.
[2022-02-23T05:03:46.401Z] Host lock lease acquired by instance ID '000000000000000000000000D90C881B'.
```

![6-01-vsc-ready.png](./images/vsc31.png)

## 2.4.6.2 Luma 웹 사이트 로드

[https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects)(으)로 이동합니다. Adobe ID으로 로그인하면 이 메시지가 표시됩니다. 웹 사이트 프로젝트를 클릭하여 엽니다.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

이제 아래 흐름을 따라 웹 사이트에 액세스할 수 있습니다. **통합**&#x200B;을 클릭합니다.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web1.png)

**통합** 페이지에서 연습 0.1에서 만든 데이터 수집 속성을 선택해야 합니다.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web2.png)

그러면 데모 웹 사이트가 열리는 것을 볼 수 있습니다. URL을 선택하고 클립보드에 복사합니다.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web3.png)

새 시크릿 브라우저 창을 엽니다.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web4.png)

이전 단계에서 복사한 데모 웹 사이트의 URL을 붙여 넣습니다. 그런 다음 Adobe ID을 사용하여 로그인하라는 메시지가 표시됩니다.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web5.png)

계정 유형을 선택하고 로그인 프로세스를 완료합니다.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web6.png)

그러면 웹 사이트가 시크릿 브라우저 창에 로드되는 것을 볼 수 있습니다. 모든 데모에 대해 새로운 시크릿 브라우저 창을 사용하여 데모 웹 사이트 URL을 로드해야 합니다.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web7.png)

## 2.4.6.3 장비 세그먼트에 대한 관심 부문에 적합

**장비** 페이지로 한 번 이동한 다음 **다시 로드하거나 새로 고치지 않음**&#x200B;합니다. 이 작업은 `--aepUserLdap-- - Interest in Equipment` 세그먼트에 대한 자격을 부여해야 합니다.

![6-04-luma-telco-nav-sports.png](./images/luma1.png)

확인하려면 프로필 뷰어 패널을 엽니다. 이제 `--aepUserLdap-- - Interest in Equipment`의 멤버여야 합니다. 세그먼트 멤버십이 프로필 뷰어 패널에서 아직 업데이트되지 않은 경우 다시 로드 단추를 클릭합니다.

![6-05-luma-telco-nav-broadband.png](./images/luma2.png)

Visual Studio 코드로 다시 전환하고 **TERMINAL** 탭을 보면 특정 **ECID**&#x200B;에 대한 세그먼트 목록이 표시됩니다. 이 활성화 페이로드는 `--aepUserLdap-- - Interest in Equipment` 세그먼트에 대한 자격이 되는 즉시 이벤트 허브에 전달됩니다.

세그먼트 페이로드를 자세히 살펴보면 `--aepUserLdap-- - Interest in Equipment`이(가) **실현됨** 상태입니다.

세그먼트 상태가 **실현됨**&#x200B;이면 프로필이 세그먼트에 방금 들어왔다는 것을 의미합니다. **existing** 상태는 프로필이 계속 세그먼트에 있음을 의미합니다.

![6-06-vsc-activation-improved.png](./images/luma3.png)

## 2.4.6.4 두 번째로 장비 페이지 방문

**장비** 페이지를 하드 새로 고치십시오.

![6-07-back-to-sports.png](./images/luma1.png)

이제 Visual Studio 코드로 다시 전환하여 **TERMINAL** 탭을 확인합니다. 아직 세그먼트가 있지만 현재 **existing** 상태입니다. 즉, 프로필은 계속 세그먼트에 있습니다.

![6-08-vsc-activation-existing.png](./images/luma4.png)

## 2.4.6.5 세 번째로 스포츠 페이지 방문

**스포츠** 페이지를 세 번째로 다시 방문하는 경우 세그먼트 관점에서 상태가 변경되지 않으므로 활성화가 수행되지 않습니다.

세그먼트 활성화는 세그먼트의 상태가 변경되는 경우에만 발생합니다.

![6-09-segment-state-change.png](./images/6-09-segment-state-change.png)

다음 단계: [요약 및 이점](./summary.md)

[모듈 2.4로 돌아가기](./segment-activation-microsoft-azure-eventhub.md)

[모든 모듈로 돌아가기](./../../../overview.md)
