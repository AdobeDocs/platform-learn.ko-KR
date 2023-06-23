---
title: Bootcamp - 물리 및 디지털 혼합 - Journey Optimizer 여정 및 푸시 만들기 - Brazilnotification
description: Bootcamp - 물리 및 디지털 혼합 - Journey Optimizer 여정 및 푸시 만들기 - Brazilnotification
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: a4ef6eaf-6b39-4450-82bf-7db99595a323
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 1%

---

# 3.3 크리 수아 조르나다에 노티파상 푸시

Neste exercícicio, você irá configurar a jornada e a mensagem que precisa ser acionada quando alguém inserir uma sinalização (beacon) usando aplicativo móvel.

Adobe Journey Optimizer 로그인 [Adobe Experience Cloud](https://experience.adobe.com). 클리크 **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirectionado para a visualização da **홈** Journey Optimizer 없음. Primeiro , verifique se você está usando o sandbox correto. O nome do sandbox que deve ser usado é `Bootcamp`. Para alternator de um sandbox para outtro, 클릭 em **Prod** 샌드박스 na lista를 선택합니다. Neste 모형아, nome do sandbox é **부트캠프**. Você estará na visualização da **홈**  do seu 샌드박스 `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 Crie a sua jornada

메뉴 없음 aesquerda, 클릭 em **여정**. Em seguida, clique em **여정 만들기** 파라 크리아르 우마 노바 호르나다.

![ACOP](./images/createjourney.png)

보테 베라 우마 텔라 데 조나다 바지아.

![ACOP](./images/journeyempty.png)

노보, 보테 크리우 움 노보 **이벤트**. 보테노메오오에벤토 `yourLastNameBeaconEntryEvent` 대용물 `yourLastName` 펠로 세우 소브레놈 Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

Agora você deve considerar este evento como o início desta Jornada. Você pode fazer isso indo para o lado esquerdo da tela e procurando pelo seu evento na lista de eventos.

![ACOP](./images/eventlist.png)

Selecione seu evento, arraste e solte o evento na tela de jornada. 수아 조나다 아고라 데베 세르 세멜란테 아오 세귄테. 클리크 **확인** alterações를 뜻하는 para salvar.

![ACOP](./images/journeyevent.png)

Como segunda etapa da jornada, você deve adicionar uma ação **푸시**. Vá para o lado esquerdo da tela para **작업**, ação 선택 **푸시** e arraste e solte a ação no segundo nó da sua jornada.

![ACOP](./images/journeyactions.png)

No lado direito da tela, agora você deve criar sua notificação push.

정의 a **범주** 코모 **마케팅** eselecione um push surface que permite vensificações push. Nesse caso, a superfície push a ser seleionada **meeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Crie a sua mensagem

클리크 **콘텐츠 편집**.

![ACOP](./images/emptymsg.png)

Em seguida, a tela abaixo será exibida :

![ACOP](./images/emailmsglist.png)

Vamos dedefinir o conteúdo da notificação push.

클리크 노 캄포 데 텍스토 **제목**.

![Journey Optimizer](./images/msg5.png)

Na área de texto, comece **올라**. Clique no ícone de personalização.

![Journey Optimizer](./images/msg6.png)

Agora você precisa trazer o token de personalização para o campo **이름** 케 에스타 아르마제나도 em `profile.person.name.firstName`. 메뉴 없음, esquerda, selected **프로필 속성**, 역할 para baixo/navegue para encontrar o o o elemento **개인** e clique na seta para avançar um nível até chegar ao campo `profile.person.name.firstName`. 클리케 노 이콘 **+** 파라 아디치오나 오 캄포 아 텔라. 클리크 **저장**.

![Journey Optimizer](./images/msg7.png)

엔탕, 보체 이라 레토르나르 파라 텔라 Clique no ícone de personalização lado do do campo **본문**.

![Journey Optimizer](./images/msg11.png)

Na área de texto, escerva `Bem-vindo(a)`.

![Journey Optimizer](./images/msg12.png)

Em seguida, clique em  **컨텍스트 속성** e **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

클리크 **이벤트**.

![ACOP](./images/jomsg4.png)

Clique no nome do seu evento, que deve ser semelhante ao seguinte: **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

클리크 **위치 컨텍스트**.

![ACOP](./images/jomsg6.png)

클리크 **POI 인터랙션**.

![ACOP](./images/jomsg7.png)

클리크 **POI 세부 정보**.

![ACOP](./images/jomsg8.png)

클릭 번호 **+** 아이콘 아니요 **POI 이름**.
세구이다, 세구인테 세라 엑시비도 클리크 **저장**.

![ACOP](./images/jomsg9.png)

수아 멘사젬 아고라 에스타 프론타. Clique na seta no canto superior esquerdo para retornar à sua jornada.

![ACOP](./images/jomsg11.png)

클리크 **확인**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Envie uma mensagem para uma tela

Como terceira etapa da jornada, você deve adicionar uma ação  **sendMessageToScreen**. Vá para o lado esquerdo da tela para **작업**, ação 선택 **sendMessageToScreen** e arraste e solte a ação no terceiro nó da sua jornada. Em seguida, você verá a tela abaixo.

![ACOP](./images/jomsg15.png)

**sendMessageToScreen** é uma ação personalizada que irá publicar uma mensagem no **엔드포인트** 우사도 펠라 엑시비상 나 로하. 아상 **sendMessageToScreen** espera que múltiplas variáveis sejam definidas. Você pode visualizar essas variáveis rolando para baixo até ver **작업 매개 변수**.

![ACOP](./images/jomsg16.png)

Agora você precisi definir os valores para cada parâmetro de ação. Siga esta tabela para entender quais valores são necessários e onde.

| 매개변수 | 값 |
|:-------------:| :---------------:|
| 게재 | `'image'` |
| ECID | `@{yourLastNameBeaconEntryEvent._experienceplatform.identification.core.ecid}` |
| 이름 | `#{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName}` |
| 이벤트 주제 | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first().name}` |
| EVENTSUBJECT | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first()._experienceplatform.core.imageURL}` |
| 샌드박스 | `'bootcamp'` |
| CONTAINERID | `''` |
| 활동 ID | `''` |
| PLACEMENTID | `''` |

{style="table-layout:auto"}

Para definir valores, clique no ícone **편집**.

![ACOP](./images/jomsg17.png)

Em seguida, selectione **고급 모드**.

![ACOP](./images/jomsg18.png)

Em seguida, cole o valor com base na tabela acima. 클리크 **확인**.

![ACOP](./images/jomsg19.png)

Repita esse processo para adicionar valores para cada campo.

>[!IMPORTANT]
>
>Para o campo ECID, há uma referência ao evento`yourLastNameBeaconEntryEvent`. 렘브레-세 드 대치르  `yourLastName` 펠로 세우 소브레놈

결과 Resultado final deve ser semelhante ao seguinte:

![ACOP](./images/jomsg20.png)

역할 para cima e clique em **확인**.

![ACOP](./images/jomsg21.png)

여정 이름을 계속 지정해야 합니다. 다음을 클릭하면 됩니다. **속성** 아이콘 을 클릭하여 표시할 수 있습니다.

![ACOP](./images/journeyname.png)

Você pode inserir o nome da jornada aqui.  `yourLastName - Beacon Entry Journey`. 클리크 **확인** alterações를 뜻하는 para salvar.

![ACOP](./images/journeyname1.png)

Agora você pode publicar sua jornada clicando em **게시**.

![ACOP](./images/publishjourney.png)

클리크 **게시** 노바멘테

![ACOP](./images/publish1.png)

Você verá uma barra de confirmação verde informando que sua jornada agora está Publada.

![ACOP](./images/published.png)

Sua jornada agora está ativa e pode ser acionada.

보테노우 에스티시우

프록시마 에타파: [3.4 테스테 수아 조르나다](./ex4.md)

[레토르나르 파라 플루소 데 우수아리오 3](./uc3.md)

[레토르나르 파라 토도스](../../overview.md)
