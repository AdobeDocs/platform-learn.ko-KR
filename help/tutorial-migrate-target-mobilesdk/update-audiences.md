---
title: 대상자 및 프로필 스크립트 업데이트 - Target을 at.js 2.x에서 Web SDK로 마이그레이션
description: Experience Platform Web SDK와의 호환성을 위해 Adobe Target 대상 및 프로필 스크립트를 업데이트하는 방법을 알아봅니다.
source-git-commit: 009548969b88d1bfa6eac23f65b1ca2144f27c34
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Platform Web SDK 호환성을 위한 Target 대상자 및 프로필 스크립트 업데이트


## 대상자 조정


자세한 내용과 모범 사례는 [프로필 스크립트](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html)에 대한 전용 설명서를 참조하세요.

## 다이내믹 컨텐츠에 대한 매개 변수 토큰 업데이트



마이그레이션 후 새 XDM mbox 매개 변수 이름을 고려하도록 조정하는 경우, 마이그레이션 이벤트 중에 영향을 받는 활동을 일시 중지하여 방문자에 대한 활동 표시 오류를 방지해야 합니다.

다음으로 [Target 구현의 유효성을 검사](validate.md)하는 방법을 알아봅니다.

>[!NOTE]
>
>Target 확장에서 최적화 확장으로 모바일 Target을 성공적으로 마이그레이션할 수 있도록 지원하기 위해 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)에 게시하여 알려 주십시오.
