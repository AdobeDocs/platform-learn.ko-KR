---
title: 모바일 앱을 Adobe Target에서 Offer Decisioning 및 Target 확장 기능으로 마이그레이션
description: 모바일 앱 구현을 Adobe Target에서 Offer Decisioning 및 Target 확장으로 마이그레이션하는 방법에 대해 알아봅니다
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: 32363b95-b6ad-44af-a3b0-e1fbbbf5a8f1
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 1%

---

# 모바일 앱을 Adobe Target에서 Offer Decisioning 및 Target 확장 기능으로 마이그레이션

이 안내서는 숙련된 Adobe Target 구현자가 기존 Adobe SDK Experience Platform을 Adobe Target 확장에서 Offer Decisioning 및 Target 확장으로 마이그레이션하는 방법을 학습하기 위한 것입니다.

Adobe Experience Platform Mobile SDK은 모바일 애플리케이션에서 전체적인 구현을 지원합니다. Target 확장은 모바일 SDK을 기반으로 구축되어 Adobe Target을 통해 앱 경험을 개인화할 수 있습니다. Offer Decisioning 및 Target 확장은 Target을 Real-Time CDP 및 Journey Optimizer과 같은 플랫폼 기반 앱과 통합하는 데 도움이 되는 Adobe Experience Platform Edge Network 기능을 사용하는 모바일 앱에서 Adobe Target을 구현하는 새로운 방법입니다.

![Offer Decisioning 및 Target 확장을 사용하여 Edge Network을 통해 Target에 연결하는 Mobile SDK을 보여 주는 다이어그램](assets/datacollection.png)

## 주요 이점

Target 확장과 비교하여 Adobe Journey Optimizer Offer Decisioning 및 Target 확장의 이점 중 일부는 다음과 같습니다.

* [Real-Time Customer Data Platform](https://experienceleague.adobe.com/ko/docs/platform-learn/tutorials/destinations/target/next-hit-personalization)에서 더 빠른 대상자 공유
* Target과 Journey Optimizer을 통합하여 [Offer Decisioning 게재](https://experienceleague.adobe.com/ko/docs/target/using/integrate/ajo/offer-decision) 지원
* 별도의 네트워크 호출의 정보 결합에 의존하지 않는 Adobe Analytics과의 긴밀한 통합
* 개발자를 위한 추가적인 구현 유연성

마이그레이션 시 Target 고객에게 가장 큰 이점은 Real-Time Customer Data Platform과의 통합입니다. Real-Time CDP은 Experience Platform에 수집된 전체 데이터 범위와 실시간 고객 프로필 기능을 기반으로 엄청난 대상 구축 기능을 제공합니다. 내장된 데이터 거버넌스 프레임워크는 해당 데이터의 책임 있는 사용을 자동화합니다. 고객 AI를 사용하면 머신 러닝 모델을 쉽게 사용하여 결과를 Adobe Target에 다시 공유할 수 있는 성향 및 이탈 모델을 구성할 수 있습니다. 또한 선택적 의료 및 Privacy &amp; Security Shield 추가 기능의 고객은 동의 적용 기능을 사용하여 개별 고객의 동의 환경 설정을 적용할 수 있습니다. Platform Mobile SDK과 Offer Decisioning 및 Target 확장은 모바일 채널에서 이러한 Real-Time CDP 기능을 사용하기 위한 요구 사항입니다.

## 마이그레이션 단계

Target 확장에서 Offer Decisioning 및 Target 확장으로 마이그레이션하는 작업의 수준은 현재 구현과 사용된 Target 기능의 복잡성에 따라 다릅니다.

구현이 아무리 간단하거나 복잡하더라도 마이그레이션 전에 현재 상태를 완전히 이해하는 것이 중요합니다. 이 안내서는 현재 구현의 구성 요소를 분류하고 각 요소를 마이그레이션하는 관리 가능한 계획을 개발하는 데 도움이 됩니다.

마이그레이션 프로세스에는 다음과 같은 주요 단계가 포함됩니다.

1. 다음을 포함하여 현재 구현 평가:
   1. 사용된 모든 Target SDK API
   1. Target의 전역 설정에 대한 수정 사항
   1. Adobe Analytics와의 통합
   1. mbox, 프로필 및 엔티티 매개 변수 사용
   1. 프로필 스크립트 및 대상자 사용
   1. 구현에 고유한 사용자 지정 코드
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

그런 다음 Target 확장과 Offer Decisioning 및 Target 확장의 자세한 [비교](comparison.md)를 검토하여 기술적인 차이점을 더 잘 이해하고 추가 포커스가 필요한 영역을 식별하십시오.

>[!NOTE]
>
>Target 확장에서 Offer Decisioning 및 Target 확장으로 모바일 Target 마이그레이션을 성공적으로 수행할 수 있도록 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484?profile.language=ko#M625)에 게시하여 알려 주십시오.
