---
title: 디버그 | at.js 2.x에서 웹 SDK로 Target 마이그레이션
description: Adobe Experience Platform Web SDK를 사용하여 Adobe Target 구현을 디버깅하는 방법을 알아봅니다. 항목에는 디버깅 옵션, 브라우저 확장, at.js와 Platform Web SDK 간의 차이점이 포함됩니다.
source-git-commit: 63edfc214c678a976fbec20e87e76d33180e61f1
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 3%

---

# Platform Web SDK를 사용하여 Target 디버그

구현, 콘텐츠 전달 또는 대상 자격 문제를 해결하기 위한 Target 활동 확인 및 Web SDK 디버깅 마이그레이션 안내서의 이 페이지에서는 at.js를 사용한 디버깅과 Platform Web SDK의 차이점을 설명합니다.

아래 표에는 테스트 및 디버깅 접근 방식의 기능과 지원이 요약되어 있습니다.

| 기능 또는 도구 | at.js 지원 | Platform Web SDK 지원 |
| --- | --- | --- |
| 활동 QA URL | 예 | 예 |
| `mboxDisable` URL 매개 변수 | 예 | 아래 정보를 참조하여 다음을 수행하십시오. [Target 기능 비활성화](#disable-target-functionality) |
| `mboxDebug` URL 매개 변수 | 예 | 사용 `alloy_debug` 유사한 디버그 정보에 대한 매개 변수 |
| `mboxTrace` URL 매개 변수 | 예 | Experience Platform 디버거 브라우저 확장 사용 |
| Adobe Experience Platform Debugger 확장 프로그램 | 예 | 예 |
| `alloy_debug` URL 매개 변수 | 해당되지 않음 | 예 |
| Adobe Experience Platform 보증 | 해당되지 않음 | 예 |

## Adobe Experience Platform Debugger 브라우저 확장 프로그램

Chrome 및 Firefox 용 Adobe Experience Platform Debugger 확장 프로그램은 웹 페이지를 살펴보고 Adobe Experience Cloud 구현의 유효성을 확인하는 데 도움이 됩니다.

모든 웹 페이지에서 Platform Debugger를 실행할 수 있으며 확장은 공개 데이터에 액세스할 수 있습니다. 확장(예: Target 추적 정보)을 사용하여 비공개 데이터에 액세스하려면 다음을 통해 Experience Cloud을 인증해야 합니다 **[!UICONTROL 로그인]** 링크를 클릭합니다.

### Adobe Experience Platform Debugger 가져오기 및 설치

Adobe Experience Platform Debugger는 Google Chrome 또는 Mozilla Firefox 브라우저에 설치할 수 있습니다. 아래 적절한 링크를 클릭하여 기본 브라우저에 확장을 설치합니다.

- [Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)
- [Firefox](https://addons.mozilla.org/ko-KR/firefox/addon/adobe-experience-platform-dbg/)

Chrome 확장 프로그램 또는 Firefox 추가 기능을 설치하면 아이콘(![](assets/start-icon.jpg))가 확장 모음에 추가됩니다. 이 아이콘을 선택하여 확장을 엽니다.

에 대한 자세한 내용은 전용 안내서 를 참조하십시오. [Adobe Experience Platform Debugger 확장 프로그램](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html) 및 모든 Adobe 웹 응용 프로그램을 디버깅하는 방법입니다.

## QA URL을 사용하여 Target 활동 미리 보기

at.js와 Platform Web SDK를 모두 사용하면 Target QA URL을 사용하여 Target 활동을 미리 볼 수 있으며, 두 구현 방법은 모두 동일한 QA 기능을 지원합니다.

Target at.js 또는 Platform Web SDK에서 이름이 인 브라우저에 특정 쿠키를 작성하도록 지시하여 작동하는 QA URL `at_qa_mode`. 이 쿠키는 특정 활동 및 경험에 대한 자격을 강제 적용하는 데 사용됩니다.

>[!CAUTION]
>
>Target QA 모드 기능은 Platform Web SDK 버전 2.13.0 이상에서 지원됩니다. Target QA 모드는 `xdm.web.webPageDetails.URL` 전달된 값 `sendEvent` 호출. 소문자 구분 등 이 값을 수정하면 Target QA 모드가 제대로 작동하지 않을 수 있습니다.

자세한 내용은 전용 안내서 를 참조하십시오 [Target 활동 QA](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html).

## 디버그 Target 구현

아래 표에서는 at.js와 Platform Web SDK 디버깅 전략의 차이점을 설명합니다.

| at.js 기능 | Platform Web SDK에 상응하는 |
| --- | --- |
| **Mbox 비활성화** - Target을 가져오기 및 렌더링에서 비활성화하여 Target 상호 작용 없이 페이지가 중단되었는지 확인<br><br>URL 매개 변수가 있는 페이지 로드: `mboxDisable=true` | 직접적인 동기는 없습니다. 브라우저의 개발자 도구로 모든 Platform Web SDK 요청을 차단할 수 있습니다. |
| **Mbox 디버그** - 브라우저 콘솔에서 모든 at.js 작업을 로그하여 렌더링 문제를 해결합니다<br><br>URL 매개 변수가 있는 페이지 로드: `mboxDebug=true` | **합금 디버그** - 개인화 Target 작업을 포함하되, 이에 제한되지 않는 SDK의 세부 작업을 기록합니다.<br><br>URL 매개 변수가 있는 페이지 로드: `alloy_debug=true`  <br /><br />또는 실행 `alloy("setDebug", { "enabled": true });` 개발자 콘솔에서 |
| **Target 추적** - Target UI에서 mbox 추적 토큰이 생성되면 의사 결정 프로세스에 참여한 세부 정보가 있는 추적 개체를 `window.___target_trace` 개체.<br><br>URL 매개 변수가 있는 페이지 로드: `mboxTrace=window&authorization={TOKEN}` | Adobe Experience Platform 디버거 확장 또는 Platform Assurance를 사용합니다. |

>[!NOTE]
>
>위에 나열된 모든 at.js 디버깅 기능은 Adobe Experience Platform Debugger의 향상된 기능에서 사용할 수 있습니다.

### Target 기능 비활성화

현재 Platform Web SDK에는 Target 응답을 선택적으로 표시하지 않는 기능이 없습니다. 그러나 브라우저의 개발자 도구, 다양한 브라우저 확장 또는 타사 애플리케이션을 통해 Platform Web SDK 요청을 무시할 수 있습니다. 예를 들어 Google Chrome에서 Platform Web SDK를 차단하려면 다음을 수행하십시오.

1. 페이지의 아무 곳이나 마우스 오른쪽 단추로 클릭하고 를 선택합니다 **Inspect**
1. 을(를) 선택합니다 **네트워크** 탭
1. 문자열로 필터링 `//ee//` 플랫폼 웹 SDK 호출만 보려면
1. 페이지를 다시 로드합니다.
1. 필터링된 네트워크 요청 중 하나를 마우스 오른쪽 단추로 클릭하고 를 선택합니다. **블록 요청 도메인**
1. 페이지를 다시 로드하고 네트워크 요청이 차단되었음을 확인합니다
1. 디버깅이 끝나면 차단된 네트워크 요청을 마우스 오른쪽 단추로 클릭하고 을 선택합니다 **차단 해제**&#x200B;를 클릭하거나 개발자 도구 패널을 닫습니다

### 디버그 로깅 보기

를 사용하여 at.js에 대한 디버그 로깅 `mboxDebug=true` URL 매개 변수는 각 Target 요청, 응답 및 콘텐츠를 페이지에 렌더링하기 위한 시도에 대한 자세한 정보를 보여줍니다. Platform Web SDK에는 `alloy_debug=true` URL 매개 변수.

| 정보가 기록됨 | at.js (`mboxDebug=true`) | Platform 웹 SDK(`alloy_debug=true`) |
| --- | --- | --- |
| 필터링에 대한 로깅 접두사 | `AT:` | `[alloy]` |
| 페이지 로드 요청 세부 사항 | 예 | 예 |
| Mbox 또는 범위 요청 세부 사항 | 예 | 예 |
| 요청 상태 | 예 | 예 |
| 응답 세부 정보 | 예 | 예 |
| 렌더링 상태 | 성공 및 오류 | 오류만 |
| 렌더링 세부 사항 | 예 | 예 |

>[!NOTE]
>
>at.js 및 Platform Web SDK에 대한 디버그 로그는 잘못된 선택기로 인해 웹 SDK에서 렌더링 오류만 알리는 주목할 만한 예외와 함께 유사한 수준의 세부 정보를 제공합니다. 디버그 로깅이 현재 렌더링이 성공했는지 확인하지 않습니다.

### Target 추적 보기

Target 추적은 활동 자격 및 방문자의 Target 프로필에 대한 세부 정보를 제공합니다. Target 추적에 공개적으로 사용할 수 없는 정보가 포함되어 있으므로 추적에 권한을 부여하려면 Adobe Experience Platform Debugger 브라우저 확장 프로그램 창 내에서 인증 또는 인증 토큰이 필요합니다.

| Target 추적 메서드 | at.js | Platform 웹 SDK |
| --- | --- | --- |
| `mboxTrace` URL 매개 변수 | 예 | 아니요 |
| Adobe Experience Platform Debugger 브라우저 확장 프로그램 | 예 | 예 |
| Adobe Experience Platform 보증 | 아니요 | 예 |


Adobe Experience Platform Debugger를 사용하여 Platform Web SDK Target 추적을 보려면 다음을 수행하십시오.

1. Platform Web SDK를 사용하여 구현된 Target이 있는 사이트의 페이지로 이동합니다
1. 아이콘을 선택하여 Adobe Experience Platform Debugger 확장 프로그램을 엽니다(![](assets/start-icon.jpg)) 내의 아무 곳에나 삽입할 수 있습니다.
1. 을(를) 선택합니다 **[!UICONTROL 로그인]** 링크
1. Adobe Experience Cloud 로그인을 사용하여 인증
1. 을(를) 선택합니다 **[!UICONTROL 로그]** 왼쪽의 탭
1. 을(를) 선택합니다 **[!UICONTROL Edge]** 맨 위에 있는 탭
1. 디버깅 세션에 이름을 지정하고 (선택 사항) **[!UICONTROL Connect]** 버튼
1. 페이지를 다시 로드하면 로그가 에지 네트워크 상호 작용에 대한 자세한 정보로 채워집니다
1. 설명에서 &quot;Target 추적&quot;으로 시작하는 로그 항목에 초점을 맞추고 을 선택합니다 **[!UICONTROL 보기]** Target 추적 세부 사항을 보려면

![Adobe Experience Platform Debugger를 사용하여 Target 추적을 보는 방법](assets/target-trace-debugger.png){zoomable=&quot;yes&quot;}

선택 후 **[!UICONTROL 보기]**&#x200B;과 같은 오버레이가 표시되므로 요청과 관련된 다음 정보를 확인할 수 있습니다.

- 일치하는 활동
- 일치하지 않는 활동
- 요청 세부 사항
- 프로필 스냅샷

에 대한 전용 안내서를 참조하십시오. [콘텐츠 전달 디버깅](https://experienceleague.adobe.com/docs/target/using/activities/troubleshoot-activities/content-trouble.html) Target 추적에 대한 자세한 정보.

### 보증 문제 해결

Target 추적 정보는 Adobe Experience Platform Debugger 브라우저 확장 프로그램 및 Assurance 애플리케이션(이전의 Project Griffon)에서 모두 볼 수 있습니다. Assurance 내에서 Target 추적을 보려면 다음을 수행합니다.

1. Adobe Experience Platform Debugger 브라우저 확장을 열고 위에 설명된 대로 원격 디버깅 세션을 연결합니다
1. 디버깅 로그 위에 세션 이름이 있는 링크를 선택합니다
1. Platform Assurance는 구현을 위해 데이터 스트림에 구성된 모든 Adobe 응용 프로그램에 대한 자세한 로깅을 로드하고 표시합니다
1. 로그 필터링 기준 `adobe.target`
1. 유형이 있는 로그 항목을 선택합니다 `com.adobe.target.trace`
1. 페이로드의 세부 사항을 확장하고 아래의 정보를 확인합니다 `context > targetTrace`

![Assurance를 사용하여 Target 추적을 보는 방법](assets/target-trace-assurance.png){zoomable=&quot;yes&quot;}

## 네트워크 요청 및 응답 검사

Platform Web SDK의 요청 페이로드 및 응답 `sendEvent` 호출은 at.js와 다릅니다. 아래 개요는 브라우저의 개발자 도구로 네트워크 호출을 검사하는 동안 요청 및 응답의 구조를 이해하는 데 도움이 됩니다.

### 콘텐츠 요청 페이로드

![플랫폼 웹 SDK 페이로드의 특정 요소 Target](assets/target-payload.png){zoomable=&quot;yes&quot;}

- 프로필, 엔티티 및 기타 mbox가 아닌 매개 변수는 아래의 이벤트 배열에 전달됩니다 `data.__adobe.target`
- 결정 범위는 아래의 이벤트 배열에 있습니다 `query.personalization.decisionScopes`
- 다운스트림으로 mbox 매개 변수에 매핑된 XDM 데이터는 아래의 events 배열에 있습니다 `xdm`

### 컨텐츠 응답 본문

![플랫폼 웹 SDK 응답 본문의 Target 특정 요소](assets/target-response.png){zoomable=&quot;yes&quot;}

- Platform 웹 SDK는 `handle` 개체
- 다음 `personalization:decisions` 작업은 Target 또는 offer decisioning의 응답을 나타냅니다
- Target 프로필은 각각 고유한 제안 ID가 접두사로 추가된 어레이로 표시됩니다 `AT:`
- 결정 범위 및 활동 세부 사항은 Proposition 어레이 내에 있습니다
- 오퍼 세부 사항은 `items` 아래에 배열 `data`
- 응답 토큰은 `items` 아래에 배열 `meta`

### 제안 이벤트 페이로드

![Target 제안 이벤트 예](assets/target-proposition-event.png){zoomable=&quot;yes&quot;}

- Target 특정 SDK 이벤트는 `decisioning.propositionDisplay` 노출 또는 `decisioning.propositionInteract` 클릭 등의 상호 작용에 대해
- 제안 이벤트의 세부 사항은 아래의 events 배열에 있습니다. `xdm._experience.decisioning`
- 디스플레이 또는 상호 작용 이벤트의 제안 ID는 Target에서 반환된 콘텐츠의 제안 ID와 일치해야 합니다


축하합니다. 자습서가 종료되었습니다. Adobe Target 구현을 웹 SDK로 마이그레이션해 주십시오!

>[!NOTE]
>
>Adobe는 at.js에서 웹 SDK로 Target 마이그레이션을 성공적으로 수행할 수 있도록 최선을 다하고 있습니다. 마이그레이션에 문제가 발생했거나 이 안내서에 중요한 정보가 누락된 것 같은 경우에는 로그인한 후 알려 주십시오 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
