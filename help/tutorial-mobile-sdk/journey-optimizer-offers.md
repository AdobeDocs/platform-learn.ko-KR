---
title: Platform Mobile SDK를 사용하여 오퍼 만들기 및 표시
description: Platform Mobile SDK 및 Adobe Journey Optimizer 의사 결정 관리를 사용하여 오퍼를 만들고 표시하는 방법을 알아봅니다.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Offers
jira: KT-14640
exl-id: c08a53cb-683e-4487-afab-fd8828c3d830
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '2470'
ht-degree: 1%

---

# 의사 결정 관리를 사용하여 오퍼 만들기 및 표시

Experience Platform Mobile SDK를 사용하여 모바일 앱에서 Journey Optimizer 의사 결정 관리의 오퍼를 표시하는 방법을 알아봅니다.

Journey Optimizer 의사 결정 관리를 사용하면 적절한 시기에 모든 접점에서 고객에게 최상의 오퍼와 경험을 제공할 수 있습니다. 디자인한 후에는 개인화된 오퍼로 대상을 타기팅하십시오.

![아키텍쳐](assets/architecture-ajo.png)

의사 결정 관리를 사용하면 마케팅 오퍼의 중앙 라이브러리와 Adobe Experience Platform에서 만든 풍부한 실시간 프로필에 규칙과 제한을 적용하는 의사 결정 엔진을 통해 손쉽게 개인화할 수 있습니다. 따라서 고객에게 적절한 시기에 적절한 오퍼를 보낼 수 있습니다. 자세한 내용은 [의사 결정 관리 정보](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/get-started-decision/starting-offer-decisioning.html?lang=en)를 참조하세요.




>[!NOTE]
>
>이 단원은 선택 사항이며 의사 결정 관리 기능을 사용하여 모바일 앱에 오퍼를 표시하려는 Journey Optimizer 사용자에게만 적용됩니다.


## 전제 조건

* SDK가 설치 및 구성된 앱을 빌드하고 실행했습니다.
* Adobe Experience Platform용 앱을 설정합니다.
* [여기](https://experienceleague.adobe.com/docs/journey-optimizer/using/access-control/privacy/high-low-permissions.html?lang=en#decisions-permissions)에 설명된 대로 오퍼 및 결정을 관리할 수 있는 적절한 권한이 있는 Journey Optimizer - 의사 결정 관리에 액세스하십시오.


## 학습 목표

이 단원에서는 다음과 같은 작업을 수행합니다

* 의사 결정 관리에 사용할 Edge 구성을 업데이트합니다.
* Journey Optimizer - Decisioning 확장을 사용하여 태그 속성을 업데이트합니다.
* 스키마를 업데이트하여 제안 이벤트를 캡처합니다.
* Assurance에서 설정의 유효성을 검사합니다.
* Journey Optimizer - 의사 결정 관리의 오퍼를 기반으로 오퍼 의사 결정을 만듭니다.
* 앱을 업데이트하여 Optimizer 확장을 등록합니다.
* 앱에서 의사 결정 관리의 오퍼를 구현합니다.


## 설정

>[!TIP]
>
>[Target을 사용하여 A/B 테스트 설정](target.md) 단원의 일부로 환경을 이미 설정한 경우 이 설정 섹션의 일부 단계를 이미 수행했을 수 있습니다.

### 데이터 스트림 구성 업데이트

모바일 앱에서 플랫폼 Edge Network으로 전송된 데이터가 의사 결정 관리인 Journey Optimizer으로 전달되도록 하려면 데이터스트림을 업데이트합니다.

1. 데이터 수집 UI에서 **[!UICONTROL 데이터스트림]**&#x200B;을(를) 선택하고 데이터스트림(예: **[!DNL Luma Mobile App]**)을 선택합니다.
1. **[!UICONTROL Experience Platform]**&#x200B;에 대해 ![자세히](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg)를 선택하고 상황에 맞는 메뉴에서 ![편집](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL 편집]**&#x200B;을 선택합니다.
1. **[!UICONTROL 데이터스트림]** > ![폴더](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) > **[!UICONTROL Adobe Experience Platform]** 화면에서 **[!UICONTROL Offer decisioning]**, **[!UICONTROL Edge 세그멘테이션]** 및 **[!UICONTROL Adobe Journey Optimizer]**&#x200B;이 선택되었는지 확인하십시오. Target 단원을 수행하려면 **[!UICONTROL Personalization 대상]**&#x200B;도 선택하십시오. 자세한 내용은 [Adobe Experience Platform 설정](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#aep)을 참조하세요.
1. 데이터스트림 구성을 저장하려면 **[!UICONTROL 저장]** 을 선택합니다.

   ![AEP 데이터스트림 구성](assets/datastream-aep-configuration-offers.png)




### Journey Optimizer - Decisioning 태그 확장 설치

1. **[!UICONTROL 태그]**(으)로 이동하여 모바일 태그 속성을 찾은 다음 속성을 엽니다.
1. **[!UICONTROL 확장]**&#x200B;을 선택하십시오.
1. **[!UICONTROL 카탈로그]**&#x200B;를 선택하십시오.
1. **[!UICONTROL Adobe Journey Optimizer - Decisioning]** 확장을 검색합니다.
1. 확장을 설치합니다. 확장은 추가 구성이 필요하지 않습니다.

   ![의사 결정 확장 추가](assets/tag-add-decisioning-extension.png)


### 스키마 업데이트

1. 데이터 수집 인터페이스로 이동하여 왼쪽 레일에서 **[!UICONTROL 스키마]**&#x200B;를 선택합니다.
1. 상단 표시줄에서 **[!UICONTROL 찾아보기]**&#x200B;를 선택합니다.
1. 스키마를 선택하여 엽니다.
1. 스키마 편집기에서 필드 그룹 옆에 있는 ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 추가]**&#x200B;를 선택합니다.
1. **[!UICONTROL 필드 그룹 추가]** 대화 상자에서 ![검색](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg)을 통해 `proposition`을(를) 검색하고 **[!UICONTROL 경험 이벤트 - 제안 상호 작용]**&#x200B;을 선택하고 **[!UICONTROL 필드 그룹 추가]**를 선택합니다. 이 필드 그룹은 오퍼와 관련된 경험 이벤트 데이터(제공 사항, 수집, 결정 및 기타 매개 변수의 일부)를 수집합니다(이 단원의 뒷부분 참조). 하지만 또한 그 제안은 어떻게 되어가고 있나요? 표시됩니까, 상호 작용합니까, 해제됩니까, 등입니다.
   ![제안](assets/schema-fieldgroup-proposition.png)
1. **[!UICONTROL 저장]**&#x200B;을 선택하여 스키마에 변경 내용을 저장합니다.


## Assurance에서 설정 확인

Assurance에서 설정을 확인하려면:

1. Assurance UI로 이동합니다.
1. 왼쪽 레일에서 **[!UICONTROL 구성]**&#x200B;을 선택하고 **[!UICONTROL ADOBE JOURNEY OPTIMIZER DECISIONING]** 아래의 **[!UICONTROL 설정 유효성 검사]** 옆에 있는 ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg)을 선택합니다.
1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.
1. 왼쪽 레일에서 **[!UICONTROL 설정 유효성 검사]**를 선택합니다. 애플리케이션의 데이터 스트림 설정과 SDK 설정이 모두 검증됩니다.
   ![AJO 의사 결정 유효성 검사](assets/ajo-decisioning-validation.png)


## 배치 생성

오퍼를 실제로 만들려면 먼저 모바일 앱에서 이러한 오퍼를 배치할 방법과 위치를 정의해야 합니다. 의사 결정 관리에서 이 목적을 위한 배치를 정의하고 JSON 페이로드를 지원하는 모바일 채널에 대한 배치를 정의합니다.

1. Journey Optimizer UI의 왼쪽 레일에서 **[!UICONTROL 의사 결정 관리]**&#x200B;에서 ![구성 요소](https://spectrum.adobe.com/static/icons/workflow_18/Smock_OfferActivities_18_N.svg) **[!UICONTROL 구성 요소]**&#x200B;를 선택합니다.

1. 상단 표시줄에서 **[!UICONTROL 배치]**&#x200B;를 선택합니다.

1. 이름이 **[!UICONTROL 모바일 JSON]**, **[!UICONTROL 모바일]**&#x200B;이(가) **[!UICONTROL 채널 유형]**, **[!UICONTROL JSON]**&#x200B;이(가) **[!UICONTROL 콘텐츠 유형]**&#x200B;인 배치가 나열되지 않으면 배치를 만들어야 합니다. 그렇지 않으면 [오퍼 만들기](#create-offers)를 계속하십시오.

모바일 JSON 배치를 만들려면 다음 작업을 수행하십시오.

1. ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) 배치 만들기를 선택하십시오.

   1. **[!UICONTROL 세부 정보]** 섹션에서 `Mobile JSON`을(를) **[!UICONTROL 이름]**(으)로 입력하고 **[!UICONTROL 채널 유형]**&#x200B;에서 **[!UICONTROL 모바일]**&#x200B;을(를) 선택하고 **[!UICONTROL 콘텐츠 유형]**&#x200B;에서 **[!UICONTROL JSON]**&#x200B;을(를) 선택합니다.
   1. 배치를 저장하려면 **[!UICONTROL 저장]**&#x200B;을 선택하십시오.

   ![배치 만들기](assets/ajo-create-placement.png)



## 오퍼 만들기

1. Journey Optimizer UI의 왼쪽 레일에서 **[!UICONTROL 의사 결정 관리]**&#x200B;에서 ![오퍼](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Offers_18_N.svg) **[!UICONTROL 오퍼]**&#x200B;를 선택합니다.
1. **[!UICONTROL 오퍼]** 화면에서 **[!UICONTROL 찾아보기]**&#x200B;를 선택하여 오퍼 목록을 확인합니다.
1. **[!UICONTROL 오퍼 만들기]**&#x200B;를 선택합니다.
1. **[!UICONTROL 새 오퍼]** 대화 상자에서 **[!UICONTROL 개인 맞춤화된 오퍼]**&#x200B;을 선택하고 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. **[!UICONTROL 새 맞춤형 오퍼 만들기]**&#x200B;의 **[!UICONTROL 세부 정보]** 단계에서:
   1. 오퍼의 **[!UICONTROL 이름]**(예: `Luma - Juno Jacket`)을 입력하고 **[!UICONTROL 시작 날짜 및 시간]** 및 **[!UICONTROL 종료 날짜 및 시간]**&#x200B;을 입력하십시오. 이 날짜 이외에는 Decisioning 엔진에서 오퍼를 선택하지 않습니다.
   1. **[!UICONTROL 다음]**을 선택합니다.
      ![오퍼 - 세부 정보](assets/ajo-offers-details.png)

1. **[!UICONTROL 새 맞춤형 오퍼 만들기]**&#x200B;의 **[!UICONTROL 표시 추가]** 단계에서:
   1. **[!UICONTROL 채널]** 목록에서 ![모바일](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DevicePhone_18_N.svg) **[!UICONTROL 모바일]**&#x200B;을 선택하고 **[!UICONTROL 배치]** 목록에서 **[!UICONTROL 모바일 JSON]**&#x200B;을 선택합니다.
   1. **[!UICONTROL 콘텐츠]**&#x200B;에 대해 **[!UICONTROL 사용자 지정]**&#x200B;을(를) 선택하십시오.
   1. **[!UICONTROL 콘텐츠 추가]**&#x200B;를 선택합니다. **[!UICONTROL 개인화 추가]** 대화 상자에서:
      1. [!UICONTROL 모드] 선택기를 사용할 수 있는 경우 **[!UICONTROL JSON]**(으)로 설정되어 있는지 확인하십시오.
      1. 다음 JSON을 입력합니다.

         ```json
         { 
             "title": "Juno Jacket",
             "text": "On colder-than-comfortable mornings, you'll love warming up in the Juno All-Ways Performance Jacket, designed to compete with wind and chill. Built-in Cocona&trade; technology aids evaporation, while a special zip placket and stand-up collar keep your neck protected.", 
             "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/women/tops/jackets/wj06-purple_main.jpg" 
         }  
         ```

      1. **[!UICONTROL 저장]**을 선택합니다.
         ![오퍼 - 사용자 지정 콘텐츠](assets/ajo-offers-customcontent.png)
   1. **[!UICONTROL 다음]**을 선택합니다.
      ![오퍼 표시](assets/ajo-offers-representations.png)

1. **[!UICONTROL 개인 맞춤화된 새 오퍼 만들기]**&#x200B;의 **[!UICONTROL 제약 조건 추가]** 단계에서:
   1. **[!UICONTROL 우선 순위]**&#x200B;을(를) `10`(으)로 설정합니다.
   1. **[!UICONTROL 한도 포함]**&#x200B;을 해제합니다.
   1. **[!UICONTROL 다음]**을 선택합니다.
      ![오퍼 - 제한](assets/ajo-offers-constraints.png)

1. **[!UICONTROL 새 개인 맞춤화된 오퍼 만들기]**&#x200B;의 **[!UICONTROL 검토]** 단계에서:
   1. 오퍼를 검토한 다음 **[!UICONTROL 마침]**&#x200B;을 선택합니다.
   1. **[!UICONTROL 오퍼 저장]** 대화 상자에서 **[!UICONTROL 저장 및 승인]**&#x200B;을 선택합니다.

1. 3~8단계를 반복하여 이름과 컨텐츠가 다른 오퍼를 4개 더 만듭니다. 다른 모든 구성 값(예: 시작 날짜 및 시간 또는 우선 순위)은 사용자가 만든 첫 번째 오퍼와 유사합니다. 중복 오퍼를 빠르게 만들고 편집할 수 있습니다.

   1. Journey Optimizer UI의 왼쪽 레일에서 ![오퍼](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Offers_18_N.svg) **[!UICONTROL 오퍼]**&#x200B;를 선택한 다음 상단 막대에서 오퍼를 선택합니다.
   1. 생성한 오퍼의 행을 선택합니다.
   1. 오른쪽 창에서 ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmall_18_N.svg) **[!UICONTROL 추가 작업]**&#x200B;을 선택하고 컨텍스트 메뉴에서 ![복제](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Duplicate_18_N.svg) **[!UICONTROL 복제]**&#x200B;을 선택합니다.

      아래 표를 사용하여 네 개의 다른 오퍼를 정의합니다.

      | 오퍼 이름 | JSON의 오퍼 콘텐츠 |
      |---|---|
      | Luma - 물병 확인 | `{ "title": "Affirm Water Bottle", "text": "You'll stay hydrated with ease with the Affirm Water Bottle by your side or in hand. Measurements on the outside help you keep track of how much you're drinking, while the screw-top lid prevents spills. A metal carabiner clip allows you to attach it to the outside of a backpack or bag for easy access.", "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/gear/fitness-equipment/ug06-lb-0.jpg" }` |
      | Luma - Desiree 피트니스 티 | `{ "title": "Desiree Fitness Tee", "text": "When you're too far to turn back, thank yourself for choosing the Desiree Fitness Tee. Its ultra-lightweight, ultra-breathable fabric wicks sweat away from your body and helps keeps you cool for the distance.", "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/women/tops/tees/ws05-yellow_main.jpg" }` |
      | Luma - Adrienne Trek Jacket | `{ "title": "Adrienne Trek Jacket", "text": "You're ready for a cross-country jog or a coffee on the patio in the Adrienne Trek Jacket. Its style is unique with stand collar and drawstrings, and it fits like a jacket should.", "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/women/tops/jackets/wj08-gray_main.jpg" }` |
      | Luma - Aero 일일 피트니스 티 | `{ "title": "Aero Daily Fitness Tee", "text": "Need an everyday action tee that helps keep you dry? The Aero Daily Fitness Tee is made of 100% polyester wicking knit that funnels moisture away from your skin. Don't be fooled by its classic style; this tee hides premium performance technology beneath its unassuming look.", "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/men/tops/tees/ms01-black_main.jpg" }` |

      {style="table-layout:fixed"}

1. 마지막 단계로 고객에게 다른 오퍼에 대한 자격이 없는 경우 전송되는 대체 오퍼를 만들어야 합니다.
   1. **[!UICONTROL 오퍼 만들기]**&#x200B;를 선택합니다.
   1. **[!UICONTROL 새 오퍼]** 대화 상자에서 **[!UICONTROL 개인 맞춤화된 오퍼]**&#x200B;을 선택하고 **[!UICONTROL 다음]**&#x200B;을 선택합니다.
   1. **[!UICONTROL 새 대체 오퍼 만들기]**&#x200B;의 **[!UICONTROL 세부 정보]** 단계에서 오퍼에 대한 **[!UICONTROL 이름]**(예: `Luma - Fallback Offer`)을 입력하고 **[!UICONTROL 다음]**&#x200B;을(를) 선택합니다.

   1. **[!UICONTROL 새 대체 오퍼 만들기]**&#x200B;의 **[!UICONTROL 표시 추가]** 단계에서:
      1. **[!UICONTROL 채널]** 목록에서 ![모바일](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DevicePhone_18_N.svg) **[!UICONTROL 모바일]**&#x200B;을 선택하고 **[!UICONTROL 배치]** 목록에서 **[!UICONTROL 모바일 JSON]**&#x200B;을 선택합니다.
      1. **[!UICONTROL 콘텐츠]**&#x200B;에 대해 **[!UICONTROL 사용자 지정]**&#x200B;을(를) 선택하십시오.
      1. **[!UICONTROL 콘텐츠 추가]**&#x200B;를 선택합니다.
      1. **[!UICONTROL 개인화 추가]** 대화 상자에서 다음 JSON을 입력하고 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

         ```json
         {  
            "title": "Luma",
            "text": "Your store for sports wear and equipment.", 
            "image": "https://luma.enablementadobe.com/content/dam/luma/en/logos/Luma_Logo.png" 
         }  
         ```

      1. **[!UICONTROL 다음]**&#x200B;을 선택합니다.


1. **[!UICONTROL 새 대체 항목 만들기]** 오퍼의 **[!UICONTROL 검토]** 단계에서:
   1. 오퍼를 검토한 다음 **[!UICONTROL 마침]**&#x200B;을 선택합니다.
   1. **[!UICONTROL 오퍼 저장]** 대화 상자에서 **[!UICONTROL 저장 및 승인]**&#x200B;을 선택합니다.

이제 다음 오퍼 목록이 있어야 합니다.
![오퍼 목록](assets/ajo-offers-list.png)


## 컬렉션 만들기

모바일 앱 사용자에게 오퍼를 제공하려면 만든 하나 이상의 오퍼로 구성된 오퍼 컬렉션을 정의해야 합니다.

1. Journey Optimizer UI의 왼쪽 레일에서 **[!UICONTROL 오퍼]**&#x200B;를 선택합니다.
1. 상단 표시줄에서 **[!UICONTROL 컬렉션]**&#x200B;을(를) 선택합니다.
1. ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 컬렉션 만들기]**&#x200B;를 선택합니다.
1. **[!UICONTROL 새 컬렉션]** 대화 상자에서 컬렉션에 사용할 **[!UICONTROL 이름]**(예: `Luma - Mobile App Collection`)을 입력하고 **[!UICONTROL 정적 컬렉션 만들기]**&#x200B;를 선택한 후 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. **[!DNL Luma - Mobile App Collection]**&#x200B;에서 컬렉션에 포함할 오퍼를 선택합니다. 이 자습서에서는 만든 오퍼 5개를 선택합니다. **[!DNL Luma]**&#x200B;을(를) 입력하는 등의 방법으로 검색 필드를 사용하여 목록을 쉽게 필터링할 수 있습니다.
1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

   ![오퍼 - 컬렉션](assets/ajo-collection-offersselected.png)


## 의사 결정 만들기

마지막 단계는 결정을 정의하는 것입니다. 이 결정은 하나 이상의 결정 범위와 대체 오퍼의 조합입니다.

의사 결정 범위는 특정 배치(예: 이메일의 HTML 또는 모바일 앱의 JSON)와 하나 이상의 평가 기준의 조합입니다.

평가 기준은 다음 두 가지를 결합한 것입니다.

* 오퍼 컬렉션,
* 자격 규칙: 예를 들어, 오퍼는 특정 대상에만 사용할 수 있습니다.
* 순위 방법: 여러 오퍼를 사용할 수 있는 경우 순위를 매기는 데 사용할 방법(예: 오퍼 우선 순위, 공식 또는 AI 모델 사용)을 선택합니다.

배치, 규칙, 등급, 오퍼, 표시, 컬렉션, 의사 결정 등이 서로 상호 작용하고 관계를 맺는 방식을 더 잘 이해하려면 [오퍼를 만들고 관리하는 주요 단계](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/get-started-decision/key-steps.html?lang=en)를 참조하십시오. 이 단원은 Journey Optimizer - 의사 결정 관리 내에서 결정을 정의하는 유연성보다는 의사 결정의 결과를 사용하는 데에만 중점을 둡니다.

1. Journey Optimizer UI의 왼쪽 레일에서 **[!UICONTROL 오퍼]**&#x200B;를 선택합니다.
1. 상단 표시줄에서 **[!UICONTROL 결정]**&#x200B;을 선택합니다.
1. ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 결정 만들기]**&#x200B;를 선택합니다.
1. **[!UICONTROL 새 오퍼 결정 만들기]**&#x200B;의 **[!UICONTROL 세부 정보]** 단계에서:
   1. 결정에 대해 **[!UICONTROL 이름]**&#x200B;을(를) 입력하십시오(예: `Luma - Mobile App Decision`). **[!UICONTROL 시작 날짜 및 시간]** 및 **[!UICONTROL 종료 날짜 및 시간]**&#x200B;을 입력하십시오.
   1. **[!UICONTROL 다음]**&#x200B;을 선택합니다.

1. **[!UICONTROL 새 오퍼 결정 만들기]**&#x200B;의 **[!UICONTROL 결정 범위 추가]** 단계에서:
   1. **[!UICONTROL 배치]** 목록에서 **[!UICONTROL 모바일 JSON]**&#x200B;을(를) 선택하십시오.
   1. **[!UICONTROL 평가 기준]** 타일에서 ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 추가]**&#x200B;를 선택합니다.
      1. **[!UICONTROL 오퍼 컬렉션 추가]** 대화 상자에서 오퍼 컬렉션을 선택합니다. 예: **[!DNL Luma - Mobile App Collection]**.
      1. **[!UICONTROL 추가]**를 선택합니다.
         ![결정 - 컬렉션 선택](assets/ajo-decision-selectcollection.png)
   1. **[!UICONTROL 자격 요건]**&#x200B;에 대해 **[!UICONTROL 없음]**&#x200B;을 선택하고 **[!UICONTROL 오퍼 우선 순위]**&#x200B;를 **[!UICONTROL 순위 지정 방법]**&#x200B;으로 선택하십시오.
   1. **[!UICONTROL 다음]**을 선택합니다.
      ![결정 범위](assets/ajo-decision-scopes.png).
1. **[!UICONTROL 새 오퍼 결정 만들기]**&#x200B;의 **[!UICONTROL 대체 오퍼 추가]** 단계에서:
   1. 대체 오퍼(예: **[!DNL Luma - Fallback offer]**)를 선택하십시오.
   1. **[!UICONTROL 다음]**&#x200B;을 선택합니다.
1. **[!UICONTROL 새 오퍼 결정 만들기]**&#x200B;의 **[!UICONTROL 요약]** 단계에서:
   1. **[!UICONTROL 마침]**&#x200B;을 선택합니다.
   1. **[!UICONTROL 오퍼 결정 저장]** 대화 상자에서 **[!UICONTROL 저장 및 활성화]**&#x200B;를 선택합니다.
   1. **[!UICONTROL 결정]** 탭에서 **[!UICONTROL Live]** 상태의 결정이 표시됩니다.

이제 오퍼 세트로 구성된 오퍼 결정을 사용할 준비가 되었습니다. 앱에서 의사 결정을 사용하려면 코드에서 의사 결정 범위를 참조해야 합니다.

1. Journey Optimizer UI에서 **[!UICONTROL 오퍼]**&#x200B;를 선택합니다.
1. 상단 표시줄에서 **[!UICONTROL 결정]**&#x200B;을 선택합니다.
1. 결정을 선택합니다(예: **[!DNL Luma - Mobile App Decision]**).
1. **[!UICONTROL 결정 범위]** 타일에서 ![복사](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) **[!UICONTROL 복사]**&#x200B;를 선택합니다.
1. 상황별 메뉴에서 **[!UICONTROL 결정 범위]**를 선택합니다.
   ![결정 범위 복사](assets/ajo-copy-decisionscope.png)
1. 텍스트 편집기를 사용하여 나중에 사용할 수 있도록 결정 범위를 붙여넣습니다. 결정 범위에는 다음과 같은 JSON 형식이 있습니다.

   ```json
   {
       "xdm:activityId":"xcore:offer-activity:xxxxxxxxxxxxxxx",
       "xdm:placementId":"xcore:offer-placement:xxxxxxxxxxxxxxx"
   }
   ```

## 앱에서 오퍼 구현

이전 단원에서 설명한 대로 모바일 태그 확장을 설치하면 구성만 제공됩니다. 그런 다음 Optimize SDK를 설치하고 등록해야 합니다. 이 단계가 명확하지 않으면 [SDK 설치](install-sdks.md) 섹션을 검토하십시오.

>[!NOTE]
>
>[SDK 설치](install-sdks.md) 섹션을 완료한 경우 SDK가 이미 설치되어 있으므로 이 단계를 건너뛸 수 있습니다.
>

1. Xcode에서 패키지 종속 항목의 패키지 목록에 [AEP 최적화](https://github.com/adobe/aepsdk-messaging-ios)가 추가되었는지 확인하십시오. [Swift 패키지 관리자](install-sdks.md#swift-package-manager)를 참조하세요.
1. Xcode 프로젝트 탐색기에서 **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]**(으)로 이동합니다.
1. `AEPOptimize`이(가) 가져오기 목록의 일부인지 확인하십시오.

   ```swift
   import AEPOptimize
   ```

1. `Optimize.self`이(가) 등록 중인 확장 배열의 일부인지 확인하십시오.

   ```swift
   let extensions = [
       AEPIdentity.Identity.self,
       Lifecycle.self,
       Signal.self,
       Edge.self,
       AEPEdgeIdentity.Identity.self,
       Consent.self,
       UserProfile.self,
       Places.self,
       Messaging.self,
       Optimize.self,
       Assurance.self
   ]
   ```

1. Xcode 프로젝트 탐색기에서 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Model]** > **[!DNL Data]** > **[!UICONTROL 의사 결정]**(으)로 이동합니다. Journey Optimizer 인터페이스에서 복사한 결정 범위 세부 정보로 `activityId` 및 `placementId` 값을 업데이트합니다.

1. Xcode 프로젝트 탐색기에서 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]**(으)로 이동합니다. `func updatePropositionOD(ecid: String, activityId: String, placementId: String, itemCount: Int) async` 함수를 찾습니다. 다음 코드를 추가합니다.

   ```swift
   // set up the XDM dictionary, define decision scope and call update proposition API
   Task {  
      let ecid = ["ECID" : ["id" : ecid, "primary" : true] as [String : Any]]
      let identityMap = ["identityMap" : ecid]
      let xdmData = ["xdm" : identityMap]
      let decisionScope = DecisionScope(activityId: activityId, placementId: placementId, itemCount: UInt(itemCount))
      Optimize.clearCachedPropositions()
      Optimize.updatePropositions(for: [decisionScope], withXdm: xdmData)
   }
   ```

   이 함수:

   * 오퍼를 제공해야 하는 프로필을 식별하는 ECID가 포함된 XDM 사전 `xdmData`을(를) 설정합니다.
   * `decisionScope`을(를) 정의합니다. 이 개체는 Journey Optimizer - 의사 결정 관리 인터페이스에서 정의한 결정에 기반하며 [의사 결정 만들기](#create-a-decision)에서 복사한 의사 결정 범위를 사용하여 정의합니다.  Luma 앱은 다음 JSON 형식을 기반으로 범위 매개 변수를 검색하는 구성 파일(`decisions.json`)을 사용합니다.

     ```swift
     "scopes": [
         {
             "name": "name of the scope",
             "activityId": "xcore:offer-activity:xxxxxxxxxxxxxxx",
             "placementId": "xcore:offer-placement:xxxxxxxxxxxxxxx",
             "itemCount": 2
         }
     ]
     ```

     그러나 Optimize API가 적절한 매개 변수(`activityId`, `placementId` 및 `itemCount`)를 가져오도록 모든 종류의 구현을 사용하여 구현에 올바른 [`DecisionScope`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#decisionscope) 개체를 만들 수 있습니다. <br/>참고: `decisions.json` 파일의 다른 키 값은 나중에 사용하기 위한 것이며 관련성이 없으며 현재 이 단원에서 자습서의 일부로 사용됩니다.

   * [`Optimize.clearCachePropositions`](https://support.apple.com/en-ie/guide/mac-help/mchlp1015/mac) 및 [`Optimize.updatePropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#updatepropositions) API를 호출합니다.  이러한 함수는 캐시된 모든 제안을 지우고 이 프로필에 대한 제안을 업데이트합니다.

1. Xcode 프로젝트 탐색기에서 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!UICONTROL Personalization]** > **[!UICONTROL EdgeOffersView]**(으)로 이동합니다. `func onPropositionsUpdateOD(activityId: String, placementId: String, itemCount: Int) async` 함수를 찾아 이 함수의 코드를 검사합니다. 이 함수에서 가장 중요한 부분은 [`Optimize.onPropositionsUpdate`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#onpropositionsupdate) API 호출입니다.

   * 의사 결정 범위(Journey Optimizer - 의사 결정 관리에서 정의함)를 기반으로 현재 프로필에 대한 제안을 검색합니다.
   * 제안에서 오퍼를 검색합니다.
   * 앱에서 제대로 표시될 수 있도록 오퍼의 콘텐츠를 래핑 해제합니다.
   * 오퍼에 대한 `displayed()` 작업을 트리거하여 오퍼가 표시되었음을 알리는 이벤트를 Edge Network에 다시 보냅니다.

1. **[!DNL EdgeOffersView]**&#x200B;에서 `.onFirstAppear` 한정자에 다음 코드를 추가하십시오. 이 코드는 오퍼를 업데이트하기 위한 콜백이 한 번만 등록되도록 합니다.

   ```swift
   // Invoke callback for offer updates
   Task {
       await self.onPropositionsUpdateOD(activityId: decision.activityId, placementId: decision.placementId, itemCount: decision.itemCount)
   }
   ```

1. **[!UICONTROL EdgeOffersView]**&#x200B;에서 `.task` 한정자에 다음 코드를 추가하십시오. 이 코드는 보기를 새로 고칠 때 오퍼를 업데이트합니다.

   ```swift
   // Clear and update offers
   await self.updatePropositionsOD(ecid: currentEcid, activityId: decision.activityId, placementId: decision.placementId, itemCount: decision.itemCount)
   ```



## 앱을 사용하여 유효성 검사

1. ![재생](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg)을 사용하여 시뮬레이터나 Xcode의 실제 장치에서 앱을 다시 빌드하고 실행합니다.

1. **[!DNL Personalisation]** 탭으로 이동합니다.

1. **[!DNL Edge Personalisation]**&#x200B;를 선택합니다.

1. 맨 위로 스크롤하면 **[!DNL DECISION LUMA - MOBILE APP DECISION]** 타일에서 정의한 컬렉션에서 두 개의 무작위 오퍼가 표시됩니다.

   <img src="assets/ajo-app-offers.png" width="300">

   모든 오퍼에 동일한 우선 순위를 부여했으므로 오퍼는 임의적이며 의사 결정 순위는 우선 순위를 기반으로 합니다.


## Assurance에서 구현 유효성 검사

Assurance에서 오퍼 구현을 확인하려면 다음을 수행하십시오.

1. [설치 지침](assurance.md#connecting-to-a-session) 섹션을 검토하여 시뮬레이터 또는 장치를 Assurance에 연결하십시오.
1. 왼쪽 레일에서 **[!UICONTROL 구성]**&#x200B;을 선택하고 **[!UICONTROL ADOBE JOURNEY OPTIMIZER DECISIONING]** 아래의 **[!UICONTROL 검토 및 시뮬레이션]** 옆에 있는 ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg)을 선택합니다.
1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.
1. 왼쪽 레일에서 **[!UICONTROL 검토 및 시뮬레이션]**&#x200B;을 선택합니다. 데이터 스트림 설정과 SDK 설정이 모두 애플리케이션에서 검증되었습니다.
1. 상단 표시줄에서 **[!UICONTROL 요청]**&#x200B;을(를) 선택합니다. **[!UICONTROL 오퍼]** 요청이 표시됩니다.
   ![AJO 의사 결정 유효성 검사](assets/assurance-decisioning-requests.png)

1. **[!UICONTROL 시뮬레이션]** 및 **[!UICONTROL 이벤트 목록]** 탭을 탐색하여 추가 기능을 사용할 수 있습니다. Journey Optimizer 의사 결정 관리 설정을 확인하세요.

## 다음 단계

이제 Journey Optimizer - 의사 결정 관리 구현에 더 많은 기능을 추가할 수 있는 모든 도구를 보유해야 합니다. 예:

* 오퍼에 다른 매개 변수 적용(예: 우선 순위, 최대 가용량)
* 앱에서 프로필 특성을 수집하고([프로필](profile.md) 참조) 이 프로필 특성을 사용하여 대상자를 빌드합니다. 그런 다음 이러한 대상을 의사 결정의 자격 규칙의 일부로 사용합니다.
* 두 개 이상의 결정 범위를 결합합니다.

>[!SUCCESS]
>
>Experience Platform Mobile SDK용 Journey Optimizer - Decisioning 확장을 사용하여 오퍼를 표시하도록 앱을 활성화했습니다.
>
>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하고 싶거나 향후 콘텐츠에 대한 제안이 있는 경우 이 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)에서 공유하십시오.

다음: **[A/B 테스트 수행](target.md)**
