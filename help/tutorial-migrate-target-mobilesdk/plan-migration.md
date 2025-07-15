---
title: 마이그레이션 계획 - 모바일 앱의 Adobe Target 구현을 Offer Decisioning 및 Target 확장으로 마이그레이션
description: at.js와 Platform Web SDK 간의 주요 차이점과 마이그레이션 노력을 계획하는 방법에 대해 알아봅니다.
exl-id: 86849319-d2ad-4338-aa1a-d307d8807d4a
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# 마이그레이션 계획

Target 확장에서 Offer Decisioning 및 Target 확장으로 마이그레이션하는 작업의 수준은 현재 구현과 사용된 Target 기능의 복잡성에 따라 다릅니다.

구현이 아무리 간단하거나 복잡하더라도 마이그레이션 전에 현재 상태를 완전히 이해하는 것이 중요합니다. 이 안내서는 현재 구현의 구성 요소를 분류하고 각 요소를 마이그레이션하는 관리 가능한 계획을 개발하는 데 도움이 됩니다.

마이그레이션 프로세스에는 다음과 같은 주요 단계가 포함됩니다.

1. 현재 구현 평가 및 마이그레이션 접근 방식 결정
1. Adobe Experience Platform Edge Network에 연결하도록 초기 구성 요소 설정
1. Target 확장을 Offer Decisioning 및 Target 확장으로 대체하도록 기본 구현을 업데이트합니다
1. 특정 사용 사례에 맞게 SDK 최적화 구현을 개선합니다. 여기에는 추가 매개 변수 전달, 응답 토큰 사용 등이 포함될 수 있습니다.
1. 프로필 스크립트, 활동 및 대상 정의와 같은 Target 인터페이스의 객체 업데이트
1. 프로덕션 앱에서 전환하기 전에 최종 구현의 유효성을 검사합니다.

>[!INFO]
>
>Adobe Experience Platform Mobile SDK 생태계 내에서 확장은 다른 이름을 가질 수 있는 애플리케이션에 가져온 SDK에 의해 구현됩니다.
>
> * **Target SDK**&#x200B;이(가) **Adobe Target 확장**&#x200B;을 구현함
> * **SDK 최적화**&#x200B;에서 **Offer Decisioning 및 Target 확장 구현**


그런 다음 Target 확장과 Offer Decisioning 및 Target 확장의 자세한 [비교](detailed-comparison.md)를 검토하여 기술적인 차이점을 더 잘 이해하고 추가 포커스가 필요한 영역을 식별하십시오.

>[!NOTE]
>
>Target 확장에서 Offer Decisioning 및 Target 확장으로 모바일 Target 마이그레이션을 성공적으로 수행할 수 있도록 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484#M625)에 게시하여 알려 주십시오.
