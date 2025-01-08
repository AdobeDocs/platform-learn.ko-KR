---
title: Firefly 서비스 시작
description: Firefly 서비스 시작
kt: 5342
doc-type: tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: 608fc570f9aa172db3578664e793f35fb3f1bf50
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 0%

---

# 1.1.1 Firefly 서비스 시작하기

이 연습에서는 Postman 및 Adobe I/O을 사용하여 Adobe Firefly 서비스 API를 쿼리합니다.

## Adobe I/O 프로젝트 구성

이 연습에서는 Firefly 서비스 API에 대해 쿼리하기 위해 Adobe I/O을 상당히 집중적으로 사용합니다. Adobe I/O을 설정하려면 아래 단계를 따르십시오.

[https://developer.adobe.com/console/home](https://developer.adobe.com/console/home)(으)로 이동

![새 통합 Adobe I/O](./images/iohome.png)

화면 오른쪽 상단 모서리에서 올바른 인스턴스를 선택해야 합니다. 인스턴스는 `--aepImsOrgName--`입니다. **새 프로젝트 만들기**&#x200B;를 클릭합니다.

![새 통합 Adobe I/O](./images/iocomp.png)

**+ 프로젝트에 추가**&#x200B;를 선택하고 **API**&#x200B;를 선택합니다.

![새 통합 Adobe I/O](./images/adobe_io_access_api.png)

그러면 다음과 같은 결과가 표시됩니다.

![새 통합 Adobe I/O](./images/api1.png)

**Creative Cloud**&#x200B;을(를) 선택하고 **Firefly - Firefly 서비스**&#x200B;를 클릭합니다. **다음**&#x200B;을 클릭합니다.

![새 통합 Adobe I/O](./images/api3.png)

이제 이 항목을 볼 수 있습니다. 자격 증명의 이름을 지정하십시오. `--aepUserLdap-- - Firefly Services OAuth credential`. **다음**&#x200B;을 클릭합니다.

![새 통합 Adobe I/O](./images/api4.png)

그런 다음 이 통합에 사용할 수 있는 권한을 정의할 제품 프로필을 선택해야 합니다.

**기본 Firefly 서비스 구성** 프로필을 선택하십시오.

**구성된 API 저장**&#x200B;을 클릭합니다.

![새 통합 Adobe I/O](./images/api9.png)

이제 Adobe I/O 통합이 준비되었습니다.

![새 통합 Adobe I/O](./images/api11.png)

**Postman용 다운로드** 단추를 클릭한 다음 **OAuth 서버-서버**&#x200B;를 클릭하여 Postman 환경을 다운로드합니다.

![새 통합 Adobe I/O](./images/iopm.png)

현재 IO 프로젝트에 일반 이름이 있습니다. 통합에 친숙한 이름을 지정해야 합니다. 표시된 대로 **프로젝트 X**(또는 유사한 이름)을 클릭합니다.

![새 통합 Adobe I/O](./images/api13.png)

**프로젝트 편집**&#x200B;을 클릭합니다.

![새 통합 Adobe I/O](./images/api14.png)

통합 이름을 입력하십시오. `--aepUserLdap-- Firefly`.

**저장**&#x200B;을 클릭합니다.

![새 통합 Adobe I/O](./images/api15.png)

이제 Adobe I/O 통합 설정이 완료되었습니다.

![새 통합 Adobe I/O](./images/api16.png)

## Adobe I/O에 대한 Postman 인증

[https://www.postman.com/downloads/](https://www.postman.com/downloads/)(으)로 이동합니다.

OS용 Postman의 관련 버전을 다운로드하여 설치합니다.

![새 통합 Adobe I/O](./images/getstarted.png)

Postman 설치 후 애플리케이션을 시작합니다.

Postman에는 환경과 컬렉션의 두 가지 개념이 있습니다.

- 환경 파일에는 거의 일관되지 않은 모든 환경 변수가 포함되어 있습니다. 환경에서는 클라이언트 ID 및 기타 같은 보안 자격 증명과 함께 Adobe 환경의 IMSOrg와 같은 항목을 찾을 수 있습니다. 환경 파일은 이전 연습에서 Adobe I/O 설정 중에 다운로드한 파일로, 다음과 같이 이름이 지정됩니다. **`oauth_server_to_server.postman_environment.json`**.

- 컬렉션에는 사용할 수 있는 여러 API 요청이 포함되어 있습니다. 2개의 컬렉션을 사용합니다.
   - Adobe I/O 인증을 위한 1개 컬렉션
   - 이 단원의 연습에 대한 컬렉션 1개

로컬 데스크톱에 [postman.zip](./../../../assets/postman/postman-ff.zip) 파일을 다운로드하십시오.

![새 통합 Adobe I/O](./images/pmfolder.png)

이 **postman.zip** 파일에서 다음 파일을 찾을 수 있습니다.

- `Adobe IO - OAuth.postman_collection.json`
- `FF - Firefly Services Tech Insiders.postman_collection.json`

**postman-ff.zip** 파일의 압축을 풀고 이 두 파일을 `oauth_server_to_server.postman_environment.json` 파일인 Adobe I/O에서 다운로드한 Postman 환경과 함께 데스크톱의 폴더에 저장합니다. 이 폴더에 다음 3개의 파일이 있어야 합니다.

![새 통합 Adobe I/O](./images/pmfolder1.png)

Postman으로 돌아갑니다. **가져오기**&#x200B;를 클릭합니다.

![새 통합 Adobe I/O](./images/postmanui.png)

**파일**&#x200B;을 클릭합니다.

![새 통합 Adobe I/O](./images/choosefiles.png)

다운로드한 2개의 파일을 추출한 바탕 화면의 폴더로 이동합니다. 이 3개의 파일을 동시에 선택하고 **열기**&#x200B;를 클릭합니다.

![새 통합 Adobe I/O](./images/selectfiles.png)

**열기**&#x200B;를 클릭하면 Postman에 가져오려는 환경 및 컬렉션에 대한 개요가 표시됩니다. **가져오기**&#x200B;를 클릭합니다.

![새 통합 Adobe I/O](./images/impconfirm.png)

이제 API를 통해 Firefly 서비스와 상호 작용하기 위해 Postman에 필요한 모든 기능을 사용할 수 있습니다.

가장 먼저 해야 할 일은 자신이 제대로 인증되었는지 확인하는 것입니다. 인증을 받으려면 액세스 토큰을 요청해야 합니다.

요청을 실행하기 전에 올바른 환경을 선택했는지 확인하십시오. 오른쪽 상단의 환경 드롭다운 목록을 확인하여 현재 선택한 환경을 확인할 수 있습니다.

선택한 환경의 이름은 이 `--aepUserLdap-- Firefly Services OAuth Credential`과(와) 유사해야 합니다.

![Postman](./images/envselemea.png)

이제 Postman 환경 및 컬렉션이 구성되고 작동합니다. 이제 Postman에서 Adobe I/O으로 인증할 수 있습니다.

**Adobe IO - OAuth** 컬렉션에서 이름이 **POST - 액세스 토큰 가져오기**&#x200B;인 요청을 선택합니다. **매개 변수**&#x200B;에서 2개의 변수 `API_KEY` 및 `CLIENT_SECRET`을(를) 참조하고 있습니다. 이 변수는 선택한 환경 `--aepUserLdap-- Firefly Services OAuth Credential`에서 가져온 것입니다.

**보내기**&#x200B;를 클릭합니다.

![Postman](./images/ioauth.png)

**보내기**&#x200B;를 클릭하면 Postman의 **본문** 섹션에 응답이 표시됩니다.

![Postman](./images/ioauthresp.png)

구성이 성공하면 다음 정보가 포함된 유사한 응답이 표시됩니다.

| 키 | 값 |
|:-------------:| :---------------:| 
| token_type | **전달자** |
| access_token | **eyJhbGciOiJSU...** |
| expires_in | **86399** |

Adobe I/O에서 특정 값(매우 긴 access_token)과 만료 창이 있는 **전달자** 토큰을 지정했습니다.

우리가 받은 토큰은 이제 24시간 동안 유효합니다. 즉, 24시간 후 Postman을 사용하여 Adobe I/O을 인증하려면 이 요청을 다시 실행하여 새 토큰을 생성해야 합니다.

## Firefly 서비스 API, 텍스트 2 이미지

이제 Firefly 서비스 API에 첫 번째 요청을 보낼 수 있습니다.

**FF - Firefly 서비스 기술 내부자** 컬렉션에서 이름이 **POST - Firefly - T2I V3**&#x200B;인 요청을 선택합니다. **본문** 섹션에 `Horses in a field`이라는 기본 프롬프트가 표시됩니다. Firefly 서비스에서 해당 이미지를 생성하도록 하려면 **보내기**&#x200B;를 클릭하십시오.

![Firefly](./images/ff1.png)

그러면 이미지 URL이 포함된 유사한 응답이 표시됩니다. 이미지 URL을 복사하여 웹 브라우저에서 엽니다.

![Firefly](./images/ff2.png)

이제 `horses in a field`을(를) 묘사하는 멋진 이미지를 볼 수 있습니다.

![Firefly](./images/ff3.png)

다음 연습을 계속하기 전에 언제든지 API 요청을 재생하십시오.

다음 단계: [1.1.2 사양이 있는 이미지 요청](./ex2.md)

[모듈 1.1로 돌아가기](./firefly-services.md)

[모든 모듈로 돌아가기](./../../../overview.md)
