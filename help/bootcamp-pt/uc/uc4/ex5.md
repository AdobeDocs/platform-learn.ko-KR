---
title: Bootcamp - Customer Journey Analytics - Customer Journey Analytics을 사용한 시각화 - 브라질
description: Bootcamp - Customer Journey Analytics - Customer Journey Analytics을 사용한 시각화 - 브라질
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Visualizations
exl-id: eb5eac54-22d8-428b-acac-16570f75085e
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 0%

---

# 4.5 Visualização usando o Customer Journey Analytics

## Objetivos

- Entenda a UI do Analysis Workspace
- Conheça alguns recursos que tornam o Analysis Workspace tão diferente.
- Aprenda a analisar no CJA usando o Analysis Workspace

## Contexto

Neste exercício, você usará o Analysis Workspace no CJA para analisar visualizações de produdutos, funis de produdutos, rotatividade 등

Vamos usar o projeto que você criou em [4.4 Preparação de dados no Analysis Workspace](./ex4.md), então acesse [https://analytics.adobe.com](https://analytics.adobe.com).

![데모](./images/prohome.png)

Abra seu 프로젝트 `yourLastName - Omnichannel Analysis`.

Com seu projeto aberto e Visualização de dados `yourLastName - Omnichannel Analysis` selectionado, você está pronto para começar a construir suas primeiras visualizações.

![데모](./images/prodataView1.png)

## Quantas visualizações de produdutos temos diariamente?

Em primeiro lugar, precisamos seleionar as datas certas para analisar os dados. Accesse o menu suspenso do calendário no lado direito da tela. Clique nele e selecione o intervalo de datas aplicável.

>[!IMPORTANT]
>
>**이번 주** **이번 달**&#x200B;에 um intervalo de datas como를 선택하십시오. Os dados disponíveis mais recentes foram absorvidos em 19 de setembro de 2022.

![데모](./images/pro1.png)
메뉴는 lado esquerdo(area de componentes)가 아니며, métricas calculladas **제품 보기**&#x200B;로 입력됩니다. Selecione-as e arraste e solte na tela, no canto superior direito da tabela de forma livre.

![데모](./images/pro2.png)

Automticamente a dimension **Day** será adicionada para criar sua primeira tabela. Agora você pode ver sua pergunta respondida imediatamente.

![데모](./images/pro3.png)

Em seguida, clique com o botão direito do mouse no resumo da métrica.

![데모](./images/pro4.png)

**시각화**&#x200B;를 클릭하여 **라인** 코모 시각화 대상을 선택합니다.

![데모](./images/pro5.png)

Você verá as suas visualizações de produto por dia.

![데모](./images/pro6.png)

Você pode alterar o escopo de tempo para o dia clicando em **설정** na visualização.

![데모](./images/pro7.png)

**데이터 Source 관리**&#x200B;에서 no ponto ao lado de **Line**&#x200B;을(를) 클릭합니다.

![데모](./images/pro7a.png)

Em seguida, clique em **선택 잠금** e selectione **선택한 항목** para bloquear esta visualização para que ela sempre exiba uma linha do tempo de Visualizações de produdutos.

![데모](./images/pro7b.png)

## 5 제품 mais visos

Quais são os 5 제품 mais vistos?

Lembre-se de salvar o project de tempos em.

| OS | 지름길 |
| ----------------- |-------------| 
| Windows | Control + S |
| Mac | Command+S |

Vamos começar a encontrar os 5 제품 mais visos. No menu do lado esquerdo, encontre o nome do produto - Dimensão.

![데모](./images/pro8.png)

Agora 배열 전자 메일 **제품 이름** 파라 대체 차원 **일**:

Este será o resultado.

![데모](./images/pro10a.png)

Em seguida, tente dividir um dos produdutos por Nome da marca. Pesquise **brandName** e arraste para baixo do primeiro nome do product.

![데모](./images/pro13.png)

Em seguida, faça um detalhamento usando o Agente de usuário. **사용자 에이전트**&#x200B;을(를) 사용합니다.

![데모](./images/pro15.png)

Em seguida, será exibida a tela abaixo :

![데모](./images/pro15a.png)

Por fim, você pode adicionar mais visualizações. Lado esquerdo, em visualizações, pesquise `Donut`이(가) 없습니다. 페그 `Donut`, arraste e solte na tela sob a visualização **Line** 

![데모](./images/pro18.png)

그런 다음 표에서 **Google Pixel XL 32GB Black Smartphone** > **Citi Signal**&#x200B;에서 수행한 분류에서 처음 5개의 **사용자 에이전트** 행을 선택합니다. 5개 행을 선택하는 동안 **CTRL** 단추(Windows의 경우) 또는 **Command** 단추(Mac의 경우)를 누릅니다.

Em seguida, na Tabela, selectione as primeiras 5 linhas de **사용자 에이전트** do detalhamento que fizemos em **Google 픽셀 XL 32GB 블랙 스마트폰** > **시티 신호**. Ao selectionar as 5 linhas, segure o botão **CTRL**(Windows 없음) ou o botão **Command**(Mac 없음).

![데모](./images/pro20.png)

Você verá o gráfico de donut alterado:

![데모](./images/pro21.png)

Você pode até adaptar o design para mais legível, tornando o gráfico de **Line** e o gráfico de **도넛** um pouco menor para que sejam exibidos lado a lado:

![데모](./images/pro22.png)

No ponto ao lado de *Donut** para **데이터 Source 관리**&#x200B;를 클릭합니다. Em seguida, clique em **Lock Selection** para bloquear essa visualização para que ela sempre exiba uma linha do tempo de Visualizações de product.

![데모](./images/pro22b.png)

Saiba mais sobre visualizações usando o Analysis Workspace em:

- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html)
- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html)

## Funil de interação do produto, da visualização à compra

Existem muitas formats de resolver esta questão. Uma delas é usar o Tipo de Interação de Produto e usá-lo em uma tabela de formato livre. Outra forma é uma **폴아웃 시각화**. Vamos usar o ultimo, pois queremos visualizar e analisar ao mesmo tempo.

페니엘 진부한 아쿠아:

![데모](./images/pro23.png)

Agora adicione um novo painel em branco clicando em **+ 빈 패널 추가**.

![데모](./images/pro24.png)

Clique na visualização de **폴아웃**.

![데모](./images/pro25.png)

메즈모 인터발로 데 다타스 중 하나를 고르면 전방을 연습할 수 있다.

![데모](./images/prodatef.png)

Em seguida, você verá:

![데모](./images/prodatefa.png)

**이벤트 유형** 차원을 제어하십시오. 구성 요소가 lado esquerdo에 없습니다.

![데모](./images/pro26.png)

Clique na seta para abrir a dimensão:

![데모](./images/pro27.png)

Você verá todos os Tipos de eventos disponíveis.

![데모](./images/pro28.png)

**commerce.productViews** 항목을 선택하십시오. e-solte-o campo **터치포인트 추가** dentro da **폴아웃 시각화**.

![데모](./images/pro29.png)

Faça o mesmo com **commerce.productListAdds** 및 **commerce.purchases** e solte-os no campo **터치포인트 추가** dentro da **폴아웃 시각화**. Sua visualização agora deve ser semelhante ao seguinte:

![데모](./images/props1.png)

Você pode fazer muitas coisas aqui. Alguns 예시 : comparar cada passo por dispositivo 비교 por fidelidade. No entanto, se quisermos analisar coisas interesantes como porque os clientes não compram depois de adicionar um item ao carrinho, podemos usar a melhor ferramenta do CJA: clicar com o botão direito.

터치포인트 **commerce.productListAdds**&#x200B;에 마우스를 가져다 대세요. Em seguida, 이 터치포인트에서 **분류 폴아웃**&#x200B;을 클릭합니다.

![데모](./images/pro32.png)

Uma nova tabela de formato livre será criada para analisar o que as pesoas fizeram se não compararam.

![데모](./images/pro33.png)

**페이지 이름**&#x200B;에 의한 **이벤트 유형**, nova tabela de formato livre, para ver em quais páginas eles estão indo, em vez da Página de confirmmação de compra.

![데모](./images/pro34.png)

## O que as pesoas fazem no site antes de sessar a página Cancelar serviço?

Novamente, há muitas formats de realizar essa análise. Vamos usar a análise de fluxo para iniciar parte da descoberta.

페니엘 진부한 아쿠아:

![데모](./images/pro0.png)

Agora adicione um novo painel em branco clicando em **+ 빈 패널 추가**.

![데모](./images/pro0a.png)

Clique na visualização **흐름**.

![데모](./images/pro35.png)

Em seguida, será exibido:

![데모](./images/pro351.png)

메즈모 인터발로 데 다타스 중 하나를 고르면 전방을 연습할 수 있다.

![데모](./images/pro0b.png)

**페이지 이름** 차원을 제어하십시오. 구성 요소가 lado esquerdo에 없습니다.

![데모](./images/pro36.png)

Clique na seta para abrir a dimensão:

![데모](./images/pro37.png)

파기나스 비스타로서 보테 엔콘트라라 토다스. Nome da página를 시작합니다. **서비스 취소**.
Arraste e solte **서비스 취소** na Visualização de fluxo no campo do media:

![데모](./images/pro38.png)

Em seguida, será exibido:

![데모](./images/pro40.png)

Vamos agora analisar se os clientes que visitaram a página C **서비스 취소** no site também ligaram para o call center e qual foi o resultado.

Nas dimension, retorne e encontre Tipo de interação de chamada. Arraste e solte **통화 상호 작용 유형** para 대체는 primeira interação à direita em **흐름 시각화**.

![데모](./images/pro43.png)

Agora você visualiza o ticket de suporte dos clientes que ligaram para a central de atendimento depois de visitar a página **Cancel Service**.

![데모](./images/pro44.png)

Em seguida, nas 차원, procuure **Call Feeling**. Arraste e solte para substitiir a primeira interação à direita na visualização de fluxo.

![데모](./images/pro46.png)

Em seguida, será exibido:

![데모](./images/flow.png)

Como pode ver, executamos uma análise omnichannel usando a visualização de fluxo. Graças a isso, descobrimos que alguns clientes que estavam pensando em cancelar o serviço tiveram uma avaliação positiva depois de ligar para o 콜 센터. Talvez tenhamos mudado de ideia com uma promoção?

## Qual é o desempenho dos clientes com um contato de 콜 센터 Positivo em relação aos principais KPIs?

Primeiramente, vamos segmentar os dados para obter apenas usuários com chamadas **positive**. CJA는 없습니다. Segmentos são chamados de Filtros. Accesse para filtros na área de components (no lado esquerdo) e clique em **+**.

![데모](./images/pro58.png)

Dentro do Constructor de filtro, dê um nome ao filtro

| 이름 | 설명 |
| ----------------- |-------------| 
| 통화 느낌 - 긍정적 | 통화 느낌 - 긍정적 |

![데모](./images/pro47.png)

Nos components (dentro do Constructor de filtro), encontre **Call Feeling** e arraste e solte na Definição do constructor de filtro.

![데모](./images/pro48.png)

Agora selectione **positive** como valor para o or filtro.

![데모](./images/pro49.png)

**사람**&#x200B;에 대한 추가 인원입니다.

![데모](./images/pro50.png)

Para finalizar, bsta clicar em **저장**.

![데모](./images/pro51.png)

엔탕, 보체 이라 레토르나르 파라 텔라 세아이다나오 레토르누, 페체오 페넬 전방향

![데모](./images/pro0c.png)

Agora adicione um novo painel em branco clicando em **+ 빈 패널 추가**.

![데모](./images/pro24c.png)

메즈모 인터발로 데 다타스 중 하나를 고르면 전방을 연습할 수 있다.

![데모](./images/pro24d.png)

**자유 형식 테이블**&#x200B;을 클릭합니다.

![데모](./images/pro52.png)

Agora arraste e solte o filtro que você acabou de criar.

![데모](./images/pro53.png)

호라 데 아디치오나 알구마스 메트리카스 Copece com **제품 보기** Arraste e solte na tabela de forma livre. 메트리카 **이벤트**&#x200B;에서 제외된 Vocée também pode입니다.

![데모](./images/pro54.png)

Mesmo com **사용자**, **장바구니에 추가** e **구매**&#x200B;의 Faça 또는 Mesmo com. Você vai acabar com uma tabela como a seguinte.

![데모](./images/pro55.png)

Graças à primeira análise de fluxo, uma nova pergunta surgiu. Então decidimos cria esta tabela e verificar alguns KPIs em um segmento para responder a essa pergunta. Como você pode ver, o tempo de insight é muito mais rápido do que usar SQL ou usar outtras soluções de BI.

## Recapitulação do Analysis Workspace e do Customer Journey Analytics

O Analysis Workspace limitações típicas de um relatório do Analytics로 todas를 제거합니다. Ele fornece uma tela robusta e flexível para criar project de analytics personalizados. Arraste e solte qualquer número de tabelas de dados, visualizações e componentes (dimensões, métricas, segmentos e granularidades de tempo) para um projeto. Você pode criar de forma de forma instantânea filtros e analises, gráficos de coorte, alertas, segmentos, análises de fluxo e relatórios de curadoria e agendamento para compartilhar com qualquer pessoa em seu negócio.

Próxima etapa: [4.6 De insights a ação](./ex6.md)

[레토르나르 파라 플루소 데 우수아리오 4](./uc4.md)

[레토르나르 파라 토도스](./../../overview.md)
