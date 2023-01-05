---
title: 초기 설정 | at.js 2.x에서 웹 SDK로 Target 마이그레이션
description: Platform Web SDK 구현에 필요한 중요한 기본 요소에 대해 알아보고 설정합니다
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 2%

---

# 초기 데이터 수집 설정 수행

at.js에서 Platform Web SDK로 마이그레이션하려면 Platform Web SDK의 적절한 데이터 캡처, 기능 및 기능을 활성화하기 위한 초기 설정이 필요합니다. 다음 단계는 [Platform 웹 SDK 구현 자습서](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=ko-KR) 웹 사이트 구현이 변경되기 전에 완료해야 합니다.

- [적절한 권한 구성](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-permissions.html)데이터 수집을 위한 Adobe Admin Console의 {target=&quot;_blank&quot;}
- [XDM 스키마 구성](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-schemas.html)Edge 네트워크에 구조화된 데이터를 전달할 {target=&quot;_blank&quot;}
- [ID 네임스페이스 구성](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities.html)교차 장치 개인화 및 mbox3rdPartyId 기능에 대한 {target=&quot;_blank&quot;}
- [데이터 스트림 만들기](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-datastream.html)Edge Network에서 데이터 전달을 사용하도록 설정하려면 {target=&quot;_blank&quot;}
- [데이터 스트림 구성](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html#configure-the-datastream)Adobe Target에 데이터를 전달하도록 하려면 {target=&quot;_blank&quot;}

>[!CAUTION]
>
>웹 SDK의 이러한 디자인 측면은 Target, Analytics 및 Audience Manager 마이그레이션 간에 조정되어야 합니다.

초기 구성이 완료되면 Adobe Experience Platform Edge 네트워크를 사용하여 Target 기능을 활성화해야 합니다.

다음으로, 다음 방법을 배웁니다. [at.js 라이브러리를 바꾸고 기본 Platform Web SDK 구현을 설정합니다](replace-library.md).

>[!NOTE]
>
>Adobe는 at.js에서 웹 SDK로 Target 마이그레이션을 성공적으로 수행할 수 있도록 최선을 다하고 있습니다. 마이그레이션에 문제가 발생했거나 이 안내서에 중요한 정보가 누락된 것 같은 경우에는 로그인한 후 알려 주십시오 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
