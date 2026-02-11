---
title: 관계형 데이터 기반 설정
description: 관계형 데이터 기반 설정
kt: 5342
doc-type: tutorial
exl-id: 532e5f2c-971f-488f-bef4-3a8141408cc8
source-git-commit: bf3bebfa3bd79829da5352e950aed3f4ef5bf6d1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 6%

---

# 3.8.1 관계형 데이터 기반 설정

[https://experience.adobe.com](https://experience.adobe.com)&#x200B;(으)로 이동하여 Adobe Journey Optimizer에 로그인합니다. **Journey Optimizer**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/aechome.png)

Journey Optimizer의 **Home** 보기로 리디렉션됩니다. 먼저 올바른 샌드박스를 사용하고 있는지 확인하십시오. 사용할 샌드박스를 `--aepSandboxName--`이라고 합니다.

![AJO OC](./images/ajohome.png)

## 3.8.1.1 관계형 기반 스키마 설정

관계형 기반 스키마는 모델 기반 데이터 모델에 대한 형식적 정의입니다.

다음을 지정합니다.

- 테이블 세트
- 각 테이블의 열
- 제한
- 테이블 간의 관계

모델 기반 데이터 모델에서 스키마 또는 테이블 구성은 데이터를 여러 테이블로 구조화하는 것입니다. 각 테이블에 한 가지 유형의 엔티티/스키마가 저장되어 있는지 확인합니다.

Adobe Journey Optimizer Orchestrated Campaigns를 사용하기위해에 데이터를 수집하는 경우 다음 소스를 사용할 수 있습니다.

- Amazon S3
- Google 클라우드 스토리지
- SFTP
- Snowflake
- Google BigQuery
- 데이터 랜딩 구역
- Azure Databricks
- 로컬 파일 업로드

이 연습의 첫 번째 단계는 관계형 기반 XDM 스키마의 구성입니다. 왼쪽 메뉴에서 **데이터 관리**(으)로 스크롤한 다음 **스키마**&#x200B;를 선택합니다. **+ 스키마 만들기**&#x200B;를 클릭합니다.

![AJO OC](./images/ajoocdata1.png)

**관계형**&#x200B;을(를) 선택하십시오.

![AJO OC](./images/ajoocdata2.png)

**DDL 파일 업로드**&#x200B;를 선택한 다음 **파일 선택**&#x200B;을 클릭합니다.

![AJO OC](./images/ajoocdata3.png)

이제 관계형 XDM 스키마가 구성되고 데이터가 수집되므로, 다음 연습에서 해당 데이터를 사용하여 오케스트레이션된 캠페인을 생성할 수 있습니다.

## 3.8.1.2 데이터 수집


## 다음 단계

[오케스트레이션된 캠페인 만들기](./ex2.md){target="_blank"}(으)로 이동

[Adobe Journey Optimizer: 캠페인](./ajocampaigns.md){target="_blank"}(으)로 돌아가기

[모든 모듈](./../../../../overview.md){target="_blank"}(으)로 돌아가기
