---
title: Bootcamp - 실시간 CDP - 세그먼트 구축 및 조치 수행 - Adobe Target에 세그먼트 보내기 - 브라질
description: Bootcamp - 실시간 CDP - 세그먼트 구축 및 조치 수행 - Adobe Target에 세그먼트 보내기 - 브라질
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 020e9fb8a1d02b93e4e95a4274806c7926c02757
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# 1.4 아상: envie segmento para o Adobe Target

Acesse [Adobe Experience Platform](https://experience.adobe.com/platform). 데포이스 데 파저 로그인, 보히라 아세사(Voqiera acessar a página initial da da Adobe Experience Platform)

![데이터 수집](./images/home.png)

낭트 드 티니어, 보어 정밀 선택 **샌드박스**. OHome은 사용자 Selecionado Bootcamp를 샌드박스로 만듭니다. É Poishivel 페이저는 Clicacando no texto **[!UICONTROL 프로덕션 제품]** 나린하 아줄 나파테 수페리어 다 데라 데포이스 드 셀레치오나 샌드박스 고유도, 보스케라 아 데라 무다 아고라 에삼 [!UICONTROL 샌드박스] 전용.

![데이터 수집](./images/sb1.png)

## 1.4.1 Active segmento para destination do Adobe Target

O Adobe Target 에스타 디스포니벨 데스티노 도 CDP em 템포를 실제로 수행합니다. Para configuration sua integraang com o Adobe Target, acesse **대상** e **카탈로그**.

Clique em **개인화** 메뉴 없음 **카테고리**. 보스케라 오 카탕 데스티노 도 **Adobe Target**. Clique em **세그먼트 활성화**.

![AT](./images/atdest1.png)

셀레치온 오디티노 ``Bootcamp Target`` eClique **다음**.

![AT](./images/atdest3.png)

Na lista de segmentos dispooniveis, selecione o segmento que voke crime [1.3 Crime 세그멘토](./ex3.md), com o nome `yourLastName - Interest in Real-Time CDP`. Em Seguida, Client em **다음**.

![AT](./images/atdest8.png)

나프시마 파지나, 클리크 **다음**.

![AT](./images/atdest9.png)

Clique em **완료**.

![AT](./images/atdest10.png)

Seu Segmento agera esta ativado para o Adobe Target.

![AT](./images/atdest11.png)

>[!IMPORTANT]
>
>Imediatamente aplus criar seu destino do Adobe Target no Real-Time CDP, pode levaraté uma hora que o destino seja ativado. 에스테레 엄템포 데 에스페라 니코 데비도 아 디치카오 다 구성상 뒤쪽 끝입니다. 파라 세그멘테이션의 힘 데 에스페라 산 데 1 호라 에 구성 아상 두 끝 포어 concluids, 시그멘토스 드 보르다 궁상 아디시오아오 데스티도 Adobe Target 에스타라상 디스타라상 파르 디스타르메테오 등은 파라 세그멘테이션의 레알

## 1.4.2 sua atividade baseada em coorado do Adobe Target 구성

Real-Time CDP 에스타타구라타족 환경(Agora que segmento esta configurado para envirau ao Adobe Target, é ushivel configuration sua ativade de Segmentaçao 또는 experiencia no Adobe Target. 네스트 연습시오, Vokee irah configuar ativvidade baseada(시각적 경험 작성기)

카지나 인시던트 다 Adobe Experience Cloud 아체산도 [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Clique em **Target** 파라 브리르

![RTCDP](./images/excl.png)

설정 **Adobe Target** homepage에는 기존의 모든 활동이 표시됩니다.
클릭 **+ 활동 만들기** 새 활동을 만들려면
나페지나도 **Adobe Target**아티비데즈(ativedentes)로 음성 베라 토다스
Clique em **+ 활동 만들기** 파라 루마 노바 타이비데이드

![RTCDP](./images/exclatov.png)

셀레치온 **경험 타깃팅**.

![RTCDP](./images/exclatcrxt.png)

셀레치온 **시각적** e 정의 **활동 URL** como `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`, mas, antes disso, substittua XX por um numero entre 01 e 30

>[!IMPORTANT]
>
>카다피분칸테 다 커패시타상 데베 우슈마 파지나다 웹 세퍼레이다 파라 에브리타아 a colisao de varias experiencias do Adobe Target. URL Acessando에 대한 É 보유yvel escoherer página da Web e encontrolar: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as páginas compartilham a mesma URL base e terminam com o numero do participante.
>
>모형의 경우 또는 참가자 1은 URL을 사용합니다 `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, 또는 30에서 URL을 사용하는 경우 `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

Selecione o 작업 공간 **AT Bootcamp**.

Clique em **다음**.

![RTCDP](./images/exclatcrxtdtlform.png)

시각적 경험 작성기의 아고라 보스케입니다. Pode Levar de 20 a 30 segundos até o site estesja completempanote carregado. 30 segondos atque o site estesamente.

![RTCDP](./images/atform1.png)

아투알멘테, 오 푸블리코 파드라오 **모든 방문자**. 클리크 노스 **세 점** 아요라도드 **모든 방문자** e-clique em **대상 변경**.

![RTCDP](./images/atform3.png)

아고라 보케스타 벤도 a lista de publicos dispoonveis, e o segmento da Adobe Experience Platform que voccriou anteriormente enao agora faz parte lista. 셀레치온 오 세그멘토 음성 변환 및 Adobe Experience Platform Clique em **대상 할당**.

![RTCDP](./images/exclatvecchaud.png)

세우 세그멘토 다 Adobe Experience Platform 아고라 파즈 파르테사 아티비데이드 드 드 세그멘타상 또는 경험 엔시아.

![RTCDP](./images/atform4.png)

Antes de alterar a imagem principal, voke deve clicar em **모두 허용** 배너 de 쿠키가 없습니다.

파라, 바파라 **찾아보기**

![RTCDP](./images/cook1.png)

Em Seguida, Client em **모두 허용**.

![RTCDP](./images/cook2.png)

Em Seguida, reggne para **작성**.

![RTCDP](./images/cook3.png)

Agora Vamos muda는 이미지 주체 na página initial do site입니다. Clique na imagem 주체 파드로는 사이트에 없습니다. client em **컨텐츠 바꾸기** e selecione **이미지**.

![RTCDP](./images/atform5.png)

페스퀴즈 오 아르퀴보 드 이미지 **rtcdp.png**. 셀레치온 e clique em **저장**.

![RTCDP](./images/atform6.png)

Vokheverá a nova experiencia com a nova imagem para o Publico selecionado

![RTCDP](./images/atform7.png)

클리크노타툴로다티비데이드 노 칸토 에케르도 파라 레노메아-라

![RTCDP](./images/exclatvecname.png)

Para o nhome, use:

- `yourLastName - RTCDP - XT (VEC)`

Clique em **다음**.

![RTCDP](./images/atform8.png)

Clique em **다음**.

![RTCDP](./images/atform8a.png)

나파지나 **목표 및 설정**, **목표 지표**.

![RTCDP](./images/atform9.png)

메타 계정 코모 정의 **참여** - **사이트에서 보낸 시간**. Clique em **저장 및 닫기**.

![RTCDP](./images/vec3.png)

아고라 보스케나 파지나 **활동 개요**. 보카인다 정밀 아티바 수아 아티비데이드.

![RTCDP](./images/atform10.png)

클리크 노 캄포 **비활성** e selecione **활성화**.

![RTCDP](./images/atform11.png)

Vokheiberá confirmmaçao visual de que sua atvidade agora esta ativa.

![RTCDP](./images/atform12.png)

Agora sua atvidade esta atva e pode user testada는 bootcamp를 수행하지 않습니다.

Se agora vokal voltar au seu site de 데드라상 e 비시타 a página do produto para **Real-Time CDP**, vokse qualficará for segmento que cruou e verla a atividde do Adobe Target exibida na página initial em tempo real.

>[!IMPORTANT]
>
>카다피분칸테 다 커패시타상 데베 우슈마 파지나다 웹 세퍼레이다 파라 에브리타아 a colisao de varias experiencias do Adobe Target. URL acessando 링크를 제어하려면 É Positivivel escoluma página da Web e 를 사용합니다. [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as páginas compartilham a mesma URL base e terminam com o numero do participante.
>
>Por 예제, 또는 Partitionante 1 사용 안 함 `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, 또는 30에서 URL을 사용하는 경우 `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

프로시마 에타파: [1.5 조치 수행: facebook에 세그먼트 보내기](./ex5.md)

[레토나르 플루소 드 우시오 1](./uc1.md)

[레토날라 파라 토도스 오모두로스](../../overview.md)
