---
title: Bootcamp - Customer Journey Analytics - Analysis Workspace의 데이터 준비 - 브라질
description: Bootcamp - Customer Journey Analytics - Analysis Workspace의 데이터 준비 - 브라질
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Workspace Basics, Calculated Metrics
exl-id: d56128af-dd1e-47ea-922f-85418e9da687
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 1%

---

# 4.4 Preparação de dados em Customer Journey Analytics

## Objetivos

- CJA의 UO do Analysis Workspace
- Entenda os conceitos de preparação de dados no Analysis Workspace
- 아프렌다 어 파제르 칼쿨로스 데 다도스

## 4.4.1 UI do Analysis Workspace no CJA

O Analysis Workspace limitações típicas de um único relatório do Analytics로 todas를 제거합니다. Ele fornece uma tela robusta e flexível para criar project de analytics personalizados. Arraste e solte qualquer número de tabelas de dados, visualizações e componentes (dimensões, métricas, segmentos e granularidades de tempo) para um projeto. Criação instantânea de avarias e segmentos, criação de cortes para análise, criação de alertas, comparação de segmentos, análise de fluxo e de falhas e relatórios de curadoria e agendamento para compartilhar com qualquer pessoa em seu negócio.

O Customer Journey Analytics traz essa solução além dos dados da plataforma. É altamente recommendável assistir a este vídeo de visão geral de quatro minutos:

>[!VIDEO](https://video.tv.adobe.com/v/35109?quality=12&learn=on)

Se você nunca usou o Analysis Workspace antes, recommendamos este vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/26266?quality=12&learn=on)

### 크리세 프로제토

Agora é hora de criar seu primeiro project do CJA. Vá para a aba de projetos dentro do CJA. 클리크 **새로 만들기**.

![데모](./images/prmenu.png)

Em seguida, você verá a tela abaixo. 선택 항목 **빈 프로젝트** 엔탕 클리크 **만들기**.

![데모](./images/prmenu1.png)

Você verá um projeto vazio.

![데모](./images/premptyprojects.png)

Primeiro , certificate-se de selecionar a Visualização de dados correta no canto superior direito da tela. Neste 예제, a Visualização de dados a ser selecionada é `vangeluwe - Omnichannel Data View`.

![데모](./images/prdv.png)

Em seguida, você irá salvar seu projeto e dar um nome a ele. Você pode usar o seguinte comando para salvar:

| OS | 지름길 |
| ----------------- |-------------| 
| Windows | Control + S |
| Mac | Command+S |

보체 베라 에스테 팝업:

![데모](./images/prsave.png)

Use esta modelo de nomenclatura:

| 이름 | 설명 |
| ----------------- |-------------| 
| `yourLastName - Omnichannel Analysis` | `yourLastName - Omnichannel Analysis` |

Em seguida, clique em **저장**.

![데모](./images/prsave2.png)

## 4.4.2 메트리카스

Embora tenhamos organizado todos os components na Visualização de dados, você ainda deve adaptar alguns deles para que os usuários de negócios estejam prontos para iniciar suas análises. Além disso, durante qualquer processo de analytics, você pode criar métricas calculardas para aprofundar a descoberta de insights.

Como orimo, criaremos uma Taxa de conversão calcullada usando a métrica/evento Compras que definimos na Visualização de dados.

## 상트베르상 분류군

Vamos começar a abrir o construtor de métricas calculladas. 클리크 **+** 파라 크리아 수아 프리메이라 Métrica calcullada no Analysis Workspace.

![데모](./images/pradd.png)

O **계산된 지표 빌더에서 계산된 지표를 작성합니다** 이라 아파레커:

![데모](./images/prbuilder.png)

엔컨트 **구매** no menu do lado esquerdo. Em **지표** 클리크 **모두 표시**

![데모](./images/calcbuildercr1.png)

Agora arraste e solte a métrica **구매** 나 디피니상 다 메트리카 캘커라다.

![데모](./images/calcbuildercr2.png)

노르말멘테, 탁사 데 콘베르상 지니피카 **전환 / 세션**. Então, vamos fazer o mesmo cálculo na tela de definição de métrica calcullada. 메르트리카 앙트레 **세션** e arraste e solte-a no criador de definição, no evento **구매**.

![데모](./images/calcbuildercr3.png)

que o operador de divisão é selecionado automticamente를 관찰하십시오.

![데모](./images/calcbuildercr4.png)

탁사 드 conversão é comumente 대표 em porcentagem. Então, vamos mudar o formato para porcentagem e selectionar 2 casas decimis.

![데모](./images/calcbuildercr5.png)

마지막으로 계산된 지표의 이름 및 설명을 변경합니다.

| Title | 설명 |
| ----------------- |-------------| 
| 전환율 | 전환율 |

Por fim, altere o nome e a descrição da métrica calcullada:

![데모](./images/calcbuildercr6.png)

나우세에스케사 지 **살바르** 메트리카 캘커다.

![데모](./images/pr9.png)

## 4.4.3 Dimensões calculladas: Filtros (segmentação) e intervalos de datas

### 필터: Dimensões calculladas

Os cálculos não devem ser apenas para métricas. Antes de iniciar qualquer análise , também é interesante criar algumas **계산된 Dimension**. 중요하고, 에센시알멘테 **세그먼트** Adobe Analytics 없음. Customer Journey Analytics 없음, segmentos são chamados de **필터**.

![데모](./images/prfilters.png)

A criação de filtros ajudará os usuários de negócios a iniciar o analytics com algumas dimensões calculladas valiosas. Isso irá automatisar algumas tarefas, além de ajudar na parte de adoção. Abaixo estão alguns 예시:

1. 미디아 프로프리아, 미디아 파가와
2. Visitas novas x recorrentes
3. Clientes com carrinho abandonado

Esses filtros podem ser criados antes ou durante a parte de análise (o que você fará no próximo exercício).

### Intervalos de datas: Dimensões de tempo calculatas

As dimensões de tempo são outro tipo de dimensões calculladas. Alguns já foram criados, mas você também pode criar suas próprias Dimensões de tempo personalizadas na fase de preparação de dados.

Essas Dimensões de tempo de calcullado ajudarão analistas e usuários de negócios a lembrar datas importantes e usá-las para filtrar e alterar o o tempo de relatório. Perguntas e dúvidas típicas quando fazemos análiss :

- Quando foi a Black Friday do ano passado? Enter os dias 21 e 29?
- Quando veiculamos aquela campanha de TV em dezembro?
- De quando a quando fizemos as vendas de verão de 2018? Quero comparar com 2019. A proposito, você sabe os dias exatos em 2019?

![데모](./images/timedimensions.png)

Agora você concluiu o exercício de preparação de dados usando Analysis Workspace do CJA.

프록시마 에타파: [4.5 Visualização usando Customer Journey Analytics](./ex5.md)

[레토르나르 파라 플루소 데 우수아리오 4](./uc4.md)

[레토르나르 파라 토도스](./../../overview.md)
