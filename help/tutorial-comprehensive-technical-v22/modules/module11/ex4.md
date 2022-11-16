---
title: Customer Journey Analytics - Analysis Workspace의 데이터 준비
description: Customer Journey Analytics - Analysis Workspace의 데이터 준비
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: c1d4037b-7656-4777-86ad-a1e3e9a8464b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 3%

---

# Analysis Workspace에서 11.4 데이터 준비

## 목표

- CJA의 Analysis Workspace UI 이해
- Analysis Workspace의 데이터 준비 개념 이해
- 데이터 계산 방법 알아보기

## 11.4.1 CJA의 Analysis Workspace UI

Analysis Workspace은 단일 Analytics 보고서의 모든 일반적인 제한 사항을 제거합니다. 사용자 지정 분석 프로젝트를 빌드하기 위한 강력하고 유연한 캔버스를 제공합니다. 많은 데이터 테이블, 시각화 및 구성 요소(차원, 지표, 세그먼트 및 시간 세부기간)를 프로젝트에 드래그하여 놓습니다. 즉시 분류 및 세그먼트를 만들고, 분석에 사용할 집단을 만들고, 경고를 만들고, 세그먼트를 비교하고, 흐름 및 폴아웃 분석을 수행하고, 비즈니스 내 누구와도 공유할 보고서를 큐레이션 및 예약합니다.

Customer Journey Analytics은 플랫폼 데이터를 기반으로 이 솔루션을 제공합니다. 4분 동안의 개요 비디오를 시청하는 것이 좋습니다.

>[!VIDEO](https://video.tv.adobe.com/v/35109?quality=12&learn=on)

이전에 Analysis Workspace을 사용하지 않았다면 이 비디오를 보는 것이 좋습니다.

>[!VIDEO](https://video.tv.adobe.com/v/26266?quality=12&learn=on)

### 프로젝트 만들기

이제 첫 번째 CJA 프로젝트를 만들 차례입니다. CJA 내의 프로젝트 탭으로 이동합니다.
**새로 만들기**&#x200B;를 클릭합니다.

![데모](./images/prmenu.png)

그러면 이게 보입니다. 선택 **빈 프로젝트** 을 클릭한 다음 **만들기**.

![데모](./images/prmenu1.png)

그러면 빈 프로젝트가 표시됩니다.

![데모](./images/premptyprojects.png)

먼저 화면의 오른쪽 상단 모서리에서 올바른 데이터 보기를 선택해야 합니다. 이 예에서 선택할 데이터 보기는 다음과 같습니다 `vangeluwe - Omnichannel Data View`.

![데모](./images/prdv.png)

그런 다음 프로젝트를 저장하고 이름을 지정합니다. 다음 명령을 사용하여 저장할 수 있습니다.

| OS | 짧은 컷 |
| ----------------- |-------------| 
| Windows | Control + S |
| Mac | Command+S |

다음 팝업이 표시됩니다.

![데모](./images/prsave.png)

다음 명명 규칙을 사용하십시오.

| 이름 | 설명 |
| ----------------- |-------------| 
| `--demoProfileLdap-- - Omnichannel Analysis` | `--demoProfileLdap-- - Omnichannel Analysis` |

다음을 클릭합니다. **저장**.

![데모](./images/prsave2.png)

## 11.4.2 계산된 지표

데이터 보기에서 모든 구성 요소를 구성했지만 비즈니스 사용자가 분석을 시작할 준비가 되도록 일부 구성 요소를 조정해야 합니다. 또한 분석 중에 계산된 지표를 만들어 인사이트 검색 결과를 세부적으로 확인할 수 있습니다.

예를 들어 계산된 지표를 만듭니다 **전환율** 사용 **구매** 데이터 보기에서 정의한 지표/이벤트.

### 전환율

계산된 지표 빌더 열기를 시작합니다. 을(를) 클릭합니다. **+** Analysis Workspace에서 첫 번째 계산된 지표를 만들려면

![데모](./images/pradd.png)

다음 **계산된 지표 빌더** 표시됩니다.

![데모](./images/prbuilder.png)

를 찾습니다. **구매** 왼쪽 메뉴에 있는 지표 목록에서 을 클릭합니다. 아래 **지표** click **모두 표시**

![데모](./images/calcbuildercr1.png)

이제 을(를) 끌어서 놓습니다 **구매** 계산된 지표 정의에 대한 지표입니다.

![데모](./images/calcbuildercr2.png)

일반적으로 전환율은 **전환 / 세션**. 따라서 계산된 지표 정의 캔버스에서 동일한 계산을 수행하겠습니다. 를 찾습니다. **세션** 지표를 드래그하여 정의 빌더 아래의 **구매** 이벤트.

![데모](./images/calcbuildercr3.png)

분할 연산자가 자동으로 선택되었음을 확인합니다.

![데모](./images/calcbuildercr4.png)

전환율은 일반적으로 백분율로 표시됩니다. 따라서 형식을 백분율로 변경하고 소수 2개를 선택합니다.

![데모](./images/calcbuildercr5.png)

마지막으로 계산된 지표의 이름 및 설명을 변경합니다.

| Title | 설명 |
| ----------------- |-------------| 
| 전환율 | 전환율 |

화면에 다음과 같은 내용이 표시됩니다.

![데모](./images/calcbuildercr6.png)

잊지 말고 **저장** 계산된 지표 를 참조하십시오.

![데모](./images/pr9.png)

## 11.4.3 계산된 Dimension: 필터(세그먼테이션) 및 날짜 범위

### 필터: 계산된 Dimension

계산은 지표에 대해서만 계산되지 않습니다. 분석을 시작하기 전에 몇 가지 분석을 만드는 것도 재미있습니다 **계산된 Dimension**. 이것은 기본적으로 **세그먼트** Adobe Analytics으로 돌아가겠습니다. Customer Journey Analytics에서 이러한 세그먼트를 **필터**.

![데모](./images/prfilters.png)

필터를 만들면 비즈니스 사용자가 몇 가지 중요한 계산된 차원으로 분석을 시작할 수 있습니다. 이를 통해 몇 가지 작업을 자동화할 수 있을 뿐만 아니라 채택을 지원할 수도 있습니다. 여기 몇 가지 예가 있습니다.

1. 자체 미디어, 유료 미디어,
2. 신규 방문과 재방문
3. 포기한 장바구니 고객

이러한 필터는 분석 부품 전이나 중에 만들 수 있습니다(다음 연습에서 수행).

### 날짜 범위: 계산된 시간 Dimension

시간 Dimension은 계산된 차원의 다른 유형입니다. 일부는 이미 만들어져 있지만 데이터 준비 단계에서 고유한 사용자 지정 시간 Dimension을 만들 수도 있습니다.

Adobe에서는 분석가 및 비즈니스 사용자가 중요한 날짜를 기억하고 이를 사용하여 보고 시간을 필터링하고 변경할 수 있도록 해주는 이러한 계산된 시간 Dimension을 제공합니다. 우리가 분석을 할 때 우리의 마음에 떠오르는 일반적인 질문들과 의심들.

- 작년에 블랙 프라이데이가 언제였나요? 21-29일?
- 12월에 TV광고를 언제 방송했나요?
- 2018년 여름 매상은 언제부터입니까? 2019년과 비교하고 싶습니다 그런데, 2019년의 정확한 날을 알고 있나요?

![데모](./images/timedimensions.png)

이제 CJA Analysis Workspace을 사용하여 데이터 준비 연습을 마쳤습니다.

다음 단계: [11.5 Customer Journey Analytics 사용 시각화](./ex5.md)

[모듈 11로 돌아가기](./customer-journey-analytics-build-a-dashboard.md)

[모든 모듈로 돌아가기](./../../overview.md)
