---
title: 데이터 설계자 및 데이터 엔지니어를 위한 Adobe Experience Platform 시작하기
description: 데이터 설계자 및 데이터 엔지니어를 위한 Adobe Experience Platform을 시작합니다.
breadcrumb-title: 개요
role: Data Architect, Data Engineer
kt: 4348
thumbnail: 4348-overview.jpg
recommendations: catalog, noDisplay
exl-id: fabbc591-840b-40dc-89af-305626a16338
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 1%

---

# 데이터 설계자 및 데이터 엔지니어를 위한 Adobe Experience Platform 시작하기

<!--5min-->

_데이터 설계자 및 데이터 엔지니어를 위한 Adobe Experience Platform 시작하기_ Experience Platform을 직접 살펴보기 위한 완벽한 시작점입니다.


<!--How do we address ETL-->

## 학습 목표

데이터 설계자와 데이터 엔지니어는 성공적인 Experience Platform 배포를 위해 긴밀히 협력해야 합니다. 이 실습 자습서에서는 _두 역할_ 따라서 고유한 비즈니스를 위해 Platform 구현을 시작하는 방법을 알고 있습니다. Experience Platform의 주요 용어, 기능, 인터페이스 및 API를 소개합니다. Real-time Customer Data Platform, Customer Journey Analytics 및 Journey Optimizer과 같은 Adobe Experience Cloud 애플리케이션의 고객은 Platform 서비스가 이러한 애플리케이션의 중요한 기반이므로 이 컨텐츠를 유용하게 사용할 수 있습니다.

![Adobe Experience Cloud 마케팅 - ID, 프로필, 세그멘테이션, 수집, 쿼리 및 거버넌스 자습서에서 다루는 플랫폼 서비스를 강조 표시하는 마케팅](assets/marketecture.png)

항목은 다음과 같습니다.

* 사용자 권한 구성
* 샌드박스 만들기
* 개발자 콘솔 프로젝트 설정 및 플랫폼 API 사용
* 스키마, 데이터 세트, ID, 병합 정책 및 데이터 거버넌스 생성을 비롯한 데이터 관리
* 일괄 처리 및 스트리밍 모드를 사용한 데이터 수집
* Adobe Experience Platform Web SDK를 사용하여 웹 데이터 캡처
* 실시간 고객 프로필 작성
* 쿼리 서비스를 사용하여 데이터 유효성 검사 및 데이터 추출
* 세그먼트 작성

## 비즈니스 시나리오

Adobe Experience Platform은 마케팅 목표를 달성하는 데 도움이 되도록 설계된 기술 플랫폼입니다. 비즈니스 사용 사례는 기술을 디자인하고 구현하는 방법을 주도해야 합니다. 이 자습서에서는 Luma라는 가상의 소매 브랜드에 중점을 둡니다. Luma는 여러 국가에서 브릭 및 몰탈 스토어를 운영하고 있으며 웹 사이트 및 모바일 앱과 함께 온라인 사이트를 운영하고 있습니다. 이들은 충성도, CRM, 웹 및 오프라인 구매 데이터를 실시간 고객 프로필에 결합하고 이러한 프로필을 활성화하여 마케팅을 한 차원 끌어올리기 위해 Adobe Experience Platform에 투자하고 있습니다. Luma의 비즈니스 목표는 회사의 목표에 부합하거나 그렇지 않을 수 있지만, 이 자습서의 실무 단계를 자신의 비즈니스 목표에 연결할 수 있어야 합니다.

## 사전 요구 사항

* 을(를) 완료했습니다 [Adobe Experience Platform 교육 과정 소개](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2020.1) Experience League 및 플랫폼 기능에 익숙함
* Adobe Experience Platform(또는 실시간 CDP 또는 Journey Optimizer과 같은 플랫폼 기반 애플리케이션)과 데이터 수집(이전 Launch)으로 제공된 계정에 액세스할 수 있습니다.
* 해당 계정의 시스템 관리자이거나 계정을 가질 수 있습니다 [사용자 권한 구성](configure-permissions.md) 활성화해줄 수 있습니다.

## 이 자습서 사용

이 자습서에서는 데이터 엔지니어 및 데이터 설계자를 위한 작업을 결합합니다. 소개 수준 자습서이므로 두 역할에 대해 작업을 완료할 수 있습니다. 이전 단원에서 구현된 내용을 바탕으로 학습되는 많은 단원들 때문에, 여러분은 그 단원을 순서대로 진행해야 합니다. 어느 과목을 빼먹어야 하는지 알려드리겠습니다.

이 자습서 중에 다양한 Platform 요소를 만들 때 가능한 한 권장되는 이름을 사용하십시오. 그러나 조직의 여러 사용자가 이 자습서를 동시에 진행하고 있는 경우 사용자 지정할 수 있는 몇 가지 상위 수준 요소 이름이 있습니다. 예를 들어, Platform 샌드박스의 이름을 &quot;Luma 자습서 플랫폼&quot; 대신 &quot;Luma 자습서 플랫폼 - Ignatus J Reilly&quot;로 지정할 수 있습니다.

문제가 발생하면 먼저 지침을 다시 읽은 다음 ![문제 기록](https://experienceleague.adobe.com/assets/img/feedback.svg) 링크를 클릭하면 각 페이지의 사이드바에 연결하여 나에게 문의하십시오.

## 기술 정보

### 샌드박스 환경

자습서에서는 샌드박스 환경을 만들고 이 환경을 사용하여 연습을 완료합니다. 샌드박스 환경을 사용하면 프로덕션 데이터를 손상시키지 않고 연습과 실험을 안전하게 완료할 수 있습니다.

### API

플랫폼이 API부터 빌드됩니다. 모든 주요 플랫폼 워크플로우에 대해 인터페이스 워크플로우가 존재하며 주로 사용되지만 자습서에는 일부 API 기반 연습이 포함되어 있습니다. Adobe Developer 콘솔의 기본 프로젝트 설정을 안내하고 다음을 제공합니다. [!DNL Postman] 플랫폼 API를 시작할 환경 및 컬렉션. 자습서를 완료한 후에는 플랫폼 API에 익숙하고 자체 배포에서 사용하는 것이 유용할 수 있습니다.

### 타사 기술

이 자습서에서는 여러 기술을 사용할 수 있지만 거의 완전히 Adobe 에코시스템 내에 남아 있습니다. 자체 플랫폼 구현에서는 특정 타사 기술과 플랫폼을 통합할 수 있습니다. 모든 고객을 위해 이 자습서를 유지하기 위해 일반적인 구현을 사용할 것입니다.

이제 첫 번째 단원에서 시작하겠습니다[권한 구성](configure-permissions.md).
