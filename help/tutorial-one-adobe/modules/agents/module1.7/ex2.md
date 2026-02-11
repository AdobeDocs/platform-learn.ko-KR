---
title: Cursor.ai를 사용하여 프로젝트 개발
description: Cursor.ai를 사용하여 프로젝트 개발
kt: 5342
doc-type: tutorial
source-git-commit: 2bfa7f4bee54df8411c96b001224d2986e9fcaf9
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# 1.7.2 Cursor.ai를 사용하여 프로젝트 개발

## 1.7.2.1 디렉터리 및 도구 설정

바탕 화면에서 이름이 `--aepUserLdap---commerce`인 새 디렉터리를 만듭니다.

![Commerce 및 에이전트](./images/cursorai1.png)

폴더를 마우스 오른쪽 단추로 클릭하고 **폴더의 새 터미널**&#x200B;을 선택합니다.

![Commerce 및 에이전트](./images/cursorai2.png)

그럼 이걸 보셔야죠

![Commerce 및 에이전트](./images/cursorai3.png)

이제 [https://github.com/adobe/commerce-integration-starter-kit](https://github.com/adobe/commerce-integration-starter-kit)을(를) 볼 수 있는 기존 Github 리포지토리를 복제해야 합니다.

이 저장소는 Adobe을 사용하여 Adobe Commerce과 ERP, CRM 및 PIM과 같은 기타 백오피스 시스템 간의 통합을 통해 실시간 연결 안정성을 개선하고 시장 출시 기간을 단축하는 Adobe Developer App Builder의 통합 시작 키트입니다.

![Commerce 및 에이전트](./images/cursorai4.png)

이 저장소를 복제하는 방법에는 여러 가지가 있습니다. 이 예에서는 터미널이 사용됩니다.

터미널 창에 다음 명령을 입력하고 실행합니다.

`git clone https://github.com/adobe/commerce-integration-starter-kit`

![Commerce 및 에이전트](./images/cursorai5.png)

몇 초 후에 이 결과가 표시됩니다.

![Commerce 및 에이전트](./images/cursorai6.png)

그런 다음 방금 만든 폴더로 이동해야 합니다. 다음 명령을 입력한 다음 실행합니다.

`cd commerce-integration-starter-kit`

![Commerce 및 에이전트](./images/cursorai7.png)

그럼 이걸 보셔야죠

![Commerce 및 에이전트](./images/cursorai8.png)

그런 다음 Cursor.ai용 Commerce 확장성 도구를 설정해야 합니다. 다음 명령을 입력한 다음 실행합니다.

`aio commerce extensibility tools-setup`

![Commerce 및 에이전트](./images/cursorai9.png)

**현재 디렉터리**&#x200B;를 선택합니다.

![Commerce 및 에이전트](./images/cursorai10.png)

**커서**&#x200B;를 선택하십시오.

![Commerce 및 에이전트](./images/cursorai11.png)

**npm**&#x200B;을(를) 선택하십시오.

![Commerce 및 에이전트](./images/cursorai12.png)

몇 분 후면 이걸 볼 수 있을 거야.

![Commerce 및 에이전트](./images/cursorai13.png)

Cursor.ai용 Commerce 확장성 도구를 설치함으로써, 이제 Cursor.ai 환경의 일부로 사용할 수 있는 MCP 서버가 있습니다. 다음 연습에서는 해당 MCP 서버를 사용하여 App Builder 프로젝트를 개발 및 배포합니다.

## 1.7.2.2 웹후크 설정

이 연습에서는 주문이 생성될 때 주문 이벤트를 해당 웹후크로 스트리밍할 수 있도록 구성해야 하는 웹후크가 필요합니다. 이 연습에서는 [https://pipedream.com/requestbin](https://pipedream.com/requestbin)을(를) 사용하여 샘플 끝점을 사용합니다.

[https://pipedream.com/requestbin](https://pipedream.com/requestbin)&#x200B;(으)로 이동하여 계정을 만든 다음 작업 영역을 만듭니다. 작업 영역이 생성되면 이와 유사한 항목이 표시됩니다.

URL을 복사하려면 **복사**&#x200B;를 클릭하세요. 다음 연습에서는 이 URL을 지정해야 합니다. 이 예제의 URL은 `https://eodts05snjmjz67.m.pipedream.net`입니다.

![Cursor.ai + Commerce](./images/webhook1.png)

## 1.7.2.3 Cursor.ai

Cursor.ai를 엽니다. **프로젝트 열기**&#x200B;를 클릭합니다.

![Cursor.ai + Commerce](./images/cursorai14.png)

만든 폴더(`--aepUserLdap---commerce`(으)로 이동합니다. 해당 폴더에서 이름이 `commerce-integration-starter-kit`인 폴더를 선택합니다. **열기를 클릭합니다**.

![Cursor.ai + Commerce](./images/cursorai15.png)

그럼 이걸 보셔야죠 계속하기 전에 Cursor.ai에서 열려 있는 최상위 폴더가 `commerce-integration-starter-kit`인지 확인하십시오.

![Cursor.ai + Commerce](./images/cursorai16.png)

`I would like to build an app that subscribes to order created events and sends them to a configurable URL with basic authentication`

## 다음 단계

[Adobe Commerce용 지능형 개발자 도구로 돌아가기](./aiassisteddev.md){target="_blank"}

[모든 모듈로 돌아가기](./../../../overview.md){target="_blank"}