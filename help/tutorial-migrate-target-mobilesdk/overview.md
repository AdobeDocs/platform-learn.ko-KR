---
title: Adobe Target에서 Adobe Journey Optimizer - Decisioning Mobile Extension으로 마이그레이션
description: 모바일 앱 구현을 Adobe Target에서 Adobe Journey Optimizer - Decisioning 확장으로 마이그레이션하는 방법을 알아봅니다
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: 32363b95-b6ad-44af-a3b0-e1fbbbf5a8f1
source-git-commit: 6e442413c178e76183f88454d97d3896f8efa8bc
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 3%

---

# Adobe Target에서 Adobe Journey Optimizer - Decisioning Mobile Extension으로 마이그레이션

이 안내서는 숙련된 Adobe Target 구현자가 기존 Adobe Experience Platform을 Mobile SDK 구현에서 Adobe Target 확장에서 Adobe Journey Optimizer - Decisioning 확장으로 마이그레이션하는 방법을 배울 수 있는 것입니다.

Adobe Experience Platform Mobile SDK은 모바일 애플리케이션에서 전체적인 구현을 지원합니다. Target 확장은 모바일 SDK을 기반으로 구축되어 Adobe Target을 통해 앱 경험을 개인화할 수 있습니다. Decisioning 확장은 Target을 Real-Time CDP 및 Journey Optimizer과 같은 플랫폼 기반 앱과 통합하는 데 도움이 되는 Adobe Experience Platform Edge Network 기능을 사용하는 모바일 앱에서 Adobe Target을 구현하는 새로운 접근 방식입니다.

## 주요 이점

Decisioning 확장의 이점 중 일부는 다음과 같습니다.

* [Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=ko-KR)에서 더 빠른 대상자 공유
* [Offer decisioning 배달](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)을(를) 지원하기 위해 Target과 Journey Optimizer 통합
* 별도의 네트워크 호출의 정보 결합에 의존하지 않는 Adobe Analytics과의 긴밀한 통합
* 개발자를 위한 추가적인 구현 유연성

마이그레이션 시 Target 고객에게 가장 큰 이점은 Real-time Customer Data Platform과의 통합입니다. Real-Time CDP은 Experience Platform에 수집된 전체 데이터 범위와 실시간 고객 프로필 기능을 기반으로 엄청난 대상 구축 기능을 제공합니다. 내장된 데이터 거버넌스 프레임워크는 해당 데이터의 책임 있는 사용을 자동화합니다. 고객 AI를 사용하면 머신 러닝 모델을 쉽게 사용하여 결과를 Adobe Target에 다시 공유할 수 있는 성향 및 이탈 모델을 구성할 수 있습니다. 또한 선택적 의료 및 Privacy &amp; Security Shield 추가 기능의 고객은 동의 적용 기능을 사용하여 개별 고객의 동의 환경 설정을 쉽게 적용할 수 있습니다. Platform Mobile SDK 및 Decisioning 확장은 모바일 채널에서 이러한 Real-Time CDP 기능을 사용하기 위한 요구 사항입니다.

## 학습 목표

이 자습서를 마치면 다음을 수행할 수 있습니다.

* 글머리 기호
* 글머리 기호 2


## 전제 조건

이 자습서를 완료하려면 먼저 다음 작업을 수행해야 합니다.

* 글머리 기호
* 글머리 기호 2


>[!NOTE]
>
>Target 확장에서 Decisioning 확장으로 모바일 Target을 성공적으로 마이그레이션할 수 있도록 지원하기 위해 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)에 게시하여 알려 주십시오.
