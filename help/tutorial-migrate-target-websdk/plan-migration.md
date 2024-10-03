---
title: Planning - Target을 at.js 2.x에서 Web SDK로 마이그레이션
description: at.js 2.x에서 Adobe Experience Platform Web SDK로 Adobe Target 구현을 계획하는 방법에 대해 알아봅니다.
exl-id: 0e8f9cde-f361-4f69-886d-aad3074cd9b2
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# at.js에서 Platform Web SDK로의 마이그레이션 계획

사이트에서 Platform Web SDK로 업그레이드하기 전에 현재 구현을 평가해야 합니다.

## 현재 at.js 구현 평가

성공적인 마이그레이션을 위한 첫 번째 단계는 현재 at.js Target 구현을 확실하게 이해하는 것입니다. 업데이트가 필요한 기능, 함수 및 사용자 지정 코드를 사용할 수 있습니다. 평가할 때 다음 사항을 고려하십시오.

### 지원되는 기능은 무엇입니까?

Platform Web SDK는 지속적으로 활성 개발 중이며, 정기적으로 기능 및 개선 사항이 추가됩니다. 현재 at.js 구현을 평가할 때 [지원되는 사용 사례](https://github.com/orgs/adobe/projects/18/views/1) 페이지에서 최신 정보를 참조하십시오.

### 오늘은 어떤 기능을 사용하나요?

Platform Web SDK 는 웹 사이트에 대한 모든 Adobe 솔루션을 단일 SDK로 통합하는 새로운 라이브러리입니다. 이를 통해 통합을 강화할 수 있으며 Adobe Experience Platform 고유의 새로운 기능을 사용할 수 있습니다. 그러나 at.js 함수는 Platform Web SDK와 이전 버전과 호환되지 않습니다. 현재 구현을 평가할 때 다음 사항에 유의하십시오.

- `getOffer()` 및 `applyOffer()` 같은 at.js 함수
- Target의 전역 설정에 대한 수정 사항
- Adobe Analytics와의 통합
- 깜박임 완화 스크립트 사용
- 응답 토큰 사용
- mbox, 프로필 및 엔티티 매개 변수 사용
- 구현에 고유한 사용자 지정 코드

### 어떤 마이그레이션 방식을 선택하시겠습니까?

at.js 구현을 다시 방문한 후에는 마이그레이션 접근 방식을 결정해야 합니다. 다음 두 가지 옵션이 있습니다.

- 전체 사이트에서 모든 Adobe 애플리케이션을 한 번에 마이그레이션
- 페이지별로 마이그레이션

Platform Web SDK는 여러 Adobe 애플리케이션을 결합하고 활성화하므로 Analytics 및 Audience Manager과 같은 다른 Adobe 애플리케이션의 Target 마이그레이션을 조정해야 합니다. 주어진 페이지의 모든 Adobe 라이브러리는 동시에 마이그레이션되어야 합니다. 특정 페이지에서 Target용 Platform Web SDK와 Analytics용 AppMeasurement의 혼합 구현은 지원되지 않습니다. 하지만 페이지 A의 Platform Web SDK와 페이지 B의 AppMeasurement이 있는 at.js 등의 서로 다른 페이지에 대한 혼합 구현이 지원됩니다.

마이그레이션하는 동안 새 코드를 테스트하고 릴리스하기 위한 회사의 프로세스 준수를 계획하고 프로덕션에 릴리스하기 전에 개발, qa 및 스테이징 환경과 같은 것을 사용해야 합니다.

>[!CAUTION]
>
>한 라이브러리가 있는 페이지에서 다른 라이브러리가 있는 페이지로 리디렉션하는 경우 리디렉션 오퍼는 페이지별 마이그레이션에서 지원되지 않습니다


그런 다음 at.js와 Platform Web SDK의 자세한 [비교](detailed-comparison.md)를 검토하여 기술적인 차이점을 더 잘 이해하고 추가 포커스가 필요한 영역을 식별하십시오.

>[!NOTE]
>
>at.js에서 Web SDK로 Target을 성공적으로 마이그레이션할 수 있도록 지원하기 위해 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)에 게시하여 알려 주십시오.
