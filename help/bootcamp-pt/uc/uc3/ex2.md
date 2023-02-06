---
title: Bootcamp - 실제 및 디지털 혼합 - Journey Optimizer 이벤트 만들기 - 브라질
description: Bootcamp - 실제 및 디지털 혼합 - Journey Optimizer 이벤트 만들기 - 브라질
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# 3.2 Crie seu evento

Adobe Journey Optimizer Acessando에서 패사 로그인 [Adobe Experience Cloud]. Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

보스케라 리크레시오나도 파라 **홈** Journey Optimizer 없음. Primeiro, verifique se voca esto o sandbox correto. O nome do sandbox que deve ser usado `Bootcamp`. Para alternar de um sandbox para, clique em **Prod** lista를 선택합니다. 네스트 모예, 노메 도 샌드박스 é **Bootcamp2**. Vokheestarala na visualizahan da **홈** 샌드박스 보내기 `Bootcamp`.

![ACOP](./images/acoptriglp.png)

메뉴 항목 없음, 역할 파라 바이소 e clique em **구성**. Em Seguida, Client no botang **관리** em Eventos.

![ACOP](./images/acopmenu.png)

Vokheverá vischang geral de todos os eventos disoniveis. Clique em **이벤트 만들기** 파라 코카 치아 세우 프로프리오 evento.

![ACOP](./images/emptyevent.png)

우마 노바 야넬라 데 에벤토 바지라 아파레서

Em Primeiro Lugar, dre um nome ao seu evento, por example: `yourLastNameBeaconEntryEvent` eVar의 예시: `Beacon Entry Event`.

![ACOP](./images/eventdescription.png)

Em Seguida, certifique-se de que **유형** 에스파디니도 코모 **단일** e, 파라 셀레카오 드 **이벤트 ID 유형**, selecione **시스템 생성**.

![ACOP](./images/eventidtype.png)

에타파 세구인테-셀레상 두 스키마. Um 스키마 Foi Prepara Explisioncio 스키마 사용 `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

데포이스 드 셀레치오나 스키마, 보케 베라 바드리오스 캄포스 센카도 셀레치오나오 **필드**. 아고라 보케 데 파사르 마우스소브레아 세상 **필드** 세라오 엑시비도스 클리케 노 아이콘 데 **편집**.

![ACOP](./images/eventpayload.png)

Vokheverá janela 팝업 드 **필드**, onde voke deve selecionar algues dos campos que precisamozamas para personalizar a jornada. Escolheremos outtres atribos de perfil posteriormente, utilizados djah existenthentes Adobe Experience Platform

![ACOP](./images/eventfields.png)

역할 파라 원 아테 대 오부토 `Place context` 마르케 아 케사 드 셀레상 com isso, todo o contexto da localizaço do cliente serla disponibilizado para jornada. Clique em **확인** 파라 살바도르 아타수

![ACOP](./images/eventpayloadbr.png)

Em Seguida, Voqe deverá를 텔라아바소라고 합니다 Clique em **저장** 마아베스 파라 아타르아수

![ACOP](./images/eventsave.png)

Seu evento agora esta configurado e salvo.

![ACOP](./images/eventdone.png)

7번 에벤토 노바멘테 파라라는 텔레아를 줄인다 **이벤트 편집** 마이스 베즈 우마 마우스소브레 **필드** 파라버 OS 3 시콘 클리케 노 아이콘 **보기**.

![ACOP](./images/viewevent.png)

아고라 보베라 우모예 카르가 에스페라다
Seu evento tem eventID de orqueststraçuniau, que pode encontrolar rolandro nessa carutil até visualiza `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

O eventID é o que deve ser envado a Adobe Experience Platform para acionar a jornada que vociraem um dos prluxiomos exlicios. Lembre-se destine eventID, voke pode precyar posteriormente.
`"eventID": "e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5"`

Clique em **확인** e, em seguida, client em **취소**.

보스케어 운동선수

프로시마 에타파: [3.3 Crie sua jornada e notificaang 푸시](./ex3.md)

[레토나르 플루소 드 우시오 3](./uc3.md)

[레토날라 파라 토도스 오모두로스](../../overview.md)
