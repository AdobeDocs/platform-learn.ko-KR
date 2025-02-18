---
title: 기초 - 데이터 수집
description: 기초 - 데이터 수집
kt: 5342
doc-type: tutorial
exl-id: 0fa38179-637b-4dda-a4e4-754a4cdd61a8
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 1%

---

# 1.2 데이터 수집

이 모듈에서는 데이터 수집에 대한 모든 것을 학습하는 것이 목표입니다. 스트리밍 및 일괄 처리에서의 데이터 수집에 대해 알아봅니다. Launch를 사용하여 스트리밍 데이터 수집을 구현하므로 실습형 랩 웹 사이트의 고객 행동이 실시간으로 Adobe Experience Platform으로 스트리밍됩니다. Adobe Experience Platform Workflow를 사용하여 CSV 파일을 가져오고 XDM 스키마에 매핑한 다음 Adobe Experience Platform에 수집하는 일괄 데이터 수집에 대해 알아봅니다.

## 학습 목표

- Adobe Experience Platform에서 XDM 스키마를 만드는 방법 알아보기
- Adobe Experience Platform에서 데이터 세트를 만드는 방법 알아보기
- Launch에서 스트리밍 끝점을 만들고 Adobe Experience Platform 확장을 구성하는 방법을 알아봅니다.
- Launch에서 규칙을 만들어 Adobe Experience Platform에 데이터를 스트리밍하는 방법에 대해 알아봅니다.
- Adobe Experience Platform Launch을 웹 페이지에 통합하는 방법을 알아봅니다
- Adobe Experience Platform Workflow를 사용하여 CSV 파일을 Adobe Experience Platform으로 수집하는 방법에 대해 알아봅니다

## 전제 조건

- Adobe Experience Platform 액세스: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Adobe Experience Platform Launch 액세스: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Postman 액세스

>[!NOTE]
>
>[Chrome 설명서용 Chrome 확장 설치](../../../getting-started/gettingstarted/ex1.md)에서 참조한 대로 Experience League 확장 기능을 설치, 구성 및 사용하는 것을 잊지 마십시오

## 연습

[1.2.1 웹 사이트 탐색](./ex1.md)

이 연습에서는 이 기능의 일부로 사용할 웹 사이트를 탐색합니다.

[1.2.2 스키마 및 식별자 설정 구성](./ex2.md)

이 연습에서는 프로필 정보 및 고객 행동을 캡처하는 데 필요한 XDM 스키마를 구성합니다. 모든 XDM 스키마에서는 모든 정보를 연결할 기본 식별자도 구성해야 합니다.

[1.2.3 데이터 세트 구성](./ex3.md)

이 연습에서는 프로필 정보 및 고객 행동을 캡처하고 저장하는 데 필요한 데이터 세트를 검색합니다.

[1.2.4 오프라인 소스에서 데이터 수집](./ex4.md)

이 연습에서는 웹 사이트 및 모바일 앱에서 데이터를 Platform으로 스트리밍하여 고객처럼 행동합니다.

[1.2.5 데이터 랜딩 영역](./ex5.md)

Azure Blob 저장소를 사용하여 데이터 랜딩 영역 Source 커넥터를 설정합니다.

[요약 및 이점](./summary.md)

이 단원의 요약 및 이점 개요

![기술 내부자](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Adobe Experience Platform과 애플리케이션에 대해 알아야 할 모든 것을 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있는 경우 향후 콘텐츠에 대한 제안 사항에 대한 일반적인 피드백을 공유하려면 기술 인사이더에게 **techinsiders@adobe.com**&#x200B;로 전자 메일을 보내 직접 문의하십시오.

[모든 모듈로 돌아가기](./../../../../overview.md)
