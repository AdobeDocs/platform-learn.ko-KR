---
title: Bootcamp - Customer Journey Analytics - Customer Journey Analytics을 사용한 시각화 - 브라질
description: Bootcamp - Customer Journey Analytics - Customer Journey Analytics을 사용한 시각화 - 브라질
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 1%

---

# 4.5 Customer Journey Analytics 사용 시각화

## 목표

- Analysis Workspace UI 이해
- Analysis Workspace의 다양한 기능을 살펴볼 수 있습니다.
- Analysis Workspace을 사용하여 CJA에서 분석하는 방법을 알아봅니다

## 컨텍스트

이 연습에서는 CJA 내의 Analysis Workspace을 사용하여 제품 보기, 제품 유입 경로, 이탈 등을 분석합니다.

에서 만든 프로젝트를 사용하겠습니다 [4.4 Analysis Workspace의 데이터 준비](./ex4.md), 다음 위치로 이동하십시오. [https://analytics.adobe.com](https://analytics.adobe.com).

![데모](./images/prohome.png)

프로젝트를 엽니다. `yourLastName - Omnichannel Analysis`.

프로젝트를 열고 데이터 보기를 사용하여 `yourLastName - Omnichannel Analysis` 선택한 경우 첫 번째 시각화 작성을 시작할 준비가 되었습니다.

![데모](./images/prodataView1.png)

## 일별로 제품 보기가 몇 개입니까

먼저 데이터를 분석할 올바른 날짜를 선택해야 합니다. 캔버스 오른쪽의 달력 드롭다운으로 이동합니다. 을(를) 클릭하고 적용 가능한 날짜 범위를 선택합니다.

>[!IMPORTANT]
>
>다음과 같은 날짜 범위를 선택하십시오 **이번 주** 또는 **이번 달**. 사용 가능한 최근 데이터가 2022년 9월 19일에 수집되었습니다.

![데모](./images/pro1.png)

왼쪽 메뉴(구성 요소 영역)에서 계산된 지표를 찾습니다 **제품 보기**. 항목을 선택하고 자유 형식 테이블 오른쪽 위의 캔버스에 드래그하여 놓습니다.

![데모](./images/pro2.png)

자동으로 차원 **일** 첫 번째 테이블을 만들기 위해 이 추가됩니다. 이제 질문에 대한 즉각적인 답변이 보입니다.

![데모](./images/pro3.png)

다음으로, 지표 요약을 마우스 오른쪽 단추로 클릭합니다.

![데모](./images/pro4.png)

클릭 **시각화** 그런 다음 **라인** 시각화로 사용할 수 있습니다.

![데모](./images/pro5.png)

제품의 보기를 일별로 볼 수 있습니다.

![데모](./images/pro6.png)

을(를) 클릭하여 시간 범위를 일별로 변경할 수 있습니다 **설정** 시각화 내에서 사용할 수 있습니다.

![데모](./images/pro7.png)

옆에 있는 점을 클릭합니다 **라인** to **데이터 소스 관리**.

![데모](./images/pro7a.png)

다음을 클릭합니다. **선택 잠금** 을(를) 선택합니다. **선택한 항목** 이 시각화를 잠그면 항상 제품 보기 타임라인을 표시하도록 할 수 있습니다.

![데모](./images/pro7b.png)

## 본 상위 5개 제품

상위 5개 제품이 무엇을 보았습니까?

때때로 프로젝트를 저장해야 합니다.

| OS | 짧은 컷 |
| ----------------- |-------------| 
| Windows | Control + S |
| Mac | Command+S |

상위 5개 제품을 확인하겠습니다. 왼쪽 메뉴에서 **제품 이름** - Dimension.

![데모](./images/pro8.png)

이제 끌어서 놓기 **제품 이름** 를 **일** 차원:

이것이 결과입니다

![데모](./images/pro10a.png)

그런 다음 제품 중 하나를 브랜드 이름으로 분류하려고 합니다. 검색 대상 **brandName** 첫 번째 제품 이름 아래에서 끌어서 놓습니다.

![데모](./images/pro13.png)

다음으로 사용자 에이전트를 사용하여 분류를 수행합니다. 검색 대상 **사용자 에이전트** 브랜드 이름 아래로 끌어서 놓습니다.

![데모](./images/pro15.png)

그러면 다음 내용이 표시됩니다.

![데모](./images/pro15a.png)

마지막으로 시각화를 더 추가할 수 있습니다. 왼쪽의 시각화 아래에서 을 검색합니다. `Donut`. Take `Donut`캔버스에서 드래그하여 캔버스에 놓습니다 **라인** 시각화.

![데모](./images/pro18.png)

그런 다음 테이블에서 처음 5개를 선택합니다 **사용자 에이전트**  우리가 수행한 분석의 행 **Google Pixel XL 32GB 블랙 스마트폰** > **시티신호**. 5개의 행을 선택하는 동안 **CTRL** 단추(Windows의 경우) 또는 **명령** 단추(Mac에서).

![데모](./images/pro20.png)

도넛 차트가 변경된 것을 볼 수 있습니다.

![데모](./images/pro21.png)

두 가지 방법을 모두 사용하여 디자인을 보다 읽기 쉽게 조정할 수도 있습니다 **라인** 그래프 및 **도넛** 옆에 붙을 수 있도록 약간 더 작은 그래프를 만듭니다.

![데모](./images/pro22.png)

옆에 있는 점을 클릭합니다 **도넛** to **데이터 소스 관리**.
다음을 클릭합니다. **선택 잠금** 이 시각화를 잠그면 항상 제품 보기 타임라인을 표시하도록 할 수 있습니다.

![데모](./images/pro22b.png)

Analysis Workspace을 사용한 시각화에 대한 자세한 내용은 다음 사이트를 참조하십시오.

- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html?lang=ko](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html?lang=ko)
- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html)

## 보기에서 구매에 이르는 제품 상호 작용 단계

이 문제를 해결하는 방법은 여러 가지가 있다. 그 중 하나는 제품 상호 작용 유형을 사용하고 자유 형식 테이블에서 사용하는 것입니다. 다른 방법은 를 사용하는 것입니다 **폴아웃 시각화**. 마지막으로 시각화하고 분석하려고 합니다.

다음을 클릭하여 현재 패널을 닫습니다.

![데모](./images/pro23.png)

이제 다음을 클릭하여 새 빈 패널을 추가합니다 **+ 빈 패널 추가**.

![데모](./images/pro24.png)

시각화를 클릭합니다 **폴아웃**.

![데모](./images/pro25.png)

이전 연습과 동일한 날짜 범위를 선택합니다.

![데모](./images/prodatef.png)

그러면 이게 보입니다.

![데모](./images/prodatefa.png)

차원 찾기 **이벤트 유형** 왼쪽의 구성 요소 아래에서 다음을 수행합니다.

![데모](./images/pro26.png)

화살표를 클릭하여 차원을 엽니다.

![데모](./images/pro27.png)

사용 가능한 모든 이벤트 유형이 표시됩니다.

![데모](./images/pro28.png)

항목을 선택합니다 **commerce.productViews** 끌어서 놓습니다 **터치 포인트 추가** 내부 필드 **폴아웃 시각화**.

![데모](./images/pro29.png)

다음 방법으로 수행합니다 **commerce.productListAdds** 및 **commerce.purchases** 그리고 그것들을 **터치 포인트 추가** 내부 필드 **폴아웃 시각화**. 이제 시각화는 다음과 같이 표시됩니다.

![데모](./images/props1.png)

여기서 많은 일을 할 수 있어요 예: 시간에 따라 비교하고, 각 단계를 장치별로 비교하거나, 충성도에 따라 비교하십시오. 하지만 고객이 장바구니에 항목을 추가한 후 구매하지 않는 이유와 같은 흥미로운 사항을 분석하려는 경우 CJA에서 가장 좋은 도구를 사용할 수 있습니다. 마우스 오른쪽 단추를 클릭합니다.

터치 포인트를 마우스 오른쪽 단추로 클릭합니다. **commerce.productListAdds**. 그런 다음 을(를) 클릭합니다. **이 터치포인트에서 폴아웃 분류**.

![데모](./images/pro32.png)

사람들이 구매하지 않은 경우 수행한 작업을 분석하기 위해 새 자유 형식 테이블이 만들어집니다.

![데모](./images/pro33.png)

변경 **이벤트 유형** by **페이지 이름**&#x200B;새 자유 형식 테이블에서 구매 확인 페이지 대신 표시할 페이지를 확인합니다.

![데모](./images/pro34.png)

## 서비스 취소 페이지에 도달하기 전에 사이트에서 사람들이 수행하는 작업은 무엇입니까?

다시 말하지만, 이 분석을 수행하는 방법에는 여러 가지가 있습니다. 흐름 분석을 사용하여 검색 부품을 시작하겠습니다.

다음을 클릭하여 현재 패널을 닫습니다.

![데모](./images/pro0.png)

이제 다음을 클릭하여 새 빈 패널을 추가합니다 **+ 빈 패널 추가**.

![데모](./images/pro0a.png)

시각화를 클릭합니다 **흐름**.

![데모](./images/pro35.png)

그러면 다음 내용이 표시됩니다.

![데모](./images/pro351.png)

이전 연습과 동일한 날짜 범위를 선택합니다.

![데모](./images/pro0b.png)

차원 찾기 **페이지 이름** 왼쪽의 구성 요소 아래에서 다음을 수행합니다.

![데모](./images/pro36.png)

화살표를 클릭하여 차원을 엽니다.

![데모](./images/pro37.png)

본 모든 페이지가 표시됩니다. 페이지 이름을 찾습니다. **서비스 취소**.
드래그 앤 드롭 **서비스 취소** 을 가운데 필드에 있는 흐름 시각화로 이동합니다.

![데모](./images/pro38.png)

그러면 다음 내용이 표시됩니다.

![데모](./images/pro40.png)

이제 가 **서비스 취소** 이 웹사이트에 있는 페이지는 콜센터라고도 하고 결과는 무엇이었는지를 나타냅니다.

차원 아래에서 다시 돌아가서 를 찾습니다. **호출 상호 작용 유형**.
드래그 앤 드롭 **호출 상호 작용 유형** 의 오른쪽에 있는 첫 번째 상호 작용을 대체하려면 **플로우 시각화**.

![데모](./images/pro43.png)

이제 를 방문한 후 콜 센터에 전화한 고객의 지원 티켓을 보게 됩니다 **서비스 취소** 페이지.

![데모](./images/pro44.png)

그런 다음 차원 아래에서 을 검색합니다. **통화 느낌**.  을(를) 끌어다 놓아 오른쪽의 첫 번째 상호 작용을 **플로우 시각화**.

![데모](./images/pro46.png)

그러면 다음 내용이 표시됩니다.

![데모](./images/flow.png)

보시다시피 플로우 시각화를 사용하여 옴니채널 분석을 실행했습니다. 서비스를 취소하려는 일부 고객들이 콜센터에 전화를 한 후 긍정적인 감정을 가진 것으로 보입니다. 승진을 통해 마음을 바꿨을까.


## 기본 KPI에 대해 양의 콜센터 연락처를 사용하는 고객은 어떻게 수행됩니까?

먼저 데이터를 세그먼트화하여 사용자에게만 **긍정적** 호출. CJA에서 세그먼트를 필터라고 합니다. 구성 요소 영역(왼쪽) 내의 필터로 이동한 다음 를 클릭합니다 **+**.

![데모](./images/pro58.png)

필터 빌더 내에서 필터에 이름을 지정합니다

| 이름 | 설명 |
| ----------------- |-------------| 
| 전화 감상 - 긍정적 | 전화 감상 - 긍정적 |

![데모](./images/pro47.png)

구성 요소(필터 빌더 내)에서 **통화 느낌** 을 사용하여 필터 빌더 정의로 끌어서 놓습니다.

![데모](./images/pro48.png)

이제 을(를) 선택합니다. **긍정적** 값을 로 설정합니다.

![데모](./images/pro49.png)

범위를 변경할 대상 **개인** 수준.

![데모](./images/pro50.png)

완료하려면 **저장**.

![데모](./images/pro51.png)

그럼 다시 오셔야 합니다 아직 수행하지 않았다면 이전 패널을 닫습니다.

![데모](./images/pro0c.png)

이제 다음을 클릭하여 새 빈 패널을 추가합니다 **+ 빈 패널 추가**.

![데모](./images/pro24c.png)

이전 연습과 동일한 날짜 범위를 선택합니다.

![데모](./images/pro24d.png)

클릭 **자유 형식 테이블**.

![데모](./images/pro52.png)

이제 방금 만든 필터를 드래그하여 놓습니다.

![데모](./images/pro53.png)

지표를 추가할 시간입니다. 다음으로 시작 **제품 보기**. 자유 형식 테이블로 끌어서 놓습니다. 또한 **이벤트** 지표.

![데모](./images/pro54.png)

다음 방법으로 수행합니다 **사람**,  **장바구니에 추가** 및 **구매**. 이런 테이블로 끝나게 될 거야

![데모](./images/pro55.png)

첫 번째 흐름 분석 덕분에, 새로운 질문이 떠올랐습니다. 그래서 이 테이블을 만들고 세그먼트에 대한 일부 KPI를 확인하여 해당 질문에 답하기로 했습니다. 알 수 있듯이, 통찰력은 SQL을 사용하거나 다른 BI 솔루션을 사용하는 것보다 훨씬 빠릅니다.

## Customer Journey Analytics 및 Analysis Workspace 요약

이 실습에서 배웠듯이 Analysis Workspace에서는 모든 채널의 데이터를 함께 결합하여 전체 고객 여정을 분석합니다. 또한 여정에 결합되지 않은 동일한 작업 공간으로 데이터를 가져올 수도 있습니다.
이렇게 하면 여정에 컨텍스트를 제공하기 위해 끊어진 데이터를 분석으로 가져오는 데 유용할 수 있습니다. 일부 예로는 NPS 데이터, 설문 조사, Facebook 광고 이벤트 또는 오프라인 상호 작용(식별되지 않음)과 같은 것들이 있습니다.

다음 단계: [4.6 인사이트에서 다음으로 시작](./ex6.md)

[사용자 흐름 4로 돌아가기](./uc4.md)

[모든 모듈로 돌아가기](./../../overview.md)
