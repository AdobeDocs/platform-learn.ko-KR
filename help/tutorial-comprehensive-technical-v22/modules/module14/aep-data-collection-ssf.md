---
title: Adobe Experience Platform 데이터 수집 및 실시간 서버 측 전달
description: 이 모듈에서는 이전에 구성한 데이터 세트, 스키마 및 Adobe Experience Platform 데이터 수집 서버 속성을 사용하여 데이터를 수집한 다음 해당 데이터 서버측을 선택한 종단점으로 전달합니다.
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: c157ca52-c84f-4398-a658-2b6067e41707
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 1%

---

# 14. Real-Time CDP 연결: 이벤트 전달

**작성자: [우터 반 겔루위](https://www.linkedin.com/in/woutervangeluwe/), [클레멘트 델랄란드](https://www.linkedin.com/in/clement-delalande/)**

이 모듈에서는 이전에 구성한 데이터 세트, 스키마 및 Adobe Experience Platform 데이터 수집 클라이언트 속성을 사용하여 데이터를 수집한 다음 해당 데이터 서버측을 선택한 종단점으로 전달합니다.

이 모듈에서 다음을 수행합니다.

- Adobe Experience Platform 데이터 수집 서버 속성 만들기
- Adobe Experience Platform 데이터 수집에서 Cloud Connector 확장을 설치하고 사용합니다
- Google 함수 종단점을 만들고 이 종단점에 데이터를 스트리밍합니다
- AWS 종단점을 만들고 이 종단점에 데이터를 스트리밍합니다

가치, 고객 여정 및 구성 프로세스를 이해하려면 다음 비디오를 시청하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/331987?quality=12&learn=on)

## 학습 목표

- Adobe Experience Platform 데이터 수집 서버 속성 및 새로운 Adobe 클라우드 커넥터 확장에 대해 숙지하십시오
- Google 및 AWS과 같은 타사 솔루션에서 Adobe Experience Platform Web SDK 데이터를 다시 사용하는 방법을 이해합니다
- Adobe Experience Platform 데이터 수집 및 서버 측 전달의 이면에 대한 아키텍처를 이해합니다.

## 전제 조건

- Adobe Experience Platform 및 Adobe Experience Platform 데이터 수집에 대한 액세스
- Adobe Experience Platform 데이터 세트 및 XDM 이해

>[!IMPORTANT]
>
>이 자습서는 특정 워크숍 형식을 용이하게 하기 위해 만들어졌습니다. 액세스 권한이 없을 수 있는 특정 시스템 및 계정을 사용합니다. 액세스 권한이 없더라도 이 매우 자세한 내용을 통해 많은 것을 배울 수 있을 것입니다. 워크샵 중 하나에 참여하고 액세스 자격 증명이 필요한 경우 Adobe 담당자에게 연락하여 필요한 정보를 제공합니다.

## 아키텍처 개요

이 모듈에서 논의하고 사용할 구성 요소를 강조 표시하는 아래 아키텍처를 살펴보십시오.

![아키텍처 개요](../../assets/images/architecturem21.png)

## 사용할 샌드박스

이 모듈의 경우 다음 샌드박스를 사용하십시오. `--aepSandboxId--`.

>[!NOTE]
>
>에서 참조한 대로 Chrome 확장 프로그램을 설치, 구성 및 사용하는 것을 잊지 마십시오 [0.1 - Experience League 설명서용 Chrome 확장 프로그램 설치](../module0/ex1.md)

## 연습

[14.1 데이터 수집 이벤트 전달 속성 만들기](./ex1.md)

이 연습에서는 Adobe Experience Platform 데이터 수집 이벤트 전달 속성을 만듭니다.

[14.2 데이터 스트림을 업데이트하여 데이터 수집 이벤트 전달 속성에 데이터를 사용할 수 있도록 합니다](./ex2.md)

이 연습에서는 기존 데이터 스트림을 업데이트하여 Adobe Experience Platform 데이터 수집 클라이언트 속성으로 수집한 데이터를 Adobe Experience Platform 데이터 수집 서버 속성에 사용할 수 있도록 합니다.

[14.3 사용자 지정 웹 후크 만들기 및 구성](./ex3.md)

이 연습에서는 사용자 지정 웹 후크를 만들고 구성하고 Web SDK에서 수집한 데이터를 해당 사용자 지정 웹 후크에 전달하기 시작합니다.

[14.4 Google 클라우드 기능 만들기 및 구성](./ex4.md)

이 연습에서는 Google 클라우드 기능을 만들고 구성하며, 웹 SDK에서 수집한 데이터 전달을 Google에 시작합니다.

[14.5 AWS 에코시스템을 위한 Forward 이벤트](./ex5.md)

이 연습에서는 AWS API Gateway, AWS Kinesis, AWS Firehose 및 AWS S3를 사용하여 AWS 환경을 구성하고 그 후에 웹 SDK에서 수집한 이벤트 데이터 전달을 시작합니다.

[요약 및 이점](./summary.md)

이 모듈의 요약 및 이점 개요

>[!NOTE]
>
>Adobe Experience Platform에 대해 알아야 할 모든 것을 배우는 데 시간을 투자해주셔서 감사합니다. 질문이 있는 경우 향후 컨텐츠에 대한 제안 사항이 있는 일반적인 피드백을 공유하려는 경우 Outlook Van Geluwe에게 이메일을 직접 보내주십시오 **vangeluw@adobe.com**.

[모든 모듈로 돌아가기](../../overview.md)
