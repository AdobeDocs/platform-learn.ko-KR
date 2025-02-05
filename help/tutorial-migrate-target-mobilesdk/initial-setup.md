---
title: 초기 설정 - Adobe Target에서 Adobe Journey Optimizer - Decisioning Mobile 확장 기능으로 마이그레이션
description: Platform Web SDK 구현에 필요한 중요한 기본 요소에 대해 알아보고 설정합니다
exl-id: dfc5abc8-0e79-454a-b1bb-6a42b1219771
source-git-commit: f3fd5f45412900dcb871bc0b346ce89108fa8913
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 5%

---

# 초기 데이터 수집 설정 수행

Target SDK에서 SDK 최적화로 마이그레이션하려면 Optimize SDK의 적절한 데이터 캡처, 기능 및 기능을 활성화하는 초기 설정이 필요합니다. 웹 사이트 구현 변경이 수행되기 전에 다음 단계를 완료해야 합니다.

- 데이터 수집을 위해 Adobe Admin Console에서 [적절한 사용 권한을 구성](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/overview#prerequisites){target="_blank"}
- 구조화된 데이터를 Edge Network에 전달하기 위한 [XDM 스키마 구성](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-schema){target="_blank"}
- Adobe Target 데이터를 받도록 [스키마를 구성](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-your-schema)
- 장치 간 개인 설정 및 mbox3rdPartyId 기능을 위해 [ID 네임스페이스를 구성](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/app-implementation/identity#set-up-a-custom-identity-namespace){target="_blank"}
- Edge Network에서 데이터 전달을 사용하려면 [데이터 스트림을 만듭니다](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-datastream){target="_blank"}
- Adobe Target에 데이터를 전달할 수 있도록 [데이터 스트림을 구성](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-datastream-configuration){target="_blank"}
- Decisioning 확장에 대한 [태그 속성 구성](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#install-adobe-journey-optimizer---decisioning-tags-extension)

>[!BEGINTABS]

>[!TAB 대상 확장]

Target 확장을 사용할 때 설치된 태그 확장:

1. Mobile Core
1. 프로필
1. Adobe Target
1. Adobe Analytics (선택 사항, Adobe Target 활동을 위한 보고 소스로 Adobe Analytics을 사용하는 경우 필요)

![Target 확장을 사용할 때 설치된 태그 확장](assets/tag-extensions-target.png)


>[!TAB Decisioning 확장]

Decisioning 확장을 사용할 때 설치된 태그 확장:

1. Mobile Core
1. 프로필
1. 동의
1. ID
1. Adobe Experience Platform Edge Network
1. Adobe Journey Optimizer - Decisioning
1. AEP Assurance (선택 사항, 디버깅에 필요)

![Decisioning 확장을 사용할 때 설치된 태그 확장](assets/tag-extensions-decisioning.png)


>[!ENDTABS]

다음으로, [at.js 라이브러리를 바꾸고 기본 Platform Web SDK 구현을 설정하는 방법](replace-library.md)을 알아봅니다.

>[!NOTE]
>
>Target 확장에서 Decisioning 확장으로 모바일 Target을 성공적으로 마이그레이션할 수 있도록 지원하기 위해 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)에 게시하여 알려 주십시오.
