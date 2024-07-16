---
title: Bootcamp - Real-time CDP - 세그먼트 작성 및 조치 - 세그먼트를 DV360으로 전송 - 브라질
description: Bootcamp - Real-time CDP - 세그먼트 작성 및 조치 - 세그먼트를 DV360으로 전송 - 브라질
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
feature: Destinations
exl-id: acb32859-6f82-44e0-8948-a045a9fe2afe
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 1%

---

# 1.5 아상: 앙비에 세그멘토 파라 오 Facebook

[Adobe Experience Platform](https://experience.adobe.com/platform)에 액세스합니다. Depois de fazer 로그인, você irá acesssar a página inicial da Adobe Experience Platform.

![데이터 수집](./images/home.png)

Antes de continar, você precisa selectionar um **sandbox**. O nome do sandbox a ser selectionado é Bootcamp. É possível fazer siso clicando no texto **[!UICONTROL 프로덕션 제품]** na linha azul na parte superior da tela. Depois de seleionar o sandbox apropriado, você verá a a tela mudando e agora você está em seu [!UICONTROL sandbox] dedicado.

![데이터 수집](./images/sb1.png)

메뉴 없음 à esquerda, vá para **대상** e, em seguida, vá para **카탈로그**. **대상 카탈로그**&#x200B;의 Você verá o. Em **대상**, 문자 **Facebook 사용자 지정 대상**&#x200B;에서 em **세그먼트 활성화**&#x200B;를 클릭합니다.

![RTCDP](./images/rtcdpgoogleseg.png)

**bootcamp-facebook**&#x200B;에서 하나를 선택하십시오. em **다음**&#x200B;을 선택하십시오.

![RTCDP](./images/rtcdpcreatedest2.png)

Na lista de segmentos disponíveis, segmento que você criou no exercício anterior의 셀렉시오네. **다음**&#x200B;을 클릭합니다.

![RTCDP](./images/rtcdpcreatedest3.png)

Na página **매핑**, verifique se a caixa de seleção **변환 적용** está marcada. **다음**&#x200B;을 클릭합니다.

![RTCDP](./images/rtcdpcreatedest4a.png)

**세그먼트 일정**&#x200B;에서 **대상의 원본**&#x200B;을(를) 선택하십시오. **고객에서 직접**&#x200B;을(를) 정의합니다. **다음**&#x200B;을 클릭합니다.

![RTCDP](./images/rtcdpcreatedest4.png)

Por fim, na página **검토**, 클릭 em **완료**.

![RTCDP](./images/rtcdpcreatedest5.png)

Seu segmento agora está vinculado aos Públicos Personalizados do Facebook. Sempre que um cliente se qualificar para esse segmento, um sinal será venado lado do servidor (server-side) do Facebook para incluir esse cliente no Público Personalizado no lado Facebook.

No Facebook , você encontrará seu segmento da Adobe Experience Platform em Públicos Personalizados:

![RTCDP](./images/rtcdpcreatedest5b.png)

Agora você pode ver seu público personalizado aparecer no Facebook:

![RTCDP](./images/rtcdpcreatedest5a.png)

[레토르나르 파라 플루소 데 우수아리오 1](./uc1.md)

[레토르나르 파라 토도스](../../overview.md)
