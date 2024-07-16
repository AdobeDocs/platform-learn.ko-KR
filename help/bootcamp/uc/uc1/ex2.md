---
title: 부트캠프 - 실시간 고객 프로필 - 나만의 실시간 고객 프로필 시각화 - UI
description: 부트캠프 - 실시간 고객 프로필 - 나만의 실시간 고객 프로필 시각화 - UI
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 4c810767-00ab-4cae-baa9-97b0cb9bf2df
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# 1.2 자신의 실시간 고객 프로필 시각화 - UI

이 연습에서는 Adobe Experience Platform에 로그인하여 UI에서 자신의 실시간 고객 프로필을 봅니다.

## 스토리

실시간 고객 프로필에는 모든 프로필 데이터가 기존 대상 멤버십은 물론 이벤트 데이터와 함께 표시됩니다. 표시된 데이터는 Adobe 애플리케이션 및 외부 솔루션에서 어디에서나 가져올 수 있습니다. 이것은 기록의 진정한 경험 시스템인 Adobe Experience Platform에서 가장 강력한 보기입니다.

## 1.2.1 Adobe Experience Platform에서 고객 프로필 보기 사용

[Adobe Experience Platform](https://experience.adobe.com/platform)(으)로 이동합니다. 로그인하면 Adobe Experience Platform 홈페이지에 접속하게 됩니다.

![데이터 수집](./images/home.png)

계속하려면 **샌드박스**&#x200B;를 선택해야 합니다. 선택할 샌드박스 이름이 ``Bootcamp``입니다. 화면 상단의 파란색 선에 있는 텍스트 **[!UICONTROL 프로덕션]**&#x200B;을(를) 클릭하면 됩니다. 적절한 [!UICONTROL 샌드박스]를 선택하면 화면이 변경되고 이제 전용 [!UICONTROL 샌드박스]에 있게 됩니다.



왼쪽 메뉴에서 **프로필** 및 **찾아보기**(으)로 이동합니다.

![고객 프로필](./images/homemenu.png)

웹 사이트의 프로필 뷰어 패널에서 ID 개요를 찾을 수 있습니다. 모든 ID는 네임스페이스에 연결됩니다.

![고객 프로필](./images/identities.png)




Adobe Experience Platform을 사용하면 모든 ID가 동일하게 중요합니다. 이전에는 ECID가 Adobe 컨텍스트에서 가장 중요한 ID였으며 다른 모든 ID는 계층 구조로 ECID에 연결되어 있었습니다. Adobe Experience Platform에서는 더 이상 해당되지 않으며 모든 ID를 기본 식별자로 간주할 수 있습니다.

일반적으로 기본 식별자는 컨텍스트에 따라 다릅니다. 콜센터에 문의하는 경우 **가장 중요한 ID는 무엇입니까?**, **전화 번호로 답장을 보낼 수 있습니다.** 하지만 CRM 팀에 문의하면 답변이 나타납니다. **이메일 주소!** Adobe Experience Platform은 이러한 복잡성을 이해하고 자동으로 관리합니다. Adobe 애플리케이션이든, Adobe 애플리케이션이 아니든 모든 애플리케이션은 기본 애플리케이션으로 간주하는 ID를 참조하여 Adobe Experience Platform과 통신합니다. 그리고 그것은 단순히 효과가 있습니다.

필드 **ID 네임스페이스**&#x200B;에 대해 **ECID**&#x200B;을(를) 선택하고 필드 **ID 값**&#x200B;에 대해 bootcamp 웹 사이트의 프로필 뷰어 패널에서 찾을 수 있는 ECID를 입력합니다. **보기**&#x200B;를 클릭합니다. 그러면 목록에 프로필이 표시됩니다. **프로필 ID**&#x200B;를 클릭하여 프로필을 엽니다.

![고객 프로필](./images/popupecid.png)

이제 고객 프로필의 두 가지 중요한 **프로필 특성**&#x200B;에 대한 개요가 표시됩니다.

![고객 프로필](./images/profile.png)

프로필에 연결된 모든 경험 이벤트에 대한 항목을 볼 수 있는 **이벤트**(으)로 이동합니다.

![고객 프로필](./images/profileee.png)

마지막으로 메뉴 옵션 **대상자 멤버십**(으)로 이동합니다. 이제 이 프로필에 적합한 모든 대상을 볼 수 있습니다.

![고객 프로필](./images/profileseg.png)

이제 익명의 또는 아는 고객을 위해 고객 경험을 개인화할 수 있는 새 대상을 만들어 보겠습니다.

다음 단계: [1.3 대상 만들기 - UI](./ex3.md)

[사용자 흐름 1로 돌아가기](./uc1.md)

[모든 모듈로 돌아가기](../../overview.md)
