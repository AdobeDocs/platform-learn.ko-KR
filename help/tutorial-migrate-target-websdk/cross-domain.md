---
title: 도메인 간 지원 활성화 | at.js 2.x에서 웹 SDK로 Target 마이그레이션
description: Experience Platform Web SDK를 사용하여 도메인 간 및 모바일 앱과 웹 브라우저 시나리오에 대한 Adobe Target을 구성하는 방법을 알아봅니다.
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# 도메인 간 방문자 프로필 활성화

Platform Web SDK는 고객이 도메인 간에 개인화된 경험을 보다 정확하게 제공할 수 있도록 해주는 방문자 ID 공유 기능을 지원합니다. 이 기능을 사용하면 타사 쿠키에 의존하지 않고 도메인 간에 일관된 개인화를 제공하고 방문자 활동 보고의 정확도를 높일 수 있습니다.

## 전제 조건

도메인 간 ID 공유를 사용하려면 Platform Web SDK 버전 2.11.0 이상을 사용해야 합니다. 이 기능은 VisitorAPI.js 버전 1.7.0 이상과도 호환됩니다.

도메인 간 ID 공유는 특수 기능을 추가하여 작동합니다 `adobe_mc` 대상 도메인의 URL에 대한 쿼리 문자열 매개 변수입니다. 이 매개 변수는 새 ID를 생성하거나 기존 ID를 사용하는 대신 방문자 ID를 지정하는 데 사용됩니다.

대상 도메인은 도메인 간 ID 공유를 위해 이러한 라이브러리 중 하나를 사용해야 합니다 `adobe_mc` 매개 변수를 사용하여 방문자 ID를 적절하게 공유하십시오.

## 접근 방식 비교

구현하기 전에 먼저 기존 구현에서 `visitor.appendVisitorIDsTo()` 함수 위에 있어야 합니다. 이 함수를 사용하는 모든 사용자 지정 코드는 새 `appendIdentityToUrl` 웹 SDK 명령.

| VisitorAPI.js | Platform 웹 SDK |
| --- | --- |
| `visitor.appendVisitorIDsTo(*url*)` | `alloy("appendIdentityToUrl", { url: *url* })` |

## 사용 `appendIdentityToURL` 명령

도메인 간 ID 공유의 경우 웹 SDK 버전 2.11.0에 대한 지원을 추가합니다 `appendIdentityToUrl` 명령. 이 명령을 사용하면 `adobe_mc` 쿼리 문자열 매개 변수가 포함된 랜딩 페이지 URL이 있는지 확인합니다.

명령은 하나의 속성이 있는 개체를 허용합니다. `url`를 반환하고 속성 url이 있는 개체를 반환합니다.

이 명령은 동의 업데이트를 기다리지 않습니다. 동의를 제공하지 않은 경우 URL은 변경되지 않고 반환됩니다.

ECID를 제공하지 않으면 `/acquire` ecid를 생성하기 위해 종단점이 호출됩니다.

다음은 도메인 간 ID 공유를 구현하는 방법의 예입니다.

이 코드는 페이지의 모든 클릭 수에 대한 이벤트 리스너를 추가합니다. 클릭이 일치하는 도메인에 대한 링크에 있었던 경우, 이 경우 adobe.com 또는 behance.com에서는 ID를 URL에 추가하고 해당 사용자가 해당 도메인에 리디렉션됩니다.

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
>태그 기능(이전 Launch)을 사용하여 웹 SDK를 구현하는 경우 사용자 지정 코드 없이 도메인 간 ID 공유를 수행할 수 있습니다. 자세한 내용은 [전용 설명서](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html#tags-extension) 자세한 내용

>[!NOTE]
>
>Platform Web SDK는 기본 모바일 앱 사용 사례를 위한 모바일-웹 ID 공유도 지원합니다. 자세한 내용은 [mobile-to-web 및 cross-domain ID 공유](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html).

다음으로, 다음 방법을 배웁니다. [대상자 및 프로필 스크립트 업데이트](update-audiences.md) 플랫폼 웹 SDK와의 호환성을 위해 입니다.

>[!NOTE]
>
>Adobe는 at.js에서 웹 SDK로 Target 마이그레이션을 성공적으로 수행할 수 있도록 최선을 다하고 있습니다. 마이그레이션에 문제가 발생했거나 이 안내서에 중요한 정보가 누락된 것 같은 경우에는 로그인한 후 알려 주십시오 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).