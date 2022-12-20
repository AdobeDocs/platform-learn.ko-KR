---
title: Web SDK 튜토리얼을 통해 Adobe Experience Cloud 구현
description: Adobe Experience Platform Web SDK를 사용하여 Experience Cloud 애플리케이션을 구현하는 방법을 알아봅니다.
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 26%

---

# Web SDK 튜토리얼을 통해 Adobe Experience Cloud 구현

Adobe Experience Platform Web SDK를 사용하여 Experience Cloud 애플리케이션을 구현하는 방법을 알아봅니다.

Experience Platform Web SDK는 Adobe Experience Cloud 고객이 Adobe Experience Platform Edge 네트워크를 통해 Adobe 애플리케이션과 타사 서비스와 상호 작용할 수 있는 클라이언트측 JavaScript 라이브러리입니다. 자세한 내용은 [Adobe Experience Platform Web SDK 개요](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html) 를 참조하십시오.

이 자습서에서는 Luma라는 샘플 소매 웹 사이트에서 Platform Web SDK의 구현을 안내합니다. [](https://luma.enablementadobe.com/content/luma/us/en.html)Luma 사이트에서는 사실적인 구현을 구축할 수 있는 풍부한 데이터 레이어 및 기능이 제공됩니다. 이 자습서를 완료하고 나면 웹 사이트에서 Platform Web SDK를 통해 모든 마케팅 솔루션 구현을 시작할 수 있습니다.

[![Luma 웹 사이트](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)


## 학습 목표

자습서를 완료하면 다음 작업을 수행할 수 있습니다.

* 데이터스트림 구성

* XDM 스키마 만들기

* 다음 Adobe Experience Cloud 애플리케이션을 추가합니다.
   * **[Adobe Experience Platform](setup-experience-platform.md)** (그리고 Adobe Real-time Customer Data Platform, Adobe Journey Optimizer, Adobe Customer Journey Analytics 등의 플랫폼에서 구축된 애플리케이션)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**

* 태그 규칙 및 XDM 개체 데이터 요소를 만들어 Adobe 응용 프로그램으로 데이터를 보냅니다

* Adobe Experience Platform Debugger를 사용하여 구현의 유효성 검사

* 사용자 동의 캡처

* 이벤트 전달을 사용하여 데이터를 타사에 전달

>[!NOTE]
>
>에 대해 유사한 다중 솔루션 자습서를 사용할 수 있습니다 [Mobile SDK](../tutorial-mobile-sdk/overview.md).

## 전제 조건

모든 Experience Cloud 고객은 Platform Web SDK를 사용할 수 있습니다. Real-time Customer Data Platform 또는 Journey Optimizer과 같은 플랫폼 기반 애플리케이션에 웹 SDK를 사용하기 위해 라이센스를 부여할 필요는 없습니다.

이 단원들에서는 사용자에게 Adobe 계정과 [필수 권한](configure-permissions.md) 를 클릭하여 단원을 완료합니다. 그렇지 않은 경우 Experience Cloud 관리자에게 연락하여 액세스 권한을 요청해야 합니다.

또한 HTML 및 JavaScript와 같은 프런트 엔드 개발 언어를 잘 알고 있다고 가정합니다. 이러한 언어를 다루는 전문가가 될 필요는 없지만 코드를 읽고 이해할 수 있는 경우 이 자습서를 통해 더 많은 정보를 얻을 수 있습니다.

그럼 시작해 보겠습니다!

[다음: ](configure-permissions.md)

>[!NOTE]
>
>Adobe Experience Platform Web SDK에 대한 학습에 시간을 내주셔서 감사합니다. 질문이 있거나 일반 피드백을 공유하거나 향후 컨텐츠에 대한 제안 사항이 있는 경우 해당 정보를 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
