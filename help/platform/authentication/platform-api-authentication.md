---
title: Experience Platform API 인증 및 액세스
description: Adobe Experience Platform API에 액세스하는 방법에 대해 알아봅니다.
role: Developer
feature: API
kt: 3688
thumbnail: 28832.jpeg
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: 60f509ef55ce121f572466a8f13953dba982a0ce
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 15%

---

# 인증 및 액세스 [!DNL Experience Platform] API

Adobe Experience Platform API에 대한 요청을 수행하려면 Experience Platform 개발자 계정이 있어야 합니다.

## Adobe Developer 콘솔에서 프로젝트 만들기 및 Postman 환경 내보내기

[[!DNL Postman]](https://www.postman.com/) 는 개발자가 Adobe Experience Platform API와 빠르고 쉽게 상호 작용할 수 있는 도구입니다.

Adobe Developer 콘솔 **Postman에 대한 세부 정보 내보내기** 기능은 단일 Postman 환경 파일의 Experience Platform API에 액세스하고 상호 작용하는 데 필요한 모든 계정 세부 정보를 쉽게 내보낼 수 있는 방법을 제공하여 Adobe Developer 콘솔에서 Postman으로 값을 복사하고 붙여넣을 필요가 없습니다.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?quality=12&learn=on)

>[!IMPORTANT]
>
>API 자격 증명을 만든 후 회사의 시스템 관리자가 자격 증명을 Experience Platform 역할과 연결해야 합니다.


## Postman으로 액세스 토큰 생성

사용 [Identity Management 서비스 API Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) Adobe Experience Platform API에 액세스하기 위해 액세스 토큰을 얻습니다.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)


## Postman을 사용하여 Experience Platform API와 상호 작용

다음을 사용하여 Adobe Experience Platform API와 상호 작용 탐색 [Adobe 제공 Experience Platform API Postman 컬렉션](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform), 을 기반으로 구축 [Adobe Developer 콘솔 환경 변수](#export-adobe-io-integration-details-to-postman) 및 [생성된 액세스 토큰](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?quality=12&learn=on)


## 추가 리소스

* [Adobe Developer Console](https://developer.adobe.com/console/home)
* [Adobe Experience Platform Postman 샘플](https://github.com/adobe/experience-platform-postman-samples)
   * [액세스 토큰 생성을 위한 Identity Management System Postman Collection](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Adobe Experience Platform API Postman 컬렉션](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [Postman 다운로드](https://www.postman.com/)
