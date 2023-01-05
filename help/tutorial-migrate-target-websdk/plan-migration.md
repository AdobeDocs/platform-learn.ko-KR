---
title: 계획 | at.js 2.x에서 웹 SDK로 Target 마이그레이션
description: at.js 2.x에서 Adobe Experience Platform Web SDK로 Adobe Target 구현을 계획하는 방법을 알아봅니다.
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# at.js에서 Platform Web SDK로의 마이그레이션을 계획합니다

사이트에서 Platform Web SDK로 업그레이드하기 전에 현재 구현을 평가해야 합니다.

## 현재 at.js 구현 평가

성공적인 마이그레이션의 첫 번째 단계는 현재 at.js Target 구현을 명확하게 이해하는 것입니다. 업데이트가 필요한 기능, 함수 및 사용자 지정 코드를 사용할 수 있습니다. 평가할 때 다음 사항을 고려하십시오.

### 지원되는 기능은 무엇입니까?

Platform Web SDK는 지속적으로 활성 개발 중이며 기능 및 개선 사항이 정기적으로 추가됩니다. 현재 at.js 구현을 평가할 때 [지원되는 사용 사례](https://github.com/orgs/adobe/projects/18/views/1) 페이지를 참조하십시오.

### 오늘은 어떤 기능을 사용하십니까?

Platform Web SDK는 웹 사이트의 모든 Adobe 솔루션을 단일 SDK로 통합하는 새로운 라이브러리입니다. 이를 통해 보다 긴밀해진 통합을 가능하게 하고 Adobe Experience Platform 고유의 새로운 기능을 사용할 수 있습니다. 그러나 at.js 함수가 Platform Web SDK와 이전 버전과 호환되지 않음을 의미합니다. 현재 구현을 평가할 때 다음을 참고하십시오.

- at.js 함수(예: ) `getOffer()` 및 `applyOffer()`
- Target의 전역 설정 수정
- Adobe Analytics와의 통합
- 플리커 완화 스크립트 사용
- 응답 토큰 사용
- mbox, 프로필 및 엔티티 매개 변수 사용
- 구현에 고유한 사용자 지정 코드

### 어떤 마이그레이션 방법을 사용합니까?

at.js 구현을 다시 방문한 후에는 마이그레이션 방법을 결정해야 합니다. 다음 두 가지 옵션을 사용할 수 있습니다.

- 전체 사이트에서 모든 Adobe 애플리케이션을 한 번에 마이그레이션
- 페이지별 마이그레이션

Platform Web SDK는 여러 Adobe 응용 프로그램을 결합하고 활성화하므로 Analytics 및 Audience Manager과 같은 다른 Adobe 응용 프로그램의 Target 마이그레이션을 조정해야 합니다. 지정된 페이지의 모든 Adobe 라이브러리는 동시에 마이그레이션해야 합니다. Target용 Platform Web SDK와 특정 페이지의 AppMeasurement for Analytics의 혼합 구현은 지원되지 않습니다. 그러나 페이지 A의 Platform Web SDK, 페이지 B의 AppMeasurement가 있는 at.js 등 여러 페이지에 걸쳐 혼합 구현이 지원됩니다.

마이그레이션을 수행할 때 새 코드를 테스트 및 릴리스하기 위한 회사의 프로세스를 따를 계획이며 프로덕션에 릴리스하기 전에 개발, qa 및 스테이징 환경과 같은 환경을 사용해야 합니다.

>[!CAUTION]
>
>한 라이브러리가 있는 페이지에서 다른 라이브러리가 있는 페이지로 리디렉션하는 경우 리디렉션 오퍼가 페이지별 마이그레이션에서 지원되지 않습니다


그런 다음 자세한 내용을 검토합니다 [at.js와 Platform Web SDK 비교](detailed-comparison.md) 기술적 차이점을 더 잘 이해하고 추가 포커스가 필요한 영역을 파악합니다.

>[!NOTE]
>
>Adobe는 at.js에서 웹 SDK로 Target 마이그레이션을 성공적으로 수행할 수 있도록 최선을 다하고 있습니다. 마이그레이션에 문제가 발생했거나 이 안내서에 중요한 정보가 누락된 것 같은 경우에는 로그인한 후 알려 주십시오 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
