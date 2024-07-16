---
title: Bootcamp - Customer Journey Analytics - Customer Journey Analytics에서 Adobe Experience Platform 데이터 세트 연결 - 브라질
description: Bootcamp - Customer Journey Analytics - Customer Journey Analytics에서 Adobe Experience Platform 데이터 세트 연결 - 브라질
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Connections
exl-id: 51078fca-f234-4e50-96ba-ee7f5e286869
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# 4.2 데이터 세트 연결 da Adobe Experience Platform Customer Journey Analytics 없음

## Objetivos

- Compreenda a UI da conexão de dados
- Traga os dados da Adobe Experience Platform para o CJA
- Entenda a ID da pessoa e a compilação de dados
- Aprenda o conceito de streaming de dados no 고객 여정

## 4.2.1 코넥상

[analytics.adobe.com](https://analytics.adobe.com) para accessar 또는 Customer Journey Analytics에 액세스합니다.

Na Página 기본 Customer Journey Analytics 수행, **연결**&#x200B;에 액세스.

![데모](./images/cja2.png)

Aqui você pode ver todas as diferences conexões feitas entre o CJA e a Plataforma. 에사스 코넥세 테임 오 메즈모 오브제티보 도스 콘훈투스 데 라투리오스 노 Adobe Analytics. No entanto, a coleta dos dados é compleetamente differente. Todos os dados vêm de dataset da Adobe Experience Platform.

Vamos criar sua primeira conexão. **새 연결 만들기**&#x200B;를 클릭합니다.

![데모](./images/cja4.png)

Você verá a UI **연결 만들기** UI.

![데모](./images/cja5.png)

아고라 보치 포데 다르 움 노메 아 수아 코넥사오.

에스테 모델 de nomenclatura 사용: `yourLastName – Omnichannel Data Connection`.

예제: `vangeluw - Omnichannel Data Connection`

Você também deve selecionar o sandbox correto para usar. 메뉴 샌드박스가 없습니다. 메뉴 샌드박스를 하나 선택하십시오. `Bootcamp` 장치를 선택하십시오. **Bootcamp**&#x200B;에 사용자 usado é를 샌드박스로 만들려면 Neste 예제를 사용하십시오. E você também deve o **일일 평균 이벤트 수**&#x200B;부터 **백만 미만까지**&#x200B;입니다.

![데모](./images/cjasb.png)

Após seleionar seu sandbox, você pode começar a adicionar dataset a esta conexão. **데이터 세트 추가**&#x200B;를 클릭합니다.

![데모](./images/cjasb1.png)

## 4.2.2 Adobe Experience Platform 데이터 세트 선택

데이터 집합 `Demo System - Event Dataset for Website (Global v1.1)`에 대한 사전 요구 사항입니다. **+** para adicionar 또는 데이터 세트 a esta conexão를 클릭합니다.

![데모](./images/cja7.png)

`Demo System - Event Dataset for Voice Assistants (Global v1.1)` 및 `Demo System - Event Dataset for Call Center (Global v1.1)`(으)로 표시되는 Agora pesquise e marque입니다.

Em seguida, você verá a tela abaixo. **다음**&#x200B;을 클릭합니다.

![데모](./images/cja9.png)

## 4.2.3 ID da pessoa e compilação de dados

### ID 다 페소

O objetivo agora é juntar sites 데이터 세트. Para cada dataset seleionado, você verá um campo chamado **개인 ID**. Cada dataset tem seu próprio campo de ID de pessoa.

![데모](./images/cja11.png)

Como você pode ver, a maioria deles tem o ID da pessoa selecionado automticamente. Isso ocorre porque um identificador principal é seleionado em cada esquema na Adobe Experience Platform. Como orimo, aqui está o esquema para `Demo System - Event Schema for Call Center (Global v1.1)`, onde você pode ver que o Identificador Primário está definido como `phoneNumber`.

![데모](./images/cja13.png)

No entanto, você ainda pode influenciar qual identificador será usado para compilar datases para sua conexão. Você pode usar qualquer identificador configurado no esquema vinculado ao seu 데이터 세트. 메뉴 없음 suspenso para explorar os ID disvoníveis em cada 데이터 세트를 클릭합니다.

![데모](./images/cja14.png)

Conforme mencionado, você pode definir ID de pesoa para cada 데이터 세트. Isso permite reunir CJA에서 데이터 세트를 다른 múltiplas origens. Imagine trazer NPS ou dados de pesquisa que seram muito interessantes e úteis para comprender o contexto e o motivo de um acontecimento.

오 nome do campo ID da pessoa não é importante, desde que o valor nos campos ID da pessoa corresponda. Digamos que temos `email` em um 데이터 세트 e `emailAddress` em outro 데이터 세트 정의 코모 ID da pessoa. `delaigle@adobe.com` tiver o mesmo valor para o campo ID da pesoa em ambos os 데이터 세트, o CJA poderá compilar os dados.

Atualmente, existem algumas outtras limitações, como compilar o comportamento anônimo para conheido. Pergentas가 자주 AQUI를 호출합니다. [FAQ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html).


### Compilando os dados usando o o ID da pessoa

Agora que você compreende o conceito de compilar dataset usando o ID da pesoa, vamos escoler `email` como ID da pesoa para cada dataset.

![데모](./images/cja15.png)

ID da pessoa에 대한 cada 데이터 세트 para autoalizar.

![데모](./images/cja12a.png)

Agora preencha o campo ID da pessoa escolendo o `email` na lista suspensa.

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

**데이터 세트 추가**&#x200B;를 클릭합니다.

![데모](./images/cja16.png)

클리크 em **저장** e vá para o próximo exercício. Depois de criar sua **Connection**, pode levar algumas horas até que seus dados estejam disponíveis no CJA.

![데모](./images/cja20.png)

Próxima etapa: [4.3 Crie uma Visualização de Dados](./ex3.md)

[레토르나르 파라 플루소 데 우수아리오 4](./uc4.md)

[레토르나르 파라 토도스](./../../overview.md)
