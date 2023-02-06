---
title: Bootcamp - Customer Journey Analytics - Analysis Workspace의 데이터 준비 - 브라질
description: Bootcamp - Customer Journey Analytics - Analysis Workspace의 데이터 준비 - 브라질
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 1%

---

# 4.4 프리카상 데 도스 Customer Journey Analytics

## 오베티보

- CJA에서 UO do Analysis Workspace 입력
- 엔켄다 os conceitos de preaçao de dados no Analysis Workspace
- 아펜다 아펠르카울쿠로스 데 도도스

## 4.4.1 UI에서 Analysis Workspace을 CJA에서 실행

O Analysis Workspace은 Todas를 무한 호스 티피카스 데 움 니코 렐라토리오 도 분석가로 제거합니다. Ele fornece uma tela robusta e flexível para prercriar projetos de analytics personalizados. Arraste e solte qualquer nude tabelas de dados, visualizasules e 구성 요소(차원, 메트리카, 세그멘토스 e granularidades de tempo) para projto. 크리아상 인스타네아 데 아바리아스 세그멘토스, 크리아상 드 코르테 아날리스, 크리아상 드 알랄르타스, 비교라상 드 세그멘토스, 아날라상 드 플루아칸소 e de falhas e relaattorrios de curaradoria e agendpartilhar com quer pessoa em segnocio

O Customer Journey Analytics 트라에사 용카상 알렘 두도스 다 플라타포마 É Altamente recomendável asissitir a este vídeo de visugular de quatro minutos:

>[!VIDEO](https://video.tv.adobe.com/v/35109?quality=12&learn=on)

Analysis Workspace 낭트의 보흐누카 우수, 레코멘데모에스테 비데오:

>[!VIDEO](https://video.tv.adobe.com/v/26266?quality=12&learn=on)

### 크리에서프로제토

CJA를 위한 아고레 호라 데 크리아르세우 프라임로 프로빌로 프로제토 CJA를 위한 Vá para aba de projetos dentro do CJA입니다. Clique em **새로 만들기**.

![데모](./images/prmenu.png)

엠세구이다, 보스케베라 텔라아비아소입니다 셀레치온 **빈 프로젝트** 엔타앙 클레케 **만들기**.

![데모](./images/prmenu1.png)

Vokverá um projito vazio.

![데모](./images/premptyprojects.png)

Primeiro, certifique-se de selecionar a Visualizaço de dados correta에서 우수한 direito da da tela에 도달할 수 없습니다. 네스테 모예, 사용자 셀레치오나다 `vangeluwe - Omnichannel Data View`.

![데모](./images/prdv.png)

엠세구이다, 보스케이라엘살바르 세우 프르제토 에다르 엄은 엘레 Vokpode Usar o seguinte comando para salbaar:

| OS | 짧은 컷 |
| ----------------- |-------------| 
| Windows | Control + S |
| Mac | Command+S |

Vokheverá este 팝업:

![데모](./images/prsave.png)

상태 모델 사용:

| 이름 | 설명 |
| ----------------- |-------------| 
| `yourLastName - Omnichannel Analysis` | `yourLastName - Omnichannel Analysis` |

Em Seguida, Client em **저장**.

![데모](./images/prsave2.png)

## 4.4.2 메트리카 계산대

엠보라 텐하모스 조직도 토도 os 구성 요소, Visualizaçao de dados, vocain da deve adaptar algues husuários de negocios jestein para iniciar suas análises. 알렘 디소, 두란테 퀄퀘어 프로세서 드 분석, 보스포데 크리알메트리카 계산 파라라 프로푼다는 데스코베르타 데 인사이트를 제공합니다.

코모 예시, 크리아레모스 타사 드 컨투아오 주산도 a métrica/evento Compras que definitionas na Visualizaçao de dados.

## 탁사 드 컨투앙

Vamos começar는 De métracas caladas의 축약자 입니다. Clique em **+** 파라 슈아 primeira 메트리카 계산라다 노 Analysis Workspace

![데모](./images/pradd.png)

O **계산된 지표 빌더** irla aprecer:

![데모](./images/prbuilder.png)

Encontre **구매** na lista de métracas no menu do lado esquerdo. Em **지표** clique em **모두 표시**

![데모](./images/calcbuildercr1.png)

아고라 아르세트 용테 **구매** na definiçao da métrica calculada.

![데모](./images/calcbuildercr2.png)

정상, 탁사 드 컨버에이션 **전환 / 세션**. 엔탕, 아모스 페이저 o mesmo cálculo na tela de definiçao de métrica calada. 메트리카 **세션** eArraste e solte-a no criador de dedefiniçao, evento 없음 **구매**.

![데모](./images/calcbuildercr3.png)

Que o perador de divisao selecionado automaticamente를 관찰하십시오.

![데모](./images/calcbuildercr4.png)

탁사 드 컨투앙 오무멘테 대표는 em portcentagem입니다. 엔탕, 바모스 무다르 o 포르마토 파라포르센타감 e selecionar 2 casas decimais.

![데모](./images/calcbuildercr5.png)

마지막으로 계산된 지표의 이름 및 설명을 변경합니다.

| Title | 설명 |
| ----------------- |-------------| 
| 전환율 | 전환율 |

푸르 피엠, 알테레 노 노메 마르탕 다 메트리카 계산라다:

![데모](./images/calcbuildercr6.png)

나앙세케사 데 **엘살바르** 메트리카 계산대.

![데모](./images/pr9.png)

## 4.4.3 차원 계산: Filtros(segmentaçao) e intervalos de datas

### 필터: 차원 계산대

알쿠로스 나방 데브엠 사 아페나스 파라메트리카 낭트 드 이니시아 qualquer análise, também é interessante criar algumas **계산된 Dimension**. 아주 중요하며, 의미있고, **세그먼트** Adobe Analytics 없음. Customer Journey Analytics 없음, 세그멘토스 상카모도 드 **필터**.

![데모](./images/prfilters.png)

크리아상 데 필트로스 아주다라로스 데 네고시오는 분석 com algumas dimension sallowas es calculaas. 이소이라오타아살아그라파스 타레파스 알렘 드 아주다르 나파르 데 아도싸오 애비소 에스타오 알구스 엑소스:

1. 미디아 프로프리아, 미디아 파가,
2. 비지타스 노바스 x 레코드
3. Clientes.com carrinho abandonado

필트로스 포데모체 크림 반테스 우 두란테 드 아나리스 (o que vocfarah no practiimo exilitioncio).

### Intervalos de datas: 차원 스템포 계산대

치수 속도가 상투로 티포 데 차원 계산대로 알건즈 바 포르람 크림도, 마스 보카 캄페 푸데 크리아르스 프라프리아 치메산 데 템포 페르스타아제 나 파제 드 프라카도 드 데카오.

에사스 디메수에스 드 템포 계산도 아주다라앙 아날라오스 데 네고시오는 레브르르 데이터를 가져오기 위해 우사-라스 여과르 e 알테르 또는 템포 데 릴라토리오 페르군타스 데 두비다스 타이피카스 취안도 파제모스 아나우리스:

- 블랙프라이데이 카노 패스카도 요? os dias 21e 29를 입력하시겠습니까?
- 까팔까르네 아캄파냐 드 TV 까드데브리오?
- 2018년 벤다스 데 베랑 데 양자도 피제모스가? Quero comparar com 2019. 프로포시토, 보이스 다이아스 2019년 전

![데모](./images/timedimensions.png)

Analysis Workspace 도 CJA의 아고라 보쿠리우 오 프리히오 드 데프레라상 데 두사오 데 쿠산도

프로시마 에타파: [4.5 시각화 아상 우산도 Customer Journey Analytics](./ex5.md)

[레토나르 플루소 드 우시오 4](./uc4.md)

[레토날라 파라 토도스 오모두로스](./../../overview.md)
