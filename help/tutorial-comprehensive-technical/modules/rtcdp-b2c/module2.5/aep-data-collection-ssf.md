---
title: Adobe Experience Platform 데이터 수집 및 실시간 서버측 전달
description: 이 모듈에서는 이전에 구성한 데이터 세트, 스키마 및 Adobe Experience Platform 데이터 수집 서버 속성을 사용하여 데이터를 수집한 다음 해당 데이터 서버측을 선택한 엔드포인트에 전달합니다.
kt: 5342
doc-type: tutorial
exl-id: aa3ab1eb-6fee-4ea9-9a0d-0d8ca803d7c2
source-git-commit: bd46be455f88007174f7e6be9a1ce5f508edc09b
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# 2.5 Real-Time CDP 연결: 이벤트 전달

이 모듈에서는 이전에 구성한 데이터 세트, 스키마 및 Adobe Experience Platform 데이터 수집 클라이언트 속성을 사용하여 데이터를 수집한 다음 해당 데이터 서버측을 선택한 엔드포인트에 전달합니다.

이 단원에서는 다음과 같은 작업을 수행합니다.

- Adobe Experience Platform 데이터 수집 서버 속성 만들기
- Adobe Experience Platform 데이터 수집에서 Adobe Cloud Connector 확장 설치 및 사용
- Google 함수 엔드포인트를 만들고 데이터를 해당 엔드포인트로 스트리밍
- AWS 엔드포인트를 만들고 데이터를 해당 엔드포인트에 스트리밍

## 학습 목표

- Adobe Experience Platform 데이터 수집 서버 속성 및 새로운 Adobe Cloud Connector 확장 숙지
- Google 및 AWS과 같은 타사 솔루션에서 Adobe Experience Platform Web SDK 데이터를 재사용하는 방법을 이해합니다
- Adobe Experience Platform 데이터 수집 및 서버측 전달의 아키텍처 이해

## 전제 조건

- Adobe Experience Platform 및 Adobe Experience Platform 데이터 수집 액세스
- Adobe Experience Platform 데이터 세트 및 XDM 이해

>[!NOTE]
>
>[Experience League 설명서용 Chrome 확장 설치](../../gettingstarted/gettingstarted/ex1.md)에서 참조한 대로 Chrome 확장 기능을 설치, 구성 및 사용하는 것을 잊지 마십시오

## 연습

[2.5.1 데이터 수집 이벤트 전달 속성 만들기](./ex1.md)

이 연습에서는 Adobe Experience Platform 데이터 수집 이벤트 전달 속성을 만듭니다.

[2.5.2 데이터 수집 이벤트 전달 속성에서 데이터를 사용할 수 있도록 데이터 스트림 업데이트](./ex2.md)

이 연습에서는 기존 데이터 스트림을 업데이트하여 Adobe Experience Platform 데이터 수집 클라이언트 속성으로 수집된 데이터를 Adobe Experience Platform 데이터 수집 서버 속성으로 사용할 수 있도록 합니다.

[2.5.3 사용자 지정 Webhook 만들기 및 구성](./ex3.md)

이 연습에서는 사용자 지정 웹후크를 만들고 구성하고 Web SDK에서 수집한 데이터를 해당 사용자 지정 웹후크로 전달하기 시작합니다.

[2.5.4 GCP Pub/Sub로 이벤트 전달](./ex4.md)

이 연습에서는 Google Cloud 함수를 만들고 구성하며, Web SDK에서 수집한 데이터를 Google으로 전달하기 시작합니다.

[2.5.5 AWS Kinesis 및 AWS S3에 이벤트 전달](./ex5.md)

이 연습에서는 AWS IAM, AWS Kinesis, AWS Firehose 및 AWS S3를 사용하여 AWS 환경을 구성한 후 웹 SDK에서 수집하는 이벤트 데이터를 전달하기 시작합니다.

[요약 및 이점](./summary.md)

이 단원의 요약 및 이점 개요

![기술 내부자](./../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Adobe Experience Platform과 애플리케이션에 대해 알아야 할 모든 것을 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있는 경우 향후 콘텐츠에 대한 제안 사항에 대한 일반적인 피드백을 공유하려면 기술 인사이더에게 **techinsiders@adobe.com**&#x200B;로 전자 메일을 보내 직접 문의하십시오.

[모든 모듈로 돌아가기](../../../overview.md)
