---
title: Adobe Experience Platform 데이터 수집 및 실시간 서버측 전달 - 사용자 지정 웹후크 만들기 및 구성
description: 사용자 지정 Webhook 만들기 및 구성
kt: 5342
doc-type: tutorial
exl-id: bb712980-5910-4f01-976b-b7fcf03f5407
source-git-commit: b4a7144217a68bc0b1bc70b19afcbc52e226500f
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 1%

---

# 2.5.3 사용자 지정 Webhook 만들기 및 구성

## 사용자 지정 Webhook 만들기

[https://pipedream.com/requestbin](https://pipedream.com/requestbin)(으)로 이동합니다. [Exercise 2.3.7 대상 SDK](./../../../modules/rtcdp-b2c/module2.3/ex7.md)에서 이 응용 프로그램을 이미 사용했습니다.

해당 서비스를 아직 사용하지 않은 경우 계정을 만든 다음 작업 영역을 만듭니다. 작업 영역이 생성되면 이와 유사한 항목이 표시됩니다.

URL을 복사하려면 **복사**&#x200B;를 클릭하세요. 다음 연습에서는 이 URL을 지정해야 합니다. 이 예제의 URL은 `https://eodts05snjmjz67.m.pipedream.net`입니다.

![데모](./images/webhook1.png)

이제 이 웹 사이트에서 이 웹후크를 만들었고, **[!DNL Event Forwarding property]**&#x200B;에서 이 웹후크를 구성하여 이벤트 전달 테스트를 시작할 수 있습니다.

## 이벤트 전달 속성 업데이트: 데이터 요소 만들기

[https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)(으)로 이동한 다음 **이벤트 전달**(으)로 이동합니다. 이벤트 전달 속성을 검색하고 클릭하여 엽니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/prop1.png)

왼쪽 메뉴에서 **데이터 요소**(으)로 이동합니다. **새 데이터 요소 만들기**&#x200B;를 클릭합니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/de1.png)

그러면 구성할 새 데이터 요소가 표시됩니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/de2.png)

다음을 선택합니다.

- **Name**(으)로 **XDM 이벤트**&#x200B;를 입력하십시오.
- **확장**(으)로 **코어**&#x200B;을(를) 선택합니다.
- **데이터 요소 형식**(으)로 **경로**&#x200B;을(를) 선택하십시오.
- **경로**(으)로 **XDM(arc.event.xdm)에서 데이터 읽기**&#x200B;를 선택합니다. 이 경로를 선택하면 웹 사이트 또는 모바일 앱에서 Adobe Edge으로 보내는 이벤트 페이로드에서 **XDM** 섹션을 필터링합니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/de3.png)

이제 이 음식을 드실 수 있습니다. **저장**&#x200B;을 클릭합니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/de3a.png)

>[!NOTE]
>
>위의 경로에서 **arc**&#x200B;을(를) 참조합니다. **arc**&#x200B;은(는) Adobe 리소스 컨텍스트를 의미하며 **arc**&#x200B;은(는) 항상 서버측 컨텍스트에서 사용 가능한 가장 높은 사용 가능한 개체를 의미합니다. Adobe Experience Platform 데이터 수집 서버 함수를 사용하여 해당 **arc** 개체에 보강 및 변환을 추가할 수 있습니다.
>
>위의 경로에서 **event**&#x200B;을(를) 참조합니다. **event**&#x200B;은(는) 고유한 이벤트를 의미하며 Adobe Experience Platform 데이터 수집 서버는 항상 모든 이벤트를 개별적으로 평가합니다. 경우에 따라 Web SDK Client Side에서 보낸 페이로드에 **events**&#x200B;에 대한 참조가 표시될 수 있지만, Adobe Experience Platform 데이터 수집 서버에서는 모든 이벤트가 개별적으로 평가됩니다.

## Adobe Experience Platform 데이터 수집 서버 속성 업데이트: 규칙 만들기

왼쪽 메뉴에서 **규칙**(으)로 이동합니다. **새 규칙 만들기**&#x200B;를 클릭합니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/rl1.png)

그러면 구성할 새 규칙이 표시됩니다. **이름**: **모든 페이지**&#x200B;를 입력하세요. 이 연습에서는 조건을 구성할 필요가 없습니다. 대신 작업을 설정합니다. **작업** 아래의 **+ 추가** 단추를 클릭합니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/rl2.png)

그러면 이걸 보게 될 거야. 다음을 선택합니다.

- **확장**: **Adobe 클라우드 커넥터**&#x200B;를 선택하십시오.
- **작업 유형**&#x200B;을 선택합니다. **가져오기 호출**.

그러면 **이름**: **Adobe 클라우드 커넥터 - 가져오기 호출**&#x200B;이 제공됩니다. 이제 다음이 표시됩니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/rl4.png)

그런 다음 다음을 구성합니다.

- 요청 메서드를 GET에서 **POST**(으)로 변경
- 이전 단계 중 하나에서 만든 사용자 지정 웹후크의 URL을 입력하십시오. `https://eodts05snjmjz67.m.pipedream.net`

이제 이 항목을 사용할 수 있습니다. 그런 다음 **본문**(으)로 이동합니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/rl6.png)

그러면 이걸 보게 될 거야. 아래 표시된 대로 데이터 요소 아이콘을 클릭합니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/rl7.png)

팝업에서 이전 단계에서 만든 데이터 요소 **XDM 이벤트**&#x200B;를 선택합니다. **선택**&#x200B;을 클릭합니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/rl8.png)

그러면 이걸 보게 될 거야. **변경 내용 유지**&#x200B;를 클릭합니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/rl9.png)

그러면 이걸 보게 될 거야. **저장**&#x200B;을 클릭합니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/rl10.png)

이제 이벤트 전달 속성에서 첫 번째 규칙을 구성했습니다. 변경 내용을 게시하려면 **흐름 게시**(으)로 이동하십시오.
표시된 대로 **편집**&#x200B;을 클릭하여 개발 라이브러리 **Main**&#x200B;을(를) 엽니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/rl11.png)

**변경된 모든 리소스 추가** 단추를 클릭하면 이 라이브러리에 규칙 및 데이터 요소가 나타납니다. **개발을 위한 저장 및 빌드**&#x200B;를 클릭합니다. 변경 사항이 배포되고 있습니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/rl13.png)

몇 분 후에 배포가 완료되고 테스트할 준비가 되었음을 알 수 있습니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/rl14.png)

## 구성 테스트

[https://dsn.adobe.com](https://dsn.adobe.com)(으)로 이동합니다. Adobe ID으로 로그인하면 이 메시지가 표시됩니다. 웹 사이트 프로젝트에서 세 점 **..**&#x200B;을(를) 클릭한 다음 **실행**&#x200B;을(를) 클릭하여 엽니다.

![DSN](./../../datacollection/module1.1/images/web8.png)

그러면 데모 웹 사이트가 열리는 것을 볼 수 있습니다. URL을 선택하고 클립보드에 복사합니다.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

새 시크릿 브라우저 창을 엽니다.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

이전 단계에서 복사한 데모 웹 사이트의 URL을 붙여 넣습니다. 그런 다음 Adobe ID을 사용하여 로그인하라는 메시지가 표시됩니다.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

계정 유형을 선택하고 로그인 프로세스를 완료합니다.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

그러면 웹 사이트가 시크릿 브라우저 창에 로드되는 것을 볼 수 있습니다. 모든 연습에서는 새로운 시크릿 브라우저 창을 사용하여 데모 웹 사이트 URL을 로드해야 합니다.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

브라우저 개발자 보기를 열면 아래에 표시된 대로 네트워크 요청을 검사할 수 있습니다. **상호 작용** 필터를 사용하면 Adobe Experience Platform 데이터 수집 클라이언트에서 Adobe Edge으로 보내는 네트워크 요청이 표시됩니다.

![Adobe Experience Platform 데이터 수집 설정](./images/hook1.png)

원시 페이로드를 선택한 경우 [https://jsonformatter.org/json-pretty-print](https://jsonformatter.org/json-pretty-print)(으)로 이동하여 페이로드를 붙여 넣으십시오. **축소/축소**&#x200B;을 클릭합니다. 그러면 JSON 페이로드, **events** 개체 및 **xdm** 개체가 표시됩니다. 이전 단계 중 하나에서 데이터 요소를 정의할 때 참조 **arc.event.xdm**&#x200B;을(를) 사용했습니다. 그러면 이 페이로드의 **xdm** 개체가 구문 분석됩니다.

![Adobe Experience Platform 데이터 수집 설정](./images/hook2.png)

이전 단계 중 하나에서 사용한 사용자 지정 Webhook [https://webhook.site/](https://webhook.site/)(으)로 보기를 전환합니다. 이제 왼쪽 메뉴에 표시되는 네트워크 요청과 함께 이와 유사한 보기가 있어야 합니다. 위에 표시된 네트워크 요청에서 필터링한 **xdm** 페이로드가 표시됩니다.

![Adobe Experience Platform 데이터 수집 설정](./images/hook3.png)

페이로드에서 아래로 조금 스크롤하여 페이지 이름을 찾습니다. 이 경우 페이지 이름은 **home**&#x200B;입니다.

![Adobe Experience Platform 데이터 수집 설정](./images/hook4.png)

이제 웹 사이트를 탐색하는 경우 이 사용자 지정 웹 후크에서 추가 네트워크 요청을 실시간으로 사용할 수 있습니다.

![Adobe Experience Platform 데이터 수집 설정](./images/hook5.png)

이제 외부 사용자 지정 웹후크에 대한 웹 SDK/XDM 페이로드의 서버측 이벤트 전달을 구성했습니다. 다음 연습에서는 유사한 접근 방식을 구성하고, 동일한 데이터를 Google 및 AWS 환경에 보냅니다.

다음 단계: [2.5.4 Google Cloud 함수 만들기 및 구성](./ex4.md)

[모듈 2.5로 돌아가기](./aep-data-collection-ssf.md)

[모든 모듈로 돌아가기](./../../../overview.md)
