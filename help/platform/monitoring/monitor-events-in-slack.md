---
title: Slack의 이벤트 모니터링
description: Adobe App Builder Webhook 프록시와 통합하여 Slack에서 Experience Platform 알림을 받는 방법을 알아봅니다.
feature: Monitoring
role: Developer, Admin
level: Intermediate
duration: 519
last-substantial-update: 2026-02-24T00:00:00Z
jira: KT-20339
exl-id: 6d4a072c-9eef-4a38-9459-9e1cbd66bfb5
source-git-commit: 4ec7a800ef963f9b1257e2f246428abff32e9b94
workflow-type: tm+mt
source-wordcount: '1539'
ht-degree: 0%

---

# Slack에서 Experience Platform 이벤트 모니터링

Adobe App Builder Webhook 프록시와 통합하여 Slack에서 Experience Platform 알림을 받는 방법을 알아봅니다. 데이터 엔지니어와 관리자는 Adobe Experience Platform에서 Slack의 사전 알림을 수신하여 플랫폼 구현의 상태를 모니터링할 수 있습니다. 이 튜토리얼에서는 Adobe App Builder을 사용하여 Adobe I/O Events을 Slack에 연결하는 아키텍처 및 구현 단계에 대해 설명합니다.


>[!VIDEO](https://video.tv.adobe.com/v/3480183?learn=on)

## Webhook 프록시의 이유는 무엇입니까?

확인 프로세스의 프로토콜 불일치로 인해 Adobe I/O Events을 Slack에 직접 연결할 수 없습니다.

* **문제**: Adobe I/O Events에 Webhook을 등록하면 Adobe에서 끝점에 &quot;문제&quot; 요청(`GET` 또는 `POST`)을 보냅니다. 끝점이 이 문제를 성공적으로 처리하고 특정 값을 반환하여 소유권을 확인해야 합니다.

* **제한 사항**: Slack의 수신 Webhooks는 메시징에 대한 JSON 페이로드만 수집하도록 설계되었습니다. Adobe의 검증 챌린지 악수를 인지하거나 이에 대응하기 위한 논리를 가지고 있지 않다.

* **솔루션**: Adobe App Builder을 사용하여 중간 웹후크 프록시를 배포합니다. 이 프록시는 Adobe과 Slack 사이에서 다음과 같은 작업을 수행합니다.
   1. Adobe의 요청을 가로채고 확인 질문에 응답합니다.
   1. 페이로드 형식을 Slack 호환 메시지로 설정하여 Slack에 전달합니다.

* **게재 메서드**: 런타임 작업.  런타임 작업은 Adobe App Builder과 함께 제공됩니다. 런타임 작업(웹이 아닌 작업)을 이벤트 처리기로 사용하는 경우 Adobe I/O Events에서 서명 확인 및 챌린지 응답을 자동으로 처리합니다. 런타임 작업은 코드가 적게 필요하고 기본 제공 보안을 제공하므로 권장되는 방법입니다.

## 아키텍처 개요

### Adobe Developer Console란?

Adobe Developer Console은 Adobe 프로젝트, API 및 자격 증명을 관리하는 중앙 포털입니다. 여기서 프로젝트를 만들고, 인증을 구성하고, 웹후크를 등록할 수 있습니다.

### App Builder란?

Adobe App Builder은 엔터프라이즈 개발자가 클라우드 기반 애플리케이션을 구축할 수 있는 완벽한 프레임워크입니다.

* **프로비저닝**: App Builder은 기본적으로 활성화되어 있지 않습니다. 조직에 기능으로 프로비저닝되어야 합니다. 조직에 **[!DNL App Builder]** 권한이 있는지 확인하십시오.

* **프로젝트 템플릿**: App Builder 프로젝트는 특히 **[!UICONTROL 의]** App Builder[!DNL Developer Console] 템플릿을 사용하여 만들어집니다([!UICONTROL 템플릿의 프로젝트] > [!UICONTROL App Builder]). 템플릿은 필요한 작업 공간과 런타임 환경을 자동으로 설정합니다.

* **App Builder 시작 안내서**: [ 설명서를 참조하여 템플릿에서 첫 번째 프로젝트를 프로비전 및 만드십시오](https://developer.adobe.com/app-builder/docs/get_started/app_builder_get_started/first-app){target=_blank}.

### Adobe I/O Runtime란?

Adobe I/O Runtime은 App Builder을 구동하는 서버를 사용하지 않는 플랫폼입니다. 이를 통해 개발자는 서버 인프라를 관리하지 않고도 HTTP 요청에 응답하여 실행되는 코드(Functions-as-a-Service)를 배포할 수 있습니다.

이 구현에서는 **Action**&#x200B;을 사용합니다. 작업은 Adobe I/O Runtime에서 실행되는 상태를 저장하지 않는 함수(Node.js로 작성)입니다. 이 작업은 Adobe I/O Events이 통신하는 공개 HTTP 끝점 역할을 합니다.

자세한 내용은 [Adobe I/O Runtime 설명서](https://developer.adobe.com/runtime/){target=_blank}를 참조하세요.

## 구현 안내서

### 전제 조건

시작하기 전에 다음을 확인하십시오.

* **Adobe Developer Console 액세스**: App Builder이 활성화된 조직 내에서 시스템 관리자 또는 [개발자 역할](../admin/add-developers.md)에 대한 액세스 권한이 있어야 합니다.

  >[!TIP]
  > App Builder 프로비저닝을 확인하려면 [Adobe Developer Console](https://developer.adobe.com/console/){target=_blank}에 로그인하고 원하는 조직에 있는지 확인하고 **[!UICONTROL 템플릿에서 프로젝트 만들기]**&#x200B;를 선택한 다음 App Builder 템플릿을 사용할 수 있는지 확인하십시오. 그렇지 않은 경우 App Builder FAQ 섹션 &quot;[App Builder을 가져오는 방법](https://developer.adobe.com/app-builder/docs/intro_and_overview/faq#how-to-get-app-builder){target=_blank}&quot;을 검토하십시오.


* **Node.js 및 npm**: 이 프로젝트에는 NPM(Node Package Manager)이 포함된 Node.js가 필요합니다. NPM은 Adobe CLI를 설치하고 프로젝트 종속성을 관리하는 데 사용됩니다.

   * [Node.js 다운로드(LTS 버전 권장)](https://nodejs.org/){target=_blank}
   * [npm 시작 안내서](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm){target=_blank} - 설치 확인 방법에 대한 안내서입니다.

* **`aio CLI`**: 터미널을 통해 설치됨: `npm install -g @adobe/aio-cli`
* **Slack 앱 구성**: 작업 영역에서 **들어오는 Webhook**&#x200B;이(가) 활성화된 Slack 앱을 설정해야 합니다.

   * [Slack 앱 만들기](https://api.slack.com/apps){target=_blank}
   * [Slack 수신 Webhooks 안내서](https://docs.slack.dev/messaging/sending-messages-using-incoming-webhooks/){target=_blank} - 이 안내서에 따라 앱을 만들고 Webhook URL(`https://hooks.slack.com/`(으)로 시작...)을 생성합니다.

### 1단계: Adobe Developer Console에서 프로젝트 만들기

먼저 Adobe Developer Console에서 App Builder 템플릿을 사용하여 프로젝트를 만듭니다.

1. [Adobe Developer Console](https://developer.adobe.com/console)에 로그인
1. **[!UICONTROL 템플릿에서 프로젝트 만들기]** 선택
1. App Builder 템플릿 선택
1. 프로젝트 제목(예: `Slack webhook integration`) 입력
1. **[!UICONTROL 저장]** 선택

### 런타임 환경 초기화

터미널에서 다음 명령을 실행하여 프로젝트 구조를 만듭니다.

#### `aio`에 로그인

```
aio login
```

#### 2단계: 새 App Builder 프로젝트 초기화

```
aio app init slack-webhook-proxy
```

1. 조직을 선택하고 **Enter**&#x200B;를 누르십시오.
1. 이전 단계에서 만든 프로젝트(예: `Slack webhook integration`)를 선택하고 **Enter**&#x200B;를 누릅니다.
1. **[!UICONTROL 내 조직에서 지원하는 템플릿만 선택]** 옵션
1. **Enter**&#x200B;를 눌러 샘플 섹션을 건너뜁니다.
1. 메시지가 표시되면 다음 구성 요소가 선택되어 있는지 확인하고(원을 채워야 함) **Enter**&#x200B;를 누릅니다.
   1. **[!UICONTROL 작업: 런타임 작업 배포]**
   1. **[!UICONTROL 이벤트: Adobe I/O Events에 게시]**
   1. **[!UICONTROL 웹 Assets: 호스팅된 정적 자산에 배포]**
1. &#39;위쪽&#39; 및 &#39;아래쪽&#39; 화살표를 사용하여 수신 목록을 탐색하고 **[!UICONTROL Adobe Experience Platform: 실시간 고객 프로필]**&#x200B;을 선택하고 **Enter**&#x200B;를 누릅니다.
1. **[!UICONTROL 일반]** 작업이 자동으로 생성됩니다.
1. UI에 대해 **[!UICONTROL 순수 HTML/JS]**&#x200B;를 선택하고 **Enter**&#x200B;를 누르십시오.
1. 외부 API 이름에 액세스하는 방법을 보여 주기 위해 **[!UICONTROL generic]**&#x200B;을(를) 샘플 작업으로 유지하고 **Enter** 키를 누릅니다.
1. **[!UICONTROL publish-events]**&#x200B;을(를) 샘플 작업 이름으로 유지하여 클라우드 이벤트 형식으로 메시지를 만들고 **Enter**&#x200B;을 누릅니다.

앱 초기화가 완료되어야 합니다.

#### 프로젝트 디렉토리로 이동합니다.

```
cd slack-webhook-proxy
```

#### 웹 작업 추가

```
aio app add action
```

1. **[!UICONTROL 내 조직에서 지원하는 템플릿만]**&#x200B;을 선택하고 **Enter**&#x200B;를 누르십시오.
2. 표시된 표에서 **[!UICONTROL publish-events]** 작업을 봅니다. 작업을 선택하려면 **Space**&#x200B;를 누르십시오. 비디오 자습서에 표시된 대로 이름 옆에 원이 있으면 **Enter**&#x200B;를 누르십시오
3. 작업 이름을 `webhook-proxy`(으)로 지정합니다

### 3단계: 프록시 작업 코드 업데이트

IDE 또는 텍스트 편집기에서 다음 코드를 사용하여 `actions/webhook-proxy/index.js` 파일을 만들거나 수정합니다. 이 구현은 이벤트를 Slack에 전달합니다. 런타임 작업 등록을 사용할 때 서명 확인 및 과제 처리가 자동으로 수행됩니다.

```javascript
const fetch = require("node-fetch");
const { Core } = require("@adobe/aio-sdk");
 
/**
 * Adobe I/O Events to Slack Runtime Proxy
 *
 * Receives events from Adobe I/O Events and forwards them to Slack.
 * Signature verification and challenge handling are automatic when
 * using Runtime Action registration (non-web action).
 */
async function main(params) {
  const logger = Core.Logger("webhook-proxy", { level: params.LOG_LEVEL || "info" });
 
  try {
    logger.info(`Event received: ${JSON.stringify(params)}`);
 
    // Forward to Slack
    return forwardToSlack(params, params.SLACK_WEBHOOK_URL, logger);
 
  } catch (error) {
    logger.error(`Error: ${error.message}`);
    return { statusCode: 500, body: { error: "Internal server error" } };
  }
}
 
/**
 * Forwards the event payload to Slack
 */
async function forwardToSlack(payload, webhookUrl, logger) {
  if (!webhookUrl) {
    logger.error("SLACK_WEBHOOK_URL not configured");
    return { statusCode: 500, body: { error: "Server configuration error" } };
  }
 
  // Extract Adobe headers passed to runtime action
  const headers = {
    "x-adobe-event-code": payload["x-adobe-event-code"],
    "x-adobe-event-id": payload["x-adobe-event-id"],
    "x-adobe-provider": payload["x-adobe-provider"]
  };
 
  const slackMessage = buildSlackMessage(payload, headers);
 
  const response = await fetch(webhookUrl, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(slackMessage)
  });
 
  if (!response.ok) {
    const errorText = await response.text();
    logger.error(`Slack API error: ${response.status} - ${errorText}`);
    return { statusCode: response.status, body: { error: errorText } };
  }
 
  logger.info("Event forwarded to Slack");
  return { statusCode: 200, body: { success: true } };
}
 
/**
 * Builds a Slack Block Kit message from the event payload
 */
function buildSlackMessage(payload, headers) {
  // Adobe passes event code as x-adobe-event-code header (available in params for runtime actions)
  const eventType = headers["x-adobe-event-code"] ||
                    payload["x-adobe-event-code"] ||
                    payload.event_code ||
                    payload.type ||
                    payload.event_type ||
                    "Adobe Event";
  const eventId = headers["x-adobe-event-id"] || payload["x-adobe-event-id"] || payload.event_id || payload.id || "N/A";
  const eventData = payload.data || payload.event || payload;
 
  return {
    blocks: [
      {
        type: "header",
        text: { type: "plain_text", text: `Event: ${eventType}`, emoji: true }
      },
      {
        type: "section",
        fields: formatDataFields(eventData)
      },
      { type: "divider" },
      {
        type: "context",
        elements: [{
          type: "mrkdwn",
          text: `*Event ID:* ${eventId}  |  *Time:* ${new Date().toISOString()}`
        }]
      }
    ]
  };
}
 
/**
 * Formats event data as Slack mrkdwn fields
 */
function formatDataFields(data, maxFields = 10) {
  if (typeof data !== "object" || data === null) {
    return [{ type: "mrkdwn", text: `*Payload:*\n${String(data)}` }];
  }
 
  const entries = Object.entries(data);
  if (entries.length === 0) {
    return [{ type: "mrkdwn", text: "_No data provided_" }];
  }
 
  return entries.slice(0, maxFields).map(([key, value]) => ({
    type: "mrkdwn",
    text: `*${key}:*\n${typeof value === "object" ? `\`\`\`${JSON.stringify(value)}\`\`\`` : value}`
  }));
}
 
exports.main = main;
```

### 4단계: 작업 구성

`app.config.yaml`의 작업 구성이 중요합니다. 웹 사용: Developer Console에서 런타임 작업으로 등록할 수 있는 웹이 아닌 작업을 만들려면 아니오를 사용하십시오.

```yaml
application:
  runtimeManifest:
    packages:
      slack-webhook-proxy:
        license: Apache-2.0
        actions:
          webhook-proxy:
            function: actions/webhook-proxy/index.js
            web: no
            runtime: nodejs:22
            inputs:
              LOG_LEVEL: info
              SLACK_WEBHOOK_URL: $SLACK_WEBHOOK_URL
            annotations:
              require-adobe-auth: false
              final: true
```

#### 이유: `web: no?`

웹이 아닌 작업을 사용하고 Developer Console의 &quot;런타임 작업&quot; 옵션을 통해 등록하면 Adobe I/O Events에서 자동으로 다음과 같은 작업을 수행합니다.

* 챌린지 확인을 처리합니다(`GET` 및 `POST` 모두).
* 작업을 호출하기 전에 디지털 서명 확인
* 작업 앞에 서명 유효성 검사기 작업을 연결합니다.

즉, 코드는 비즈니스 논리(Slack으로 전달)만 처리하면 됩니다.

### 4단계: 환경 변수 업데이트

자격 증명을 안전하게 관리하기 위해 환경 변수를 사용합니다. 프로젝트의 루트에 `.env` 파일을 만들거나 수정하여 Slack 웹후크 URL을 추가합니다. `.env` 파일이 표시되지 않으면 시스템에 숨겨진 파일을 표시하십시오.

```
# ... other .env file content ...
 
SLACK_WEBHOOK_URL=https://hooks.slack.com/services/YOUR/WEBHOOK/URL
```

### 5단계: 작업 배포

환경 변수가 설정되면 작업을 배포합니다. 터미널에서 이 명령을 실행할 때는 프로젝트의 루트(예: `slack-webhook-proxy`)에 있어야 합니다.

```
aio app deploy
```

작업이 Adobe I/O Runtime에 배포되고 Developer Console에서 등록에 사용할 수 있습니다.

### 6단계: Adobe Developer Console에서 작업 등록

작업이 배포되었으므로 이제 Adobe 이벤트의 대상으로 등록합니다.

1. [Adobe Developer Console](https://developer.adobe.com/console){target=_blank}(으)로 이동하여 App Builder 프로젝트를 엽니다.
1. **[!UICONTROL Workspace]** 선택
1. **[!UICONTROL 서비스 추가]**&#x200B;를 선택하고 **[!UICONTROL 이벤트]**&#x200B;를 선택합니다.
1. **[!UICONTROL Adobe Experience Platform]**&#x200B;을(를) 제품으로 선택합니다.
1. 이벤트 유형으로 **[!UICONTROL 플랫폼 알림]**&#x200B;을(를) 선택하십시오.
1. Slack에서 알림을 받을 특정 이벤트(또는 모두)를 선택하고 **[!UICONTROL 다음]**&#x200B;을 선택합니다.
1. [OAuth 자격 증명을 만들거나](https://experienceleague.adobe.com/en/docs/platform-learn/tutorials/api/platform-api-authentication){target=_blank}하십시오.
1. **[!UICONTROL 이벤트 등록 세부 정보]** 구성:
   1. **[!UICONTROL 등록 이름]**: 등록에 수사적 이름을 지정하십시오.
   1. **[!UICONTROL 등록 설명]**: 다른 기여자가 수행하는 작업을 알 수 있도록 명확하게 표시되는지 확인하십시오.
   1. **[!UICONTROL 다음]** 선택
   1. **[!UICONTROL 배달 메서드]**: **[!UICONTROL 런타임 작업]**(&quot;Webhook&quot;가 아님)을 선택합니다.
   1. **[!UICONTROL 런타임 작업]**: 드롭다운에서 `webhook-proxy`을(를) 선택합니다(표시되지 않는 경우 페이지 새로 고침).
1. **[!UICONTROL 구성된 이벤트 저장]**&#x200B;을 선택합니다.


### 7단계: 샘플 이벤트를 사용하여 유효성 검사

구성된 이벤트 옆에 있는 &#39;샘플 이벤트 보내기&#39; 아이콘을 클릭하여 전체 흐름을 처음부터 끝까지 테스트할 수 있습니다.

샘플 이벤트는 Slack 앱을 만들고 웹후크를 만들 때 구성한 채널에서 전송됩니다. 다음과 유사한 내용이 표시됩니다.

![Slack의 모니터링 이벤트 예](../assets/slack-monitor.png)

축하합니다. Slack과 Experience Platform 이벤트를 통합했습니다!

### 일반적인 문제

다음은 프록시를 구성할 때 발생할 수 있는 몇 가지 문제와 이러한 문제를 해결할 수 있는 몇 가지 잠재적인 방법입니다.

* **IMS 조직을 볼 수 없습니다**: `aio app init`을(를) 실행할 때 IMS 조직 목록이 표시되지 않으면 다음을 시도하십시오. 터미널에서 `aio logout`을(를) 실행하고 기본 웹 브라우저에서 Experience Cloud에서 로그아웃한 다음 `aio login`을(를) 다시 실행하십시오.
* **드롭다운에 작업이 표시되지 않음**: `web: no`이(가) `app.config.yaml`에 설정되어 있는지 확인하십시오. 런타임 작업 드롭다운에는 웹이 아닌 작업만 표시됩니다. 배포 후 Developer Console 페이지를 새로 고칩니다.
* **서명 확인 실패**: 활성화 로그에 이 오류가 표시되면 Adobe의 기본 제공 유효성 검사기가 요청을 거부했음을 의미합니다. 이는 합법적인 Adobe 이벤트에서는 일어나서는 안 됩니다. 이벤트 등록이 올바르게 구성되었는지 확인합니다.
* **Slack에서 메시지를 받지 못함**: `SLACK_WEBHOOK_URL`이(가) `.env` 파일에 올바르게 설정되어 있고 Slack 앱에서 수신 Webhook을 사용하도록 설정되어 있는지 확인하십시오.
* **작업 시간 초과**: 런타임 작업의 시간 제한은 60초입니다. 작업이 더 오래 걸리는 경우 저널링 접근 방식을 대신 사용하는 것이 좋습니다.
