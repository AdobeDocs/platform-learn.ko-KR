---
title: Bootcamp - 실시간 CDP - 세그먼트 구축 및 조치 - 세그먼트를 Adobe Target으로 보내기 - 브라질
description: Bootcamp - 실시간 CDP - 세그먼트 구축 및 조치 - 세그먼트를 Adobe Target으로 보내기 - 브라질
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 862afd4c-1b6c-48fe-bc1f-967c065642e0
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# 1.4 아상: 앙비에 세그멘토 파라 오 Adobe Target

액세스 [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer 로그인, você irá acesssar a página inicial da Adobe Experience Platform.

![데이터 수집](./images/home.png)

Antes de continar, você precisa selecionar um **샌드박스**. O nome do sandbox a ser selectionado é Bootcamp. 레 포시벨 파제 이스소 클리칸도 노 텍토 **[!UICONTROL 프로덕션 프로덕션]** 나 리냐 아줄 나 파르테 수페리어 다 텔라. Depois de seleionar o sandbox apropriado, você verá a a tela mudando e agora você está em seu [!UICONTROL 샌드박스] 헌신.

![데이터 수집](./images/sb1.png)

## 1.4.1 Active seu segmento para o destino do Adobe Target

O Adobe Target está disvonível como um destino do CDP em real. Para configurar sua integrção com o Adobe Target, Accesse **대상** e **카탈로그**.

클리크 **개인화** 메뉴 없음 **카테고리**. 보테베라오카르탕 데 데스티노 두 **Adobe Target**. 클리크 **세그먼트 활성화**.

![위치](./images/atdest1.png)

대상 선택 ``Bootcamp Target`` e 파벌 **다음**.

![위치](./images/atdest3.png)

Na lista de segmentos disponíveis, segiono segmento que você criou em [1.3 크림 세그멘토](./ex3.md), com o nome `yourLastName - Interest in Real-Time CDP`. Em seguida, clique em **다음**.

![위치](./images/atdest8.png)

나 프록시마 파기나, 클리크 엠 **다음**.

![위치](./images/atdest9.png)

클리크 **완료**.

![위치](./images/atdest10.png)

Seu segmento agora está ativado para o Adobe Target.

![위치](./images/atdest11.png)

>[!IMPORTANT]
>
>Imediatamente após criar seu destino do Adobe Target no Real-Time CDP, pode levar até uma hora para que o destino seja ativado. Este um tempo de espera único devido à definição da configuração de 백 엔드. Depois que o tempo de espera inicial de 1 hora e a configuração do 백 엔드 forem concluídos, os segmentos de borda recém-adicionados que são enviados ao destino do Adobe Target estarão disponíveis para segmentação em real.

## 1.4.2 Adobe Target에서 sua atividade 구성

Agora que seu segmento Real-Time CDP está configurado para ser enviado Adobe Target, é posível configurar sua atividade de Segmentação por experiência no Adobe Target. Neste exercício, você irá configurar uma atividade baseada no Visual Experience Composer.

에세세 아 파기나 원시적 다 Adobe Experience Cloud 아체산도 [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). 클리크 **Target** 파라 아브리르

![RTCDP](./images/excl.png)

나파기나의 원조 **Adobe Target**, atividades로 voê verá todas는 존재합니다.
클리크 **+ 활동 만들기** 파라 크리아르 uma nova atividade.

![RTCDP](./images/exclatov.png)

선택 항목 **경험 타기팅**.

![RTCDP](./images/exclatcrxt.png)

선택 항목 **비주얼** e defina **활동 URL** 코모 `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`, mas, antes disso, substituta XX por um número entre 01 e 60.

>[!IMPORTANT]
>
>Cada participante da capacitação deve usar uma página da Web separada para evitar a colisão de várias experiências do Adobe Target. É possível escoher uma página da Web e encontrar a URL acessando: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as páginas compartilham a mesma URL base e terminam com o número do participante.
>
>Por modeo, o participante 1 deve usar a URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, 또는 참가자 30은 URL을 사용합니다. `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

작업 영역 선택 **부트캠프에서**.

클리크 **다음**.

![RTCDP](./images/exclatcrxtdtlform.png)

Agora você está no Visual Experience Composer. Pode levar de 20 a 30 segundos até o site esteja compleetamente carregado.

![RTCDP](./images/atform1.png)

아투알멘테, 오 푸블리코 파드랑 상 **모든 방문자**. 클리크 nos **점 3개** 아오라도데 **모든 방문자** e clique em **대상 변경**.

![RTCDP](./images/atform3.png)

Agora você está vendo a lista de públicos disponíveis, e o segmento da Adobe Experience Platform que você anterious e enviou ao Adobe Target agora faz parte dessa lista. Selecione o segmento que você criou anteriormente na Adobe Experience Platform. 클리크 **대상자 할당**.

![RTCDP](./images/exclatvecchaud.png)

Seu segmento da Adobe Experience Platform agora faz parte dessa Atividade de segmentação por experiência.

![RTCDP](./images/atform4.png)

Antes de alterar a imagem principal, você deve clicar em **모두 허용** 쿠키를 삭제하는 배너가 없습니다.

Para isso, vá para **찾아보기**

![RTCDP](./images/cook1.png)

Em seguida, clique em **모두 허용**.

![RTCDP](./images/cook2.png)

Em seguida, 레토른 파라 **작성**.

![RTCDP](./images/cook3.png)

Agora vamos mudar a imagem principal na página inicial do site. Clique na imagem principal padrão no site, clique em **컨텐츠 바꾸기** e selectione **이미지**.

![RTCDP](./images/atform5.png)

페스키세오 아르키보 데 이마젬 **rtcdp.png**. 선택 e clique em **저장**.

![RTCDP](./images/atform6.png)

Você verá a nova experiência com a nova imagem para o seu Público seleionado

![RTCDP](./images/atform7.png)

Clique no título da sua atividade no canto superior esquerdo para renomeá-la.

![RTCDP](./images/exclatvecname.png)

파라 이름, 사용:

- `seuSobrenome - RTCDP - XT (VEC)`

클리크 **다음**.

![RTCDP](./images/atform8.png)

클리크 **다음**.

![RTCDP](./images/atform8a.png)

나파기나 **목표 및 설정**, 액세스 **목표 지표**.

![RTCDP](./images/atform9.png)

메타 주도자 코모 정의 **참여** - **사이트에서 보낸 시간**. 클리크 **저장 및 닫기**.

![RTCDP](./images/vec3.png)

아고라보사이에스타나파기나 **활동 개요**. 보테아인다 프레시사 아티바르 수아 아티비다데

![RTCDP](./images/atform10.png)

클리크 노 캄포 **비활성** e selectione **활성화**.

![RTCDP](./images/atform11.png)

Você receberá uma confirmmação visual de que sua atividade agora está ativa.

![RTCDP](./images/atform12.png)

Agora sua atividade está ativa e pode ser testada 사이트는 부트캠프를 하지 않습니다.

Se agora você voltar ao seu site de demonstração e visitar a página do produto para **Real-Time CDP**, você se qualificará instantaneamente para o segmento que criou e verá a atividade do Adobe Target exibida na página inicial em tempo real.

>[!IMPORTANT]
>
>Cada participante da capacitação deve usar uma página da Web separada para evitar a colisão de várias experiências do Adobe Target. É possível escoher uma página da Web e encontrar a URL acessando ao link: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as páginas compartilham a mesma URL base e terminam com o número do participante.
>
>Por modeo, o participante 1 deve usar a `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, 또는 참가자 30은 URL을 사용합니다. `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

프록시마 에타파: [1.5 아상: 앙비에 세그멘토 파라 오 Facebook](./ex5.md)

[레토르나르 파라 플루소 데 우수아리오 1](./uc1.md)

[레토르나르 파라 토도스](../../overview.md)
