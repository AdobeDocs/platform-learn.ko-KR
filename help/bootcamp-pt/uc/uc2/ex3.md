---
title: Bootcamp - Journey Optimizer 여정 및 이메일 메시지 만들기 - 브라질
description: Bootcamp - Journey Optimizer 여정 및 이메일 메시지 만들기 - 브라질
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Journeys
exl-id: d486d1aa-7b8e-4301-91e6-4c84fba0c72a
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 0%

---

# 2.3 Crie sua jornada e mensagem de email

Neste exercício, você irá configurar a jornada que precisa ser acionada quando alguém criar uma conta no site de demonstração.

Adobe Journey Optimizer에 대한 Faça 로그인으로 [Adobe Experience Cloud](https://experience.adobe.com)을(를) 수행할 수 있습니다. **Journey Optimizer**&#x200B;을(를) 클릭합니다.

![AOP](./images/acophome.png)

Journey Optimizer의 Você será redirectionado para visualização da **Home** Primeiro , verifique se você está usando o sandbox correto. 샌드박스 que deve ser usado é `Bootcamp`을(를) 하겠습니다. Para alternator de um sandbox para outtro를 클릭하고, em **Prod**&#x200B;를 선택하여 샌드박스 NA lista를 선택합니다. 샌드박스 é **Bootcamp**&#x200B;를 수행하지 마십시오. **Home** 샌드박스 `Bootcamp`를 실행합니다.

![AOP](./images/acoptriglp.png)

## 2.3.1 Crie a sua jornada

메뉴가 없습니다. **여정**&#x200B;을(를) 클릭합니다. Em seguida, clique em **여정 만들기** para criar uma nova jornada.

![AOP](./images/createjourney.png)

보테 베라 우마 텔라 데 조나다 바지아.

![AOP](./images/journeyempty.png)

전방향 운동 금지, 보테 크리우 움 노보 **이벤트**. 보테노메우오에벤토 `seuSobrenomeAccountCreationEvent` e 대체 `seuSobrenome` pelo seu sobrenome. Este foi o resultado da criação do Evento:

![AOP](./images/eventdone.png)

Agora você deve considerar este evento como o início desta Jornada. Você pode fazer isso indo para o lado esquerdo da tela e procurando pelo seu evento na lista de eventos.

![AOP](./images/eventlist.png)

Selecione seu evento, arraste e solte o evento na tela de Jornada. Sua Jornada agora deve ser semelhante ao seguinte:

![AOP](./images/journeyevent.png)

Como segunda etapa da jornada, você deve adicionar uma etapa curta de **대기**. Vá para o lado esquerdo da tela até a seção **오케스트레이션** para encontrar isso. Você usará atributos de perfil e precisará garantir que eles sejam preenchidos no Perfil do Cliente em tempo real.

![AOP](./images/journeywait.png)

수아 조나다 아고라 데베 세르 세멜란테 아오 세귄테. No lado direito da tela você precisa configurar o tempo de espera. 코모 1분짜리로 정하세요 Isso dará bastante tempo para que os atributos do perfil estejam disponíveis após o disparo do evento.

![AOP](./images/journeywait1.png)

**확인** para salvar suas alterações를 클릭합니다.

Como terceira etapa da jornada, você deve adicionar uma ação **이메일**. Vá para o lado esquerdo da tela para **작업**, ação **이메일**&#x200B;을(를) 선택하십시오. 아고라오세긴테세라 엑시비도

![AOP](./images/journeyactions.png)

**범주** 코모 **마케팅**&#x200B;에서 UMA **전자 메일 표면**&#x200B;을(를) 선택하여 e-메일을 환경 설정합니다. Nesse caso, **전자 메일 표면** 사용자 선택 전자 메일 Certifique-se de que as caixas de seleção **이메일 클릭** e **이메일 열기** estejam marcadas.

![AOP](./images/journeyactions1.png)

A próximo etapa é criar sua mensagem. Para isso, **콘텐츠 편집**&#x200B;을 클릭합니다.

![AOP](./images/journeyactions2.png)

## 2.3.2 Crie a sua mensagem

Para criar sua mensagem, **콘텐츠 편집**&#x200B;을(를) 클릭합니다.

![AOP](./images/journeyactions2.png)

오 세구인테 세라 엑시비도.

![AOP](./images/journeyactions3.png)

**제목 줄**&#x200B;의 campo de texto를 클릭하지 마십시오.

![Journey Optimizer](./images/msg5.png)

Na área de texto, 커뮤니케이션 **Olá**

![Journey Optimizer](./images/msg6.png)

A linha de assunto ainda não está pronta. Em seguida, você precisa trazer o token de personalização para o **이름** que está armazenado em `profile.person.name.firstName`. 메뉴 없음 à esquerda, role para baixo para encontrar o o elemento **Person** e clique na seta para visualizar mais campos

![Journey Optimizer](./images/msg7.png)

Agora는 요소에 **전체 이름** e clique na seta para visualizar mais campos를 추가합니다.

![Journey Optimizer](./images/msg8.png)

Por fim, localize o campo **First name** e clique no símbolo **+** ao lado dele. Você verá o token de personalização aparecer no campo de texto.

![Journey Optimizer](./images/msg9.png)

Em seguida, adicione o texto, **agradecemos a sua inscrição!** 질문에 답합니다. **저장**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/msg10.png)

엔탕, 보체 이라 레토르나르 파라 텔라 **이메일 Designer** 파라 크리어 또는 콘투도 이메일 클릭.

![Journey Optimizer](./images/msg11.png)

Na próxima tela, será solicitado que você forneça o conteúdo e-mail através de 3 métodos diferences:

- **처음부터 디자인**: Comece com uma tela em branco e use o editor WYSIWYG para arrastar e soltar a estrutura e os components de conteúdo para criar visualmente o conteúdo e-mail.
- **직접 코드**: Crie seu próprio modelo de e-mail codificando usando HTML
- **HTML 가져오기**: Importe um modelo HTML existente, que você poderá editar.

**HTML 가져오기**&#x200B;를 클릭합니다.

![Journey Optimizer](./images/msg12.png)

Arquivo **mailtemplatebootcamp.html**, que você pode baixa [aqui](../../assets/html/mailtemplatebootcamp.html.zip)에 대한 Arraste e solte입니다. 임포타르를 클릭합니다.

![Journey Optimizer](./images/msg13.png)

Você verá este modelo de e-mail 페이지:

![Journey Optimizer](./images/msg14.png)

Vamos는 이메일을 개인화합니다. Clique ao lado texto **Olá** e, em seguida, clique no ícone **Personalization 추가**.

![Journey Optimizer](./images/msg35.png)

Em seguida, você precisa trazer o token de personalização **이름** que está armazenado em `profile.person.name.firstName`. 메뉴 없음, 현지화 또는 요소 **Person**, 파사 uma busca detalhada no 요소 **전체 이름** e clique no ícone **+** para adicionar o campo **이름** ao 편집기.

**저장**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/msg36.png)

Agora você verá como o campo de personalização foi adicionado ao seu texto.

![Journey Optimizer](./images/msg37.png)

**저장** para salvar sua mensagem을 클릭합니다.

![Journey Optimizer](./images/msg55.png)

Retorne para o painel de mensagens clicando na seta ao lado do do texto da linha de assunto no canto superior esquerdo.

![Journey Optimizer](./images/msg56.png)

Agora você concluiu a criação do seu email de cadastro. Clique na seta no canto superior esquerdo para retornar à sua jornada.

![Journey Optimizer](./images/msg57.png)

**확인**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/msg57a.png)

## 2.3.3 게시 a sua jornada

Você ainda precisa dar um nome à sua jornada. Você pode fazer siso clicando no ícone **속성** no canto superior direito da tela.

![AOP](./images/journeyname.png)

Você pode fazer는 표시 안 함 항목 표시 안 함 항목 표시 안 함 항목 &quot;Name&quot; e inserindo o seguinte nome `yourLastName - Account Creation Journey`. **OK** para salvar를 mudanças로 클릭합니다.

![AOP](./images/journeyname1.png)

Agora você pode publicar sua jornada clicando em **Publish**.

![AOP](./images/publishjourney.png)

**Publish** novamente를 클릭합니다.

![AOP](./images/publish1.png)

Você verá uma barra de confirmação verde informando que sua jornada agora está Publada.

![AOP](./images/published.png)

보테노우 에스티시우

Próxima etapa: [2.4 Teste sua jornada](./ex4.md)

[레토르나르 파라 플루소 데 우수아리오 2](./uc2.md)

[레토르나르 파라 토도스](../../overview.md)
