---
title: Bootcamp - 콜센터의 Personalization - 브라질
description: Bootcamp - 콜센터의 Personalization - 브라질
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 7acf778b-042f-4deb-9406-ddcf63daacda
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# 2.6 Personalização no call center

Conforme discutido várias vezes durante o bootcamp, personalizar a experiencia do cliente é algo que deve acontecer de maneira omnichannel. Um call center geralmente é bastante desconectado do restante da jornada do cliente e isso pode, com frequência, levar a experiências frustrantes do cliente, mas não precisa ser assim. Vamos mostrar um modeo de como call center pode ser facilmente conectado à Adobe Experience Platform, em 템포 리얼.

## 플루소 다 조르나다 두 클리엔테

No exercício anterior, usando o aplicativo móvel, você comprou um produto clicando no botão **구매**.

![DSN](./images/app20.png)

Vamos supor que você tenha uma pergunta sobre o status do seu peedo, o que você faria? Normalmente, você ligaria para o 콜 센터.

Antes de ligar para o 콜 센터, você precisa saber seu **충성도 ID**. Você pode encontrar seu ID de fidelidade no Visualizador de Perfil do site.

![DSN](./images/cc1.png)

Nesse caso, o **충성도 ID** é **5863105**. Como parte de nossa implementação personalizada do recurso de call center no ambiente de demonstração, você deve adicionar um prefixo seu **충성도 ID**. O prefixo é **11373**, portanto, o ID de fidelidade a ser usado neste moreo é **11373** 5863105.

바모스 파제르 아고라 seu telefone e ligue para o número **+1 (323) 745-1670**&#x200B;을 사용합니다.

![DSN](./images/cc2.png)

Será solicitado que você insira seu id de fidelidade, seguido de **#**. Digite seu ID de fidelidade.

![DSN](./images/cc3.png)

보테 오우비라 **안녕하세요, 님**. Esse nome é retirado Perfil do Cliente em tempo real na Adobe Experience Platform. Você tem 3 escolas. Pressione 또는 número **1**, **주문 상태**.

![DSN](./images/cc4.png)

Depois de ouvir o status do seu peedo, você terá a opção de pressionar **1** para voltar ao menu principal ou pressionar 2. **2** 대기 중.

![DSN](./images/cc5.png)

Em seguida, será solicitado que você avalie sua experiência de call centre, selectionando um número entre 1 e 5, sendo 1 baixo e 5 alto. Faça sua escolha.

![DSN](./images/cc6.png)

Sua chamada para o 콜 센터 세라 엔세라다.

[Adobe Experience Platform](https://experience.adobe.com/platform)에 액세스합니다. Depois de fazer 로그인, você irá acesssar a página inicial da Adobe Experience Platform.

![데이터 수집](./images/home.png)

Antes de continar, você precisa selectionar um **sandbox**. 사용자 selectionado é ``Bootcamp``을(를) 샌드박스로 설정하지 마십시오. É possível fazer siso clicando no texto **[!UICONTROL 프로덕션 제품]** na linha azul na parte superior da tela. [!UICONTROL sandbox] apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandbox] dedicado에 대한 선택권이 있습니다.

![데이터 수집](./images/sb1.png)

메뉴 없음, **프로필**&#x200B;에 액세스 **찾아보기**.

![고객 프로필](./images/homemenu.png)

**ID 네임스페이스** **이메일** 이메일 인사이어를 선택하여 e-mail do seu perfil de cliente를 실행합니다. **보기**&#x200B;를 클릭합니다. 파라 아브리 수 페필

![DSN](./images/cc7.png)

Você verá seu perfil de cliente novamente. **이벤트**&#x200B;에 액세스합니다.

![DSN](./images/cc8.png)

Em eventos, você verá 2 eventos com um eventType de **callCenter**. O primeiro evento é o resultado da sua resposta à pergunta **통화 만족도를 평가하세요** (avalie seu chamada).

![DSN](./images/cc9.png)

역할 um pouco para baixo e você verá o evento que foi registrado quando você seleionou a opção de verificar o **주문 상태**.

![DSN](./images/cc10.png)

**세그먼트 멤버십**&#x200B;에 액세스합니다. Agora você verá que 2 segmentos se qualificam em seu perfil, em tempo real, com base nas interações que você por meio do 콜 센터 Essas associações de segmento podem e devem ser usadas para impactar qual comunicação e personalização acontece em qualquer outo canal.

![DSN](./images/cc11.png)

보테노우 에스티시우

[레토르나르 파라 플루소 데 우수아리오 2](./uc2.md)

[레토르나르 파라 토도스](../../overview.md)
