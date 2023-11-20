---
title: Experience Platform 디버거를 사용하여 Web SDK 구현 확인
description: Adobe Experience Platform Debugger을 사용하여 Platform Web SDK 구현의 유효성을 검사하는 방법을 알아봅니다. 이 단원은 Web SDK를 사용하여 Adobe Experience Cloud 구현 자습서의 일부입니다.
feature: Web SDK,Tags,Debugger
exl-id: 150bb1b1-4523-4b44-bd4e-6cabc468fc04
source-git-commit: e2594d3b30897001ce6cb2f6908d75d0154015eb
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 5%

---

# Experience Platform 디버거를 사용하여 Web SDK 구현 확인

Adobe Experience Platform Debugger을 사용하여 Platform Web SDK 구현의 유효성을 검사하는 방법을 알아봅니다.

Experience Platform 디버거는 Chrome 및 Firefox 브라우저에서 사용할 수 있는 확장 프로그램으로, 웹 페이지에서 구현된 Adobe 기술을 볼 수 있도록 도와줍니다. 원하는 브라우저용 버전을 다운로드합니다.

* [Firefox 확장](https://addons.mozilla.org/ko-KR/firefox/addon/adobe-experience-platform-dbg/)
* [Chrome 확장 프로그램](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

이전에 디버거를 사용한 적이 없고 이 디버거가 이전 Adobe Experience Cloud 디버거와 다른 경우에는 5분 분량의 개요 비디오를 시청하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/32156?learn=on)

이 단원에서는 [Adobe Experience Platform Debugger 확장](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) 에서 하드코딩된 태그 속성을 바꾸려면 [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html) 자신의 재산과 함께

이 기법은 환경 전환이라고 하며 나중에 웹 사이트에서 태그를 사용하여 작업할 때 유용합니다. 브라우저에서 프로덕션 웹 사이트를 로드할 수 있지만 *개발* 태그 환경입니다. 이 기능을 사용하면 일반 코드 릴리스와 독립적으로 태그 변경 사항을 만들고 확인할 수 있습니다. 결국, 일반 코드 릴리스에서 마케팅 태그 릴리스가 이렇게 분리되는 것은 고객이 태그를 우선 사용하는 주요 이유 중 하나입니다!

## 학습 목표

이 단원이 끝나면 디버거를 사용하여 다음을 수행할 수 있습니다.

* 대체 태그 라이브러리 로드
* XDM 개체가 데이터를 예상 Edge Network로 캡처하고 보내고 있는지 확인합니다.

## 전제 조건

데이터 수집 태그 및 [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} 을(를) 통해 다음 자습서의 이전 단원을 완료했습니다.

* [권한 구성](configure-permissions.md)
* [XDM 스키마 구성](configure-schemas.md)
* [ID 네임스페이스 구성](configure-identities.md)
* [데이터스트림 구성](configure-datastream.md)
* [태그 속성에 설치된 Web SDK 확장](install-web-sdk.md)
* [데이터 요소 만들기](create-data-elements.md)
* [태그 규칙 만들기](create-tag-rule.md)


## 디버거를 사용하여 대체 태그 라이브러리 로드

이 튜토리얼에서는 공개적으로 호스팅되는 [Luma 데모 웹 사이트](https://luma.enablementadobe.com/content/luma/us/en.html). 홈페이지를 열고 책갈피를 지정합니다.

![Luma 홈페이지](assets/validate-luma-site.png)

Experience Platform 디버거에는 기존 태그 라이브러리를 다른 태그 라이브러리로 바꿀 수 있는 멋진 기능이 있습니다. 이 기법은 유효성 검사에 유용하며, 이를 통해 이 자습서의 많은 구현 단계를 건너뛸 수 있습니다.

1. Luma 사이트가 열려 있는지 확인하고 Experience Platform 디버거 확장 아이콘을 선택합니다.
1. 디버거가 열리고 이 자습서와 관련이 없는 하드코딩된 구현에 대한 일부 세부 정보가 표시됩니다(디버거를 연 후 Luma 사이트를 다시 로드해야 할 수 있음).
1. 디버거가 &quot;&quot;인지 확인합니다.**[!UICONTROL Luma에 연결됨]**&#x200B;아래 그림과 같이 &quot;을(를) 선택한 다음 &quot;**[!UICONTROL 잠금]**&quot; 아이콘을 클릭하여 Luma 사이트에 디버거를 잠급니다.
1. 다음 항목 선택 **[!UICONTROL 로그인]** 버튼을 클릭하고 Adobe ID를 사용하여 Adobe Experience Cloud에 로그인합니다.
1. 이제 다음으로 이동 **[!UICONTROL Experience Platform 태그]** 왼쪽 탐색

   ![Debugger 태그 화면](assets/validate-launch-screen.png)

1. 다음 항목 선택 **[!UICONTROL 구성]** 탭
1. 오른쪽에 표시되는 **[!UICONTROL 페이지 포함 코드]**&#x200B;를 열고 **[!UICONTROL 작업]** 드롭다운, 선택 **[!UICONTROL 바꾸기]**

   ![Actions > Replace 를 선택합니다.](assets/validate-switch-environment.png)

1. 사용자가 인증되었으므로 디버거는 사용 가능한 태그 속성 및 환경을 가져옵니다. 다음 항목 선택 `Web SDK Course` 속성
1. 다음 항목 선택 `Development` 환경
1. 다음 항목 선택 **[!UICONTROL 적용]** 단추

   ![대체 태그 속성 선택](assets/validate-switch-selection.png)

1. 이제 Luma 웹 사이트가 다시 로드됩니다. _태그 속성 포함_.

   ![태그 속성이 대체됨](assets/validate-switch-success.png)

자습서를 계속 진행하면 이 기술을 사용하여 Luma 사이트를 고유한 태그 속성에 매핑하여 Platform Web SDK 구현의 유효성을 검사합니다. 프로덕션 웹 사이트에서 태그 사용을 시작할 때 이와 동일한 기술을 사용하여 변경 내용의 유효성을 검사할 수 있습니다.

## Experience Platform 디버거에서 구현의 유효성 검사

디버거를 사용하여 Platform Web SDK 구현의 유효성을 검사하고 Platform Edge Network로 전송된 데이터를 볼 수 있습니다.

1. 다음으로 이동 **[!UICONTROL 요약]** 왼쪽 탐색에서 태그 속성의 세부 정보를 보려면

   ![요약 탭](assets/validate-summary.png)

1. 이제 다음으로 이동 **[!UICONTROL Experience Platform Web SDK]** 을(를) 클릭하여 왼쪽 탐색 창에서 **[!UICONTROL 네트워크 요청]**
1. 를 엽니다. **[!UICONTROL events]** 행 (이 스크린샷에 자신보다 많은 요청이 표시되며 향후 단원의 요청이 포함되어 지금은 무시할 수 있으니 걱정하지 마십시오.)

   ![Adobe Experience Platform Web SDK 요청](assets/validate-aep-screen.png)

1. 다음을 확인하는 방법에 주목하십시오. `web.webpagedetails.pageView` 에 지정한 이벤트 유형 [!UICONTROL 이벤트 보내기] 작업 및 기타 기본 제공 변수 `AEP Web SDK ExperienceEvent Mixin` 형식

   ![이벤트 세부 사항](assets/validate-event-pageViews.png)

1. 아래로 스크롤하여 `web` 개체를 선택하여 열고 `webPageDetails.name`, `webPageDetails.server`, 및 `webPageDetails.siteSection`. 홈 페이지의 해당 digitalData 데이터 레이어 변수와 일치해야 합니다

   ![네트워크 탭](assets/validate-xdm-content.png)

ID 맵 세부 정보의 유효성을 검사할 수도 있습니다.

1. 자격 증명 `test@adobe.com`/`test`를 사용하여 Luma 사이트에 로그인합니다.

1. [Luma 홈 페이지](https://luma.enablementadobe.com/content/luma/us/en.html)로 돌아갑니다.

1. 를 엽니다. **[!UICONTROL Experience Platform Web SDK]** 왼쪽 탐색 메뉴의 섹션

   ![Debugger의 웹 SDK](assets/identity-debugger-websdk-dark.png)

1. 다음 항목 선택 **[!UICONTROL events]** 팝업에서 세부 정보를 여는 행

   ![Debugger의 웹 SDK](assets/identity-deugger-websdk-event-dark.png)

1. 검색 **identityMap** 팝업 내에서 여기 있습니다. `lumaCrmId` authenticatedState, id 및 primary의 세 가지 키 사용:
   ![Debugger의 웹 SDK](assets/identity-deugger-websdk-event-lumaCrmId-dark.png)


## 브라우저 개발 도구로 유효성 검사

이러한 유형의 요청 세부 사항은 브라우저의 웹 개발자 도구에도 표시됩니다 **네트워크** 탭(웹 사이트에서 태그 라이브러리를 로드하고 있다고 가정).

1. 브라우저의 웹 개발자 도구를 엽니다 **네트워크** 페이지를 탭하고 다시 로드합니다. 다음을 포함한 호출 필터링 `/ee` 호출을 찾으려면 해당 호출을 선택한 다음 **헤더** 탭, 및 **페이로드** 탭

   ![네트워크 탭](assets/validate-dev-console.png)

1. 로 이동 **응답** 를 탭하고 ECID 값이 응답에 어떻게 포함되는지 확인합니다. 다음 연습에서 프로필 정보의 유효성을 검사하는 데 사용할 이 값을 복사하십시오

   ![네트워크 탭](assets/validate-dev-console-ecid.png)

   >[!NOTE]
   >
   >    위의 스크린샷과 동일한 양의 페이로드 요청이 표시되지 않을 수 있습니다. 이 차이는 다음에 대한 향후 학습 내용이기 때문입니다. [Target 설정](setup-target.md) 스크린샷 생성 시 이(가) 완료되었습니다. 지금은 이 차이를 무시할 수 있습니다.

이제 페이지에서 실행되는 XDM 개체와 데이터 수집의 유효성을 검사하는 방법에 대한 지식이 있으면 Platform Web SDK를 사용하여 개별 Adobe 애플리케이션을 설정할 수 있습니다.

[다음: ](setup-experience-platform.md)

>[!NOTE]
>
>Adobe Experience Platform Web SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하려는 경우 또는 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
