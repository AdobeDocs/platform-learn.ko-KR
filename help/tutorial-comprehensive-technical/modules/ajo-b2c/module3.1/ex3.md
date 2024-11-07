---
title: 구성 ID 업데이트 및 여정 테스트
description: 구성 ID 업데이트 및 여정 테스트
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# 3.1.3 데이터 수집 속성 업데이트 및 여정 테스트

## 3.1.3.1 데이터 수집 속성 업데이트

[Adobe Experience Platform 데이터 수집](https://experience.adobe.com/launch/)(으)로 이동하여 **태그**&#x200B;를 선택합니다.

이전에 보았던 Adobe Experience Platform 데이터 수집 속성 페이지입니다.

![속성 페이지](./../../../modules/datacollection/module1.1/images/launch1.png)

모듈 0에서 데모 시스템은 웹 사이트용 클라이언트 속성과 모바일 앱용 클라이언트 속성 두 개를 만들었습니다. **[!UICONTROL 검색]** 상자에서 `--aepUserLdap--`을(를) 검색하여 찾으십시오. **Web** 속성을 열려면 클릭하세요.

![검색 상자](./../../../modules/datacollection/module1.1/images/property6.png)

그러면 이걸 보게 될 거야.

![설치 시작](./images/rule1.png)

왼쪽 메뉴에서 **규칙**(으)로 이동하여 규칙 **프로필 등록**&#x200B;을 검색합니다. **프로필 등록** 규칙을 클릭하여 엽니다.

![설치 시작](./images/rule2.png)

그러면 이 규칙의 세부 사항이 표시됩니다. **AEP로 &quot;등록 이벤트&quot; 보내기 - JO 트리거** 작업을 열려면 클릭하세요.

![설치 시작](./images/rule3.png)

그런 다음 이 작업이 트리거되면 특정 데이터 요소를 사용하여 XDM 데이터 구조를 정의하는 것을 볼 수 있습니다. 해당 데이터 요소를 업데이트해야 하며 [연습 7.1](./ex1.md)에서 구성한 이벤트의 **이벤트 ID**&#x200B;을(를) 정의해야 합니다.

![설치 시작](./images/rule4.png)

이제 데이터 요소 **XDM - 등록 이벤트**&#x200B;를 업데이트해야 합니다. 이렇게 하려면 **데이터 요소**(으)로 이동하십시오. **XDM - 등록 이벤트**&#x200B;를 검색하고 클릭하여 해당 데이터 요소를 엽니다.

![설치 시작](./images/rule5.png)

그러면 다음과 같은 결과가 표시됩니다.

![설치 시작](./images/rule6.png)

`_experience.campaign.orchestration.eventID` 필드로 이동합니다. 현재 값을 제거하고 eventID를 붙여넣습니다.

다시 말해서 이벤트 ID는 **구성 > 이벤트**&#x200B;의 Adobe Journey Optimizer에서 찾을 수 있으며 이벤트 ID는 이벤트 페이로드의 샘플 페이로드에서 찾을 수 있습니다. 이러한 페이로드는 `"eventID": "227402c540eb8f8855c6b2333adf6d54d7153d9d7d56fa475a6866081c574736"`과(와) 같습니다.

![AOP](./images/payloadeventID.png)

eventID를 붙여넣은 후 화면은 다음과 같아야 합니다. **저장** 또는 **라이브러리에 저장**&#x200B;을 클릭합니다.

![설치 시작](./images/rule7.png)

마지막으로 변경 사항을 게시해야 합니다. 왼쪽 메뉴에서 **흐름 게시**(으)로 이동합니다.

![설치 시작](./images/rule8.png)

**변경된 모든 리소스 추가**&#x200B;를 클릭한 다음 **개발에 저장 및 빌드**&#x200B;를 클릭합니다.

![설치 시작](./images/rule9.png)

그런 다음 라이브러리가 업데이트되고 1~2분 후 구성을 테스트할 수 있습니다.

## 3.1.3.2 여정 테스트

[https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects)(으)로 이동합니다. Adobe ID으로 로그인하면 이 메시지가 표시됩니다. 웹 사이트 프로젝트를 클릭하여 엽니다.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

**Screens** 페이지에서 **실행**&#x200B;을 클릭합니다.

![DSN](./../../../modules/datacollection/module1.1/images/web2.png)

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

화면 왼쪽 상단 모서리에 있는 Adobe 로고 아이콘을 클릭하여 프로필 뷰어를 엽니다.

![데모](./../../../modules/datacollection/module1.2/images/pv1.png)

프로필 뷰어 패널과 현재 알 수 없는 이 고객의 기본 식별자로 **Experience Cloud ID**&#x200B;를 사용하는 실시간 고객 프로필을 살펴보십시오.

![데모](./../../../modules/datacollection/module1.2/images/pv2.png)

등록/로그인 페이지로 이동합니다. **계정 만들기**&#x200B;를 클릭합니다.

![데모](./../../../modules/datacollection/module1.2/images/pv9.png)

자세한 내용을 입력하고 **등록**&#x200B;을 클릭하면 이전 페이지로 리디렉션됩니다.

![데모](./../../../modules/datacollection/module1.2/images/pv10.png)

프로필 뷰어 패널을 열고 실시간 고객 프로필로 이동합니다. 프로필 뷰어 패널에 새로 추가된 이메일 및 전화 식별자와 같은 모든 개인 데이터가 표시됩니다.

![데모](./../../../modules/datacollection/module1.2/images/pv11.png)

계정을 만든 후 1분이 지나면 Adobe Journey Optimizer에서 계정 만들기 이메일을 받게 됩니다.

![설치 시작](./images/email.png)

다음 단계: [요약 및 이점](./summary.md)

[모듈 3.1로 돌아가기](./journey-orchestration-create-account.md)

[모든 모듈로 돌아가기](../../../overview.md)
