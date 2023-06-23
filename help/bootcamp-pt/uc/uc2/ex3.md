---
title: Bootcamp - Journey Optimizer 여정 및 이메일 메시지 만들기 - 브라질
description: Bootcamp - Journey Optimizer 여정 및 이메일 메시지 만들기 - 브라질
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: d486d1aa-7b8e-4301-91e6-4c84fba0c72a
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 3%

---

# 2.3 Crie sua jornada e mensagem de email

Neste exercício, você irá configurar a jornada que precisa ser acionada quando alguém criar uma conta no site de demonstração.

Adobe Journey Optimizer 로그인 [Adobe Experience Cloud](https://experience.adobe.com). 클리크 **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirectionado para a visualização da **홈**  Journey Optimizer 없음. Primeiro , verifique se você está usando o sandbox correto. O nome do sandbox que deve ser usado é `Bootcamp`. Para alternator de um sandbox para outtro, 클릭 em **Prod** 샌드박스 na lista를 선택합니다. Neste 모형아, nome do sandbox é **부트캠프**. Você estará na visualização da **홈** do seu 샌드박스 `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 2.3.1 Crie a sua jornada

메뉴 없음 aesquerda, 클릭 em **여정**. Em seguida, clique em **여정 만들기** 파라 크리아르 우마 노바 호르나다.

![ACOP](./images/createjourney.png)

보테 베라 우마 텔라 데 조나다 바지아.

![ACOP](./images/journeyempty.png)

노보, 보테 크리우 움 노보 **이벤트**. 보테노메오오에벤토 `seuSobrenomeAccountCreationEvent` 대용물 `seuSobrenome` 펠로 세우 소브레놈 Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

Agora você deve considerar este evento como o início desta Jornada. Você pode fazer isso indo para o lado esquerdo da tela e procurando pelo seu evento na lista de eventos.

![ACOP](./images/eventlist.png)

Selecione seu evento, arraste e solte o evento na tela de Jornada. Sua Jornada agora deve ser semelhante ao seguinte:

![ACOP](./images/journeyevent.png)

Como segunda etapa da jornada, você deve adicionar uma etapa curta de **대기**. Vá para o lado esquerdo da tela até a seção **오케스트레이션** 파라 엔콘트라르 isso. Você usará atributos de perfil e precisará garantir que eles sejam preenchidos no Perfil do Cliente em tempo real.

![ACOP](./images/journeywait.png)

수아 조나다 아고라 데베 세르 세멜란테 아오 세귄테. No lado direito da tela você precisa configurar o tempo de espera. 코모 1분짜리로 정하세요 Isso dará bastante tempo para que os atributos do perfil estejam disponíveis após o disparo do evento.

![ACOP](./images/journeywait1.png)

클리크 **확인** alterações를 뜻하는 para salvar.

Como terceira etapa da jornada, você deve adicionar uma ação **이메일**. Vá para o lado esquerdo da tela para **작업**, ação 선택 **이메일** e arraste e solte a ação no segundo nó da sua jornada. 아고라오세긴테세라 엑시비도

![ACOP](./images/journeyactions.png)

정의 a **범주** 코모 **마케팅** e selecione uma **이메일 표면** que permita o envio de e-mail. 네스카소, a **이메일 표면** e-mail을 보냅니다. Certifque-se de que as caixas de 셀레상 **이메일 클릭 수** e **이메일 열람수** 에스테잼 마카다스

![ACOP](./images/journeyactions1.png)

A próximo etapa é criar sua mensagem. 파라 이소, 클리크 **콘텐츠 편집**.

![ACOP](./images/journeyactions2.png)

## 2.3.2 Crie a sua mensagem

Para criar sua mensagem, clique em **콘텐츠 편집**.

![ACOP](./images/journeyactions2.png)

오 세구인테 세라 엑시비도.

![ACOP](./images/journeyactions3.png)

클리크 노 캄포 데 텍스토 **제목 줄**.

![Journey Optimizer](./images/msg5.png)

Na área de texto, comece **올라**

![Journey Optimizer](./images/msg6.png)

A linha de assunto ainda não está pronta. Em seguida, você precisa trazer o token de personalização para o **이름** 케 에스타 아르마제나도 em `profile.person.name.firstName`. 메뉴 없음 à esquerda, 역할 para baixo para encontrar o o elemento **개인** e clique na seta para visualizar mais campos

![Journey Optimizer](./images/msg7.png)

Agora encontre o elemento **전체 이름** e clique na seta para visualizar mais campos.

![Journey Optimizer](./images/msg8.png)

Por fim, localize o campo **이름** 이 클리크 노 심볼로 **+**  아오 라도 델레. Você verá o token de personalização aparecer no campo de texto.

![Journey Optimizer](./images/msg9.png)

Em seguida, adicione에서 texto, **아그라데세모스 a sua inscrição!** 질문에 답합니다. 클리크 **저장**.

![Journey Optimizer](./images/msg10.png)

엔탕, 보체 이라 레토르나르 파라 텔라 클리크 **이메일 디자이너**  para criar o contudo do email.

![Journey Optimizer](./images/msg11.png)

Na próxima tela, será solicitado que você forneça o conteúdo e-mail através de 3 métodos diferences:

- **처음부터 디자인**: Comece com uma tela em branco e use o editor WYSIWYG PARA ARRASTAR E SOLTAR A ESTRUTURA E OS COMPONENTES DE CONTEÚDO PARA CRIAR VISUALMENTE O CONTEÚDO E-MAIL.
- **나만의 코드 작성**: Crie seu próprio modelo de e-mail codificando usando HTML
- **가져오기 HTML**: Importe um modelo HTML existente, que você poderá editar.

클리크 **가져오기 HTML**.

![Journey Optimizer](./images/msg12.png)

아르키보 **mailtemplatebootcamp.html**, que voê pode baixa [바다오리](../../assets/html/mailtemplatebootcamp.html.zip). 임포타르를 클릭합니다.

![Journey Optimizer](./images/msg13.png)

Você verá este modelo de e-mail 페이지:

![Journey Optimizer](./images/msg14.png)

Vamos는 이메일을 개인화합니다. 클리케 아오 라도 문자 **올라** e, em 세구이다, 클리크 노 이콘 **개인화 추가**.

![Journey Optimizer](./images/msg35.png)

Em seguida, você precisa trazer o token de personalização **이름** 케 에스타 아르마제나도 em `profile.person.name.firstName`. 메뉴 없음, 현지화 또는 요소 **개인**, 파사 uma busca detalhada no elemento **전체 이름** 이클리케 노 이콘 **+** 파라 아디치오나 오 캄포 **이름** ao 편집기.

클리크 **저장**.

![Journey Optimizer](./images/msg36.png)

Agora você verá como o campo de personalização foi adicionado ao seu texto.

![Journey Optimizer](./images/msg37.png)

클리크 **저장** 파라 살바르 수아 멘사젬.

![Journey Optimizer](./images/msg55.png)

Retorne para o painel de mensagens clicando na seta ao lado do do texto da linha de assunto no canto superior esquerdo.

![Journey Optimizer](./images/msg56.png)

Agora você concluiu a criação do seu email de cadastro. Clique na seta no canto superior esquerdo para retornar à sua jornada.

![Journey Optimizer](./images/msg57.png)

클리크 **확인**.

![Journey Optimizer](./images/msg57a.png)

## 2.3.3 게시 a sua jornada

Você ainda precisa dar um nome à sua jornada. 보테 포데 파제 이소 클리칸도 노 이콘 **속성** 칸토 수페리어 디레이토 다 텔라.

![ACOP](./images/journeyname.png)

Você pode fazer isso clicando no item clicar no item &quot;Name&quot; e inserindo o seguinte nome `yourLastName - Account Creation Journey`. 클리크 **확인** 무단사로서의 파라 살바르

![ACOP](./images/journeyname1.png)

Agora você pode publicar sua jornada clicando em **게시**.

![ACOP](./images/publishjourney.png)

클리크 **게시**  노바멘테

![ACOP](./images/publish1.png)

Você verá uma barra de confirmação verde informando que sua jornada agora está Publada.

![ACOP](./images/published.png)

보테노우 에스티시우

프록시마 에타파: [2.4 테스테 수아 조르나다](./ex4.md)

[레토르나르 파라 플루소 데 우수아리오 2](./uc2.md)

[레토르나르 파라 토도스](../../overview.md)
