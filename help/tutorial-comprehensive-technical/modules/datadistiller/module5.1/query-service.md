---
title: 쿼리 서비스
description: 쿼리 서비스
kt: 5342
doc-type: tutorial
source-git-commit: 7d2f5f842559b2d6d9f115f3993268a4b36a0fe0
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 1%

---

# 5.1 쿼리 서비스

**작성자: [Marc Meewis](https://www.linkedin.com/in/marcmeewis/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

이 모듈에서는 Adobe Experience Platform 쿼리 서비스의 실습형 미리 보기를 제공합니다. 쿼리 서비스를 사용하면 모든 Adobe Experience Cloud 애플리케이션 데이터에 대해 옴니채널 쿼리를 수행하여 Adobe Campaign, Analytics, Audience Manager, Target 및 Advertising Cloud의 데이터와 Adobe Experience Platform에 로드/삽입된 기타 고객 데이터를 연결 및 분석할 수 있습니다.

쿼리 서비스는 서버를 사용하지 않는 도구입니다. PostgreSQL 호환성을 통해 여러 클라이언트 애플리케이션에서 SQL 쿼리 및 연결을 지원합니다.
웹 인터랙션 데이터, 콜 센터 인터랙션 및 플랫폼에 업로드된 고객 충성도 데이터와 결합하여 플랫폼에 삽입된 데이터를 사용합니다.

## 학습 목표

- Adobe Experience Platform UI 이해하기
- 쿼리 서비스에 연결하고 SQL 쿼리 실행
- Adobe Experience Platform에서 데이터 세트 탐색
- 타블로 또는 Power BI을 Adobe Experience Platform 쿼리 서비스에 연결하여 시각화 및 보고서 만들기

## 전제 조건

- SQL에 대한 일부 친숙성이 선호되지만 필수는 아닙니다.
- Adobe Experience Platform 액세스: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 데이터 세트 (실습 중에 사용된 데이터 세트, 사전 로드됨)
- PostgreSQL
- Tableau 또는 Microsoft Power BI 데스크탑
- **이 에셋 다운로드**:
   - [JSON - 샘플 데이터: 웹 사이트 상호 작용](./../../../assets/json/ee.json)
   - [JSON - 샘플 데이터: 콜 센터 상호 작용](./../../../assets/json/callcenter.json)
   - [JSON - 샘플 데이터: 충성도](./../../../assets/json/loyalty.json)

>[!NOTE]
>
>[0.1 - Experience League 설명서용 Chrome 확장 설치](../../gettingstarted/gettingstarted/ex1.md)에서 참조한 대로 Chrome 확장 기능을 설치, 구성 및 사용하는 것을 잊지 마십시오.

## 연습

[5.1.0 사전 요구 사항](./ex0.md)

이 지원 연습에서 쿼리를 실행하려면 PSQL을 설치해야 합니다. 운영 체제에 따라 Microsoft Power BI 또는 Tableau를 설치해야 합니다. Windows 사용자는 Power BI 또는 타블로 중에서 선택할 수 있습니다. Mac 사용자는 Tableau를 설치해야 합니다.

[5.1.1 시작](./ex1.md)

이 연습에서는 Adobe Experience Platform 쿼리 서비스 사용자 인터페이스를 살펴보고 데이터 세트에 대해 알아보고 쿼리를 찾은 다음 마지막으로 PSQL에서 연결을 설정합니다.

[5.1.2 쿼리 서비스 사용](./ex2.md)

이 연습에서는 기본 쿼리 서비스 구문에 대해 알아보고 쿼리에서 XDM 스키마의 속성을 식별할 수 있습니다.

[5.1.3 쿼리, 쿼리, 쿼리... 및 이탈 분석](./ex3.md)

이 연습에서는 쿼리를 수행하게 되며 일부 이탈 분석을 수행하는 동안 Adobe 정의 함수에 대해 알아봅니다. 이 과정이 끝나면 Microsoft Power BI에서 사용할 데이터 세트를 준비하는 쿼리를 작성합니다.

[5.1.4 쿼리에서 데이터 세트 생성](./ex4.md)

이 연습에서는 이전에 실행한 쿼리에서 데이터 세트를 생성하고 다음 연습에서 이 데이터 세트를 사용합니다.

[5.1.5 쿼리 서비스 및 Power BI](./ex5.md)

이 연습에서는 Power BI을 Adobe Experience Platform 및 쿼리 서비스에 연결하여 콜센터 상호 작용 분석을 수행합니다.

[5.1.6 쿼리 서비스 및 타블로](./ex6.md)

이 연습에서는 Tableau를 Adobe Experience Platform 및 쿼리 서비스에 연결하여 콜센터 상호 작용 분석을 수행합니다.

[5.1.7 쿼리 서비스 API](./ex7.md)

이 연습에서는 쿼리 템플릿 및 쿼리 일정을 관리하기 위해 쿼리 서비스 API를 사용합니다.

[요약 및 이점](./summary.md)

이 단원의 요약 및 이점 개요

>[!NOTE]
>
>Adobe Experience Platform과 애플리케이션에 대해 알아야 할 모든 것을 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있는 경우 향후 콘텐츠에 대한 제안 사항에 대한 일반적인 피드백을 공유하려면 기술 인사이더에게 **techinsiders@adobe.com**&#x200B;로 전자 메일을 보내 직접 문의하십시오.

[모든 모듈로 돌아가기](../../../overview.md)
