---
title: 부트캠프 - 실시간 고객 프로필 - 세그먼트 만들기 - UI - 브라질
description: 부트캠프 - 실시간 고객 프로필 - 세그먼트 만들기 - UI - 브라질
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 9b8d93b5-5bed-4600-8602-b438a0893612
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 2%

---

# 1.3 크림 세그멘토 - UI

Neste exercício, você irá criar um segmento usando o Construtor de Segmentos da Adobe Experience Platform.

## 히스토리아

액세스 [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer 로그인, você irá acesssar a página inicial da Adobe Experience Platform.

![데이터 수집](./images/home.png)

Antes de continar, você precisa selecionar um **샌드박스**. 샌드박스 a ser selectionado é ``Bootcamp``. 레 포시벨 파제 이스소 클리칸도 노 텍토 **[!UICONTROL 프로덕션 프로덕션]** 나 리냐 아줄 나 파르테 수페리어 다 텔라. Depois de seleionar o sandbox apropriado, você verá a a tela mudando e agora você está em seu [!UICONTROL 샌드박스] 헌신.

![데이터 수집](./images/sb1.png)

메뉴 없음, 에스케다 **세그먼트**. Nesta página, você tem uma visão geral de todos os segmentos existentes. Clique no botão + Criar segmento para começar a criar um novo segmento.

![세그먼테이션](./images/menuseg.png)

Quando estimer no novo constructor de segmentos, você irá perceber imediatamente a opção de menu **속성** 레페렌시아 **XDM 개별 프로필**.

![세그먼테이션](./images/segmentationui.png)

Como o XDM é a linguagem que alimenta o setor de experiência, o XDM também é a base para o o constructor de segmentos. Todos os dados ingeridos na plataforma devem ser mapeados em relação XDM e, portanto, todos os dados se tornam parte do mesmo modelo de dados, independentemente da origem deses dados. Isso oferece uma grande vantagem ao criar segmentos, pois a partir dessa interface do usuário do constructor de segmento, é posível combinar dados de qualquer oregem no mesmo fluxo de trabalho. Os segmentos criados no Constructor de segmentos podem ser experiados para soluções como Adobe Target, Adobe Campaign e Adobe Audience Manager para ativazão.

Agora você precisa criar um segmento de todos os clientes que visualizaram o produto **Real-Time CDP**.

Para construir este segmento, você precisa adicionar um evento de experiência. Você pode encontrar todos os Eventos de experiência clicando no ícone **이벤트** 나 바라 데 메뉴 **필드**.

![세그먼테이션](./images/findee.png)

Em seguida, você verá o nó **XDM 경험 이벤트** 니벨 수페리어 클리크 **XDM ExperienceEvent**.

![세그먼테이션](./images/see.png)

액세스 **제품 목록 항목**.

![세그먼테이션](./images/plitems.png)

선택 항목 **이름** e arraste e solte o objeto **이름** do menu à esquerda na tela do constructor de segmentos na seção **이벤트**. Em seguida, o seguinte será exibido:

![세그먼테이션](./images/eewebpdtlname.png)

오 파라메트로 데 콤파라상 데베 세르 **다음과 같음** e, no campo de entrada, insira **Real-time CDP**.

![세그먼테이션](./images/pv.png)

Sempre que adicionar um elemento ao constructor de segmentos, você pode clicar no botão **예상 새로 고침** para obter uma nova estimativa da população em seu segmento.

![세그먼테이션](./images/refreshest.png)

파라 **평가 방법**, 선택 항목 **Edge**.

![세그먼테이션](./images/evedge.png)

Por fim, vamos dar um nome ao seu segmento e salvá-lo.

Como modelo de nomenclatura, 사용:

- `seuSobrenome - Interest in Real-Time CDP`

Em seguida, 클리크 노 보탕 **저장 및 닫기** 파라 살바르 세그멘토

![세그먼테이션](./images/segmentname.png)

Agora você irá retornar à página de visão geral do segmento, onde verá uma visualizaão de amostra dos perfis de clientes que se qualificam para o seu segmento.

![세그먼테이션](./images/savedsegment.png)

Agora você pode continar no próximo exercício e usar seu segmento com o Adobe Target.

프록시마 에타파: [1.4 아상: 앙비에 세그멘토 파라 오 Adobe Target](./ex4.md)

[레토르나르 파라 플루소 데 우수아리오 1](./uc1.md)

[레토르나르 파라 토도스](../../overview.md)
