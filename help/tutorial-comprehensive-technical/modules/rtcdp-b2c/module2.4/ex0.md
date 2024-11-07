---
title: Microsoft Azure Event Hub에 대한 세그먼트 활성화 - Microsoft Azure 환경 구성
description: Microsoft Azure Event Hub에 대한 세그먼트 활성화 - Microsoft Azure 환경 구성
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 2.4.0 환경 구성

## 2.4.0.1 Azure 구독 만들기

>[!NOTE]
>
>이미 Azure 구독이 있는 경우 이 단계를 건너뛸 수 있습니다. 이 경우 연습 13.0.2를 계속하십시오.

[https://portal.azure.com](https://portal.azure.com)(으)로 이동하여 Azure 계정으로 로그인하세요. 전자 메일 주소가 없는 경우 개인 전자 메일 주소를 사용하여 Azure 계정을 만드세요.

![02-azure-portal-email.png](./images/02-azure-portal-email.png)

로그인에 성공하면 다음 화면이 표시됩니다.

![03-azure-logged-in.png](./images/03-azure-logged-in.png)

왼쪽 메뉴를 클릭하고 **모든 리소스**&#x200B;를 선택합니다. 아직 구독하지 않은 경우 Azure 구독 화면이 표시됩니다. 이 경우 **Azure 무료 평가판으로 시작**&#x200B;을 선택하세요.

![04-azure-start-subscribe.png](./images/04-azure-start-subscribe.png)

Azure 구독 양식을 작성하고 활성화를 위한 휴대폰과 신용 카드를 제공하십시오(30일 동안 프리 티어가 제공되며 업그레이드하지 않는 한 요금이 부과되지 않음).

![05-azure-subscription-form.png](./images/05-azure-subscription-form.png)

구독 프로세스가 완료되면 다음 작업을 수행할 수 있습니다.

![06-azure-subscription-ok.png](./images/06-azure-subscription-ok.png)


## 2.4.0.2 Visual Code Studio 설치

Microsoft Visual Code Studio를 사용하여 Azure 프로젝트를 관리합니다. [이 링크](https://code.visualstudio.com/download)를 통해 다운로드할 수 있습니다. 동일한 웹 사이트에서 특정 OS에 대한 설치 지침을 따르십시오.

## 2.4.0.3 Visual Code Extensions 설치

[https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)에서 Visual Studio 코드용 Azure 함수를 설치하십시오. 설치 단추를 클릭합니다.

![07-azure-code-extension-install.png](./images/07-azure-code-extension-install.png)

[https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account)에서 Azure 계정을 설치하고 Visual Studio 코드에 로그인하세요. 설치 단추를 클릭합니다.

![08-azure-account-extension-install.png](./images/08-azure-account-extension-install.png)

## 2.4.0.4 node.js 설치

>[!NOTE]
>
>node.js가 이미 설치되어 있는 경우 이 단계를 건너뛸 수 있습니다. 이 경우 연습 13.0.5를 계속하십시오.

### macOS

먼저 [Homebrew](https://brew.sh/)을(를) 설치했는지 확인하십시오. [여기](https://brew.sh/)의 지침을 따르십시오.

![노드](./images/brew.png)

Homebrew를 설치한 후 다음 명령을 실행합니다.

```javascript
brew install node
```

### Windows

[nodejs.org](https://nodejs.org/en/) 웹 사이트에서 직접 [Windows Installer](https://nodejs.org/en/#home-downloadhead)을(를) 다운로드합니다.

## 2.4.0.5 node.js 버전 확인

이 모듈의 경우 node.js 버전 12가 설치되어 있어야 합니다. 다른 버전의 node.js는 연습 13.5에서 문제를 일으킬 수 있습니다.

계속하기 전에 이제 node.js 버전을 확인하십시오.

이 명령을 실행하여 node.js 버전을 확인합니다.

```javascript
node -v
```

버전이 12보다 낮거나 높은 경우 업그레이드하거나 다운그레이드해야 합니다.

### macOS에서 node.js 버전 업그레이드/다운그레이드

패키지 **n**&#x200B;이(가) 설치되어 있는지 확인하십시오.

패키지 **n**&#x200B;을(를) 설치하려면 다음 명령을 실행하십시오.

```javascript
sudo npm install -g n
```

버전이 버전 12 이하인 경우 이 명령을 실행하여 업그레이드하거나 다운그레이드합니다.

```javascript
sudo n 12.6.0
```

### Windows에서 node.js 버전 업그레이드/다운그레이드

Windows > Campaign 컨트롤 패널 > 프로그램 추가 또는 제거에서 node.js를 제거합니다.

[nodejs.org](https://nodejs.org/en/) 웹 사이트에서 필요한 버전을 설치하는 중입니다.

## 2.4.0.6 NPM 패키지 설치: 요청

node.js 설정의 일부로 패키지 **요청**&#x200B;을(를) 설치해야 합니다.

패키지 **요청**&#x200B;을(를) 설치하려면 다음 명령을 실행하십시오.

```javascript
npm install request
```


다음 단계: [2.4.1 Microsoft Azure EventHub 환경 구성](./ex1.md)

[모듈 2.4로 돌아가기](./segment-activation-microsoft-azure-eventhub.md)

[모든 모듈로 돌아가기](./../../../overview.md)
