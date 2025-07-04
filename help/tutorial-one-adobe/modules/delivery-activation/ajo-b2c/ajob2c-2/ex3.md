---
title: Adobe Journey Optimizer - 외부 날씨 API, SMS 작업 등 - 사용자 지정 작업 정의
description: Adobe Journey Optimizer - 외부 날씨 API, SMS 작업 등 - 사용자 지정 작업 정의
kt: 5342
doc-type: tutorial
exl-id: 92752e84-3bbe-4d11-b187-bd9fdbbee709
source-git-commit: e3d3b8e3abdea1766594eca53255df024129cb2c
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 3%

---

# 3.2.3 사용자 지정 작업 정의

이 연습에서는 Slack 채널에 메시지를 보내는 사용자 지정 작업을 만듭니다.

[Adobe Journey Optimizer](https://experience.adobe.com)&#x200B;(으)로 이동하여 Adobe Experience Cloud에 로그인합니다. **Journey Optimizer**&#x200B;을(를) 클릭합니다.

![AOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Journey Optimizer의 **Home** 보기로 리디렉션됩니다. 먼저 올바른 샌드박스를 사용하고 있는지 확인하십시오. 사용할 샌드박스를 `--aepSandboxName--`이라고 합니다. 그러면 샌드박스 **의**&#x200B;홈`--aepSandboxName--` 보기에 있게 됩니다.

![AOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

이제 기존 Slack 채널을 사용하여 해당 Slack 채널로 메시지를 전송합니다. Slack에는 사용하기 쉬운 API가 있으며 Adobe Journey Optimizer을 사용하여 해당 API를 트리거할 수 있습니다.

![데모](./images/slack.png)

왼쪽 메뉴에서 아래로 스크롤하여 **구성**&#x200B;을 클릭합니다. 그런 다음 **작업**&#x200B;에서 **관리** 단추를 클릭합니다.

![데모](./images/menuactions.png)

그러면 **작업** 목록이 표시됩니다. **작업 만들기**&#x200B;를 클릭합니다.

![데모](./images/acthome.png)

빈 작업 팝업이 표시됩니다.

![데모](./images/emptyact.png)

작업의 이름으로 `--aepUserLdap--TextSlack`을(를) 사용합니다.

설명을 `Send Message to Slack`(으)로 설정합니다.

**URL 구성**&#x200B;의 경우 다음을 사용하십시오.

- URL: `https://2mnbfjyrre.execute-api.us-west-2.amazonaws.com/prod`
- 메서드: **POST**

>[!NOTE]
>
>위의 URL은 위에서 언급한 대로 요청을 AWS 채널에 전달하는 Slack Lambda 함수를 참조합니다. 이 작업은 Adobe 소유 Slack 채널에 대한 액세스를 보호하기 위해 수행됩니다. 고유한 Slack 채널이 있는 경우 [https://api.slack.com/](https://api.slack.com/)을(를) 통해 Slack 앱을 만들어야 합니다. 그런 다음 해당 Slack 앱에서 들어오는 Webhook을 만든 다음 위의 URL을 들어오는 Webhook URL로 바꿔야 합니다.

![데모](./images/slackname.png)

**인증**&#x200B;을 **인증 안 함**(으)로 설정해야 합니다.

![데모](./images/slackauth.png)

**페이로드**&#x200B;에서 Slack에 전송할 필드를 정의해야 합니다. 논리적으로 Adobe Journey Optimizer과 Adobe Experience Platform이 개인화의 뇌가 되기를 원하므로 Slack으로 보낼 텍스트는 Adobe Journey Optimizer에서 정의한 다음 Slack으로 보내어 실행해야 합니다.

**요청**&#x200B;에 대해 **페이로드 편집** 아이콘을 클릭하십시오.

![데모](./images/slackmsgp.png)

그러면 빈 팝업 창이 표시됩니다.

![데모](./images/slackmsgpopup.png)

아래 텍스트를 복사하여 빈 팝업 창에 붙여넣습니다.

```json
{
 "text": {
  "toBeMapped": true,
  "dataType": "string",
  "label": "textToSlack"
 }
}
```

그러면 이걸 보게 될 거야. **저장**&#x200B;을 클릭합니다.

![데모](./images/slackmsgpopup1.png)

위로 스크롤하고 **저장**&#x200B;을 한 번 더 클릭하여 작업을 저장합니다.

![데모](./images/slackmsgpopup3.png)

이제 사용자 지정 작업이 **작업** 목록에 속합니다.

![데모](./images/slackdone.png)

이벤트, 외부 데이터 소스 및 작업을 정의했습니다. 그런 다음 이 모든 것을 하나의 여정에 결합합니다.

## 다음 단계

[3.2.4 여정 및 메시지 만들기](./ex4.md){target="_blank"}(으)로 이동

[Adobe Journey Optimizer: 외부 데이터 원본 및 사용자 지정 작업으로 돌아가기](journey-orchestration-external-weather-api-sms.md){target="_blank"}

[모든 모듈](./../../../../overview.md){target="_blank"}(으)로 돌아가기
