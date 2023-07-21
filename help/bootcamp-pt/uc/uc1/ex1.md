---
title: Bootcamp - 실시간 고객 프로필 - 알 수 없음에서 웹 사이트에 알려짐 - 브라질
description: Bootcamp - 실시간 고객 프로필 - 알 수 없음에서 웹 사이트에 알려짐 - 브라질
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 853a69d2-5dac-413d-bb40-ef29604a26ae
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 1%

---

# 1.1 Do desconheido ao conheido em nosso site

## Contexto

Adobe Experience Platform 데셈펜하 움 파펠 임포르탕테 네사 호르나다. A plataforma é o cérebro da comunicação, o **경험적 기록 시스템**.

Plataforma é um ambiente em que a palavra cliente engloba mais do que clientes conhecydos. Um visitante desconhecido no site também é um cliente do ponto de vista da Plataforma e, como tal, todo o comportamento de um visitante desconhecido também é enviado à Plataforma. Graças a essa abordagem, quando esse visitante eventualmente se torna um cliente conheido, uma marca também pode visualizar o que aconteceu antes daquele momento. Isso ajuda a partir de uma perspectiva de otimização de atribuição e experiência.

## 플루소 다 조르나다 두 클리엔테

액세스 [https://bootcamp.aepdemo.net](https://bootcamp.aepdemo.net). 클리크 **모두 허용**.

![DSN](./images/web8.png)

Clique no ícone do logotipo da Adobe no canto superior esquerdo da tela para abrir o Visualizador de perfil.

![데모](./images/pv1.png)

Verifique o painel do Visualizador de perfil e no Perfil do cliente em tempo real com o **EXPERIENCE CLOUD ID** como o identificador primário para este cliente que ainda é desconhecido.

![데모](./images/pv2.png)

Você também pode ver todos os Eventos de Experiência coletados com base no comportamento do cliente. A lista está vazia no momento, mas isso mudará em breve.

![데모](./images/pv3.png)

Accesse a opção de 메뉴 **애플리케이션 서비스** 제품 없음 선택 **Real-Time CDP**.

![데모](./images/pv4.png)

Você verá a página de detalhes do producto. 음 에벤토 데 experiencia 두 티포 **제품 보기** agora foi enviado para a Adobe Experience Platform usando a implementação do Web SDK que você revisou no Módulo 1. Abra o painel Visualizador de perfil e verifique seus **경험 이벤트**.

![데모](./images/pv5.png)

Accesse a opção de 메뉴 **애플리케이션 서비스** 제품 없음 선택 **Adobe Journey Optimizer**. Mais um Evento de experiencia foi experiado para a Adobe Experience Platform.

![데모](./images/pv7.png)

Abra o painel Visualizador de perfil. Agora você verá 2 Eventos de experiência do tipo **제품 보기**. Embora o comportamento seja anônimo, cada clique é rastreado e armazenado na Adobe Experience Platform. Depois que o cliente anônimo se tornar conhecido, poderemos mesclar todo o comportamento anônimo automicamente ao perfil conhecido.

![데모](./images/pv8.png)

Agora vamos analisar seu perfil de cliente e usar seu comportamento para personalizar sua experiencia do cliente no site.

프록시마 에타파: [1.2 Visualize seu próprio perfil de cliente em tempo real - UI](./ex2.md)

[레토르나르 파라 플루소 데 우수아리오 1](./uc1.md)

[레토르나르 파라 토도스](../../overview.md)
