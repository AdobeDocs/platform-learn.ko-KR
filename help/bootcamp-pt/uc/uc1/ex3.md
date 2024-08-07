---
title: 부트캠프 - 실시간 고객 프로필 - 세그먼트 만들기 - UI - 브라질
description: 부트캠프 - 실시간 고객 프로필 - 세그먼트 만들기 - UI - 브라질
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Segments
exl-id: 9b8d93b5-5bed-4600-8602-b438a0893612
source-git-commit: ee5c0af17c12f1d90774a3a4150c9788e2368e39
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 2%

---

# 1.3 크림 세그멘토 - UI

Neste exercício, você irá criar um segmento usando o Construtor de Segmentos da Adobe Experience Platform.

## 히스토리아

[Adobe Experience Platform](https://experience.adobe.com/platform)에 액세스합니다. Depois de fazer 로그인, você irá acesssar a página inicial da Adobe Experience Platform.

![데이터 수집](./images/home.png)

Antes de continar, você precisa selectionar um **sandbox**. 사용자 selectionado é ``Bootcamp``을(를) 샌드박스로 설정하지 마십시오. É possível fazer siso clicando no texto **[!UICONTROL 프로덕션 제품]** na linha azul na parte superior da tela. Depois de seleionar o sandbox apropriado, você verá a a tela mudando e agora você está em seu [!UICONTROL sandbox] dedicado.

![데이터 수집](./images/sb1.png)

메뉴가 없습니다. **세그먼트**&#x200B;에 액세스하십시오. Nesta página, você tem uma visão geral de todos os segmentos existentes. Clique no botão + Criar segmento para começar a criar um novo segmento.

![세그먼테이션](./images/menuseg.png)

Quando estimator no novo constructor de segmentos, você irá perceber imediatamente a opção de menu **속성** e a referência do **XDM 개별 프로필**.

![세그먼테이션](./images/segmentationui.png)

Como o XDM é a linguagem que alimenta o setor de experiência, o XDM também é a base para o o constructor de segmentos. Todos os dados ingeridos na plataforma devem ser mapeados em relação XDM e, portanto, todos os dados se tornam parte do mesmo modelo de dados, independentemente da origem deses dados. Isso oferece uma grande vantagem ao criar segmentos, pois a partir dessa interface do usuário do constructor de segmento, é posível combinar dados de qualquer oregem no mesmo fluxo de trabalho. Os segmentos criados no Constructor de segmentos podem ser experiados para soluções como Adobe Target, Adobe Campaign e Adobe Audience Manager para ativazão.

Agora você precisa criar um segmento de todos os clientes que visualizaram o produto **Real-Time CDP**.

Para construir este segmento, você precisa adicionar um evento de experiência. Você pode encontar todos os Eventos de experience nicando no ícone **이벤트** na barra de 메뉴 **필드**.

![세그먼테이션](./images/findee.png)

Em seguida, você verá o nó **XDM ExperienceEvents**&#x200B;이(가) 우수하지 않습니다. **XDM ExperienceEvent**&#x200B;을(를) 클릭합니다.

![세그먼테이션](./images/see.png)

**제품 목록 항목**&#x200B;에 액세스합니다.

![세그먼테이션](./images/plitems.png)

**이름**&#x200B;을(를) 선택하십시오 e asset e solte o objeto **이름** do menu à esquerda na tela do constructor de segmentos na seção **Events**. Em seguida, o seguinte será exibido:

![세그먼테이션](./images/eewebpdtlname.png)

O parâmetro de comparação deve ser **equals** e, campo de entrada 없음, insira **실시간 CDP**.

![세그먼테이션](./images/pv.png)

Sempre que que adicionar um elemento ao constructor de segmentos, você pode clicar no botão **Refresh Estimate** para obter uma nova estimativa da população em seu segmento.

![세그먼테이션](./images/refreshest.png)

**평가 메서드**, **Edge**&#x200B;을(를) 선택하십시오.

![세그먼테이션](./images/evedge.png)

Por fim, vamos dar um nome ao seu segmento e salvá-lo.

Como modelo de nomenclatura, 사용:

- `seuSobrenome - Interest in Real-Time CDP`

Em seguida, clique no botão **저장하고 닫기** para salvar seu segmento.

![세그먼테이션](./images/segmentname.png)

Agora você irá retornar à página de visão geral do segmento, onde verá uma visualizaão de amostra dos perfis de clientes que se qualificam para o seu segmento.

![세그먼테이션](./images/savedsegment.png)

Agora você pode continar no próximo exercício e usar seu segmento com o Adobe Target.

Próxima etapa: [1.4 Ação: envie seu segmento para o Adobe Target](./ex4.md)

[레토르나르 파라 플루소 데 우수아리오 1](./uc1.md)

[레토르나르 파라 토도스](../../overview.md)
