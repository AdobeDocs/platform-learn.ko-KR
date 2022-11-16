---
title: Microsoft Azure 이벤트 허브에 세그먼트 활성화 - Microsoft Azure 환경 구성
description: Microsoft Azure 이벤트 허브에 세그먼트 활성화 - Microsoft Azure 환경 구성
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 79711c1a-674c-4233-9c6c-af3bad6d0e0c
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# 13.0 환경 구성

## 13.0.1 Azure 구독 만들기

>[!NOTE]
>
>이미 Azure 구독이 있는 경우 이 단계를 건너뛸 수 있습니다. 이 경우 13.0.2를 계속 연습하십시오.

이동 [https://portal.azure.com](https://portal.azure.com) Azure 계정으로 로그인합니다. 계정이 없는 경우 개인 전자 메일 주소를 사용하여 Azure 계정을 만드십시오.

![02-azure-portal-email.png](./images/02-azure-portal-email.png)

로그인이 성공하면 다음 화면이 표시됩니다.

![03-azure-logged-in.png](./images/03-azure-logged-in.png)

왼쪽 메뉴에서 을(를) 클릭하고 을(를) 선택합니다 **모든 리소스**&#x200B;을 지정하는 경우 아직 구독하지 않은 경우 Azure 구독 화면이 나타납니다. 이 경우 을(를) 선택합니다. **Azure 무료 체험판으로 시작**.

![04-azure-start-subscribe.png](./images/04-azure-start-subscribe.png)

Azure 구독 양식을 작성하고, 활성화할 휴대폰과 신용 카드를 제공하십시오(30일 동안 무료 계층이 있고, 업그레이드하지 않으면 요금이 청구되지 않음).

![05-azure-subscription-form.png](./images/05-azure-subscription-form.png)

구독 프로세스가 완료되면 을 진행하십시오.

![06-azure-subscription-ok.png](./images/06-azure-subscription-ok.png)


## 13.0.2 Visual Code Studio 설치

Microsoft Visual Code Studio를 사용하여 Azure 프로젝트를 관리합니다. 을 통해 다운로드할 수 있습니다 [이 링크](https://code.visualstudio.com/download). 동일한 웹 사이트에서 특정 OS에 대한 설치 지침을 따르십시오.

## 13.0.3 Visual Code 확장 설치

Visual Studio 코드용 Azure 함수 설치 위치 [https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions). install 단추를 클릭합니다.

![07-azure-code-extension-install.png](./images/07-azure-code-extension-install.png)

다음 위치에서 Visual Studio 코드용 Azure 계정 및 로그인 설치 [https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account). install 단추를 클릭합니다.

![08-azure-account-extension-install.png](./images/08-azure-account-extension-install.png)

## 13.0.4 node.js 설치

>[!NOTE]
>
>이미 node.js가 설치되어 있으면 이 단계를 건너뛸 수 있습니다. 이 경우 13.0.5를 계속 연습하십시오.

### macOS

반드시 [홈브루](https://brew.sh/) 먼저 설치됩니다. 다음 지침을 따르십시오 [여기](https://brew.sh/).

![노드](./images/brew.png)

Homebrew를 설치한 후 다음 명령을 실행합니다.

```javascript
brew install node
```

### Windows

다운로드 [Windows Installer](https://nodejs.org/en/#home-downloadhead) 에서 직접 [nodejs.org](https://nodejs.org/en/) 웹 사이트.

## 13.0.5 node.js 버전 확인

이 모듈의 경우 node.js 버전 12가 설치되어 있어야 합니다. node.js의 다른 버전은 연습 13.5에 문제가 있을 수 있습니다.

계속하기 전에 지금 node.js 버전을 확인하십시오.

이 명령을 실행하여 node.js 버전을 확인합니다.

```javascript
node -v
```

버전이 12세 이하일 경우 업그레이드하거나 다운그레이드해야 합니다.

### macOS의 node.js 버전 업그레이드/다운그레이드

패키지가 있는지 확인합니다 **n** 설치되었습니다.

패키지를 설치하려면 **n**, 다음 명령을 실행합니다.

```javascript
sudo npm install -g n
```

버전이 버전 12 이하일 경우 이 명령을 실행하여 업그레이드하거나 다운그레이드합니다.

```javascript
sudo n 12.6.0
```

### Windows에서 node.js 버전 업그레이드/다운그레이드

Windows > Campaign 컨트롤 패널 > 프로그램 추가/제거에서 node.js를 제거합니다.

에서 필요한 버전 설치 [nodejs.org](https://nodejs.org/en/) 웹 사이트입니다.

## 13.0.6 NPM 패키지 설치: 요청

패키지를 설치해야 합니다. **요청** node.js 설정의 일부로 사용됩니다.

패키지를 설치하려면 **요청**, 다음 명령을 실행합니다.

```javascript
npm install request
```


다음 단계: [13.1 Microsoft Azure EventHub 환경 구성](./ex1.md)

[모듈 13으로 돌아가기](./segment-activation-microsoft-azure-eventhub.md)

[모든 모듈로 돌아가기](./../../overview.md)
