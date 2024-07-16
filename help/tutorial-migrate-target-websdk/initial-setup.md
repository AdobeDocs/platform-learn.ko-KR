---
title: 초기 설정 | Target을 at.js 2.x에서 Web SDK로 마이그레이션
description: 플랫폼 웹 SDK 구현에 필요한 중요한 기본 요소에 대해 알아보고 설정합니다
exl-id: dbf9683b-1cfc-474a-9c38-432cad4d1533
source-git-commit: 4690d41f92c83fe17eda588538d397ae1fa28af0
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# 초기 데이터 수집 설정 수행

at.js에서 Platform Web SDK로 마이그레이션하려면 Platform Web SDK의 적절한 데이터 캡처, 기능 및 기능을 활성화하기 위한 초기 설정이 필요합니다. 웹 사이트 구현을 변경하기 전에 [Platform Web SDK 구현 자습서](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=ko-KR)의 다음 단계를 완료해야 합니다.

- 데이터 수집을 위해 Adobe Admin Console에서 [적절한 사용 권한을 구성](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-permissions.html){target="_blank"}
- 구조화된 데이터를 Edge Network에 전달하기 위한 [XDM 스키마 구성](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-schemas.html){target="_blank"}
- 장치 간 개인 설정 및 mbox3rdPartyId 기능을 위해 [ID 네임스페이스를 구성](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities.html){target="_blank"}
- Edge Network에서 데이터 전달을 사용하려면 [데이터 스트림을 만듭니다](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-datastream.html){target="_blank"}
- Adobe Target에 데이터를 전달할 수 있도록 [데이터 스트림을 구성](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html#configure-the-datastream){target="_blank"}

>[!CAUTION]
>
>이러한 설계 측면은 Target, Analytics 및 Audience Manager 마이그레이션 간에 조정되어야 합니다.

초기 구성이 완료되면 Adobe Experience Platform Edge Network을 사용하여 Target 기능을 활성화해야 합니다.

다음으로, [at.js 라이브러리를 바꾸고 기본 Platform Web SDK 구현을 설정하는 방법](replace-library.md)을 알아봅니다.

>[!NOTE]
>
>at.js에서 Web SDK로 Target을 성공적으로 마이그레이션할 수 있도록 지원하기 위해 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)에 게시하여 알려 주십시오.
