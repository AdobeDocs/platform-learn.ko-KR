---
title: 웹 데이터에 대한 XDM 스키마 만들기
description: 데이터 수집 인터페이스에서 웹 데이터에 대한 XDM 스키마를 만드는 방법을 알아봅니다. 이 단원은 Web SDK를 사용하여 Adobe Experience Cloud 구현 자습서의 일부입니다.
feature: Web SDK,Schemas
source-git-commit: f08866de1bd6ede50bda1e5f8db6dbd2951aa872
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 1%

---

# 웹 데이터에 대한 XDM 스키마 만들기

데이터 수집 인터페이스에서 웹 데이터에 대한 XDM 스키마를 만드는 방법을 알아봅니다.

XDM(Experience Data Model) 스키마는 Adobe Experience Platform에서 데이터를 수집하기 위한 기본 구성 요소, 원칙 및 우수 사례입니다.

Platform Web SDK는 스키마를 사용하여 웹 이벤트 데이터를 표준화하고 Platform Edge Network로 보낸 다음 최종적으로 데이터를 데이터스트림에 구성된 Experience Cloud 애플리케이션으로 전달합니다. 이 단계는 고객 경험 데이터를 Experience Platform에 수집하는 데 필요한 표준 데이터 모델을 정의하고 이러한 표준을 기반으로 구축된 다운스트림 서비스 및 애플리케이션을 활성화하므로 매우 중요합니다.

## 데이터를 모델링하는 이유는 무엇입니까?

기업은 자신의 도메인에 대해 소통하기 위한 고유한 언어를 가지고 있습니다. 자동차 대리점은 제조사, 모형, 실린더 등을 취급한다. 항공사는 항공편 번호, 서비스 등급, 좌석 배정 업무를 처리합니다. 이 용어 중 일부는 특정 회사에 고유하며 일부는 업계 수직 간에 공유되고 일부는 거의 모든 비즈니스에서 공유됩니다. 업계 카테고리 또는 더 광범위한 카테고리 간에 공유되는 용어의 경우 이러한 용어의 이름을 지정하고 공통된 방식으로 구성할 때 데이터를 사용하여 강력한 작업을 시작할 수 있습니다.

예를 들어, 많은 사업체들이 주문을 처리합니다. 만약 이 사업체들이 집단적으로 비슷한 방식으로 주문을 모델화하기로 결정했다면? 예를 들어 데이터 모델이 `priceTotal` 주문의 총 가격을 나타내는 속성? 개체에 라는 속성도 있으면 어떻게 합니까? `currencyCode` 및 `purchaseOrderNumber`? 주문 개체에 이름이 인 속성이 포함되어 있을 수 있습니다. `payments` 그러면 결제 객체의 배열이 됩니다. 각 개체는 주문에 대한 결제를 나타냅니다. 예를 들어 고객이 주문의 일부를 상품권으로 결제하고 나머지는 신용카드로 결제했을 수도 있다. 다음과 같은 모델을 만들 수 있습니다.

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

주문을 처리하는 모든 기업이 업계에서 흔히 볼 수 있는 용어에 대해 일관된 방식으로 주문 데이터를 모델링하기로 결정했다면 마법 같은 일이 벌어지기 시작할 수 있다. 데이터(prop 및 evar, 누구나?)를 지속적으로 해석하고 번역하는 대신 조직 내외부에서 정보를 보다 유연하게 교환할 수 있습니다. 머신 러닝을 통해 귀하의 데이터를 보다 쉽게 이해할 수 있습니다 _수단_ 실행 가능한 통찰력을 제공합니다. 관련 데이터를 표시하기 위한 사용자 인터페이스가 보다 직관적이 될 수 있습니다. 동일한 모델링을 따르는 파트너 및 공급업체와 데이터를 원활하게 통합할 수 있습니다.

이것이 Adobe의 목표입니다. [경험 데이터 모델](https://business.adobe.com/products/experience-platform/experience-data-model.html). XDM은 산업에서 일반적인 데이터에 대한 규범적 모델링을 제공하는 동시에 특정 요구 사항에 맞게 모델을 확장할 수도 있습니다. Adobe Experience Platform은 XDM을 중심으로 빌드되므로 Experience Platform에 전송된 데이터는 XDM에 있어야 합니다. 데이터를 Experience Platform으로 보내기 전에 현재 데이터 모델을 XDM으로 변환할 수 있는 위치와 방법을 생각하기보다 조직 전체에 XDM을 보다 널리 적용하여 번역이 거의 필요하지 않도록 하십시오.


>[!NOTE]
>
> 이 단원의 연습에서는 데모용으로 의 고객이 본 컨텐츠와 구매한 제품을 캡처하는 예제 스키마를 빌드합니다. [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html). 이러한 단계를 사용하여 고유한 목적에 맞는 다른 스키마를 생성할 수 있지만 먼저 예제 스키마를 생성할 때 스키마 편집기의 기능을 학습하는 것이 좋습니다.

XDM 스키마에 대한 자세한 내용은 과정을 참조하십시오. [XDM으로 고객 경험 데이터 모델링](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) 또는 [XDM 시스템 개요](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=ko).

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* 데이터 수집 인터페이스 내에서 XDM 스키마 생성
* XDM 스키마에 필드 그룹 추가
* 모범 사례를 사용하여 웹 이벤트 데이터에 대한 XDM 스키마 만들기

## 전제 조건

데이터 수집 및 Adobe Experience Platform에 필요한 모든 프로비저닝 및 사용자 권한은에 설명되어 있습니다. [개요](overview.md) 페이지를 가리키도록 업데이트하는 중입니다.

## XDM 스키마 만들기

XDM 스키마는 Experience Platform의 데이터를 설명하는 표준 방법이므로 스키마를 준수하는 모든 데이터를 충돌 없이 조직에서 재사용하거나 여러 조직 간에 공유할 수 있습니다. 자세한 내용은 [스키마 컴포지션 기본 사항](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=ko-KR).

이 연습에서는 웹 이벤트 데이터를 캡처하기 위해 권장되는 기준 필드 그룹을 사용하여 XDM 스키마를 만듭니다. [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}:

1. 를 엽니다. [데이터 수집 인터페이스](https://launch.adobe.com/){target="_blank"}
1. 올바른 샌드박스에 있는지 확인합니다. 오른쪽 상단 모서리에서 샌드박스를 찾습니다

   >[!NOTE]
   >
   >Real-Time CDP 또는 Journey Optimizer과 같은 플랫폼 기반 애플리케이션의 고객인 경우 이 자습서에서는 개발 샌드박스를 사용하는 것이 좋습니다. 그렇지 않으면 **[!UICONTROL Prod]** 샌드박스.

1. 다음으로 이동 **[!UICONTROL 스키마]** 왼쪽 탐색
1. 다음 항목 선택 **[!UICONTROL 스키마 만들기]** 오른쪽 상단의 단추

   ![스키마 만들기](assets/schema-xdm-create-schema.png)
1. 선택 **[!UICONTROL 경험 이벤트]** 다음 화면에서
1. 선택 **[!UICONTROL 다음]**

   ![스키마 경험 이벤트](assets/schema-experience-event.png)

1. 아래에 스키마 이름 입력 **[!UICONTROL 스키마 표시 이름]** 필드, 이 경우 `Luma Web Event Data`

   >[!TIP]
   >
   >XDM 스키마에 대한 일반적인 명명 규칙은 데이터 소스 다음에 스키마 이름을 지정하는 것입니다.


1. 완료 선택

   ![스키마 경험 이벤트 찾기](assets/schema-name-schema.png)

## 필드 그룹 추가

앞에서 언급했듯이 XDM은 다운스트림 Adobe Experience Platform 서비스에서 사용할 공통 구조 및 정의를 제공하여 고객 경험 데이터를 표준화하는 핵심 프레임워크입니다. XDM 표준을 준수함으로써, _모든 고객 경험 데이터_ 는 일반적인 표현으로 통합될 수 있습니다. 이 접근 방식을 사용하면 고객 작업에서 중요한 통찰력을 얻고, 세그먼트를 통해 고객 대상을 정의하고, 여러 소스의 데이터를 사용하여 개인화 목적으로 고객 속성을 표현할 수 있습니다. 다음을 참조하십시오 [데이터 모델링 모범 사례](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/best-practices.html?lang=en) 추가 정보.

가능하면 기존 필드 그룹을 사용하고 제품과 관계없는 모델 및 이름 지정 규칙을 준수하는 것이 좋습니다. 위의 사전 정의된 필드 그룹에 맞지 않는 조직 고유의 데이터에 대해 사용자 정의 필드 그룹을 만들 수 있습니다. 다음을 참조하십시오 [스키마 편집기를 사용하여 스키마 만들기](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en#create) 사용자 지정 스키마에 대한 자세한 단계.

>[!TIP]
> 
>이 연습에서는 웹 데이터 수집에 권장되는 사전 정의된 필드 그룹을 추가합니다. _**[!UICONTROL AEP 웹 SDK ExperienceEvent]**_ 및 _**[!UICONTROL 고객 경험 이벤트]**_.
>
>
> 를 구현하는 경우에만 **Adobe Analytics** (Web SDK를 사용하고 데이터를에 전송하지 않음) **Experience Platform**, 사용 [!UICONTROL Adobe Analytics ExperienceEvent 템플릿] XDM 스키마를 정의하는 필드 그룹입니다. 다음에서 사용됩니다. [Analytics 설정](setup-analytics.md) 레슨.

1. 다음에서 **[!UICONTROL 필드 그룹]** 섹션, 선택 **[!UICONTROL 추가]**

   ![새 필드 그룹](assets/schema-new-field-group.png)

1. 검색 대상 [!UICONTROL `AEP Web SDK ExperienceEvent`]
1. 상자를 선택합니다.
1. 검색 대상 [!UICONTROL `Consumer Experience Event`]
1. 상자를 선택합니다.
1. 선택 **[!UICONTROL 필드 그룹 추가]**

   ![필드 그룹 추가](assets/schema-add-field-group.jpg)

두 필드 그룹 모두에서 웹의 데이터 수집에 필요한 가장 일반적으로 사용되는 키-값 쌍에 액세스할 수 있습니다. 다음 [!UICONTROL 표시 이름] 각 필드의 은 플랫폼 기반 애플리케이션의 세그먼트 빌더 인터페이스에서 마케터에게 표시되며, 필요에 따라 표준 필드의 표시 이름을 변경할 수 있습니다. 원하지 않는 필드를 제거할 수도 있습니다. 필드 그룹 이름을 클릭하면 인터페이스에 속한 키-값 쌍 그룹화가 강조 표시됩니다. 아래 예제에서 어떤 그룹이 속해 있는지 알 수 있습니다 **[!UICONTROL 고객 경험 이벤트]**.

![스키마 필드 그룹](assets/schema-consumer-experience-event.png)

이 단원은 시작에 불과합니다. 고유한 웹 이벤트 스키마를 구축할 때 비즈니스 요구 사항을 탐색하고 문서화해야 합니다. 이 프로세스는 을(를) 만드는 것과 유사합니다 [비즈니스 요구 사항 문서](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-a-business-requirements-document.html) 및 [솔루션 디자인 참조](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr.html) Adobe Analytics 구현의 경우, 단, 다음과 같은 요구 사항이 포함되어야 합니다. _모든 다운스트림 데이터 수신자_ Platform, Target 및 이벤트 전달 대상 등.


### identityMap 개체

라는 웹 사용자를 식별하는 데 사용되는 특수 필드가 있습니다. `[!UICONTROL identityMap]`.

![Luma 웹 이벤트 데이터](assets/schema-identityMap.png)

웹에서 사용자를 식별하는 데 필요한 Experience Cloud ID가 저장되어 있으므로 모든 웹 관련 데이터 수집에 반드시 필요한 개체입니다. 또한 인증된 사용자의 내부 고객 ID를 설정하는 키입니다. `[!UICONTROL identityMap]` 다음에서 자세히 설명합니다. [ID 구성](configure-identities.md) 레슨. 를 사용하여 모든 스키마에 자동으로 포함됩니다. **[!UICONTROL XDM ExperienceEvent]** 클래스.


>[!IMPORTANT]
>
> 다음을 활성화할 수 있습니다. **[!UICONTROL 프로필]** 스키마를 저장하기 전에 스키마. **금지** 이 시점에서 활성화하십시오. 프로필에 대해 스키마를 활성화하면 비활성화하거나 삭제할 수 없습니다. 이 시점에서도 필드를 스키마에서 제거할 수 없지만 [UI의 필드 사용 중단](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/field-deprecation-ui.html?lang=en#deprecate). 이러한 의미는 프로덕션 환경에서 자체 데이터를 사용하여 작업할 때 나중에 기억해야 합니다.
>
>
>이 설정에 대해서는 다음 중 자세히 설명합니다. [설정 Experience Platform](setup-experience-platform.md) 레슨.
>![프로필 스키마](assets/schema-profile.png)

이 단원을 완료하려면 **[!UICONTROL 저장]** 오른쪽 위에 있습니다.

![스키마 저장](assets/schema-select-save.png)


이제 태그 속성에 Web SDK 확장을 추가할 때 이 스키마를 참조할 수 있습니다.


[다음: ](configure-identities.md)

>[!NOTE]
>
>Adobe Experience Platform Web SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나, 일반적인 피드백을 공유하거나, 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오. [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
