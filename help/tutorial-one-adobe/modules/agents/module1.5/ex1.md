---
title: CJA 및 ChatGPT(MCP 서버 포함)
description: CJA 및 ChatGPT(MCP 서버 포함)
kt: 5342
doc-type: tutorial
source-git-commit: b8906d1995dcb470789be2a1297eb48cb7690a9c
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---

# 1.5.1 CJA 및 ChatGPT(MCP 서버 포함)

[!BADGE Alpha]

+++Alpha 세부 정보
MCP 서버 Alpha과 함께 CJA &amp; Claude.ai를 사용함으로써 귀하는 Alpha이 어떠한 종류의 보증도 없이 &quot;있는 그대로&quot; 제공된다는 것을 인정합니다. Adobe은 Alpha을 유지, 수정, 업데이트, 변경, 수정 또는 지원할 의무가 없습니다. 이러한 Alpha 및/또는 동봉된 자료의 올바른 기능이나 성능에 어떤 식으로든 의존하지 말고 주의하는 것이 좋습니다. Alpha은 Adobe의 기밀 정보로 간주됩니다. 귀하가 Adobe에 제공한 모든 &quot;피드백&quot;(Alpha 사용 중 발생하는 문제 또는 결함, 제안, 개선 사항 및 권장 사항을 포함하되 이에 국한되지 않는 Alpha 관련 정보)은 이에 따라 해당 피드백에 대한 모든 권한, 제목 및 관심을 포함하여 Adobe에 할당됩니다.

+++

>[!NOTE]
>
>ChatGPT가 있는 MCP 서버를 설정하고 사용하여 CJA에 연결하는 이 연습은 이 연습 [1.1 Customer Journey Analytics: Adobe Experience Platform의 맨 위에 있는 Analysis Workspace을 사용하여 대시보드를 빌드](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/customer-journey-analytics-build-a-dashboard.md)와(과) 관련이 있습니다. 아래 연습에서 사용 중인 CJA 데이터 보기 및 연결은 해당 연습에서 설정된 데이터 보기 및 연결입니다. 아래 결과를 복제하려면 먼저 해당 지침을 따라야 합니다.

## 비디오

이 비디오에서는 이 연습과 관련된 모든 단계에 대한 설명과 데모를 제공합니다.

>[!VIDEO](https://video.tv.adobe.com/v/3479159?quality=12&learn=on)

## 1.5.1.1 CJA용 ChatGPT에서 사용자 지정 앱 만들기

>[!NOTE]
>
>ChatGPT에서 CJA을 사용하려면 다음 요구 사항이 있습니다.
>- OpenAI의 ChatGPT의 유료 버전
>- ChatGPT 웹 클라이언트 사용

[https://chatgpt.com/](https://chatgpt.com/){target="_blank"}(으)로 이동한 다음 계정 세부 정보를 사용하여 로그인합니다. 로그인하면 이 메시지가 표시됩니다. 사용자 이름을 클릭합니다.

![ChatGPT](./images/chatgpt1.png)

**설정**&#x200B;을 선택하세요.

![ChatGPT](./images/chatgpt2.png)

**앱**(으)로 이동한 다음 **고급 설정**&#x200B;을 선택합니다.

![ChatGPT](./images/chatgpt3.png)

**개발자 모드**&#x200B;를 켠 다음 **뒤로**&#x200B;를 클릭하세요.

![ChatGPT](./images/chatgpt4.png)

**앱 만들기**&#x200B;를 클릭합니다.

![ChatGPT](./images/chatgpt5.png)

다음과 같이 필드를 채웁니다.

- **이름**: `CJA`
- **MCP 서버 URL**: Adobe 담당자에게 확인
- **인증**: `OAuth`

**이해하고 계속하겠습니다**&#x200B;에 대한 확인란을 선택하세요.

**만들기**&#x200B;를 클릭합니다.

![ChatGPT](./images/chatgpt6.png)

성공적으로 로그인하면 이제 CJA 앱이 성공적으로 연결되었음을 알 수 있습니다.

![ChatGPT](./images/chatgpt8.png)

## CJA에서 1.5.1.2 컨텍스트 설정

이 창을 닫습니다.

![ChatGPT 및 CJA](./images/chatgpt9.png)

그럼 이걸 보셔야죠 **+** 아이콘을 클릭하고 **자세히**(으)로 이동한 다음 **CJA**&#x200B;을(를) 선택합니다.

![ChatGPT 및 CJA](./images/chatgpt10.png)

ChatGPT를 통해 CJA과 상호 작용하기 전에 컨텍스트를 설정해야 합니다.

이 연습에서는 다음을 사용하도록 컨텍스트를 설정해야 합니다.

- **데이터 보기**: **—aepUserLdap— - 옴니채널 데이터 보기**

Dataview 설정은 ChatGPT가 질문을 할 때 확인해야 하는 데이터 보기를 식별하는 데 도움이 됩니다.

다음 **확인**&#x200B;을 입력하고 **보내기** 단추를 클릭하세요.

```javascript
list dataviews
```

![ChatGPT 및 CJA](./images/chatgpt11.png)

그러면 사용 가능한 유사한 데이터 보기 목록이 표시됩니다.

![ChatGPT 및 CJA](./images/chatgpt11a.png)

사용해야 하는 데이터 보기로 변경하려면 다음 **Prompt**&#x200B;을(를) 입력하고 **보내기** 단추를 클릭하십시오.

```javascript
switch to dataview --aepUserLdap-- - Omnichannel Data View
```

![ChatGPT 및 CJA](./images/chatgpt12.png)

그럼 이걸 보셔야죠

![ChatGPT 및 CJA](./images/chatgpt16.png)

이제 컨텍스트가 제대로 설정되었으므로 다음에 특정 프롬프트 전송을 시작할 수 있습니다.

## 1.5.1.3 데이터 보기 탐색

>[!NOTE]
>
>여기에서 사용 중인 데이터 보기가 연습 [데이터 보기 만들기](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md)의 일부로 설정되었습니다.

다음 **프롬프트**&#x200B;를 입력하고 **보내기** 단추를 클릭하여 사용 가능한 지표와 차원을 탐색합니다.

```javascript
list the available metrics and dimensions
```

![ChatGPT 및 CJA](./images/chatgpt101.png)

그런 다음 연습 [데이터 보기 만들기](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md)의 일부로 설정된 지표 및 차원을 포함하는 이 응답이 표시됩니다.

![ChatGPT 및 CJA](./images/chatgpt102.png)

## 1.5.1.4 자유 형식 테이블 - 제품 보기

이제 데이터 탐색을 시작할 수 있습니다. 먼저 아래 프롬프트를 입력하고 **보내기**&#x200B;를 클릭하여 보고서 요청을 제출합니다.

```javascript
how many product views happened on January 21?
```

![ChatGPT 및 CJA](./images/chatgpt103.png)

**RunReport**&#x200B;를 선택하십시오.

![ChatGPT 및 CJA](./images/chatgpt104.png)

그러면 다음과 같은 응답이 표시됩니다.

![ChatGPT 및 CJA](./images/chatgpt105.png)

이제 차원을 추가하여 응답을 분류할 수 있습니다. 다음 **프롬프트**&#x200B;를 입력하고 **보내기** 단추를 클릭하십시오.

```javascript
break down product views by product name
```

![ChatGPT 및 CJA](./images/chatgpt106.png)

그러면 다음과 같은 응답이 표시됩니다.

![ChatGPT 및 CJA](./images/chatgpt107.png)

이제 시각화를 만들 수도 있습니다. 다음 **프롬프트**&#x200B;를 입력하고 **보내기** 단추를 클릭하십시오.

```javascript
create a line visualization by hour for product views on January 21
```

![ChatGPT 및 CJA](./images/chatgpt108.png)

**프로젝트 업데이트**&#x200B;를 선택하십시오.

![ChatGPT 및 CJA](./images/chatgpt109.png)

**RunReport**&#x200B;를 선택하십시오.

![ChatGPT 및 CJA](./images/chatgpt110.png)

그럼 이걸 보셔야죠

![ChatGPT 및 CJA](./images/chatgpt111.png)

아래로 스크롤합니다.

![ChatGPT 및 CJA](./images/chatgpt112.png)

이제 이 선 그래프를 다운로드할 수도 있습니다. 다음 **프롬프트**&#x200B;를 입력하고 **보내기** 단추를 클릭하십시오.

```javascript
export this chart to PNG
```

![ChatGPT 및 CJA](./images/chatgpt113.png)

그럼 이걸 보셔야죠 **PNG 다운로드**&#x200B;를 클릭합니다.

![ChatGPT 및 CJA](./images/chatgpt114.png)

다음 **프롬프트**&#x200B;를 입력하고 **보내기** 단추를 클릭하십시오.

```javascript
can you breakdown product views by user agent?
```

![ChatGPT 및 CJA](./images/chatgpt115.png)

**RunReport**&#x200B;를 선택하십시오.

![ChatGPT 및 CJA](./images/chatgpt116.png)

그럼 이걸 보셔야죠

![ChatGPT 및 CJA](./images/chatgpt117.png)

## 1.5.1.5 폴아웃 시각화

다음 **프롬프트**&#x200B;를 입력하고 **보내기** 단추를 클릭하십시오.

```javascript
can you create a fallout visualization for the product interaction funnel, starting with all traffic and then in the next steps add Product Views, Add to Cart and purchases?
```

![ChatGPT 및 CJA](./images/chatgpt118.png)

**프로젝트 업데이트**&#x200B;를 선택하십시오.

![ChatGPT 및 CJA](./images/chatgpt119.png)

**RunReport**&#x200B;를 선택하십시오.

![ChatGPT 및 CJA](./images/chatgpt120.png)

그럼 이런 걸 보셔야겠네요 다음 **프롬프트**&#x200B;를 입력하고 **보내기** 단추를 클릭하십시오.

```javascript
can you show me a visualization of the above fallout analysis?
```

![ChatGPT 및 CJA](./images/chatgpt120a.png)

**PNG 다운로드**&#x200B;를 클릭합니다.

![ChatGPT 및 CJA](./images/chatgpt121.png)

이제 폴아웃 분석의 시각화가 표시됩니다.

![ChatGPT 및 CJA](./images/chatgpt122.png)

다음 **프롬프트**&#x200B;를 입력하고 **보내기** 단추를 클릭하십시오.

```javascript
break down the fallout analysis at the touchpoint of the add to carts
```

![ChatGPT 및 CJA](./images/chatgpt123.png)

**RunReport**&#x200B;를 선택하십시오.

![ChatGPT 및 CJA](./images/chatgpt124.png)

[분석 및 에이전트](./analyticsagents.md){target="_blank"}(으)로 돌아가기

[모든 모듈로 돌아가기](./../../../overview.md){target="_blank"}