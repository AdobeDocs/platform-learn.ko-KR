---
title: 데이터 수집 - 페더레이션 대상 구성
description: 데이터 수집 - 페더레이션 대상 구성
kt: 5342
doc-type: tutorial
exl-id: 44660f3e-0594-4578-9531-1c918992aa9d
source-git-commit: bd46be455f88007174f7e6be9a1ce5f508edc09b
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# 1.3 페더레이션 대상 구성

이 모듈의 목표는 Federated Audience Composition을 사용하여 대상자를 만드는 방법에 대해 모두 학습하는 것입니다.

Experience Platform의 FAC(Federated Audience Composition)를 사용하면 엔터프라이즈 데이터 웨어하우스의 해당 고가치 속성으로 대상에 액세스하고 대상을 만들 수 있습니다. 이 기능은 세분화, 타기팅, 활성화 및 효과적인 고객 경험의 전달을 개선하기 위해 Experience Platform의 실시간 고객 프로필과 대상을 보강하고 보완합니다. Federated Audience Composition을 사용하여 메타데이터를 통해 원격 데이터베이스를 연결하여 가상 데이터베이스를 만듭니다. 이 접근 방식은 액세스를 단순화하고, 중복을 줄이고, 최종 사용자 경험을 향상시킵니다. 팀에게는 참여 워크플로우에 대한 대상을 구성할 때 데이터 세트를 Experience Platform에 직접 수집하거나 데이터 웨어하우스에 있는 데이터 세트에 액세스할 수 있는 유연성이 부여됩니다. 이 접근 방식은 데이터 웨어하우스 투자 및 자산을 활용하여 Real-Time CDP 및 Journey Optimizer을 보완합니다. Federated Audience Composition을 통해 고객은 중요한 새로운 사용 사례 패턴 전반에서 배치 및 실시간 기능을 활용하고 결합할 수 있습니다.

- 연합 대상 세그멘테이션: 팀은 Real-Time CDP 및 Journey Optimizer에서 마케터에게 친숙한 드래그 앤 드롭 대상 구성 UI를 사용하여 대상을 작성할 수 있지만, 쿼리가 데이터 웨어하우스에 푸시되어 중요한 기본 데이터를 중복 없이 웨어하우스에 남기고 필수 데이터 세트에 대한 유연한 액세스를 제공합니다.
- 대상 강화: Real-Time CDP 및 Journey Optimizer에 구축된 대상은 Adobe Experience Platform에서 지속되지 않는 추가 프로필 기반 및 비프로필 기반 데이터 세트를 사용하여 타깃팅 및 개인화를 개선하기 위해 추가 엔터프라이즈 데이터로 보강할 수 있습니다. 예를 들어 소매 브랜드는 최근 온라인 구매자의 고객을 맨 위의 오프라인 위치 목록으로 보완하여 크로스 채널 온라인 및 매장 내 프로모션을 위한 대상을 구축할 수 있습니다.
- 프로필 강화: 팀은 데이터 웨어하우스에서 Real-Time CDP에 상주하고 Journey Optimizer을 통해 액세스하는 실행 가능한 고객 프로필 내에 현재 경험을 유지하는 데 중요한 프로필 속성을 선택할 수 있습니다. 그런 다음 이러한 추가 데이터 포인트를 사용자 작업 및 고객 사용 사례에 따라 이벤트 동작에 의해 트리거되는 다운스트림 세그먼테이션 및 개인화에 사용할 수 있습니다. 이렇게 하면 고객 프로필에 보존된 다른 속성 및 동작 신호와 함께 페더레이션 대상과 함께 가져온 속성을 즉시 세분화 및 개인화에 사용할 수 있습니다.

Federated Audience Composition은 Real-Time CDP 및 Journey Optimizer 고객에게 언제 어떤 데이터를 사용할지 결정할 수 있는 유연성을 제공하며, 불필요하게 중복되는 데이터 세트나 통합 패턴을 방지하는 데 도움이 됩니다. 이는 엔터프라이즈 데이터를 사용하여 대상자를 선별하고 가치가 높은 속성을 조정하는 통합 접근 방식과 즉각적인 크로스 채널 참여에 최적화된 시스템이 결합된 고유한 방식을 나타냅니다. 따라서 데이터 이동이 줄어들지만, 채널 전반에서 지연 시간이 짧은 일관된 활성화를 위해 가치가 높은 대상과 속성을 활용할 수 있는 새로운 기회가 생깁니다.

## 학습 목표

- Adobe Experience Platform과 Snowflake을 연결하는 방법 알아보기
- Adobe Experience Platform에서 페더레이션 데이터에 대한 데이터 모델을 만드는 방법을 알아봅니다
- Adobe Experience Platform에서 연합 대상 구성을 만드는 방법을 알아봅니다

## 전제 조건

- Adobe Experience Platform 액세스: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Snowflake 데이터 웨어하우스 액세스

## 연습

[1.3.1 Snowflake 환경 설정](./ex1.md)

이 연습에서는 Snowflake 체험판 계정을 설정하고 Adobe Experience Platform에 연결합니다

[1.3.2 스키마, 데이터 모델 및 링크 만들기](./ex2.md)

이 연습에서는 페더레이션 데이터에 대해 AEP에서 데이터 모델을 구성합니다.

[1.3.3 통합 컴포지션 만들기](./ex3.md)

이 연습에서는 페더레이션 데이터에 대해 AEP에서 데이터 모델을 구성합니다.

[요약 및 이점](./summary.md)

이 단원의 요약 및 이점 개요

![기술 내부자](./../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Adobe Experience Platform과 애플리케이션에 대해 알아야 할 모든 것을 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있는 경우 향후 콘텐츠에 대한 제안 사항에 대한 일반적인 피드백을 공유하려면 기술 인사이더에게 **techinsiders@adobe.com**&#x200B;로 전자 메일을 보내 직접 문의하십시오.

[모든 모듈로 돌아가기](../../../overview.md)
