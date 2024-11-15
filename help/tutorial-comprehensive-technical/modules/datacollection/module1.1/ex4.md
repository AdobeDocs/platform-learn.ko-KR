---
title: 기초 - Adobe Experience Platform 데이터 수집 및 Web SDK 확장 기능 설정 - 클라이언트측 웹 데이터 수집
description: 기초 - Adobe Experience Platform 데이터 수집 및 Web SDK 확장 기능 설정 - 클라이언트측 웹 데이터 수집
kt: 5342
doc-type: tutorial
exl-id: dce7f1b5-72ca-41b2-9aa8-41c13ce25c82
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# 1.1.4 클라이언트측 웹 데이터 수집

## 1.1.4.1 요청의 데이터 유효성 검사

### Adobe Experience Platform Debugger 설치

Experience Platform 디버거는 Chrome 및 Firefox 브라우저에서 사용할 수 있는 확장으로, 웹 페이지에서 구현된 Adobe 기술을 볼 수 있도록 도와줍니다. 기본 브라우저에 대한 버전을 설치합니다.

- [Firefox 확장 프로그램](https://addons.mozilla.org/ko-KR/firefox/addon/adobe-experience-platform-dbg/)

- [Chrome 확장](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

이전에 디버거를 사용한 적이 없고 이전 Adobe Experience Cloud 디버거와 다른 경우 5분 분량의 개요 비디오를 시청하면 됩니다.

>[!VIDEO](https://video.tv.adobe.com/v/32156?quality=12&learn=on)

시크릿 모드에서 데모 웹 사이트를 로드할 경우 Experience Platform 디버거도 시크릿 모드에서 사용할 수 있는지 확인해야 합니다. 이렇게 하려면 브라우저에서 **chrome://extensions**(으)로 이동하여 Experience Platform 디버거 확장을 엽니다.

다음 2가지 설정이 활성화되어 있는지 확인합니다.

- 개발자 모드
- 시크릿 허용

![EXP 뉴스 홈페이지](./images/ext1.png)

### 데모 웹 사이트 열기

[https://dsn.adobe.com](https://dsn.adobe.com)(으)로 이동합니다. Adobe ID으로 로그인하면 이 메시지가 표시됩니다. 웹 사이트 프로젝트에서 세 점 **..**&#x200B;을(를) 클릭한 다음 **실행**&#x200B;을(를) 클릭하여 엽니다.

![DSN](.//images/web8.png)

그러면 데모 웹 사이트가 열리는 것을 볼 수 있습니다. URL을 선택하고 클립보드에 복사합니다.

![DSN](./../../gettingstarted/gettingstarted/images/web3.png)

새 시크릿 브라우저 창을 엽니다.

![DSN](./../../gettingstarted/gettingstarted/images/web4.png)

이전 단계에서 복사한 데모 웹 사이트의 URL을 붙여 넣습니다. 그런 다음 Adobe ID을 사용하여 로그인하라는 메시지가 표시됩니다.

![DSN](./../../gettingstarted/gettingstarted/images/web5.png)

계정 유형을 선택하고 로그인 프로세스를 완료합니다.

![DSN](./../../gettingstarted/gettingstarted/images/web6.png)

그러면 웹 사이트가 시크릿 브라우저 창에 로드되는 것을 볼 수 있습니다. 모든 데모에 대해 새로운 시크릿 브라우저 창을 사용하여 데모 웹 사이트 URL을 로드해야 합니다.

![DSN](./../../gettingstarted/gettingstarted/images/web7.png)

### Experience Platform 디버거를 사용하여 Edge으로 이동하는 호출을 확인합니다.

데모 웹 사이트가 열려 있는지 확인하고 Experience Platform 디버거 확장 아이콘 을 클릭합니다.

![EXP 뉴스 홈페이지](./images/ext2.png)

디버거가 열리고 Adobe Experience Platform 데이터 수집 속성에서 만든 구현의 세부 정보가 표시됩니다. 방금 편집한 확장 및 규칙을 디버깅하고 있다는 점을 기억하십시오.

인증하려면 오른쪽 상단의 **[!UICONTROL 로그인]** 단추를 클릭하십시오. Adobe Experience Platform 데이터 수집 인터페이스로 이미 브라우저 탭이 열려 있는 경우 인증 단계가 자동으로 실행되므로 사용자 이름과 암호를 다시 입력할 필요가 없습니다.

![AEP 디버거](./images/validate2.png)

그러면 디버거에 로그인됩니다.

![AEP 디버거](./images/validate2ab.png)

데모 웹 사이트의 다시 로드 단추를 눌러 해당 특정 탭에 디버거를 연결합니다.

![AEP 디버거](./images/validate2a.png)

위의 그림과 같이 디버거가 **[!UICONTROL 홈에 연결됨]**&#x200B;인지 확인한 다음 **[!UICONTROL 잠금]** 아이콘을 클릭하여 디버거를 데모 웹 사이트로 잠급니다. 이 작업을 수행하지 않으면 디버거가 초점을 맞추고 있는 모든 브라우저 탭의 구현 세부 사항이 표시되도록 계속 전환하므로 혼동을 줄 수 있습니다. 디버거가 잠기면 아이콘이 **잠금 해제**(으)로 변경됩니다.

![AEP 디버거](./images/validate3.png)

그런 다음 데모 웹 사이트의 **플랜** 범주 페이지와 같은 페이지로 이동합니다.

![AEP 디버거 AEP 웹 SDK 확장](./images/validate4.png)

이제 왼쪽 탐색에서 **[!UICONTROL 웹 SDK Experience Platform]**&#x200B;을 클릭하여 **[!UICONTROL 네트워크 요청]**&#x200B;을 확인합니다.

각 요청에 **[!UICONTROL events]** 행이 있습니다.

![AEP 디버거 AEP 웹 SDK 확장](./images/validate5.png)

**[!UICONTROL 이벤트]** 행을 열려면 클릭하세요. **web.webpagedetails.pageViews** 이벤트와 **Web SDK ExperienceEvent XDM** 형식을 준수하는 기타 기본 제공 변수를 확인하는 방법을 참고하십시오.

![이벤트 값](./images/validate8.png)

이러한 유형의 요청 세부 사항은 네트워크 탭에도 표시됩니다. **상호 작용**&#x200B;을 통해 요청을 필터링하여 웹 SDK에서 보낸 요청을 찾습니다. 페이로드 섹션에서 XDM 페이로드에 대한 모든 세부 정보를 찾을 수 있습니다.

![네트워크 탭](./images/validate9.png)

다음 단계: [1.1.5 Adobe Analytics 및 Adobe Audience Manager 구현](./ex5.md)

[모듈 1.1로 돌아가기](./data-ingestion-launch-web-sdk.md)

[모든 모듈로 돌아가기](./../../../overview.md)
