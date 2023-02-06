---
title: Bootcamp - 실시간 고객 프로필 - 세그먼트 만들기 - UI - 브라질
description: Bootcamp - 실시간 고객 프로필 - 세그먼트 만들기 - UI - 브라질
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 2%

---

# 1.3 Cribe segmento - UI

네스트 연습시오, 보레 이라 크림 세그멘토 우산도 오 시멘토스 드 Adobe Experience Platform

## 히스토리아

Acesse [Adobe Experience Platform](https://experience.adobe.com/platform). 데포이스 데 파저 로그인, 보히라 아세사(Voqiera acessar a página initial da da Adobe Experience Platform)

![데이터 수집](./images/home.png)

낭트 드 티니어, 보어 정밀 선택 **샌드박스**. ONome do sandbox a ser selecionado ``Bootcamp``. É Poishivel 페이저는 Clicacando no texto **[!UICONTROL 프로덕션 제품]** 나린하 아줄 나파테 수페리어 다 데라 데포이스 드 셀레치오나 샌드박스 고유도, 보스케라 아 데라 무다 아고라 에삼 [!UICONTROL 샌드박스] 전용.

![데이터 수집](./images/sb1.png)

Esquerda 메뉴 없음, Acesse **세그먼트**. 네스타 파지나, 보테 테우마 비샹거 데 토도스 세그멘토스가 존재해요. Clinque no botang + Criar segmento para começar는 Criar nova segmento의 중심입니다.

![세그먼테이션](./images/menuseg.png)

Quando estimator de segmentos, voke irah perceber imediatamente a opçao de 메뉴 **속성** 레퍼런시아 **XDM 개별 프로필**.

![세그먼테이션](./images/segmentationui.png)

Como o XDM é는 링귀아그엠 키쿠멘타(Lineagem quickenta) 또는 De experiencia, XDM tamém é a base para o de segmentos. Todos os dadoos ingeridos na platform devem ser mapeados em relaçao XDM e, poranto, todos os dados se tornam parte do mesmo modelo de dados, independent da origins dedos에서 dedes를 생성합니다. Isso oferece uma grande vantagem ao criar segmentos, pois a partitor interface do usuário do constructor de segmento, é combinados de qualquer origem on mesmo fluxo de trabalho. Os 세그멘토스를 마우스로 가리킨 후 세그먼트멘토스를 마우스로 하는 Envaado soluçules como Adobe Target, Adobe Campaign e Adobe Audience Manager para ativaçao를 클릭합니다.

Agora voc precisa crim segmento de todos os clientes que visualizaram o produto **Real-Time CDP**.

파라샤세게세그멘토, 보크리시오나르 에벤토 드 경험. 보려 **이벤트** 바르라 데 메뉴 **필드**.

![세그먼테이션](./images/findee.png)

Em 세구이다, 보스케베라 오 노 **XDM ExperienceEvents** 니벨보다 우수하세요. Clique em **XDM ExperienceEvent**.

![세그먼테이션](./images/see.png)

Acesse **제품 목록 항목**.

![세그먼테이션](./images/plitems.png)

셀레치온 **이름** Arraste Solte o objto **이름** 메뉴 à esquerda na tela do constructor de segmentos na seçao **이벤트**. Em 세구이다, Seguinte serla exibido:

![세그먼테이션](./images/eewebpdtlname.png)

오 파라메트로 드 비교라상 데베 **다음과 같음** e- campo de entrada, intra **실시간 CDP**.

![세그먼테이션](./images/pv.png)

세크레 아디치오나르 구테르 세그멘토스 드 세그멘토스, 보케 포데 클리커 노 보탕 **예상 새로 고침** 파라 오베르마 노바 견적 활동(da pomaçao em segmento)

![세그먼테이션](./images/refreshest.png)

파라 **평가 방법**, selecione **Edge**.

![세그먼테이션](./images/evedge.png)

Por fim, vamos dar um nome ao seu segmmento e salsa-lo.

Como modelo de nomenclatura, 사용:

- `yourLastName - Interest in Real-Time CDP`

Em Seguida, Client no botang **저장 후 닫기** para salvar segmento.

![세그먼테이션](./images/segmentname.png)

아고라 보키라 레로나 대 파지나 데 비잔 게랄 두 세그멘토, 온데 베라 시각화 아모조 두 do perfis que se qualpicficam para o seu segmento.

![세그먼테이션](./images/savedsegment.png)

아고라 보케 포데 연속적인 프리시모 연습시오 우사 세우 세그멘토 com o Adobe Target.

프로시마 에타파: [1.4 아상: envie segmento para o Adobe Target](./ex4.md)

[레토나르 플루소 드 우시오 1](./uc1.md)

[레토날라 파라 토도스 오모두로스](../../overview.md)
