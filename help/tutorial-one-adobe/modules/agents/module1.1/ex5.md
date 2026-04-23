---
title: Adobe Marketing Agent 포 클로드
description: Adobe Marketing Agent 포 클로드
kt: 5342
doc-type: tutorial
exl-id: 2563ca77-699b-4cd3-af51-1105cea03c79
source-git-commit: 2339a3a9c122a3e757c59eec3a9be54acf8d9c1e
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 1%

---

# 1.1.5 Adobe Marketing Agent for Claude

[!BADGE Beta]

+++Beta 세부 정보
Claude Beta과 함께 Adobe Marketing Agent을 사용함으로써 귀하는 Beta이 어떠한 종류의 보증도 없이 &quot;있는 그대로&quot; 제공된다는 것을 인정합니다. Adobe은 Beta을 유지, 수정, 업데이트, 변경, 수정 또는 지원할 의무가 없습니다. 이러한 Beta 및/또는 동봉된 자료의 올바른 기능이나 성능에 어떤 식으로든 의존하지 말고 주의하는 것이 좋습니다. Beta은 Adobe의 기밀 정보로 간주됩니다.  귀하가 Adobe에 제공한 모든 &quot;피드백&quot;(Beta 사용 중 발생하는 문제 또는 결함, 제안, 개선 사항 및 권장 사항을 포함하되 이에 국한되지 않는 Beta 관련 정보)은 이에 따라 해당 피드백에 대한 모든 권한, 제목 및 관심을 포함하여 Adobe에 할당됩니다.

+++

## 전제 조건

아래 문서화된 대로 이 랩의 단계를 수행하려면 다음 액세스가 필요합니다.

- Real-Time CDP, Journey Optimizer 및 Customer Journey Analytics 액세스
- Adobe Experience Cloud의 AI Assistant 액세스
- AEP Agent Orchestrator 액세스
- 클로드 액세스

## 비디오

이 비디오에서는 이 연습과 관련된 모든 단계에 대한 설명과 데모를 제공합니다.

>[!VIDEO](https://video.tv.adobe.com/v/3482212?quality=12&learn=on)

이 실험실은 개발 중입니다.

## 1.1.5.1 CJA용 Claude.ai에서 사용자 지정 앱 만들기

>[!NOTE]
>
>Claude.ai에서 Adobe Marketing Agent을 사용하려면 다음 사항이 필요합니다.
>- 클로드.ai의 유료 버전

[https://claude.ai/](https://claude.ai/){target="_blank"}(으)로 이동한 다음 계정 세부 정보를 사용하여 로그인합니다. 로그인하면 이 메시지가 표시됩니다.

![클라우드.ai](./images/claude1.png)

계정을 열고 **설정**&#x200B;을(를) 선택합니다.

![클라우드.ai](./images/claude2.png)

**커넥터**(으)로 이동한 다음 **사용자 지정으로 이동**&#x200B;을 클릭합니다.

![클라우드.ai](./images/claude2a.png)

**+**&#x200B;을(를) 클릭한 다음 **사용자 지정 커넥터 추가**&#x200B;를 선택합니다.

![클라우드.ai](./images/claude3.png)

다음과 같이 필드를 채웁니다.

- **이름**: `Adobe Marketing Agent`
- **MCP 서버 URL**: Adobe 담당자에게 문의하십시오.

**추가를 클릭합니다**.

![클라우드.ai](./images/claude4.png)

그럼 이걸 보셔야죠 새 채팅을 시작하려면 **+**&#x200B;을(를) 클릭하세요.

![클라우드.ai](./images/claude5.png)

**+** 아이콘을 클릭하고 **커넥터**(으)로 이동한 다음 **Adobe Marketing Agent**&#x200B;이(가) 활성화되어 있는지 확인하십시오.

![클라우드.ai](./images/claude6.png)

## 1.1.5.2 인증 및 컨텍스트 설정

Claude.ai를 통해 Adobe Marketing Agent과 추가로 상호 작용하려면 로그인하고 컨텍스트를 설정해야 합니다.

다음 메시지를 입력하고 **보내기**&#x200B;를 클릭합니다.

```
login to Adobe Marketing Agent
```

![클라우드.ai](./images/claude7.png)

**항상 허용**&#x200B;을 선택하세요.

![클라우드.ai](./images/claude8.png)

Adobe 마케팅 에이전트에 로그인하려면 링크를 **.

![클라우드.ai](./images/claude8a.png)

**링크 열기**&#x200B;를 클릭합니다.

![클라우드.ai](./images/claude8b.png)

**액세스 허용**&#x200B;을 클릭합니다.

![클라우드.ai](./images/claude8c.png)

인증이 완료되면 이 메시지가 표시됩니다. 클로드로 돌아가

![클라우드.ai](./images/claude8d.png)

다음 명령을 입력하고 **보내기**&#x200B;를 클릭합니다.

```javascript
logged in
```

![클라우드.ai](./images/claude8e.png)

이제 정상적으로 로그인되었습니다. 다음 단계는 컨텍스트를 설정하는 것입니다. 다음 메시지를 입력하고 **보내기**&#x200B;를 클릭합니다.


```javascript
change context
```

![Claude.ai 및 CJA](./images/claude9.png)

**조직**&#x200B;을 선택하세요. 이 명령을 반복하여 나중에 샌드박스 및 데이터 보기를 변경할 수도 있습니다.

![Claude.ai 및 CJA](./images/claude10.png)

인스턴스 이름을 입력하고 **보내기**&#x200B;를 클릭합니다.

![Claude.ai 및 CJA](./images/claude11.png)

**항상 허용**&#x200B;을 선택하세요.

![Claude.ai 및 CJA](./images/claude12.png)

그럼 이런 걸 보셔야겠네요

![Claude.ai 및 CJA](./images/claude13.png)

샌드박스가 아직 제대로 설정되지 않은 경우 다음 명령을 사용하여 사용해야 하는 샌드박스로 변경할 수 있습니다. **보내기**&#x200B;를 클릭합니다. 또는 위의 명령 `change context`을(를) 사용한 다음 **샌드박스**&#x200B;를 선택할 수 있습니다

```javascript
change sandbox to --aepSandboxName--
```

![Claude.ai 및 CJA](./images/claude14.png)

데이터 보기가 아직 제대로 설정되지 않은 경우 다음 명령을 사용하여 사용해야 하는 샌드박스로 변경할 수 있습니다(아래 명령의 XXX를 데이터 보기 이름으로 바꾸기). **보내기**&#x200B;를 클릭합니다. 또는 위의 `change context` 명령을 사용한 다음 **데이터 보기**&#x200B;를 선택할 수 있습니다

```javascript
change dataview to XXX
```

![Claude.ai 및 CJA](./images/claude15.png)

**조직**, **샌드박스** 및 **데이터 보기**&#x200B;가 제대로 설정되면 Adobe Marketing Agent에 질문할 준비가 되었습니다.

## 다음 단계

[Agent Orchestrator](./agentorchestrator.md){target="_blank"}로 돌아가기

[모든 모듈로 돌아가기](./../../../overview.md){target="_blank"}
