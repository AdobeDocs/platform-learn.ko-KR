---
title: Apache Kafka에서 Adobe Experience Platform으로 데이터 스트리밍
description: 이 모듈에서는 Kafka Connect용 Adobe Experience Platform 싱크 커넥터를 사용하여 Apache Kafka 클러스터를 설정하고 주제, 제작자 및 소비자를 정의하고 Adobe Experience Platform으로 데이터를 스트리밍하는 방법에 대해 알아봅니다.
kt: 5342
doc-type: tutorial
exl-id: 28c63675-272e-46ff-88fc-6cd4096d66ca
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 1%

---

# 2.6 Apache Kafka에서 Adobe Experience Platform으로 데이터 스트리밍

이 모듈에서는 Kafka Connect를 통해 Adobe Experience Platform 싱크 커넥터를 사용하여 Apache Kafka 클러스터를 설정하고 주제, 제작자 및 소비자를 정의하고 Adobe Experience Platform으로 데이터를 스트리밍하는 방법에 대해 알아봅니다.

## 학습 목표

- 로컬 Kafka 클러스터의 기본 설정 수행
- Kafka 주제 만들기, Kafka 제작자 및 Kafka 소비자 사용
- Kafka Connect 및 Adobe Experience Platform 싱크 커넥터 구성
- 이벤트를 수동으로 제작하고 해당 이벤트가 Adobe Experience Platform에서 수집되는지 확인
- Kafka Connect에서 기존 Twitter 프로듀서 라이브러리를 사용하여 Twitter 데이터를 Adobe Experience Platform에 스트리밍

## 전제 조건

- Java JDK23 이상을 컴퓨터에 설치해야 합니다. [https://www.oracle.com/java/technologies/javase-jdk11-downloads.html](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)에서 해당 JDK를 다운로드할 수 있습니다.
- Adobe Experience Platform 액세스

>[!NOTE]
>
>[Chrome 설명서용 Chrome 확장 설치](../../../getting-started/gettingstarted/ex1.md)에서 참조한 대로 Experience League 확장 기능을 설치, 구성 및 사용하는 것을 잊지 마십시오

## 연습

[2.6.1 Apache Kafka 소개](./ex1.md)

이 연습에서는 Apache Kafka의 기본 사항에 대해 알아봅니다

[2.6.2 Kafka 클러스터 설치 및 구성](./ex2.md)

이 연습에서는 기본 Apache Kafka 클러스터를 다운로드, 설치 및 구성합니다.

[2.6.3 Adobe Experience Platform에서 HTTP API 스트리밍 끝점 구성](./ex3.md)

이 연습에서는 Adobe Experience Platform에서 HTTP API Source 커넥터를 구성합니다.

[2.6.4 Kafka Connect 및 Adobe Experience Platform 싱크 커넥터 설치 및 구성](./ex4.md)

이 연습에서는 Kafka Connect를 사용하여 Adobe Experience Platform 싱크 커넥터를 설치하고 사용하며 이벤트를 Adobe Experience Platform에 수동으로 전송합니다.

[요약 및 이점](./summary.md)

이 단원의 요약 및 이점 개요

![기술 내부자](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Adobe Experience Platform과 애플리케이션에 대해 알아야 할 모든 것을 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있는 경우 향후 콘텐츠에 대한 제안 사항에 대한 일반적인 피드백을 공유하려면 기술 인사이더에게 **techinsiders@adobe.com**&#x200B;로 전자 메일을 보내 직접 문의하십시오.

[모든 모듈로 돌아가기](./../../../../overview.md)
