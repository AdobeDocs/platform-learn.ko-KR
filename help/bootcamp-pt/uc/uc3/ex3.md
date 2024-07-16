---
title: Bootcamp - 물리 및 디지털 혼합 - Journey Optimizer 여정 및 푸시 만들기 - Brazilnotification
description: Bootcamp - 물리 및 디지털 혼합 - Journey Optimizer 여정 및 푸시 만들기 - Brazilnotification
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: a4ef6eaf-6b39-4450-82bf-7db99595a323
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%

---

# 3.3 크리 수아 조르나다에 노티피카상 푸시

Neste exercícicio, você irá configurar a jornada e a mensagem que precisa ser acionada quando alguém inserir uma sinalização (beacon) usando aplicativo móvel.

Adobe Journey Optimizer에 대한 Faça 로그인으로 [Adobe Experience Cloud](https://experience.adobe.com)을(를) 수행할 수 있습니다. **Journey Optimizer**&#x200B;을(를) 클릭합니다.

![AOP](./images/acophome.png)

Journey Optimizer의 Você será redirectionado para visualização da **Home** Primeiro , verifique se você está usando o sandbox correto. 샌드박스 que deve ser usado é `Bootcamp`을(를) 하겠습니다. Para alternator de um sandbox para outtro를 클릭하고, em **Prod**&#x200B;를 선택하여 샌드박스 NA lista를 선택합니다. 샌드박스 é **Bootcamp**&#x200B;를 수행하지 마십시오. **Home** 샌드박스 `Bootcamp`를 실행합니다.

![AOP](./images/acoptriglp.png)

## 3.3.1 Crie a sua jornada

메뉴가 없습니다. **여정**&#x200B;을(를) 클릭합니다. Em seguida, clique em **여정 만들기** para criar uma nova jornada.

![AOP](./images/createjourney.png)

보테 베라 우마 텔라 데 조나다 바지아.

![AOP](./images/journeyempty.png)

전방향 운동 금지, 보테 크리우 움 노보 **이벤트**. 보테노메우오에벤토 `yourLastNameBeaconEntryEvent` e 대체 `yourLastName` pelo seu sobrenome. Este foi o resultado da criação do Evento:

![AOP](./images/eventdone.png)

Agora você deve considerar este evento como o início desta Jornada. Você pode fazer isso indo para o lado esquerdo da tela e procurando pelo seu evento na lista de eventos.

![AOP](./images/eventlist.png)

Selecione seu evento, arraste e solte o evento na tela de jornada. 수아 조나다 아고라 데베 세르 세멜란테 아오 세귄테. **확인** para salvar suas alterações를 클릭합니다.

![AOP](./images/journeyevent.png)

Como segunda etapa da jornada, você deve adicionar uma ação **푸시**. Vá para o lado esquerdo da tela para **Actions**, select one a ação **Push** e arraste e solte a ação no segundo nó da sua jornada.

![AOP](./images/journeyactions.png)

No lado direito da tela, agora você deve criar sua notificação push.

**카테고리** 코모 **마케팅**&#x200B;을(를) 선택합니다. Nesse caso, 수퍼피시 푸시 사용자 selectionada **mmeeewis-app-mobile-bootcamp**.

![AOP](./images/journeyactions1.png)

## 3.3.2 Crie a sua mensagem

**콘텐츠 편집**&#x200B;을 클릭합니다.

![AOP](./images/emptymsg.png)

Em seguida, a tela abaixo será exibida :

![AOP](./images/emailmsglist.png)

Vamos dedefinir o conteúdo da notificação push.

**Title**&#x200B;에 대한 캠페인 데이터 중복 제거를 클릭합니다.

![Journey Optimizer](./images/msg5.png)

Na área de texto 님, **Olá**&#x200B;님! Clique no ícone de personalização.

![Journey Optimizer](./images/msg6.png)

Agora você precisa trazer o token de personalização para o campo **이름** que está armazenado em `profile.person.name.firstName`. 메뉴가 없습니다. **프로필 속성**, 역할 para baixo/navegue para encontrar o o elemento **사람** e clique na seta para avançar um nível até chegar ao campo `profile.person.name.firstName`. Clique no ícone **+** para adicionar o campo à tela. **저장**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/msg7.png)

엔탕, 보체 이라 레토르나르 파라 텔라 Clique no ícone de personalização lado do do campo **Body**.

![Journey Optimizer](./images/msg11.png)

Na área de texto, escerva `Bem-vindo(a)`.

![Journey Optimizer](./images/msg12.png)

Em seguida입니다. **컨텍스트 특성** e **Journey Orchestration**&#x200B;을 클릭하세요.

![AOP](./images/jomsg3.png)

**이벤트**&#x200B;를 클릭합니다.

![AOP](./images/jomsg4.png)

Clique no nome do seu evento, que deve ser semelhante ao seguinte: **yourLastNameBeaconEntryEvent**

![AOP](./images/jomsg5.png)

**컨텍스트 배치**&#x200B;를 클릭합니다.

![AOP](./images/jomsg6.png)

**POI 인터랙션**&#x200B;을 클릭합니다.

![AOP](./images/jomsg7.png)

**POI 세부 정보**&#x200B;를 클릭합니다.

![AOP](./images/jomsg8.png)

**+** 아이콘 **POI 이름**을 클릭합니다.
세구이다, 세구인테 세라 엑시비도 **저장**&#x200B;을 클릭합니다.

![AOP](./images/jomsg9.png)

수아 멘사젬 아고라 에스타 프론타. Clique na seta no canto superior esquerdo para retornar à sua jornada.

![AOP](./images/jomsg11.png)

**확인**&#x200B;을 클릭합니다.

![AOP](./images/jomsg14.png)

## 3.3.2 Envie uma mensagem para uma tela

Como terceira etapa da jornada, você deve adicionar uma ação **sendMessageToScreen**. Vá para o lado esquerdo da tela para **Actions**, select ione a ação **sendMessageToScreen** e arraste e solte a ção no terceiro nó da sua jornada. Em seguida, você verá a tela abaixo.

![AOP](./images/jomsg15.png)

**sendMessageToScreen** é uma ação personalizada que irá publicar uma mensagem no **Endpoint** usado pela exibição na loja. Ação **sendMessageToScreen** espera que múltiplas variáveis sejam definidas. Você pode visualizar essas variáveis rolando para baixo até ver **Action 매개 변수**.

![AOP](./images/jomsg16.png)

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

Para는 valores를 정의하며, hicone를 사용하지 않습니다. **편집**.

![AOP](./images/jomsg17.png)

Em 스키마입니다. **고급 모드**&#x200B;를 선택하십시오.

![AOP](./images/jomsg18.png)

Em seguida, cole o valor com base na tabela acima. **확인**&#x200B;을 클릭합니다.

![AOP](./images/jomsg19.png)

Repita esse processo para adicionar valores para cada campo.

>[!IMPORTANT]
>
>Para o campo ECID, há uma referência ao evento`yourLastNameBeaconEntryEvent`. 대체 `yourLastName` 펠로 순 소브레놈(sobrenome)을 Lembre-se de substitiir합니다.

결과 Resultado final deve ser semelhante ao seguinte:

![AOP](./images/jomsg20.png)

역할 para cima e clique em **확인**.

![AOP](./images/jomsg21.png)

여정 이름을 계속 지정해야 합니다. 화면 오른쪽 상단의 **속성** 아이콘을 클릭하면 됩니다.

![AOP](./images/journeyname.png)

Você pode inserir o nome da jornada aqui. `yourLastName - Beacon Entry Journey` 사용. **확인** para salvar suas alterações를 클릭합니다.

![AOP](./images/journeyname1.png)

Agora você pode publicar sua jornada clicando em **Publish**.

![AOP](./images/publishjourney.png)

**Publish** novamente를 클릭합니다.

![AOP](./images/publish1.png)

Você verá uma barra de confirmação verde informando que sua jornada agora está Publada.

![AOP](./images/published.png)

Sua jornada agora está ativa e pode ser acionada.

보테노우 에스티시우

Próxima etapa: [3.4 Teste sua jornada](./ex4.md)

[레토르나르 파라 플루소 데 우수아리오 3](./uc3.md)

[레토르나르 파라 토도스](../../overview.md)
