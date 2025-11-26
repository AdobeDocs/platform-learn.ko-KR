---
title: Agent Orchestrator 시작하기
description: Agent Orchestrator 시작하기
kt: 5342
doc-type: tutorial
source-git-commit: dee5b0855eeeb455bf22f511d11cd13f7e904889
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 0%

---

# 1.1.1 Agent Orchestrator 시작하기

## Agent Orchestrator에서 1.1.1.1 컨텍스트 설정

[https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat)&#x200B;(으)로 이동합니다.

그럼 이걸 보셔야죠 조직 **Experience Platform International**&#x200B;에 있는지 확인하세요.

![Agent Orchestrator](./images/ao1.png)

**컨텍스트** 창을 클릭합니다.

![Agent Orchestrator](./images/ao2.png)

컨텍스트를 다음으로 설정합니다.

- **설명서 Source**: **Customer Journey Analytics**
- **샌드박스**: **가속화**
- **데이터 보기**: **2026년 B2C 가속화**

**컨텍스트 설정**&#x200B;을 클릭합니다.

![Agent Orchestrator](./images/ao3.png)

## 1.1.1.2 전체 구매 트렌드로 시작하여 컨텍스트를 고정하고 파이버 확대

**의도**

특히 최근 60일 동안 모바일, 유선전화, 인터넷, TV, 파이버 등 카테고리 요구 사항에 대한 최고 수준의 펄스 수신 이는 뉴욕 롤아웃 이후 계절성, 프로모션 효과 및 지역 분산에 대한 기준선을 설정합니다.

다음 **확인**&#x200B;을 입력하고 **보내기** 단추를 클릭하세요.

```javascript
Show me purchases by mainCategory over the last 2 months.
```

![Agent Orchestrator](./images/ao4.png)

그런 다음 이 메시지가 표시됩니다.

![Agent Orchestrator](./images/ao5.png)

다음 **확인**&#x200B;을 입력하고 **보내기** 단추를 클릭하세요.

`Show me purchases by mainCategory = Fiber over the last 2 months per week`

![Agent Orchestrator](./images/ao6.png)

그런 다음 파이버 관련 추세로 드릴다운하는 이 내용을 확인해야 합니다.

**작업**: 증가 곡선과 지역 급등에 주의하십시오.

![Agent Orchestrator](./images/ao7.png)

## 1.1.1.3에서 주문과 콘텐츠 환경 설정의 상관 관계를 지정합니다.

**의도**

컨텐츠 환경 설정(예: SciFi, Sports, Drama)이 특히 고대역폭 요구 사항에 대한 광대역 업그레이드 동작을 예측한다는 가설을 테스트합니다.

다음 **확인**&#x200B;을 입력하고 **보내기** 단추를 클릭하세요.

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/ao8.png)

그런 다음 이 메시지가 표시됩니다.

![Agent Orchestrator](./images/ao9.png)

## 1.1.1.4 기존 파이버 여정 식별

**의도**

제목에 &quot;파이버&quot;가 포함된 활성 여정 또는 최근에 체결된 세그먼트를 확인합니다(예: &quot;파이버 업그레이드 NYC - 9월&quot;, &quot;파이버 평가판 - 스트리밍 번들&quot;).

다음 **확인**&#x200B;을 입력하고 **보내기** 단추를 클릭하세요.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/ao12.png)

그런 다음 이 메시지가 표시됩니다.

![Agent Orchestrator](./images/ao13.png)

파이버 메시징을 사용하여 활성 또는 과거 여정을 나열합니다.

작업: 복제할 고성능 여정을 목록에 추가합니다.

다음 **확인**&#x200B;을 입력하고 **보내기** 단추를 클릭하세요.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/ao14.png)

그런 다음 이 메시지가 표시됩니다.

![Agent Orchestrator](./images/ao15.png)

## 1.1.1.5 시드 확인

**의도**:

CitiSignal - Fibre Max Launch Promotion 여정의 초기 정의(예: &quot;SciFi 장르 환경 설정&quot;, &quot;4+ 장치&quot;, &quot;스트림 ≥ 300GB/month&quot;)를 대상으로 한 특성)를 이해합니다.

자동 완성을 사용하려면 다음 **Prompt**&#x200B;을(를) 입력한 다음 **+CitiSignal fib**&#x200B;을(를) 입력하십시오. 여정 **CitiSignal - 파이버 최대 시작 승격**&#x200B;을 선택하십시오.

```javascript
What was the initial audience in the journey named 
```

![Agent Orchestrator](./images/ao16.png)

그럼 이걸 보셔야죠 **보내기** 단추를 클릭합니다.

![Agent Orchestrator](./images/ao17.png)

그럼 이걸 보셔야죠

![Agent Orchestrator](./images/ao18.png)

## 1.1.1.6 폴아웃 분석을 통해 여정 성능의 유효성 검사

**의도**

Customer Journey Analytics에서 단계별 funnel 구축

제품 보기→ 장바구니→ 추→ 또→ 주문 완료→ 위해 →을 →

파이버 관련 SKU 보기를 분기로 포함합니다.

다음 **확인**&#x200B;을 입력하고 **보내기** 단추를 클릭하세요.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/ao19.png)

## 1.1.1.7 새 대상 만들기

**의도**

위 연구 결과에 따르면, 많은 데이터를 소비하고 공상과학 또는 판타지 장르를 선호하는 고객 사이에 상관 관계가 있습니다. 이제 대상에서 이러한 속성을 결합합니다.

[https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat)&#x200B;(으)로 이동합니다.

다음 **확인**&#x200B;을 입력하고 **보내기** 단추를 클릭하세요.

>[!NOTE]
>
>도우미의 컨텍스트가 샌드박스 **가속화** 및 데이터 보기 **2026 B2C 가속화**&#x200B;를 가리키는지 확인하십시오.

```javascript
Create an audience that combines people with an average download per month of over 2000 GB and a preferred genre of sci-fi or fantasy.
```

![Agent Orchestrator](./images/ao32.png)

계획을 검토합니다. `yes`을(를) 입력하고 **보내기**&#x200B;를 클릭합니다.

![Agent Orchestrator](./images/ao33.png)

세그먼트 쿼리 표현식을 검토합니다. `yes`을(를) 입력하고 **보내기** 단추를 클릭합니다.

![Agent Orchestrator](./images/ao34.png)

세그먼트 크기 추정을 검토합니다. `yes`을(를) 입력하고 **보내기** 단추를 클릭합니다.

![Agent Orchestrator](./images/ao35.png)

**검토**&#x200B;를 클릭합니다.

![Agent Orchestrator](./images/ao36.png)

세그먼트 정의를 검토합니다. **만들기**&#x200B;를 클릭합니다.

![Agent Orchestrator](./images/ao37.png)

이제 대상자가 생성되었습니다.

![Agent Orchestrator](./images/ao38.png)

>[!NOTE]
>
>새 대상을 만들 때 24시간 후에 도우미에서 추가 용도로 대상을 사용할 수 있습니다.

## 1.1.1.8 사용량이 많은 기존 대상을 찾아 사용 중인지 확인

**의도**:

월별 데이터 사용 임계값으로 정의된 &quot;대량 다운로드&quot;를 사용하여 이름이 지정된 대상을 찾습니다.

>[!NOTE]
>
>이전 단계에서 새 대상을 만든 경우, 도우미가 대상을 추가로 사용할 수 있으려면 24시간이 걸립니다. 이제 다른 기존 대상을 대신 사용해야 합니다.

[https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat)&#x200B;(으)로 이동합니다.

그럼 이걸 보셔야죠 조직 **Experience Platform International**&#x200B;에 있는지 확인하세요.

다음 **확인**&#x200B;을 입력하고 **보내기** 단추를 클릭하세요.

>[!NOTE]
>
>도우미의 컨텍스트가 샌드박스 **가속화** 및 데이터 보기 **2026 B2C 가속화**&#x200B;를 가리키는지 확인하십시오.

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

![Agent Orchestrator](./images/ao30.png)

그럼 이걸 보셔야죠

![Agent Orchestrator](./images/ao31.png)

이미 &quot;헤비 다운로더&quot;에 대한 일부 기존 대상자가 있습니다. 이미 사용 중인지 알아보겠습니다.

다음 **확인**&#x200B;을 입력하고 **보내기** 단추를 클릭하세요.

```javascript
Which of the above are used in a journey? 
```

![Agent Orchestrator](./images/ao50.png)

그러면 이와 비슷한 것을 볼 수 있을 겁니다.

![Agent Orchestrator](./images/ao51.png)

이제 해당 여정이 활성 상태인지 확인해야 합니다. 다음 **확인**&#x200B;을 입력하고 **보내기** 단추를 클릭하세요.

```javascript
Which of the above are used in a journey? 
```

![Agent Orchestrator](./images/ao52.png)

그러면 이와 비슷한 것을 볼 수 있을 겁니다. 해당 여정은 현재 실행되고 있지 않습니다.

![Agent Orchestrator](./images/ao53.png)

Fibre Max를 출시하려면 이제 새 여정을 만들어야 합니다.

## 1.1.1.9 파이버 최대 시작에 대한 새 여정 만들기

**의도**:

복합 대상을 타깃팅하는 새 여정을 빌드합니다.

대규모 다운로드 ∩ SciFi 환경 설정(kbaa_5207bf 대상 키).

[https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat)&#x200B;(으)로 이동합니다.

그럼 이걸 보셔야죠 조직 **Experience Platform International**&#x200B;에 있는지 확인하세요.

다음 **확인**&#x200B;을 입력하고 **보내기** 단추를 클릭하세요.

>[!NOTE]
>
>도우미의 컨텍스트가 샌드박스 **가속화** 및 데이터 보기 **2026 B2C 가속화**&#x200B;를 가리키는지 확인하십시오.

```javascript
Create a  journey towards the audience Heavy Downloaders - Sci-Fi Preference_kbaa_5207bf. The journey is for the rollout of fiber broadband. There will 2 versions of an email  based on  a split of the audience based on who is in the "Eligble for Fiber upgrade" audience.  After 3 days, profiles from both email treatments who have not purchased fibre max will be sent a follow up email. 
```

![Agent Orchestrator](./images/aocj1.png)

그럼 이걸 보셔야죠 `yes`을(를) 입력하고 생성을 클릭합니다.

![Agent Orchestrator](./images/aocj2.png)

그럼 이걸 보셔야죠 `yes`을(를) 입력하고 생성을 클릭합니다.

![Agent Orchestrator](./images/aocj3.png)

그럼 이걸 보셔야죠 `The first one`을(를) 입력하고 생성을 클릭합니다.

![Agent Orchestrator](./images/aocj4.png)

그럼 이걸 보셔야죠 `yes`을(를) 입력하고 생성을 클릭합니다.

![Agent Orchestrator](./images/aocj5.png)

응답을 검토합니다. `yes`을(를) 입력하고 생성을 클릭합니다.

![Agent Orchestrator](./images/aocj6.png)

**검토**&#x200B;를 클릭합니다.

![Agent Orchestrator](./images/aocj7.png)

LDAP로 여정 이름을 업데이트하여 고유한 이름을 만듭니다. **저장**&#x200B;을 클릭합니다.

![Agent Orchestrator](./images/aocj8.png)

이제 여정이 초안 모드에서 생성되었습니다.

![Agent Orchestrator](./images/aocj9.png)

## 1.1.1.10 여정 충돌 관리

[https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat)&#x200B;(으)로 이동합니다.

그럼 이걸 보셔야죠 조직 **Experience Platform International**&#x200B;에 있는지 확인하세요.

다음 **확인**&#x200B;을 입력하고 **보내기** 단추를 클릭하세요.

>[!NOTE]
>
>도우미의 컨텍스트가 설명서 소스 **Journey Optimizer**, 샌드박스 **가속화** 및 데이터 보기 **2026년 B2C 가속화**&#x200B;를 가리키는지 확인하십시오.

```javascript
How can I manage journey conflicts?
```

![Agent Orchestrator](./images/aocj80.png)

정보를 검토하십시오.

![Agent Orchestrator](./images/aocj81.png)

아래로 스크롤하고 **소스**&#x200B;를 선택하여 Experience League에서 가져온 정보를 확인합니다.

![Agent Orchestrator](./images/aocj82.png)

다음 **확인**&#x200B;을 입력하고 **보내기** 단추를 클릭하세요.

```javascript
List any conflicts for "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/aocj70.png)

여정 충돌 정보를 검토합니다.

![Agent Orchestrator](./images/aocj71.png)

아래로 스크롤하여 더 많은 여정 충돌 세부 정보를 찾습니다.

![Agent Orchestrator](./images/aocj72.png)

## 1.1.1.11개 실험

[https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat)&#x200B;(으)로 이동합니다.

그럼 이걸 보셔야죠 조직 **Experience Platform International**&#x200B;에 있는지 확인하세요.

다음 **확인**&#x200B;을 입력하고 **보내기** 단추를 클릭하세요.

>[!NOTE]
>
>도우미의 컨텍스트가 샌드박스 **가속화** 및 데이터 보기 **2026 B2C 가속화**&#x200B;를 가리키는지 확인하십시오.

```javascript
How are the experiments performing for the journey named 'CitiSignal - Fiber Max Launch Promotion'?
```

![Agent Orchestrator](./images/aoea0.png)

그런 다음 이 메시지가 표시됩니다.

![Agent Orchestrator](./images/aoea1.png)

각 치료의 전환율을 비교하려면 제안을 클릭한 다음 **보내기**&#x200B;를 클릭하십시오.

![Agent Orchestrator](./images/aoea2.png)

그러면 다음과 같은 자세한 비교가 표시됩니다.

![Agent Orchestrator](./images/aoea4.png)

[Agent Orchestrator](./agentorchestrator.md){target="_blank"}(으)로 돌아가기

[모든 모듈로 돌아가기](./../../../overview.md){target="_blank"}