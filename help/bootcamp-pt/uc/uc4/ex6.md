---
title: Bootcamp - Customer Journey Analytics - 통찰력에서 행동까지 - 브라질
description: Bootcamp - Customer Journey Analytics - 통찰력에서 행동까지 - 브라질
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Audiences
exl-id: 28b87e21-3168-447e-9a93-a6ae7e969657
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# 4.6 도스 인사이트 아 아상

## Objetivos

- Entenda como criar um público com base em uma visão coletada no Customer Journey Analytics
- Use esse público no CDP em tempo real e no Adobe Journey Optimizer

## 4.6.1 Crie uma audyncia e publish-a

Em seu projeto, você criou um filtro chamado **감정 호출** e conseguiu visualizar a quantidade de usuários que tiveram suas ligações ao call center classificadas como **양성인**. Agora, você poderá criar um segmento com은 usuários e ativação-los em jornadas ou em canais de comunicação를 이용합니다.

O primeiro passo é: no painel criado no ultimo exercício, 선택 a linha **1. 통화 느낌 - 긍정적**, clique com o botão direito de seu mouse e selecione a opção **선택 항목에서 대상 만들기**:

![데모](./images/aud1.png)

Em seguida, dê um nome para a sua audyncia seguindo o modelo **yourLastName - cia 대상자 호출 긍정적 느낌**:

![데모](./images/aud2.png)

Note que é posível ter um preview da audyncia que está sendo criada:

![데모](./images/aud3.png)

Para finalizar, clique em **퍼블리카**:

![데모](./images/aud4.png)

## 4.6.2 Use sua audyncia como parte de um segmento

Voltando para a Adobe Experience Platform, vá em **세그먼트 > 찾아보기** e você conseguirá visualizar o seu segmento criado no CJA pronto e disponível para ser usado nas suas ativações jornadas!

![데모](./images/aud5.png)

Vamos agora usar esse segmento em uma ativação no Facebook e em uma jornada do cliente!

## 4.6.3 Use seu segmento na Real-Time CDP em tempo real

나 Adobe Experience Platform, vá em **세그먼트 > 찾아보기** 이 encontre a audiência que você criou no CJA:

![데모](./images/aud6.png)

Clique no seu segmento e, em seguida , clique em **대상에 활성화**:

![데모](./images/aud7.png)

목적지 선택 chamada bootcamp-facebook e, em seguida, 클릭 em Next:

![데모](./images/aud8.png)

Em seguida, clique em Next novamente:

![데모](./images/aud9.png)

옵상 셀시오네 **대상의 출처** e defina como **고객으로부터 직접** 다음 을 클릭합니다.

![데모](./images/aud10.png)

포르 핌, 나 파기나 **리뷰** 완료 를 클릭합니다.

![데모](./images/aud11.png)

프론토! Agora o seu segmento está vinculado aos públicos personalizados do Facebook.
아고라, AJO의 vamos utilizar esse segmento!

## 4.6.4 Adobe Journey Optimizer에서 seu segmento 사용

Na interface da Adobe Experience Platform clique em Journey Optimizer e, em seguida, no menu lateral esquerdo, clique em **여정** e comece a criar uma jornada clicando em **여정 만들기**:

![데모](./images/aud20.png)

![데모](./images/aud21.png)

![데모](./images/aud22.png)

Em seguida, no menu lateral esquerdo, em Eventos, selectione **세그먼트 선별** 이 아라스테와 아테 아 조나다:

![데모](./images/aud23.png)

Em 세구이다, em **세그먼트** 클리크 **편집** para selectionar um segmento:

![데모](./images/aud24.png)

Selecione a audiência que você criou no CJA e clique em **저장**:

![데모](./images/aud25.png)

프론토! A partir daí você pode criar uma jornada para clientes que se qualificam para esse segmento!

[사용자 흐름으로 돌아가기 4](./uc4.md)

[Voltar para todos 운영 체제](./../../overview.md)
