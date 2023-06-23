---
title: 개발자 콘솔 및 Postman 설정
seo-title: Set up Developer Console and Postman | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 개발자 콘솔 및 Postman 설정
description: 이 단원에서는 Adobe Developer 콘솔에서 프로젝트를 설정하고 다음을 제공합니다 [!DNL Postman] Platform API 사용을 시작할 수 있는 컬렉션
role: Data Architect, Data Engineer
feature: API
jira: KT-4348
thumbnail: 4348-set-up-developer-console-and-postman.jpg
exl-id: 72b541fa-3ea1-4352-b82b-c5b79ff98491
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 1%

---

# 개발자 콘솔 설정 및 [!DNL Postman]

<!--30min-->

이 단원에서는 Adobe Developer 콘솔에서 프로젝트를 설정하고 을 다운로드합니다 [!DNL Postman] platform API 사용을 시작할 수 있도록 컬렉션을 구성합니다.

이 자습서에서 API 연습을 완료하려면 [운영 체제용 Postman 앱을 다운로드합니다.](https://www.postman.com/downloads/) Experience Platform API를 사용하는 데 필수는 없지만 Postman을 사용하면 API 워크플로가 더 쉬워지며, Adobe Experience Platform에서는 API 호출을 실행하고 작동 방법을 학습하는 데 도움이 되는 수십 개의 Postman 컬렉션을 제공합니다. 이 자습서의 나머지 부분에서는 Postman에 대한 일부 작업 지식을 가정합니다. 도움이 필요하면 를 참조하십시오. [Postman 설명서](https://learning.postman.com/).

플랫폼은 API를 기반으로 구축됩니다. 인터페이스 옵션은 모든 주요 작업에 대해 존재하지만, 어느 시점에서 Platform API를 사용할 수도 있습니다. 예를 들어 사용자 인터페이스가 구축되기 전에 데이터를 수집하거나 샌드박스 간에 항목을 이동하고 일상적인 작업을 자동화하거나 새 Platform 기능을 사용합니다.

**데이터 설계자** 및 **데이터 엔지니어** 이 자습서 외부에서 Platform API를 사용해야 할 수도 있습니다.

## 권한 필요

다음에서 [권한 구성](configure-permissions.md) 단원, 이 단원을 완료하는 데 필요한 모든 액세스 제어를 설정합니다.

<!--
* Permission item Sandboxes > `Luma Tutorial`
* Developer-role access to the `Luma Tutorial Platform` product profile
-->

## Adobe Developer 콘솔 설정

Adobe Developer 콘솔은 Adobe API 및 SDK에 액세스하거나, 실시간에 가까운 이벤트를 듣거나, 런타임에 함수를 실행하거나, 플러그인 또는 App Builder 애플리케이션을 빌드하는 개발자 대상입니다. 이 플러그인을 사용하여 Experience Platform API에 액세스합니다. 자세한 내용은 [Adobe Developer 콘솔 설명서](https://www.adobe.io/apis/experienceplatform/console/docs.html)

1. 로컬 컴퓨터에 다음 이름의 폴더 만들기 `Luma Tutorial Assets` 자습서에 사용된 파일의 경우.

1. 를 엽니다. [Adobe Developer 콘솔](https://console.adobe.io){target="_blank"}

1. 로그인하고 올바른 조직에 속해 있는지 확인하십시오

1. 선택 **[!UICONTROL 새 프로젝트 만들기]** 위치: [!UICONTROL 빠른 시작] 메뉴 아래의 제품에서 사용할 수 있습니다.

   ![새 프로젝트 만들기](assets/adobeio-createNewProject.png)


1. 새로 만든 프로젝트에서 **[!UICONTROL 프로젝트 편집]** 단추
1. 변경 **[!UICONTROL 프로젝트 제목]** 끝 `Luma Tutorial API Project` (회사에서 여러 사람이 이 튜토리얼을 수강하는 경우 이름 추가)
1. **[!UICONTROL 저장]**&#x200B;을 선택합니다

   ![Adobe Developer 콘솔 프로젝트 API 구성](assets/adobeio-renameProject.png)


1. 선택 **[!UICONTROL API 추가]**

   ![Adobe Developer 콘솔 프로젝트 API 구성](assets/adobeio-addAPI.png)

1. 다음을 선택하여 목록 필터링 **[!UICONTROL Adobe Experience Platform]**

1. 사용 가능한 API 목록에서 **[!UICONTROL EXPERIENCE PLATFORM API]** 및 선택 **[!UICONTROL 다음]**.

   ![Adobe Developer 콘솔 프로젝트 API 구성](assets/adobeio-AEPAPI.png)

1. 선택 **[!UICONTROL OAuth 서버 간]** 을(를) 자격 증명으로 사용 및 선택 **[!UICONTROL 다음]**.
   ![OAuth 서버 간 선택](assets/adobeio-choose-auth.png)

1. 다음 항목 선택 `AEP-Default-All-Users` 제품 프로필 및 선택 **[!UICONTROL 구성된 API 저장]**

   ![제품 프로필 선택](assets/adobeio-selectProductProfile.png)

1. 이제 Developer Console 프로젝트가 생성되었습니다!

1. 다음에서 **[!UICONTROL 사용해 보기]** 페이지의 섹션에서 다음을 선택합니다. **[!UICONTROL Postman 다운로드]** 다음을 선택합니다. **[!UICONTROL OAuth 서버 간]** 을(를) 다운로드하려면 [!DNL Postman] 환경 json 파일입니다. 저장 `oauth_server_to_server.postman_environment.json` (으)로 `Luma Tutorial Assets` 폴더를 삭제합니다.


   ![Adobe Developer 콘솔 프로젝트 API 구성](assets/adobeio-io-api.png)

## 시스템 관리자가 역할에 API 자격 증명을 추가하도록 합니다

API 자격 증명을 사용하여 Experience Platform과 상호 작용하려면 시스템 관리자가 이전 단원에서 만든 역할에 API 자격 증명을 할당하도록 해야 합니다.  시스템 관리자가 아닌 경우 다음 메시지를 보냅니다.

1. 다음 [!UICONTROL 이름] API 자격 증명(`Credential in Luma Tutorial API Project`)
1. 다음 [!UICONTROL 기술 계정 이메일] 자격 증명(시스템 관리자가 자격 증명을 찾는 데 도움이 됨)

   ![[!UICONTROL 이름] 및 [!UICONTROL 기술 계정 이메일] / 자격 증명](assets/postman-credentialDetails.png)

다음은 시스템 관리자의 지침입니다.

1. 에 로그인 [Adobe Experience Platform](https://platform.adobe.com)
1. 선택 **[!UICONTROL 권한]** 을(를) 왼쪽 탐색에서 [!UICONTROL 역할] 화면
1. 를 엽니다. `Luma Tutorial Platform` 역할
   ![역할 열기](assets/postman-openRole.png)
1. 다음 항목 선택 **[!UICONTROL API 자격 증명]** 탭
1. 선택 **[!UICONTROL API 자격 증명 추가]**
   ![자격 증명 추가](assets/postman-addCredential.png)
1. 다음 찾기 `Credential in Luma Tutorial API Project` 자격 증명, 다음으로 필터링 [!UICONTROL 기술 계정 이메일] 목록이 긴 경우 튜토리얼 참가자가 제공
1. 자격 증명 선택
1. **[!UICONTROL 저장]**&#x200B;을 선택합니다


   ![자격 증명 추가](assets/postman-findCredential.png)

## Postman 설정

>[!CAUTION]
>
>Postman 인터페이스는 정기적으로 업데이트됩니다. 이 자습서의 스크린샷은 Mac용 Postman v10.15.1로 촬영되었지만 인터페이스 옵션이 변경되었을 수 있습니다.


1. 다운로드 및 설치 [[!DNL Postman]](https://www.postman.com/downloads/)
1. 열기 [!DNL Postman] 작업 공간 만들기
   ![환경 가져오기](assets/postman-createWorkspace.png)

1. 다운로드한 json 환경 파일 가져오기, `oauth_server_to_server.postman_environment.json`
   ![환경 가져오기](assets/postman-importEnvironment.png)
1. 위치 [!DNL Postman], 드롭다운에서 환경 선택

1. 아이콘을 선택하여 환경 변수를 확인합니다.

   ![환경 변경](assets/postman-changeEnvironment.png)


### 샌드박스 이름 및 테넌트 ID 추가

다음 `SANDBOX_NAME` 및 `TENANT_ID` 및 `CONTAINER_ID` 변수는 Adobe Developer 콘솔 내보내기에 포함되지 않으므로 수동으로 추가합니다.

1. 위치 [!DNL Postman]를 열고 **환경 변수**
1. 다음 항목 선택 **편집** 환경 이름 오른쪽에 있는 링크
1. 다음에서 **새 변수 필드 추가**, 입력 `SANDBOX_NAME`
1. 두 값 필드 모두에 을 입력합니다 `luma-tutorial`, 이전 단원에서 샌드박스에 제공한 이름입니다. 예를 들어 luma-tutorial-ignatiusjreilly와 같은 샌드박스에 다른 이름을 사용한 경우 해당 값을 사용해야 합니다.
1. 다음에서 **새 변수 필드 추가**, 입력 `TENANT_ID`
1. 웹 브라우저로 전환하고 Experience Platform 인터페이스로 이동하여 URL 부분을 추출하여 회사의 테넌트 ID를 조회합니다 *@ 기호 뒤*. 예를 들어 내 테넌트 ID는 입니다. `techmarketingdemos` 하지만 여러분의 의견은 다릅니다.

   ![플랫폼 인터페이스 URL에서 테넌트 ID 가져오기](assets/postman-getTenantId.png)

1. 이 값을 복사하고 로 돌아갑니다. [!DNL Postman] 환경 관리 화면
1. 두 값 필드 모두에 테넌트 ID 붙여넣기
1. 다음에서 **새 변수 필드 추가**, 입력 `CONTAINER_ID`
1. 입력 `global` 두 값 필드 모두에

   >[!NOTE]
   >
   >`CONTAINER_ID` 은 자습서 중에 값이 여러 번 변경되는 필드입니다. 날짜 `global` 이 사용되면 API는 Platform 계정의 Adobe 제공 요소와 상호 작용합니다. 날짜 `tenant` 가 사용되고 API가 고유한 사용자 지정 요소와 상호 작용합니다.

1. **저장**&#x200B;을 선택합니다

   ![SANDBOX_NAME, TENANT_ID 및 CONTAINER_ID 필드가 환경 변수로 추가됨](assets/postman-addEnvFields.png)



## API 호출 만들기

### 액세스 토큰 검색

Adobe은 다양한 세트의 [!DNL Postman] Experience Platform API를 살펴보는 데 도움이 되는 컬렉션입니다. 이러한 컬렉션은 [Adobe Experience Platform Postman 샘플 GitHub 리포지토리](https://github.com/adobe/experience-platform-postman-samples). 이 자습서 전체에서 이 리포지토리를 여러 번 사용하고 나중에 회사에 대한 Experience Platform을 구현할 때 이 리포지토리를 책갈피로 지정해야 합니다.

첫 번째 컬렉션은 Adobe Identity Management 서비스(IMS) API와 함께 작동합니다. Postman 내에서 액세스 토큰을 검색하는 편리한 방법입니다.

액세스 토큰을 생성하려면:

1. 다운로드 [Identity Management 서비스 API 컬렉션](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) (으)로 `Luma Tutorial Assets` 폴더
1. 컬렉션 가져오기 [!DNL Postman]
1. 요청 선택 **oAuth: 액세스 토큰 요청** 요청 및 선택 **보내기**
1. You should get a `200 OK` 응답에 액세스 토큰이 있는 응답

   ![토큰 요청](assets/postman-requestToken.png)

1. 액세스 토큰은 다음과 같이 자동으로 저장됩니다. **액세스 토큰** 의 환경 변수 [!DNL Postman] 환경.

   ![Postman](assets/postman-config.png)


### Platform API와 상호 작용

이제 모든 것이 올바르게 구성되었는지 확인하기 위해 Platform API 호출을 만들겠습니다.

를 엽니다. [Experience Platform [!DNL Postman] gitHub의 컬렉션](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). 이 페이지에는 다양한 Platform API에 대한 많은 컬렉션이 있습니다. 북마킹을 강력히 추천합니다

이제 첫 번째 API 호출을 만들어 보겠습니다.

1. 다운로드 [스키마 레지스트리 API 컬렉션](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Schema%20Registry%20API.postman_collection.json) (으)로 `Luma Tutorial Assets` 폴더
1. 가져오기 [!DNL Postman]
1. 열기 **스키마 레지스트리 API > 스키마 > 스키마 목록**
1. 다음을 살펴보십시오. **매개 변수** 및 **헤더** 이전에 입력한 환경 변수 중 일부를 탭에 포함하는 방법을 확인합니다.
1. 다음 사항에 주의하십시오. **헤더 > 값 필드 수락** 이(가) (으)로 설정됨 `application/vnd.adobe.xed-id+json`. 스키마 레지스트리 API에는 다음 중 하나가 필요합니다 [지정된 Accept 헤더 값](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/getting-started.html?lang=en#accept) 응답에서 다른 형식을 제공합니다.
1. 선택 **보내기** 첫 번째 Platform API를 호출하려면

네가 성공하기를 바란다 `200 OK` 아래 그림과 같이 샌드박스에서 사용 가능한 Adobe 제공 XDM 스키마 목록이 포함된 응답입니다.

![Postman의 첫 번째 API 호출](assets/postman-firstAPICall.png)

호출이 성공하지 못한 경우 잠시 API 호출의 오류 응답 세부 정보를 사용하여 디버깅하고 위의 단계를 검토하십시오. 문제가 발생하면 다음 사항에 도움을 요청하십시오. [커뮤니티 포럼](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform/ct-p/adobe-experience-platform-community) 또는 이 페이지의 오른쪽에 있는 링크를 사용하여 &quot;문제를 기록&quot;하십시오.

Platform 권한, 샌드박스 및 [!DNL Postman] 설정할 준비가 되었습니다. [스키마의 모델 데이터](model-data-in-schemas.md)!
