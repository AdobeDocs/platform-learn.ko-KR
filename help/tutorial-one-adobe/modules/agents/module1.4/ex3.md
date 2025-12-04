---
title: 데이터 수집 태그를 사용한 Brand Concierge 구현
description: 데이터 수집 태그를 사용한 Brand Concierge 구현
kt: 5342
doc-type: tutorial
source-git-commit: 3704abb57e9fa64c2ff6d6914b6da8b46a5f44aa
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 3%

---

# 1.4.3 데이터 수집 태그를 사용하여 Brand Concierge 구현

>[!IMPORTANT]
>
>이 연습은 진행 중이며 아직 끝나지 않았습니다.

## 데이터 수집 태그 속성

Brand Concierge은 Adobe Experience Platform에 데이터를 보내야 합니다. 이렇게 하려면 웹 SDK(또는 alloy.js)를 웹 사이트에 배포해야 합니다.

이를 수행하려면 이제 데이터 수집 태그 속성을 만들어야 합니다.

[https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}(으)로 이동합니다. **데이터 수집**&#x200B;을 엽니다.

![Brand Concierge](./images/aep101.png)

**새 속성**&#x200B;을 클릭합니다.

![Brand Concierge](./images/aep102.png)

`--aepUserLdap-- - CitiSignal Website + Brand Concierge` 이름을 입력하고 웹 사이트의 도메인도 입력하십시오.

**저장**&#x200B;을 클릭합니다.

![Brand Concierge](./images/aep103.png)

속성을 검색한 다음 엽니다.

![Brand Concierge](./images/aep104.png)

**확장**(으)로 이동한 다음 **카탈로그**(으)로 이동합니다.

![Brand Concierge](./images/aep105.png)

`web sdk`을(를) 검색한 다음 확장 **Adobe Experience Platform Web SDK**&#x200B;을(를) 클릭합니다. **설치**&#x200B;를 클릭합니다.

![Brand Concierge](./images/aep106.png)

그럼 이걸 보셔야죠 여기에서 데이터 스트림에 대한 세부 사항만 제공하면 됩니다. 그러려면 아래로 조금 스크롤하세요.

![Brand Concierge](./images/aep107.png)

세 가지 환경 **프로덕션**, **스테이징** 및 **개발**&#x200B;에 대해 다음을 선택하십시오.

- **샌드박스**: `--aepUserLdap-- - bc`
- **데이터 스트림**: `--aepUserLdap-- - Brand Concierge`

**저장**&#x200B;을 클릭합니다.

![Brand Concierge](./images/aep108.png)

그럼 이걸 보셔야죠 **규칙**(으)로 이동합니다.

![Brand Concierge](./images/aep108a.png)

**새 규칙 만들기**&#x200B;를 클릭합니다.

![Brand Concierge](./images/aep109.png)

`Homepage` 이름을 입력하십시오. 그런 다음 **이벤트**&#x200B;에서 **+ 추가**&#x200B;를 클릭합니다.

![Brand Concierge](./images/aep110.png)

다음 옵션을 선택합니다.

- **확장**: **코어**
- **이벤트 유형**: **라이브러리가 로드됨(페이지 상단)**

**변경 내용 유지**&#x200B;를 클릭합니다.

![Brand Concierge](./images/aep111.png)

그럼 이걸 보셔야죠 **CONDITIONS**&#x200B;에서 **+ 추가**&#x200B;를 클릭합니다.

![Brand Concierge](./images/aep112.png)

다음 옵션을 선택합니다.

- **논리 형식**: **보통**
- **확장**: **코어**
- **조건 유형**: **쿼리 문자열이 없는 경로**
- **경로가 ...**: 웹 사이트 도메인을 입력하십시오(이 경우 `https://vangeluw.adobedemosystem.com/`).

**변경 내용 유지**&#x200B;를 클릭합니다.

![Brand Concierge](./images/aep113.png)

그럼 이걸 보셔야죠 **작업**&#x200B;에서 **+ 추가**&#x200B;를 클릭합니다.

![Brand Concierge](./images/aep114.png)

다음 옵션을 선택합니다.

- **확장**: **코어**
- **작업 유형**: **사용자 지정 코드**
- **언어**: **JavaScript**

**편집기 열기**&#x200B;를 클릭합니다.

![Brand Concierge](./images/aep115.png)

다음 코드를 붙여넣습니다.

```javascript
window["alloy"]("sendEvent", {
        conversation: {fetchConversationalExperience: true}
    }).then(result=> {
        console.log("Conversation experience fetched", result);
        window["alloy"]("bootstrapConversationalExperience", {
            selector: "#brand-concierge-mount",
						// src: "main.js",
            src: "https://experience-stage.adobe.net/solutions/experience-platform-brand-concierge-web-agent/static-assets/main.js",
            stylingConfigurations: window.styleConfiguration,
						stickySession: true
        })
    });
```

**저장**&#x200B;을 클릭합니다.

![Brand Concierge](./images/aep116.png)

그럼 이걸 보셔야죠 **변경 내용 유지**&#x200B;를 클릭합니다.

![Brand Concierge](./images/aep117.png)

그럼 이걸 보셔야죠 **저장**&#x200B;을 클릭합니다.

![Brand Concierge](./images/aep118.png)

**게시 흐름**(으)로 이동합니다. **라이브러리 추가**&#x200B;를 클릭합니다.

![Brand Concierge](./images/aep119.png)

이름을 입력하고 환경에 대해 `Dev`개발(개발)**을 선택한 다음**&#x200B;변경된 모든 리소스 추가&#x200B;**를 클릭합니다.**

**개발을 위한 저장 및 구축**&#x200B;을 클릭합니다.

![Brand Concierge](./images/aep120.png)

몇 분 후에 라이브러리가 빌드됩니다. **개발** 옆에 **녹색 점**&#x200B;이 표시될 때까지 기다리십시오. 그런 다음 **환경**(으)로 이동합니다.

![Brand Concierge](./images/aep121.png)

**개발** 환경에 대한 **설치** 아이콘을 클릭합니다.

![Brand Concierge](./images/aep122.png)

그럼 이걸 보세요 라이브러리의 경로를 복사하려면 **복사** 단추를 클릭하세요. 웹 사이트에서 이를 구현해야 합니다.

라이브러리 경로는 다음과 같아야 합니다.
`<script src="https://assets.adobedtm.com/XXXXXXX/XXXXXXXX/launch-XXXXXXXXX-development.min.js" async></script>`

![Brand Concierge](./images/aep123.png)

[Brand Concierge](./brandconcierge.md){target="_blank"}(으)로 돌아가기

[모든 모듈로 돌아가기](./../../../overview.md){target="_blank"}