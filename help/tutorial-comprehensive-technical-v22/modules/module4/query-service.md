---
title: 쿼리 서비스
description: 쿼리 서비스
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 74943e52-8a7e-4db7-9407-7deeab008fa7
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 1%

---

# 4. 쿼리 서비스

**작성자: [마크 메위스](https://www.linkedin.com/in/marcmeewis/), [우터 반 겔루위](https://www.linkedin.com/in/woutervangeluwe/)**

이 모듈에서는 Adobe Experience Platform Query Service의 실시간 미리 보기가 제공됩니다. Query Service를 사용하면 모든 Adobe Experience Cloud 애플리케이션 데이터에 대해 옴니채널 쿼리를 수행하고 Adobe Campaign, Analytics, Audience Manager, Target 및 Advertising Cloud과 Adobe Experience Platform에 로드되거나 삽입된 기타 고객 데이터에 데이터를 결합하고 분석할 수 있습니다.

쿼리 서비스는 서버를 사용하지 않는 도구입니다. PostgreSQL 호환성을 통해 여러 클라이언트 응용 프로그램에서 SQL 쿼리 및 연결을 지원합니다.
Adobe에서는 플랫폼에 업로드된 고객 충성도 데이터와 결합하여 웹 상호 작용 데이터, 콜 센터 상호 작용 중 하나를 사용하여 플랫폼에 삽입된 데이터를 사용합니다.

## 학습 목표

- Adobe Experience Platform UI에 익숙해지십시오
- 쿼리 서비스에 연결하고 SQL 쿼리를 실행합니다
- Adobe Experience Platform에서 데이터 세트 탐색
- 표 또는 Power BI을 Adobe Experience Platform 쿼리 서비스에 연결하여 시각화 및 보고서를 만듭니다

## 전제 조건

- SQL에 대해 잘 알고 있지만 필수는 아닙니다
- Adobe Experience Platform 액세스: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 데이터 세트(랩 중에 사용된 데이터 세트, 미리 로드됨)
- PostgreSQL
- 타블로 또는 Microsoft Power BI 데스크탑
- **다음 자산 다운로드**:
   - [JSON - 샘플 데이터: 웹 사이트 상호 작용](./../../assets/json/ee.json)
   - [JSON - 샘플 데이터: 콜 센터 상호 작용](./../../assets/json/callcenter.json)
   - [JSON - 샘플 데이터: 충성도](./../../assets/json/loyalty.json)

>[!IMPORTANT]
>
>이 자습서는 특정 워크숍 형식을 용이하게 하기 위해 만들어졌습니다. 액세스 권한이 없을 수 있는 특정 시스템 및 계정을 사용합니다. 액세스 권한이 없더라도 이 매우 자세한 내용을 통해 많은 것을 배울 수 있을 것입니다. 워크샵 중 하나에 참여하고 액세스 자격 증명이 필요한 경우 Adobe 담당자에게 연락하여 필요한 정보를 제공합니다.

## 아키텍처 개요

이 모듈에서 논의하고 사용할 구성 요소를 강조 표시하는 아래 아키텍처를 살펴보십시오.

![아키텍처 개요](../../assets/images/architecturem7.png)

## 사용할 샌드박스

이 모듈의 경우 다음 샌드박스를 사용하십시오. `--module7sandbox--`.

>[!NOTE]
>
>에서 참조한 대로 Chrome 확장 프로그램을 설치, 구성 및 사용하는 것을 잊지 마십시오 [0.1 - Experience League 설명서용 Chrome 확장 프로그램 설치](../module0/ex1.md)

## 연습

[4.0 사전 요구 사항](./ex0.md)

이 지원 연습에서 쿼리를 실행하려면 PSQL을 설치해야 합니다. 운영 체제에 따라 Microsoft Power BI 또는 타블로를 설치해야 합니다. Windows 사용자는 Power BI 또는 타블로 중에서 선택할 수 있습니다. Mac 사용자는 타블로를 설치해야 합니다.

[4.1 시작하기](./ex1.md)

이 연습에서는 Adobe Experience Platform Query Service 사용자 인터페이스를 살펴보고 데이터 세트에 대해 알아보고 쿼리를 찾은 다음 마지막으로 PSQL에서 연결을 설정합니다.

[4.2 쿼리 서비스 사용](./ex2.md)

이 연습에서는 기본 쿼리 서비스 구문에 대해 알아보고 쿼리에서 XDM 스키마의 속성을 식별할 수 있습니다.

[4.3 쿼리, 쿼리, 쿼리... 및 이탈 분석](./ex3.md)

이 연습에서는 쿼리를 수행하면서 몇 가지 이탈 분석을 수행하는 동안 Adobe 정의 함수에 대해 알아봅니다. 이 작업이 끝나면 Microsoft Power BI에서 사용할 데이터 세트를 준비하는 쿼리를 작성합니다.

[4.4 쿼리에서 데이터 세트 생성](./ex4.md)

이 연습에서는 이전 연습에서 실행된 쿼리에서 데이터 세트를 생성하고 다음 연습에서 이 데이터 세트를 사용합니다.

[4.5 쿼리 서비스 및 Power BI](./ex5.md)

이 연습에서는 Power BI을 Adobe Experience Platform 및 Query Service에 연결하여 Callcenter Interaction Analysis를 수행합니다.

[4.6 쿼리 서비스 및 타블로](./ex6.md)

이 연습에서는 타블로와 Adobe Experience Platform 및 쿼리 서비스를 연결하여 Callcenter 상호 작용 분석을 수행합니다.

[4.7 Query Service API](./ex7.md)

이 연습에서는 Query Service API를 사용하여 쿼리 템플릿 및 쿼리 일정을 관리합니다.

[요약 및 이점](./summary.md)

이 모듈의 요약 및 이점 개요

>[!NOTE]
>
>Adobe Experience Platform에 대해 알아야 할 모든 것을 배우는 데 시간을 투자해주셔서 감사합니다. 질문이 있는 경우 향후 컨텐츠에 대한 제안 사항이 있는 일반적인 피드백을 공유하려는 경우 Outlook Van Geluwe에게 이메일을 직접 보내주십시오 **vangeluw@adobe.com**.

[모든 모듈로 돌아가기](../../overview.md)
