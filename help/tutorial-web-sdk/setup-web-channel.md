---
title: Platform Web SDK를 사용하여 Journey Optimizer 웹 채널 설정
description: Platform Web SDK를 사용하여 Journey Optimizer 웹 채널을 구현하는 방법에 대해 알아봅니다. 이 단원은 Web SDK를 사용하여 Adobe Experience Cloud 구현 자습서의 일부입니다.
solution: Data Collection,Experience Platform,Journey Optimizer
feature-set: Journey Optimizer
feature: Web Channel,Web SDK
jira: KT-15411
exl-id: ab83ce56-7f54-4341-8750-b458d0db0239
source-git-commit: 8602110d2b2ddc561e45f201e3bcce5e6a6f8261
workflow-type: tm+mt
source-wordcount: '2892'
ht-degree: 0%

---


# Web SDK를 사용하여 Journey Optimizer 웹 채널 설정

Adobe Journey Optimizer 구현 방법 알아보기 [웹 채널](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/web/get-started-web) Adobe Experience Platform Web SDK를 사용합니다. 이 단원에서는 기본 웹 채널 사전 요구 사항, 구성을 위한 자세한 단계 및 충성도 상태를 중심으로 하는 사용 사례에 대해 설명합니다.

이 단원을 따르면 Journey Optimizer 사용자는 Journey Optimizer 웹 디자이너를 사용하여 고급 온라인 개인화에 웹 채널을 사용할 수 있습니다.

![Web SDK 및 Adobe Analytics 다이어그램](assets/dc-websdk-ajo.png)

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* 웹 채널 경험을 게재할 때 웹 SDK의 기능과 중요성을 이해합니다.
* 샘플 Luma 충성도 보상 사용 사례를 활용하여 처음부터 끝까지 웹 채널 캠페인을 만드는 프로세스를 이해합니다.
* 인터페이스 내에서 캠페인 속성, 작업 및 일정을 구성합니다.
* Adobe Experience Cloud Visual Editing Helper 확장 기능의 기능과 이점을 이해합니다.
* 웹 디자이너를 사용하여 이미지, 헤더 및 기타 요소를 포함한 웹 페이지 콘텐츠를 편집하는 방법에 대해 알아봅니다.
* 오퍼 결정 구성 요소를 사용하여 웹 페이지에 오퍼를 삽입하는 방법을 알아봅니다.
* 웹 채널 캠페인의 품질과 성공을 보장하기 위한 모범 사례를 숙지하십시오.

## 전제 조건

이 섹션의 학습 내용을 완료하려면 먼저 다음을 수행해야 합니다.

* 데이터 요소 및 규칙 설정을 포함하여 Platform Web SDK의 초기 구성에 대한 모든 단원을 완료합니다.
* Adobe Experience Platform Web SDK 태그 확장 버전이 2.16 이상인지 확인하십시오.
* Journey Optimizer 웹 디자이너를 사용하여 웹 채널 경험을 작성하는 경우 Google Chrome 또는 Microsoft® Edge 브라우저를 사용하는지 확인하십시오.
* 또한 을 다운로드하고 활성화했는지 확인합니다. [Adobe Experience Cloud Visual Editing Helper 브라우저 확장 기능](https://chromewebstore.google.com/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca).
* 브라우저에서 서드파티 쿠키가 허용되는지 확인하십시오. 브라우저에서 광고 차단기를 비활성화해야 할 수도 있습니다.

  >[!CAUTION]
  >
  > Journey Optimizer 웹 디자이너에서 특정 웹 사이트는 다음 이유 중 하나로 인해 안정적으로 열리지 않을 수 있습니다.
  > 
  > 1. 웹 사이트에는 엄격한 보안 정책이 있습니다.
  > 1. 웹 사이트는 iframe 내에 포함됩니다.
  > 1. 고객의 QA 또는 스테이지 사이트는 외부에서 액세스할 수 없습니다(내부 사이트임).

* 웹 경험을 만들고 Adobe Experience Manager Assets Essentials 라이브러리의 콘텐츠를 포함할 때에는 다음을 수행해야 합니다. [이 콘텐츠를 게시하기 위한 하위 도메인 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/web/configure-web-channel/web-delegated-subdomains).
* 콘텐츠 실험 기능을 사용하는 경우 웹 데이터 세트도 보고 구성에 포함되어야 합니다.
* 현재, 웹 속성에서 웹 채널 캠페인을 작성하고 게재하기 위해 두 가지 유형의 구현이 지원됩니다.
   * 클라이언트측 전용: 웹 사이트를 수정하려면 Adobe Experience Platform Web SDK를 구현해야 합니다.
   * 하이브리드 모드: Platform Personalization Server API를 활용하여 Edge Network 서버측을 요청할 수 있습니다. 그런 다음 API의 응답이 클라이언트측에서 수정 사항을 렌더링하기 위해 Adobe Experience Platform Web SDK에 제공됩니다. 자세한 내용은 Adobe Experience Platform Edge Network 서버 API 설명서를 참조하십시오. 하이브리드 모드에 대한 추가 세부 정보 및 구현 샘플은 이 블로그 게시물에서 찾을 수 있습니다.

  >[!NOTE]
  >
  >서버측 전용 구현은 현재 지원되지 않습니다.




## 용어

먼저 웹 채널 캠페인 내에서 사용되는 용어를 이해해야 합니다.

* **웹 채널**: 웹을 통한 커뮤니케이션 또는 콘텐츠 전달 매체입니다. 이 안내서의 컨텍스트에서 개인화된 콘텐츠가 Adobe Journey Optimizer 내에서 Platform Web SDK를 사용하여 웹 사이트 방문자에게 전달되는 메커니즘을 나타냅니다.
* **웹 표면**: 콘텐츠가 전달되는 URL로 식별되는 웹 속성을 나타냅니다. 단일 또는 여러 웹 페이지를 포함할 수 있습니다.
* **Journey Optimizer 웹 디자이너**: 사용자가 웹 채널 경험을 디자인할 수 있는 Journey Optimizer 내의 특정 도구 또는 인터페이스입니다.
* **Adobe Experience Cloud Visual Edit Helper**: 웹 채널 경험을 시각적으로 편집하고 디자인하는 데 도움이 되는 브라우저 확장 기능입니다.
* **데이터스트림**: 웹 채널 경험을 제공할 수 있는 Adobe Experience Platform 서비스 내의 구성입니다.
* **병합 정책**: 인바운드 캠페인의 정확한 활성화 및 게시를 보장하는 구성
* **대상자**: 특정 기준을 충족하는 사용자 또는 사이트 방문자의 특정 세그먼트.
* **웹 디자이너**: 코드를 깊이 삽입하지 않고 웹 경험을 시각적으로 편집하고 디자인하는 데 도움이 되는 인터페이스 또는 도구입니다.
* **표현식 편집기**: 사용자가 데이터 속성이나 기타 기준을 기반으로 웹 콘텐츠에 개인화를 추가할 수 있도록 해주는 웹 디자이너 내의 도구입니다.
* **오퍼 결정 구성 요소**: 의사 결정 관리에 따라 특정 방문자에게 표시하기에 가장 적합한 오퍼를 결정하는 데 도움이 되는 웹 디자이너의 구성 요소입니다.
* **콘텐츠 실험**: 다양한 콘텐츠 변형을 테스트하여 인바운드 클릭수와 같은 원하는 지표 측면에서 가장 뛰어난 성과를 보이는 변형을 찾는 방법입니다.
* **처리**: 콘텐츠 실험의 맥락에서 처리란 다른 콘텐츠에 대해 테스트되는 특정 콘텐츠 변형을 의미합니다.
* **시뮬레이션**: 라이브 대상에 대해 웹 채널 경험을 활성화하기 전에 시각화하기 위한 미리보기 메커니즘입니다.

## 데이터 스트림 구성

이미 데이터 스트림에 Adobe Experience Platform 서비스를 추가했습니다. 이제 웹 채널 경험을 제공할 수 있도록 Adobe Journey Optimizer 옵션을 활성화해야 합니다.

데이터 스트림에서 Adobe Journey Optimizer을 구성하려면 다음 작업을 수행하십시오.

1. 로 이동 [데이터 수집](https://experience.adobe.com/#/data-collection){target="blank"} 인터페이스.
1. 왼쪽 탐색에서 을 선택합니다. **[!UICONTROL 데이터스트림]**.
1. 이전에 만든 Luma 웹 SDK 데이터스트림을 선택합니다.

   ![데이터 스트림 선택](assets/web-channel-select-datastream.png)

1. 선택 **[!UICONTROL 편집]** Adobe Experience Platform 서비스 내에서 사용할 수 있습니다.

   ![데이터 스트림 편집](assets/web-channel-edit-datastream.png)

1. 다음 확인: **[!UICONTROL Adobe Journey Optimizer]** 상자.

   ![AJO 확인란 선택](assets/web-channel-check-ajo-box.png)

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

이렇게 하면 Journey Optimizer에 대한 인바운드 이벤트가 Adobe Experience Platform Edge Network에서 올바르게 처리됩니다.

## 병합 정책 구성

병합 정책이 다음을 사용하여 정의되었는지 확인합니다. **[!UICONTROL Active-On-Edge 병합 정책]** 옵션이 활성화되었습니다. 이 병합 정책 옵션은 에지에서 인바운드 캠페인의 정확한 활성화 및 게시를 보장하기 위해 Journey Optimizer 인바운드 채널에 사용됩니다.

병합 정책에서 옵션을 구성하려면 다음을 수행합니다.

1. 로 이동 **[!UICONTROL 고객]** > **[!UICONTROL 프로필]** Experience Platform 또는 Journey Optimizer 인터페이스의 페이지
1. 다음 항목 선택 **[!UICONTROL 병합 정책]** 탭.
1. 정책을 선택합니다(일반적으로 를 사용하는 것이 가장 좋음). [!UICONTROL 기본 시간 기반] policy)를 누르고 **[!UICONTROL Active-On-Edge 병합 정책]** 내의 옵션 **[!UICONTROL 구성]** 단계.

   ![병합 정책 전환](assets/web-channel-active-on-edge-merge-policy.png)

## 콘텐츠 실험을 위한 웹 데이터 세트 구성

웹 채널 캠페인 내에서 콘텐츠 실험을 사용하려면 사용된 웹 데이터 세트도 보고 구성에 포함되어야 합니다. Journey Optimizer 보고 시스템은 읽기 전용 방식으로 데이터 세트를 사용하여 기본 제공 콘텐츠 실험 보고서를 채웁니다.

[콘텐츠 실험 보고를 위한 데이터 세트 추가는 이 섹션에 자세히 설명되어 있습니다](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/content-experiment/reporting-configuration#add-datasets).

## 사용 사례 개요 - 충성도 보상

이 단원에서는 샘플 충성도 보상 사용 사례를 사용하여 Web SDK를 사용한 웹 채널 경험의 구현을 자세히 설명합니다.

이 사용 사례를 통해 Journey Optimizer 캠페인 및 웹 디자이너를 활용하여 Journey Optimizer이 고객에게 최상의 인바운드 경험을 제공하는 데 어떻게 도움이 되는지 더 잘 이해할 수 있습니다.

이 자습서는 구현자를 대상으로 하므로 이 단원에는 Journey Optimizer의 실질적인 인터페이스 작업이 포함되어 있습니다. 이러한 인터페이스 작업은 일반적으로 마케터가 처리하지만, 구현자가 일반적으로 웹 채널 캠페인 생성을 담당하지 않더라도 프로세스에 대한 통찰력을 얻는 것이 유용할 수 있습니다.

### 충성도 스키마 만들기 및 샘플 데이터 수집

Web SDK 데이터를 Adobe Experience Platform에 수집하면 Platform에 수집한 다른 데이터 소스에서 보강할 수 있습니다. 예를 들어 사용자가 Luma 사이트에 로그인하면 ID 그래프가 Experience Platform에서 생성되고 다른 모든 프로필 활성화 데이터 세트는 잠재적으로 함께 결합되어 실시간 고객 프로필을 구축할 수 있습니다. 이를 실제로 보려면 Journey Optimizer 웹 캠페인에서 실시간 고객 프로필을 사용할 수 있도록 몇 가지 샘플 충성도 데이터를 사용하여 Adobe Experience Platform에서 다른 데이터 세트를 신속하게 만듭니다. 이미 유사한 연습을 했기 때문에 지침은 간단합니다.

충성도 스키마를 만듭니다.

1. 새 스키마 만들기
1. 선택 **[!UICONTROL 개인 프로필]** (으)로 [!UICONTROL 기본 클래스]
1. 스키마 이름 지정 `Luma Loyalty Schema`
1. 추가 [!UICONTROL 고객 충성도 세부 정보] 필드 그룹
1. 추가 [!UICONTROL 인구 통계 세부 정보] 필드 그룹
1. 다음 항목 선택 `Person ID` 필드 및 다음으로 표시 [!UICONTROL 신원] 및 [!UICONTROL 기본 ID] 사용 `Luma CRM Id` [!UICONTROL ID 네임스페이스].
1. 에 대한 스키마 활성화 [!UICONTROL 프로필]

   ![충성도 스키마](assets/web-channel-loyalty-schema.png)

데이터 세트를 만들고 샘플 데이터를 수집하려면 다음을 수행하십시오.

1. 에서 새 데이터 세트 만들기 `Luma Loyalty Schema`
1. 데이터 세트 이름 지정 `Luma Loyalty Dataset`
1. 다음에 대한 데이터 세트 활성화 [!UICONTROL 프로필]
1. 샘플 파일 다운로드 [luma-loyalty-forWeb.json](assets/luma-loyalty-forWeb.json)
1. 파일을 데이터 세트로 드래그 앤 드롭
1. 데이터가 성공적으로 수집되었는지 확인

   ![충성도 스키마](assets/web-channel-loyalty-dataset.png)

### 대상자 만들기

대상자는 공통 트레이트를 중심으로 프로필을 함께 그룹화합니다. 웹 캠페인에서 사용할 수 있는 빠른 대상을 만듭니다.

1. Experience Platform 인터페이스에서 **[!UICONTROL 대상]** 왼쪽 탐색
1. 선택 **[!UICONTROL 대상자 만들기]**
1. 선택 **[!UICONTROL 규칙 작성]**
1. 선택 **[!UICONTROL 만들기]**

   ![대상자 만들기](assets/web-campaign-create-audience.png)

1. 선택 **[!UICONTROL 속성]**
1. 다음 찾기 **[!UICONTROL 충성도]** > **[!UICONTROL 계층]** 필드를 지정하고 로 끌어서 놓습니다. **[!UICONTROL 속성]** 섹션
1. 대상을 사용자로 정의 `tier` 은(는) `gold`
1. 대상자의 이름을 지정합니다. `Luma Loyalty Rewards – Gold Status`
1. 선택 **[!UICONTROL Edge]** (으)로 **[!UICONTROL 평가 방법]**
1. 선택 **[!UICONTROL 저장]**

   ![대상자 정의](assets/web-campaign-define-audience.png)

이는 매우 간단한 대상자이므로 Edge 평가 방법을 사용할 수 있습니다. Edge 대상은 Edge에서 평가되므로, Web SDK에서 Platform Edge Network에 대해 수행한 동일한 요청에서 대상 정의를 평가하고 사용자가 자격이 있는지 즉시 확인할 수 있습니다.

### 충성도 보상 캠페인 만들기

샘플 충성도 데이터를 수집하고 세그먼트를 만들었으므로 이제 Adobe Journey Optimizer에서 충성도 보상 웹 채널 캠페인을 만드십시오.

샘플 캠페인을 만들려면:

1. 를 엽니다. [Journey Optimizer](https://experience.adobe.com/journey-optimizer/home){target="_blank"} 인터페이스

   >[!NOTE]
   >
   > 스키마, 데이터 세트 및 대상은 모두 일반적인 Experience Platform 구성이므로 Journey Optimizer 인터페이스에서도 빌드할 수 있습니다.

1. 다음으로 이동 **[!UICONTROL 여정 관리]** > **[!UICONTROL 캠페인]** 왼쪽 탐색
1. 클릭 **[!UICONTROL 캠페인 만들기]** 오른쪽 상단에 있습니다.
1. 다음에서 **[!UICONTROL 속성]** 섹션에서 캠페인을 실행할 방법을 지정합니다. 충성도 보상 사용 사례의 경우 **예약됨**.

   ![예약된 캠페인](assets/web-channel-campaign-properties-scheduled.png)

1. 다음에서 **[!UICONTROL 작업]** 섹션에서 다음을 선택합니다. **[!UICONTROL 웹 채널]**. 다음으로:  **[!UICONTROL 웹 표면]**, 선택 **[!UICONTROL 페이지 URL]**.

   >[!NOTE]
   >
   >웹 표면은 콘텐츠가 전달되는 URL로 식별되는 웹 속성을 나타냅니다. 단일 페이지 URL에 해당하거나 여러 페이지를 포함할 수 있으므로 하나 또는 여러 웹 페이지에 수정 사항을 적용할 수 있습니다.

1. 다음을 선택합니다. **[!UICONTROL 페이지 URL]** 이 캠페인의 한 페이지에 경험을 배포하기 위한 웹 표면 옵션 Luma 페이지의 URL을 입력합니다. `https://luma.enablementadobe.com/content/luma/us/en.html`

1. 웹 표면이 정의되면 다음을 선택합니다 **[!UICONTROL 만들기]**.

   ![웹 표면 선택](assets/web-channel-web-surface.png)

1. 이제 새 웹 채널 캠페인에 몇 가지 추가 세부 정보를 추가합니다. 먼저 캠페인 이름을 지정합니다. 호출 `Luma Loyalty Rewards – Gold Status`. 원할 경우 캠페인에 설명을 추가할 수 있습니다. 추가 **[!UICONTROL 태그]** 전체 캠페인 분류를 개선합니다.

   ![캠페인 이름 지정](assets/web-channel-campaign-name.png)

1. 기본적으로 캠페인은 모든 사이트 방문자에 대해 활성화됩니다. 이 사용 사례에서는 gold status 보상 멤버만 경험을 볼 수 있습니다. 활성화하려면 **[!UICONTROL 대상자 선택]** 및 선택 `Luma Loyalty Rewards – Gold Status` 대상입니다.

1. 다음에서 **[!UICONTROL ID 네임스페이스]** 필드에서 선택한 세그먼트 내의 개인을 식별하기 위한 네임스페이스를 선택합니다. Luma 사이트에 캠페인을 배포하므로 ECID 네임스페이스를 선택할 수 있습니다. 내 프로필 `Luma Loyalty Rewards – Gold Status` 다양한 ID 중 ECID 네임스페이스가 없는 대상자는 웹 채널 캠페인에서 타깃팅되지 않습니다.

   ![ID 유형 선택](assets/web-channel-indentity-type.png)

1. 다음을 사용하여 캠페인을 오늘 일자로 시작하도록 예약합니다. **[!UICONTROL 캠페인 시작]** 옵션을 사용하고 1주일 후에 끝남 **[!UICONTROL 캠페인 종료]** 옵션을 선택합니다.

   ![캠페인 일정](assets/web-channel-campaign-schedule.png)

>[!NOTE]
>
>웹 채널 캠페인의 경우 방문자가 페이지를 열면 웹 경험이 표시됩니다. 따라서 Adobe Journey Optimizer의 다른 유형의 캠페인과 달리 **[!UICONTROL 작업 트리거]** 섹션을 구성할 수 없습니다.

### 충성도 보상 콘텐츠 실험

위로 스크롤하는 경우 **[!UICONTROL 작업]** 섹션에서 선택적으로 실험을 만들어 에 대해 더 잘 작동하는 콘텐츠를 테스트할 수 있습니다. `Luma Loyalty Rewards – Gold Status` 대상입니다. 캠페인 구성의 구성 요소로 두 가지 처리를 만들고 테스트해 보겠습니다.

콘텐츠 실험을 만들려면 다음 작업을 수행하십시오.

1. 클릭 **[!UICONTROL 실험 만들기]**.

   ![실험 만들기](assets/web-channel-create-content-experiment.png)

1. 먼저 선택 **[!UICONTROL 성공 지표]**. 콘텐츠 효과를 결정하는 지표입니다. 선택 **[!UICONTROL 고유 인바운드 클릭수]**&#x200B;를 클릭하여 웹 경험 CTA에서 더 많은 클릭 수를 생성하는 컨텐츠 처리를 확인합니다.

   ![성공 지표 선택](assets/web-channel-content-experiment-metric.png)

1. 웹 채널을 사용하여 실험을 설정하고 **[!UICONTROL 인바운드 클릭수]**, **[!UICONTROL 고유 인바운드 클릭수]**, **[!UICONTROL 페이지 보기 수]**, 또는 **[!UICONTROL 고유 페이지 조회수]** 지표, **[!UICONTROL 클릭 동작]** 드롭다운을 사용하면 특정 페이지의 클릭 수 및 보기를 정확하게 추적하고 모니터링할 수 있습니다.

1. 필요한 경우 **[!UICONTROL 유지]** 그것은 두 가지 치료 중 어느 것도 받지 않습니다. 지금은 선택하지 않은 상태로 둡니다.

1. 또한 다음을 선택할 수 있습니다. **[!UICONTROL 균등 분배]**. 처리 분할이 항상 균일하게 분할되도록 하려면 이 옵션을 선택합니다.

[Adobe Journey Optimizer 웹 채널의 콘텐츠 실험에 대해 자세히 알아보기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/content-experiment/get-started-experiment).

### Visual Helper를 사용하여 콘텐츠 편집

이제 웹 채널 경험을 작성해 보겠습니다. 이렇게 하려면 Adobe Experience Cloud을 사용합니다 **[!UICONTROL Visual Helper]**. 이 도구는 Google Chrome 및 Microsoft® Edge와 호환되는 브라우저 확장 기능입니다. 경험을 빌드하기 전에 확장을 다운로드했는지 확인하십시오. 또한 웹 페이지에 웹 SDK가 포함되어 있는지 확인합니다.

1. 다음 범위 내 **[!UICONTROL 작업]** 캠페인의 탭에서 **[!UICONTROL 콘텐츠 편집]**. 단일 페이지 URL을 표면으로 입력했으므로 작성기에서 작업을 시작할 준비가 되어 있어야 합니다.

   ![콘텐츠 편집](assets/web-channel-edit-content.png)

1. 지금 클릭 **[!UICONTROL 웹 페이지 편집]** 작성을 시작합니다.

   ![웹 페이지 편집](assets/web-channel-edit-web-page.png)

1. 웹 작성기를 사용하여 일부 요소를 편집하여 시작하십시오. 상황별 메뉴를 사용하여 Luma 영웅 이미지 헤더를 편집합니다. 오른쪽에 있는 상황별 창의 스타일을 조정합니다.

   ![상황별 편집 추가](assets/web-channel-some-contextual-edit.png)

1. 또한 을 사용하여 컨테이너에 개인화를 추가합니다. **[!UICONTROL 표현식 편집기]**.

   ![개인화 추가](assets/web-channel-add-basic-personalization.png)

1. 클릭 수에 대해 경험이 제대로 추적되는지 확인합니다. 선택 **[!UICONTROL 클릭 추적 요소]** 상황별 메뉴에서 사용할 수 있습니다.

   ![클릭 추적](assets/web-channel-click-tracking.png)

1. 사용 **[!UICONTROL 오퍼 결정 구성 요소]** 을 클릭하여 웹 페이지에 오퍼를 삽입합니다. 이 구성 요소는 **[!UICONTROL 의사 결정 관리]** Luma 방문자에게 제공할 최상의 오퍼를 선택합니다.


### HTML 디자인 변경 사항

충성도 보상 캠페인의 구성 요소로서 사이트를 보다 발전시키거나 사용자 지정 변경하려는 경우 사용할 수 있는 몇 가지 방법이 있습니다.

사용 **[!UICONTROL 구성 요소]** HTML 또는 다른 컨텐츠를 Luma 사이트에 직접 추가하는 창입니다.

![구성 요소 창 탐색](assets/web-channel-components-pane.png)

페이지 상단에 새 HTML 구성 요소를 추가합니다. HTML 디자인 인터페이스 또는 **[!UICONTROL 상황별]** 창.

![사용자 정의 HTML 추가](assets/web-channel-add-html-component.png)

HTML 또는 **[!UICONTROL 수정 사항]** 창. 이 창에서는 페이지에서 구성 요소를 선택하고 디자이너 인터페이스에서 편집할 수 있습니다.

편집기 내에서 HTML을 `Luma Loyalty Rewards – Gold Status` 대상입니다. 선택 **[!UICONTROL 유효성 검사]**.

![HTML 확인](assets/web-channel-add-custom-html-validate.png)

이제 새로운 맞춤형 HTML 구성 요소를 검토하여 맞춤화 및 촉감을 확인하십시오.

![사용자 정의 HTML 검토](assets/web-channel-review-custom-html.png)

다음을 사용하여 특정 구성 요소 편집 **[!UICONTROL CSS 선택기 유형]** 수정했습니다.

![CSS 수정](assets/web-channel-css-selector.png)

를 사용하여 사용자 지정 코드 추가 **페이지 `<head>` 유형** 수정했습니다.

![헤드 수정](assets/web-channel-page-head-modification.png)

가능성은 다음을 사용하여 무한합니다. **[!UICONTROL Visual Helper]**.

### 충성도 보상 콘텐츠 시뮬레이션

캠페인을 활성화하기 전에 수정된 웹 페이지의 미리보기를 확인하십시오. 웹 채널 경험을 시뮬레이션하도록 테스트 프로필을 구성해야 합니다.

경험을 시뮬레이션하려면 다음 작업을 수행하십시오.

1. 선택 **[!UICONTROL 콘텐츠 시뮬레이션]** 캠페인 내.

   ![콘텐츠 시뮬레이션](assets/web-channel-simulate-content.png)

1. 시뮬레이션을 수신할 테스트 프로필을 선택하십시오. 테스트 프로필은 `Luma Loyalty Rewards – Gold Status` 적절한 치료를 받을 대상자.

1. 테스트 프로필에 대한 미리보기가 표시됩니다.

### 충성도 보상 캠페인 활성화

마지막으로 웹 채널 캠페인을 활성화합니다.

1. 선택 **활성화하려면 검토**.

1. 마지막으로 캠페인 세부 정보를 확인하라는 메시지가 표시됩니다. 선택 **[!UICONTROL 활성화]**. 캠페인이 사이트에서 라이브 상태가 되는 데 최대 15분 정도 소요될 수 있습니다.

### 충성도 보상 QA

다음과 같은 몇 가지 로그인을 사용하여 &quot;gold status&quot; 사용자를 시뮬레이션하고 캠페인을 사용할 수 있습니다.

1. `cleavlandeuler@emailsim.io`/`test`
1. `leftybeagen@emailsim.io`/`test`
1. `jenimartinho@emailsim.io`/`test`

모범 사례로서 다음을 모니터링합니다. **[!UICONTROL 웹]** 캠페인 특정 KPI에 대한 캠페인 라이브 및 글로벌 보고서의 탭입니다. 이 캠페인의 경우 경험 노출 횟수를 모니터링하고 클릭 비율을 표시합니다.

![웹 보고서 보기](assets/web-channel-web-report.png)

### Adobe Experience Platform Debugger을 사용한 웹 채널 유효성 검사

Chrome과 Firefox 모두에서 사용할 수 있는 Adobe Experience Platform Debugger 확장 기능은 웹 페이지를 분석하여 Adobe Experience Cloud 솔루션 구현에서 문제를 식별합니다.

Luma 사이트에서 디버거를 사용하여 프로덕션의 웹 채널 경험을 확인할 수 있습니다. 이는 충성도 보상 사용 사례가 작동하고 실행 중인 경우 모든 것이 올바르게 구성되도록 하는 모범 사례입니다.

[여기 안내서를 사용하여 브라우저에서 디버거를 구성하는 방법을 알아봅니다](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/debugger/overview).

디버거를 사용하여 유효성 검사를 시작하려면 다음을 수행하십시오.

1. 웹 채널 경험이 있는 Luma 웹 페이지로 이동합니다.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. 웹 페이지에서 를 엽니다. **[!UICONTROL Adobe Experience Platform Debugger]**.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. 다음으로 이동 **요약**. 다음을 확인합니다 **[!UICONTROL 데이터 스트림 ID]** 와 일치 **[!UICONTROL 데이터스트림]** 위치: **[!UICONTROL Adobe 데이터 수집]** Adobe Journey Optimizer을 활성화한 경우.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. 그런 다음 다양한 Luma 충성도 계정으로 사이트에 로그인하고 디버거를 사용하여 Adobe Experience Platform Edge Network에 전송된 요청의 유효성을 검사할 수 있습니다.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. 아래 **[!UICONTROL 솔루션]** 다음으로 이동 **[!UICONTROL Experience Platform Web SDK]**.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. 다음 범위 내 **구성** 탭, 켜기/끄기 **[!UICONTROL 디버깅 활성화]**. 이렇게 하면 내의 세션에 대한 로깅을 사용할 수 있습니다. **[!UICONTROL Adobe Experience Platform 보증]** 세션.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. 다양한 Luma 충성도 계정으로 사이트에 로그인하고 디버거를 사용하여 로 전송된 요청의 유효성을 검사합니다. **[!UICONTROL Adobe Experience Platform Edge 네트워크]**. 이러한 모든 요청은에서 캡처해야 합니다. **[!UICONTROL 보증]** 로그 추적용.
<!--
   ![ADD SCREENSHOT](#)
-->

[다음: ](setup-decision-management.md)

>[!NOTE]
>
>Adobe Experience Platform Web SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나, 일반적인 피드백을 공유하거나, 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오. [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
