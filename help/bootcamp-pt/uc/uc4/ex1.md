---
title: 부트캠프 - Customer Journey Analytics - Customer Journey Analytics 101 - 브라질
description: 부트캠프 - Customer Journey Analytics - Customer Journey Analytics 101 - 브라질
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
exl-id: 63933d9e-b774-483f-b547-188c77440595
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# 4.1 Customer Journey Analytics 101

## Objetivos

- 엔텐다 오 케 에 오 CJA
- Entenda qual é o papel do CJA
- Entenda o workflow do CJA: da conexão de dados aos insights

## 4.1.1 O que é o Customer Journey Analytics?

O Customer Journey Analytics (CJA) fornece uma 인터페이스 em que os times de Analytics, Negócios e Tecnologia conseguem unir todos os dados da companhia e analisar a jornada cross-channel (online e offline) do cliente de ponta a ponta. O CJA é capaz de fornecer contexto e clareza para essa jornada, trazendo uma visão acionável em cima das dificuldades no processo de conversão e possibilitando o planejamento de experiências relevantes e personalizadas nos pontos mais relevantes.

O CJA traz o Analysis Workspace conectado à Adobe Experience Platform. A Adobe Experience Platform é o cérebro da comunicação e da orquestração e, com o CJA, as marcas agora podem contextualizar e visualizar todos seses dados, para que as equipes de negócios e insights possam aprender com eles, analisando toda a jornada on-line para off-line do cliente.

As equipes de negócios e insights podem conversar com o CJA, fazer perguntas e obter respoas em tempo real com a interface do usuário de arrastar e soltar, apontar e clicar e fácil de usar do Analysis Workspace.

![데모](./images/cja-adv-analysis1.png)

## 4.1.2 Principais vantagens

Os três principais beneficios para os clientes são:

- A capacidade de disponibilizar insights para todos (ou seja, democratizar o acesso aos dados).
- A capacidade de de ver o cliente em uma jornada contextual (ou seja, os dados podem ser visualizados sequencialmente, abrangendo múltiplos canais on-line e off-line).
- A capacidade de de aproveitar o poder dos dados sem que haja a necessidade (ou seja, permite que indivíduos usm dados para desbloquear insights e análises profundas para ativação de marketing).

## 4.1.3 ## 4.1.3 Por que escoler o Customer Journey Analytics?

O CJA não se destina a substicir um aplicativo de BI atual, como Power BI, Microstrategy, Locker ou Tableau. O objetivo deses aplicativos de BI é visualizar dados para criar painéis corporativos para que todos em uma organização possam ver métricas importantes rapidamente. O objetivo do CJA é trazer poder de análise para as equipes de Marketing e Negócios, tornando-o uma ferramenta de análise obrigatória para essas pessoas



Tradicionalmente, os aplicativos de BI têm sido incapazes de permitur a verdadeira inteligência do cliente:

- Eles não podem fazer atribuição e não fazem análises de jornada do cliente.
- Os aplicativos de BI precisam saber a pergunta com antecedência
- As consultas interativas são limitadas pela estrutura do banco de dados
- 하빌리다데스 데 상에니까리아스
- Os aplicativos de BI não permitem você pergunte o motivo de um acontecimento.
- Os aplicativos de BI não têm conexão direta com os pontos de contato do cliente.

Portanto , usuários de negócios e analistas chegam a becos sem saída quase imediatamente, tornando a análise cara, lenta, infilexível e desconectada dos sisemas de ação.

Com o CJA você pode ter uma visão competa da jornada do cliente, usando dados offline e online, com as ferramantas certas para reduzir o tempo de insight, tornando os usários de negócios independentes para entender por que algo aconteceu e como responder a isso.

![데모](./images/cja-use-case.png)

## 4.1.4 Comprenda o fluxo de trabalho do Customer Journey Analytics

Antes de iniciar os próximos exercícios, é essential compreender quais etapas são necessárias para trazer dados da Adobe Experience Platform para o CJA para visualizá-los e obter alguns insights profundos. É o que chamamos de fluxo de trabalho do CJA. Vamos 유효성 검사:

![데모](./images/cja-work-flow.jpg)

Antes de iniciar as etapas acima, não se equeça da etapa 0, que é compreender os dados que estão disponíveis na Adobe Experience Platform.

**쓰레기가 들어오면, 쓰레기가 나와요.** Você deve ter uma ideia clara de quais dados estão disponíveis e como os esquemas na Adobe Experience Platform são configurados. Compreender os dados que estão na Adobe Experience Platform facilitará as coisas, não só na parte de conexão de dados, mas também na hora de construir visualizações e fazer análiss.

## 4.1.5 Etapa 0: Compreender esquemas e dataset da Adobe Experience Platform

Adobe Experience Platform에 대한 URL 로그인: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer 로그인, você irá acesssar a página inicial da Adobe Experience Platform.

![데이터 수집](../uc1/images/home.png)

Antes de continar, você precisa selecionar um **샌드박스**. 샌드박스 a ser selectionado é ``Bootcamp``. 보테 포데 파제 이소 클리칸도 노 이콘 **[!UICONTROL Prod]** 칸토 수페리어 디레이토 다 텔라. Depois de seleionar o sandbox adopriado, você verá a tela mudando e agora você está em seu sandbox dedicado.

![데이터 수집](../uc1/images/sb1.png)

Adobe Experience Platform에서 스키마 e 데이터 세트를 확인합니다.

| 데이터 세트 | 스키마 |
| ----------------- |-------------| 
| 데모 시스템 - 웹 사이트에 대한 이벤트 데이터 세트(전역 v1.1) | 데모 시스템 - 웹 사이트에 대한 이벤트 스키마(전역 v1.1) |
| 데모 시스템 - 콜 센터용 이벤트 데이터 세트(글로벌 v1.1) | 데모 시스템 - 콜 센터용 이벤트 스키마(글로벌 v1.1) |
| 데모 시스템 - Voice Assistant용 이벤트 데이터 세트(글로벌 v1.1) | 데모 시스템 - Voice Assistant용 이벤트 스키마(전역 v1.1) |

Certifique-se de ter verificado ao menos:

- 식별자: CRMID, 전화번호, ECID, 이메일. Quais identities são os identificadores primários, quais são os identificadores secundários?

Você pode encontrar os identificadores abrindo um schema e observando o objeto `_experienceplatform.identification.core`. 스키마 확인 [데모 시스템 - 웹 사이트에 대한 이벤트 스키마(전역 v1.1)](https://experience.adobe.com/platform/schema).

![데모](./images/identity.png)

- Objeto de comércio dentro do schema 살펴보기 [데모 시스템 - 웹 사이트에 대한 이벤트 스키마(전역 v1.1)](https://experience.adobe.com/platform/schema).

![데모](./images/commerce.png)

- 할 일 시각화 [데이터 세트](https://experience.adobe.com/platform/dataset/browse?limit=50&amp;page=1&amp;sortDescending=1&amp;sortField=created) e verifique os dados

Agora você está pronto para começar a usar a interface do usuário do Customer Journey Analytics.

프록시마 에타파: [4.2 데이터 세트 연결 da Adobe Experience Platform Customer Journey Analytics 없음](./ex2.md)

[레토르나르 파라 플루소 데 우수아리오 4](./uc4.md)

[레토르나르 파라 토도스](../../overview.md)
