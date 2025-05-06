---
title: 시작하기 - Adobe I/O
description: 시작하기 - Adobe I/O
kt: 5342
doc-type: tutorial
exl-id: 00f17d4f-a2c8-4e8e-a1ff-556037a60629
source-git-commit: cc8efbdbcf90607f5a9bc98a2e787b61b4cd66d9
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# Adobe I/O 프로젝트 구성

## Adobe I/O 프로젝트 만들기

이 연습에서는 Adobe I/O을 사용하여 다양한 Adobe 끝점을 쿼리합니다. Adobe I/O을 설정하려면 다음 단계를 따르십시오.

[https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}(으)로 이동합니다.

![Adobe I/O 새 통합](./images/iohome.png){zoomable="yes"}

화면 오른쪽 상단 모서리에서 올바른 인스턴스를 선택해야 합니다. 인스턴스는 `--aepImsOrgName--`입니다.

>[!NOTE]
>
> 아래 스크린샷은 선택된 특정 조직을 보여 줍니다. 이 자습서를 수행하는 경우 조직의 이름이 다를 수 있습니다. 이 자습서에 등록하면 사용할 환경 세부 정보가 제공되었으므로 해당 지침을 따르십시오.

**새 프로젝트 만들기**&#x200B;를 선택합니다.

![Adobe I/O 새 통합](./images/iocomp.png){zoomable="yes"}

### FIREFLY SERVICES API

그럼 이걸 보셔야죠 **+ 프로젝트에 추가**&#x200B;를 선택하고 **API**&#x200B;를 선택합니다.

![Adobe I/O 새 통합](./images/adobe_io_access_api.png){zoomable="yes"}

화면이 다음과 같아야 합니다.

![Adobe I/O 새 통합](./images/api1.png){zoomable="yes"}

**Creative Cloud**&#x200B;을(를) 선택하고 **Firefly - Firefly Services**&#x200B;을(를) 선택한 후 **다음**&#x200B;을(를) 선택합니다.

![Adobe I/O 새 통합](./images/api3.png){zoomable="yes"}

자격 증명의 이름을 지정하십시오. `--aepUserLdap-- - One Adobe OAuth credential`다음 **다음**&#x200B;을 선택하세요.

![Adobe I/O 새 통합](./images/api4.png){zoomable="yes"}

기본 프로필 **기본 Firefly Services 구성**&#x200B;을 선택하고 **구성된 API 저장**&#x200B;을 선택합니다.

![Adobe I/O 새 통합](./images/api9.png){zoomable="yes"}

그럼 이걸 보셔야죠

![Adobe I/O 새 통합](./images/api10.png){zoomable="yes"}

### PHOTOSHOP SERVICES API

**+ 프로젝트에 추가**&#x200B;를 선택한 다음 **API**&#x200B;를 선택합니다.

![Azure 저장소](./images/ps2.png){zoomable="yes"}

**Creative Cloud**&#x200B;을(를) 선택하고 **Photoshop - Firefly Services**&#x200B;을(를) 선택합니다. **다음**&#x200B;을 선택합니다.

![Azure 저장소](./images/ps3.png){zoomable="yes"}

**다음**&#x200B;을 선택합니다.

![Azure 저장소](./images/ps4.png){zoomable="yes"}

그런 다음 이 통합에 사용할 수 있는 권한을 정의하는 제품 프로필을 선택해야 합니다.

**기본 Firefly Services 구성** 및 **기본 Creative Cloud 자동화 서비스 구성**&#x200B;을 선택합니다.

**구성된 API 저장**&#x200B;을 선택합니다.

![Azure 저장소](./images/ps5.png){zoomable="yes"}

그럼 이걸 보셔야죠

![Adobe I/O 새 통합](./images/ps7.png){zoomable="yes"}

### ADOBE EXPERIENCE PLATFORM API

**+ 프로젝트에 추가**&#x200B;를 선택한 다음 **API**&#x200B;를 선택합니다.

![Azure 저장소](./images/aep1.png){zoomable="yes"}

**Adobe Experience Platform**&#x200B;을 선택하고 **Experience Platform API**&#x200B;를 선택합니다. **다음**&#x200B;을 선택합니다.

![Azure 저장소](./images/aep2.png){zoomable="yes"}

**다음**&#x200B;을 선택합니다.

![Azure 저장소](./images/aep3.png){zoomable="yes"}

그런 다음 이 통합에 사용할 수 있는 권한을 정의하는 제품 프로필을 선택해야 합니다.

**Adobe Experience Platform - 모든 사용자 - PROD**&#x200B;를 선택합니다.

**구성된 API 저장**&#x200B;을 선택합니다.

![Azure 저장소](./images/aep4.png){zoomable="yes"}

그럼 이걸 보셔야죠

![Adobe I/O 새 통합](./images/aep5.png){zoomable="yes"}

### 프로젝트 이름

프로젝트 이름을 클릭합니다.

![Adobe I/O 새 통합](./images/api13.png){zoomable="yes"}

**프로젝트 편집**&#x200B;을 선택합니다.

![Adobe I/O 새 통합](./images/api14.png){zoomable="yes"}

통합 이름을 입력하십시오. `--aepUserLdap-- One Adobe tutorial`다음 **저장**&#x200B;을 선택합니다.

![Adobe I/O 새 통합](./images/api15.png){zoomable="yes"}

Adobe I/O 프로젝트 설정이 완료되었습니다.

![Adobe I/O 새 통합](./images/api16.png){zoomable="yes"}

## 다음 단계

[옵션 1: Postman 설치](./ex7.md){target="_blank"}(으)로 이동

[옵션 2: PostBuster 설정](./ex8.md){target="_blank"}(으)로 이동

[시작하기](./getting-started.md){target="_blank"}(으)로 돌아가기

[모든 모듈](./../../../overview.md){target="_blank"}(으)로 돌아가기
