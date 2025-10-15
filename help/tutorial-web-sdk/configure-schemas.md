---
title: 웹 데이터에 대한 XDM 스키마 만들기
description: 데이터 수집 인터페이스에서 웹 데이터에 대한 XDM 스키마를 만드는 방법을 알아봅니다. 이 수업은 Web SDK를 사용하여 Adobe Experience Cloud 구현 튜토리얼의 일부입니다.
feature: Web SDK,Schemas
jira: KT-15398
exl-id: 2858ce03-4f95-43ac-966c-1b647b33ef16
source-git-commit: 7ccbaaf4db43921f07c971c485e1460a1a7f0334
workflow-type: tm+mt
source-wordcount: '1541'
ht-degree: 3%

---

# 웹 데이터에 대한 XDM 스키마 만들기

Adobe Experience Platform 데이터 컬렉션 인터페이스에서 웹 데이터에 대한 XDM 스키마를 만드는 방법을 알아봅니다.

XDM(Experience Data Model) 스키마는 Adobe Experience Platform에서 데이터를 수집하기 위한 기본 구성 요소, 원칙 및 우수 사례입니다.

Platform Web SDK은 스키마를 사용하여 웹 이벤트 데이터를 표준화하고 Platform Edge Network으로 보낸 다음 궁극적으로 데이터를 데이터스트림에 구성된 모든 Experience Cloud 애플리케이션에 전달합니다. 이 단계는 고객 경험 데이터를 Experience Platform에 수집하는 데 필요한 표준 데이터 모델을 정의하고 이러한 표준을 기반으로 구축된 다운스트림 서비스 및 애플리케이션을 활성화하므로 매우 중요합니다.

>[!NOTE]
>
>Web SDK으로 Adobe Analytics, Adobe Target 또는 Adobe Audience Manager을 구현하는 데 XDM 스키마가 _필요하지 않습니다_(나중에 볼 수 있듯이 `data` 개체 대신 `xdm` 개체로 데이터를 전달할 수 있음). Journey Optimizer, Real-Time Customer Data Platform, Customer Journey Analytics과 같은 플랫폼 기반 애플리케이션의 가장 성능 좋은 구현에 XDM 스키마가 필요합니다. 자체 구현에서 XDM 스키마를 사용하지 않기로 결정할 수도 있지만 이 자습서의 일부로 사용해야 합니다.

## 데이터를 모델링하는 이유는 무엇입니까?

기업은 자신의 도메인에 대해 소통하기 위한 고유한 언어를 가지고 있습니다. 자동차 대리점은 제조사, 모형, 실린더 등을 취급한다. 항공사는 항공편 번호, 서비스 등급, 좌석 배정 업무를 처리합니다. 이 용어 중 일부는 특정 회사에 고유하며 일부는 업계 수직 간에 공유되고 일부는 거의 모든 비즈니스에서 공유됩니다. 업계 카테고리 또는 더 광범위한 카테고리 간에 공유되는 용어의 경우 이러한 용어의 이름을 지정하고 공통된 방식으로 구성할 때 데이터를 사용하여 강력한 작업을 시작할 수 있습니다.

예를 들어, 많은 사업체들이 주문을 처리합니다. 만약 이 사업체들이 집단적으로 비슷한 방식으로 주문을 모델화하기로 결정했다면? 예를 들어 데이터 모델이 주문의 총 가격을 나타내는 `priceTotal` 속성이 있는 개체로 구성된 경우 어떻게 합니까? 개체에 `currencyCode` 및 `purchaseOrderNumber` 속성이 있으면 어떻게 됩니까? 주문 개체에 결제 개체 배열인 `payments` 속성이 포함되어 있을 수 있습니다. 각 개체는 주문에 대한 결제를 나타냅니다. 예를 들어 고객이 주문의 일부를 상품권으로 결제하고 나머지는 신용카드로 결제했을 수도 있다. 다음과 같은 모델을 만들 수 있습니다.

```json
{
  "order": {
    "priceTotal": 89.50,
    "currencyCode": "EUR",
    "purchaseOrderNumber": "JWN20192388410012",
    "payments": [
      {
        "paymentType": "gift_card",
        "paymentAmount": 50
      },
      {
        "paymentType": "credit_card",
        "paymentAmount": 39.50
      }
    ]
  }
}
```

주문을 처리하는 모든 기업이 업계에서 흔히 볼 수 있는 용어에 대해 일관된 방식으로 주문 데이터를 모델링하기로 결정했다면 마법 같은 일이 벌어지기 시작할 수 있다. 데이터(prop 및 evar, 누구나?)를 지속적으로 해석하고 번역하는 대신 조직 내외부에서 정보를 보다 유연하게 교환할 수 있습니다. 머신 러닝은 데이터 _의 의미_&#x200B;를 보다 쉽게 이해하고 실행 가능한 통찰력을 제공할 수 있습니다. 관련 데이터를 표시하기 위한 사용자 인터페이스가 보다 직관적이 될 수 있습니다. 동일한 모델링을 따르는 파트너 및 공급업체와 데이터를 원활하게 통합할 수 있습니다.

Adobe [경험 데이터 모델](https://business.adobe.com/kr/products/experience-platform/experience-data-model.html)의 목표입니다. XDM은 산업에서 일반적인 데이터에 대한 규범적 모델링을 제공하는 동시에 특정 요구 사항에 맞게 모델을 확장할 수도 있습니다. Adobe Experience Platform은 XDM을 중심으로 빌드되므로 Experience Platform에 전송된 데이터는 XDM에 있어야 합니다. 데이터를 Experience Platform에 보내기 전에 현재 데이터 모델을 XDM으로 변환할 수 있는 위치와 방법을 생각하기보다 조직 전체에서 XDM을 더 널리 적용하여 번역이 거의 필요하지 않도록 하십시오.


>[!NOTE]
>
> 데모 목적으로 이 단원의 연습에서는 [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html)에서 본 콘텐츠 및 고객이 구매한 제품을 캡처하는 예제 스키마를 빌드합니다. 이러한 단계를 사용하여 고유한 목적에 맞는 다른 스키마를 생성할 수 있지만 먼저 예제 스키마를 생성할 때 스키마 편집기의 기능을 학습하는 것이 좋습니다.

XDM 스키마에 대해 자세히 알아보려면 재생 목록 [XDM으로 고객 경험 데이터 모델링](https://experienceleague.adobe.com/ko/playlists/experience-platform-model-your-customer-experience-data-with-xdm)을 보거나 [XDM 시스템 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/home)를 참조하십시오.

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* 데이터 수집 인터페이스 내에서 XDM 스키마 생성
* XDM 스키마에 필드 그룹 추가
* 모범 사례를 사용하여 웹 이벤트 데이터에 대한 XDM 스키마 만들기

## 전제 조건

데이터 수집 및 Adobe Experience Platform에 필요한 모든 프로비저닝 및 사용자 권한은 [개요](overview.md) 페이지에 설명되어 있습니다.

## XDM 스키마 만들기

XDM 스키마는 Experience Platform의 데이터를 설명하는 표준 방법이므로 스키마를 준수하는 모든 데이터를 충돌 없이 조직에서 재사용하거나 여러 조직 간에 공유할 수 있습니다. 자세한 내용은 [스키마 컴포지션의 기본 사항](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/schema/composition)을 참조하세요.

이 연습에서는 [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}에서 웹 이벤트 데이터를 캡처하는 데 권장되는 기준 필드 그룹을 사용하여 XDM 스키마를 만듭니다.

1. [데이터 수집 인터페이스](https://experience.adobe.com/data-collection/){target="_blank"} 열기
1. 올바른 샌드박스에 있는지 확인합니다. 오른쪽 상단 모서리에서 샌드박스를 찾습니다

   >[!NOTE]
   >
   >Real-Time CDP 또는 Journey Optimizer과 같은 플랫폼 기반 애플리케이션의 고객인 경우 이 자습서에서는 개발 샌드박스를 사용하는 것이 좋습니다. 그렇지 않은 경우 **[!UICONTROL Prod]** 샌드박스를 사용하십시오.

1. 왼쪽 탐색 영역에서 **[!UICONTROL 스키마]**(으)로 이동
1. 오른쪽 상단에서 **[!UICONTROL 스키마 만들기]** 단추를 선택합니다.

   ![스키마 만들기](assets/schema-xdm-create-schema.png)
1. 다음 화면에서 **[!UICONTROL 경험 이벤트]** 선택
1. **[!UICONTROL 다음]** 선택

   ![스키마 경험 이벤트](assets/schema-experience-event.png)

1. **[!UICONTROL 스키마 표시 이름]** 필드 아래에 스키마 이름을 입력하십시오(이 경우 `Luma Web Event Data`).

   >[!TIP]
   >
   >XDM 스키마에 대한 일반적인 명명 규칙은 데이터 소스 다음에 스키마 이름을 지정하는 것입니다.


1. 완료 선택

   ![스키마 경험 이벤트 찾기](assets/schema-name-schema.png)

## 필드 그룹 추가

앞에서 언급했듯이 XDM은 다운스트림 Adobe Experience Platform 서비스에서 사용할 공통 구조 및 정의를 제공하여 고객 경험 데이터를 표준화하는 핵심 프레임워크입니다. XDM 표준을 준수하여 _모든 고객 경험 데이터_&#x200B;를 일반 표현에 통합할 수 있습니다. 이 접근 방식을 사용하면 고객 작업에서 중요한 통찰력을 얻고, 세그먼트를 통해 고객 대상을 정의하고, 여러 소스의 데이터를 사용하여 개인화 목적으로 고객 속성을 표현할 수 있습니다. 자세한 내용은 [데이터 모델링 모범 사례](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/schema/best-practices)를 참조하세요.

가능하면 기존 필드 그룹을 사용하고 제품과 관계없는 모델 및 이름 지정 규칙을 준수하는 것이 좋습니다. 위의 사전 정의된 필드 그룹에 맞지 않는 조직 고유의 데이터에 대해 사용자 정의 필드 그룹을 만들 수 있습니다. 사용자 지정 스키마에 대한 자세한 단계는 [스키마 편집기를 사용하여 스키마 만들기](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/tutorials/create-schema-ui#create)를 참조하십시오.

>[!TIP]
> 
>이 연습에서는 웹 데이터 수집에 대해 권장되는 사전 정의된 필드 그룹인 _&#x200B;**[!UICONTROL AEP Web SDK ExperienceEvent]**&#x200B;_ 및 _&#x200B;**[!UICONTROL 소비자 경험 이벤트]**&#x200B;_&#x200B;을(를) 추가합니다.
>


1. **[!UICONTROL 필드 그룹]** 섹션에서 **[!UICONTROL 추가]**&#x200B;를 선택합니다.

   ![새 필드 그룹](assets/schema-new-field-group.png)

1. [!UICONTROL `AEP Web SDK ExperienceEvent`] 검색
1. 상자를 선택합니다.
1. [!UICONTROL `Consumer Experience Event`] 검색
1. 상자를 선택합니다.
1. **[!UICONTROL 필드 그룹 추가]** 선택

   ![필드 그룹 추가](assets/schema-add-field-group.png)

두 필드 그룹 모두에서 웹의 데이터 수집에 필요한 가장 일반적으로 사용되는 키-값 쌍에 액세스할 수 있습니다. 각 필드의 [!UICONTROL 표시 이름]은(는) 플랫폼 기반 응용 프로그램의 세그먼트 빌더 인터페이스에서 마케터에게 표시되며, 필요에 따라 표준 필드의 표시 이름을 변경할 수 있습니다. 원하지 않는 필드를 제거할 수도 있습니다. 필드 그룹 이름을 클릭하면 인터페이스에 속한 키-값 쌍 그룹화가 강조 표시됩니다. 아래 예제에서는 **[!UICONTROL 고객 경험 이벤트]**&#x200B;에 속하는 필드를 확인합니다.

![스키마 필드 그룹](assets/schema-consumer-experience-event.png)

이 단원은 시작에 불과합니다. 고유한 웹 이벤트 스키마를 구축할 때 비즈니스 요구 사항을 탐색하고 문서화해야 합니다. 이 프로세스는 Adobe Analytics 구현에 대한 [비즈니스 요구 사항 문서](https://experienceleague.adobe.com/ko/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-a-business-requirements-document) 및 [솔루션 디자인 참조](https://experienceleague.adobe.com/ko/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr)를 만드는 것과 비슷하지만 플랫폼, 대상 및 이벤트 전달 대상과 같은 _모든 다운스트림 데이터 수신자_&#x200B;에 대한 요구 사항을 포함해야 합니다.


### identityMap 개체

`[!UICONTROL identityMap]`(이)라는 웹 사용자를 식별하는 데 사용되는 특수 필드가 있습니다.

![Luma 웹 이벤트 데이터](assets/schema-identityMap.png)

웹에서 사용자를 식별하는 데 필요한 Experience Cloud ID가 포함되어 있으므로 모든 웹 관련 데이터 수집에 반드시 필요한 개체입니다. 또한 인증된 사용자의 내부 고객 ID를 설정하는 키입니다. `[!UICONTROL identityMap]`에 대해서는 [ID 구성](configure-identities.md) 단원에서 자세히 설명합니다. **[!UICONTROL XDM ExperienceEvent]** 클래스를 사용하는 모든 스키마에 자동으로 포함됩니다.


>[!IMPORTANT]
>
> 스키마를 저장하기 전에 스키마에 대해 **[!UICONTROL 프로필]**&#x200B;을(를) 활성화할 수 있습니다. **지금 사용하도록 설정하지 마십시오**. 프로필에 대해 스키마를 활성화하면 전체 샌드박스를 재설정하지 않고 비활성화하거나 삭제할 수 없습니다. UI에서 필드를 [사용하지 않음](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/tutorials/field-deprecation-ui#deprecate)할 수 있지만 스키마에서 필드를 제거할 수도 없습니다. 이러한 의미는 프로덕션 환경에서 자체 데이터를 사용하여 작업할 때 나중에 기억해야 합니다.
>
>
>이 설정은 [Experience Platform 설정](setup-experience-platform.md) 단원에서 자세히 설명합니다.
>&#x200B;>![프로필 스키마](assets/schema-profile.png)

이 단원을 완료하려면 오른쪽 상단의 **[!UICONTROL 저장]**&#x200B;을 선택하세요.

![스키마 저장](assets/schema-select-save.png)


이제 태그 속성에 웹 SDK 확장을 추가할 때 이 스키마를 참조할 수 있습니다.

>[!NOTE]
>
>Adobe Experience Platform 웹 SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하고 싶거나 향후 콘텐츠에 대한 제안이 있는 경우 이 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=ko)에서 공유하십시오.
