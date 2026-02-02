---
title: MCP 서버가 있는 Adobe Analytics 및 Claude.ai
description: MCP 서버가 있는 Adobe Analytics 및 Claude.ai
kt: 5342
doc-type: tutorial
source-git-commit: 5eb5432251ee7193909ed4ec7decd0d94d0843a2
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# 1.5.3 Adobe Analytics &amp; Claude.ai(MCP 서버 포함)

[!BADGE Alpha]

+++Alpha 세부 정보
MCP 서버 Alpha과 함께 CJA &amp; Claude.ai를 사용함으로써 귀하는 Alpha이 어떠한 종류의 보증도 없이 &quot;있는 그대로&quot; 제공된다는 것을 인정합니다. Adobe은 Alpha을 유지, 수정, 업데이트, 변경, 수정 또는 지원할 의무가 없습니다. 이러한 Alpha 및/또는 동봉된 자료의 올바른 기능이나 성능에 어떤 식으로든 의존하지 말고 주의하는 것이 좋습니다. Alpha은 Adobe의 기밀 정보로 간주됩니다. 귀하가 Adobe에 제공한 모든 &quot;피드백&quot;(Alpha 사용 중 발생하는 문제 또는 결함, 제안, 개선 사항 및 권장 사항을 포함하되 이에 국한되지 않는 Alpha 관련 정보)은 이에 따라 해당 피드백에 대한 모든 권한, 제목 및 관심을 포함하여 Adobe에 할당됩니다.

+++

## 비디오

이 비디오에서는 이 연습과 관련된 모든 단계에 대한 설명과 데모를 제공합니다.

>[!VIDEO](https://video.tv.adobe.com/v/3479562?quality=12&learn=on)

## 1.5.3.1 Adobe Analytics용 Claude.ai에서 사용자 지정 앱 만들기

>[!NOTE]
>
>Claude.ai에서 Adobe Analytics을 사용하려면 다음 사항이 필요합니다.
>- 클로드.ai의 유료 버전
>- Claude.ai 웹 클라이언트 사용

[https://claude.ai/](https://claude.ai/){target="_blank"}(으)로 이동한 다음 계정 세부 정보를 사용하여 로그인합니다. 로그인하면 이 메시지가 표시됩니다. **+** 아이콘을 클릭합니다.

![클라우드.ai](./images/claudeaa1.png)

**커넥터 추가**&#x200B;를 선택합니다.

![클라우드.ai](./images/claudeaa2.png)

**사용자 지정 항목 추가**&#x200B;를 클릭합니다.

![클라우드.ai](./images/claudeaa3.png)

다음과 같이 필드를 채웁니다.

- **이름**: `CJA`
- **MCP 서버 URL**: Adobe 담당자에게 확인

**추가를 클릭합니다**.

![클라우드.ai](./images/claudeaa4.png)

그럼 이걸 보셔야죠 **연결**&#x200B;을 클릭합니다.

![클라우드.ai](./images/claudeaa5.png)

인증이 완료되면 이 메시지가 표시됩니다. 새 채팅을 시작하려면 **+** 아이콘을 클릭하세요.

![클라우드.ai](./images/claudeaa6.png)

**+**, **커넥터**(으)로 이동하면 이제 **Adobe Analytics** 커넥터가 활성화되어 있습니다.

![클라우드.ai](./images/claudeaa7.png)

이제 데이터 분석을 시작할 준비가 되었습니다.

![클라우드.ai](./images/claudeaa8.png)

## Adobe Analytics에서 1.5.3.2 컨텍스트 설정

Claude.ai를 통해 CJA과 더 상호 작용하기 전에 컨텍스트를 설정해야 합니다.

이 연습에서는 다음을 사용하도록 컨텍스트를 설정해야 합니다.

- **보고서 세트**: **CID - 데모 데이터**

보고서 세트 설정은 Cloud.ai가 질문을 할 때 확인해야 하는 데이터를 식별하는 데 도움이 됩니다.

다음 **확인**&#x200B;을 입력하고 **보내기** 단추를 클릭하세요.

```javascript
list report suites
```

![클라우드.ai](./images/claudeaa9.png)

**항상 허용**&#x200B;을 선택하세요.

![클라우드.ai](./images/claudeaa10.png)

**항상 허용**&#x200B;을 선택하세요.

![클라우드.ai](./images/claudeaa11.png)

그럼 이런 걸 보셔야겠네요

![클라우드.ai](./images/claudeaa12.png)

다음 **확인**&#x200B;을 입력하고 **보내기** 단추를 클릭하세요.

```javascript
use report suite CID Demo Data
```

![클라우드.ai](./images/claudeaa13.png)

**항상 허용**&#x200B;을 선택하세요.

![클라우드.ai](./images/claudeaa14.png)

이제 보고서 세트가 선택되었습니다.

![클라우드.ai](./images/claudeaa15.png)

## 1.5.2.3 보고서 세트 탐색

다음 **프롬프트**&#x200B;를 입력하고 **보내기** 단추를 클릭하여 사용 가능한 지표와 차원을 탐색합니다.

```javascript
list the available metrics and dimensions
```

![Claude.ai 및 CJA](./images/claudeaa101.png)

**항상 허용**&#x200B;을 선택하세요.

![Claude.ai 및 CJA](./images/claudeaa102.png)

**항상 허용**&#x200B;을 다시 선택하십시오.

![Claude.ai 및 CJA](./images/claudeaa103.png)

그러면 이 보고서 세트에 설정된 지표 및 차원을 포함하는 이 응답이 표시됩니다.

![Claude.ai 및 CJA](./images/claudeaa104.png)

## 1.5.2.4개 보고서

이제 데이터 탐색을 시작할 수 있습니다. 먼저 아래 프롬프트를 입력하고 **보내기**&#x200B;를 클릭하여 보고서 요청을 제출합니다.

```javascript
show me pageviews for Feb 2?
```

![Claude.ai 및 CJA](./images/claudeaa105.png)

그럼 이런 걸 보셔야겠네요

![Claude.ai 및 CJA](./images/claudeaa106.png)

다음 **확인**&#x200B;을 입력하고 **보내기** 단추를 클릭하세요.

```javascript
break down pageviews by page name
```

![Claude.ai 및 CJA](./images/claudeaa107.png)

그럼 이걸 보셔야죠

![Claude.ai 및 CJA](./images/claudeaa108.png)

다음 **확인**&#x200B;을 입력하고 **보내기** 단추를 클릭하세요.

```javascript
give me an overview of page names, page views by marketing channel
```

![Claude.ai 및 CJA](./images/claudeaa109.png)

그럼 이런 걸 보셔야겠네요

![Claude.ai 및 CJA](./images/claudeaa110.png)

분석을 보려면 아래로 조금 스크롤하십시오.

![Claude.ai 및 CJA](./images/claudeaa111.png)

다음 **확인**&#x200B;을 입력하고 **보내기** 단추를 클릭하세요.

```javascript
Analyze different metrics by marketing channel
```

![Claude.ai 및 CJA](./images/claudeaa112.png)

그럼 이런 걸 보셔야겠네요

![Claude.ai 및 CJA](./images/claudeaa113.png)

이제 이 연습을 완료했습니다.

[분석 및 에이전트](./analyticsagents.md){target="_blank"}(으)로 돌아가기

[모든 모듈로 돌아가기](./../../../overview.md){target="_blank"}