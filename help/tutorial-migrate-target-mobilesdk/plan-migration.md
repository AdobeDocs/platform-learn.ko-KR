---
title: Planning - 모바일 앱의 Target을 Target 확장에서 Optimize 확장으로 마이그레이션
description: at.js 2.x에서 Adobe Experience Platform Web SDK로 Adobe Target 구현을 계획하는 방법에 대해 알아봅니다.
source-git-commit: 009548969b88d1bfa6eac23f65b1ca2144f27c34
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# Optimize 확장으로의 Target 마이그레이션 계획

Target 확장에서 모바일 앱의 최적화 확장으로 Target을 업그레이드하기 전에 현재 구현을 평가해야 합니다.

## 현재 Target 확장 구현 평가

성공적인 마이그레이션을 위한 첫 번째 단계는 현재 Target 확장 구현을 확실히 이해하는 것입니다. 업데이트가 필요한 기능, 함수 및 사용자 지정 코드를 사용할 수 있습니다. 평가할 때 다음 사항을 고려하십시오.

### 지원되는 기능은 무엇입니까?

<!--Platform Web SDK is under continuous active development and features and enhancements are added regularly. As you evaluate your current at.js implementation, refer to the [supported use cases](https://github.com/orgs/adobe/projects/18/views/1) page for the latest information.-->

### 오늘은 어떤 기능을 사용하나요?

<!--Platform Web SDK is a new library that consolidates all Adobe solutions for the websites into a single SDK. This enables tighter integration and enables new capabilities unique to Adobe Experience Platform. However, this also means at.js functions are not backwards compatible with Platform Web SDK. As you evaluate your current implementation, make note of the following:

- at.js functions such as `getOffer()` and `applyOffer()`
- Modifications to Target's global settings
- Integration with Adobe Analytics
- Use of a flicker mitigation script
- Use of response tokens
- Use of mbox, profile, and entity parameters
- Custom code unique to your implementation-->

### 어떤 마이그레이션 방식을 선택하시겠습니까?

<!--Once you have revisited your at.js implementation, you need to determine a migration approach. There are two options:

- Migrate all Adobe applications at once across the entire site
- Migrate on a page-by-page basis

Because Platform Web SDK combines and enables multiple Adobe applications, you must coordinate the Target migration of other Adobe applications like Analytics and Audience Manager. All Adobe libraries on a given page should be migrated at the same time. A mixed implementation of Platform Web SDK for Target and AppMeasurement for Analytics on a particular page is not supported. However, a mixed implementation across different pages is supported, for example Platform Web SDK on page A, and at.js with AppMeasurement on page B.

As you migrate, you should plan on following your company's process for testing and releasing new code and use things like development, qa, and staging environments before you release to production.-->

<!--
>[!CAUTION]
>
>Redirect offers are not supported in page-by-page migrations if redirecting from a page with one library to a page with a different library
-->


그런 다음 Target 확장과 Optimize 확장에 대한 자세한 [비교](detailed-comparison.md)를 검토하여 기술적 차이점을 더 잘 이해하고 추가 포커스가 필요한 영역을 식별하십시오.

>[!NOTE]
>
>Target 확장에서 최적화 확장으로 모바일 Target을 성공적으로 마이그레이션할 수 있도록 지원하기 위해 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)에 게시하여 알려 주십시오.
