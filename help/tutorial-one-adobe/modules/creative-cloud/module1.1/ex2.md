---
title: Microsoft Azure 및 사전 서명된 URL을 사용하여 Firefly 프로세스 최적화
description: Microsoft Azure 및 사전 서명된 URL을 사용하여 Firefly 프로세스를 최적화하는 방법을 알아봅니다
role: Developer
level: Beginner
jira: KT-5342
doc-type: tutorial
exl-id: 5f9803a4-135c-4470-bfbb-a298ab1fee33
source-git-commit: 8e410ad378d61f23d1d880d12e57f9d5e4e523c1
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 1%

---

# Microsoft Azure 및 사전 서명된 URL을 사용하여 Firefly 프로세스 최적화

Microsoft Azure 및 사전 서명된 URL을 사용하여 Firefly 프로세스를 최적화하는 방법을 알아봅니다.

## Azure 구독 만들기

>[!NOTE]
>
>기존 Azure 구독이 있는 경우 이 단계를 건너뛸 수 있습니다. 그런 경우에는 다음 연습을 진행하십시오.

1. [https://portal.azure.com](https://portal.azure.com){target="_blank"}(으)로 이동하여 Azure 계정으로 로그인하세요. 전자 메일 주소가 없는 경우 개인 전자 메일 주소를 사용하여 Azure 계정을 만드세요.

   ![Azure 저장소](./images/02azureportalemail.png)

   로그인에 성공하면 다음 화면이 표시됩니다.

   ![Azure 저장소](./images/03azureloggedin.png)

1. 아직 구독하지 않은 경우 왼쪽 메뉴에서 **모든 리소스**&#x200B;를 선택하면 Azure 구독 화면이 표시됩니다.

1. 구독하지 않은 경우 **Azure 무료 평가판으로 시작**&#x200B;을 선택하세요.

   ![Azure 저장소](./images/04azurestartsubscribe.png)

1. Azure 구독 양식을 작성하고 활성화할 휴대폰과 신용 카드를 제공하십시오(30일 동안 프리 티어가 제공되며 업그레이드하지 않으면 요금이 부과되지 않음).

   가입 절차가 끝나면 가셔도 좋습니다.

   ![Azure 저장소](./images/06azuresubscriptionok.png)

## Azure 스토리지 계정 만들기

1. `storage account`을(를) 검색한 다음 **저장소 계정**&#x200B;을(를) 선택하십시오.

   ![Azure 저장소](./images/azs1.png)

1. **+ 만들기**&#x200B;를 선택합니다.

![Azure 저장소](./images/azs2.png)

1. **구독**&#x200B;을(를) 선택하고 **리소스 그룹**&#x200B;을(를) 선택하거나 만듭니다.

1. **저장소 계정 이름**&#x200B;에서 `--aepUserLdap--`을(를) 사용합니다.

1. **검토 + 만들기**&#x200B;를 선택합니다.

   ![Azure 저장소](./images/azs3.png)

1. **만들기**&#x200B;를 선택합니다.

   ![Azure 저장소](./images/azs4.png)

1. 확인 후 **리소스로 이동**&#x200B;을 선택합니다.

       ![Azure 스토리지](./images/azs5.png)
   
이제 Azure 저장소 계정을 사용할 준비가 되었습니다.

    ![Azure 스토리지](./images/azs6.png)

1. **데이터 저장소**&#x200B;를 선택한 다음 **컨테이너**(으)로 이동합니다. **+ 컨테이너**&#x200B;을(를) 선택하십시오.

   ![Azure 저장소](./images/azs7.png)

1. 이름에 `--aepUserLdap--`을(를) 사용하고 **만들기**&#x200B;를 선택하십시오.

   ![Azure 저장소](./images/azs8.png)

   이제 컨테이너를 사용할 준비가 되었습니다.

   ![Azure 저장소](./images/azs9.png)

## 1.1.2.3 Azure Storage Explorer 설치

1. [파일을 관리하려면 Microsoft Azure 저장소 탐색기를 다운로드하세요](https://azure.microsoft.com/en-us/products/storage/storage-explorer#Download-4){target="_blank"}. 특정 OS에 맞는 버전을 선택하고 다운로드하여 설치합니다.

   ![Azure 저장소](./images/az10.png)

1. 응용 프로그램을 열고 **Azure로 로그인**&#x200B;을 선택합니다.

   ![Azure 저장소](./images/az11.png)

1. **구독**&#x200B;을 선택하세요.

   ![Azure 저장소](./images/az12.png)

1. **Azure**&#x200B;를 선택한 후 **다음**&#x200B;을 선택하세요.

   ![Azure 저장소](./images/az13.png)

1. Microsoft Azure 계정을 선택하고 인증 프로세스를 완료합니다.

   ![Azure 저장소](./images/az14.png)

   인증 후 이 메시지가 나타납니다.

   ![Azure 저장소](./images/az15.png)

1. Microsoft Azure Storage Explorer 앱으로 돌아가서 구독을 선택하고 **탐색기 열기**&#x200B;를 선택합니다.

>[!NOTE]
>
>계정이 표시되지 않으면 전자 메일 주소 옆에 있는 **톱니바퀴** 아이콘을 클릭하고 **필터링 해제**&#x200B;를 선택하십시오.

    ![Azure 스토리지](./images/az16.png)

저장소 계정이 **저장소 계정**&#x200B;에 나타납니다.

    ![Azure 스토리지](./images/az17.png)

1. **Blob 컨테이너**&#x200B;를 연 다음 이전 연습에서 만든 컨테이너를 선택합니다.

   ![Azure 저장소](./images/az18.png)

## 수동 파일 업로드 및 이미지 파일을 스타일 참조로 사용

1. 원하는 이미지 파일을 업로드하거나 [이 파일](./images/gradient.jpg){target="_blank"}을 컨테이너에 업로드하십시오.

   ![Azure 저장소](./images/gradient.jpg)

   업로드한 후에는 컨테이너에서 볼 수 있습니다.

   ![Azure 저장소](./images/az19.png)

1. `gradient.jpg`을(를) 마우스 오른쪽 단추로 클릭한 다음 **공유 액세스 서명 가져오기**&#x200B;를 선택합니다.

   ![Azure 저장소](./images/az20.png)

1. **권한**&#x200B;에서는 **읽기**&#x200B;만 필요합니다. **만들기**&#x200B;를 선택합니다.

   ![Azure 저장소](./images/az21.png)

1. Firefly에 대한 다음 API 요청에 대해 이 이미지 파일의 사전 서명된 URL을 복사합니다.

   ![Azure 저장소](./images/az22.png)

1. Postman으로 돌아가서 **POST - Firefly - T2I(styleref) V3** 요청을 엽니다.
**본문**&#x200B;에 나타납니다.

   ![Azure 저장소](./images/az23.png)

1. 자리 표시자 URL을 이미지 파일의 사전 서명된 URL로 바꾸고 **보내기**&#x200B;를 선택합니다.

   ![Azure 저장소](./images/az24.png)

1. 브라우저에서 응답 Firefly 서비스 새 이미지를 엽니다.

   ![Azure 저장소](./images/az25.png)

   다른 이미지는 `horses in a field`과(와) 함께 표시되지만, 이번에는 스타일 참조로 제공한 이미지 파일과 비슷합니다.

   ![Azure 저장소](./images/az26.png)

## 프로그램 파일 업로드

Azure 저장소 계정으로 프로그래밍 방식의 파일 업로드를 사용하려면 파일을 쓸 수 있는 권한을 가진 새 **SAS(공유 액세스 서명)** 토큰을 만들어야 합니다.

1. Azure 저장소 탐색기에서 컨테이너를 마우스 오른쪽 단추로 클릭하고 **공유 액세스 서명 가져오기**&#x200B;를 선택합니다.

   ![Azure 저장소](./images/az27.png)

1. **권한**&#x200B;에서 다음 필수 권한을 선택하십시오.

   - **읽기**
   - **추가**
   - **만들기**
   - **쓰기**
   - **목록**

1. **만들기**&#x200B;를 선택합니다.

   ![Azure 저장소](./images/az28.png)

1. **SAS-token**&#x200B;을 받은 후 **복사**&#x200B;를 선택하세요.

   ![Azure 저장소](./images/az29.png)

   **SAS-token**&#x200B;을 사용하여 Azure 저장소 계정에 파일을 업로드하세요.

1. Postman으로 돌아가서 **FF - Firefly 서비스 기술 내부자** 폴더를 선택한 다음 **Firefly** 폴더에서 **..**&#x200B;을(를) 선택하고 **요청 추가**&#x200B;를 선택합니다.

   ![Azure 저장소](./images/az30.png)

1. 빈 요청의 이름을 **Azure 저장소 계정에 파일 업로드**(으)로 변경하고 **요청 유형**&#x200B;을(를) **PUT**(으)로 변경하고 SAS 토큰 URL을 URL 섹션에 붙여 넣은 다음 **본문**&#x200B;을(를) 선택합니다.

   ![Azure 저장소](./images/az31.png)

1. 그런 다음 로컬 컴퓨터에서 파일을 선택하거나 [여기](./images/gradient2-p.jpg){target="_blank"}에 있는 다른 이미지 파일을 사용하십시오.

   ![그라데이션 파일](./images/gradient2-p.jpg)

1. **본문**&#x200B;에서 **이진**, **파일 선택**&#x200B;을 차례로 선택한 다음 **+ 로컬 컴퓨터에서 새 파일을 선택합니다**.

   ![Azure 저장소](./images/az32.png)

1. 선택한 파일을 선택하고 **열기**&#x200B;를 선택합니다.

   ![Azure 저장소](./images/az33.png)

1. 그런 다음 물음표 **앞에 커서를 놓아 Azure 저장소 계정에서 사용할 파일 이름을 지정하십시오.다음과 같은 URL의**:

   ![Azure 저장소](./images/az34.png)

   URL은 현재 다음과 비슷하지만 변경해야 합니다.

   `https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03...`

1. 파일 이름을 `gradient2-p.jpg`(으)로 변경하고 다음과 같이 파일 이름을 포함하도록 URL을 변경합니다.

   `https://vangeluw.blob.core.windows.net/vangeluw/gradient2-p.jpg?sv=2023-01-03...`

   ![Azure 저장소](./images/az34a.png)

1. 그런 다음 **헤더**(으)로 이동하여 다음과 같이 새 헤더를 수동으로 추가합니다.

   | 키 | 값 |
   |:-------------:| :---------------:| 
   | `x-ms-blob-type` | `BlockBlob` |


   ![Azure 저장소](./images/az35.png)

1. **인증**(으)로 이동하여 **인증 유형**&#x200B;을(를) **인증 없음**(으)로 설정하고 **전송**&#x200B;을(를) 선택합니다.

   ![Azure 저장소](./images/az36.png)

1. 그런 다음 이 빈 응답이 Postman에 나타나며 이는 파일 업로드가 괜찮음을 의미합니다.

   ![Azure 저장소](./images/az37.png)

1. Azure Storage Explorer로 돌아가면 폴더의 콘텐츠가 새로 고침되고 새로 업로드된 파일이 나타납니다.

   ![Azure 저장소](./images/az38.png)

## 프로그래밍 파일 사용

장기적으로 Azure 저장소 계정에서 파일을 프로그래밍 방식으로 읽으려면 파일을 읽을 수 있는 권한이 있는 새 **SAS(공유 액세스 서명)** 토큰을 만들어야 합니다. 기술적으로 이전 연습에서 만든 SAS 토큰을 사용할 수 있지만 가장 좋은 방법은 **읽기** 권한만 있는 별도의 토큰과 **쓰기** 권한만 있는 별도의 토큰을 사용하는 것입니다.

### 장기 읽기 SAS 토큰

1. Azure Storage Explorer로 돌아가서 컨테이너를 마우스 오른쪽 단추로 클릭한 다음 **공유 액세스 서명 가져오기**&#x200B;를 선택합니다.

   ![Azure 저장소](./images/az27.png)

1. **권한**&#x200B;에서 다음 필수 권한을 선택하십시오.

   - **읽기**
   - **목록**

1. **만료 시간**&#x200B;을(를) 지금부터 1년으로 설정합니다.

1. **만들기**&#x200B;를 선택합니다.

   ![Azure 저장소](./images/az100.png)

1. URL을 복사하고 컴퓨터의 파일에 기록하여 읽기 권한이 있는 장기 SAS 토큰을 가져옵니다.

   ![Azure 저장소](./images/az101.png)

   URL은 다음과 같아야 합니다.

   `https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

   위의 URL에서 두 가지 값을 파생할 수 있습니다.

   - `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
   - `AZURE_STORAGE_CONTAINER`: `vangeluw`
   - `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

### 장기 쓰기 SAS 토큰

1. Azure Storage Explorer로 돌아가서 컨테이너를 마우스 오른쪽 단추로 클릭하고 **공유 액세스 서명 가져오기**&#x200B;를 선택합니다.

   ![Azure 저장소](./images/az27.png)

1. **권한**&#x200B;에서 다음 필수 권한을 선택하십시오.

   - **추가**
   - **만들기**
   - **쓰기**

1. **만료 시간**&#x200B;을(를) 지금부터 1년으로 설정합니다.

1. **만들기**&#x200B;를 선택합니다.

   ![Azure 저장소](./images/az102.png)

1. URL을 복사하고 컴퓨터의 파일에 기록하여 읽기 권한이 있는 장기 SAS 토큰을 가져옵니다.

   ![Azure 저장소](./images/az103.png)

   URL은 다음과 같아야 합니다.

   `https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

위의 URL에서 두 가지 값을 파생할 수 있습니다.

    - &#39;AZURE_STORAGE_URL&#39;: &#39;https://vangeluw.blob.core.windows.net&#39;
    - &#39;AZURE_STORAGE_CONTAINER&#39;: &#39;vangeluw&#39;
    - &#39;AZURE_STORAGE_SAS_READ&#39;: &#39;?sv=2023-01-03&amp;st=2025-01-13T07%3A36%3A35Z&amp;se=2026-01-14T07%3A36%3A00Z&amp;sr=c&amp;sp=rl&amp;sig=4r%2FcSJLlt%2LT bst9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
    - &#39;AZURE_STORAGE_SAS_WRITE&#39;: `?sv=2023-01-03&amp;st=2025-01-13T07%3A38%3A59Z&amp;se=2026-01-14T07%3A38%3A00Z&amp;sr=c&amp;sp=acw&amp;sig=l9%2R fmuYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

### Postman의 변수

위의 섹션에서 볼 수 있듯이 읽기 및 쓰기 토큰 모두에 몇 가지 일반적인 변수가 있습니다.

그런 다음 위의 SAS 토큰의 다양한 요소를 저장하는 변수를 Postman에서 만들어야 합니다. 두 URL에 동일한 몇 가지 값이 있습니다.

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`: `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

향후 API 상호 작용의 경우, 주요 변경 사항은 에셋 이름이지만 위의 변수는 동일합니다. 이 경우 매번 수동으로 지정할 필요가 없도록 Postman에서 변수를 만드는 것이 적절합니다.

1. Postman에서 **환경**&#x200B;을 선택하고 **모든 변수**&#x200B;을 연 다음 **환경**&#x200B;을 선택합니다.

   ![Azure 저장소](./images/az104.png)

1. 표시되는 표에 이 4개의 변수를 만들고 **초기 값** 및 **현재 값** 열에 대해 특정 개인 값을 입력하십시오.

   - `AZURE_STORAGE_URL`: 내 url
   - `AZURE_STORAGE_CONTAINER`: 컨테이너 이름
   - `AZURE_STORAGE_SAS_READ`: SAS 읽기 토큰
   - `AZURE_STORAGE_SAS_WRITE`: SAS 쓰기 토큰

1. **저장**&#x200B;을 선택합니다.

   ![Azure 저장소](./images/az105.png)

   이전 연습 중 하나에서 **Firefly - T2I(styleref) V3** 요청의 **본문**&#x200B;은(는) 다음과 같이 표시되었습니다.

   `"url": "https://vangeluw.blob.core.windows.net/vangeluw/gradient.jpg?sv=2023-01-03&st=2025-01-13T07%3A16%3A52Z&se=2026-01-14T07%3A16%3A00Z&sr=b&sp=r&sig=x4B1XZuAx%2F6yUfhb28hF0wppCOMeH7Ip2iBjNK5A%2BFw%3D"`

   ![Azure 저장소](./images/az24.png)

1. URL을 다음으로 변경:

   `"url": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/gradient.jpg{{AZURE_STORAGE_SAS_READ}}"`

1. 변경 내용을 테스트하려면 **보내기**&#x200B;를 선택하십시오.

   ![Azure 저장소](./images/az106.png)

   변수가 올바르게 구성된 경우 이미지 URL이 반환됩니다.

   ![Azure 저장소](./images/az107.png)

1. 이미지 URL을 열어 이미지를 확인합니다.

   ![Azure 저장소](./images/az108.jpg)

## 다음 단계

[Adobe Firefly 및 Adobe Photoshop API](./ex3.md){target="_blank"}(으)로 이동

[Adobe Firefly 서비스 개요](./firefly-services.md){target="_blank"}(으)로 돌아가기

[모든 모듈](./../../../overview.md){target="_blank"}(으)로 돌아가기