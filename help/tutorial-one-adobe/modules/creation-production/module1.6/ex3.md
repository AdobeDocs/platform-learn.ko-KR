---
title: 외부 DAM 앱 만들기
description: 외부 DAM 앱 만들기
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 6823e8a0-dde7-460a-a48a-6787e65e4104
source-git-commit: fe162f285d67cc2a37736f80715a5c5717835e95
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 0%

---

# 1.6.3 외부 DAM 앱 만들기 및 배포

## 1.6.3.1 샘플 앱 파일 다운로드

[https://github.com/adobe/genstudio-extensibility-examples](https://github.com/adobe/genstudio-extensibility-examples)&#x200B;(으)로 이동합니다. **코드**&#x200B;를 클릭한 다음 **ZIP 다운로드**&#x200B;를 선택합니다.

![외부 DAM](./images/extdam1.png)

zip 파일을 바탕 화면에 압축 해제합니다.

![외부 DAM](./images/extdam2.png)

**genstudio-extensibility-examples-main** 폴더를 엽니다. 여러 샘플 앱이 표시됩니다. 이 연습에서 관심있는 것은 **genstudio-external-dam-app**&#x200B;입니다.

해당 디렉터리를 복사하여 바탕 화면에 붙여넣습니다.

![외부 DAM](./images/extdam4.png)

이제 바탕 화면에 이 기능이 표시됩니다.

![외부 DAM](./images/extdam3.png)

다음 연습에서는 **genstudio-external-dam-app** 폴더만 사용합니다.

## 1.6.3.2 Adobe Developer 명령줄 인터페이스 구성

**genstudio-external-dam-app** 폴더를 마우스 오른쪽 단추로 클릭하고 **폴더의 새 터미널**&#x200B;을 선택합니다.

![외부 DAM](./images/extdam5.png)

그럼 이걸 보셔야죠 `aio login` 명령을 입력하십시오. 이 명령은 사용자 브라우저로 리디렉션되고 사용자가 로그인합니다.

![외부 DAM](./images/extdam6.png)

로그인에 성공하면 브라우저에 표시됩니다.

![외부 DAM](./images/extdam7.png)

그러면 브라우저가 터미널 창으로 다시 리디렉션됩니다. **로그인 성공**&#x200B;이라는 메시지와 브라우저가 반환하는 긴 토큰이 표시됩니다.

![외부 DAM](./images/extdam8.png)

다음 단계는 외부 DAM 앱에 사용할 인스턴스 및 Adobe IO 프로젝트를 구성하는 것입니다.

이렇게 하려면 이전에 구성한 Adobe IO 프로젝트에서 파일을 다운로드해야 합니다.

[https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}(으)로 이동하여 이전에 만든 `--aepUserLdap-- GSPeM EXT` 프로젝트를 엽니다. **프로덕션** 작업 영역을 엽니다.

![외부 DAM](./images/extdam9.png)

**모두 다운로드**&#x200B;를 클릭합니다. JSON 파일이 다운로드됩니다.

![외부 DAM](./images/extdam10.png)

**다운로드** 디렉터리에서 외부 DAM 앱의 루트 디렉터리로 JSON 파일을 복사합니다.

![외부 DAM](./images/extdam11.png)

터미널 창으로 돌아갑니다. `aio app use XXX-YYY-Production.json` 명령을 입력하십시오.

>[!NOTE]
>
>파일 이름과 일치하도록 파일 이름을 변경해야 합니다.

명령이 실행되면 이제 외부 DAM 앱이 이전에 만든 App Builder을 사용하여 Adobe IO 프로젝트에 연결됩니다.

![외부 DAM](./images/extdam12.png)

## 1.6.3.3 GenStudio 확장성 SDK 설치

**GenStudio 확장성 SDK**&#x200B;을 설치해야 합니다. SDK에 대한 자세한 내용은 [https://github.com/adobe/genstudio-extensibility-sdk](https://github.com/adobe/genstudio-extensibility-sdk)에서 확인할 수 있습니다.

SDK을 설치하려면 터미널 창에서 다음 명령을 실행합니다.

`npm install @adobe/genstudio-extensibility-sdk`

![외부 DAM](./images/extdam13.png)

몇 분 후에 SDK이 설치됩니다.

![외부 DAM](./images/extdam14.png)

## 1.6.3.4 Visual Studio 코드에서 외부 DAM 앱을 검토합니다.

Visual Studio 코드를 엽니다. 폴더를 열려면 **열기...**&#x200B;를 클릭하세요.

![외부 DAM](./images/extdam15.png)

이전에 다운로드한 앱이 포함된 **genstudio-external-dam-app** 폴더를 선택하십시오.

![외부 DAM](./images/extdam16.png)

**.env** 파일을 열려면 클릭하세요.

![외부 DAM](./images/extdam17.png)

**.env** 파일은 이전 단계에서 실행한 `aio app use` 명령에 의해 만들어졌으며 App Builder을 사용하여 Adobe IO 프로젝트에 연결하는 데 필요한 정보가 포함되어 있습니다.

![외부 DAM](./images/extdam18.png)

이제 폴더의 루트에 2개의 새 파일을 만들어야 합니다.

- `.env.dev` 질문에 답합니다. **새 파일** 단추를 클릭한 다음 파일 이름 `.env.dev`을(를) 입력하십시오.

![외부 DAM](./images/extdam19.png)

- `.env.prod`.  **새 파일** 단추를 클릭한 다음 파일 이름 `.env.prod`을(를) 입력하십시오.

![외부 DAM](./images/extdam20.png)

이러한 파일에는 이전에 만든 AWS S3 버킷에 연결하는 데 필요한 자격 증명이 포함됩니다.

```
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_REGION=
AWS_BUCKET_NAME=
```

이전 연습에서 IAM 사용자를 만든 후 필드 **`AWS_ACCESS_KEY_ID`** 및 **`AWS_SECRET_ACCESS_KEY`**&#x200B;을(를) 사용할 수 있습니다. 이를 기록하라는 메시지가 표시되면 이제 값을 복사할 수 있습니다.

![ETL](./images/cred1.png)

버킷 이름 옆의 AWS S3 홈 보기에서 **`AWS_REGION`** 필드를 가져올 수 있습니다. 이 예제에서 지역은 **us-west-2**&#x200B;입니다.

![ETL](./images/bucket2.png)

필드 **`AWS_BUCKET_NAME`**&#x200B;은(는) `--aepUserLdap---gspem-dam`이어야 합니다.

이 정보를 사용하면 이러한 각 변수의 값을 업데이트할 수 있습니다.

```
AWS_ACCESS_KEY_ID=XXX
AWS_SECRET_ACCESS_KEY=YYY
AWS_REGION=us-west-2
AWS_BUCKET_NAME=--aepUserLdap---gspem-dam
```

이제 이 텍스트를 `.env.dev`과(와) `.env.prod` 파일에 모두 붙여 넣어야 합니다. 변경 사항을 저장하는 것을 잊지 마십시오.

![외부 DAM](./images/extdam21.png)


![외부 DAM](./images/extdam22.png)

그런 다음 터미널 창으로 돌아갑니다. 이 명령 실행:

`export $(grep -v '^#' .env.dev | xargs)`

![외부 DAM](./images/extdam23.png)

## 1.6.3.5 외부 DAM 앱 실행

터미널 창에서 `aio app run` 명령을 실행합니다. 그러면 1-2분 후에 보게 될 거예요.

![외부 DAM](./images/extdam24.png)

이제 앱이 실행 중인지 확인했습니다. 다음 단계는 배포하는 것입니다.

먼저 **CTRL+C**&#x200B;를 눌러 앱 실행을 중지합니다. 그런 다음 `aio app deploy` 명령을 입력합니다. 이 명령은 코드를 Adobe IO에 배포합니다.

따라서 배포된 애플리케이션에 액세스하기 위한 유사한 URL을 받게 됩니다.

`https://133309-201burgundyguan.adobeio-static.net/index.html`

![외부 DAM](./images/extdam27.png)

이제 테스트 목적으로 위의 URL에 접두사로 `?ext=`을(를) 추가하여 해당 URL을 쿼리 문자열 매개 변수로 사용할 수 있습니다. 그러면 이 쿼리 문자열 매개 변수가 생성됩니다.

`?ext=https://133309-201burgundyguan.adobeio-static.net/index.html`

[https://experience.adobe.com/genstudio/create](https://experience.adobe.com/genstudio/create)&#x200B;(으)로 이동합니다.

![외부 DAM](./images/extdam25.png)

그런 다음 쿼리 문자열 매개 변수를 **#** 바로 앞에 추가합니다. 새 URL은 다음과 같아야 합니다.

`https://experience.adobe.com/?ext=https://133309-201burgundyguan.adobeio-static.net/index.html#/@experienceplatform/genstudio/create`

페이지가 정상적으로 로드됩니다. 새 배너를 만들려면 **배너**&#x200B;를 클릭하십시오.

![외부 DAM](./images/extdam26.png)

템플릿을 선택하고 **사용**&#x200B;을 클릭합니다.

![외부 DAM](./images/extdam28.png)

**콘텐츠에서 선택**&#x200B;을 클릭합니다.

![외부 DAM](./images/extdam29.png)

그런 다음 드롭다운 목록에서 외부 DAM을 선택할 수 있어야 합니다.

![외부 DAM](./images/extdam30.png)

로컬 컴퓨터에서 코드를 변경할 때 앱을 다시 배포해야 합니다. 다시 배포할 때 다음 터미널 명령을 사용합니다.

`aio app deploy --force-build --force-deploy`

이제 앱을 게시할 준비가 되었습니다.

## 다음 단계

[앱을 개인적으로 게시](./ex4.md){target="_blank"}(으)로 이동

[GenStudio for Performance Marketing - 확장성](./genstudioext.md){target="_blank"}(으)로 돌아가기

[모든 모듈](./../../../overview.md){target="_blank"}(으)로 돌아가기
