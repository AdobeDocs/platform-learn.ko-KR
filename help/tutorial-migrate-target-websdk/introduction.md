---
title: 소개 | Target을 at.js 2.x에서 Web SDK로 마이그레이션
description: Adobe Target 구현을 at.js 2.x에서 Adobe Experience Platform Web SDK로 마이그레이션하는 방법에 대해 알아봅니다. 주제에는 JavaScript 라이브러리 로드, 매개 변수 전송, 렌더링 활동 및 기타 주목할 만한 콜아웃이 포함됩니다.
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: c8920fde-ad6b-4f2d-a35f-ce865b35bba0
source-git-commit: 4690d41f92c83fe17eda588538d397ae1fa28af0
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 4%

---

# Target을 at.js 2.x에서 Platform Web SDK로 마이그레이션

이 안내서는 숙련된 Adobe Target 구현자가 at.js 구현을 Adobe Experience Platform Web SDK로 마이그레이션하는 방법에 대해 학습하기 위한 것입니다.

Adobe Experience Platform Web SDK는 Adobe Experience Cloud 고객이 Adobe Experience Platform Edge Network을 통해 Experience Cloud 서비스와 상호 작용할 수 있도록 하는 클라이언트측 JavaScript 라이브러리입니다. 이 새 라이브러리는 별도의 Adobe 애플리케이션 라이브러리의 기능을 새로운 Adobe Experience Platform 기능을 최대한 활용할 수 있는 하나의 간단한 패키지에 결합합니다.

## 주요 이점

독립형 at.js 라이브러리와 비교한 Platform Web SDK의 이점 중 일부는 다음과 같습니다.

* [Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=ko-KR)에서 더 빠른 대상자 공유
* [Offer decisioning 배달](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)을(를) 지원하기 위해 Target과 Journey Optimizer 통합
* [자사 ID](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/generate-first-party-device-ids.html?lang=ko)를 사용하여 더 긴 기간 방문자 식별을 위해 ECID를 생성하는 기능
* Adobe 애플리케이션 간 네트워크 호출 통합
* 적은 설치 공간으로 페이지 속도 지표 개선
* 별도의 네트워크 호출의 정보 결합에 의존하지 않는 Adobe Analytics과의 긴밀한 통합
* 개발자를 위한 추가적인 구현 유연성

마이그레이션 시 Target 고객에게 가장 큰 이점은 Real-time Customer Data Platform과의 통합입니다. Real-Time CDP은 Experience Platform에 수집된 전체 데이터 범위와 실시간 고객 프로필 기능을 기반으로 엄청난 대상 구축 기능을 제공합니다. 내장된 데이터 거버넌스 프레임워크는 해당 데이터의 책임 있는 사용을 자동화합니다. 고객 AI를 사용하면 머신 러닝 모델을 쉽게 사용하여 결과를 Adobe Target에 다시 공유할 수 있는 성향 및 이탈 모델을 구성할 수 있습니다. 또한 선택적 의료 및 Privacy &amp; Security Shield 추가 기능의 고객은 동의 적용 기능을 사용하여 개별 고객의 동의 환경 설정을 쉽게 적용할 수 있습니다. Platform Web SDK는 웹 채널에서 이러한 RTCDP 기능을 사용하기 위한 요구 사항입니다.

## 학습 목표

이 자습서를 마치면 다음을 수행할 수 있습니다.

* at.js와 Platform Web SDK의 Target 구현 차이점 이해
* Target 기능에 대한 초기 구성 설정
* at.js 라이브러리를 Platform Web SDK로 업그레이드
* 양식 기반 및 시각적 경험 작성기 활동 렌더링
* Target에 매개 변수 전달
* 전환 이벤트 추적
* 도메인 간 지원 활성화
* 대상자 및 프로필 스크립트 업데이트
* 구현의 유효성 검사
* Target 경험 전달 디버그


## 전제 조건

이 자습서를 완료하려면 먼저 다음 작업을 수행해야 합니다.

* 현재 Target at.js 구현에 대한 기술적인 이해를 구하십시오
* 스스로 예제를 시도할 수 있도록 Target 인스턴스에 대해 [편집기 또는 게시자 역할](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80)이 있는지 확인하십시오
* Adobe Target에서 활동을 설정하는 방법을 이해할 수 있습니다. 새로 고침이 필요한 경우 다음 튜토리얼 및 안내서가 이 단원에 유용합니다.
   * [Visual Experience Composer 사용](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer.html)
   * [양식 기반 경험 작성기 사용](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer.html)
   * [경험 타깃팅 활동 만들기](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html)

준비가 되면 성공적으로 마이그레이션하기 위한 첫 번째 단계는 [마이그레이션 프로세스와 at.js 및 Platform Web SDK의 차이점에 대해 알아보는 것입니다](migration-overview.md).

>[!NOTE]
>
>at.js에서 Web SDK로 Target을 성공적으로 마이그레이션할 수 있도록 지원하기 위해 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)에 게시하여 알려 주십시오.
