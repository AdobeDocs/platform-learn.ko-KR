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
source-wordcount: '463'
ht-degree: 0%

---

# 2.2 크리 세우 에벤토

Adobe Journey Optimizer 로그인 [Adobe Experience Cloud](https://experience.adobe.com). 클리크 **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirectionado para a visualização da **홈** Journey Optimizer 없음. Primeiro , verifique se você está usando o sandbox correto. O nome do sandbox que deve ser usado é `Bootcamp`. Para alternator de um sandbox para outr, select o sandbox na lista를 클릭합니다. Neste 모형아, nome do sandbox é **부트캠프**. Você estará na visualização da **홈** do seu 샌드박스 `Bootcamp`.

![ACOP](./images/acoptriglp.png)

메뉴 없음 à esquerda, 역할 para baixo e clique em **구성**. Em seguida, 클리크 노 보탕 **관리** 아베이소 데 **이벤트**.

![ACOP](./images/acopmenu.png)

Você verá uma visão geral de todos os eventos disponíveis. 클리크 **이벤트 만들기** para começar a criar seu próprio evento.

![ACOP](./images/emptyevent.png)

우마 노바 자넬라 데 에벤토 바지아 이라파레체입니다.

![ACOP](./images/emptyevent1.png)

Em primeiro lugar , dê um nome ao seu evento como , por moremo : `seuSobrenomeAccountCreationEvent` e adicione uma descrição como, por orimo: `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Em seguida, certifique-se de que **유형** 에스타 디피도 코모 **단일** e, para seleção de **이벤트 ID 유형**, 선택 항목 **시스템 생성됨**.

![ACOP](./images/eventidtype.png)

에타파 세귄테 é a seleção do schema. Um schema foi preparado para este exercício. 스키마 사용 `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de seleionar o Schema, você verá vários campos sendo seleionados na seção **필드**. Agora você deve passar o mouse sobre a seção **필드** e três ícones 팝업 serão exibidos. 클리케 노 이콘 **편집**.

![ACOP](./images/eventpayload.png)

Você verá uma janela 팝업 드 **필드**, onde você deve selectionar alguns dos campos que precisamos para personalizar o e-mail. Escoleheremos outos atributos de perfil posteriormente, utilizando os dados já existentes na Adobe Experience Platform.

![ACOP](./images/eventfields.png)

오브젝트 없음 `_experienceplatform.demoEnvironment`, pcertificate-se de selectionar os campos **brandLogo** e **brandName**.

![ACOP](./images/eventpayloadbr.png)

오브젝트 없음 `_experienceplatform.identification.core`, campo의 certificate-se de selectionar **이메일**.

![ACOP](./images/eventpayloadbrid.png)

클리크 **확인** &#39;알테라수에스&#39;라는 이름의 파라 살바르

![ACOP](./images/saveok.png)

Em seguida, a tela abaixo deve ser exibida. 클리크 **저장**  mais uma vez para salvar suas alterações ..

![ACOP](./images/eventsave.png)

Seu evento agora esta configurado e salvo.

![ACOP](./images/eventdone.png)

Clique no seu evento novamente para abrir mais uma vez a tela **이벤트 편집**. 파세오마우스소브레 **필드** para ver os 3 ícones outra vez. 클리케 노 이콘 **페이로드 보기**.

![ACOP](./images/viewevent.png)

Agora você verá um examo da carga útil esperada.
Seu evento tem um eventID de orquestração único, que você pode encontrar rolando para baixo nessa carga útil (payload) até visualizar `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

O eventID é o que deve ser enviado à Adobe Experience Platform para acionar a jornada que você construirá em um dos próximos exerccios. Lembre-se deste eventID, você pode precisar dele posterionte.
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

클리크 **확인** e, em seguida, clique em **취소**.

아고라보사이테누에스티시우

프록시마 에타파: [ 2.3 Crie sua mensagem de email](./ex3.md)

[레토르나르 파라 플루소 데 우수아리오 2](./uc2.md)

[레토르나르 파라 토도스](../../overview.md)
