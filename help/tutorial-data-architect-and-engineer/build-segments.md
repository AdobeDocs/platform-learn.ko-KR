---
title: 세그먼트 작성
seo-title: Build segments | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 세그먼트 작성
description: 이 단원에서는 이전 단원에서 수집한 프로필 데이터를 기반으로 몇 가지 세그먼트를 빌드합니다.
role: Data Architect
feature: Data Governance
jira: KT-4348
thumbnail: 4348-build-segments.jpg
exl-id: cd05e814-1ea7-48ba-adf6-1a71504c623e
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 2%

---

# 세그먼트 작성

<!-- 30 min-->
이 단원에서는 이전 단원에서 수집한 프로필 데이터를 기반으로 몇 가지 세그먼트를 빌드합니다.

실시간 고객 프로필이 있으면 유사한 트레이트를 공유하고 마케팅 전략에 유사하게 응답할 수 있는 개인 사용자의 세그먼트를 만들 수 있습니다. 이러한 세그먼트의 빌딩 블록은 이전에 만든 XDM 필드입니다.

**데이터 설계자** 은(는) 이 자습서 외부에 세그먼트를 만들고 이 작업으로 동료를 지원해야 합니다.

연습을 시작하기 전에 이 짧은 비디오를 시청하여 세그먼트 만들기에 대해 자세히 알아보십시오.
>[!VIDEO](https://video.tv.adobe.com/v/27254?quality=12&learn=on)


## 권한 필요

다음에서 [권한 구성](configure-permissions.md) 단원, 특히 이 단원을 완료하는 데 필요한 모든 액세스 제어를 설정합니다.

* 권한 항목 **[!UICONTROL 프로필 관리]** > **[!UICONTROL 세그먼트 관리]**, **[!UICONTROL 세그먼트 보기]**, 및 **[!UICONTROL 대상 세그먼트 내보내기]**
* 권한 항목 **[!UICONTROL 프로필 관리]** > **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 프로필 관리]**
* 권한 항목 **[!UICONTROL 샌드박스]** > `Luma Tutorial`
* 에 대한 사용자 역할 액세스 권한 `Luma Tutorial Platform` 제품 프로필
* 에 대한 개발자 역할 액세스 `Luma Tutorial Platform` 제품 프로필(API용)

## 기본 세그먼트 작성

골드 또는 플래티넘 상태의 충성도 프로그램 고객을 위한 간단한 세그먼트를 만들어 보겠습니다

1. Platform 사용자 인터페이스에서 **[!UICONTROL 세그먼트]** 왼쪽 탐색
1. 다음 항목 선택 **[!UICONTROL 세그먼트 만들기]** 단추
1. 스키마 빌더 왼쪽에는 속성(레코드 데이터), 이벤트(시계열 데이터) 및 대상에 대한 세 개의 탭이 있습니다
1. 톱니바퀴 아이콘을 선택하면 세그먼트 빌더에 데이터가 있는 필드만 기본적으로 표시되고 병합 정책을 변경할 수 있습니다
1. 속성 탭에서 **XDM 개인 프로필 > 충성도** 폴더(&quot;충성도&quot;를 검색할 수도 있음)
1. 드래그 앤 드롭, `Tier` 속성 필드 메뉴에서 세그먼트 빌더 캔버스로
1. 선택 `Tier` 다음과 같음 `Gold` 또는 `Platinum`
1. 선택 **[!UICONTROL 예상 새로 고침]** 세그먼트에 적합한 프로필 수를 확인하려면
1. 다음으로: **[!UICONTROL 이름]**, 입력 `Luma customers with level Gold or Above`
1. **[!UICONTROL 저장]**을 선택합니다
   ![세그먼트](assets/segment-goldOrAbove.png)

<!--## Build a sequential segment-->

## 동적 세그먼트 작성

이 연습에서는 30일 이내에 동일한 제품을 두 번 구매한 고객을 위한 세그먼트를 만듭니다. 동적 세그먼트를 사용하면 필드를 변수로 사용하여 세그먼테이션의 크기를 조정할 수 있습니다.

1. 다음으로 이동 **[!UICONTROL 세그먼트]** 왼쪽 탐색
1. 다음 항목 선택 **[!UICONTROL 세그먼트 만들기]** 단추
1. 다음 항목 선택 **[!UICONTROL 이벤트]** 탭
1. 목록 필터링 대상 `purchases`
1. 드래그 **[!UICONTROL 구매]** 캔버스에 대한 이벤트 유형 _두 번_
1. 둘 사이에 있는 시계 아이콘을 선택합니다 **[!UICONTROL 구매]** 이벤트 및 선택 &quot;30일 이내&quot;
1. 이때 세그먼트 정의가 다음을 읽는지 확인합니다. **&quot;최소 1개의 구매 이벤트가 있는 대상자를 포함시킨 후 30일 이내에 최소 1개의 구매 이벤트가 있는 대상자 포함&quot;**
   ![30일 이내에 2회 구입](assets/segment-twoPurchases.png)
1. 이제 이벤트 필터를 다음으로 변경 `sku`
1. SKU 필드를 두 번째 구매 이벤트로 드래그합니다.
   ![SKU로 30일 이내 2회 구매](assets/segment-twoPurchases-addSku.png)
1. 이제 이벤트 필터 지우기
1. 다음에서 볼 수 있습니다. **[!UICONTROL 변수 찾아보기]** 섹션에는 두 개의 구매 이벤트에 대한 폴더가 있습니다. 탐색하려면 클릭 **[!UICONTROL 구매 1]**\
   ![SKU를 사용하여 30일 이내에 두 번 구매한 경우 첫 번째 구매를 검색하십시오.](assets/segment-twoPurchases-browsePurchaseOne.png)
1. 드릴다운하여 **[!UICONTROL 제품 목록 항목]** 폴더에서 **[!UICONTROL SKU]** 필드를 만든 후 오른쪽의 **[!UICONTROL 다음과 같음]** 피연산자. 해당 영역을 마우스로 가리키면 &quot;피연산자 비교를 위해 추가&quot; 섹션에 놓습니다
1. 세그먼트 이름 지정 `Bought same product within 30 days`
1. 대상 정의가 **&quot;(SKU가 Purchases1 SKU와 같음) 구매 이벤트가 1개 이상인 대상자를 포함시킨 후 30일 이내에 구매 이벤트가 1개 이상인 경우&quot;**
1. **[!UICONTROL 저장]** 버튼을 선택합니다

   ![지난 30일 세그먼트에서 동일한 제품 구매](assets/segment-boughtSameProduct.png)

## 다중 엔티티 세그먼트 작성

다음 사이에 관계를 만든 방법을 기억하십시오. `Luma Offline Purchase Events Schema` 및 `Luma Product Catalog Schema` 이전 수업에서? 다중 엔티티 세그먼테이션을 사용하여 스키마의 관계를 사용할 수 있도록 그렇게 했습니다.

고급 다중 엔티티 세그멘테이션 기능을 사용하면 여러 XDM 클래스를 사용하여 세그먼트를 만들어 스키마를 확장할 수 있습니다. 따라서 세그먼트 빌더는 프로필 데이터 저장소의 기본인 것처럼 추가 필드에 액세스할 수 있습니다

다음 세그먼트는 사이에 빌드한 관계를 적용하여 만듭니다. `Luma Product Catalog Schema` 및 내 `Luma Offline Purchase Events Schema`.

1. 다음으로 이동 **[!UICONTROL 세그먼트]** 왼쪽 탐색
1. 다음 항목 선택 **[!UICONTROL 세그먼트 만들기]** 단추
1. 다음 항목 선택 **[!UICONTROL 이벤트]** 탭
1. 목록 필터링 대상 `purchases`
1. 드래그 **[!UICONTROL 구매]** 캔버스에 대한 이벤트 유형
1. 이벤트 위에 있는 시계 드롭다운을 선택하고 **[!UICONTROL 지난 30일]**
1. 필터 **[!UICONTROL 이벤트]** 나열 대상 `category` 을(를) 드래그하십시오. **[!UICONTROL 제품 범주]** 필드 대상 **[!UICONTROL 구매]**
1. 연산자를 다음으로 변경 **[!UICONTROL 다음으로 시작]** 및 입력 `men` 텍스트 상자에
1. 다음으로: **[!UICONTROL 이름]**, 입력 `Purchased a Men's product in the last 30 days`
1. 대상 정의 확인 `(Include audience who have at least 1 Purchases event where ((Product Category starts with men)) ) and occurs in last 30 day(s)`
1. **[!UICONTROL 저장]** 버튼을 선택합니다

   ![지난 30일 세그먼트에서 동일한 제품 구매](assets/segment-purchasedMens.png)

## 일괄 처리 및 스트리밍 세분화

클릭 **[!UICONTROL 세그먼트]** 왼쪽 탐색에서 잠시 다음 세 가지 세그먼트를 검토해 보겠습니다.

* 세그먼트 중 두 개는 일괄 처리 세그먼트이고 한 개는 스트리밍 세그먼트입니다.
* Platform은 가능하면 기본적으로 스트리밍 세그먼테이션으로 설정하므로 기준을 충족하는 즉시 세그먼트를 얻을 수 있습니다. 세그먼트 정의가 스트리밍하기에 너무 복잡한 경우 자동으로 배치로 변환됩니다. 이 경우, 구매 이벤트의 전환 확인 기간이 7일 이상이었으므로 두 세그먼트는 뱃치로 기본 설정되었습니다. 스트리밍 제한에 대한 전체 및 최신 목록은 을 참조하십시오. [설명서](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/streaming-segmentation.html).
* 배치 작업은 매일 일정으로 실행되며 전환할 수 있습니다.

![지난 30일 세그먼트에서 동일한 제품 구매](assets/segment-review.png)

## 추가 리소스

* [세그먼테이션 서비스 설명서](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html)
* [세그먼테이션 서비스 API 참조](https://www.adobe.io/experience-platform-apis/references/segmentation/)

세분화, 특히 세그먼트 활성화와 관련된 내용이 더 있습니다. 이러한 주제는 다른 튜토리얼에서 다루어질 것입니다.

모든 연습을 다 마쳤구나! 다음 단계로 진행하십시오. [결론](conclusion.md).
