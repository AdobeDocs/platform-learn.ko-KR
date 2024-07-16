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
source-wordcount: '471'
ht-degree: 0%

---

# 3.2 크리 세우 에벤토

Adobe Journey Optimizer에 대한 Faça 로그인으로 [Adobe Experience Cloud]을(를) 수행할 수 있습니다. **Journey Optimizer**&#x200B;을(를) 클릭합니다.

![AOP](./images/acophome.png)

Journey Optimizer에서 **Home** Você será redirectionado para. Primeiro , verifique se você está usando o sandbox correto. 샌드박스 que deve ser usado é `Bootcamp`을(를) 하겠습니다. Para alternator de um sandbox para outtro를 클릭하고, em **Prod**&#x200B;를 선택하여 샌드박스 NA lista를 선택합니다. 샌드박스 é **Bootcamp**&#x200B;를 수행하지 마십시오. **Home** 샌드박스 `Bootcamp`를 실행합니다.

![AOP](./images/acoptriglp.png)

메뉴 없음 à esquerda, 역할 para baixo e clique em **구성**. Em seguida, clique no botão **관리** em 이벤트.

![AOP](./images/acopmenu.png)

Você verá uma visão geral de todos os eventos disponíveis. **이벤트 만들기** para começar a criar seu próprio evento를 클릭합니다.

![AOP](./images/emptyevent.png)

우마 노바 자넬라 데 에벤토 바지아 이라파레체입니다.

Em primeiro lugar, dê um nome ao seu evento como, por modeo: `yourLastNameBeaconEntryEvent` e adicione uma descrição como, por modeo: `Beacon Entry Event`.

![AOP](./images/eventdescription.png)

Em seguida, certifique-se de que **Type** está definido como **Unitary** e, para seleção de **Event ID Type**, selectione **System Generated**.

![AOP](./images/eventidtype.png)

에타파 세귄테 é a seleção do schema. Um schema foi preparado para este exercício. 스키마 `Demo System - Event Schema for Mobile App (Global v1.1) v.1`을(를) 사용합니다.

![AOP](./images/eventschema.png)

Depois de seleionar o Schema, você verá vários campos sendo seleionados na seção **Fields**. Agora você deve passar o mouse sobre a seção **필드** e três ícones pop-up serão exibidos. **편집**&#x200B;을 클릭합니다.

![AOP](./images/eventpayload.png)

Você verá uma janela 팝업 de **필드**, onde você deve selectionar alguns dos campos que precisamos para personalizar a jornada. Escoleheremos outtros atributos de perfil posteriormente, utilizando os dados já existentes na Adobe Experience Platform

![AOP](./images/eventfields.png)

역할 para baixo até ver o objeto `Place context` e marque a caixa de seleção. Com isso, todo o contexto da localização do cliente será disponibilizado para jornada. **확인** para salvar suas alterações를 클릭합니다.

![AOP](./images/eventpayloadbr.png)

Em seguida, você deverá ver a tela abaixo. Clique em **저장** mais uma vez para salvar suas alterações.

![AOP](./images/eventsave.png)

Seu evento agora esta configurado e salvo.

![AOP](./images/eventdone.png)

Clique no seu evento novamente para abrir a tela **이벤트 편집** mais uma vez. os 3 ícones에서 마우스 조각 **필드** para를 통과합니다. **보기**&#x200B;를 클릭합니다.

![AOP](./images/viewevent.png)

Agora você verá um orimo do payload esperado.
Seu evento tem um eventID de orquestração único, que você pode encontrar rolando para baixo nessa carga útil até visualiza `_experience.campaign.orchestration.eventID`.

![AOP](./images/payloadeventID.png)

O eventID é o que deve ser enviado à Adobe Experience Platform para acionar a jornada que você construirá em um dos próximos exerccios. Lembre-se deste eventID, você pode precisar dele posterionte.
`"eventID": "e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5"`

**확인**&#x200B;을 클릭하세요. **취소**&#x200B;를 클릭하세요.

보테노우 에스티시우

Próxima etapa: [3.3 Crie sua jornada e notificação push](./ex3.md)

[레토르나르 파라 플루소 데 우수아리오 3](./uc3.md)

[레토르나르 파라 토도스](../../overview.md)
