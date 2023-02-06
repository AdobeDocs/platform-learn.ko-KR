---
title: Bootcamp - Customer Journey Analytics - 데이터 보기 만들기 - 브라질
description: Customer Journey Analytics - 데이터 보기 만들기 - 브라질
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 072179998d19c32589280defdb257a86d8728fea
workflow-type: tm+mt
source-wordcount: '1655'
ht-degree: 2%

---

# 4.3 크리우마 시각화 아상 데 도스

## 오베티보

- 엔켄다 a UI de Visualizaçao de Dados
- 데디치카스 데 비지타
- 압충다 아트리부이상 에지센시아 em 우마 시각화상 데

## 4.3.1 시각화 아상 데 도스

Agora, com sua conexao concluida da, é poghyvel progredir para increenciar a visualizaha입니다. 우마 디페렌사 o Adobe Analytics e o CJA é que o CJA precsa de uma visualizaçao de para librar e preparos dantes da visualizaçao

Uma Visualizaang de Dados é semelhante ao conceptor de Virtual Report Suites no Adobe Analytics, onde voke estableelectee as definitiçules de visita com rehecimento de contexto, filtragem e também como 구성 요소 카마도로 구성됩니다.

세라 필요히오, 미니모, 우마 비가시상 데 도가오 또는 코네상. 엔토토, 파라알건스 카소스 데 루소, é 올리티플라스 비주알리아수스 데 다아스 파라 a mesma conexao, com o objito de fornecer insights difertes para para는 구분을 제공합니다. 보데세자 쿠에 프레사 세자 앙다파 도르도, 포르마 아보르오 드 코모도 마르카다 카다 키프. 알건스 공장:

- Métracas de UX Apenas a equipment de UX Design
- os mesmos para KPIs e métracas para o Google Analytics e para o Customer Journey Analytics, para que de analise digital fale apenas 1 숙어종(para equipment de analise digital fale apenas 1 dioma) 을 사용합니다.
- Visualizaçao de Dados Filtrada para mostrar, por example, dados para apenas um mercado, ou marca, ou apenas Disposityvos moveis.

Na tela de **연결** 마르케 아 카이사 데 셀레카상 다 코네시 보카부 데 크림 Clique em  **데이터 보기 만들기**.

![데모](./images/exta.png)

Vokheserah rereconado para o fluxo de trabalho **데이터 보기 만들기** 워크플로우.

![데모](./images/0-v2.png)

## 4.3.2 정의 카상 드 시각화 상 데 도스

아고라 보케드 구성어는 정의 라시카스 파라라 시각화 아상 드 다사로 구성된다.

![데모](./images/0-v2.png)

A **연결** 케 보크루우 노 운동회 전타 에스타 셀레치오나다 수아 콘네상 `yourLastName – Omnichannel Data Connection`.

![데모](./images/ext5.png)

Em Seguida, 둥어 내 아 비가시리아상 데 도가두 세그네스 에스테 모드라로 데 노멘클래라투라: `yourLastName – Omnichannel Data View`.

Insight o mesmo valor para a a description: `yourLastName – Omnichannel Data View`.

| 이름 | 설명 |
| ----------------- |-------------| 
| `yourLastName – Omnichannel Data View` | `yourLastName – Omnichannel Data View` |

![데모](./images/1-v2.png)

파라 **시간대**, selecione o fuso horário **베르림, 에스토콜모, 로마, 베르나, 브루셀라, 비엔나, 암스테르담 GMT+01:00**. Este é um cenário realmente interessante, pois algumas empresas operam em diferets países e geografias. 알로카르오 후시오 호라리오 세라리오 파히스 에비타라 에로스 디피코 드 다도스, 코모, 모체 모체, 아크레디타르 크 피소아 캄비세타스 4h no 페루

![데모](./images/ext7.png)

보칭탐벨 포데 수정 이스소 나오 오바리가토리오, 마스 알건스 clientes gostam de usar Pessoas, Visitas e Acessos em vez de Pessoa, Sessang e Eventos (convençao de nomenclauatprao do Customer Journey Analytics).

Agora voke deve ter를 세구인티스 구성 aguidas 정의:

![데모](./images/1-v2.png)

Clique em **저장 후 계속**.

![데모](./images/12-v2.png)

## 4.3.3 구성 요소 다 시각화 아상 데 도스

네스트 운동료, 보테 이라 구성 오드로스 구성 요소, 요아리우스 파라 아올리사르 오데아도 e visualizah-los usando o Analysis Workspace. 네스타 IU, 홀레스 아레스 프린시파스:

- 라도 에케르도: 구성 요소 Dispatonoveis dos 데이터 세트 선택기
- 미오: 구성 요소 아다시오나도아 Visualizaçao de Dados
- 라도 디레토: 구성 요소

![데모](./images/2-v2.png)

>[!IMPORTANT]
>
>세보나오 엔콘트라 메트리카 아우드 치상피카, 베르피케 세오 캄포 `Contains data` foi removido de sua visualizaçao de dados. 카소 콘트라리오, 캄포
>
>![데모](./images/2-v2a.png)

아고라 보크레세 아라스타 e 솔타르 성분의 구성 요소 **추가된 구성 요소**. 파라, vokee deve selecionar os 구성 요소(à esquerda e arrastah-los e soltala-los na tela no meio)

Vamos começar com o primeiro 구성 요소: **이름(web.webPageDetails.name)**. Pesquise 구성 요소 e arreste-o e solte-o na tela.

![데모](./images/3-v2.png)

에세 구성 요소 데 오노메 다 파지나, 코모 포데 유도체 다 라이투라 두 캄포 스키마 `(web.webPageDetails.name)`.

엔토토, 유사 **이름** 코모 노메 나오 아 멜호르 콘벤싸오 드 노멘클라투라 아움 우수아리오 코포라티보 압필더 라피다멘테 치상

Vamos muda o nome para **페이지 이름**. 구성 요소 없음 e o renomeie na a rea **구성 요소 설정**.

![데모](./images/3-0-v2.png)

As Configuaçules de persitencia 상 **지속성 설정**. CJA에서 Os의 Conceitos de e prop nao 확장, 구성 Ausaus de Persistaterncia possibilitam um compportsemelhante로 구성됩니다.

![데모](./images/3-0-v21.png)

Se voknao alteressas confiaçaus, CJA irah interprear a dimenscomo **Prop** (니벨 데 오코르렛차) 알렘디소, 시데모들은 지스티엔시아 파라 톨라를 치수마 **eVar** (발로르 아오 룽오 다 조르나다.)

Se vonang estiver findarizado com eVars e Props, [레아 메이스 소브레 isso 나](https://experienceleague.adobe.com/docs/analytics/landing/an-key-concepts.html)..

Vamos deixar o Nome da Página Como Prop. 데사 포마, 보크 노세어 아테나 네후마 **지속성 설정**.

| 검색할 구성 요소 이름 | 새 이름 | 지속성 설정 |
| ----------------- |-------------| --------------------| 
| 이름(web.webPageDetails.name) | 페이지 이름 |  |

Em Seguida, escolha a dimension **phoneNumber** e 솔테-a tela. 오노보 데브 사용자 **전화 번호**.

![데모](./images/3-1-v2.png)

포르피엠, 아모스 알테르는 Confiaçaus로, 푸스는 누메로 도 셀룰러 디베 퍼시에르의 니벨 도 우슈아우리오.

파라 알테아, 퍼라 바이소 메뉴 à direita e abra aba **지속성**:

![데모](./images/5-v2.png)

마르크 a caixa de seleçao para modificar을 구성 아수 드 지스테니아의 구성으로 사용할 수 있습니다. 셀레치온 **가장 최근** e o escopo **개인(보고 기간)**, pois nos preocoupamos apenas com o ulutimo numero de cellular da pessoa. Se o cliente nang preencher o cellular em visitas futuras, voke ainda verá esse valor prenchido.

![데모](./images/6-v2.png)

| 검색할 구성 요소 이름 | 새 이름 | 지속성 설정 |
| ----------------- |-------------| --------------------| 
| phoneNumber | 전화 번호 | 가장 최근, 개인(보고 기간) |

O 프르시모 구성 요소 테 `web.webPageDetails.pageViews.value`.

메뉴 없음, 페스퀴즈 `web.webPageDetails.pageViews.value`. Arraste Solte Métrica na tela.

알테레 오노메 파라 **페이지 보기 수** 아래에 **구성 요소 설정**.

| 검색할 구성 요소 이름 | 새 이름 | 속성 설정 |
| ----------------- |-------------| --------------------| 
| web.webPageDetails.pageViews.value | 페이지 보기 횟수 |  |

![데모](./images/7-v2.png)

파라(Para)는 구아수 데 트리부이카오, 디히사르모스 엠브랑코

옵바카오: 구성 아싸오에스 데 지스테냐나메트리카메틸캄포데모르 알타다스 노 Analysis Workspace. Em algues casos, voqe pode optar por configula-las aqui eviitar que os usuários de negocios que pensar qual é o melhorer modelo de persistencia. em algures casos, vote pode optar por configula-las aqui para eviitar que os usuarios de negocios que pensar qual é o melhorer modelo de persistencencia.

Em 세구이다, 보테 테라 케 구성 바리아 치몽스 메트리카, 콘포르메 마르카도 타벨라 아바오.

### 차원

| 검색할 구성 요소 이름 | 새 이름 | 지속성 설정 |
| ----------------- |-------------| --------------------| 
| brandName | 브랜드 이름 | 가장 최근, 세션 |
| 냉소 | 통화 느낌 |  |
| 호출 ID | 호출 상호 작용 유형 |  |
| callTopic | 통화 항목 | 가장 최근, 세션 |
| ecid | ECID | 가장 최근, 개인(보고 기간) |
| 이메일 | 이메일 ID | 가장 최근, 개인(보고 기간) |
| 결제 유형 | 결제 유형 |  |
| 제품 추가 메서드 | 제품 추가 메서드 | 가장 최근, 세션 |
| 이벤트 유형 | 이벤트 유형 |  |
| 이름(productListItems.name) | 제품 이름 |  |
| SKU | SKU(세션) | 가장 최근, 세션 |
| 거래 ID | 거래 ID |  |
| URL(web.webPageDetails.URL) | URL |  |
| 사용자 에이전트 | 사용자 에이전트 | 가장 최근, 세션 |

### 메트리카

| 검색할 구성 요소 이름 | 새 이름 | 속성 설정 |
| ----------------- |-------------| --------------------| 
| 수량 | 수량 |  |
| commerce.order.priceTotal | 매출  |  |

Sua Configuration açao deve ser semelhante ao seguinte:

![데모](./images/11-v2.png)

나앙 세케사 데 살바르 수아 시각화상 드 도도스. 엔타앙 클락크 **저장**.

![데모](./images/12-v2s.png)

## 4.3.4 메트리카 계산대

엠보라 텐하모스 조직도 토도 os 구성 요소, Visualizaçao de dados, vocain da deve adaptar algues husuários de negocios jestein para iniciar suas análises.

Se voke se lembra, nao troxemos expificamente Métricacas como Adicionar ao Carrinho, Visualizasan do produto ou Compras a Visualizaçao de ados. 엔토토, 테모스 치메상 카마다: **이벤트 유형**. 엔탕, 아모스 유래 티포스 드 아싸오 크릴란도 3 메트리카 산세

Vamos começar com a primeira Métrica: **제품 보기**.

라도 에케르도, 페스퀴즈 **이벤트 유형** 차원을 선택합니다. Em Seguida, arraste-o e solte-o na tela **포함된 구성 요소**.

![데모](./images/calcmetr1.png)

Clique para selecionar a nova métrica **이벤트 유형**.

![데모](./images/calcmetr2.png)

아고알타레 오 노메 마르카오 두 구성 요소 파라 os 세구인테 발오르레스:

| 구성 요소 이름 | 구성 요소 설명 |
| ----------------- |-------------| 
| 제품 보기 | 제품 보기 |

![데모](./images/calcmetr3.png)

아고라 바모스 콘타르 아페나스 데 **제품 보기**. 단락 기호, 역할 매개 변수 사서함 em **구성 요소 설정** 아테 버 발로레스 데 **제외 값 포함**. 인증서-세 드 하빌타아 오파상 **포함/제외 값 설정**.

![데모](./images/calcmetr4.png)

코모 수용체 **제품 보기**, 특히 **commerce.productViews** 그리트리리오스.

![데모](./images/calcmetr5.png)

아고라 메트리카 산술라 프론타!

Em Seguida, Repeta o mesmo processo para eventos **장바구니에 추가** e **구매**.

### 장바구니에 추가

Primeiro, arraste solte a mesma 차원 **이벤트 유형**.

![데모](./images/calcmetr1.png)

폴 베라 알레타 팝업드-오 캄포 디루타도, 포이에스스타모스는 메스마바벨 Clique em **추가**:

![데모](./images/calcmetr6.png)

아고라, 시그아 o mesmo processo que fizemos para métrica Visualizacx de produto:
- Primeiro Altere와 Nome는
- Por fim, adicioone **commerce.productListAdds** 코모 크리테리오 파라라 카르타에나에 추가

| 이름 | 설명 | 기준 |
| ----------------- |-------------| -------------|
| 장바구니에 추가 | 장바구니에 추가 | commerce.productListAdds |

![데모](./images/calcmetr6a.png)

### 구매

Primeiro, arraste solte a mesma 차원 **이벤트 유형** 코모 피제모스 파라라 듀아스 메트리카스 앙테리아스

![데모](./images/calcmetr1.png)

폴 베라 알레타 팝업드-오 캄포 디루타도, 포이에스스타모스는 메스마바벨 Clique em **추가**:

![데모](./images/calcmetr7.png)

Agora, siga o o o mesmo processo que fizemos para as métras 제품 보기 를 장바구니에 추가합니다.
- Primeiro Altere와 Nome는
- Por fim, adicioone **commerce.purchases** como critérios para contenabilizar apenas as as compras

| 이름 | 설명 | 기준 |
| ----------------- |-------------| -------------|
| 구매 | 구매 | commerce.purchases |

![데모](./images/calcmetr7a.png)

수아 구성 아오 세구인테 최종 데버 서입니다. Clique em **저장 후 계속**.

![데모](./images/calcmetr8.png)

## 4.3.5 구성 요소 다 구성 아상 데 도스

보려 레그레시오나도 파라 에스타

![데모](./images/8-v2.png)

네스타 아바, 보테 수정자 알구마스 구성상 파라 알가르타 아가르타 포르마 오 드 상파카도 가입니다. Vamos começar definindo **세션 시간 초과** 코모 30분 그라사스 아오 레지스트로 데 데이터 e 호라 데 카다 evento de experiencia, vokal pode estender o hersemo de uma sessao em todos os canais. 포르 모예, o que acontece se um clientte ligar para o 콜 센터에서 de visitor o site? 우산도 템포스 리마이트 데 세사오 개인아도스, 보케 템무타 플렉시빌리다드 파라 디치어 오 쿠마 수싸상 에모 에사 아소스 아소스 데소 도파입니다.

![데모](./images/ext8.png)

네스타 아바 보데 모디피카(Nesta aba pode modificar) 아웃라타(coisas rotracar os dados usando segmento/filo) 보흐나파쉬라 파저 이소네세 운동

![데모](./images/10-v2.png)

양자도 단말, 클릭크 em **저장 및 완료**.

![데모](./images/13-v2.png)

>[!NOTE]
>
>Vokpode Voltar a esta Visualizaçao de dados posteriormente alterar는 구성 ausees e os 구성 요소로 qualquer momento로 대체됩니다. 아테라앙 아페타라오인 코모 드도스 히스토리코스 모스타도스처럼

아고라 보퀘데 연속악단 a parte de visualizaçao e anailise!

프로시마 에타파: [4.4 프리카상 데 도스 Customer Journey Analytics](./ex4.md)

[레토나르 플루소 드 우시오 4](./uc4.md)

[레토날라 파라 토도스 오모두로스](./../../overview.md)
