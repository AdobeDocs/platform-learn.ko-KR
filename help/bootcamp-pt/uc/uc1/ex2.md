---
title: Bootcamp - 실시간 고객 프로필 - 나만의 실시간 고객 프로필 시각화 - UI - 브라질
description: Bootcamp - 실시간 고객 프로필 - 나만의 실시간 고객 프로필 시각화 - UI - 브라질
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 4eebb080-77fd-4162-aa64-d599f1274c93
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 1%

---

# 1.2 Visualize seu próprio perfil de cliente em tempo real - UI

Neste exercício, você irá fazer login na Adobe Experience Platform e visualizar seu próprio Perfil de cliente em tempo real na UI.

## 히스토리아

No Perfil do cliente em tempo real, todos os dados do perfil são exibidos juntamente com os dados do evento, além das associações de segmentos existentes. Os dados mostrados podem vir de qualquer lugar, de aplicativos da Adobe e soluções externas. Essa é a exibição mais poderosa da Adobe Experience Platform, o verdadeiro local do sitema de experiência.

## 1.2.1 visualização do perfil do client na Adobe Experience Platform 사용

[Adobe Experience Platform](https://experience.adobe.com/platform)에 액세스합니다. Depois de fazer 로그인, você irá acesssar a página inicial da Adobe Experience Platform.

![데이터 수집](./images/home.png)

Antes de continar, você precisa selectionar um **sandbox**. O nome do sandbox a ser selectionado é Bootcamp. É possível fazer siso clicando no texto **[!UICONTROL 프로덕션 제품]** na linha azul na parte superior da tela. Depois de seleionar o sandbox apropriado, você verá a a tela mudando e agora você está em seu [!UICONTROL sandbox] dedicado.

![데이터 수집](./images/sb1.png)

메뉴 없음, **프로필**&#x200B;에 액세스 **찾아보기**.

![고객 프로필](./images/homemenu.png)

No painel Visualizador de perfil no seu site, você pode encontrar a visão geral da identidade. Cada id está vinculada a um namespace.

![고객 프로필](./images/identities.png)

No painel Visualizador de perfil, agora você pode ver uma는 semelante a seguinte를 식별합니다.

| 네임스페이스 | 신원 |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 19428085896177382402834560825640259081 |

Com a Adobe Experience Platform, todos os ID são igualmente importantes. Anteriormente, o ECID era o ID importante no contextto da Adobe e todos os outros IDs estavam vinculados ao ECID em uma relação hierárquica. Com a Adobe Experience Platform, isso mudou e cada ID pode ser considerado um identificador primário.

Normamente, o identificador primário depende do contexto. Se você pergentar ao seu 콜 센터: **Qual é o ID mais importante?** Eles provavelmente responderão: **o número de telefone!** Mas se você pergentar à sua equipe de CRM, eles responderão: **o endereço de email!** A Adobe Experience Platform entende essa complexidade e gerencia isso para você. Cada aplicativo, seja um aplicativo da Adobe ou não, se comunicará com a Adobe Experience Platform referindo-se ao ID consideram principal. E simplesmente funciona.

Para o campo **ID 네임스페이스**, selectione **ECID** e para o campo **ID 값** insira o ECID que você pode encontrar no painel Visualizador de perfil do site do Bootcamp. **보기**&#x200B;를 클릭합니다. Você verá seu perfil na lista. **프로필 ID** para abrir seu perfil을 클릭합니다.

![고객 프로필](./images/popupecid.png)

Agora você tem uma visão geral de alguns **Atributos de perfil** importantes do seu perfil de cliente.

![고객 프로필](./images/profile.png)

Accesse **Events**, onde você pode ver as entradas de cada evento de experiência vinculado ao seu Perfil.

![고객 프로필](./images/profileee.png)

Por fim, opção de 메뉴 **세그먼트 멤버십**&#x200B;에 액세스하세요. Agora você verá todos os segmentos que se qualificam para este perfil.

![고객 프로필](./images/profileseg.png)

Agora vamos criar um novo segmento que permitrá que você experiência do cliente para um cliente anônimo ou conheido를 개인화합니다.

Próxima etapa: [1.3 Crie um segmento - UI](./ex3.md)

[레토르나르 파라 플루소 데 우수아리오 1](./uc1.md)

[레토르나르 파라 토도스](../../overview.md)
