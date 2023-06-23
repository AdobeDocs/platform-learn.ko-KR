---
title: Bootcamp - Customer Journey Analytics - Customer Journey Analytics에서 Adobe Experience Platform 데이터 세트 연결 - 브라질
description: Bootcamp - Customer Journey Analytics - Customer Journey Analytics에서 Adobe Experience Platform 데이터 세트 연결 - 브라질
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 51078fca-f234-4e50-96ba-ee7f5e286869
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 2%

---

# 4.2 데이터 세트 연결 da Adobe Experience Platform Customer Journey Analytics 없음

## Objetivos

- Compreenda a UI da conexão de dados
- Traga os dados da Adobe Experience Platform para o CJA
- Entenda a ID da pessoa e a compilação de dados
- Aprenda o conceito de streaming de dados no 고객 여정

## 4.2.1 코넥상

액세스 [analytics.adobe.com](https://analytics.adobe.com) para accesssar o Customer Journey Analytics.

Na página inicial do Customer Journey Analytics, Accesse **연결**.

![데모](./images/cja2.png)

Aqui você pode ver todas as diferences conexões feitas entre o CJA e a Plataforma. 에사스 코넥세 테임 오 메즈모 오브제티보 도스 콘훈투스 데 라투리오스 노 Adobe Analytics. No entanto, a coleta dos dados é compleetamente differente. Todos os dados vêm de dataset da Adobe Experience Platform.

Vamos criar sua primeira conexão. 클리크 **새 연결 만들기**.

![데모](./images/cja4.png)

보사이베라아 UI **연결 만들기** UI.

![데모](./images/cja5.png)

아고라 보치 포데 다르 움 노메 아 수아 코넥사오.

Use esta modelo de nomenclatura: `yourLastName – Omnichannel Data Connection`.

예제: `vangeluw - Omnichannel Data Connection`

Você também deve selecionar o sandbox correto para usar. 메뉴 샌드박스 없음, 샌드박스 하나 선택, 개발자 버전 `Bootcamp`. Neste modeo, o sandbox a ser usado é o **부트캠프**. E você também deve definir o **일일 평균 이벤트 수** 끝 **백만 미만**.

![데모](./images/cjasb.png)

Após seleionar seu sandbox, você pode começar a adicionar dataset a esta conexão. 클리크 **데이터 세트 추가**.

![데모](./images/cjasb1.png)

## 4.2.2 Adobe Experience Platform 데이터 세트 선택

데이터 세트 페스퀴즈 `Demo System - Event Dataset for Website (Global v1.1)`. 클리크 **+** para adicionar o dataset a esta conexão.

![데모](./images/cja7.png)

아고라 페스키에 마르크 as caixas de seleção `Demo System - Event Dataset for Voice Assistants (Global v1.1)` 및 `Demo System - Event Dataset for Call Center (Global v1.1)`.

Em seguida, você verá a tela abaixo. 클리크 **다음**.

![데모](./images/cja9.png)

## 4.2.3 ID da pessoa e compilação de dados

### ID 다 페소

O objetivo agora é juntar sites 데이터 세트. Para cada dataset seleionado, você verá um campo chamado **개인 ID**. Cada dataset tem seu próprio campo de ID de pessoa.

![데모](./images/cja11.png)

Como você pode ver, a maioria deles tem o ID da pessoa selecionado automticamente. Isso ocorre porque um identificador principal é seleionado em cada esquema na Adobe Experience Platform. Como 모형, aqui está o esquema para `Demo System - Event Schema for Call Center (Global v1.1)`, onde você pode ver que o Identificador Primário está definido como `phoneNumber`.

![데모](./images/cja13.png)

No entanto, você ainda pode influenciar qual identificador será usado para compilar datases para sua conexão. Você pode usar qualquer identificador configurado no esquema vinculado ao seu 데이터 세트. 메뉴 없음 suspenso para explorar os ID disvoníveis em cada 데이터 세트를 클릭합니다.

![데모](./images/cja14.png)

Conforme mencionado, você pode definir ID de pesoa para cada 데이터 세트. Isso permite reunir CJA에서 데이터 세트를 다른 múltiplas origens. Imagine trazer NPS ou dados de pesquisa que seram muito interessantes e úteis para comprender o contexto e o motivo de um acontecimento.

오 nome do campo ID da pessoa não é importante, desde que o valor nos campos ID da pessoa corresponda. 디가모스 케 테모스 `email` em um 데이터 세트 e `emailAddress` em outro 데이터 세트 definido como ID da pessoa. Se `delaigle@adobe.com` tiver o mesmo valor para o campo ID da pesoa em ambos os dataset, o CJA poderá compilar os dados.

Atualmente, existem algumas outtras limitações, como compilar o comportamento anônimo para conheido. Pergentas 자주 aqui로 컨설팅: [FAQ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html?lang=ko-KR).


### Compilando os dados usando o o ID da pessoa

Agora que você comprende o conceito de compilar dataset usando o ID da pesoa, vamos escoler `email` como ID da pesoa para cada 데이터 세트.

![데모](./images/cja15.png)

ID da pessoa에 대한 cada 데이터 세트 para autoalizar.

![데모](./images/cja12a.png)

Agora preencha o campo ID da pessoa escolendo o `email` 나 리스타 서스펜사

![데모](./images/cja17.png)

Depois de compilar os três dataset, estamos prontos para continuar.

| 데이터 세트 | 개인 ID |
| ----------------- |-------------| 
| 데모 시스템 - 웹 사이트에 대한 이벤트 데이터 세트(전역 v1.1) | 이메일 |
| 데모 시스템 - Voice Assistant용 이벤트 데이터 세트(글로벌 v1.1) | 이메일 |
| 데모 시스템 - 콜 센터용 이벤트 데이터 세트(글로벌 v1.1) | 이메일 |

Você também precisa garantir que , para cada dataset , essas opções estejam habilitadas :

- Importar todos os novos dados
- Preencher todos os ados existentes
- Preencher tipo de fonte de dados com &quot;기타&quot;
- Preencher a descrição com o mesmo nome do 데이터 세트

클리크 **데이터 세트 추가**.

![데모](./images/cja16.png)

클리크 **저장** 파라 오 프록시모 엑세시치오 데포아 드 크랴르 수아 **연결**, pode levar algumas horas até que seus dados estejam disponíveis no CJA.

![데모](./images/cja20.png)

프록시마 에타파: [4.3 Crie uma Visualização de Dados](./ex3.md)

[레토르나르 파라 플루소 데 우수아리오 4](./uc4.md)

[레토르나르 파라 토도스](./../../overview.md)
