---
title: 부트캠프 - Customer Journey Analytics - 데이터 보기 만들기 - 브라질
description: Customer Journey Analytics - 데이터 보기 만들기 - 브라질
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 8cfd4467-167d-4235-a305-4596e3a7d4fb
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '1655'
ht-degree: 2%

---

# 4.3 Crie uma Visualização de Dados

## Objetivos

- Entenda a UI de Visualização de Dados
- Compreenda as configurações básicas de definição de visita
- Compreenda a a atribuição e a Persistência em uma 시각화

## 4.3.1 Visualização de Dados

Agora, com sua conexão concluída, é posível progredir para influenciar a visualização. Uma differença entre o Adobe Analytics e o CJA é que o CJA precisa de uma visualização de dados para limpar e preparar os dados antes da visualização.

Uma Visualização de Dados é semelhante ao conceito de 가상 보고서 세트 no Adobe Analytics, onde você estabelecee as definições de visita com reconheciimento de contexto, filtragem e também como os components são chamados.

Será neceário, no mynimo, uma Visualização de Dados por conexão. No entanto, para alguns casos de uso, é ótimo ter múltiplas Visualizações de Dados para mesma conexão, com o objetivo de fornecer insights para equipes diffintas. Se você deseja que sua empresa seja orientada por dados, deve adaptar a forma como os dados são visos em cada equipe. 알고리즘 예시:

- Métricas de UX apenas para equipe de UX 디자인
- 사용 os mesmos nomes para KPIs e metricas para o Google Analytics e para o Customer Journey Analytics, para que a equipe de análise digital fale apenas 1 idioma.
- Visualização de Dados filtrada para mostrar, por orimo, dados para apenas um mercado, ou uma marca, ou apenas para Dispositivos móveis.

나텔라 데 **연결** 마르케 아 카이사 드 셀레상 다 코넥상 케 보슈 아카보 드 크리아르. 클리크  **데이터 보기 만들기**.

![데모](./images/exta.png)

Você será redirectionado para o fluxo de trabalho **데이터 보기 만들기** 워크플로입니다.

![데모](./images/0-v2.png)

## 4.3.2 Definição de Visualização de Dados

Agora você pode configurar as definições básicas para sua Visualização de dados.

![데모](./images/0-v2.png)

A **연결** 케 보테 크리우 노 exercício 전각 já está selectionada. 수아 코넥상 세 차마 `yourLastName – Omnichannel Data Connection`.

![데모](./images/ext5.png)

Em seguida, dê um nome à sua 시각화 Ação de Dados seguindo este 모델 de nomenclatura: `yourLastName – Omnichannel Data View`.

Insira o mesmo valor para a 설명: `yourLastName – Omnichannel Data View`.

| 이름 | 설명 |
| ----------------- |-------------| 
| `yourLastName – Omnichannel Data View` | `yourLastName – Omnichannel Data View` |

![데모](./images/1-v2.png)

파라 **시간대**, 후소 호라리오 선택 **Berlim, Estocolmo, Roma, Berna, Bruxelas, Viena, 암스테르담 GMT+01:00**. Este um cenário realmente interest, pois algumas empresas operam em differents países e geografias. Alocar o fuso horário certo para cada país evitará erros típicos de dados, como, por orimo, acreditar que a maioria das pesoas combra camisetas às 4h no Peru.

![데모](./images/ext7.png)

Você também pode modificar a nomenclatura das métricas principais (Pessoa, Sessão e Evento). Isso não é obrigatório, mas alguns clientes gostam de usar Pesoas, Visitas e Acessos em vez de Pessoa, Sesão e Eventos (convenção de nomenclatura padrão do Customer Journey Analytics).

Agora você deve ter as seguintes configuraões definidas:

![데모](./images/1-v2.png)

클리크 **저장 및 계속**.

![데모](./images/12-v2.png)

## 4.3.3 Components da Visualização de Dados

Neste exercício, você irá configurar os components necessários para analisar os dados e visualizá-los usando o Analysis Workspace. Nesta IU, há três áreas principais :

- Lado esquerdo: Components disponíveis dos dataset selectionados
- 미디어: Components adicioneados à Visualização de Dados
- Lado direito: Configurações do componente

![데모](./images/2-v2.png)

>[!IMPORTANT]
>
>Se você não encontrar uma métrica ou dimensão esecífica, verifique se o campo `Contains data` foi removido de sua visualização de dados. 카소 콘트라리오, 에세 캄포
>
>![데모](./images/2-v2a.png)

Agora você precisa e soltar os components necessários para a análise nos **구성 요소 추가됨**. Para isso, você deve selecionar os components no menu à esquerda e arrastá-los e soltá-los na tela no meio.

Vamos começar com o primeiro 구성 요소 : **이름(web.webPageDetails.name)**. Pesquise esse componente arraste-o e solte-o na tela.

![데모](./images/3-v2.png)

Esse componente é o nome da página, como você pode derivar da leitura do campo do schema `(web.webPageDetails.name)`.

엔탄토 없음, usar **이름** como o nome não é a melhor conventção de nomenclatura para um usuário corporativo compreender rapidamente essa dimensão.

파모스 무다르 오놈 파라 **페이지 이름**. Clique no componente o renomeie na area **구성 요소 설정**.

![데모](./images/3-0-v2.png)

As Configurações de persistência 상 **지속성 설정**. Os conceitos de eVars e prop não existem no CJA, mas as configurações de Persistência possibilitam um comportamento semelhante.

![데모](./images/3-0-v21.png)

Se voche não alterar essas configurações, o CJA irá intertar a dimensão como um **Prop** (nível de ocorência). Além disso, podemos alterar a Persistência para tornar a dimensão uma **eVar** (페르시스터 오발루 아오 롱고 다 조르나다).

Se você não estiver familiarizado com eVars e Props, [라이아 마이스 소브레 이소 나 다큐멘타상](https://experienceleague.adobe.com/docs/analytics/landing/an-key-concepts.html)..

Vamos deixar o Nome da Página como Prop. 데사 포르마, 보체 낭 precisa alterar nenhuma **지속성 설정**.

| 검색할 구성 요소 이름 | 새 이름 | 지속성 설정 |
| ----------------- |-------------| --------------------| 
| 이름(web.webPageDetails.name) | 페이지 이름 |          |

Em seguida, escloha a dimensão **전화번호** 솔테나텔라 오노보놈 데브 세르 **전화 번호**.

![데모](./images/3-1-v2.png)

Por fim, vamos alterar as Configurações de persistência, pois o Número do Cellar deve persistir no nível do usuário.

Para alterar a Persistência, 역할 para baixo no menu à direita e abra a aba **지속성**:

![데모](./images/5-v2.png)

Marque a caixa de seleção para modificar as configurações de persistência. 선택 항목 **가장 최근** eo 에스코포 **개인(보고 기간)**, pois nos preocupamos apenas com o ultimo número de celular da pesoa. Se o cliente não preencher o celular em visitas futuras, você ainda verá esse valor preenchido.

![데모](./images/6-v2.png)

| 검색할 구성 요소 이름 | 새 이름 | 지속성 설정 |
| ----------------- |-------------| --------------------| 
| 전화번호 | 전화 번호 | 가장 최근, 개인(보고 기간) |

O próximo componente `web.webPageDetails.pageViews.value`.

메뉴 없음, 에스케르다, 페스키즈 `web.webPageDetails.pageViews.value`. Arraste e solte essa métrica na tela.

Altere o nome para **페이지 보기 수** 다음 아래에 **구성 요소 설정**.

| 검색할 구성 요소 이름 | 새 이름 | 속성 설정 |
| ----------------- |-------------| --------------------| 
| web.webPageDetails.pageViews.value | 페이지 보기 횟수 |         |

![데모](./images/7-v2.png)

Para as configurações de atribuição, deixaremos em branco.

Observação : As configurações de persistência nas métricas também podem ser alteradas no Analysis Workspace. Em alguns casos, você pode optar por configurá-las aqui para evitar que os usuários de negócios tenham que pensar qual é o melhor modelo de persistência.

Em seguida, você terá que configurar várias Dimensões Métricas, conforme indado na tabela abaixo.

### 디안수에스

| 검색할 구성 요소 이름 | 새 이름 | 지속성 설정 |
| ----------------- |-------------| --------------------| 
| brandName | 브랜드 이름 | 가장 최근, 세션 |
| 냉정감 | 콜감 |          |
| 호출 ID | 호출 상호 작용 유형 |          |
| callTopic | 통화 주제 | 가장 최근, 세션 |
| ecid | ECID | 가장 최근, 개인(보고 기간) |
| 이메일 | 이메일 ID | 가장 최근, 개인(보고 기간) |
| 결제 유형 | 결제 유형 |          |
| 제품 추가 메서드 | 제품 추가 메서드 | 가장 최근, 세션 |
| 이벤트 유형 | 이벤트 유형 |         |
| 이름(productListItems.name) | 제품 이름 |         |
| SKU | SKU(세션) | 가장 최근, 세션 |
| 거래 ID | 거래 ID |         |
| URL (web.webPageDetails.URL) | URL |         |
| 사용자 에이전트 | 사용자 에이전트 | 가장 최근, 세션 |

### 메트리카

| 검색할 구성 요소 이름 | 새 이름 | 속성 설정 |
| ----------------- |-------------| --------------------| 
| 수량 | 수량 |          |
| commerce.order.priceTotal | 매출  |         |

Sua configuração deve ser semelhante ao seguinte:

![데모](./images/11-v2.png)

Não se equeça de Salvar sua Visualização de Dados. 엔탕 클리케 **저장**.

![데모](./images/12-v2s.png)

## 4.3.4 메트리카스

Embora tenhamos organizado todos os components na Visualização de dados, você ainda deve adaptar alguns deles para que os usuários de negócios estejam prontos para iniciar suas análises.

Se você se lembra, não trouxemos especificamente Métricas como Adicionar ao Carrinho, Visualização do produto ou Compras para Visualização de dados. No entanto, temos uma dimensão chamada: **이벤트 유형**. Então, vamos derivar deses tipos de interação criando 3 métricas calculladas.

Vamos começar com a primeira Métrica : **제품 보기**.

No lado esquerdo, pequise **이벤트 유형** 차원을 선택합니다. Em seguida, arraste-o e solte-o na tela **포함된 구성 요소**.

![데모](./images/calcmetr1.png)

Clique para selecionar a nova métrica **이벤트 유형**.

![데모](./images/calcmetr2.png)

Agora altere o nome e a descrição do componente para os seguintes valores:

| 구성 요소 이름 | 구성 요소 설명 |
| ----------------- |-------------| 
| 제품 보기 | 제품 보기 |

![데모](./images/calcmetr3.png)

아고라 바모스 콘타 아페나스 **제품 보기**. Para fazer isso, 역할 para baixo em **구성 요소 설정** 아테 베르 발로레스 데 **포함/제외 값**. 하빌리타르 아 옵상 **포함/제외 값 설정**.

![데모](./images/calcmetr4.png)

코모 케레모스 콘타 아페나스 **제품 보기**, 특히 **commerce.productViews** 크리테리오스

![데모](./images/calcmetr5.png)

아고라 아 수아 메트리카 캘쿨라다 에스타 프로타!

Em seguida, repita o mesmo processo para os eventos **장바구니에 추가** e **구매**.

### 장바구니에 추가

Primeiro, arraste a mesma dimensional **이벤트 유형**.

![데모](./images/calcmetr1.png)

Você verá um alerta pop-up de um Campo Duplicado, pois estamos usando a mesma variável. 클리크 **그대로 추가**:

![데모](./images/calcmetr6.png)

Agora, siga o mesmo processo que fizemos para a métrica Visualizações de product:
- Primeiro altere o nome e a descrição.
- Por fim, adicione **commerce.productListAdds** como critério para contar apenas 장바구니에 추가

| 이름 | 설명 | 기준 |
| ----------------- |-------------| -------------|
| 장바구니에 추가 | 장바구니에 추가 | commerce.productListAdds |

![데모](./images/calcmetr6a.png)

### 구매

Primeiro, arraste a mesma dimensional **이벤트 유형** 코모 fizemos para as duas métricas anteriores.

![데모](./images/calcmetr1.png)

Você verá um alerta pop-up de um Campo Duplicado, pois estamos usando a mesma variável. 클리크 **그대로 추가**:

![데모](./images/calcmetr7.png)

Agora, siga o mesmo processo que fizemos para as métricas 제품 보기 e 장바구니에 추가:
- Primeiro altere o nome e a descrição.
- Por fim, adicione **commerce.purchase** como critérios para contabilizar apenas as Compras

| 이름 | 설명 | 기준 |
| ----------------- |-------------| -------------|
| 구매 | 구매 | commerce.purchases |

![데모](./images/calcmetr7a.png)

Sua configuração final deve ser semelhante ao seguinte. 클리크 **저장 및 계속**.

![데모](./images/calcmetr8.png)

## 4.3.5 Components da Configuração de Dados

Você deve ser redirectionado para tela:

![데모](./images/8-v2.png)

Nesta aba, você pode modificar algumas configurações importantes para alterar a forma como os dados são processados. Vamos começar definindo o **세션 시간 초과** 코모 30분 Graças ao registro de data e hora de cada evento de experiência, você pode estender o conceito de uma sessão em todos os canais. Por formo, o que acontece se um cliente ligar para o call center depois de visitar o site? Usando Tempos Limite de Sesão personalizados, você tem muita flexibilidade para decisdir o que é uma sessão e como essão irá mesclar os dados.

![데모](./images/ext8.png)

Nesta aba você modificar outtras coisas como filtrar os dados usando um segmento/filtro. Você não precisará fazer isso neste exercício.

![데모](./images/10-v2.png)

Quando 터미널, 절벽 **저장 및 마침**.

![데모](./images/13-v2.png)

>[!NOTE]
>
>Você pode voltar a esta Visualização de dados posteriormente alterar as configuraçõe os componentes a qualquer momento. As alterações afetarão a forma como os dados históricos são mostrados.

Agora você pode continuar com a parte de visualização e análise!

프록시마 에타파: [4.4 Preparação de dados em Customer Journey Analytics](./ex4.md)

[레토르나르 파라 플루소 데 우수아리오 4](./uc4.md)

[레토르나르 파라 토도스](./../../overview.md)
