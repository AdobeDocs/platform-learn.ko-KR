---
title: Bootcamp - 물리 및 디지털 혼합 - Journey Optimizer 이벤트 만들기 - 브라질
description: Bootcamp - 물리 및 디지털 혼합 - Journey Optimizer 이벤트 만들기 - 브라질
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 2133b560-09d8-419d-bb99-05d0f3df52cc
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 3.2 크리 세우 에벤토

Adobe Journey Optimizer 로그인 [Adobe Experience Cloud]. 클리크 **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirectionado para **홈** Journey Optimizer 없음. Primeiro , verifique se você está usando o sandbox correto. O nome do sandbox que deve ser usado é `Bootcamp`. Para alternator de um sandbox para outtro, 클릭 em **Prod** 샌드박스 na lista를 선택합니다. Neste 모형아, nome do sandbox é **부트캠프**. Você estará na visualização da **홈** do seu 샌드박스 `Bootcamp`.

![ACOP](./images/acoptriglp.png)

메뉴 없음 à esquerda, 역할 para baixo e clique em **구성**. Em seguida, 클리크 노 보탕 **관리** em Eventos.

![ACOP](./images/acopmenu.png)

Você verá uma visão geral de todos os eventos disponíveis. 클리크 **이벤트 만들기** para começar a criar seu próprio evento.

![ACOP](./images/emptyevent.png)

우마 노바 자넬라 데 에벤토 바지아 이라파레체입니다.

Em primeiro lugar , dê um nome ao seu evento como , por moremo : `yourLastNameBeaconEntryEvent` e adicione uma descrição como, por orimo: `Beacon Entry Event`.

![ACOP](./images/eventdescription.png)

Em seguida, certifique-se de que **유형** 에스타 디피도 코모 **단일** e, para seleção de **이벤트 ID 유형**, 선택 항목 **시스템 생성됨**.

![ACOP](./images/eventidtype.png)

에타파 세귄테 é a seleção do schema. Um schema foi preparado para este exercício. 스키마 사용 `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de seleionar o Schema, você verá vários campos sendo seleionados na seção **필드**. Agora você deve passar o mouse sobre a seção **필드** e três ícones 팝업 serão exibidos. 클리케 노 이콘 데 **편집**.

![ACOP](./images/eventpayload.png)

Você verá uma janela 팝업 드 **필드**, onde você deve selectionar alguns dos campos que precisamos para personalizar a jornada. Escoleheremos outtros atributos de perfil posteriormente, utilizando os dados já existentes na Adobe Experience Platform

![ACOP](./images/eventfields.png)

역할 para baixo até ver o objeto `Place context` e marque a caixa de seleção. Com isso, todo o contexto da localização do cliente será disponibilizado para jornada. 클리크 **확인** alterações를 뜻하는 para salvar.

![ACOP](./images/eventpayloadbr.png)

Em seguida, você deverá ver a tela abaixo. 클리크 **저장** mais uma vez para salvar suas alterações.

![ACOP](./images/eventsave.png)

Seu evento agora esta configurado e salvo.

![ACOP](./images/eventdone.png)

Clique no seu evento novamente para abrir a tela **이벤트 편집** 우마 베즈 파세오마우스소브레 **필드** para ver os 3 ícones. 클리케 노 이콘 **보기**.

![ACOP](./images/viewevent.png)

Agora você verá um orimo do payload esperado.
Seu evento tem um eventID de orquestração único, que você pode encontrar rolando para baixo nessa carga útil até visualiza `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

O eventID é o que deve ser enviado à Adobe Experience Platform para acionar a jornada que você construirá em um dos próximos exerccios. Lembre-se deste eventID, você pode precisar dele posterionte.
`"eventID": "e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5"`

클리크 **확인** e, em seguida, clique em **칸셀라**.

보테노우 에스티시우

프록시마 에타파: [3.3 크리 수아 조르나다에 노티파상 푸시](./ex3.md)

[레토르나르 파라 플루소 데 우수아리오 3](./uc3.md)

[레토르나르 파라 토도스](../../overview.md)
