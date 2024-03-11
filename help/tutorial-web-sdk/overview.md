---
title: Web SDK 튜토리얼을 통해 Adobe Experience Cloud 구현
description: Adobe Experience Platform Web SDK를 사용하여 Experience Cloud 애플리케이션을 구현하는 방법에 대해 알아봅니다.
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: 9f75ef042342e1ff9db6039e722159ad96ce5e5b
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 11%

---

# Web SDK 튜토리얼을 통해 Adobe Experience Cloud 구현

>[!CAUTION]
>
>2024년 3월 15일 금요일에 이 자습서에 대한 주요 변경 사항을 게시하려고 합니다. 이 시점 이후에는 많은 연습이 변경되며 모든 단원을 완료하려면 튜토리얼을 처음부터 다시 시작해야 할 수 있습니다.


Adobe Experience Platform Web SDK를 사용하여 Experience Cloud 애플리케이션을 구현하는 방법에 대해 알아봅니다.

Experience Platform Web SDK는 Adobe Experience Cloud 고객이 Adobe Experience Platform Edge Network를 통해 Adobe 애플리케이션 및 서드파티 서비스와 모두 상호 작용할 수 있도록 하는 클라이언트측 JavaScript 라이브러리입니다. 다음을 참조하십시오 [Adobe Experience Platform 웹 SDK 개요](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=ko-KR) 를 참조하십시오.

이 튜토리얼에서는 샘플 소매 웹 사이트인 Luma에서 Platform Web SDK를 구현하는 과정을 안내합니다. 다음 [Luma 사이트](https://luma.enablementadobe.com/content/luma/us/en.html) 에는 사실적인 구현을 구축할 수 있는 풍부한 데이터 레이어와 기능이 있습니다. 이 자습서를 완료한 후에는 자체 웹 사이트에서 Platform Web SDK를 통해 모든 마케팅 솔루션 구현을 시작할 준비가 되어 있어야 합니다.

[![Luma 웹 사이트](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)


## 학습 목표

자습서를 완료하면 다음 작업을 수행할 수 있습니다.

* 데이터스트림 구성

* XDM 스키마 만들기

* 다음 Adobe Experience Cloud 애플리케이션을 추가합니다.
   * **[Adobe Experience Platform](setup-experience-platform.md)** (및 Adobe Real-time Customer Data Platform, Adobe Journey Optimizer, Adobe Customer Journey Analytics 등 플랫폼을 기반으로 구축된 애플리케이션)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**

* 태그 규칙 및 XDM 개체 데이터 요소를 만들어 데이터를 Adobe 응용 프로그램으로 보냅니다.

* Adobe Experience Platform Debugger을 사용하여 구현의 유효성 검사

* 사용자 동의 캡처

* 이벤트 전달을 사용하여 데이터를 서드파티에 전달

>[!NOTE]
>
>에 대해 유사한 다중 솔루션 자습서를 사용할 수 있습니다. [Mobile SDK](../tutorial-mobile-sdk/overview.md).

## 전제 조건

모든 Experience Cloud 고객은 Platform Web SDK를 사용할 수 있습니다. Web SDK를 사용하기 위해 Real-time Customer Data Platform 또는 Journey Optimizer과 같은 플랫폼 기반 애플리케이션에 라이센스를 부여할 필요는 없습니다.

이 단원들에서는 Adobe 계정과 [필수 권한](configure-permissions.md) 레슨을 완료합니다. 그렇지 않은 경우 Experience Cloud 관리자에게 연락하여 액세스 권한을 요청해야 합니다.

또한 HTML 및 JavaScript와 같은 프런트 엔드 개발 언어를 잘 알고 있다고 가정합니다. 이러한 언어에 대해 전문가가 될 필요는 없지만 코드를 읽고 이해할 수 있는 경우 이 자습서를 통해 자세한 내용을 확인할 수 있습니다.

그럼 시작해 보겠습니다!

[다음: ](configure-permissions.md)

>[!NOTE]
>
>Adobe Experience Platform Web SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하려는 경우 또는 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
