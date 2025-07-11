---
title: Experience Platform API 인증 및 액세스
description: Adobe Experience Platform API에 액세스하는 방법에 대해 알아봅니다.
feature: API
role: Developer
level: Beginner,Intermediate
doc-type: Technical Video
duration: 226
last-substantial-update: 2023-06-21T00:00:00Z
jira: KT-3688
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: 311b296d67cf39867e7c9f3fd9f0458dfefcfdfd
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 7%

---

# [!DNL Experience Platform]개 API 인증 및 액세스

Adobe Experience Platform API를 시작하는 방법을 알아봅니다. 첫 번째 단계는 Adobe Developer Console에서 프로젝트를 만들고 자격 증명을 얻는 것입니다. 이 튜토리얼에서는 Experience Platform API 요청을 시작할 수 있도록 Adobe Developer Console에서 프로젝트를 만들고 Postman 환경 파일을 내보내는 프로세스를 안내합니다.

[[!DNL Postman]](https://www.postman.com/)은(는) 개발자가 Adobe Experience Platform API와 빠르고 쉽게 상호 작용할 수 있도록 지원하는 타사 애플리케이션입니다.

[Adobe Developer Console의](https://developer.adobe.com/console/home) **Postman에 대한 세부 정보 내보내기** 기능을 사용하면 단일 Postman 환경 파일에서 Experience Platform API에 액세스하고 상호 작용하는 데 필요한 계정 세부 정보를 쉽게 내보낼 수 있으므로 Adobe Developer Console에서 Postman으로 값을 복사하여 붙여넣을 필요가 없습니다.

>[!IMPORTANT]
>
>[Adobe Developer Console](https://developer.adobe.com/console/home)에 액세스하려면 [Adobe Admin Console](https://helpx.adobe.com/enterprise/using/admin-roles.html)의 [시스템 관리자](https://helpx.adobe.com/enterprise/using/manage-developers.html#:~:text=Add%20developers%20to%20a%20single%20product%20profile&text=In%20the%20Admin%20Console%2C%20navigate,in%20the%20upper%2Dright%20corner.) 또는 [개발자](https://adminconsole.adobe.com)여야 합니다.
>
> API 자격 증명을 만든 후 시스템 관리자는 자격 증명을 Experience Platform의 역할에 연결해야 합니다.
>
>자세한 지침은 [개발자 추가 및 API 자격 증명에 대한 권한 부여 튜토리얼](../admin/add-developers.md)을 참조하세요.


>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on&enablevpops)

<!-- CARDS
* generate-an-access-token.md
* use-apis-with-postman.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Generate an Experience Platform API access token with Postman">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="generate-an-access-token.md" title="Postman을 사용하여 Experience Platform API 액세스 토큰 생성" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/29698/?format=jpeg&nocache=1752259602830" alt="Postman을 사용하여 Experience Platform API 액세스 토큰 생성"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="generate-an-access-token.md" target="_blank" rel="referrer" title="Postman을 사용하여 Experience Platform API 액세스 토큰 생성">Postman을 사용하여 Experience Platform API 액세스 토큰 생성</a>
                    </p>
                    <p class="is-size-6">Postman을 사용하여 Experience Platform API 액세스 토큰을 생성하는 방법을 알아봅니다</p>
                </div>
                <a href="generate-an-access-token.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Use Experience Platform APIs with Postman">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="use-apis-with-postman.md" title="Postman에서 Experience Platform API 사용" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/29704/?format=jpeg&nocache=1752259602844" alt="Postman에서 Experience Platform API 사용"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="use-apis-with-postman.md" target="_blank" rel="referrer" title="Postman에서 Experience Platform API 사용">Postman에서 Experience Platform API 사용</a>
                    </p>
                    <p class="is-size-6">Adobe에서 제공한 Postman 컬렉션을 사용하여 Adobe Experience Platform API 탐색</p>
                </div>
                <a href="use-apis-with-postman.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->
