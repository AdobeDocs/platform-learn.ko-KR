---
title: Experience Platform API 인증 및 액세스
description: Adobe Experience Platform API에 액세스하는 방법에 대해 알아봅니다.
role: Developer
feature: API
kt: 3688
thumbnail: 28832.jpeg
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 10%

---

# 인증 및 액세스 [!DNL Experience Platform] API

Adobe Experience Platform API를 호출하려면 먼저 Experience Platform 개발자 계정에 액세스할 수 있어야 합니다.

개발자 계정에 액세스하는 방법에 대한 단계별 지침은 [Experience Platform API 인증 자습서](https://www.adobe.com/go/platform-api-authentication-en).

## Experience Platform API를 만들어 Postman으로 내보내기

[Postman](https://www.getpostman.com/) 는 개발자가 Adobe Experience Platform API와 빠르고 쉽게 상호 작용할 수 있는 도구입니다.

Adobe Developer 콘솔 **Postman 내보내기 세부 사항** 기능을 사용하면 단일 Postman 환경 파일에서 Experience Platform API에 액세스하고 상호 작용하는 데 필요한 모든 계정 세부 사항을 손쉽게 내보낼 수 있으므로 Adobe Developer 콘솔에서 값을 복사하여 Postman에 붙여넣을 필요가 없습니다.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?quality=12&learn=on)

## Postman으로 액세스 토큰 생성

를 사용하십시오 [Identity Management 서비스 API Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) 비프로덕션 사용을 위해 Adobe Experience Platform API에 액세스하기 위한 액세스 토큰 가져오기

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

>[!WARNING]
>
> Adobe I/O 액세스 토큰 생성 Postman 컬렉션에서 언급한 대로, 선언된 생성 방법은 비프로덕션 사용에 적합합니다. 로컬 서명은 타사 호스트에서 JavaScript 라이브러리를 로드하고 원격 서명은 개인 키를 소유 및 운영되는 웹 서비스로 보냅니다. Adobe은 이 개인 키를 저장하지 않지만 프로덕션 키는 다른 사람과 공유해서는 안 됩니다.

## Postman을 사용하여 Adobe I/O API와 상호 작용

를 사용하여 Adobe I/O API와 상호 작용 탐색 [Adobe 제공 Experience Platform API Postman 컬렉션](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform), [Adobe I/O 환경 변수](#export-adobe-io-integration-details-to-postman) 및 [생성된 액세스 토큰](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?quality=12&learn=on)

Adobe에서 제공한 Postman 컬렉션은 모든 Adobe I/O API에 대해 존재할 수 없지만 제공된 [Experience Platform API Postman 컬렉션](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform) 는 이러한 사용 사례에 대해 고유한 Postman 컬렉션을 정의하는 방법에 대한 안내서로 사용할 수 있습니다.

## 추가 리소스

* [Adobe I/O 콘솔](https://console.adobe.io)
* [Adobe Experience Platform Postman 샘플](https://github.com/adobe/experience-platform-postman-samples)
   * [Adobe I/O 액세스 토큰 생성 Postman 컬렉션](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Adobe Experience Platform API Postman 컬렉션](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [Postman 다운로드](https://www.getpostman.com/)
