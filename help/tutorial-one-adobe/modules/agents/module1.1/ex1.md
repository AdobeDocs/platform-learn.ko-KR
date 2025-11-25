---
title: Agent Orchestrator 시작하기
description: Agent Orchestrator 시작하기
kt: 5342
doc-type: tutorial
source-git-commit: e90dee164dfe098c9fc56a04c481a733c0843858
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 0%

---

# 1.1.1 Agent Orchestrator 시작하기

## 1.1.1 Agent Orchestrator에서 컨텍스트 설정

AI Assistant로 이동하여 큰 보기에 배치합니다.

분석 작업을 위해 CJA 컨텍스트에 있는지 확인합니다.

>[!NOTE]
>
>분석(CJA)과 오케스트레이션(JO) 간을 이동할 때 컨텍스트 전환을 사용합니다.

## 1.1.2 전반적인 구매 트렌드로 시작하여 컨텍스트를 고정하고 광섬유로 확대

**프롬프트**:

```javascript
Show me purchases by mainCategory over the last 2 month
```

**의도**: 특히 최근 60일 동안 모바일, 유선전화, 인터넷, TV, 파이버 등 범주 요구 사항에 대한 전체 펄스 받기. 이는 NY 롤아웃 이후의 계절성, 프로모션 효과 및 지역 차이에 대한 기준선을 설정합니다.

생각:

&quot;Fibre가 postNY에서 점유율을 높이고 있습니까? 우리는 Copper/DSL 인터넷의 조립을 보고 있습니까? Shift 키와 TV 번들의 혼합은 무엇입니까?&quot;

&quot;이는 비엔나의 대응 가능 대상을 평가하고 현실적인 목표를 설정하는 데 도움이 될 것입니다.&quot;

마케터가 기대하는 실행 가능한 읽기 단위:

메인 범주별 누적 막대/라인 구매 차트(일별/주별 그레인).

이전 기간과의 범주별 구매 비율.

프로모션 날짜와 관련된 주목할 만한 급증.

>[!NOTE]
>
>지연 특성 파악 - 일부 기존 스키마의 &quot;인터넷&quot;에서 Fibre 주문이 캡처될 수 있습니다. 그렇다면 결정 전에 분류를 조정하십시오.

 

**프롬프트**:

```javascript
Show me purchases by mainCategory over the last 2 monthzoom into fiber performance
```

**다음 프롬프트**

`Show me purchases by mainCategory = Fiber over the last 2 months`

Fibre별 추세를 자세히 살펴봅니다.

**작업** 증가 곡선 및 지역 급등을 기록합니다.

## 1.1.3 주문과 콘텐츠 환경 설정 간 상관 관계

**프롬프트**:

```javascript
Show me ordersYTD by preferred genre for the last 2 months
```

**의도** 콘텐츠 환경 설정(예: SciFi, Sports, Drama)이 특히 고대역폭 요구 사항에 맞게 광대역 업그레이드 동작을 예측한다는 가설을 테스트합니다.

**생각 중**

&quot;SciFi 팬들은 종종 4K를 시청하고 여러 디바이스에서 스트리밍하므로 짧은 지연 시간을 중요시할 수 있습니다.&quot;

&quot;SciFi(및 Sports)가 최근 주문과 관련이 있는지 여부를 수치화하겠습니다.&quot;

**예상 출력**

최근 2개월로 제한된, 기본 장르 별로 분류된 주문 피벗(YTD 필터 적용됨).

주문 전환율 및 AOV(평균 주문 값)로 장르의 등급을 지정합니다.

의사 결정: SciFi가 강력한 신호를 보여주는 경우, 이는 비엔나의 Fibre Max 출시(예: &quot;다시 버퍼링 안 함&quot; 메시지, 프리미엄 번들)의 주요 크리에이티브 기둥이 됩니다.

**프롬프트**

`Show me ordersYTD by preferred genre for the last 2 months`

**의도**

장르별 전환 분석 (예: 공상 과학, 스포츠).

**목표** 파이버 업그레이드를 위한 Sci-Fi 팬 색인 초과 여부를 확인합니다.

## 1.1.4 기존 파이버 여정 확인

**프롬프트**:

```javascript
What journey was running and had Fiber in the name
```

**의도** 제목에 &quot;파이버&quot;가 포함된 활성 여정 또는 최근에 체결된 세그먼트를 검색합니다(예: &quot;파이버 업그레이드 NYC - 9월&quot;, &quot;파이버 평가판 - 스트리밍 번들&quot;).

**생각 중**

&quot;이들 여정 중 어떤 것이 잘 수행되었고, 그 유발인자는 무엇이었습니까?&quot;

&quot;Vienna에서 가장 뛰어난 오케스트레이션 논리를 재사용할 수 있습니까?&quot;

**예상 출력**

상태(활성, 일시 정지됨, 종료됨), 날짜 범위, 대상 여정, KPI(열람율, CTR, 전환)가 있는 세그먼트 목록입니다.

다음으로 이동: 복제/적응을 위해 하나 또는 두 개의 성공적인 파이버 여정을 후보 목록에 추가합니다.

**프롬프트**

`What journey was running and had Fiber in the name?`

파이버 메시징을 사용하여 활성 또는 과거 여정을 나열합니다.

작업: 복제할 고성능 여정을 목록에 추가합니다.

## 1.1.5 시드 대상자에게 관련 내역 프로모션 확인

**프롬프트**:

```javascript
What was the initial audience in that SCi-Fi promo 2024 - jl journey
```

**의도** 타깃팅을 유도한 특성(예: &quot;SciFi 장르 환경 설정&quot;, &quot;4+ 장치&quot;, &quot;스트림 ≥ 300GB/월&quot;)인 &quot;SciFi Promo 2024 - jl&quot; 여정의 시드 정의를 이해합니다.

**생각 중**

&quot;검증된 SciFi 크리에이티브를 Fibre Max 성능 메시지와 결합하고자 합니다.&quot;

&quot;만약 청중들이 무거운 다운로드자들과 겹친다면, 우리는 그 성향을 쌓을 수 있다.&quot;

**예상 출력**

대상 기준(포함/제외), 대상 크기, 영역 필터, 최신성, 빈도 임계값.

>[!NOTE]
>
>컨텍스트를 CJA으로 변경

이 시점에서부터 마케터는 올바른 보고를 위해 분석 모드로 전환합니다.

**프롬프트**:

```javascript
What was the initial audience in that SCi-Fi promo 2024 - jl journey?
```

대상 기준(스트리밍 습관, 장치 수)을 검토합니다.

목표: 고대역폭 요구 사항에 대한 트레이트를 파악합니다.

## 1.1.6 폴아웃 분석을 통해 여정 성능 확인

**프롬프트**:

```javascript
Create a fall-out report on the "Sci-Fi Promo 2024 - jl" journey
```

>[!NOTE]
>
>컨텍스트를 CJA으로 변경)

**의도** Customer Journey Analytics에서 계단식 funnel 구축

제품 보기→ 장바구니→ 추→ 또→ 주문 완료→ 위해 →을 →

파이버 관련 SKU 보기를 분기로 포함합니다.

생각:

&quot;이메일 열기, 랜딩 페이지 로드, PDP, 체크아웃 마찰 등 인력이 손실되는 곳은 어디입니까?&quot;

&quot;Fibre PDP에서 SciFi 사용자가 평균보다 많거나 적거나 바운스됩니까?&quot;

예상 출력:

각 단계에서 드롭오프 비율이 있는 폴아웃 시각화.

세그먼트 오버레이(SciFi와 스포츠 및 기타).

기술적인 마찰에 대한 장치/브라우저 분류.

결정:

체크아웃 드롭오프가 높은 경우 제품/UX와 조정하여 결제 플로우를 수정합니다.

PDP 종료가 높으면 재작업 요구 명확성(속도, 설치 시간, 번들 값)을 나타냅니다.

>[!NOTE]
>
>JO로 컨텍스트 변경

이제 마케팅 담당자는 오케스트레이션 및 대상 작업을 위해 Adobe Journey Optimizer으로 이동합니다.

**프롬프트**:

```javascript
Create a fall-out report on the "Sci-Fi Promo 2024 - jl" journey 
```

funnel 시각화 작성: 주문→ 체크아웃→ 클릭한 →으로 →.

작업: 드롭오프 지점을 식별하고 메시지 또는 UX를 최적화합니다.


## 1.1.7 높은 사용률에 맞는 기존 대상 찾기

**프롬프트**:

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

>[!NOTE]
>
>컨텍스트를 Adobe Journey Optimizer으로 변경

의도: 월간 데이터 사용량 임계값, 스트리밍 시간 또는 장치 동시성으로 정의될 수 있는 &quot;대량 다운로드&quot;와 함께 이름이 지정된 JO 대상을 찾습니다.

생각:

&quot;Heavy Downloaders와 같은 대상이 있다면 속도, 신뢰성, 계층 제한 없는 Fibre Max 포지셔닝에 적합합니다.&quot;

예상 출력:

대상 메타데이터: 정의 기준, 크기, 마지막 새로 고침, 거버넌스 태그, 지역 가용성

**프롬프트**:

```javascript
Is there an audience that has " heavy downloaders" in the title 
```

데이터 사용량이 많은 대상을 찾습니다.

목표: 파이버 최대 타깃팅을 위한 Sf 환경 설정과 결합

## 1.1.8 해당 대상이 이미 사용 중인지 확인합니다

**프롬프트**:

```javascript
Which of the above are used in a journey? 
```

의도: 대상자와 여정 간의 연결 확인 - 메시지가 이중화되거나 현재 프로그램과 충돌하지 않는지 확인합니다.

생각:

&quot;Heavy Downloaders가 이미 유지 여정에 있는 경우 피로를 방지하기 위해 억제 논리나 빈도 제한이 필요합니다.&quot;

예상 출력:

매핑: 대상자 → 여정 이름, 상태, 연락처 정책, 마지막 전송, 성능.

결정:

사용 중인 경우 Vienna 실행에 대한 제외 또는 공유 제외를 만듭니다.

사용하지 않는 경우 새 여정의 경우 녹색 표시등입니다.

프롬프트:

위 중 여정에서 사용되는 것은 무엇입니까?

활성 캠페인과 겹치지 않도록 합니다.

조치: 필요한 경우 제외를 적용합니다.

## 1.1.9 Fibre Max Launch용 새 여정 만들기

**프롬프트**:

```javascript
Create a  journey towards the audience Heavy Downloaders - Sci-Fi Preference_kbaa_5207bf. The journey is for the rollout of fiber broadband. There will 2 versions of an email  based on  a split of the audience based on who is in the "Eligble for Fiber upgrade" audience.  After 3 days, profiles from both email treatments who have not purchased fibre max will be sent a follow up email. 
```

의도: 복합 대상을 타겟팅하는 새 JO 여정 구축:

대규모 다운로드 ∩ SciFi 환경 설정(kbaa_5207bf 대상 키).

생각:

&quot;이는 높은 성향 및 창의적 관련성, Fibre Max의 좋은 점입니다.&quot;

&quot;Vienna의 가용성과 관련된 멀티 터치 경험을 조율할 것입니다.&quot;

여정 디자인(JO):

시작 기준:

대상: Heavy Downloaders - Sf Preference_kbaa_5207bf

지역: 비엔나 지하철(ZIP/우편 번호 목록 또는 지역 다각형)

자격 조건: 현재 파이버 구독자가 아니라 활성 &quot;파이버 업그레이드 NYC - 9월&quot; 캠페인에 없음.

트리거 및 시간:

Vienna 출시 14일 전(2026년 1월): 이메일 미리 보기—&quot;Fibre Max 출시 예정&quot;

시작 주: 기본 이메일 + 인앱 배너 + 유료 미디어 동기화(CDP 대상을 통해).

T+3일: 비헤이비어 분할 - 클릭이 없는 경우 SMS를 살짝 밉니다. 클릭했지만 주문하지 않은 경우 설치 관리자 가용성 CTA으로 다시 타깃팅합니다.

T+10일: 무료 설치와 1개월 할인 비교(A/B).

Personalization:

SciFi 애호가를 위한 동적 복사본(지연 시간/4K 스트리밍 후크).

장치 조합(게임 콘솔, 스트리밍 박스)에 적합한 속도/지연 클레임입니다.

번들 권장 사항: Fibre Max + 프리미엄 TV scifi 콘텐츠 팩.

거버넌스

빈도 상한: 10일당 최대 3번의 터치

현재 파이버 구독자가 있는지 또는 설치할 티켓이 있는지 표시하지 않습니다.

옵트아웃 환경 설정을 준수합니다.

측정 계획(CJA):

추적: 게재, 열기, 클릭, PDP 보기, 체크아웃 시작, 주문 완료.

KPI: Fibre Max로의 전환율, 제어 대비 업그레이드, 시간 초과 설치

진단: 장치/장르 세그먼트별 폴아웃 보고서.

모양

이 모든 것이 일치하는 방식(마케터의 정신 모델)

수요 진단(Fibre→ 전체 범주)

contenttoconversion 신호(장르별 주문)를 증명합니다.

지뢰에 성공한 여정(Fibernamed 여정 및 SciFi 프로모션 대상자 찾기).

마찰 지점 유효성 검사(Sf 여정에서 CJA 폴아웃).

성향 세그먼트(대규모 다운로드 ∩ SciFi)에 대해 활성화합니다.


[Agent Orchestrator](./agentorchestrator.md){target="_blank"}(으)로 돌아가기

[모든 모듈로 돌아가기](./../../../overview.md){target="_blank"}