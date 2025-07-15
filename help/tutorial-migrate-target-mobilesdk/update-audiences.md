---
title: Target 대상 및 프로필 스크립트 업데이트 - 모바일 앱의 Adobe Target 구현을 Offer Decisioning 및 Target 확장으로 마이그레이션합니다.
description: Offer Decisioning 및 Target 확장과의 호환성을 위해 Adobe Target 대상 및 프로필 스크립트를 업데이트하는 방법을 알아봅니다.
exl-id: de3ce2c7-0066-496a-a8a7-994d7ce3d92c
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# Decisioning 모바일 확장 호환성에 대한 Target 대상 및 프로필 스크립트 업데이트


Target을 Offer Decisioning 및 Target 확장으로 마이그레이션하는 기술 업데이트를 완료한 후 원활한 전환을 위해 대상, 프로필 스크립트 및 활동 일부를 업데이트해야 할 수 있습니다.

>[!INFO]
>
>모든 mbox 매개 변수를 `data.__adobe.target` 개체로 마이그레이션하는 경우 아래와 같이 대상, 프로필 스크립트 및 활동을 업데이트할 필요가 없습니다.


mbox 매개 변수를 `xdm` 개체로 마이그레이션하는 경우 변경 내용을 프로덕션에 게시하기 전에 다음을 수행해야 합니다.

* mbox 매개 변수를 사용하는 대상자 업데이트
* mbox 매개 변수를 사용하는 프로필 스크립트 업데이트
* mbox 매개 변수 토큰 대체를 사용하는 모든 오퍼 및 활동을 업데이트하십시오(예: `${mbox.parameter_name}`).

## 대상자 조정

mbox 매개 변수를 `xdm` 개체로 마이그레이션하는 경우 사용자 지정 mbox 매개 변수를 사용하는 대상을 업데이트하여 새 XDM 매개 변수 이름을 사용해야 합니다. 예를 들어 `page_name`에 대한 사용자 지정 매개 변수가 `web.webpagedetails.pageName`에 매핑될 수 있습니다.

Target 확장과 Offer Decisioning 및 Target 확장 모두와의 호환성을 보장하기 위한 한 가지 접근 방법은 아래와 같이 `OR` 조건이 사용되도록 관련 대상을 업데이트하는 것입니다.

![Offer Decisioning 및 Target 확장 호환성에 대한 Target 대상 업데이트를 보는 방법](assets/target-audience-update.png){zoomable="yes"}

## 프로필 스크립트 편집

mbox 매개 변수를 `xdm` 개체로 마이그레이션하는 경우 대상과 유사한 새 XDM 매개 변수 이름을 참조하도록 프로필 스크립트를 업데이트해야 합니다. mbox 매개 변수 이름을 변경해도 Target과 Decisioning 구현 간에 프로필 스크립트가 작동하는 방식에는 차이가 없습니다.

호환성을 확인하는 한 가지 방법은 프로필 스크립트 코드에서 `OR` 조건을 사용하는 것입니다.

프로필 스크립트 예:

```Javascript
if(mbox.param('pageName') == 'Product Details'){
  return true
}
```

Platform Web SDK 호환성을 위한 프로필 스크립트가 업데이트되었습니다.

```Javascript
if((mbox.param('pageName') == 'Product Details') || (mbox.param('web.webPageDetails.pageName') =='Product Details')){
  return true
}
```

자세한 내용과 모범 사례는 [프로필 스크립트](https://experienceleague.adobe.com/ko/docs/target/using/audiences/visitor-profiles/profile-parameters)에 대한 전용 설명서를 참조하세요.

## 다이내믹 컨텐츠에 대한 매개 변수 토큰 업데이트

mbox 매개 변수를 `xdm` 개체로 마이그레이션하는 경우 [동적 콘텐츠 대체](https://experienceleague.adobe.com/ko/docs/target/using/experiences/offers/passing-profile-attributes-to-the-html-offer)를 사용하는 오퍼, 권장 사항 디자인 또는 활동이 있으면 새 XDM 매개 변수 이름을 고려하여 그에 따라 업데이트해야 할 수 있습니다.

mbox 매개 변수에 토큰 교체를 사용하는 방법에 따라 기존 설정을 개선하여 이전 매개 변수와 새 매개 변수 이름을 모두 고려할 수 있습니다. 그러나 JSON 오퍼에서와 같이 사용자 정의 JavaScript 코드를 사용할 수 없는 상황에서는 마이그레이션이 완료된 후 프로덕션 사이트에서 라이브를 만들고 사본을 만들어야 합니다.

JSON 오퍼 예:

```JSON
{
  "pageName" : "${mbox.page_name}",
  "layoutVariation" : "grid"
}
```

XDM 개체 매개 변수 이름을 사용하는 JSON 오퍼의 예:

```JSON
{
  "pageName" : "${mbox.web.webPagedDetails.pageName}",
  "layoutVariation" : "grid"
}
```

마이그레이션 후 새 XDM mbox 매개 변수 이름을 고려하도록 조정하는 경우, 마이그레이션 이벤트 중에 영향을 받는 활동을 일시 중지하여 방문자에 대한 활동 표시 오류를 방지해야 합니다.


다음으로 [Target 구현의 유효성을 검사](validate.md)하는 방법을 알아봅니다.

>[!NOTE]
>
>Target 확장에서 Offer Decisioning 및 Target 확장으로 모바일 Target 마이그레이션을 성공적으로 수행할 수 있도록 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=ko#M463)에 게시하여 알려 주십시오.
