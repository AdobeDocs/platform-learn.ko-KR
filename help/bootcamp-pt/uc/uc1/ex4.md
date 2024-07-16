---
title: Bootcamp - 실시간 CDP - 세그먼트 구축 및 조치 - 세그먼트를 Adobe Target으로 보내기 - 브라질
description: Bootcamp - 실시간 CDP - 세그먼트 구축 및 조치 - 세그먼트를 Adobe Target으로 보내기 - 브라질
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
solution: Experience Platform, Target
feature: Segments, Integrations
exl-id: 862afd4c-1b6c-48fe-bc1f-967c065642e0
source-git-commit: ee5c0af17c12f1d90774a3a4150c9788e2368e39
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---

# 1.4 아상: 앙비에 세그멘토 파라 오 Adobe Target

[Adobe Experience Platform](https://experience.adobe.com/platform)에 액세스합니다. Depois de fazer 로그인, você irá acesssar a página inicial da Adobe Experience Platform.

![데이터 수집](./images/home.png)

Antes de continar, você precisa selectionar um **sandbox**. O nome do sandbox a ser selectionado é Bootcamp. É possível fazer siso clicando no texto **[!UICONTROL 프로덕션 제품]** na linha azul na parte superior da tela. Depois de seleionar o sandbox apropriado, você verá a a tela mudando e agora você está em seu [!UICONTROL sandbox] dedicado.

![데이터 수집](./images/sb1.png)

## 1.4.1 Active seu segmento para o destino do Adobe Target

O Adobe Target está disvonível como um destino do CDP em real. Adobe Target에 대한 Para 구성 sua integrção com, **대상**&#x200B;에 액세스 **카탈로그**.

**카테고리** 메뉴에서 **Personalization**&#x200B;을(를) 클릭합니다. Você verá o cartão de destino do **Adobe Target**. **세그먼트 활성화**&#x200B;를 클릭합니다.

![시간](./images/atdest1.png)

대상 ``Bootcamp Target``을(를) 선택한 후 **다음**&#x200B;을(를) 클릭합니다.

![시간](./images/atdest3.png)

Na lista de segmentos disponíveis, selecione o segmento que você criou em [1.3 Crie um segmento](./ex3.md), com o nome `yourLastName - Interest in Real-Time CDP`. Em seguida, **다음**&#x200B;을 클릭합니다.

![시간](./images/atdest8.png)

나 프록시마 파기나, **다음**&#x200B;을 클릭합니다.

![시간](./images/atdest9.png)

**완료**&#x200B;를 클릭합니다.

![시간](./images/atdest10.png)

Seu segmento agora está ativado para o Adobe Target.

![시간](./images/atdest11.png)

>[!IMPORTANT]
>
>Imediatamente após criar seu destino do Adobe Target no Real-Time CDP, pode levar até uma hora para que o destino seja ativado. Este um tempo de espera único devido à definição da configuração de 백 엔드. Depois que o tempo de espera inicial de 1 hora e a configuração do 백 엔드 forem concluídos, os segmentos de borda recém-adicionados que são enviados ao destino do Adobe Target estarão disponíveis para segmentação em real.

## 1.4.2 Adobe Target에서 sua atividade 구성

Agora que seu segmento Real-Time CDP está configurado para ser enviado Adobe Target, é posível configurar sua atividade de Segmentação por experiência no Adobe Target. Neste exercício, você irá configurar uma atividade baseada no Visual Experience Composer.

파기나 이니셜 다 Adobe Experience Cloud acessando [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/)에 액세스하십시오. **대상** 파라 버전을 클릭합니다.

![RTCDP](./images/excl.png)

기본적으로 **Adobe Target**을(를) 하고 아티비다데스(atividades)가 존재하므로 보테 베라 토다(você verá todas)를 사용합니다.
**+ 활동 만들기** 파라 크리아 uma nova atividade를 클릭합니다.

![RTCDP](./images/exclatov.png)

**경험 타깃팅**&#x200B;을 선택하세요.

![RTCDP](./images/exclatcrxt.png)

**활동 URL** 쉼표 `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`, mas, antes disso, substituta XX por um número entre 01 e 60을 정의합니다. **Visual**&#x200B;을(를) 선택합니다.

>[!IMPORTANT]
>
>Cada participante da capacitação deve usar uma página da Web separada para evitar a colisão de várias experiências do Adobe Target. É possível escoher uma página da Web e encontrar a URL accessando: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as páginas compartilham a mesma URL base e terminam com o número do participante.
>
>Por 예시, 또는 참가자 1은 URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`을(를), 또는 참가자 30은 URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`을(를) 사용합니다.

**AT Bootcamp** 작업 영역에서 하나를 선택하십시오.

**다음**&#x200B;을 클릭합니다.

![RTCDP](./images/exclatcrxtdtlform.png)

Agora você está no Visual Experience Composer. Pode levar de 20 a 30 segundos até o site esteja compleetamente carregado.

![RTCDP](./images/atform1.png)

Atualmente, o público padrão são **모든 방문자**. **모든 방문자**&#x200B;를 클릭합니다. **대상 변경**&#x200B;을 클릭합니다. **3점**

![RTCDP](./images/atform3.png)

Agora você está vendo a lista de públicos disponíveis, e o segmento da Adobe Experience Platform que você anterious e enviou ao Adobe Target agora faz parte dessa lista. Selecione o segmento que você criou anteriormente na Adobe Experience Platform. **대상자 할당**&#x200B;을 클릭합니다.

![RTCDP](./images/exclatvecchaud.png)

Seu segmento da Adobe Experience Platform agora faz parte dessa Atividade de segmentação por experiência.

![RTCDP](./images/atform4.png)

Antes de alterar a imagem principal, você deve clicar em **모두 허용** 배너 드 쿠키가 없습니다.

Para isso, vá para **찾아보기**

![RTCDP](./images/cook1.png)

Em seguida입니다. **모두 허용**&#x200B;을 클릭하세요.

![RTCDP](./images/cook2.png)

Em seguida, retorne para **작성**.

![RTCDP](./images/cook3.png)

Agora vamos mudar a imagem principal na página inicial do site. Clique na imagem principal padrão no site, selectione **이미지**&#x200B;에서 **콘텐츠 바꾸기**&#x200B;를 클릭합니다.

![RTCDP](./images/atform5.png)

Pesquise o arquivo de imagem **rtcdp.png**. **저장**&#x200B;을 클릭합니다.

![RTCDP](./images/atform6.png)

Você verá a nova experiência com a nova imagem para o seu Público seleionado

![RTCDP](./images/atform7.png)

Clique no título da sua atividade no canto superior esquerdo para renomeá-la.

![RTCDP](./images/exclatvecname.png)

파라 이름, 사용:

- `seuSobrenome - RTCDP - XT (VEC)`

**다음**&#x200B;을 클릭합니다.

![RTCDP](./images/atform8.png)

**다음**&#x200B;을 클릭합니다.

![RTCDP](./images/atform8a.png)

**목표 및 설정**&#x200B;에 액세스, **목표 지표**&#x200B;에 액세스

![RTCDP](./images/atform9.png)

메타 주체 코모 **참여** - **사이트에서 보낸 시간**&#x200B;을 정의합니다. **저장 및 닫기**&#x200B;를 클릭합니다.

![RTCDP](./images/vec3.png)

Agora você está na página **활동 개요**. 보테아인다 프레시사 아티바르 수아 아티비다데

![RTCDP](./images/atform10.png)

**활성화**&#x200B;를 선택하면 캠페인 **비활성**&#x200B;을(를) 클릭할 수 없습니다.

![RTCDP](./images/atform11.png)

Você receberá uma confirmmação visual de que sua atividade agora está ativa.

![RTCDP](./images/atform12.png)

Agora sua atividade está ativa e pode ser testada 사이트는 부트캠프를 하지 않습니다.

Se agora você voltar ao seu site de demonstração e visitar a página do produto para **Real-Time CDP**, você se qualificará instantaneamente para o segmento que criou e verá a atividade do Adobe Target exibida na página inicial em tempo real.

>[!IMPORTANT]
>
>Cada participante da capacitação deve usar uma página da Web separada para evitar a colisão de várias experiências do Adobe Target. É possível escoher uma página da Web e encontrar a URL accessando ao 링크: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as páginas compartilham a mesma URL base e terminam com o número do participante.
>
>Por 예시, o participante 1 deve usar a `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, o participante 30 deve usar a URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

Próxima etapa: [1.5 Ação: envie seu segmento para o Facebook](./ex5.md)

[레토르나르 파라 플루소 데 우수아리오 1](./uc1.md)

[레토르나르 파라 토도스](../../overview.md)
