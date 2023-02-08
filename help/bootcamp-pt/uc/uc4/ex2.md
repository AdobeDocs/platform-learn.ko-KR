---
title: Bootcamp - Customer Journey Analytics - Customer Journey Analytics에서 Adobe Experience Platform 데이터 세트 연결 - 브라질
description: Bootcamp - Customer Journey Analytics - Customer Journey Analytics에서 Adobe Experience Platform 데이터 세트 연결 - 브라질
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 3272d288185415b4604fe48f18c19f8f06e6dce0
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 2%

---

# 4.2 Adobe Experience Platform 데이터 세트 다 Customer Journey Analytics 없음

## 오베티보

- 포괄적인 UI da conexao de dados
- Traga os dados da Adobe Experience Platform para o CJA
- Entenda a ID da 페소아 e a compilaçao de dados
- 고객 여정에서 Aprendda o conceptor de dados 스트리밍

## 4.2.1 Conexao

Acesse [analytics.adobe.com](https://analytics.adobe.com) Customer Journey Analytics에 대한 파라 메시지

Na página indicial do Customer Journey Analytics, esse **연결**.

![데모](./images/cja2.png)

퀘이 보크는 CJA e a Plataforma의 디페렌터스 케엑시르로 베르투 Essas conexauseules tem o mesmo objito dos conjuntos de relatorios no Adobe Analytics. 엔토토가 없고, 콜레타 도스 디도다 메톨트암테 Adobe Experience Platform의 Todos os dados vetm de 데이터 세트

아모스 크리아르수아 코네상 Clique em **새 연결 만들기**.

![데모](./images/cja4.png)

Vokheverla a UI **연결 만들기** UI.

![데모](./images/cja5.png)

아고라 보케데 다르 움노메 아수아 코네상

상태 모델 사용: `yourLastName – Omnichannel Data Connection`.

예제: `vangeluw - Omnichannel Data Connection`

Voqtampém deve selecionar 또는 Sandbox correto para usar. 메뉴 샌드박스 없음, 셀렉티온 세트 샌드박스, 사용자 정의 `Bootcamp`. 중첩된 예제, 또는 샌드박스 사용자 usado é o **Bootcamp**. E voktampém definir o **일일 평균 이벤트 수** to **100만 미만**.

![데모](./images/cjasb.png)

Apos selecionar seu 샌드박스, Voke pode começar는 Esta Conexao의 adiconar 데이터 세트 Clique em **데이터 세트 추가**.

![데모](./images/cjasb1.png)

## 4.2.2 Selecione 데이터 세트 다 Adobe Experience Platform

데이터 집합에 유지 `Demo System - Event Dataset for Website (Global v1.1)`. Clique em **+** 데이터 세트 a esta conexao의 para adiconar

![데모](./images/cja7.png)

아고라 페스퀴즈 마르케와 카이사스 데 셀레상 `Demo System - Event Dataset for Voice Assistants (Global v1.1)` 및 `Demo System - Event Dataset for Call Center (Global v1.1)`.

엠세구이다, 보스케베라 텔라아비아소입니다 Clique em **다음**.

![데모](./images/cja9.png)

## 4.2.3 ID da 페소아 e 컴파일라상 드 도스

### ID da 페소아

O objetivo oora é juntar는 데이터 세트를 가져옵니다. 파라카다 데이터 세트 셀레치오나도, 보스케어 캄까마도 **개인 ID**. 카다 데이터 세트 세트 세우 프로프리오 데 ID 드 페소아

![데모](./images/cja11.png)

코모 보스포데 버, 모리아어가 ID 다 페소아 셀레시오네이도 오토메이트이다. 이스소 오코르레 포르크 식별주체 é selecionado em cada esquema 또는 Adobe Experience Platform. 코모 예시, 아키 에스타 오 에스케마 파라 `Demo System - Event Schema for Call Center (Global v1.1)`, 온드 보스포데 베크 o 식별자 알바르 프리마리오 에스타 디퀴도 코모 `phoneNumber`.

![데모](./images/cja13.png)

엔토어 없음, 보카앤다 포데 영향력 있는 ID 주체 세라 우샤도 파라 컴파일 데이터 세트 파라 수아 쿠에시 Vokpode Usar qualquer identifier configurado no esquema vinculado seu 데이터 집합을 구성합니다. 메뉴 일시 중단 없음, para explorer os ID의 discoonveis em cada 데이터 세트를 클릭합니다.

![데모](./images/cja14.png)

Conforme mencionado, vopode definir diferentes IDs de pessoa para 데이터 세트에 있습니다. Isso permite reunir diferences 데이터 세트 de mltiplas는 CJA에서 원본으로 사용됩니다. 트레이저 NPS u dados de pesquisa que seriam muito interessantes e uteis para comparender o contextho de acontecimento.

O nome do campo ID da pessoa nao importante, desde que o valor nos campos ID da pessoa. 디가모스 크 테모스 `email` em um 데이터 세트 e `emailAddress` aem 초과 데이터 세트 정의 como ID da 페소아. Se `delaigle@adobe.com` Tiver o mesmo valor para o campo ID da pessoa em ambos os 데이터 세트 또는 CJA poderá compilar os dados 입니다.

아투알멘테, existem algumas algulaus, como compilar o comportamento animo para conhecido. 퍼군타스주파수 아퀴로 영사: [FAQ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html?lang=ko-KR).


### Compilando dados usando o o ID da 페소아

Agora que vocde o concetito de compilar 데이터 세트, usando o ID da pessoa, vamos escoher `email` como ID da pessoa para cada 데이터 세트.

![데모](./images/cja15.png)

Acesse cada 데이터 세트 단락 또는 ID da 페소아.

![데모](./images/cja12a.png)

아고라 프레엔차 o 캄포 ID 다 페소아 에스콜헨도 오 `email` 멜빵도 들어

![데모](./images/cja17.png)

Depois de compilar os tras 데이터 세트, estamos prontos para continuar.

| 데이터 세트 | 개인 ID |
| ----------------- |-------------| 
| 데모 시스템 - 웹 사이트의 이벤트 데이터 세트(글로벌 v1.1) | 이메일 |
| 데모 시스템 - 음성 도우미에 대한 이벤트 데이터 세트(글로벌 v1.1) | 이메일 |
| 데모 시스템 - 콜 센터의 이벤트 데이터 세트(글로벌 v1.1) | 이메일 |

Voqtampém precisa garantir que, para cada 데이터 세트, essas opçaus estejam habilitadas:

- 이차르토도스 노보스
- Preencher todos os dexistentes
- Preencher tipo de fonte de dados com &quot;Other&quot;
- Preencher a descriçao com o mesmo nome do Dataset

Clique em **데이터 세트 추가**.

![데모](./images/cja16.png)

Clique em **저장** e vah para o prokximo 운동 시우 데포이스 데 크리아르 수아 **연결**, pode levar algumas horas até que destesegos jam disclooneveis no CJA.

![데모](./images/cja20.png)

프로시마 에타파: [4.3 크리우마 시각화 아상 데 도스](./ex3.md)

[레토나르 플루소 드 우시오 4](./uc4.md)

[레토날라 파라 토도스 오모두로스](./../../overview.md)
