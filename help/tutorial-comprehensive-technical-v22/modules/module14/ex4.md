---
title: 데이터 수집 및 실시간 서버 측 전달 - Google Cloud 기능 만들기 및 구성
description: Google Cloud 기능 만들기 및 구성
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: d3678a30-6df9-44aa-a2fa-970127f75f59
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1600'
ht-degree: 0%

---

# 14.4 Google 클라우드 기능 만들기 및 구성

## 14.4.1 Google 클라우드 기능 만들기

이동 [https://console.cloud.google.com/](https://console.cloud.google.com/). 이동 **클라우드 함수**.

![GCP](./images/gcp1.png)

그러면 이게 보입니다. 클릭 **함수 만들기**.

![GCP](./images/gcp2.png)

그러면 이게 보입니다.

![GCP](./images/gcp6.png)

다음 옵션을 선택합니다.

- **함수 이름**: `--demoProfileLdap---event-forwarding`
- **지역**: 원하는 영역 선택
- **트리거 유형**: 선택 **HTTP**
- **인증**: 선택 **인증되지 않은 호출 허용**

이제 이걸 가져가세요 **저장**&#x200B;을 클릭합니다.

![GCP](./images/gcp7.png)

클릭 **다음**.

![GCP](./images/gcp8.png)

그러면 다음 내용이 표시됩니다.

![GCP](./images/gcp9.png)

다음 옵션을 선택합니다.

- **런타임**: 선택 **Node.js 16** (또는 최근 항목)
- **진입점**: enter **helloAEP**

클릭 **API 활성화** 활성화됨 **Cloud Build API**. 그러면 새 창이 보입니다. 새 창에서 **활성화** 다시 한 번

![GCP](./images/gcp10.png)

그러면 이게 보입니다. 클릭 **활성화**.

![GCP](./images/gcp11.png)

한 번 **Cloud Build API** 이 활성화되면 이 표시됩니다.

![GCP](./images/gcp12.png)

다음 위치로 돌아갑니다 **클라우드 기능**.
클라우드 함수 인라인 편집기에서 다음 코드가 있는지 확인합니다.

```javascript
/**
 * Responds to any HTTP request.
 *
 * @param {!express:Request} req HTTP request context.
 * @param {!express:Response} res HTTP response context.
 */
exports.helloAEP = (req, res) => {
  let message = req.query.message || req.body.message || 'Hello World!';
  res.status(200).send(message);
};
```

다음을 클릭합니다. **배포**.

![GCP](./images/gcp13.png)

그러면 이게 보입니다. 이제 클라우드 기능을 만들고 있습니다. 2분 정도 걸릴 수 있습니다.

![GCP](./images/gcp14.png)

함수가 생성되어 실행되면 이를 확인할 수 있습니다. 함수 이름을 클릭하여 엽니다.

![GCP](./images/gcp15.png)

그러면 이게 보입니다. 이동 **트리거**. 그러면 **트리거 URL** Launch Server Side에서 종단점을 정의하는 데 사용할 작업입니다.

![GCP](./images/gcp16.png)

다음과 같은 트리거 URL을 복사합니다. **https://europe-west1-dazzling-pillar-273812.cloudfunctions.net/vangeluw-event-forwarding**.

다음 단계에서는 Adobe Experience Platform 데이터 수집 서버를 구성하여 다음에 대한 특정 정보를 스트리밍합니다 **페이지 보기 수** Google Cloud 기능에 연결할 수도 있습니다. 전체 페이로드를 그대로 전달하는 대신 다음과 같은 메시지만 보낼 수 있습니다. **ECID**, **timestamp** 및 **페이지 이름** Google Cloud 기능에 연결할 수도 있습니다.

다음은 위에 언급된 변수를 필터링하기 위해 구문 분석해야 하는 페이로드의 예입니다.

```json
{
  "events": [
    {
      "xdm": {
        "eventType": "web.webpagedetails.pageViews",
        "web": {
          "webPageDetails": {
            "URL": "https://builder.adobedemo.com/run/vangeluw-OCUC",
            "name": "vangeluw-OCUC",
            "viewName": "vangeluw-OCUC",
            "pageViews": {
              "value": 1
            }
          },
          "webReferrer": {
            "URL": "https://builder.adobedemo.com/run/vangeluw-OCUC/equipment"
          }
        },
        "device": {
          "screenHeight": 1080,
          "screenWidth": 1920,
          "screenOrientation": "landscape"
        },
        "environment": {
          "type": "browser",
          "browserDetails": {
            "viewportWidth": 1920,
            "viewportHeight": 451
          }
        },
        "placeContext": {
          "localTime": "2022-02-23T06:51:07.140+01:00",
          "localTimezoneOffset": -60
        },
        "timestamp": "2022-02-23T05:51:07.140Z",
        "implementationDetails": {
          "name": "https://ns.adobe.com/experience/alloy/reactor",
          "version": "2.8.0+2.9.0",
          "environment": "browser"
        },
        "_experienceplatform": {
          "identification": {
            "core": {
              "ecid": "08346969856929444850590365495949561249"
            }
          },
          "demoEnvironment": {
            "brandName": "vangeluw-OCUC"
          },
          "interactionDetails": {
            "core": {
              "channel": "web"
            }
          }
        }
      },
      "query": {
        "personalization": {
          "schemas": [
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
          ],
          "decisionScopes": [
            "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0YzA1MjM4MmUxYjY1MDUiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTRiZjA5ZGM0MTkwZWJiYSJ9",
            "__view__"
          ]
        }
      }
    }
  ],
  "query": {
    "identity": {
      "fetch": [
        "ECID"
      ]
    }
  },
  "meta": {
    "state": {
      "domain": "adobedemo.com",
      "cookiesEnabled": true,
      "entries": [
        {
          "key": "kndctr_907075E95BF479EC0A495C73_AdobeOrg_identity",
          "value": "CiYwODM0Njk2OTg1NjkyOTQ0NDg1MDU5MDM2NTQ5NTk0OTU2MTI0OVIPCPn66KfyLxgBKgRJUkwx8AH5-uin8i8="
        },
        {
          "key": "kndctr_907075E95BF479EC0A495C73_AdobeOrg_consent_check",
          "value": "1"
        },
        {
          "key": "kndctr_907075E95BF479EC0A495C73_AdobeOrg_consent",
          "value": "general=in"
        }
      ]
    }
  }
}
```

다음은 구문 분석해야 하는 정보가 포함된 필드입니다.

- ECID: **events.xdm._experienceplatform.id.core.ecid**
- timestamp: **timestamp**
- 페이지 이름: **events.xdm.web.webPageDetails.name**

이제 Adobe Experience Platform 데이터 수집 서버로 이동하여 데이터 요소를 구성하면 됩니다.

## 14.4.2 이벤트 전달 속성 업데이트: 데이터 요소

이동 [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/) 그리고 **이벤트 전달**. 이벤트 전달 속성을 검색하고 클릭하여 엽니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/prop1.png)

왼쪽 메뉴에서 **데이터 요소**. 클릭 **데이터 요소 추가**.

![Adobe Experience Platform 데이터 수집 SSF](./images/de1gcp.png)

그러면 구성할 새 데이터 요소가 표시됩니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/de2gcp.png)

다음을 선택합니다.

- 로서의 **이름**, 입력 **customerECID**.
- 로서의 **확장**, 선택 **코어**.
- 로서의 **데이터 요소 유형**, 선택 **경로**.
- 로서의 **경로**, 입력 `arc.event.xdm.--aepTenantId--.identification.core.ecid`. 이 경로를 입력하면 필드를 필터링합니다 **ecid** 웹 사이트 또는 모바일 앱에서 Adobe Edge으로 전송된 이벤트 페이로드에서

>[!NOTE]
>
>위 및 아래 경로에는 **arc**. **arc** Adobe 리소스 컨텍스트 및 **arc** 항상 서버 측 컨텍스트에서 사용할 수 있는 가장 높은 사용 가능한 개체를 나타냅니다. 데이터 보강 및 변형도 여기에 추가될 수 있습니다 **arc** Adobe Experience Platform 데이터 수집 서버 함수를 사용하는 개체.
>
>위 및 아래 경로에는 **이벤트**. **이벤트** 은 고유한 이벤트를 나타내며 Adobe Experience Platform 데이터 수집 서버는 항상 모든 이벤트를 개별적으로 평가합니다. 경우에 따라 **events** 웹 SDK 클라이언트측에서 전송하지만 Adobe Experience Platform 데이터 수집 서버에서는 모든 이벤트를 개별적으로 평가합니다.

이제 이걸로 하시겠어요 **저장**&#x200B;을 클릭합니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/gcdpde1.png)

클릭 **데이터 요소 추가**.

![Adobe Experience Platform 데이터 수집 SSF](./images/addde.png)

그러면 구성할 새 데이터 요소가 표시됩니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/de2gcp.png)

다음을 선택합니다.

- 로서의 **이름**, 입력 **eventTimestamp**.
- 로서의 **확장**, 선택 **코어**.
- 로서의 **데이터 요소 유형**, 선택 **경로**.
- 로서의 **경로**, 입력 **arc.event.xdm.timestamp**. 이 경로를 입력하면 필드를 필터링합니다 **timestamp** 웹 사이트 또는 모바일 앱에서 Adobe Edge으로 전송된 이벤트 페이로드에서

이제 이걸로 하시겠어요 **저장**&#x200B;을 클릭합니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/gcdpde2.png)

클릭 **데이터 요소 추가**.

![Adobe Experience Platform 데이터 수집 SSF](./images/addde.png)

그러면 구성할 새 데이터 요소가 표시됩니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/de2gcp.png)

다음을 선택합니다.

- 로서의 **이름**, 입력 **pageName**.
- 로서의 **확장**, 선택 **코어**.
- 로서의 **데이터 요소 유형**, 선택 **경로**.
- 로서의 **경로**, 입력 **arc.event.xdm.web.webPageDetails.name**. 이 경로를 입력하면 필드를 필터링합니다 **이름** 웹 사이트 또는 모바일 앱에서 Adobe Edge으로 전송된 이벤트 페이로드에서

이제 이걸로 하시겠어요 **저장**&#x200B;을 클릭합니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/gcdpde3.png)

이제 다음 데이터 요소를 만들었습니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/de3gcp.png)

## 14.4.3 이벤트 전달 속성 업데이트: 규칙 업데이트

왼쪽 메뉴에서 **규칙**. 이전 연습에서 규칙을 만들었습니다 **모든 페이지**. 해당 규칙을 클릭하여 엽니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/rl1gcp.png)

그럼 이게 될 거야 을(를) 클릭합니다. **+** 아래에 있는 아이콘 **작업** 새 작업을 추가하려면 다음을 수행하십시오.

![Adobe Experience Platform 데이터 수집 SSF](./images/rl2gcp.png)

그러면 이게 보입니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/rl4gcp.png)

다음을 선택합니다.

- 을(를) 선택합니다 **확장**: **Adobe 클라우드 커넥터**.
- 을(를) 선택합니다 **작업 유형**: **가져오기 호출 만들기**.

그러면 이렇게 될 겁니다 **이름**: **Adobe 클라우드 커넥터 - 가져오기 호출 만들기**. 이제 다음을 볼 수 있습니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/rl5gcp.png)

다음으로, 다음을 구성합니다.

- 요청 프로토콜을 GET에서 로 변경합니다. **POST**
- 다음과 같은 이전 단계 중 하나에서 만든 Google 클라우드 함수의 URL을 입력합니다. **https://europe-west1-dazzling-pillar-273812.cloudfunctions.net/vangeluw-event-forwarding**

이제 이걸 가져가세요 다음으로 이동 **본문**.

![Adobe Experience Platform 데이터 수집 SSF](./images/rl6gcp.png)

그러면 이게 보입니다. 에 대한 라디오 단추를 클릭합니다. **JSON**.

![Adobe Experience Platform 데이터 수집 SSF](./images/rl7gcp.png)

구성 **본문** 아래와 같이 변경하는 것을 의미합니다.

| 키 | 값 |
|--- |--- |
| customerECID | {{customerECID}} |
| pageName | {{pageName}} |
| eventTimestamp | {{eventTimestamp}} |

그러면 이게 보입니다. **변경사항 유지**&#x200B;를 클릭합니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/rl9gcp.png)

그러면 이게 보입니다. **저장**&#x200B;을 클릭합니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/rl10gcp.png)

이제 Adobe Experience Platform 데이터 수집 서버 속성에서 기존 규칙을 업데이트합니다. 이동 **게시 흐름** 변경 사항을 게시하려면 다음을 수행하십시오. 개발 라이브러리를 엽니다. **기본** 를 클릭합니다. **편집** 표시된 대로.

![Adobe Experience Platform 데이터 수집 SSF](./images/rl12gcp.png)

을(를) 클릭합니다. **변경된 모든 리소스 추가** 버튼을 클릭하면 규칙 및 데이터 요소가 이 라이브러리에 표시됩니다. 다음을 클릭합니다. **개발을 위한 저장 및 구축**. 이제 변경 사항을 배포하고 있습니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/rl13gcp.png)

몇 분 후에 배포가 완료되고 테스트를 받을 준비가 되었음을 알 수 있습니다.

![Adobe Experience Platform 데이터 수집 SSF](./images/rl14.png)

## 14.3.4 구성 테스트

이동 [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Adobe ID으로 로그인하면 다음이 표시됩니다. 웹 사이트 프로젝트를 클릭하여 엽니다.

![DSN](../module0/images/web8.png)

이제 아래 흐름을 따라 웹 사이트에 액세스할 수 있습니다. 클릭 **통합**.

![DSN](../module0/images/web1.png)

설정 **통합** 페이지에서 연습 0.1에서 생성된 데이터 수집 속성을 선택해야 합니다.

![DSN](../module0/images/web2.png)

그러면 데모 웹 사이트가 열립니다. URL을 선택하고 클립보드에 복사합니다.

![DSN](../module0/images/web3.png)

새 시크릿 브라우저 창을 엽니다.

![DSN](../module0/images/web4.png)

이전 단계에서 복사한 데모 웹 사이트의 URL을 붙여넣습니다. 그런 다음 Adobe ID을 사용하여 로그인하라는 메시지가 표시됩니다.

![DSN](../module0/images/web5.png)

계정 유형을 선택하고 로그인 프로세스를 완료합니다.

![DSN](../module0/images/web6.png)

그러면 시크릿 브라우저 창에서 로드되는 웹 사이트가 표시됩니다. 모든 데모에서는 신선하고 시크릿 브라우저 창을 사용하여 데모 웹 사이트 URL을 로드해야 합니다.

![DSN](../module0/images/web7.png)

브라우저 개발자 보기를 열면 아래에 표시된 대로 네트워크 요청을 검사할 수 있습니다. 필터를 사용하는 경우 **상호 작용**, Adobe Experience Platform 데이터 수집 클라이언트가 Adobe Edge에 보내는 네트워크 요청을 볼 수 있습니다.

![Adobe Experience Platform 데이터 수집 설정](./images/hook1.png)

보기를 Google Cloud 함수로 전환한 다음 로 이동합니다. **로그**. 이제 이 뷰와 유사한 보기가 있고 많은 로그 항목이 표시됩니다. 볼 때마다 **함수 실행이 시작됨**: Google 클라우드 함수에서 수신 트래픽을 수신했음을 의미합니다.

![Adobe Experience Platform 데이터 수집 설정](./images/hook3gcp.png)

수신 데이터로 작업할 수 있도록 함수를 약간 업데이트하여 Adobe Experience Platform 데이터 수집 서버에서 수신한 정보를 표시하겠습니다. 이동 **소스** 을(를) 클릭합니다. **편집**.

![Adobe Experience Platform 데이터 수집 설정](./images/hook4gcp.png)

다음 화면에서 **다음**.

![Adobe Experience Platform 데이터 수집 설정](./images/gcf1.png)

다음과 같이 코드를 업데이트합니다.

```javascript
/**
 * Responds to any HTTP request.
 *
 * @param {!express:Request} req HTTP request context.
 * @param {!express:Response} res HTTP response context.
 */
exports.helloAEP = (req, res) => {
  console.log('>>>>> Function has started. The following information was received from Event Forwarding:');
  console.log(req.body);

  let message = req.query.message || req.body.message || 'Hello World!';
  res.status(200).send(message);
};
```

그럼 이걸로 주세요 클릭 **배포**.

![Adobe Experience Platform 데이터 수집 설정](./images/gcf2.png)

2분 후에 함수가 다시 배포됩니다. 함수 이름을 클릭하여 엽니다.

![Adobe Experience Platform 데이터 수집 설정](./images/gcf3.png)

데모 웹 사이트에서 다음과 같은 제품으로 이동합니다 **디드레 편안한 카프리**.

![Adobe Experience Platform 데이터 수집 설정](./images/gcf3a.png)

보기를 Google Cloud 함수로 전환한 다음 로 이동합니다. **로그**. 이제 이 뷰와 유사한 보기가 있고 많은 로그 항목이 표시됩니다.

이제 데모 웹 사이트의 모든 페이지 보기에 대해 수신된 정보를 표시하는 Google 클라우드 함수의 로그에 새 로그 항목이 표시됩니다.

![Adobe Experience Platform 데이터 수집 설정](./images/gcf4.png)

이제 Adobe Experience Platform 데이터 수집에서 수집한 데이터를 실시간으로 Google 클라우드 기능 엔드포인트로 전송했습니다. 여기에서 이 데이터는 저장 및 보고를 위한 BigQuery와 같은 모든 Google Cloud Platform 애플리케이션이나 기계 학습 사용 사례에 사용할 수 있습니다.

다음 단계: [14.5 AWS 에코시스템을 위한 Forward 이벤트](./ex5.md)

[모듈 14로 돌아가기](./aep-data-collection-ssf.md)

[모든 모듈로 돌아가기](./../../overview.md)
