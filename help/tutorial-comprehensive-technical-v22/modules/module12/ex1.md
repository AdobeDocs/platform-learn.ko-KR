---
title: BigQuery Source Connector를 사용하여 Adobe Experience Platform에서 Google Analytics 데이터를 수집 및 분석 - Google Cloud Platform 계정 만들기
description: BigQuery Source Connector를 사용하여 Adobe Experience Platform에서 Google Analytics 데이터를 수집 및 분석 - Google Cloud Platform 계정 만들기
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 632ff2fe-ae56-4481-b281-c11224b18639
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---

# 12.1 Google Cloud Platform 계정 만들기

## 목표

- Google Cloud Platform 계정 만들기
- Google Cloud Platform Console에 익숙해지십시오
- BigQuery 프로젝트 만들기 및 준비

## 12.1.1 Google BigQuery를 Adobe Experience Platform에 연결하여 Google Analytics 데이터를 가져오는 이유는 무엇입니까

Google 클라우드 플랫폼(GCP)은 Google에서 제공하는 공용 클라우드 컴퓨팅 서비스 세트입니다. Google 클라우드 플랫폼에는 Google 하드웨어에서 실행되는 컴퓨팅, 스토리지 및 애플리케이션 개발을 위한 다양한 호스팅 서비스가 포함되어 있습니다.

BigQuery는 이러한 서비스 중 하나이며 항상 Google Analytics 360에 포함됩니다. Google Analytics에서 직접 데이터를 가져오려고 하면 데이터 샘플링이 자주 수행됩니다(예: API). Google에 BigQuery가 포함되어 있어 샘플링되지 않은 데이터를 얻을 수 있으므로 브랜드에서는 SQL을 사용하여 고급 분석을 수행할 수 있으며 GCP의 기능을 활용할 수 있습니다.

Google Analytics 데이터는 배치 메커니즘을 사용하여 BigQuery에 매일 로드됩니다. 따라서 실시간 개인화 및 활성화 사용 사례에 이 GCP/BigQuery 통합을 사용하는 것은 적절하지 않습니다.

브랜드가 Google Analytics 데이터를 기반으로 실시간 개인화 사용 사례를 제공하려는 경우 Google 태그 관리자를 사용하여 웹 사이트에서 해당 데이터를 수집한 다음 실시간으로 Adobe Experience Platform으로 스트리밍할 수 있습니다.

GCP/BigQuery Source Connector는..

- 웹 사이트에서 모든 고객 행동을 추적하고 실시간 활성화가 필요하지 않은 분석, 데이터 과학 및 개인화 사용 사례를 위해 Adobe Experience Platform에서 해당 데이터를 로드합니다.
- 분석 및 데이터 과학 사용 사례를 위해 이전 데이터를 Adobe Experience Platform에 다시 로드합니다.

## 12.1.2 Google 계정 만들기

Google Cloud Platform 계정을 얻으려면 Google 계정이 필요합니다.

## 12.1.3 Google Cloud Platform 계정 활성화

이제 Google 계정이 있으므로 Google 클라우드 플랫폼 환경을 만들 수 있습니다. 이렇게 하려면 다음 위치로 이동하십시오. [https://console.cloud.google.com/](https://console.cloud.google.com/).

다음 페이지에서 약관에 동의합니다.

![데모](./images/ex1/1.png)

다음을 클릭합니다. **프로젝트 선택**.

![데모](./images/ex1/2.png)

클릭 **새 프로젝트**.

![데모](./images/ex1/createproject.png)

다음의 명명 규칙에 따라 프로젝트에 이름을 지정하십시오.

| 규칙 | 예 |
| ----------------- |-------------| 
| `--demoProfileLdap---googlecloud` | 델리글러글러클라우드 |

![데모](./images/ex1/3.png)

**만들기**&#x200B;를 클릭합니다.

![데모](./images/ex1/3-1.png)

화면 오른쪽 상단의 알림이 만들기가 끝날 때까지 기다립니다. 그런 다음 **프로젝트 보기**.

![데모](./images/ex1/4.png)

그런 다음 화면 상단의 검색 막대로 이동하여 를 입력합니다 **BigQuery**. 첫 번째 결과를 선택합니다.

![데모](./images/ex1/7.png)

그러면 BigQuery 콘솔로 리디렉션되고 팝업 메시지가 표시됩니다.

**완료**&#x200B;를 클릭합니다.

![데모](./images/ex1/5.png)

이 모듈의 목표는 Google Analytics 데이터를 Adobe Experience Platform으로 가져오는 것입니다. 이를 수행하려면 시작할 Google Analytics 데이터 세트에 있는 더미 데이터가 필요합니다.

클릭 **데이터 추가** 왼쪽 메뉴에서 을 클릭한 다음 **공개 데이터 세트 탐색**.

![데모](./images/ex1/18.png)

그러면 다음 창이 표시됩니다.

![데모](./images/ex1/19.png)

검색어 입력 **Google Analytics 샘플** 검색 막대에서 첫 번째 결과를 선택합니다.

![데모](./images/ex1/20.png)

데이터 세트에 대한 설명이 있는 다음 화면이 표시됩니다. 클릭 **데이터 집합 보기**.

![데모](./images/ex1/21.png)

그러면 이 항목이 표시되는 BigQuery로 리디렉션됩니다 **bigquery-public-data** 데이터 세트 아래의 **탐색기**.

![데모](./images/ex1/22a.png)

in **탐색기**&#x200B;이제 많은 표가 표시됩니다. 자유롭게 탐색해 보세요. `google_analytics_sample`로 이동합니다.

![데모](./images/ex1/22.png)

클릭하여 표를 엽니다 `ga_sessions`.

![데모](./images/ex1/23.png)

다음 연습을 계속하려면 컴퓨터의 별도의 텍스트 파일에 다음 내용을 적어 두십시오.

| 자격 증명 | 이름 지정 | 예 |
| ----------------- |-------------| -------------|
| 프로젝트 이름 | `--demoProfileLdap---googlecloud` | vangeluw-googglecloud |
| 프로젝트 ID | random | completed-task-306413 |

을(를) 클릭하여 프로젝트 이름과 프로젝트 ID를 찾을 수 있습니다 **프로젝트 이름** 상단 메뉴 막대에서 다음을 수행합니다.

![데모](./images/ex1/projectMenu.png)

그러면 오른쪽에 프로젝트 ID가 표시됩니다.

![데모](./images/ex1/projetcselection.png)

이제 연습 12.2로 이동하여 Google Analytics 데이터를 쿼리하여 손이 더럽습니다.

다음 단계: [12.2 BigQuery에서 첫 번째 쿼리 만들기](./ex2.md)

[모듈 12로 돌아가기](./customer-journey-analytics-bigquery-gcp.md)

[모든 모듈로 돌아가기](./../../overview.md)
