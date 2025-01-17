---
title: Microsoft Azure 및 사전 서명된 URL을 사용하여 Firefly 프로세스 최적화
description: Microsoft Azure 및 사전 서명된 URL을 사용하여 Firefly 프로세스 최적화
kt: 5342
doc-type: tutorial
exl-id: 5f9803a4-135c-4470-bfbb-a298ab1fee33
source-git-commit: f1f70a0e4ea3f59b5b121275e7db633caf953df9
workflow-type: tm+mt
source-wordcount: '1527'
ht-degree: 1%

---

# 1.1.2 Microsoft Azure 및 사전 서명된 URL을 사용하여 Firefly 프로세스 최적화

## 1.1.2.1 Azure 구독 만들기

>[!NOTE]
>
>기존 Azure 구독이 있는 경우 이 단계를 건너뛸 수 있습니다. 그런 경우에는 다음 연습을 진행하십시오.

[https://portal.azure.com](https://portal.azure.com)(으)로 이동하여 Azure 계정으로 로그인하세요. 전자 메일 주소가 없는 경우 개인 전자 메일 주소를 사용하여 Azure 계정을 만드세요.

![Azure 저장소](./images/02azureportalemail.png)

로그인에 성공하면 다음 화면이 표시됩니다.

![Azure 저장소](./images/03azureloggedin.png)

왼쪽 메뉴를 클릭하고 **모든 리소스**&#x200B;를 선택합니다. 아직 구독하지 않은 경우 Azure 구독 화면이 표시됩니다. 이 경우 **Azure 무료 평가판으로 시작**&#x200B;을 선택하세요.

![Azure 저장소](./images/04azurestartsubscribe.png)

Azure 구독 양식을 작성하고 활성화할 휴대폰과 신용 카드를 제공하십시오(30일 동안 프리 티어가 제공되며 업그레이드하지 않으면 요금이 부과되지 않음).

구독 프로세스가 완료되면 다음 작업을 수행할 수 있습니다.

![Azure 저장소](./images/06azuresubscriptionok.png)

## 1.1.2.2 Azure 스토리지 계정 생성

`storage account`을(를) 검색한 다음 **저장소 계정**&#x200B;을(를) 클릭합니다.

![Azure 저장소](./images/azs1.png)

**+ 만들기**&#x200B;를 클릭합니다.

![Azure 저장소](./images/azs2.png)

다음 세부 정보를 입력합니다.

- **구독** 선택
- **리소스 그룹** 선택(또는 만들기)
- **저장소 계정 이름**: `--aepUserLdap--` 사용

**검토 + 만들기**&#x200B;를 클릭합니다.

![Azure 저장소](./images/azs3.png)

**만들기**&#x200B;를 클릭합니다.

![Azure 저장소](./images/azs4.png)

그러면 유사한 확인을 받게 됩니다. **리소스로 이동**&#x200B;을 클릭합니다.

![Azure 저장소](./images/azs5.png)

이제 Azure 저장소 계정을 사용할 준비가 되었습니다.

![Azure 저장소](./images/azs6.png)

**데이터 저장소**&#x200B;를 클릭한 다음 **컨테이너**(으)로 이동합니다. **+ 컨테이너**&#x200B;를 클릭합니다.

![Azure 저장소](./images/azs7.png)

이름은 `--aepUserLdap--`을(를) 사용합니다. **만들기**&#x200B;를 클릭합니다.

![Azure 저장소](./images/azs8.png)

이제 컨테이너를 사용할 준비가 되었습니다.

![Azure 저장소](./images/azs9.png)

## 1.1.2.3 Azure Storage Explorer 설치

Microsoft Azure Storage Explorer를 사용하여 파일을 관리합니다. [이 링크](https://azure.microsoft.com/en-us/products/storage/storage-explorer#Download-4)를 통해 다운로드할 수 있습니다. 특정 OS에 맞는 버전을 선택하고 다운로드하여 설치합니다.

![Azure 저장소](./images/az10.png)

응용 프로그램이 설치되면 엽니다. 이와 비슷한 것을 보게 될 겁니다. **Azure로 로그인**&#x200B;을 클릭합니다.

![Azure 저장소](./images/az11.png)

**구독**&#x200B;을 클릭합니다.

![Azure 저장소](./images/az12.png)

**Azure**&#x200B;를 선택하고 **다음**&#x200B;을 클릭합니다.

![Azure 저장소](./images/az13.png)

Microsoft Azure 계정을 선택하고 인증 프로세스를 완료합니다.

![Azure 저장소](./images/az14.png)

인증되면 다음과 같은 메시지가 표시됩니다.

![Azure 저장소](./images/az15.png)

Microsoft Azure Storage Explorer 앱으로 다시 전환합니다. 구독을 선택하고 **탐색기 열기**&#x200B;를 클릭합니다.

>[!NOTE]
>
>계정이 표시되지 않으면 전자 메일 주소 옆에 있는 **톱니바퀴** 아이콘을 클릭하고 **필터링 해제**&#x200B;를 선택하십시오.

![Azure 저장소](./images/az16.png)

그런 다음 저장소 계정을 **저장소 계정**&#x200B;에서 찾을 수 있습니다.

![Azure 저장소](./images/az17.png)

**Blob 컨테이너**&#x200B;를 연 다음 이전 연습에서 만든 컨테이너를 클릭합니다.

![Azure 저장소](./images/az18.png)

## 1.1.2.4 수동 파일 업로드 및 이미지 파일을 스타일 참조로 사용

이제 선택한 이미지 파일을 컨테이너에 업로드해야 합니다. 원하는 이미지 파일을 사용하거나 [이 파일](./images/gradient.jpg)을(를) 컴퓨터에 다운로드하여 사용할 수 있습니다.

![Azure 저장소](./images/gradient.jpg)

이미지 파일을 Azure Storage Explorer의 컨테이너에 놓습니다.

업로드되면 컨테이너에 표시됩니다.

![Azure 저장소](./images/az19.png)

`gradient.jpg` 파일을 마우스 오른쪽 단추로 클릭한 다음 **공유 액세스 서명 가져오기**&#x200B;를 클릭합니다.

![Azure 저장소](./images/az20.png)

**권한**&#x200B;에서는 **읽기**&#x200B;만 필요합니다. **만들기**&#x200B;를 클릭합니다.

![Azure 저장소](./images/az21.png)

그러면 이 이미지 파일에 대한 사전 서명된 URL이 표시됩니다. 다음 API Firefly에 필요할 때 복사합니다.

![Azure 저장소](./images/az22.png)

Postman으로 돌아갑니다. **POST - Firefly - T2I(styleref) V3** 요청을 엽니다. 그러면 **본문**&#x200B;에서 볼 수 있습니다.

![Azure 저장소](./images/az23.png)

자리 표시자 URL을 Azure Storage Explorer에서 복사한 이미지 파일의 사전 서명된 URL로 바꿉니다. 그럼 이걸로 드셔보세요 **보내기**&#x200B;를 클릭합니다.

![Azure 저장소](./images/az24.png)

그런 다음 Firefly 서비스에서 새 이미지와 함께 응답을 다시 받게 됩니다. 브라우저에서 이미지 파일을 엽니다.

![Azure 저장소](./images/az25.png)

그러면 `horses in a field`이(가) 있는 다른 이미지가 표시되지만, 이번에는 스타일 참조로 제공한 이미지 파일과 스타일이 유사합니다.

![Azure 저장소](./images/az26.png)

## 1.1.2.5 프로그래밍 방식 파일 업로드

Azure 저장소 계정으로 프로그래밍 방식의 파일 업로드를 사용하려면 파일을 쓸 수 있는 권한을 가진 새 **SAS(공유 액세스 서명)** 토큰을 만들어야 합니다.

이렇게 하려면 Azure Storage Explorer로 돌아갑니다. 컨테이너를 마우스 오른쪽 단추로 클릭한 다음 **공유 액세스 서명 받기**&#x200B;를 클릭합니다.

![Azure 저장소](./images/az27.png)

**권한**&#x200B;에서 다음 권한이 필요합니다.

- **읽기**
- **추가**
- **만들기**
- **쓰기**
- **목록**

**만들기**&#x200B;를 클릭합니다.

![Azure 저장소](./images/az28.png)

그러면 **SAS 토큰**&#x200B;을 받게 됩니다. **복사**&#x200B;를 클릭합니다.

![Azure 저장소](./images/az29.png)

이제 이 **SAS-token**&#x200B;을 사용하여 Azure 저장소 계정에 파일을 업로드할 수 있습니다. Postman으로 돌아가 확인하십시오.

**FF - Firefly 서비스 기술 내부자** 폴더를 클릭하여 선택한 다음 **요청** 폴더에서 세 점 **..**&#x200B;을(를) 클릭하고 **Firefly 추가**&#x200B;를 클릭합니다.

![Azure 저장소](./images/az30.png)

그러면 빈 요청이 있습니다. 요청 이름을 **Azure 저장소 계정에 파일 업로드**(으)로 변경하고 **요청 유형**&#x200B;을(를) **PUT**(으)로 변경하고 SAS 토큰 URL을 URL 섹션에 붙여 넣습니다.

그런 다음 **본문**&#x200B;을 클릭합니다.

![Azure 저장소](./images/az31.png)

이제 로컬 컴퓨터에서 파일을 선택해야 합니다. 선택한 새 이미지 파일을 사용하거나 [여기](./images/gradient2-p.jpg)에서 찾을 수 있는 다른 이미지 파일을 사용할 수 있습니다.

![그라데이션 파일](./images/gradient2-p.jpg)

**본문**&#x200B;에서 **이진**&#x200B;을 선택한 다음 **파일 선택**&#x200B;을 클릭한 다음 **+ 로컬 컴퓨터에서 새 파일**&#x200B;을 클릭합니다.

![Azure 저장소](./images/az32.png)

원하는 파일을 선택하고 **열기**&#x200B;를 클릭합니다.

![Azure 저장소](./images/az33.png)

그러면 이걸 보게 될 거야. 다음으로 Azure 저장소 계정에서 사용할 파일 이름을 지정합니다. 그러려면 큐로를 **물음표 앞에 넣어야 합니다.URL의**. 현재 여기에서 이를 확인할 수 있습니다.

![Azure 저장소](./images/az34.png)

URL은 현재 다음과 비슷하지만 변경해야 합니다.

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03...`

사용할 파일 이름은 `gradient2-p.jpg`입니다. 즉, 다음과 같이 파일 이름을 포함하려면 URL을 변경해야 합니다.

`https://vangeluw.blob.core.windows.net/vangeluw/gradient2-p.jpg?sv=2023-01-03...`

![Azure 저장소](./images/az34a.png)

그런 다음 새 헤더를 수동으로 추가해야 하는 **헤더**(으)로 이동합니다. 사용:

| 키 | 값 |
|:-------------:| :---------------:| 
| `x-ms-blob-type` | `BlockBlob` |


![Azure 저장소](./images/az35.png)

**인증**(으)로 이동하여 **인증 유형**&#x200B;을(를) **인증 없음**(으)로 설정합니다. **보내기**&#x200B;를 클릭합니다.

![Azure 저장소](./images/az36.png)

그러면 Postman에서 이 빈 응답이 표시됩니다. 즉, 파일 업로드가 제대로 수행되었습니다.

![Azure 저장소](./images/az37.png)

그런 다음 Azure Storage Explorer로 돌아가서 폴더의 콘텐츠를 새로 고치면 새로 업로드된 파일이 여기에서 나타납니다.

![Azure 저장소](./images/az38.png)

## 1.1.2.6 프로그램 파일 사용

장기적으로 Azure 저장소 계정에서 파일을 프로그래밍 방식으로 읽으려면 파일을 읽을 수 있는 권한이 있는 새 **SAS(공유 액세스 서명)** 토큰을 만들어야 합니다. 기술적으로 이전 연습에서 만든 SAS 토큰을 사용할 수 있지만 가장 좋은 방법은 **읽기** 권한만 있는 별도의 토큰과 **쓰기** 권한만 있는 별도의 토큰을 사용하는 것입니다.

### 장기 읽기 SAS 토큰

이렇게 하려면 Azure Storage Explorer로 돌아갑니다. 컨테이너를 마우스 오른쪽 단추로 클릭한 다음 **공유 액세스 서명 받기**&#x200B;를 클릭합니다.

![Azure 저장소](./images/az27.png)

**권한**&#x200B;에서 다음 권한이 필요합니다.

- **읽기**
- **목록**

**만료 시간**&#x200B;을(를) 지금부터 1년으로 설정합니다.

**만들기**&#x200B;를 클릭합니다.

![Azure 저장소](./images/az100.png)

그러면 읽기 권한이 있는 장기 SAS 토큰을 받게 됩니다. URL을 복사하여 컴퓨터의 파일에 기록합니다.

![Azure 저장소](./images/az101.png)

URL은 다음과 같이 표시됩니다.

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

위의 URL에서 두 가지 값을 파생할 수 있습니다.

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

### 장기 쓰기 SAS 토큰

이렇게 하려면 Azure Storage Explorer로 돌아갑니다. 컨테이너를 마우스 오른쪽 단추로 클릭한 다음 **공유 액세스 서명 받기**&#x200B;를 클릭합니다.

![Azure 저장소](./images/az27.png)

**권한**&#x200B;에서 다음 권한이 필요합니다.

- **추가**
- **만들기**
- **쓰기**

**만료 시간**&#x200B;을(를) 지금부터 1년으로 설정합니다.

**만들기**&#x200B;를 클릭합니다.

![Azure 저장소](./images/az102.png)

그러면 읽기 권한이 있는 장기 SAS 토큰을 받게 됩니다. URL을 복사하여 컴퓨터의 파일에 기록합니다.

![Azure 저장소](./images/az103.png)

URL은 다음과 같이 표시됩니다.

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

위의 URL에서 다시 두 개의 값을 파생할 수 있습니다.

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`: `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

### Postman의 변수

위의 섹션에서 볼 수 있듯이 읽기 및 쓰기 토큰 모두에 몇 가지 일반적인 변수가 있습니다.

이제 위의 SAS 토큰의 다양한 요소를 저장할 변수를 Postman에 만들어야 합니다.
두 URL에 동일한 몇 가지 값이 있습니다.

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`: `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

향후 API 상호 작용의 경우, 주요 변경 사항은 에셋 이름이며, 위의 변수는 그대로 유지됩니다. 이 경우 매번 수동으로 지정할 필요가 없도록 Postman에서 변수를 만드는 것이 적절합니다.

이렇게 하려면 Postman을 엽니다. **환경** 아이콘을 클릭하고 **모든 변수** 메뉴를 열고 **환경**&#x200B;을 클릭합니다.

![Azure 저장소](./images/az104.png)

그럼 이걸 보게나 표시되는 표에 이 4개의 변수를 만들고 **초기 값** 및 **현재 값** 열에 대해 특정 개인 값을 입력하십시오.

- `AZURE_STORAGE_URL`: 내 url
- `AZURE_STORAGE_CONTAINER`: 컨테이너 이름
- `AZURE_STORAGE_SAS_READ`: SAS 읽기 토큰
- `AZURE_STORAGE_SAS_WRITE`: SAS 쓰기 토큰

**저장**&#x200B;을 클릭합니다.

![Azure 저장소](./images/az105.png)

이전 연습 중 하나에서 **Firefly - T2I(styleref) V3** 요청의 **본문**&#x200B;은(는) 다음과 같이 표시되었습니다.

`"url": "https://vangeluw.blob.core.windows.net/vangeluw/gradient.jpg?sv=2023-01-03&st=2025-01-13T07%3A16%3A52Z&se=2026-01-14T07%3A16%3A00Z&sr=b&sp=r&sig=x4B1XZuAx%2F6yUfhb28hF0wppCOMeH7Ip2iBjNK5A%2BFw%3D"`

![Azure 저장소](./images/az24.png)

이제 URL을 다음과 같이 변경할 수 있습니다.

`"url": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/gradient.jpg{{AZURE_STORAGE_SAS_READ}}"`

변경 내용을 테스트하려면 **보내기**&#x200B;를 클릭하세요.

![Azure 저장소](./images/az106.png)

변수가 올바른 방식으로 구성된 경우 이미지 URL이 반환됩니다.

![Azure 저장소](./images/az107.png)

이미지 URL을 열어 이미지를 확인합니다.

![Azure 저장소](./images/az108.jpg)

다음 단계: [1.1.3 Adobe Firefly 및 Adobe Photoshop](./ex3.md)

[모듈 1.1로 돌아가기](./firefly-services.md)

[모든 모듈로 돌아가기](./../../../overview.md)
