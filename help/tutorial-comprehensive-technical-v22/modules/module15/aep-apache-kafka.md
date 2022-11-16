---
title: Apache Kafka에서 Adobe Experience Platform으로 데이터를 스트리밍
description: 이 모듈에서는 Kafka Connect용 Adobe Experience Platform 싱크 커넥터를 사용하여 Apache Kafka 클러스터를 설정하고, 주제, 생산자 및 소비자를 정의하고, 데이터를 Adobe Experience Platform으로 스트리밍하는 방법을 알아봅니다.
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: e1e283b1-93b7-4d06-b9ed-beac48a99c3f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 2%

---

# 15. Apache Kafka에서 Adobe Experience Platform으로 스트림 데이터

**작성자: [비벡 티와리](https://www.linkedin.com/in/vivek-tiwari-25092656/), [니푼 네어](https://www.linkedin.com/in/nipunnair/), [우터 반 겔루위](https://www.linkedin.com/in/woutervangeluwe/)**

이 모듈에서는 Kafka Connect를 통해 Adobe Experience Platform 싱크 커넥터를 사용하여 Apache Kafka 클러스터를 설정하고, 주제, 생산자 및 소비자를 정의하고, 데이터를 Adobe Experience Platform으로 스트리밍하는 방법을 알아봅니다.

## 학습 목표

- 로컬 Kafka 클러스터의 기본 설정 수행
- Kafka 주제를 만들고, Kafka 생성자와 Kafka 소비자를 사용합니다
- Kafka 연결 및 Adobe Experience Platform 싱크 커넥터 구성
- 이벤트를 수동으로 생성하고 Adobe Experience Platform에서 해당 이벤트를 수집하도록 확인합니다
- Kafka Connect의 기존 Twitter 생성 라이브러리를 사용하여 Twitter 데이터를 Adobe Experience Platform으로 스트리밍할 수 있습니다

## 전제 조건

- Java JDK11 이상을 컴퓨터에 설치해야 합니다. 여기에서 해당 JDK를 다운로드할 수 있습니다. [https://www.oracle.com/java/technologies/javase-jdk11-downloads.html](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)
- Adobe Experience Platform 액세스

## 아키텍처 개요

이 모듈에서 논의하고 사용할 구성 요소를 강조 표시하는 아래 아키텍처를 살펴보십시오.

![아키텍처 개요](../../assets/images/architecturem24.png)

## 사용할 샌드박스

이 모듈의 경우 다음 샌드박스를 사용하십시오. `--aepSandboxId--`.

>[!NOTE]
>
>에서 참조한 대로 Chrome 확장 프로그램을 설치, 구성 및 사용하는 것을 잊지 마십시오 [0.1 - Experience League 설명서용 Chrome 확장 프로그램 설치](../module0/ex1.md)

## 연습

[15.1 Apache Kafka 소개](./ex1.md)

이 연습에서는 Apache Kafka의 기본 사항에 대해 학습할 수 있습니다

[15.2 Kafka 클러스터 설치 및 구성](./ex2.md)

이 연습에서는 기본 Apache Kafka 클러스터를 다운로드, 설치 및 구성합니다.

[15.3 Adobe Experience Platform에서 HTTP API 스트리밍 끝점 구성](./ex3.md)

이 연습에서는 Adobe Experience Platform에서 HTTP API 소스 커넥터를 구성합니다.

[15.4 Kafka Connect 및 Adobe Experience Platform Sink Connector 설치 및 구성](./ex4.md)

이 연습에서는 Kafka Connect를 사용하여 Adobe Experience Platform 싱크 커넥터를 설치하고 사용할 수 있으며, 이벤트를 Adobe Experience Platform에 수동으로 보냅니다.

[요약 및 이점](./summary.md)

이 모듈의 요약 및 이점 개요

>[!NOTE]
>
>Adobe Experience Platform에 대해 알아야 할 모든 것을 배우는 데 시간을 투자해주셔서 감사합니다. 질문이 있는 경우 향후 컨텐츠에 대한 제안 사항이 있는 일반적인 피드백을 공유하려는 경우 Outlook Van Geluwe에게 이메일을 직접 보내주십시오 **vangeluw@adobe.com**.

[모든 모듈로 돌아가기](../../overview.md)
