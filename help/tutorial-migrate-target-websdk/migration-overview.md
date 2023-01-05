---
title: 마이그레이션 개요 | at.js 2.x에서 웹 SDK로 Target 마이그레이션
description: at.js와 Platform Web SDK의 주요 차이점과 마이그레이션 작업을 계획하는 방법에 대해 알아봅니다.=
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 0%

---

# at.js에서 Platform Web SDK로 마이그레이션 Target 개요

at.js에서 Platform Web SDK로 마이그레이션하기 위한 작업 수준은 사용되는 현재 구현 및 제품 기능의 복잡성에 따라 다릅니다.

구현이 간단하거나 복잡하더라도 마이그레이션하기 전에 현재 상태를 완전히 이해하는 것이 중요합니다. 이 안내서는 현재 구현의 구성 요소를 분류하고 각 조각을 마이그레이션하기 위한 관리 가능한 계획을 개발하는 데 도움이 됩니다.

마이그레이션 프로세스에는 다음 주요 단계가 포함됩니다.

1. 현재 구현을 평가하고 마이그레이션 방법을 결정합니다
1. Adobe Experience Platform Edge 네트워크에 연결할 초기 구성 요소를 설정합니다
1. 기본 구현을 업데이트하여 at.js를 Platform Web SDK로 바꿉니다
1. 특정 사용 사례에 대한 Platform Web SDK 구현을 개선합니다. 여기에는 추가 매개 변수 전달, 단일 페이지 앱(SPA) 보기 변경 사항 처리, 응답 토큰 사용 등이 포함될 수 있습니다.
1. 프로필 스크립트, 활동 및 대상 정의 등 Target 인터페이스에서 개체를 업데이트합니다
1. 프로덕션 환경에서 전환하기 전에 최종 구현의 유효성 검사

## at.js와 Platform Web SDK의 주요 차이점

마이그레이션 프로세스를 시작하기 전에 at.js와 Platform Web SDK의 차이점을 이해하는 것이 중요합니다.

### 운영 차이점

Platform 웹 SDK는 여러 Adobe 애플리케이션의 기능을 단일 라이브러리로 결합합니다. 이러한 통합 접근 방식은 팀 간의 책임과 프로세스를 고려하여 원활한 구현을 보장해야 함을 의미합니다.

|  | at.js 2.x Target | Platform 웹 SDK |
|---|---|---|
| 소유권 | at.js 라이브러리는 다른 애플리케이션 라이브러리와 독립적입니다. 이러한 서로 다른 라이브러리의 사용자 지정 및 소유권은 조직의 서로 다른 팀에 적합할 수 있습니다. | Platform 웹 SDK 라이브러리와 전달된 데이터는 모든 Adobe 애플리케이션에 대해 통합됩니다. Platform Web SDK 구현의 소유권은 모든 다운스트림 애플리케이션의 이해 당사자를 나타내야 합니다. |
| 유지 관리 | 별도의 팀이 Target 및 Analytics와 같은 각 Adobe 애플리케이션에 대한 구현 개선 작업에 참여할 수 있습니다. | 이상적으로는 단일 팀이 Platform Web SDK 구현에 영향을 주는 개선 사항을 담당해야 합니다. |
| 프로세스 | Target 구현을 변경하면 Analytics와 같은 다른 응용 프로그램과 비교하여 다른 케이던스 또는 QA 요구 사항이 있는 프로세스를 따를 수 있습니다. | Platform Web SDK 구현을 변경하면 모든 다운스트림 애플리케이션을 고려해야 하며 QA 및 게시 프로세스를 그에 따라 조정해야 합니다. |
| 공동 작업 | Target 관련 데이터는 Target 호출에서 직접 전달할 수 있습니다. 구현에 따라 추가적인 Target 호출이 있을 수 있습니다. 이 작업은 Adobe Analytics 데이터에 직접적인 영향을 주지 않으며 분석 팀과의 조정도 중요하지 않습니다. | Platform Web SDK 호출에서 전달된 데이터는 Target 및 Analytics 모두에 전달할 수 있습니다. 변경 사항이 특정 애플리케이션에 부정적인 영향을 주지 않도록 하려면 팀 간의 조정이 필요합니다. |

### 기술적 차이점

Platform Web SDK는 Target at.js 라이브러리의 진화가 아닙니다. 웹 채널용 모든 Adobe 애플리케이션을 구현하는 새롭고 통합된 방법입니다. 알아야 할 기술적 차이점이 몇 가지 있습니다.

|  | at.js 2.x Target | Platform 웹 SDK |
|---|---|---|
| 라이브러리 기능 | at.js에서 제공하는 Target 기능입니다. Visitor.js 및 AppMeasurement.js에서 제공하는 다른 애플리케이션과의 통합 | 단일 Platform Web SDK 라이브러리에서 제공하는 모든 Adobe 애플리케이션에 대한 기능입니다. alloy.js |
| 공연 | at.js는 애플리케이션 간의 적절한 통합을 위해 로드되어야 하는 여러 라이브러리 중 하나입니다. 이로 인해 최적의 로드 시간이 줄어듭니다. | Platform Web SDK는 여러 애플리케이션별 라이브러리가 필요하지 않으므로 페이지 로드 성능이 향상됩니다. |
| 요청 | 각 Adobe 애플리케이션에 대해 별도의 호출을 생성합니다. Target 호출은 주로 다른 네트워크 호출과 독립적입니다. | 모든 Adobe 애플리케이션에 대한 단일 호출. 이러한 호출에서 전달된 데이터에 대한 변경 사항은 여러 다운스트림 애플리케이션에 영향을 줄 수 있습니다. |
| 로드 순서 | 다른 Adobe 애플리케이션과의 적절한 통합을 위해서는 라이브러리 및 네트워크 호출의 특정 로드 순서가 필요합니다. | 적절한 통합은 서로 다른 애플리케이션별 네트워크 호출의 데이터 결합에 의존하지 않으므로 로드 순서는 중요하지 않습니다. |
| 에지 네트워크 | 선택적으로 Target에 관련된 CNAME과 함께 Adobe Experience Cloud Edge Network(tt.omtrdc.net)를 사용합니다. | Adobe Experience Platform Edge Network(edge.adobedc.net)를 선택적으로 단일 CNAME과 함께 사용합니다. |
| 기본 용어 | at.js 이름 지정: <br> - `mbox` <br> - `pageLoad` 이벤트(글로벌 mbox) <br> - `offer` | Platform Web SDK에 해당 항목: <br> - `decisionScope` <br> - `__view__` decisionScope <br> - `proposition` |

### 비디오 개요

다음 비디오에서는 Adobe Experience Platform Web SDK 및 Adobe Experience Platform Edge 네트워크에 대한 개요를 제공합니다.

>[!VIDEO](https://video.tv.adobe.com/v/34141/?quality=12&learn=on)

이제 at.js와 Platform Web SDK의 높은 수준의 차이점을 파악했으므로 다음을 수행할 수 있습니다 [마이그레이션 계획](plan-migration.md).

>[!NOTE]
>
>Adobe는 at.js에서 웹 SDK로 Target 마이그레이션을 성공적으로 수행할 수 있도록 최선을 다하고 있습니다. 마이그레이션에 문제가 발생했거나 이 안내서에 중요한 정보가 누락된 것 같은 경우에는 로그인한 후 알려 주십시오 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).