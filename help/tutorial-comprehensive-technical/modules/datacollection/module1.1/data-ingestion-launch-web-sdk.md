---
title: 1.1 Adobe Experience Platform 데이터 수집 및 웹 SDK 확장 설정
description: 기초 - Adobe Experience Platform 데이터 수집 및 웹 SDK 확장 설정
kt: 5342
doc-type: tutorial
exl-id: b69ebe41-ff28-4dde-b639-198201120742
source-git-commit: 1526661a80b4d551627dfca42a7e97c9498dd1f2
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---

# 1.1 Foundation - Adobe Experience Platform 데이터 수집 및 웹 SDK 태그 확장 설정

이 기본 모듈에서는 Adobe의 데이터 수집 비전을 소개하고 Adobe Experience Platform 데이터 수집, Adobe Experience Platform SDK 및 Adobe Experience Platform Edge Network을 통해 웹 사이트 및 모바일 애플리케이션에서 Adobe Experience Platform 및 기타 애플리케이션으로 데이터를 가져오는 방법에 대해 설명합니다.

이 모듈에서는 Adobe Experience Platform 기술 튜토리얼의 범위를 벗어나는 데 영향을 미치는 몇 가지 개념과 기술을 소개합니다. 이 연습의 어떤 부분이 나머지 종합 자습서의 기본이 되는지 분명해야 합니다. 이 자습서에서는 Edge Network 및 해당 기능에 대해 자세히 설명하며 추가 정보 및 자습서는 어디로 이동해야 하는지 설명합니다.

## 학습 목표

- 브랜드가 Adobe Experience Platform 데이터 수집을 TMS(Tag Management System)로 사용하는 방법을 알아봅니다.
- 브랜드가 Adobe 제품으로 데이터를 수집하는 데 사용하는 데이터 흐름에 대해 알아봅니다.
- Adobe Experience Platform Edge Network을 통해 Adobe Experience Platform 및 기타 제품에 데이터를 전송하는 방법을 알아봅니다.
- 웹 및 모바일에서 데이터를 수집하는 데이터 요소 및 규칙을 만드는 방법을 알아봅니다.
- [Web SDK](https://experienceleague.adobe.com/ko/docs/experience-platform/web-sdk/home) 추적 이벤트와 해당 콘텐츠를 디버깅하는 방법에 대해 알아봅니다.
- 데이터 계층이 무엇이고 데이터 계층을 구현할 때 Adobe이 권장하는 사항을 알아봅니다.
- [웹 SDK](https://experienceleague.adobe.com/ko/docs/experience-platform/web-sdk/home)을(를) 처음부터 구현하는 단계에 대해 알아봅니다.
- 웹 구현과 모바일 구현의 차이점에 대해 알아봅니다.

## 전제 조건

- Adobe Experience Platform 액세스: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Adobe Experience Platform 데이터 수집에 액세스: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- 데모 웹 사이트 액세스

>[!NOTE]
>
>[Experience League 설명서용 Chrome 확장 설치](../../gettingstarted/gettingstarted/ex1.md)에서 참조한 대로 Chrome 확장 기능을 설치, 구성 및 사용하는 것을 잊지 마십시오

## 연습

[1.1.1 Adobe Experience Platform 데이터 수집 이해](./ex1.md)

이 연습에서는 Adobe Experience Platform 데이터 수집 UI를 살펴보고 그 기능에 대해 알아봅니다.

[1.1.2 Edge Network, 데이터스트림 및 서버측 데이터 수집](./ex2.md)

이 연습에서는 Adobe Experience Platform 데이터 수집 인터페이스에서 Adobe 제품으로 데이터를 전달하고 데모 웹 사이트에서 사용하는 데이터 스트림을 조사하는 방법에 대해 알아봅니다.

[1.1.3 Adobe Experience Platform 데이터 수집 소개](./ex3.md)

이 연습에서는 확장을 설정하고 데이터 요소와 규칙을 빌드하고 웹에 게시하는 방법에 대해 알아봅니다.

[1.1.4 클라이언트측 웹 데이터 수집](./ex4.md)

이 연습에서는 설치된 웹 SDK을 디버깅하여 작동 방식과 향후 연습에서 사용할 데이터를 파악합니다.

[1.1.5 Adobe Analytics 및 Adobe Audience Manager 구현](./ex5.md)

이 연습에서는 Adobe Analytics 및 Adobe Audience Manager의 웹 SDK으로 수집된 웹 데이터를 참조하고 사용합니다.

[1.1.6 Adobe Target 구현](./ex6.md)

이 연습에서는 웹 SDK을 통해 구현된 Adobe Target에서 활동을 설정합니다.

[Adobe Experience Platform의 1.1.7 XDM 스키마 요구 사항](./ex7.md)

웹 SDK에서 Adobe Experience Platform으로 데이터를 수집할 수 있도록 하려면 Adobe Experience Platform에서 특정 XDM mixin이 XDM 스키마의 일부가 되어야 합니다.

[요약 및 이점](./summary.md)

이 단원의 요약 및 이점 개요

![기술 내부자](./../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Adobe Experience Platform과 애플리케이션에 대해 알아야 할 모든 것을 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있는 경우 향후 콘텐츠에 대한 제안 사항에 대한 일반적인 피드백을 공유하려면 기술 인사이더에게 **techinsiders@adobe.com**&#x200B;로 전자 메일을 보내 직접 문의하십시오.

[모든 모듈로 돌아가기](../../../overview.md)
