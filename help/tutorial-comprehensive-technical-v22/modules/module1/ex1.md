---
title: Foundation - Adobe Experience Platform 데이터 수집 및 Web SDK 확장 설정 - Adobe Experience Platform 데이터 수집 설명
description: Foundation - Adobe Experience Platform 데이터 수집 및 Web SDK 확장 설정 - Adobe Experience Platform 데이터 수집 설명
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: f498bb8c-659c-44b4-bb2e-36ea14640773
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 5%

---

# 1.1 Adobe Experience Platform 데이터 수집 이해

## 컨텍스트

Adobe Experience Platform 데이터 수집은 많은 사용 사례에 대해 브랜드에서 사용합니다. 관련 고객 환경을 향상하는 데 필요한 모든 분석, 마케팅 및 광고 솔루션을 배포하고 관리하는 간단한 방법을 고객에게 제공하는 차세대 Tag Management 시스템(TMS)입니다. Adobe Experience Platform 데이터 수집에 대한 추가 요금은 없으며 모든 Adobe Experience Cloud 고객이 사용할 수 있습니다. 브랜드에서는 Adobe Experience Platform 데이터 수집을 사용하여 다음을 수행할 수 있습니다.

- Adobe Experience Platform과 Adobe Experience Cloud 애플리케이션을 구현합니다.
- 각각 고유한 요구 사항을 제공하여 조직의 여러 부분에 대한 다양한 요구 사항을 관리합니다 **속성** 관리
- 테스트 및 수명 주기 관리를 허용합니다.
- 사용자 지정 Javascript와 타사 태그를 주입하고, 모두 한 곳에서 관리됩니다.

## UI 살펴보기

이동 [Adobe Experience Platform 데이터 수집](https://experience.adobe.com/#/data-collection/).

이동 **태그**. 이제 **[!UICONTROL 속성]** 보기. 여기에 나열된 속성은 자습서 관리를 위한 것입니다. 다음 속성은..

- 앱 및 웹 속성
- 다양한 방식으로 고객을 제공하는 다양한 웹 사이트 예를 들어 Luma Retail에는 하나의 속성이 있고, Luma Travel에는 또 다른 속성이 있습니다
- 기존 및 현재 웹 사이트
- 다양한 웹 사이트에 공통으로 사용되는 특정 Adobe Analytics 디자인
- 외부 사이트와 함께 내부 인트라넷 페이지

![론치 속성 보기](./images/launch1.png)

이제 왼쪽 레일을 보세요.

![왼쪽 레일 시작](./images/launch2.png)

- **[!UICONTROL 태그]** 모든 클라이언트측 속성에 대한 개요를 제공합니다.
- **[!UICONTROL 앱 서피스]** 모든 앱 구성에 대한 개요를 제공하여 푸시 알림(Project Sierra와 함께 사용/사용)을 활성화합니다
- **[!UICONTROL 데이터 스트림]** 그 안에서 탐험 [다음 연습](./ex2.md)
- **[!UICONTROL 이벤트 전달]** 에서 탐색된 모든 서버측 속성에 대한 개요를 제공합니다. [모듈 14 - Real-Time CDP 연결: 이벤트 전달](../module14/aep-data-collection-ssf.md)

## 추가 정보

Adobe Experience Platform 데이터 수집은 Adobe Experience Platform 자습서를 벗어나는 범위를 제공하는 매우 고급 도구입니다. 조직에서 태그 관리 기능에 Adobe Experience Platform 데이터 수집을 사용하지 않고 코드를 주입하고 태그를 관리하는 데 Adobe이 아닌 태그 관리 솔루션을 사용할 수 있습니다. 비Adobe 태그 관리 솔루션을 사용하는 것은 Adobe 및 Adobe Professional Services에서 지원합니다.
Adobe Experience Platform 데이터 수집을 이해하는 데 도움이 되는 사용자를 위한 일부 추가 독서는 아래에 포함되어 있습니다.

- [Adobe Experience Platform 데이터 수집 사용 안내서](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)
- [Web SDK 튜토리얼을 통해 Adobe Experience Cloud 구현](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=ko-KR)
- [사용자 권한 설정](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html)
- [API 설명서](https://developer.adobelaunch.com/api/)

다음 단계: [1.2 Edge Network, 데이터 스트림 및 서버 측 데이터 수집](./ex2.md)

[모듈 1로 돌아가기](./data-ingestion-launch-web-sdk.md)

[모든 모듈로 돌아가기](./../../overview.md)
