---
title: 공급업체 태그를 이벤트 전달로 이동하는 것이 좋습니다.
description: 서버측 데이터 배포를 위해 클라이언트측 공급업체 태그를 평가하는 방법을 알아봅니다.
feature: Event Forwarding, Tags, Integrations
role: Admin, Developer, Architect, Data Engineer
level: Intermediate, Experienced
jira: KT-9921
exl-id: f8fd351a-435c-4cc1-b987-ed2ead20d4d6
source-git-commit: 7edf8fc46943ae2f1e6e2e20f4d589d7959310c8
workflow-type: tm+mt
source-wordcount: '1279'
ht-degree: 0%

---

# 클라이언트측 공급업체 태그를 이벤트 전달로 이동하는 것이 좋습니다.

클라이언트측 공급업체 태그를 브라우저 및 장치에서 서버로 이동하는 것을 고려해야 하는 몇 가지 강력한 이유가 있습니다. 이 문서에서는 잠재적으로 이벤트 전달 속성으로 이동할 수 있는 클라이언트측 공급업체 태그를 평가하는 방법에 대해 설명합니다.

이 평가는 클라이언트측 공급업체 태그를 제거하고 이벤트 전달 속성에서 서버측 데이터 배포로 바꾸는 것을 고려하는 경우에만 필요합니다. 이 문서에서는 사용자가 [데이터 수집](https://experienceleague.adobe.com/docs/data-collection.html) 및 [이벤트 전달](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)의 기본 사항을 잘 알고 있다고 가정합니다.

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과 제품 설명서에 몇 가지 용어 변경 사항이 적용되었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html)를 참조하십시오.

브라우저 공급업체가 서드파티 쿠키를 처리하는 방법을 변경하고 있습니다. Advertising 및 마케팅 공급업체 및 기술에서는 종종 많은 클라이언트측 태그를 사용해야 합니다. 이러한 문제는 고객이 서버측 데이터 배포를 추가하는 두 가지 강력한 이유에 불과합니다.

>[!NOTE]
>
>이 문서의 `Tag`은(는) 클라이언트측 코드(일반적으로 방문자가 사이트 또는 앱과 상호 작용하는 동안 브라우저나 장치에서 데이터 수집에 사용되는 공급업체의 JavaScript)를 의미합니다. `Website` 또는 `site`은(는) 웹 사이트, 웹 응용 프로그램 또는 모바일 장치용 응용 프로그램을 나타냅니다. 이러한 목적의 &quot;태그&quot;는 종종 픽셀이라고도 합니다.

## 사용 사례 및 데이터 {#use-cases-data}

첫 번째 단계는 클라이언트측 공급업체 태그로 구현된 사용 사례를 정의하는 것입니다. 예를 들어 Facebook(메타) 픽셀을 생각해 보십시오. 이벤트 전달 확장을 사용하여 사이트에서 [메타 전환 API](https://exchange.adobe.com/apps/ec/109168/meta-conversions-api)(으)로 이동하면 특정 사용 사례를 먼저 문서화합니다.

현재 클라이언트측 공급업체 코드의 경우:

- 클라이언트측 태그에 노출되어 전달되는 특정 이벤트와 기타 데이터 포인트는 무엇입니까?
- 이러한 데이터 전송은 언제 어디서 발생합니까?

이 평가를 문서화하기 위해 사용자 자신만 사용하는 경우에도 데이터의 목록, 스프레드시트, 다이어그램 또는 기타 레코드와 이벤트 시퀀스를 만드는 것이 유용합니다. 데이터 소스에 대한 레이블을 포함해야 합니다. 레이블은 어디에서 가져옵니까? 대상—어디로 이동합니까? 변환 - 소스와 대상 간에 어떤 일이 발생합니까?

이 예에서는 방문자가 Facebook 광고를 본 후 사이트와 상호 작용할 때 Facebook 픽셀과의 전환을 추적합니다. 다른 소셜 플랫폼에서 관련 광고를 본 후 사이트와 상호 작용할 수도 있습니다. facebook 광고 도구 및 보고서에서 이러한 전환을 보려면 필요한 데이터가 Facebook에 도착해야 합니다. 이 데이터에는 다운로드, 등록, 좋아요, 또는 구매와 같은 전환 이벤트가 포함될 수 있습니다.

### 데이터 {#data}

기존 클라이언트측 태그를 사용하면 사이트에서 실행되거나 실행될 때 사용 사례의 데이터에 어떤 일이 발생합니까? 공급업체 태그 없이 클라이언트에서 필요한 데이터를 캡처하여 이벤트 전달로 보낼 수 있습니까? [태그](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html) 또는 기타 태그 관리 시스템을 사용하는 경우 대부분의 방문자 상호 작용 데이터를 수집 및 배포에 사용할 수 있습니다. 그러나 클라이언트 측 공급업체 태그 없이 필요할 때, 필요한 위치에서, 필요한 형식으로 사용 사례에 필요한 데이터를 사용할 수 있습니까? 다음은 고려해야 할 몇 가지 추가 데이터 질문입니다.

- 모든 이벤트에 공급업체 사용자 ID가 필요합니까?
- 그렇다면 클라이언트측 태그 없이 수집하거나 생성하는 방법은 무엇입니까?
- 공급업체는 런타임에 특별히 클라이언트측 코드가 필요합니까?
- 필요한 다른 데이터는 무엇입니까? 해당 데이터는 어디에서 가져옵니까?

대부분의 클라이언트측 공급업체 태그는 특정 사용 사례에 대해 많은 데이터 포인트가 필요하지 않지만, 이러한 평가 중에 사용 사례와 필요한 데이터를 확인하는 것이 좋습니다.

## 공급업체 API {#vendor-apis}

이제 를 구현하기 위한 특정 사용 사례, 필요한 데이터 및 소스에서 대상까지의 이벤트 시퀀스를 알고 있습니다. 사용 사례가 이벤트 전달에 적합한지 확인하기 위해 이제 공급업체 API 세부 사항을 조사할 수 있습니다.

>[!IMPORTANT]
>
>많은 공급업체가 서버 간 전송을 위해 API를 활성화하고 있지만, 현재 이러한 목적에 맞는 API를 보유하고 있지 않은 업체도 많습니다.

### API 조사 {#investigate-apis}

다음은 공급업체 API 끝점을 조사하는 데 수행할 수 있는 몇 가지 단계입니다.

공급업체에는 이벤트 데이터의 서버 간 전송을 위해 설계된 API가 있습니까? 먼저 이러한 특정 API 엔드포인트에 대한 요구 사항을 찾습니다.

- 필요한 데이터를 보내기 위한 API 끝점이 있습니까? 사용 사례를 지원하는 끝점을 찾으려면 공급업체의 개발자 또는 API 설명서를 참조하십시오.
- 이벤트 데이터 스트리밍을 허용합니까, 아니면 배치 데이터만 허용합니까?
- 어떤 인증 방법을 지원합니까? 토큰, HTTP, OAuth 클라이언트 자격 증명 버전 또는 기타 이벤트 전달에서 지원하는 메서드는 [여기](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html)를 참조하세요.
- 해당 API의 새로 고침 오프셋은 무엇입니까? 그 제한이 이벤트 전달 최소 범위와 호환됩니까? 세부 정보 [여기](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html#:~:text=you%20can%20configure%20the%20Refresh%20Offset%20value%20for%20the%20secret).
- 관련 끝점에 어떤 데이터가 필요합니까?
- 끝점에 대한 모든 호출에 공급업체별 사용자 식별자가 필요합니까?
- 이러한 식별자가 필요한 경우 클라이언트측 코드 없이 어디에서 생성하고 캡처할 수 있습니까?

즉,

- 공급업체는 사용 사례에 필요한 API 엔드포인트를 제공합니까?
- 이벤트 전달을 위한 호환 인증 방법이 있습니까?
- (클라이언트측에서 또는 다른 API 호출에서) 이벤트 전달 구현에 필요한 모든 데이터에 액세스할 수 있습니까?

이러한 질문에 &quot;예&quot;라고 답변할 수 있다면 태그는 이벤트 전달 속성에서 클라이언트에서 서버로 이동하는 것이 좋습니다.

공급업체에 사용 사례를 지원하기 위한 API 끝점이 없는 경우 분명히 해당 공급업체 태그는 클라이언트측 공급업체 태그 대신 이벤트 전달을 사용하는 데 적합하지 않습니다.

API가 있지만 모든 API 호출에 일부 고유 방문자 또는 사용자 ID가 필요한 경우 어떻게 합니까? 사이트에서 실행 중인 공급업체 클라이언트측 코드(태그)가 없는 경우 해당 ID에 어떻게 액세스할 수 있습니까?

일부 공급업체는 서드파티 쿠키 없이 새로운 세상을 위해 시스템을 변경하고 있습니다. 이러한 변경 사항에는 [UUID](https://developer.mozilla.org/en-US/docs/Glossary/UUID) 또는 기타 [고객 생성 ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html)와 같은 대체 고유 식별자 사용이 포함됩니다. 공급업체에서 고객 생성 ID를 허용하는 경우 클라이언트에서 웹 또는 모바일 SDK를 사용하여 플랫폼 Edge Network으로 보내거나 이벤트 전달 시 API 호출에서 받을 수 있습니다. 이벤트 전달 규칙에서 해당 공급업체에 데이터를 보낼 때 필요에 따라 해당 식별자를 포함하기만 하면 됩니다.

공급업체가 자체 클라이언트측 태그만 생성하거나 액세스할 수 있는 데이터(예: 공급업체별 고유 ID)를 필요로 하는 경우 해당 공급업체 태그는 이동하기에 적합하지 않을 수 있습니다. _적절한 API 없이 해당 데이터 수집을 이벤트 전달로 이동한다는 생각으로 클라이언트측 태그를 리버스 엔지니어링하려는 것은 권장되지 않습니다._

[Adobe Experience Platform Cloud Connector](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/cloud-connector/overview.html) 확장은 서버 간 이벤트 데이터 전송에 적합한 API를 가진 공급업체를 통해 필요에 따라 HTTP 요청을 할 수 있습니다. 공급업체별 확장은 좋은 기능이며 더 많은 확장이 현재 활성 개발 중인 상태이지만, 추가적인 공급업체 확장을 기다리지 않고 Cloud Connector 확장을 사용하여 이벤트 전달 규칙을 구현할 수 있습니다.

## 도구 {#tools}

[Postman](https://www.postman.com/)와 같은 도구 또는 Visual Studio Code [Thunder Client](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client) 또는 [HTTP Client](https://marketplace.visualstudio.com/items?itemName=mkloubert.vscode-http-client)와 같은 텍스트 편집기 확장을 사용하면 공급업체 API 끝점을 더 쉽게 조사하고 테스트할 수 있습니다.

## 다음 단계 {#next-steps}

이 문서에서는 공급업체 클라이언트측 태그를 평가하고 이벤트 전달 속성에서 서버측으로 이동할 수 있는 일련의 단계를 제공했습니다. 관련 항목에 대한 자세한 내용은 다음 링크를 참조하십시오.

- Adobe Experience Platform의 [태그 관리](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)
- 서버측 처리를 위한 [이벤트 전달](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)
- 데이터 수집에서 [용어 업데이트](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html)
