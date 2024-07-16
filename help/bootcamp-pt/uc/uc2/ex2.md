---
title: Bootcamp - Journey Optimizer 이벤트 만들기 - 브라질
description: Bootcamp - Journey Optimizer 이벤트 만들기 - 브라질
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 1b9d7a35-cddf-4f4a-ad0a-95723b00c278
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# 2.2 크리 세우 에벤토

Adobe Journey Optimizer에 대한 Faça 로그인으로 [Adobe Experience Cloud](https://experience.adobe.com)을(를) 수행할 수 있습니다. **Journey Optimizer**&#x200B;을(를) 클릭합니다.

![AOP](./images/acophome.png)

Journey Optimizer의 Você será redirectionado para visualização da **Home** Primeiro , verifique se você está usando o sandbox correto. 샌드박스 que deve ser usado é `Bootcamp`을(를) 하겠습니다. Para alternator de um sandbox para outr, select o sandbox na lista를 클릭합니다. 샌드박스 é **Bootcamp**&#x200B;를 수행하지 마십시오. **Home** 샌드박스 `Bootcamp`를 실행합니다.

![AOP](./images/acoptriglp.png)

메뉴 없음 à esquerda, 역할 para baixo e clique em **구성**. Em seguida, clique no botão **관리** abaixo de **이벤트**.

![AOP](./images/acopmenu.png)

Você verá uma visão geral de todos os eventos disponíveis. **이벤트 만들기** para começar a criar seu próprio evento를 클릭합니다.

![AOP](./images/emptyevent.png)

우마 노바 자넬라 데 에벤토 바지아 이라파레체입니다.

![AOP](./images/emptyevent1.png)

Em primeiro lugar, dê um nome ao seu evento como, por modeo: `seuSobrenomeAccountCreationEvent` e adicione uma descrição como, por modeo: `Account Creation Event`.

![AOP](./images/eventdescription.png)

Em seguida, certifique-se de que **Type** está definido como **Unitary** e, para seleção de **Event ID Type**, selectione **System Generated**.

![AOP](./images/eventidtype.png)

에타파 세귄테 é a seleção do schema. Um schema foi preparado para este exercício. 스키마 `Demo System - Event Schema for Website (Global v1.1) v.1`을(를) 사용합니다.

![AOP](./images/eventschema.png)

Depois de seleionar o Schema, você verá vários campos sendo seleionados na seção **Fields**. Agora você deve passar o mouse sobre a seção **필드** e três ícones pop-up serão exibidos. **편집**&#x200B;을 클릭합니다.

![AOP](./images/eventpayload.png)

Você verá uma janela 팝업 de **필드**, onde você deve selectionar alguns dos campos que precisamos para personalizar o e-mail. Escoleheremos outos atributos de perfil posteriormente, utilizando os dados já existentes na Adobe Experience Platform.

![AOP](./images/eventfields.png)

`_experienceplatform.demoEnvironment` 개체가 없습니다. **brandLogo** e **brandName**.

![AOP](./images/eventpayloadbr.png)

`_experienceplatform.identification.core` 개체가 없습니다. campo **전자 메일**&#x200B;에 대한 certifque-se de selectionar입니다.

![AOP](./images/eventpayloadbrid.png)

Alterações와 같은 para salvar로 **확인**&#x200B;을(를) 클릭합니다.

![AOP](./images/saveok.png)

Em seguida, a tela abaixo deve ser exibida. Clique em **저장** mais uma vez para salvar suas alterações.

![AOP](./images/eventsave.png)

Seu evento agora esta configurado e salvo.

![AOP](./images/eventdone.png)

Clique no seu evento novamente para abrir mais uma vez a tela **이벤트 편집**. Passe o mouse sobre **필드** para ver os 3 ícones outra vez. **페이로드를 봅니다**.

![AOP](./images/viewevent.png)

Agora você verá um examo da carga útil esperada.
Seu evento tem um eventID de orquestração único, que você pode encontrar rolando para baixo nessa carga útil (payload) até visualizar `_experience.campaign.orchestration.eventID`.

![AOP](./images/payloadeventID.png)

O eventID é o que deve ser enviado à Adobe Experience Platform para acionar a jornada que você construirá em um dos próximos exerccios. Lembre-se deste eventID, você pode precisar dele posterionte.
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

**확인**&#x200B;을, **취소**&#x200B;를 클릭합니다.

아고라보사이테누에스티시우

Próxima etapa: [ 2.3 Crie sua mensagem de email](./ex3.md)

[레토르나르 파라 플루소 데 우수아리오 2](./uc2.md)

[레토르나르 파라 토도스](../../overview.md)
