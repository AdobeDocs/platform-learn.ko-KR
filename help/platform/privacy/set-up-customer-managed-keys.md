---
title: CMK(고객 관리 키) 설정
description: 자체 암호화 키를 사용하여 사용하지 않는 데이터 암호화를 관리합니다.
feature: Privacy
role: Admin, Data Architect, Data Engineer, Developer
level: Experienced
jira: KT-11382
thumbnail: 3410673.jpeg
last-substantial-update: 2024-06-28T00:00:00Z
exl-id: 04cb1aeb-3260-4259-bb02-8392d9d787a2
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 8%

---

# CMK(고객 관리 키) 설정

자체 암호화 키를 사용하여 활용도가 낮은 데이터 암호화를 관리합니다. 자세한 내용은 [고객 관리 키 설명서](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/customer-managed-keys.html?lang=ko)를 참조하세요.

>[!VIDEO](https://video.tv.adobe.com/v/3410673/?learn=on&enablevpops)

>[!IMPORTANT]
>
> Adobe Experience Platform의 고객 관리 키는 현재 Healthcare Shield 또는 Privacy and Security Shield 고객만 사용할 수 있습니다.

>[!WARNING]
>
>CMK를 설정한 후에는 시스템 관리 키로 되돌릴 수 없습니다. Azure에서 키를 안전하게 관리하고 Key Vault, Key 및 CMK 앱에 대한 액세스 권한을 제공하여 데이터에 대한 액세스 권한을 상실하지 않도록 해야 합니다.
