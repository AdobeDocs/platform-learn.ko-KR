---
title: 마이그레이션 계획 - Adobe Target에서 Adobe Journey Optimizer으로 마이그레이션 - Decisioning Mobile 확장
description: at.js와 Platform Web SDK 간의 주요 차이점과 마이그레이션 노력을 계획하는 방법에 대해 알아봅니다.
exl-id: 86849319-d2ad-4338-aa1a-d307d8807d4a
source-git-commit: f3fd5f45412900dcb871bc0b346ce89108fa8913
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---

# 마이그레이션 계획

Target 확장에서 Decisioning 확장으로 마이그레이션하는 작업의 수준은 현재 구현의 복잡성과 사용되는 제품 기능에 따라 다릅니다.

구현이 아무리 간단하거나 복잡하더라도 마이그레이션 전에 현재 상태를 완전히 이해하는 것이 중요합니다. 이 안내서는 현재 구현의 구성 요소를 분류하고 각 요소를 마이그레이션하는 관리 가능한 계획을 개발하는 데 도움이 됩니다.

마이그레이션 프로세스에는 다음과 같은 주요 단계가 포함됩니다.

1. 현재 구현 평가 및 마이그레이션 접근 방식 결정
1. Adobe Experience Platform Edge Network에 연결하도록 초기 구성 요소 설정
1. 기본 구현을 업데이트하여 Target 확장 및 Decisioning 확장 대체
1. 특정 사용 사례에 맞게 SDK 최적화 구현을 개선합니다. 여기에는 추가 매개 변수 전달, 응답 토큰 사용 등이 포함될 수 있습니다.
1. 프로필 스크립트, 활동 및 대상 정의와 같은 Target 인터페이스의 객체 업데이트
1. 프로덕션 환경에서 전환하기 전에 최종 구현의 유효성을 확인합니다.

## Target 확장과 Decisioning 확장 간의 주요 차이점

마이그레이션 프로세스를 시작하기 전에 Target 확장과 Decisioning 확장 간의 차이점을 이해하는 것이 중요합니다.

### 운영상의 차이점

| | Target at.js 2.x | Platform Web SDK |
|---|---|---|
| 프로세스 | Target 구현을 변경하면 Analytics와 같은 다른 애플리케이션과 비교하여 케이던스 또는 QA 요구 사항이 다른 프로세스를 따를 수 있습니다. | Decisioning 확장 구현을 변경하면 모든 다운스트림 애플리케이션을 고려해야 하며 QA 및 게시 프로세스를 적절하게 조정해야 합니다. |
| 공동 작업 | Target에 대한 데이터는 Target 호출에서 직접 전달할 수 있습니다. Target 보고 소스가 Adobe Analytics인 경우, Target 확장의 적절한 추적 방법이 Target 컨텐츠 표시 및 상호 작용을 위해 호출될 때 Target에 관련된 데이터를 Adobe Analytics에도 전달할 수 있습니다. | Target 보고 소스가 Adobe Analytics이고, Adobe Analytics이 데이터 스트림에서 활성화되어 있으며, Target 콘텐츠가 표시되고 상호 작용할 때 Decisioning 확장의 적절한 추적 메서드가 호출되는 경우 Decisioning 확장 호출에서 전달된 데이터를 Target과 Analytics 모두에 전달할 수 있습니다. |

### 기술적 차이점

| | Target 확장 | Decisioning 확장 |
|---|---|---|
| 종속성 | Mobile Core SDK에만 종속 | Mobile Core 및 Edge Network SDK에 따라 다름 |
| 라이브러리 기능 | Adobe Target에서만 콘텐츠 가져오기 지원 | Adobe Target 및 Offer decisioning에서 컨텐츠 가져오기 지원 |
| 요청 | 대상 호출은 대개 다른 네트워크 호출과 독립적입니다 | 대상 네트워크 호출은 Edge SDK의 메시징 과 같은 다른 Edge 기반 솔루션에 대한 네트워크 호출과 함께 큐에 올라가 순차적으로 실행됩니다. |
| Edge Network | 데이터 수집 UI의 [Target 구성](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui)에 지정된 클라이언트 코드(clientcode.tt.omtrdc.net)와 함께 Target 서버 값 또는 Adobe Experience Cloud Edge Network을 사용합니다. | 데이터 수집 UI의 Adobe Experience Platform [Edge Network 구성](https://developer.adobe.com/client-sdks/edge/edge-network/#configure-the-edge-network-extension-in-data-collection-ui)에 지정된 Edge 네트워크 도메인을 사용합니다. |
| 기본 용어 | mbox, 타겟 매개 변수 | DecisionScope, Map (Android)/dictionary (iOS) for target parameters |
| 기본 콘텐츠 | 네트워크 호출에 실패하거나 오류가 발생하는 경우 반환되는 TargetRequest에 클라이언트측 기본 콘텐츠를 전달할 수 있습니다. | 클라이언트측 기본 컨텐츠 전달을 허용하지 않습니다. 네트워크 호출에 실패하거나 오류가 발생하는 경우 콘텐츠를 반환하지 않습니다. |
| Target 매개 변수 | 요청당 글로벌 TargetParameters 및 mbox당 다른 TargetParameters를 전달할 수 있습니다. | 요청당 글로벌 TargetParameters 전달만 허용 |

그런 다음 Target 확장과 Decisioning 확장의 자세한 [비교](detailed-comparison.md)를 검토하여 기술적 차이점을 더 잘 이해하고 추가 포커스가 필요한 영역을 식별합니다.

>[!NOTE]
>
>Target 확장에서 Decisioning 확장으로 모바일 Target을 성공적으로 마이그레이션할 수 있도록 지원하기 위해 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)에 게시하여 알려 주십시오.
