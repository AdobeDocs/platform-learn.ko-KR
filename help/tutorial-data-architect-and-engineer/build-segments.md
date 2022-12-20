---
title: 세그먼트 작성
seo-title: Build segments | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 세그먼트 작성
description: 이 단원에서는 이전 단원에서 수집한 프로필 데이터를 기반으로 일부 세그먼트를 만듭니다.
role: Data Architect
feature: Data Governance
kt: 4348
thumbnail: 4348-build-segments.jpg
exl-id: cd05e814-1ea7-48ba-adf6-1a71504c623e
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 2%

---

# 세그먼트 작성

<!-- 30 min-->
이 단원에서는 이전 단원에서 수집한 프로필 데이터를 기반으로 일부 세그먼트를 만듭니다.

실시간 고객 프로필이 있으면 유사한 트레이트를 공유하고 마케팅 전략과 유사하게 응답할 수 있는 개인 세그먼트를 만들 수 있습니다. 이러한 세그먼트의 기본 구성요소는 이전에 만든 XDM 필드입니다.

**데이터 설계자** 은 이 자습서를 벗어나는 세그먼트를 만들고 이 작업을 사용하여 동료를 지원해야 합니다.

연습을 시작하기 전에 이 짧은 비디오에서 세그먼트 만들기에 대한 자세한 내용을 살펴보십시오.
>[!VIDEO](https://video.tv.adobe.com/v/27254?quality=12&learn=on)


## 필요한 권한

에서 [권한 구성](configure-permissions.md) 단원에서 이 단원을 완료하는 데 필요한 모든 액세스 컨트롤을 설정합니다. 특히

* 권한 항목 **[!UICONTROL 프로필 관리]** > **[!UICONTROL 세그먼트 관리]**, **[!UICONTROL 세그먼트 보기]**, 및 **[!UICONTROL 대상 세그먼트 내보내기]**
* 권한 항목 **[!UICONTROL 프로필 관리]** > **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 프로필 관리]**
* 권한 항목 **[!UICONTROL 샌드박스]** > `Luma Tutorial`
* 에 대한 사용자 역할 액세스 `Luma Tutorial Platform` 제품 프로필
* 에 대한 개발자 역할 액세스 `Luma Tutorial Platform` 제품 프로필(API용)

## 기본 세그먼트 작성

골드 또는 플래티넘 상태를 사용하는 충성도 프로그램 고객을 위한 간단한 세그먼트를 만들어 보겠습니다

1. Platform 사용자 인터페이스에서 로 이동합니다. **[!UICONTROL 세그먼트]** 왼쪽 탐색
1. 을(를) 선택합니다 **[!UICONTROL 세그먼트 만들기]** 버튼
1. 스키마 빌더 왼쪽에 속성(레코드 데이터), 이벤트(시계열 데이터) 및 대상에 대한 세 개의 탭이 있습니다
1. 톱니바퀴 아이콘을 선택하여 세그먼트 빌더의 기본값이 데이터가 있는 필드만 표시하도록 하면서도 병합 정책을 변경할 수 있도록 하는 방법을 확인합니다
1. 속성 탭에서 **XDM 개별 프로필 > 충성도** 폴더(&quot;충성도&quot;를 검색할 수도 있음)
1. 끌어서 놓기, `Tier` 속성 필드 메뉴에서 세그먼트 빌더 캔버스까지
1. 선택 `Tier` 다음과 같음 `Gold` 또는 `Platinum`
1. 선택 **[!UICONTROL 예상 새로 고침]** 세그먼트에 적합한 프로필 수 확인
1. 로서의 **[!UICONTROL 이름]**, 입력 `Luma customers with level Gold or Above`
1. **[!UICONTROL 저장]**을 선택합니다
   ![세그먼트](assets/segment-goldOrAbove.png)

<!--## Build a sequential segment-->

## 동적 세그먼트 작성

이 연습에서는 30일 이내에 동일한 제품을 두 번 구매한 고객을 위한 세그먼트를 만듭니다. 동적 세그먼트를 사용하면 필드를 변수로 사용하여 세그멘테이션의 크기를 조정할 수 있습니다.

1. 이동 **[!UICONTROL 세그먼트]** 왼쪽 탐색
1. 을(를) 선택합니다 **[!UICONTROL 세그먼트 만들기]** 버튼
1. 을(를) 선택합니다 **[!UICONTROL 이벤트]** 탭
1. 목록을 다음으로 필터링 `purchases`
1. 을(를) 드래그합니다. **[!UICONTROL 구매]** 캔버스에 이벤트 유형 _두 번 씩_
1. 두 시간 사이에 있는 시계 아이콘을 선택합니다 **[!UICONTROL 구매]** 이벤트를 선택하고 &quot;30일 이내&quot;를 선택합니다.
1. 이 시점에서 세그먼트 정의가 표시되는지 확인합니다. **&quot;구매 이벤트가 1개 이상 있고 30일 이내에 구매 이벤트가 1개 이상 있는 대상 포함&quot;**

   ![30일 이내에 2회 구매](assets/segment-twoPurchases.png)
1. 이제 이벤트 필터를 로 변경합니다. `sku`
1. SKU 필드를 두 번째 구매 이벤트로 드래그합니다
   ![SKU를 통해 30일 이내에 2회 구입](assets/segment-twoPurchases-addSku.png)
1. 이제 이벤트 필터 지우기
1. 에 가 표시되어야 합니다. **[!UICONTROL 변수 찾아보기]** 섹션에 두 개의 구매 이벤트를 위한 폴더가 있습니다. 탐색하려면 클릭 **[!UICONTROL 구매 1]**\
   ![SKU를 사용하여 30일 이내에 두 개의 구매를 수행하면 첫 번째 구매를 찾아봅니다](assets/segment-twoPurchases-browsePurchaseOne.png)
1. 드릴 다운하여 **[!UICONTROL 제품 목록 항목]** 폴더에서 을 선택합니다. **[!UICONTROL SKU]** 필드를 만든 후 오른쪽의 **[!UICONTROL 다음과 같음]** 피연산자 영역을 마우스로 가리키면 &quot;피연산자를 비교할 추가&quot; 섹션에 해당 영역을 놓습니다
1. 세그먼트 이름을 지정합니다 `Bought same product within 30 days`
1. 대상 정의가 **&quot;최소 1개 이상의 구매 이벤트가 있는 30일 이내에 1개 이상의 구매 이벤트가 있는 대상 포함&quot;(SKU가 Purchases1 SKU와 같음)**
1. **[!UICONTROL 저장]** 버튼을 선택합니다

   ![지난 30일 세그먼트에서 동일한 제품 구매](assets/segment-boughtSameProduct.png)

## 다중 엔티티 세그먼트 작성

Adobe에서 `Luma Offline Purchase Events Schema` 그리고 `Luma Product Catalog Schema` 이전 수업에서? 다중 엔티티 세그먼테이션을 사용하여 스키마에서 관계를 사용할 수 있도록 했습니다.

고급 다중 엔티티 세그먼테이션 기능을 사용하면 여러 XDM 클래스를 사용하여 세그먼트를 만들어 스키마를 확장할 수 있습니다. 따라서 세그먼트 빌더는 프로필 데이터 저장소가 기본인 것처럼 추가 필드에 액세스할 수 있습니다

다음 세그먼트를 만들려면 사이에 만든 관계를 적용합니다 `Luma Product Catalog Schema` 그리고 `Luma Offline Purchase Events Schema`.

1. 이동 **[!UICONTROL 세그먼트]** 왼쪽 탐색
1. 을(를) 선택합니다 **[!UICONTROL 세그먼트 만들기]** 버튼
1. 을(를) 선택합니다 **[!UICONTROL 이벤트]** 탭
1. 목록을 다음으로 필터링 `purchases`
1. 을(를) 드래그합니다. **[!UICONTROL 구매]** 캔버스에 이벤트 유형
1. 이벤트 위에 있는 시계 드롭다운을 선택하고 을(를) 선택합니다 **[!UICONTROL 지난 30일]**
1. 필터 **[!UICONTROL 이벤트]** 목록 대상 `category` 그런 다음 **[!UICONTROL 제품 카테고리]** 필드 위치 **[!UICONTROL 구매]**
1. 연산자를 로 변경합니다. **[!UICONTROL 다음으로 시작]** 을 입력합니다. `men` 텍스트 상자에
1. 로서의 **[!UICONTROL 이름]**, 입력 `Purchased a Men's product in the last 30 days`
1. 대상 정의를 확인합니다 `(Include audience who have at least 1 Purchases event where ((Product Category starts with men)) ) and occurs in last 30 day(s)`
1. **[!UICONTROL 저장]** 버튼을 선택합니다

   ![지난 30일 세그먼트에서 동일한 제품 구매](assets/segment-purchasedMens.png)

## 일괄 처리 및 스트리밍 세그멘테이션

클릭 **[!UICONTROL 세그먼트]** 왼쪽 탐색에서 세 가지 세그먼트를 잠시 살펴보겠습니다.

* 두 개의 세그먼트는 일괄 처리 세그먼트이며 하나는 스트리밍 세그먼트입니다.
* 플랫폼은 가능한 한 스트리밍 세그먼테이션으로 기본 설정되며, 기준을 충족하는 즉시 세그먼트에 대해 고객에게 자격을 부여합니다. 세그먼트 정의가 스트리밍에 너무 복잡하면 자동으로 배치로 변환됩니다. 이 경우 구매 이벤트의 전환 확인 기간이 7일 이상인 경우, 두 세그먼트가 기본적으로 배치로 설정됩니다. 스트리밍 제한 사항의 전체 및 현재 목록을 보려면 [설명서](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/streaming-segmentation.html).
* 배치 작업은 일별 일정에 따라 실행되며, 토글할 수 있습니다.

![지난 30일 세그먼트에서 동일한 제품 구매](assets/segment-review.png)

## 추가 리소스

* [Segmentation Service 설명서](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html)
* [세그먼테이션 서비스 API 참조](https://www.adobe.io/experience-platform-apis/references/segmentation/)

특히 세그먼트 활성화와 관련하여 세그멘테이션에 대한 자세한 내용이 있습니다. 이러한 주제들은 다른 자습서에서 다룹니다.

너는 모든 운동을 통해 해냈다! 다음 위치로 이동하십시오. [결론](conclusion.md).
