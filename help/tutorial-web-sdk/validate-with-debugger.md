---
title: Experience Platform Debugger를 사용하여 웹 SDK 구현 확인
description: Adobe Experience Platform Debugger을 사용하여 Platform Web SDK 구현의 유효성을 검사하는 방법을 알아봅니다. 이 수업은 Web SDK를 사용하여 Adobe Experience Cloud 구현 튜토리얼의 일부입니다.
feature: Web SDK,Tags,Debugger
jira: KT-15405
exl-id: 150bb1b1-4523-4b44-bd4e-6cabc468fc04
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 3%

---

# Experience Platform Debugger를 사용하여 웹 SDK 구현 확인

Adobe Experience Platform Debugger를 사용하여 Adobe Experience Platform Web SDK 구현의 유효성을 검사하는 방법을 알아봅니다.

Experience Platform Debugger는 Chrome 및 Firefox 브라우저에서 사용할 수 있는 확장으로, 웹 페이지에서 Adobe 기술이 구현된 것을 볼 수 있도록 도와줍니다. 원하는 브라우저용 버전을 다운로드합니다.

* [Firefox 확장 프로그램](https://addons.mozilla.org/ko-KR/firefox/addon/adobe-experience-platform-dbg/)
* [Chrome 확장](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

이전에 디버거를 사용한 적이 없는 경우 5분 분량의 개요 비디오를 시청해 보십시오.

>[!VIDEO](https://video.tv.adobe.com/v/32156?learn=on&enablevpops)

이 단원에서는 [Adobe Experience Platform Debugger 확장](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)을 사용하여 [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html)에서 하드코딩된 태그 속성을 자신의 속성으로 바꿉니다.

이 기법은 환경 전환이라고 하며 나중에 웹 사이트에서 태그를 사용하여 작업할 때 유용합니다. 이를 통해 브라우저에서 프로덕션 웹 사이트를 로드할 수 있지만 *개발* 태그 라이브러리를 사용할 수 있습니다. 이 기능을 사용하면 일반 코드 릴리스와 독립적으로 태그 변경 사항을 만들고 확인할 수 있습니다. 결국, 일반 코드 릴리스에서 마케팅 태그 릴리스가 이렇게 분리되는 것은 고객이 태그를 우선 사용하는 주요 이유 중 하나입니다!

## 학습 목표

이 단원이 끝나면 디버거를 사용하여 다음을 수행할 수 있습니다.

* 대체 태그 라이브러리 로드
* 클라이언트측 XDM 이벤트가 예상대로 데이터를 캡처하여 Platform Edge Network에 전송하는지 확인합니다.
* Edge 추적을 활성화하여 Platform Edge Network에서 보낸 서버측 요청 보기

## 전제 조건

데이터 수집 태그 및 [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}에 익숙하고 자습서의 이전 단원을 완료했습니다.

* [XDM 스키마 구성](configure-schemas.md)
* [ID 네임스페이스 구성](configure-identities.md)
* [데이터스트림 구성](configure-datastream.md)
* [태그 속성에 설치된 웹 SDK 확장](install-web-sdk.md)
* [데이터 요소 만들기](create-data-elements.md)
* [ID 만들기](create-identities.md)
* [태그 규칙 만들기](create-tag-rule.md)

## 디버거를 사용하여 대체 태그 라이브러리 로드

Experience Platform Debugger에는 기존 태그 라이브러리를 다른 태그 라이브러리로 바꿀 수 있는 멋진 기능이 있습니다. 이 기법은 유효성 검사에 유용하며, 이를 통해 이 자습서의 많은 구현 단계를 건너뛸 수 있습니다.

1. [Luma 데모 웹 사이트](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}가 열려 있는지 확인하고 Experience Platform 디버거 확장 아이콘을 선택합니다.
1. 디버거가 열리고, 하드코딩된 구현에 대한 몇 가지 세부 사항이 표시됩니다(디버거를 연 후 Luma 사이트를 다시 로드해야 할 수 있음)
1. 디버거가 아래 그림과 같이 &quot;**[!UICONTROL Luma]**&quot;에 연결되어 있는지 확인한 다음 &quot;**[!UICONTROL 잠금]**&quot; 아이콘을 선택하여 디버거를 Luma 사이트에 잠급니다.
1. **[!UICONTROL 로그인]** 단추를 선택하고 Adobe ID를 사용하여 Adobe Experience Cloud에 로그인합니다.
1. 이제 왼쪽 탐색에서 **[!UICONTROL Experience Platform 태그]**(으)로 이동합니다.

   ![디버거 태그 화면](assets/validate-launch-screen.png)

1. **[!UICONTROL 구성]** 탭 선택
1. **[!UICONTROL 페이지 포함 코드]**&#x200B;를 표시하는 오른쪽의 **[!UICONTROL 작업]** 드롭다운을 열고 **[!UICONTROL 바꾸기]**&#x200B;를 선택합니다

   ![작업 > 바꾸기](assets/validate-switch-environment.png) 선택

1. 사용자가 인증되었으므로 디버거는 사용 가능한 태그 속성 및 환경을 가져옵니다. 속성 선택
1. `Development` 환경 선택
1. **[!UICONTROL 적용]** 단추 선택

   ![대체 태그 속성 선택](assets/validate-switch-selection.png)

1. 이제 Luma 웹 사이트가 _을(를) 고유한 태그 속성으로 다시 로드합니다_.

   ![태그 속성이 대체됨](assets/validate-switch-success.png)

자습서를 계속 진행할 때, Luma 사이트를 자신의 태그 속성에 매핑하여 Platform Web SDK 구현의 유효성을 검사하는 이 기술을 사용합니다. 자체 웹 사이트에서 태그를 사용할 때 이와 동일한 기술을 사용하여 프로덕션 웹 사이트에서 개발 태그 라이브러리의 유효성을 검사할 수 있습니다.

## Experience Platform Debugger를 사용하여 클라이언트측 네트워크 요청 확인

디버거를 사용하여 Platform Web SDK 구현에서 트리거된 클라이언트측 비콘의 유효성을 검사하여 Platform Edge Network으로 전송된 데이터를 볼 수 있습니다.

1. 태그 속성의 세부 정보를 보려면 왼쪽 탐색에서 **[!UICONTROL 요약]**(으)로 이동하십시오

   ![요약 탭](assets/validate-summary.png)

1. 이제 왼쪽 탐색 영역에서 **[!UICONTROL Experience Platform Web SDK]**(으)로 이동하여 **[!UICONTROL 네트워크 요청]**&#x200B;을 확인합니다.
1. **[!UICONTROL 이벤트]** 행 열기

   ![Adobe Experience Platform Web SDK 요청](assets/validate-aep-screen.png)

1. [!UICONTROL 변수 업데이트] 작업에 지정한 `web.webpagedetails.pageView` 이벤트 형식과 `AEP Web SDK ExperienceEvent` 필드 그룹을 준수하는 기타 기본 제공 변수를 확인하는 방법에 대해 알아보십시오

   ![이벤트 세부 사항](assets/validate-event-pageViews.png)

1. `web` 개체로 스크롤한 다음 선택하여 열고 `webPageDetails.name`, `webPageDetails.server` 및 `webPageDetails.siteSection`을(를) 검사합니다. 홈 페이지의 해당 `digitalData` 데이터 계층 변수와 일치해야 합니다.

>[!TIP]
>
> 홈 페이지의 `digitalData` 데이터 레이어를 보고 비교하려면 다음 작업을 수행하십시오.
>
> 1. Luma 홈 페이지에서 브라우저 개발자 도구를 엽니다. Chrome의 경우 키보드에서 `F12` 단추를 선택합니다.
> 1. **[!UICONTROL 콘솔]** 탭 선택
> 1. `digitalData`을(를) 입력하고 키보드에서 `Enter`을(를) 선택하여 데이터 레이어 값을 표시합니다.

![네트워크 탭](assets/validate-xdm-content.png)

ID 맵 세부 정보의 유효성을 검사할 수도 있습니다.

1. 자격 증명 `test@adobe.com`/`test`을(를) 사용하여 Luma 사이트에 로그인합니다

1. [Luma 홈 페이지](https://luma.enablementadobe.com/content/luma/us/en.html)로 돌아갑니다.

1. 왼쪽 탐색에서 **[!UICONTROL Experience Platform Web SDK]** 섹션을 엽니다.

   디버거의 ![웹 SDK](assets/identity-debugger-websdk-dark.png)

1. 팝업에서 세부 정보를 열려면 **[!UICONTROL events]** 행을 선택하십시오.

   디버거의 ![웹 SDK](assets/identity-deugger-websdk-event-dark.png)

1. 팝업에서 **identityMap**&#x200B;을(를) 검색합니다. 여기에는 authenticatedState, ID 및 기본 키의 세 가지 키가 포함된 `lumaCrmId`이(가) 표시됩니다.
   디버거의 ![웹 SDK](assets/identity-deugger-websdk-event-lumaCrmId-dark.png)

### 브라우저 개발 도구를 사용하여 클라이언트측 요청 유효성 검사

이러한 유형의 요청 세부 정보는 브라우저의 웹 개발자 도구 **네트워크** 탭에도 표시됩니다(웹 사이트에서 태그 라이브러리를 로드하고 있다고 가정).

1. 브라우저의 웹 개발자 도구 **네트워크** 탭을 열고 페이지를 다시 로드합니다. `/ee`(으)로 호출을 필터링하여 호출을 찾아 선택한 다음 **헤더** 탭과 **페이로드** 탭을 찾습니다

   ![네트워크 탭](assets/validate-dev-console.png)

1. **응답** 탭으로 이동하여 ECID 값이 응답에 어떻게 포함되는지 확인합니다.

   ![네트워크 탭](assets/validate-dev-console-ecid.png)

   >[!NOTE]
   >
   > ECID 값은 네트워크 응답에 표시됩니다. 네트워크 요청의 `identityMap` 부분에 포함되지 않았거나 쿠키에 이 형식으로 저장되지 않습니다.

## Experience Platform Debugger를 사용하여 서버측 네트워크 요청 확인

[데이터 스트림 구성](configure-datastream.md) 단원에서 학습한 대로 Platform Web SDK은 먼저 디지털 속성에서 Platform Edge Network으로 데이터를 전송합니다. 그런 다음 Platform Edge Network에서 데이터 스트림에 활성화된 해당 서비스에 대한 추가 서버측 요청을 수행합니다. 디버거에서 Edge Trace 를 사용하여 Platform Edge Network에서 수행한 서버측 요청의 유효성을 검사할 수 있습니다.

<!--Furthermore, you can also validate the fully processed payload after it reaches an Adobe application by using [Adobe Experience Platform Assurance](https://experienceleague.adobe.com/ko/docs/experience-platform/assurance/home). -->


### Edge 추적 활성화

Edge 추적을 활성화하려면 다음을 수행하십시오.

1. **[!UICONTROL Experience Platform Debugger]**&#x200B;의 왼쪽 탐색에서 **[!UICONTROL 로그]**&#x200B;를 선택합니다.
1. **[!UICONTROL Edge]** 탭을 선택하고 **[!UICONTROL 연결]**&#x200B;을 선택합니다.

   ![Edge 추적 연결](assets/analytics-debugger-edgeTrace.png)

1. 지금은 비어 있습니다

   ![연결된 Edge 추적](assets/analytics-debugger-edge-connected.png)

1. [Luma 홈 페이지](https://luma.enablementadobe.com/)를 새로 고치고 **[!UICONTROL Experience Platform Debugger]**&#x200B;를 다시 확인하여 데이터가 통과되는지 확인하십시오.

   ![Analytics 비콘 Edge 추적](assets/validate-edge-trace.png)

이 시점에서는 데이터 스트림에서 를 활성화하지 않았기 때문에 Adobe 애플리케이션으로 이동하는 Platform Edge Network 요청을 볼 수 없습니다. 향후 단원에서는 Edge Trace 를 사용하여 Adobe 애플리케이션 및 이벤트 전달에 대한 보내는 서버측 요청을 확인합니다. 그러나 먼저 Platform Edge Network—Adobe Experience Platform Assurance에서 수행한 서버측 요청의 유효성을 검사하는 다른 도구에 대해 알아보십시오.

[다음: ](validate-with-assurance.md)

>[!NOTE]
>
>Adobe Experience Platform 웹 SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하고 싶거나 향후 콘텐츠에 대한 제안이 있는 경우 이 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=ko)에서 공유하십시오.
