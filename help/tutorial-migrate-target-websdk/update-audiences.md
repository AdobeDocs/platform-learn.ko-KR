---
title: 대상자 및 프로필 스크립트 업데이트 | at.js 2.x에서 웹 SDK로 Target 마이그레이션
description: Experience Platform Web SDK와의 호환성을 위해 Adobe Target 대상 및 프로필 스크립트를 업데이트하는 방법을 알아봅니다.
source-git-commit: 43740912bc5a941aa21c5f38ed2c1aac74abffbc
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---

# Platform Web SDK 호환성을 위해 Target 대상 및 프로필 스크립트 업데이트

Platform Web SDK로 Target을 마이그레이션하기 위한 기술 업데이트를 완료한 후 일부 대상, 프로필 스크립트 및 활동을 업데이트하여 원활하게 전환할 수 있습니다.

모든 Target mbox 매개 변수는 Platform Web SDK 구현과 함께 XDM 형식으로 전달해야 합니다. 프로덕션에 변경 사항을 게시하기 전에 다음을 수행해야 합니다.

* mbox 매개 변수를 사용하는 대상 업데이트
* mbox 매개 변수를 사용하는 프로필 스크립트 업데이트
* 모든 오퍼 및 활동을 업데이트하여 mbox 매개 변수 토큰 대체를 사용합니다(예: `${mbox.parameter_name}`)


>[!WARNING]
>
> 2022년 10월 1일 이후에 시작된 Platform Web SDK 구현은 [미리 가져오기 해결 방법](prefetch-workaround.md) 를 사용하여 이 페이지에 설명된 기능 중 일부를 성공적으로 사용할 수 있습니다.

## 대상자 조정

사용자 지정 mbox 매개 변수를 사용하는 모든 대상은 새 XDM 매개 변수 이름을 사용하도록 업데이트해야 합니다. 예를 들어 `page_name` 에 매핑되어 있을 수 있음 `web.webpagedetails.pageName`.

at.js 및 Platform Web SDK와의 호환성을 보장하는 한 가지 접근 방법은 다음과 같이 관련 대상을 업데이트하여 `OR` 조건은 아래와 같이 사용됩니다.

![Platform Web SDK 호환성을 위해 Target 대상자 업데이트를 보는 방법](assets/target-audience-update.png)

## 프로필 스크립트 편집

프로필 스크립트는 대상과 유사하게 새 XDM 매개 변수 이름을 참조하도록 업데이트해야 합니다. mbox 매개 변수 이름 변경 외에도 at.js와 Platform Web SDK 구현 간에 프로필 스크립트가 작동하는 방식에는 차이가 없습니다.

한 가지 방법은 호환성이 `OR` 프로필 스크립트 코드의 조건입니다.

프로필 스크립트 예:

```Javascript
if(mbox.param('pageName') == 'Product Details'){
  return true
}
```

Platform Web SDK 호환성을 위한 프로필 스크립트가 업데이트되었습니다.

```Javascript
if((mbox.param('pageName') == 'Product Details') || (mbox.param('page.webpagedetails.pageName') =='Product Details')){
  return true
}
```

자세한 내용 및 우수 사례가 필요하면 [프로필 스크립트](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html).

## 동적 컨텐츠에 대한 매개 변수 토큰 업데이트

를 사용하는 오퍼, 권장 사항 디자인 또는 활동이 있는 경우 [동적 콘텐츠 대체](https://experienceleague.adobe.com/docs/target/using/experiences/offers/passing-profile-attributes-to-the-html-offer.html)를 업데이트하면 새 XDM 매개 변수 이름을 참조할 수 있습니다.

mbox 매개 변수에 대한 토큰 대체를 사용하는 방법에 따라, 이전 및 새 매개 변수 이름을 모두 계산하도록 기존 설정을 향상시킬 수 있습니다. 그러나 JSON 오퍼에서와 같이 사용자 지정 JavaScript 코드가 불가능한 상황에서는 마이그레이션이 완료되고 프로덕션 사이트에서 활성 상태가 되면 복사본을 만들고 업데이트를 해야 합니다.

JSON 오퍼 예:

```JSON
{
  "pageName" : "${mbox.page_name}",
  "layoutVariation" : "grid"
}
```

Platform Web SDK 매개 변수 이름을 사용하는 JSON 오퍼 예:

```JSON
{
  "pageName" : "${mbox.web.webpagedetails.pageName}",
  "layoutVariation" : "grid"
}
```

새 XDM mbox 매개 변수 이름을 설명하기 위해 마이그레이션 후 조정을 선택하는 경우 마이그레이션 이벤트 동안 영향을 받은 활동을 일시 중지하여 활동 표시 오류가 방문자에게 표시되지 않도록 하십시오.

다음으로, 다음 방법을 배웁니다. [Target 구현의 유효성 검사](validate.md).

>[!NOTE]
>
>Adobe는 at.js에서 웹 SDK로 Target 마이그레이션을 성공적으로 수행할 수 있도록 최선을 다하고 있습니다. 마이그레이션에 문제가 발생했거나 이 안내서에 중요한 정보가 누락된 것 같은 경우에는 로그인한 후 알려 주십시오 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).