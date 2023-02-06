---
title: Bootcamp - 물리적 및 디지털 혼합 - Journey Optimizer 여정 및 푸시 만들기 - 브라일로 알림
description: Bootcamp - 물리적 및 디지털 혼합 - Journey Optimizer 여정 및 푸시 만들기 - 브라일로 알림
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 020e9fb8a1d02b93e4e95a4274806c7926c02757
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 2%

---

# 3.3 Crie sua jornada e notificaang 푸시

네스트 운동시오, 보테 이라오 는 조나다 어 멘사그엠 정밀 카시오나다 알구에마 인슈마 시날리잔(비콘) 우산도 아피카티보 모벨

Adobe Journey Optimizer Acessando에서 패사 로그인 [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Vokheserá rereconado para visualizaçao da **홈** Journey Optimizer 없음. Primeiro, verifique se voca esto o sandbox correto. O nome do sandbox que deve ser usado `Bootcamp`. Para alternar de um sandbox para, clique em **Prod** lista를 선택합니다. 네스트 모예, 노메 도 샌드박스 é **Bootcamp**. Vokheestarala na visualizahan da **홈**  샌드박스 보내기 `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 설명 아하라

메뉴 항목 없음, 클릭 **여정**. Em Seguida, Client em **여정 만들기** 파라 루마 노바 조나다

![ACOP](./images/createjourney.png)

Vokheverá uma tela de jornada vazia.

![ACOP](./images/journeyempty.png)

운동 금지 전낭, **이벤트**. 보네오우오에벤토 `yourLastNameBeaconEntryEvent` e치슈투유 `yourLastName` 펠로 세우 소브레놈 에벤토:

![ACOP](./images/eventdone.png)

아고라 보테 데비는 evento eko o início desta jornada를 고려합니다. 보테 포데 페저소 인도 파라 오 라도 에케르도 다 텔라 에프쿠란도 펠로 에벤토 나리스타 드 에벤토스

![ACOP](./images/eventlist.png)

셀레치온 세우 evento, arrite e solte o evento na tela de jornada. 수아 조나라 아고라 데베 세멜한테 아오 세구인테 경. Clique em **확인** 파라 살바도르 아타수

![ACOP](./images/journeyevent.png)

코모 세군다 에타파 다 조나다, 보레 데디치오나르 아상 **푸시**. Vá para o lado esquerdo da tela para **작업**, 셀레치온 **푸시** 아르라스트 이 솔테 아싸오 노 세그돈 노 노 다 수아 조나다

![ACOP](./images/journeyactions.png)

라도 디레이토 다 테라, 아고라 보케크리아 수아 알피쿠아상 푸시하지 마.

정의 **카테고리** como **마케팅** e selecione uma phecie 푸시 쿠퍼마이트 환경 알림 푸시 네세 카소, 피시 한 사람이 **miewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 기준 a 메뉴

Clique em **컨텐츠 편집**.

![ACOP](./images/emptymsg.png)

Em 세구이다. 텔라 아비소 세라 exibida:

![ACOP](./images/emailmsglist.png)

Vamos definir o contexutudo da notificaang push.

클리크 노 캄포 데 텍토 **제목**.

![Journey Optimizer](./images/msg5.png)

나알레아 데 텍토 **올라**. 클리케 노 아이콘 드 개인화 아상.

![Journey Optimizer](./images/msg6.png)

아고라 보정밀 트라저 오 토큰 드 개인화 아상 파라 오 캄포 **이름** 케 에스타 아르마젠라도 `profile.person.name.firstName`. 메뉴 항목 없음, 셀레치온 **프로필 속성**, 역할 para baixo/navegue para encontract 또는 elemento **개인** 클릭엔세타 파라 아바탄샤르 캄페 `profile.person.name.firstName`. 클리케 노 아이콘 **+** 파라아디치오캄포 아 텔라 Clique em **저장**.

![Journey Optimizer](./images/msg7.png)

엔탕, 보테 이라르토리나 파라 에스타 클리케 노 아이콘 데 페르스타리아상 라도 두 캄포 **본문**.

![Journey Optimizer](./images/msg11.png)

나알레아 데 텍토, 에스크레바 `Bem-vindo(a)`.

![Journey Optimizer](./images/msg12.png)

Em Seguida, Client em  **상황별 속성** 그리고 **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

Clique em **이벤트**.

![ACOP](./images/jomsg4.png)

Clique no nome do seu evento, que deve ser semelhante ao seguinte: **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

Clique em **컨텍스트 배치**.

![ACOP](./images/jomsg6.png)

Clique em **POI 상호 작용**.

![ACOP](./images/jomsg7.png)

Clique em **POI 세부 사항**.

![ACOP](./images/jomsg8.png)

클리크 번호 **+** 아이콘 없음 **POI 이름**.
Em Seguida와 Seguinte serla exibido입니다. Clique em **저장**.

![ACOP](./images/jomsg9.png)

수아 몽사감 아고에스타 발타 란케나 세타는 에스쿠도 파라 레트로나다 보다 우수한 에스쿠르를 얻을 수 없다.

![ACOP](./images/jomsg11.png)

Clique em **확인**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Enviuma mensagem para tela

코모 테세이라 에타파 다 조나다, 보레 데디치오나르 아상  **sendMessageToScreen** 작업. Vá para o lado esquerdo da tela para **작업**, 셀레치온 **sendMessageToScreen** 아르라스트 이 솔테 아싸오 노 테르세이로 노다 수아 조르나다 엠세구이다, 보스케베라 텔라아비아소입니다

![ACOP](./images/jomsg15.png)

**sendMessageToScreen** é uma açao personalizada uala publicar mensagem no ponto de extremidade usado pela exibçao na loja 아상 **sendMessageToScreen** 에스페라 케 뮤티플라 바리바 세잼 정의 Vokpode visualizar essas variables roballao para baixo até ver **작업 매개 변수**.

![ACOP](./images/jomsg16.png)

아고라 보콜세어 디히어 로스 발오르스 파라카다 파라메트로 드 아상 시가 에스타 타벨라 파라 펜덴더 쿠아스 발로아스

| 매개 변수 | 값 |
|:-------------:| :---------------:|
| 배달 | `'image'` |
| ECID | `@{yourLastNameBeaconEntryEvent._experienceplatform.identification.core.ecid}` |
| 이름 | `#{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName}` |
| EVENTSUBJECT | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first().name}` |
| EVENTSUBJECTURL | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first()._experienceplatform.core.imageURL}` |
| 샌드박스 | `'bootcamp'` |
| CONTAINERID | `''` |
| ACTIVITYID | `''` |
| PLACEMENTID | `''` |

{style=&quot;table-layout:auto&quot;}

파라 정의 발아들, 클리크 노 아이콘 **편집**.

![ACOP](./images/jomsg17.png)

Em Seguida, selecione **고급 모드**.

![ACOP](./images/jomsg18.png)

Em Seguida, cole o valor com base na tabela acima. Clique em **확인**.

![ACOP](./images/jomsg19.png)

리피타는 파라 아디치오나 발로레스 카다 캄포를 처리했습니다.

>[!IMPORTANT]
>
>파라오 캄포 ECID, 후마 레페른시아 에벤토`yourLastNameBeaconEntryEvent`. 렘브레 드 치스티튜르  `yourLastName` 펠로 세우 소브레놈

O 결과 최종 디브 사용자 semelhante ao seguinte:

![ACOP](./images/jomsg20.png)

역할 매개 변수 e clique em **확인**.

![ACOP](./images/jomsg21.png)

여정에 이름을 지정해야 합니다. 다음을 클릭하여 수행할 수 있습니다 **속성** 화면 오른쪽 상단의 아이콘을 클릭합니다.

![ACOP](./images/journeyname.png)

보테 인서르 오노메 다 조나카이  `yourLastName - Beacon Entry Journey`. Clique em **확인** 파라 살바도르 아타수

![ACOP](./images/journeyname1.png)

아고라 포데 퍼블리어 수아 조르나다 **게시**.

![ACOP](./images/publishjourney.png)

Clique em **게시** 노바멘테.

![ACOP](./images/publish1.png)

Vokverá uma barra de confirmçao verde informando que sua jornada ethla esta publada.

![ACOP](./images/published.png)

수아 조르나다 아고라 에스타 아티바 포데 카시오나다.

보스케어 운동선수

프로시마 에타파: [3.4 Teste sua jornada](./ex4.md)

[레토나르 플루소 드 우시오 3](./uc3.md)

[레토날라 파라 토도스 오모두로스](../../overview.md)
