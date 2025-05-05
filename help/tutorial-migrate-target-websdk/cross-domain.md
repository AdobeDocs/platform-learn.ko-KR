---
title: 도메인 간 지원 활성화 - Target을 at.js 2.x에서 Web SDK로 마이그레이션
description: Experience Platform Web SDK를 사용하여 도메인 간 및 모바일 앱용 Adobe Target을 웹 브라우저 시나리오에 맞게 구성하는 방법에 대해 알아봅니다.
exl-id: 6ec24ddc-8f6d-4331-a3ae-bd0f3a7d6e78
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# 도메인 간 방문자 프로필 활성화

Platform Web SDK는 고객이 도메인 간에 개인화된 경험을 보다 정확하게 제공할 수 있도록 하는 방문자 ID 공유 기능을 지원합니다. 이 기능을 사용하면 도메인 간에 일관된 개인화를 제공할 수 있으며 서드파티 쿠키에 의존하지 않고 방문자 활동 보고의 정확도를 향상시킬 수 있습니다.

## 전제 조건

도메인 간 ID 공유를 사용하려면 Platform Web SDK 버전 2.11.0 이상을 사용해야 합니다. 이 기능은 VisitorAPI.js 버전 1.7.0 이상과도 호환됩니다.

도메인 간 ID 공유는 대상 도메인의 URL에 특수 `adobe_mc` 쿼리 문자열 매개 변수를 추가하여 작동합니다. 이 매개 변수는 새 ID를 생성하거나 기존 ID를 사용하는 대신 방문자 ID를 지정하는 데 사용됩니다.

대상 도메인은 도메인 간 ID 공유에 이러한 라이브러리 중 하나를 사용하여 `adobe_mc` 매개 변수를 처리하고 방문자 ID를 올바르게 공유해야 합니다.

## 접근 방식 비교

구현하기 전에 먼저 기존 구현에서 `visitor.appendVisitorIDsTo()` 함수를 사용하는지 확인하십시오. 이 함수를 사용하는 모든 사용자 지정 코드는 새 `appendIdentityToUrl` Web SDK 명령을 사용하도록 업데이트해야 합니다.

| VisitorAPI.js | Platform Web SDK |
| --- | --- |
| `visitor.appendVisitorIDsTo(*url*)` | `alloy("appendIdentityToUrl", { url: *url* })` |

## `appendIdentityToURL` 명령 사용

도메인 간 ID 공유를 위해 Web SDK 버전 2.11.0은 `appendIdentityToUrl` 명령에 대한 지원을 추가합니다. 이 명령을 사용하면 `adobe_mc` 쿼리 문자열 매개 변수가 생성됩니다.

이 명령은 속성 `url`이(가) 있는 개체를 수락하고 속성 url이 있는 개체를 반환합니다.

이 명령은 동의 업데이트를 기다리지 않습니다. 동의를 제공하지 않은 경우 URL은 변경되지 않고 반환됩니다.

ECID를 제공하지 않으면 `/acquire` 끝점을 호출하여 ECID를 생성합니다.

다음은 도메인 간 ID 공유를 구현하는 방법의 예입니다.

이 코드는 페이지의 모든 클릭 수에 대한 이벤트 리스너를 추가합니다. 일치하는 도메인에 대한 링크(이 경우 adobe.com 또는 behance.com)를 클릭하면 URL에 ID가 추가되고 사용자가 해당 URL로 리디렉션됩니다.

```Javascript
document.addEventListener("click", event => {
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) {
    return;
  }
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith("adobe.com") && !url.hostname.endsWith("behance.com")) {
    return;
  }
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    document.location = result.url;
  });
});
```

>[!TIP]
>
>태그 기능(이전 Launch)을 사용하여 Web SDK를 구현하는 경우 사용자 지정 코드 없이 도메인 간 ID 공유를 수행할 수 있습니다. 자세한 내용은 [전용 설명서](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html?lang=ko#tags-extension)를 참조하세요.

>[!NOTE]
>
>Platform Web SDK는 기본 모바일 앱 사용 사례에 대해 모바일-웹 ID 공유도 지원합니다. 자세한 내용은 [Mobile-to-Web 및 도메인 간 ID 공유](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html?lang=ko)에 대한 전용 설명서를 참조하십시오.

다음으로 Platform Web SDK와의 호환성을 보장하기 위해 [대상 및 프로필 스크립트를 업데이트](update-audiences.md)하는 방법에 대해 알아봅니다.

>[!NOTE]
>
>at.js에서 Web SDK로 Target을 성공적으로 마이그레이션할 수 있도록 지원하기 위해 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=ko#M463)에 게시하여 알려 주십시오.
