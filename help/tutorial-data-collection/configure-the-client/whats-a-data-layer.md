---
title: 데이터 계층이란 무엇입니까?
description: 데이터 계층이란 무엇입니까?
exl-id: a53572c1-1295-4ed4-8a3d-aafff3235138
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# 데이터 계층이란 무엇입니까?

사이트에서 마케팅 기술을 구현할 때에는 UI 전체에 중요한 데이터 조각이 흩어져 있을 수 있습니다. 예를 들어 제품 이름이 페이지의 제목에 있을 수 있으며 제품 이미지 아래의 페이지에서 가격이 더 낮을 수 있습니다. 해당 데이터를 Adobe 또는 다른 공급업체로 보내려면 필요한 데이터가 포함된 HTML 요소를 찾아 해당 요소에서 데이터를 가져온 다음 가져옵니다. 그러나 엔지니어링 팀이 헤더에서 사이드바로 제품 이름을 이동하기로 결정하면 어떻게 됩니까? 구현이 중단됩니다. 구현에서 더 이상 제목을 찾을 수 없거나, 더 나아가 제목을 찾아 관련 없는 데이터를 서버에 보냅니다.

데이터 계층의 주요 목표 중 하나는 이 문제를 해결하는 것입니다. 가장 간단한 데이터 계층은 JavaScript 개체 또는 페이지의 제품에 대한 데이터를 포함하는 배열입니다. 여기에는 마케팅 기술이 목표 달성에 필요한 모든 관련 데이터가 포함됩니다. 사용자 인터페이스 요소에 의존하여 이 데이터를 제공하지 않으면 구현이 더 강력하게 구현됩니다. 데이터 계층은 데이터를 보유하며 계약으로 간주해야 합니다. 일반적으로 이 계약은 데이터를 데이터 계층에 배치하는 엔지니어링 팀과 데이터 계층에서 데이터를 검색하는 마케팅 팀 사이에 있습니다.

엔지니어가 데이터 계층의 구조를 변경하려는 경우 마케팅 구현에 적합한 변경을 수행할 수 있도록 마케팅 팀과 작업하는 것을 훨씬 더 고려합니다. 이런 소통과 협력 _반드시_ 강력한 구현을 위해 조직에 구축됩니다.

## 컨테이너와 컨텐츠 비교

업계에서, &quot;데이터 계층&quot;이라는 용어가 약간 느슨하게 주위에 던져지며 종종 혼동 및 잘못된 커뮤니케이션으로 이어질 수 있습니다. 구슬을 한 상자 고려해 보십시오. 다음 두 가지 부분이 있습니다. 컨테이너(상자)와 내용(구명)입니다. 마찬가지로 데이터 레이어에는 두 가지 부분이 있는 것으로 간주됩니다. 컨테이너(JavaScript 개체 또는 배열)와 콘텐츠(다음과 같은 데이터 조각) `priceTotal`, `currencyCode`, 및 `purchaseOrderNumber` ).

이 자습서는 Adobe 클라이언트 데이터 레이어를 참조하므로 컨텐츠가 아니라 컨테이너를 참조합니다. XDM을 참조하면 컨테이너가 아니라 컨텐츠를 참조합니다. Adobe 클라이언트 데이터 레이어를 사용할 때 컨텐츠가 XDM인지 아니면 고유한 데이터 모델인지는 중요하지 않습니다. Adobe 클라이언트 데이터 계층은 중요하지 않습니다. 그냥 상자에요. 하지만, _is_ 특별한 힘이 있는 상자..

## 변경 내용 통신

데이터 레이어를 사용할 때 언제든지 컨텐츠를 변경할 수 있습니다. 여러 시간에 데이터를 사용할 수 있기 때문에 좋은 기능입니다. 예를 들어, 사용자에 대한 일부 데이터를 즉시 사용할 수 있지만, 추가 정보를 위해 타사에 비동기 요청을 해야 할 수 있습니다. 이것은 특별한 배려가 필요하다. 어떤 시점에서 이러한 비동기 데이터를 Adobe Experience Platform에 보내야 하는 경우 마케팅 기술은 특정 데이터가 데이터 계층에 추가되어 전송할 준비가 되었음을 어떻게 알 수 있습니까? 보다 스마트한 데이터 계층인 이벤트 기반의 데이터 레이어가 필요합니다.

이벤트 기반 데이터 계층은 마케팅 기술이 변화에 대응할 수 있도록 컨텐츠가 변경되었다는 것을 전달할 수 있습니다. 제대로 사용하면 변경 사항이 발생할 때 통신할 방법이 없는 데이터 레이어에서 종종 발생하는 시간 문제를 방지할 수 있습니다.

Adobe 클라이언트 데이터 계층은 이벤트 기반 데이터 레이어입니다.

[다음: ](how-to-use-the-adobe-client-data-layer.md)

>[!NOTE]
>
>데이터 수집에 시간을 내어 주셔서 감사합니다. 질문이 있거나 일반 피드백을 공유하거나 향후 컨텐츠에 대한 제안 사항이 있는 경우 해당 정보를 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
