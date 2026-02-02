---
title: MCP 서버가 있는 CJA 및 Claude.ai
description: MCP 서버가 있는 CJA 및 Claude.ai
kt: 5342
doc-type: tutorial
source-git-commit: 5eb5432251ee7193909ed4ec7decd0d94d0843a2
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 0%

---

# 1.5.2 CJA &amp; Claude.ai(MCP 서버 포함)

[!BADGE Alpha]

+++Alpha 세부 정보
MCP 서버 Alpha과 함께 CJA &amp; Claude.ai를 사용함으로써 귀하는 Alpha이 어떠한 종류의 보증도 없이 &quot;있는 그대로&quot; 제공된다는 것을 인정합니다. Adobe은 Alpha을 유지, 수정, 업데이트, 변경, 수정 또는 지원할 의무가 없습니다. 이러한 Alpha 및/또는 동봉된 자료의 올바른 기능이나 성능에 어떤 식으로든 의존하지 말고 주의하는 것이 좋습니다. Alpha은 Adobe의 기밀 정보로 간주됩니다. 귀하가 Adobe에 제공한 모든 &quot;피드백&quot;(Alpha 사용 중 발생하는 문제 또는 결함, 제안, 개선 사항 및 권장 사항을 포함하되 이에 국한되지 않는 Alpha 관련 정보)은 이에 따라 해당 피드백에 대한 모든 권한, 제목 및 관심을 포함하여 Adobe에 할당됩니다.

+++


>[!NOTE]
>
>CJA에 연결하기 위해 Claude.ai가 있는 MCP 서버를 설정하고 사용하는 것에 대한 이 연습은 이 연습 [1.1 Customer Journey Analytics: Adobe Experience Platform의 맨 위에 있는 Analysis Workspace을 사용하여 대시보드를 빌드](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/customer-journey-analytics-build-a-dashboard.md)와(과) 관련이 있습니다. 아래 연습에서 사용 중인 CJA 데이터 보기 및 연결은 해당 연습에서 설정된 데이터 보기 및 연결입니다. 아래 결과를 복제하려면 먼저 해당 지침을 따라야 합니다.

## 비디오

이 비디오에서는 이 연습과 관련된 모든 단계에 대한 설명과 데모를 제공합니다.

>[!VIDEO](https://video.tv.adobe.com/v/3479561?quality=12&learn=on)

## 1.5.2.1 CJA용 Claude.ai에서 사용자 지정 앱 만들기

>[!NOTE]
>
>Claude.ai에서 CJA을 사용하려면 다음 사항이 필요합니다.
>- 클로드.ai의 유료 버전
>- Claude.ai 웹 클라이언트 사용

[https://claude.ai/](https://claude.ai/){target="_blank"}(으)로 이동한 다음 계정 세부 정보를 사용하여 로그인합니다. 로그인하면 이 메시지가 표시됩니다. **+** 아이콘을 클릭합니다.

![클라우드.ai](./images/claude1.png)

**커넥터 추가**&#x200B;를 선택합니다.

![클라우드.ai](./images/claude2.png)

**사용자 지정 항목 추가**&#x200B;를 클릭합니다.

![클라우드.ai](./images/claude3.png)

다음과 같이 필드를 채웁니다.

- **이름**: `CJA`
- **MCP 서버 URL**: Adobe 담당자에게 확인

**추가를 클릭합니다**.

![클라우드.ai](./images/claude4.png)

그럼 이걸 보셔야죠 **연결**&#x200B;을 클릭합니다.

![클라우드.ai](./images/claude5.png)

인증이 완료되면 이 메시지가 표시됩니다. 새 채팅을 시작하려면 **+** 아이콘을 클릭하세요.

![클라우드.ai](./images/claude6.png)

**+**, **커넥터**(으)로 이동하면 이제 **CJA** 커넥터가 활성화되어 있습니다.

![클라우드.ai](./images/claude8.png)

이제 데이터 분석을 시작할 준비가 되었습니다.

![클라우드.ai](./images/claude7.png)

## CJA에서 1.5.2.2 컨텍스트 설정

Claude.ai를 통해 CJA과 더 상호 작용하기 전에 컨텍스트를 설정해야 합니다.

이 연습에서는 다음을 사용하도록 컨텍스트를 설정해야 합니다.

- **데이터 보기**: **—aepUserLdap— - 옴니채널 데이터 보기**

데이터 보기 설정은 질문을 할 때 Claude.ai가 확인해야 하는 데이터 보기를 식별하는 데 도움이 됩니다.

다음 **확인**&#x200B;을 입력하고 **보내기** 단추를 클릭하세요.

```javascript
list dataviews
```

![Claude.ai 및 CJA](./images/claude9.png)

**항상 허용**&#x200B;을 선택하세요.

![Claude.ai 및 CJA](./images/claude10.png)

그러면 사용 가능한 유사한 데이터 보기 목록이 표시됩니다.

![Claude.ai 및 CJA](./images/claude11.png)

사용해야 하는 데이터 보기로 변경하려면 다음 **Prompt**&#x200B;을(를) 입력하고 **보내기** 단추를 클릭하십시오.

```javascript
switch to dataview --aepUserLdap-- - Omnichannel Data View
```

![Claude.ai 및 CJA](./images/claude11a.png)

**항상 허용**&#x200B;을 선택하세요.

![Claude.ai 및 CJA](./images/claude12.png)

그럼 이걸 보셔야죠

![Claude.ai 및 CJA](./images/claude16.png)

이제 컨텍스트가 제대로 설정되었으므로 다음에 특정 프롬프트 전송을 시작할 수 있습니다.

## 1.5.2.3 데이터 보기 탐색

>[!NOTE]
>
>여기에서 사용 중인 데이터 보기가 연습 [데이터 보기 만들기](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md)의 일부로 설정되었습니다.

다음 **프롬프트**&#x200B;를 입력하고 **보내기** 단추를 클릭하여 사용 가능한 지표와 차원을 탐색합니다.

```javascript
list the available metrics and dimensions
```

![Claude.ai 및 CJA](./images/claude101.png)

**항상 허용**&#x200B;을(를) 두 번 선택합니다. 한 번은 **지표**&#x200B;을(를) 검색하고 두 번째는 **차원**&#x200B;을(를) 검색합니다.

![Claude.ai 및 CJA](./images/claude101a.png)

그런 다음 연습 [데이터 보기 만들기](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md)의 일부로 설정된 지표 및 차원을 포함하는 이 응답이 표시됩니다.

![Claude.ai 및 CJA](./images/claude102.png)

## 1.5.2.4 자유 형식 테이블 - 제품 보기

이제 데이터 탐색을 시작할 수 있습니다. 먼저 아래 프롬프트를 입력하고 **보내기**&#x200B;를 클릭하여 보고서 요청을 제출합니다.

```javascript
how many product views happened on January 21, 2026?
```

![Claude.ai 및 CJA](./images/claude103.png)

**항상 허용**&#x200B;을 선택하세요.

![Claude.ai 및 CJA](./images/claude104.png)

그러면 다음과 같은 응답이 표시됩니다.

![Claude.ai 및 CJA](./images/claude105.png)

이제 차원을 추가하여 응답을 분류할 수 있습니다. 다음 **프롬프트**&#x200B;를 입력하고 **보내기** 단추를 클릭하십시오.

```javascript
break down product views by product name
```

![Claude.ai 및 CJA](./images/claude106.png)

그러면 다음과 같은 응답이 표시됩니다.

![Claude.ai 및 CJA](./images/claude107.png)

이제 시각화를 만들 수도 있습니다. 다음 **프롬프트**&#x200B;를 입력하고 **보내기** 단추를 클릭하십시오.

```javascript
create a line visualization by hour for product views on January 21
```

![Claude.ai 및 CJA](./images/claude108.png)

그럼 이걸 보셔야죠

![Claude.ai 및 CJA](./images/claude109.png)

이제 이 선 그래프를 다운로드할 수도 있습니다. 다음 **프롬프트**&#x200B;를 입력하고 **보내기** 단추를 클릭하십시오.

```javascript
export this chart to PNG
```

![Claude.ai 및 CJA](./images/claude113.png)

그럼 이걸 보셔야죠 **다운로드**&#x200B;를 클릭합니다.

![Claude.ai 및 CJA](./images/claude114.png)

그런 다음 다운로드한 PNG를 열고 다른 문서에서 사용할 수 있습니다.

![Claude.ai 및 CJA](./images/claude114a.png)

다음 **프롬프트**&#x200B;를 입력하고 **보내기** 단추를 클릭하십시오.

```javascript
can you breakdown product views by user agent?
```

![Claude.ai 및 CJA](./images/claude115.png)

그럼 이걸 보셔야죠

![Claude.ai 및 CJA](./images/claude117.png)

## 1.5.2.5 폴아웃 시각화

다음 **프롬프트**&#x200B;를 입력하고 **보내기** 단추를 클릭하십시오.

```javascript
can you create a fallout visualization for the product interaction funnel, starting with all traffic and then in the next steps add Product Views, Add to Cart and purchases?
```

![Claude.ai 및 CJA](./images/claude118.png)

그런 다음 Customer Journey Analytics에서 제공한 데이터를 기반으로 Claude.ai가 생성한 시각화가 포함된 것과 같은 것을 볼 수 있습니다.

![Claude.ai 및 CJA](./images/claude119.png)

다음 단계: [MCP 서버가 있는 Adobe Analytics 및 Claude.ai](./ex3.md){target="_blank"}

[분석 및 에이전트](./analyticsagents.md){target="_blank"}(으)로 돌아가기

[모든 모듈로 돌아가기](./../../../overview.md){target="_blank"}