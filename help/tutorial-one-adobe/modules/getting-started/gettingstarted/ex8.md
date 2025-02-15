---
title: 시작하기 - Postman 설정
description: 시작하기 - Postman 설정
kt: 5342
doc-type: tutorial
source-git-commit: 431f7696df12c8c133aced57c0f639c682304dee
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 2%

---

# 옵션 2: PostBuster 설정

>[!IMPORTANT]
>
>Adobe 직원이 아닌 경우 지침을 따라 [Postman 설치](./ex7.md)하십시오. 아래 지침은 Adobe 직원만을 대상으로 합니다. 이미 Postman을 구성한 경우 이 연습을 건너뛰고 [설치할 응용 프로그램](./ex9.md)으로 이동하십시오.

## PostBuster 설치

[https://adobe.service-now.com/esc?id=adb_esc_kb_article&amp;sysparm_article=KB0020542](https://adobe.service-now.com/esc?id=adb_esc_kb_article&amp;sysparm_article=KB0020542)(으)로 이동합니다.

**PostBuster**&#x200B;의 최신 릴리스를 다운로드하려면 클릭하세요.

![PostBuster](./images/pb1.png)

OS에 맞는 버전을 다운로드하십시오.

![PostBuster](./images/pb2.png)

다운로드가 완료되고 설치되면 PostBuster를 엽니다. 그럼 이걸 보셔야죠 **가져오기**&#x200B;를 클릭합니다.

![PostBuster](./images/pb3.png)

[postbuster.json.zip](./../../../assets/postman/postbuster.json.zip)을(를) 다운로드하고 데스크톱에서 추출하십시오.

![PostBuster](./images/pbpb.png)

**파일 선택**&#x200B;을 클릭합니다.

![PostBuster](./images/pb4.png)

**postbuster.json** 파일을 선택하십시오. **열기를 클릭합니다**.

![PostBuster](./images/pb5.png)

그럼 이걸 보셔야죠 **검사**&#x200B;를 클릭합니다.

![PostBuster](./images/pb6.png)

**가져오기**&#x200B;를 클릭합니다.

![PostBuster](./images/pb7.png)

그럼 이걸 보셔야죠 을(를) 클릭하여 가져온 컬렉션을 엽니다.

![PostBuster](./images/pb8.png)

이제 컬렉션을 볼 수 있습니다. 일부 환경 변수를 포함하도록 환경을 구성해야 합니다.

![PostBuster](./images/pb9.png)

**기본 환경**&#x200B;을 클릭한 다음 **편집** 아이콘을 클릭합니다.

![PostBuster](./images/pb10.png)

그럼 이걸 보셔야죠

![PostBuster](./images/pb11.png)

아래 환경 자리 표시자를 복사하여 **기본 환경**&#x200B;에 붙여넣습니다.

```json
{
	"CLIENT_SECRET": "",
	"API_KEY": "",
	"ACCESS_TOKEN": "",
	"SCOPES": [
		"openid",
		"AdobeID",
		"read_organizations", 
		"additional_info.projectedProductContext", 
		"session",
		"ff_apis",
		"firefly_api"
	],
	"TECHNICAL_ACCOUNT_ID": "",
	"IMS": "ims-na1.adobelogin.com",
	"IMS_ORG": "",
	"access_token": "",
	"IMS_TOKEN": "",
	"AZURE_STORAGE_URL": "",
	"AZURE_STORAGE_CONTAINER": "",
	"AZURE_STORAGE_SAS_READ": "",
	"AZURE_STORAGE_SAS_WRITE": ""
}
```

그럼 이걸 드셔보세요

![PostBuster](./images/pb12.png)

## Adobe I/O 변수 입력

[https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}(으)로 이동하여 프로젝트를 엽니다.

![Adobe I/O 새 통합](./images/iopr.png){zoomable="yes"}

**OAuth 서버 간**(으)로 이동합니다.

![Adobe I/O 새 통합](./images/iopbvar1.png){zoomable="yes"}

이제 Adobe I/O 프로젝트에서 다음 값을 복사하여 PostBuster 기본 환경에 붙여넣어야 합니다.

- 클라이언트 ID
- 클라이언트 암호(**클라이언트 암호 검색** 클릭)
- 기술 계정 ID
- 조직 ID(아래로 스크롤하여 조직 ID 찾기)

![Adobe I/O 새 통합](./images/iopbvar2.png){zoomable="yes"}

위의 변수를 하나씩 복사하여 PostBuster의 **기본 환경**&#x200B;에 붙여 넣으십시오.

| Adobe I/O의 변수 이름 | PostBuster 기본 환경의 변수 이름 |
|:-------------:| :---------------:| 
| 클라이언트 ID | `API_KEY` |
| 클라이언트 암호 | `CLIENT_SECRET` |
| 기술 계정 ID | `TECHNICAL_ACCOUNT_ID` |
| 조직 ID | `IMS_ORG` |

이러한 변수를 하나씩 복사하면 PostBuster 기본 환경은 다음과 같이 표시됩니다.

![Adobe I/O 새 통합](./images/iopbvar3.png){zoomable="yes"}

**Adobe IO - OAuth** 컬렉션에서 이름이 **POST - 액세스 토큰 가져오기**&#x200B;인 요청을 선택하고 **전송**&#x200B;을 선택합니다.

다음 정보가 포함된 유사한 응답이 표시됩니다.

| 키 | 값 |
|:-------------:| :---------------:| 
| token_type | **전달자** |
| access_token | **eyJhbGciOiJS...** |
| expires_in | **86399** |

Adobe I/O **전달자 토큰**&#x200B;에 특정 값(매우 긴 access_token)과 만료 창이 있으며, 이제 24시간 동안 유효합니다. 즉, 24시간 후 Postman을 사용하여 Adobe API와 상호 작용하려면 이 요청을 다시 실행하여 새 토큰을 생성해야 합니다.

![Adobe I/O 새 통합](./images/iopbvar4.png){zoomable="yes"}

이제 PostBuster 환경이 설정되고 작동합니다. 이제 시작 모듈을 완료했습니다.

## 다음 단계

[설치할 응용 프로그램](./ex9.md){target="_blank"}(으)로 이동

[시작하기](./getting-started.md){target="_blank"}(으)로 돌아가기

[모든 모듈](./../../../overview.md){target="_blank"}(으)로 돌아가기