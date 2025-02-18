---
title: BigQuery Source 커넥터를 사용하여 Adobe Experience Platform에서 Google Analytics 데이터 수집 및 분석 - GCP 및 BigQuery를 Adobe Experience Platform에 연결
description: BigQuery Source 커넥터를 사용하여 Adobe Experience Platform에서 Google Analytics 데이터 수집 및 분석 - GCP 및 BigQuery를 Adobe Experience Platform에 연결
kt: 5342
doc-type: tutorial
exl-id: 00695ec0-34e0-4a20-afe3-bee4016eef58
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 1%

---

# 1.2.3 GCP 및 BigQuery를 Adobe Experience Platform에 연결

## 목표

- Google Cloud Platform 내의 API 및 서비스 살펴보기
- Google API 테스트를 위한 OAuth Playground 숙지
- Adobe Experience Platform에서 첫 번째 BigQuery 연결 만들기

## 컨텍스트

Adobe Experience Platform은 BigQuery 데이터 세트를 Adobe Experience Platform으로 가져오는 데 도움이 되는 커넥터를 **소스** 내에 제공합니다. 이 데이터 커넥터는 Google BigQuery API를 기반으로 합니다. 따라서 Adobe Experience Platform에서 API 호출을 받을 수 있도록 Google Cloud Platform 및 BigQuery 환경을 제대로 준비하는 것이 중요합니다.

Adobe Experience Platform에서 BigQuery Source 커넥터를 구성하려면 다음 4가지 값이 필요합니다.

- 프로젝트
- clientId
- 클라이언트 암호
- refreshToken

지금까지 첫 번째 ID **프로젝트 ID**&#x200B;만 있습니다. 이 **프로젝트 ID** 값은 연습 12.1에서 BigQuery 프로젝트를 만들 때 Google에서 생성한 임의의 ID입니다.

분리된 텍스트 파일에 프로젝트 ID를 복사하십시오.

| 자격 증명 | 이름 지정 | 예 |
| ----------------- |-------------| -------------|
| 프로젝트 ID | random | possible-bee-447102-h3 |

상단 메뉴 모음에서 **프로젝트 이름**&#x200B;을 클릭하여 프로젝트 ID를 언제든지 확인할 수 있습니다.

![데모](./images/ex1projectMenu.png)

프로젝트 ID는 오른쪽에 표시됩니다.

![데모](./images/ex1projetcselection.png)

이 연습에서는 다른 3개의 필수 필드를 가져오는 방법을 배웁니다.

- clientId
- 클라이언트 암호
- refreshToken

## 1.2.3.1 Google 인증 플랫폼

시작하려면 Google Cloud Platform 홈 페이지로 돌아가십시오. 이렇게 하려면 화면의 왼쪽 상단 모서리에 있는 로고를 클릭하면 됩니다.

![데모](./images/ex25.png)

홈 페이지를 방문하면 검색 창에서 **Google 인증 플랫폼**&#x200B;을 검색합니다. 첫 번째 결과를 클릭하여 엽니다.

![데모](./images/ex24.png)

이제 **Google 인증 플랫폼** 홈 페이지가 표시됩니다. **GET 시작**&#x200B;을 클릭합니다.

![데모](./images/ex26.png)

**앱 이름**&#x200B;의 경우 다음 항목을 사용하십시오.

| 이름 지정 | 예 |
| ----------------- |-------------| 
| `--aepUserLdap-- - AEP BigQuery Connector` | vangeluw - AEP BigQuery 커넥터 |

필드 **사용자 지원 전자 메일**&#x200B;의 전자 메일 주소를 선택하십시오.

**다음**&#x200B;을 클릭합니다.

![데모](./images/go1.png)

**외부**&#x200B;를 선택하고 **다음**&#x200B;을 클릭합니다.

![데모](./images/go2.png)

메일 주소를 입력하고 **다음**&#x200B;을 클릭하세요.

![데모](./images/go3.png)

확인란을 선택하고 **계속**&#x200B;을 클릭합니다. 그런 다음 **만들기**&#x200B;를 클릭합니다.

![데모](./images/go4.png)

## 1.2.3.2 OAuth 클라이언트 만들기

**OAUTH 클라이언트 만들기**&#x200B;를 클릭합니다.

![데모](./images/ex261.png)

그러면 이걸 보게 될 거야.

![데모](./images/ex2611.png)

**웹 응용 프로그램**&#x200B;을 선택하십시오.

![데모](./images/ex212.png)

몇 개의 새 필드가 표시됩니다. 이제 OAuth 클라이언트 ID의 **이름**&#x200B;을 입력하고 **승인된 리디렉션 URI**&#x200B;도 입력해야 합니다.

필드 **이름**&#x200B;의 경우 다음 항목을 사용하십시오.

| 필드 | 값 | 예 |
| ----------------- |-------------| -------------| 
| 이름 | ldap - AEP BigQuery 커넥터 | vangeluw - Platform BigQuery 커넥터 |

![데모](./images/ex2122.png)


**승인된 리디렉션 URI**&#x200B;에서 **+ URI 추가**&#x200B;를 클릭합니다. 아래의 새 URI를 추가합니다.

| 필드 | 값 |
| ----------------- |-------------| 
| 승인된 리디렉션 URI | https://developers.google.com/oauthplayground |

**승인된 리디렉션 URI** 필드는 Adobe Experience Platform에서 BigQuery Source 커넥터 설정을 완료하는 데 필요한 RefreshToken을 가져오는 데 나중에 필요하므로 매우 중요한 필드입니다.

**만들기**&#x200B;를 클릭합니다.

![데모](./images/ex2121.png)

이제 OAuth 클라이언트 ID가 생성됩니다. 클라이언트 ID와 클라이언트 암호를 보려면 클릭하십시오.

![데모](./images/ex220.png)

그러면 클라이언트 ID 및 클라이언트 암호 값이 표시됩니다.

이 두 필드를 복사하여 바탕 화면의 텍스트 파일에 붙여넣으십시오. 이러한 자격 증명은 나중에 언제든지 액세스할 수 있지만, BigQuery 프로젝트 ID 옆에 있는 텍스트 파일에 저장하면 더 쉽게 액세스할 수 있습니다.

Adobe Experience Platform에서 BigQuery Source Connector 설정을 요약 하면 이제 다음 값을 이미 사용할 수 있습니다.

| BigQuery 커넥터 자격 증명 | 값 |
| ----------------- |-------------| 
| 프로젝트 ID | 고유한 프로젝트 ID(예:: possible-bee-447102-h3) |
| clientid | clientid |
| clientsecret | yourclientsecret |

![데모](./images/ex2200.png)

그런 다음 OAuth 앱을 게시해야 합니다. **대상자**(으)로 이동하여 **앱 게시**&#x200B;를 클릭합니다.

![데모](./images/ex2pub1.png)

**확인**&#x200B;을 클릭합니다.

![데모](./images/ex2pub2.png)

**refreshToken**&#x200B;이 아직 없습니다. 보안상의 이유로 refreshToken은 필수입니다. API의 세계에서 토큰은 일반적으로 24시간마다 만료됩니다. 따라서 Source 커넥터 설정에서 Google Cloud Platform 및 BigQuery에 계속 연결할 수 있도록 24시간마다 보안 토큰을 새로 고치려면 **refreshToken**&#x200B;이 필요합니다.

## 1.2.3.3 BigQuery API 및 refreshToken

Google Cloud Platform API에 액세스하기 위해 refreshToken을 가져오는 방법은 여러 가지가 있습니다. 이러한 옵션 중 하나는 예를 들어 Postman을 사용하는 것입니다.
하지만 Google은 API를 사용하여 테스트하고 재생할 수 있는 보다 쉬운 도구를 만들었습니다. 이 도구는 **OAuth 2.0 Playground**&#x200B;입니다.

**OAuth 2.0 Playground**&#x200B;에 액세스하려면 [https://developers.google.com/oauthplayground](https://developers.google.com/oauthplayground)(으)로 이동하십시오.

그러면 **OAuth 2.0 플레이그라운드** 홈 페이지가 표시됩니다.

![데모](./images/ex222.png)

화면 오른쪽 상단의 **톱니바퀴** 아이콘을 클릭합니다. 설정이 위의 이미지에서 볼 수 있는 것과 동일한지 확인하십시오.

**자신의 OAuth 자격 증명 사용** 확인란을 선택합니다.

![데모](./images/ex2221.png)

두 개의 필드가 나타납니다.

이 표의 다음 필드를 입력하십시오.

| 플레이그라운드 API 설정 | Google API 자격 증명 |
| ----------------- |-------------| 
| OAuth 클라이언트 ID | 고유한 클라이언트 ID(데스크탑의 텍스트 파일 내) |
| OAuth 클라이언트 암호 | 고유한 클라이언트 암호(데스크탑의 텍스트 파일) |

자격 증명을 작성했으면 **닫기**&#x200B;를 클릭하세요.

![데모](./images/ex223a.png)

왼쪽 메뉴에서 사용 가능한 모든 Google API를 볼 수 있습니다. **BigQuery API v2**&#x200B;을(를) 검색하고 클릭하여 엽니다.

![데모](./images/ex227.png)

그런 다음 아래 이미지에 표시된 범위를 선택합니다. 사용 가능한 각 API를 클릭해야 하며 선택한 각 API에 대해 확인 표시가 표시됩니다.

그런 다음 **API 승인**&#x200B;을 클릭합니다.

![데모](./images/ex226.png)

GCP 및 BigQuery 설정에 사용한 이메일 주소를 클릭합니다.

![데모](./images/ex2266.png)

큰 경고가 표시됩니다. **이 앱은 확인되지 않습니다**. 이 문제는 Platform BigQuery 커넥터가 아직 공식적으로 검토되지 않았기 때문에 Google은 정품 앱인지 여부를 알 수 없습니다.

**고급**&#x200B;을 클릭합니다.

![데모](./images/ex232.png)

다음으로 **이동 —aepUserLdap— - AEP BigQuery Connector(안전하지 않음)**&#x200B;을 클릭합니다.

![데모](./images/ex233.png)

그러면 액세스를 위한 보안 프롬프트가 표시됩니다. **모두 선택**&#x200B;을 클릭합니다.

![데모](./images/ex229.png)

아래로 스크롤하여 **계속**&#x200B;을 클릭합니다.

![데모](./images/ex230.png)

이제 OAuth 2.0 플레이그라운드로 다시 전송되며 이 내용이 표시됩니다. **토큰에 대한 인증 코드 교환**&#x200B;을 클릭합니다.

![데모](./images/ex236.png)

몇 초 후 **2단계 - 토큰에 대한 Exchange 인증 코드** 보기가 자동으로 닫히고 **3단계 - API에 대한 요청 구성**&#x200B;이 표시됩니다.

**토큰에 대한 2단계 Exchange 인증 코드**(으)로 돌아가야 하므로 **토큰에 대한 2단계 Exchange 인증 코드**&#x200B;을 다시 클릭하여 **토큰 새로 고침**&#x200B;을 시각화하십시오.

![데모](./images/ex237.png)

이제 **토큰 새로 고침**&#x200B;이 표시됩니다.

![데모](./images/ex238.png)

**새로 고침 토큰**&#x200B;을 복사하여 바탕 화면의 텍스트 파일에 다른 BigQuery Source 커넥터 자격 증명과 함께 붙여 넣습니다.

| BigQuery Source 커넥터 자격 증명 | 값 |
| ----------------- |-------------| 
| 프로젝트 ID | 고유한 임의 프로젝트 ID(예:: apt-summer-273608) |
| clientid | clientid |
| clientsecret | yourclientsecret |
| refreshtoken | yourrefreshtoken |

다음으로 Adobe Experience Platform에서 Source 커넥터를 설정해 보겠습니다.

## 1.2.3.5 - 고유한 BigQuery 테이블과 플랫폼 연결

URL [https://experience.adobe.com/platform](https://experience.adobe.com/platform)로 이동하여 Adobe Experience Platform에 로그인합니다.

로그인하면 Adobe Experience Platform 홈페이지에 접속하게 됩니다.

![데이터 수집](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

계속하려면 **샌드박스**&#x200B;를 선택해야 합니다. 선택할 샌드박스 이름이 ``--aepSandboxName--``입니다. 적절한 샌드박스를 선택하면 화면이 변경되고 이제 전용 샌드박스에 있습니다.

![데이터 수집](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

왼쪽 메뉴에서 소스로 이동합니다. 그러면 **소스** 홈 페이지가 표시됩니다. **소스** 메뉴에서 **데이터베이스**&#x200B;를 클릭합니다. **Google BigQuery** 카드를 클릭합니다. 그런 다음 **설정**&#x200B;을 클릭합니다.

![데모](./images/s1.png)

이제 새 연결을 만들어야 합니다.

**새 계정**&#x200B;을 클릭합니다. 이제 GCP 및 BigQuery에서 수행한 설정을 기반으로 아래 필드를 모두 작성해야 합니다.

![데모](./images/s3.png)

먼저 연결의 이름을 지정하겠습니다.

이 명명 규칙을 사용하십시오.

| BigQuery 커넥터 자격 증명 | 값 | 예 |
| ----------------- |-------------| -------------| 
| 계정 이름 | `--aepUserLdap-- - BigQuery Connection` | vangeluw - BigQuery 연결 |
| 설명 | `--aepUserLdap-- - BigQuery Connection` | vangeluw - BigQuery 연결 |

그러면 다음 항목이 제공됩니다.

![데모](./images/ex239a.png)

그런 다음 바탕 화면의 텍스트 파일에 저장한 GCP 및 BigQuery API **계정 인증**-세부 정보를 작성합니다.

| BigQuery 커넥터 자격 증명 | 값 |
| ----------------- |-------------| 
| 프로젝트 ID | 고유한 임의 프로젝트 ID(예:: possible-bee-447102-h3) |
| clientId | ... |
| 클라이언트 암호 | ... |
| refreshToken | ... |

**계정 인증** 세부 정보는 이제 다음과 같습니다. **소스에 연결**&#x200B;을 클릭합니다.

![데모](./images/ex239xx.png)

**계정 인증** 세부 정보를 올바르게 작성한 경우 이제 **연결됨** 확인을 확인하여 연결이 제대로 작동하고 있는지 시각적으로 확인해야 합니다. **다음**&#x200B;을 클릭합니다.

![데모](./images/ex2projectid.png)

이제 이전 연습에서 만든 BigQuery 데이터 세트가 표시됩니다.

![데모](./images/datasets.png)

잘했어! 다음 연습에서는 해당 테이블의 데이터를 로드하고 Adobe Experience Platform의 스키마 및 데이터 세트에 대해 매핑합니다.

## 다음 단계

[1.2.4 BigQuery에서 Adobe Experience Platform으로 데이터 로드](./ex4.md){target="_blank"}(으)로 이동

BigQuery Google Analytics 커넥터를 사용하여 Adobe Experience Platform에서 [Source 데이터 수집 및 분석](./customer-journey-analytics-bigquery-gcp.md){target="_blank"}(으)로 돌아가기

[모든 모듈](./../../../../overview.md){target="_blank"}(으)로 돌아가기
