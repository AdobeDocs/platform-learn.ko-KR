---
title: 기초 - 데이터 수집
description: 기초 - 데이터 수집
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: dbbc0539-ae1b-488d-b312-76a74d4d361f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 2%

---

# 2. 기초 - 데이터 수집

**작성자: [우터 반 겔루위](https://www.linkedin.com/in/woutervangeluwe/)**

이 모듈에서 목표는 데이터 처리에 대한 모든 것을 학습하는 것입니다. 스트리밍 및 일괄 처리에서 데이터 처리에 대해 알아봅니다. Launch를 사용하여 스트리밍 데이터 섭취 를 구현하므로 실습 랩 웹 사이트의 고객 동작이 실시간으로 Adobe Experience Platform으로 스트리밍됩니다. Adobe Experience Platform 워크플로우를 사용하여 CSV 파일을 가져오고 XDM 스키마에 매핑한 다음 Adobe Experience Platform에 수집하여 배치 데이터 처리에 대해 알아봅니다.

## 학습 목표

- Adobe Experience Platform에서 XDM 스키마를 만드는 방법을 알아보십시오
- Adobe Experience Platform에서 데이터 세트를 만드는 방법을 알아봅니다
- Launch에서 스트리밍 끝점을 만들고 Adobe Experience Platform 확장을 구성하는 방법을 알아봅니다
- Launch에서 규칙을 만들어 데이터를 Adobe Experience Platform으로 스트리밍하는 방법을 알아봅니다
- 웹 페이지에 Adobe Experience Platform Launch을 통합하는 방법을 알아봅니다
- Adobe Experience Platform 워크플로우를 사용하여 CSV 파일을 Adobe Experience Platform에 수집하는 방법을 알아봅니다

## 사전 요구 사항

- Adobe Experience Platform에 액세스: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Adobe Experience Platform Launch 액세스: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- 액세스 권한 [https://public.aepdemo.net](https://public.aepdemo.net)
- Postman 액세스

>[!IMPORTANT]
>
>이 자습서는 특정 워크숍 형식을 용이하게 하기 위해 만들어졌습니다. 액세스 권한이 없을 수 있는 특정 시스템 및 계정을 사용합니다. 액세스 권한이 없더라도 이 매우 자세한 내용을 통해 많은 것을 배울 수 있을 것입니다. 워크샵 중 하나에 참여하고 액세스 자격 증명이 필요한 경우 Adobe 담당자에게 연락하여 필요한 정보를 제공합니다.

## 아키텍처 개요

이 모듈에서 논의하고 사용할 구성 요소를 강조 표시하는 아래 아키텍처를 살펴보십시오.

![아키텍처 개요](../../assets/images/architecturem2.png)

## 사용할 샌드박스

이 모듈의 경우 다음 샌드박스를 사용하십시오. `--module2sandbox--`.

>[!NOTE]
>
>에서 참조한 대로 Chrome 확장 프로그램을 설치, 구성 및 사용하는 것을 잊지 마십시오 [0.1 - Experience League 설명서용 Chrome 확장 프로그램 설치](../module0/ex1.md)

## 연습

[2.1 웹 사이트 탐색](./ex1.md)

이 연습에서는 이 설정의 일부로 사용할 웹 사이트를 살펴봅니다.

[2.2 스키마 구성 및 식별자 설정](./ex2.md)

이 연습에서는 프로필 정보 및 고객 행동을 캡처하도록 필요한 XDM 스키마 를 구성합니다. 모든 XDM 스키마에서는 모든 정보를 연결할 기본 식별자를 구성해야 합니다.

[2.3 데이터 세트 구성](./ex3.md)

이 연습에서는 프로필 정보 및 고객 동작을 캡처하고 저장하는 데 필요한 데이터 세트를 검색합니다.

[2.4 오프라인 소스에서 데이터 수집](./ex4.md)

이 연습에서는 웹 사이트 및 모바일 앱으로 이동하여 고객처럼 데이터를 Platform으로 스트리밍합니다.

[2.5 데이터 랜딩 영역](./ex5.md)

Azure Blob 저장소를 사용하여 데이터 랜딩 영역 소스 커넥터를 설정합니다.

[요약 및 이점](./summary.md)

이 모듈의 요약 및 이점 개요

>[!NOTE]
>
>Adobe Experience Platform에 대해 알아야 할 모든 것을 배우는 데 시간을 투자해주셔서 감사합니다. 질문이 있는 경우 향후 컨텐츠에 대한 제안 사항이 있는 일반적인 피드백을 공유하려는 경우 Outlook Van Geluwe에게 이메일을 직접 보내주십시오 **vangeluw@adobe.com**.

[모든 모듈로 돌아가기](../../overview.md)
