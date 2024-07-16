---
title: Experience Platform API 인증 및 액세스
description: Adobe Experience Platform API에 액세스하는 방법에 대해 알아봅니다.
feature: API
role: Developer
level: Beginner
jira: KT-3688
thumbnail: 28832.jpeg
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 10%

---

# [!DNL Experience Platform]개 API 인증 및 액세스

Adobe Experience Platform API를 시작하는 방법을 알아봅니다. 이 튜토리얼에서는 인증 자격 증명을 만들고 Experience Platform API 요청을 시작하는 프로세스를 안내합니다.

## Adobe Developer Console에서 프로젝트를 만들고 Postman 환경 내보내기{#export-integration-details-to-postman}

[[!DNL Postman]](https://www.postman.com/)은(는) 개발자가 Adobe Experience Platform API와 빠르고 쉽게 상호 작용할 수 있도록 지원하는 타사 애플리케이션입니다.

[Adobe Developer Console의](https://developer.adobe.com/console/home) **Postman에 대한 세부 정보 내보내기** 기능을 사용하면 단일 Postman 환경 파일의 Experience Platform API에 액세스하고 상호 작용하는 데 필요한 계정 세부 정보를 쉽게 내보낼 수 있으므로 Adobe Developer Console에서 Postman으로 값을 복사하여 붙여넣을 필요가 없습니다.

>[!IMPORTANT]
>
>[Adobe Developer Console](https://developer.adobe.com/console/home)에 액세스하려면 [Adobe Admin Console](https://adminconsole.adobe.com)의 [시스템 관리자](https://helpx.adobe.com/enterprise/using/admin-roles.html) 또는 [개발자](https://helpx.adobe.com/enterprise/using/manage-developers.html#:~:text=Add%20developers%20to%20a%20single%20product%20profile&amp;text=In%20the%20Admin%20Console%2C%20navigate,in%20the%20upper%2Dright%20corner.)여야 합니다.
>
> API 자격 증명을 만든 후 시스템 관리자는 자격 증명을 Experience Platform의 역할과 연결해야 합니다.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on)

## Postman으로 액세스 토큰 생성{#generate-an-access-token-with-postman}

[Adobe Identity Management 서비스 API](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)를 사용하여 Adobe Experience Platform API에 액세스할 수 있는 액세스 토큰을 얻으십시오.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?learn=on)


## Postman을 사용하여 Experience Platform API와 상호 작용

[Adobe 제공 Experience Platform API Postman 컬렉션](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)을 사용하여 [Adobe Developer Console 환경 변수](#export-integration-details-to-postman) 및 [생성된 액세스 토큰](#generate-an-access-token-with-postman)을 기반으로 빌드하는 Adobe Experience Platform API와 상호 작용하는 방법을 살펴봅니다.

>[!VIDEO](https://video.tv.adobe.com/v/29704/?learn=on)


## 이 비디오에서 참조된 리소스

* [Adobe Developer Console](https://developer.adobe.com/console/home)
* [Adobe Experience Platform Postman 샘플](https://github.com/adobe/experience-platform-postman-samples)
   * [액세스 토큰을 생성하기 위한 Identity Management System Postman 컬렉션](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Adobe Experience Platform API Postman 컬렉션](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [Postman 다운로드](https://www.postman.com/)
