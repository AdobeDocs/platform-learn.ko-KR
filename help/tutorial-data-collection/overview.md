---
title: 개요
description: 개요
exl-id: 527d8f73-33d0-45a6-b7a4-5e46cdb7c138
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 2%

---

# Adobe Experience Platform 데이터 수집 사용

사용자 브라우저에서 발생하는 이벤트에 대한 데이터를 수집하는 것은 마케팅 전략의 기본 용어입니다. Adobe은 이 데이터를 관리하는 데 도움이 되는 몇 가지 도구를 제공했습니다. 이러한 각 도구에 대해 개별적으로 숙지할 수 있지만, 이 자습서에서는 이러한 각 도구가 수행하는 작업과 공동 목표를 달성하기 위해 함께 작업하는 방법에 대한 광범위한 보기를 제공합니다.

이 자습서에서는 다음 전략을 설명합니다.

1. Adobe Experience Platform 내에서 데이터 구조화 및 유지
1. 브라우저에서 데이터를 관리하고 특정 이벤트가 발생했음을 알려주십시오
1. 관련 데이터를 Adobe Experience Platform에 보내 이러한 이벤트에 반응합니다.

이 자습서에서는 Adobe 클라이언트 데이터 레이어, Adobe Experience Platform Web SDK 및 [!DNL Tags] 보다 처방적이고 원활한 구현을 위해 이러한 도구를 타사 또는 사내 도구와 혼용하여 사용할 수도 있으므로 완벽한 유연성을 얻을 수 있습니다.

## 예시 상황

이 자습서 중에 전자 상거래 사이트에서 간단한 제품 페이지에 대한 데이터 수집을 구현합니다.

1. 제품 페이지가 브라우저에 로드됩니다. 여기에서 사용자가 제품을 보았음을 추적합니다.
1. 사용자가 제품을 구매하기로 결정하므로 버튼을 클릭하여 장바구니에 제품을 추가합니다. 여기에서 사용자가 새 장바구니를 열고 Adobe Experience Platform에 경험 이벤트를 보내어 제품을 장바구니에 추가했는지 추적합니다.
1. 마지막으로 사용자가 _앱 다운로드_ 모바일 앱에 관심이 있으므로 연결합니다. 사용자가 링크를 클릭했음을 추적합니다.

그럼 시작해 보겠습니다!

[다음: ](structuring-your-data.md)

>[!NOTE]
>
>데이터 수집에 시간을 내어 주셔서 감사합니다. 질문이 있거나 일반 피드백을 공유하거나 향후 컨텐츠에 대한 제안 사항이 있는 경우 해당 정보를 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
