---
title: Bootcamp - 콜 센터의 개인화 - 브라질
description: Bootcamp - 콜 센터의 개인화 - 브라질
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: 7acf778b-042f-4deb-9406-ddcf63daacda
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---

# 2.6 Personalização no call center

Conforme discutido várias vezes durante o bootcamp, personalizar a experiencia do cliente é algo que deve acontecer de maneira omnichannel. Um call center geralmente é bastante desconectado do restante da jornada do cliente e isso pode, com frequência, levar a experiências frustrantes do cliente, mas não precisa ser assim. Vamos mostrar um modeo de como call center pode ser facilmente conectado à Adobe Experience Platform, em 템포 리얼.

## 플루소 다 조르나다 두 클리엔테

No exercício anterior, usando o aplicativo móvel, você comprou um produto clicando no botão **구매**.

![DSN](./images/app20.png)

Vamos supor que você tenha uma pergunta sobre o status do seu peedo, o que você faria? Normalmente, você ligaria para o 콜 센터.

Antes de ligar para o 콜 센터, você precisa saber seu **고객 충성도 ID**. Você pode encontrar seu ID de fidelidade no Visualizador de Perfil do site.

![DSN](./images/cc1.png)

네스카소, o **고객 충성도 ID** é **5863105**. Como parte de nossa implementação personalizada do recurso de call center no ambiente de demonstração, você deve adicionar um prefixo seu **고객 충성도 ID**. O prefivo é **11373**, portanto, o ID de fidelidade a ser usado neste orimo é **11373 5863105**.

바모스 파제르 아고라 Use seu telefone e ligue para o número **+1 (323) 745-1670**.

![DSN](./images/cc2.png)

Será solicitado que você insira seu ID de fidelidade, 세기도 **#**. Digite seu ID de fidelidade.

![DSN](./images/cc3.png)

보사이오우비라 **안녕하세요, 스놈**. Esse nome é retirado Perfil do Cliente em tempo real na Adobe Experience Platform. Você tem 3 escolas. 프레시오네오누메로 **1**, **주문 상태**.

![DSN](./images/cc4.png)

Depois de ouvir o status do seu peedo, você terá a opção de pressionar **1** para voltar ao 메뉴 principal ou pressionar 2. 프레시오네 **2**.

![DSN](./images/cc5.png)

Em seguida, será solicitado que você avalie sua experiência de call centre, selectionando um número entre 1 e 5, sendo 1 baixo e 5 alto. Faça sua escolha.

![DSN](./images/cc6.png)

Sua chamada para o 콜 센터 세라 엔세라다.

액세스 [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer 로그인, você irá acesssar a página inicial da Adobe Experience Platform.

![데이터 수집](./images/home.png)

Antes de continar, você precisa selecionar um **샌드박스**. 샌드박스 a ser selectionado é ``Bootcamp``. 레 포시벨 파제 이스소 클리칸도 노 텍토 **[!UICONTROL 프로덕션 프로덕션]** 나 리냐 아줄 나 파르테 수페리어 다 텔라. Depois de selectionar o [!UICONTROL 샌드박스] apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL 샌드박스] 헌신.

![데이터 수집](./images/sb1.png)

메뉴 없음, 에스케다 **프로필** e **찾아보기**.

![고객 프로필](./images/homemenu.png)

다음 중 하나 선택 **ID 네임스페이스** **이메일** e insira o endereço de e-mail do seu perfil de cliente. 클리크 **보기**. 파라 아브리 수 페필

![DSN](./images/cc7.png)

Você verá seu perfil de cliente novamente. 액세스 **이벤트**.

![DSN](./images/cc8.png)

Em eventos, você verá 2 eventos com um eventType de **콜 센터**. O primeiro evento é o resultado da sua resposta à pergunta **통화 만족도 평가** (아발리 슈 카마다).

![DSN](./images/cc9.png)

역할 um pouco para baixo e você verá o evento que foi registrado quando você seleionou a opção de verificar o **주문 상태**.

![DSN](./images/cc10.png)

액세스 **세그먼트 멤버십**. Agora você verá que 2 segmentos se qualificam em seu perfil, em tempo real, com base nas interações que você por meio do 콜 센터 Essas associações de segmento podem e devem ser usadas para impactar qual comunicação e personalização acontece em qualquer outo canal.

![DSN](./images/cc11.png)

보테노우 에스티시우

[레토르나르 파라 플루소 데 우수아리오 2](./uc2.md)

[레토르나르 파라 토도스](../../overview.md)
