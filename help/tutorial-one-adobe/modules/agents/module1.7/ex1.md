---
title: 개발 환경 설정
description: 개발 환경 설정
kt: 5342
doc-type: tutorial
exl-id: c9bfb327-362f-4475-89da-8e9788940d56
source-git-commit: 25901342e8d9c46b0edce3b2092b9f1d66ba5849
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# 1.7.1 개발 환경 설정

## 1.7.1.1 Adobe I/O 프로젝트 만들기

[https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}(으)로 이동합니다.

화면 오른쪽 상단 모서리에서 올바른 인스턴스를 선택해야 합니다. 인스턴스는 `--aepImsOrgName--`입니다.

>[!NOTE]
>
> 아래 스크린샷은 선택된 특정 조직을 보여 줍니다. 이 자습서를 수행하는 경우 조직의 이름이 다를 수 있습니다. 이 자습서에 등록하면 사용할 환경 세부 정보가 제공되었으므로 해당 지침을 따르십시오.

**템플릿에서 프로젝트 만들기**&#x200B;를 선택합니다.

![GSPeM 확장성](./images/commerceagent1.png)

**App Builder**&#x200B;을(를) 선택합니다.

![GSPeM 확장성](./images/commerceagent2.png)

이름 `--aepUserLdap-- Commerce Events`을(를) 입력하십시오. **저장**&#x200B;을 클릭합니다.

![GSPeM 확장성](./images/commerceagent4.png)

그럼 이런 걸 보셔야겠네요

![GSPeM 확장성](./images/commerceagent5.png)

**+ 서비스 추가**&#x200B;를 클릭한 다음 **API**&#x200B;을(를) 선택합니다.

![GSPeM 확장성](./images/commerceagent6.png)

API **I/O 이벤트**&#x200B;를 검색하여 선택하십시오. **다음**&#x200B;을 클릭합니다.

![GSPeM 확장성](./images/commerceagent7.png)

자격 증명의 이름을 `vangeluw Commerce Events - Production`(으)로 변경합니다. **구성된 API 저장**&#x200B;을 클릭합니다.

![GSPeM 확장성](./images/commerceagent8.png)

그럼 이걸 보셔야죠 **+ 서비스 추가**&#x200B;를 클릭한 다음 **API**&#x200B;을(를) 선택합니다.

![GSPeM 확장성](./images/commerceagent9.png)

API **I/O 관리 API**&#x200B;를 검색하여 선택하십시오. **다음**&#x200B;을 클릭합니다.

![GSPeM 확장성](./images/commerceagent10.png)

**구성된 API 저장**&#x200B;을 클릭합니다.

![GSPeM 확장성](./images/commerceagent11.png)

그럼 이걸 보셔야죠 **+ 서비스 추가**&#x200B;를 클릭한 다음 **API**&#x200B;을(를) 선택합니다.

![GSPeM 확장성](./images/commerceagent12.png)

API **Adobe Commerce as a Cloud Service**&#x200B;을(를) 검색하고 선택합니다. **다음**&#x200B;을 클릭합니다.

![GSPeM 확장성](./images/commerceagent13.png)

**서버 간 인증**&#x200B;을 선택합니다. **다음**&#x200B;을 클릭합니다.

![GSPeM 확장성](./images/commerceagent14.png)

**다음**&#x200B;을 클릭합니다.

![GSPeM 확장성](./images/commerceagent15.png)

**기본 - Cloud Manager**&#x200B;을(를) 선택합니다. **구성된 API 저장**&#x200B;을 클릭합니다.

![GSPeM 확장성](./images/commerceagent16.png)

그럼 이걸 보셔야죠 **+ 서비스 추가**&#x200B;를 클릭한 다음 **API**&#x200B;을(를) 선택합니다.

![GSPeM 확장성](./images/commerceagent17.png)

API **Adobe Commerce용 Adobe I/O Events**&#x200B;을(를) 검색하고 선택합니다. **다음**&#x200B;을 클릭합니다.

![GSPeM 확장성](./images/commerceagent18.png)

**구성된 API 저장**&#x200B;을 클릭합니다.

![GSPeM 확장성](./images/commerceagent19.png)

이제 프로젝트가 설정되었으며 사용할 수 있습니다.

![GSPeM 확장성](./images/commerceagent20.png)

## 1.7.1.2 개발 환경 구성

확장 가능한 앱을 만들고 제출하고 배포하려면 컴퓨터의 로컬 개발 환경에 다음 응용 프로그램 및 패키지가 설치되어 있어야 합니다.

- Node.js(버전 20.x 이상)
- npm(Node.js와 함께 패키지됨)
- Adobe Developer 명령줄 인터페이스(CLI)

이러한 응용 프로그램 또는 패키지가 컴퓨터에 아직 설치되지 않은 경우 다음 단계를 수행합니다.

### Node.js 및 npm

[https://nodejs.org/en/download](https://nodejs.org/en/download)&#x200B;(으)로 이동합니다. 그런 다음 Node.js 및 npm을 설치하기 위해 실행해야 하는 여러 터미널 명령과 함께 이 메시지가 표시됩니다. 여기에 표시된 명령은 MacBook에 적용할 수 있습니다.

![GSPeM 확장성](./images/commerceagent21.png)

먼저 새 터미널 창을 엽니다. 스크린샷의 2행에 언급된 명령을 붙여넣고 실행합니다.

`curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash`

그런 다음 스크린샷의 5행에 있는 명령을 실행합니다.

`\. "$HOME/.nvm/nvm.sh"`

두 명령을 성공적으로 실행한 후 다음 명령을 실행합니다.

`node -v`

버전 번호가 반환되는 것을 볼 수 있습니다.

![GSPeM 확장성](./images/commerceagent22.png)

그런 다음 이 명령을 실행합니다.

`npm -v`

NPM이 아직 설치되지 않은 경우 `npm install -g npm@11.9.0` 명령을 사용하여 설치할 수 있습니다.

버전 번호가 반환되는 것을 볼 수 있습니다.

![GSPeM 확장성](./images/commerceagent23.png)

마지막 2개의 명령이 버전 번호를 성공적으로 반환한 경우 이 2개의 기능을 성공적으로 구성했습니다.

### Adobe Developer 명령줄 인터페이스(CLI)

Adobe Developer 명령줄 인터페이스(CLI)를 설치하려면 터미널 창에서 다음 명령을 실행합니다.

`npm install -g @adobe/aio-cli`

이 명령을 실행하는 데 2분 정도 걸릴 수 있습니다. 종료 결과는 다음과 유사해야 합니다.

![GSPeM 확장성](./images/commerceagent24.png)

이제 Adobe Developer 명령줄 인터페이스(CLI)도 성공적으로 설치되었습니다.

### Commerce용 Adobe Developer CLI(명령줄 인터페이스) SDK 확장

Commerce용 Adobe I/O SDK 확장을 설치하려면 터미널 창에서 다음 명령을 실행합니다.

`npm install @adobe/aio-commerce-sdk`

![GSPeM 확장성](./images/commerceagent25.png)

### Adobe I/O CLI용 Adobe Commerce 플러그인

Adobe I/O CLI용 Adobe Commerce 플러그인을 설치하려면 터미널 창에서 다음 명령을 실행합니다.

`aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime`

![GSPeM 확장성](./images/commerceagent26.png)

이제 Adobe Commerce, Adobe I/O Events 및 Adobe I/O Runtime과 함께 App Builder 프로젝트를 실행할 수 있는 기본 요소를 설정했습니다.

## 다음 단계

[커서를 사용하여 프로젝트 개발](./ex2.md){target="_blank"}(으)로 이동

[Adobe Commerce용 지능형 개발자 도구로 돌아가기](./aiassisteddev.md){target="_blank"}

[모든 모듈로 돌아가기](./../../../overview.md){target="_blank"}
