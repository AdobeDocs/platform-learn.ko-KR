---
title: Customer Journey Analytics을 사용하여 모바일 앱 데이터 보고 및 분석
description: Customer Journey Analytics을 사용하여 모바일 앱과의 상호 작용을 보고하고 분석하는 방법을 알아봅니다.
solution: Data Collection,Experience Platform,Analytics
hide: true
hidefromtoc: true
source-git-commit: 7237bc0e6fabd74157022b99e6edee47ef83f1c9
workflow-type: tm+mt
source-wordcount: '3410'
ht-degree: 1%

---

# Customer Journey Analytics을 사용하여 보고 및 분석

Customer Journey Analytics과의 모바일 앱 상호 작용을 보고하고 분석하는 방법에 대해 알아봅니다.

이전 단원에서 수집하여 Platform Edge Network으로 전송한 모바일 앱 이벤트 데이터는 데이터스트림에 구성된 서비스로 전달됩니다. 다음을 수행한 경우 [Experience Platform으로 데이터 보내기](platform.md) 단원: 이제 해당 데이터가 데이터 세트로 Experience Platform의 데이터 레이크에 저장됩니다. 그런 다음 해당 데이터를 Customer Journey Analytics이 보고 및 분석에 사용할 수 있습니다.

Adobe Analytics과 달리 Customer Journey Analytics은 *사용* Experience Platform에서 만들었으며 앱에서 데이터를 전송하는 데이터 세트의 데이터. Adobe Experience Platform Mobile SDK를 사용하면 데이터를 Customer Journey Analytics으로 직접 전송하지 않습니다. 대신 Customer Journey Analytics은 Experience Platform 데이터 세트의 데이터를 사용합니다.

자습서의 이 단원은 Luma 자습서 앱에서 캡처한 데이터를 보고하고 분석하는 데 중점을 둡니다. Customer Journey Analytics의 고유한 기능 중 하나는 여러 소스(CRM, 판매 지점, 로열티 애플리케이션, 콜 센터)와 채널(웹, 모바일, 오프라인)의 데이터를 결합하여 고객 여정에 대한 심도 있는 통찰력을 제공하는 것입니다. 이 기능은 이 단원에서 다루지 않습니다. 다음을 참조하십시오 [Customer Journey Analytics 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) 추가 정보.


## 전제 조건

조직이 프로비저닝되고 Customer Journey Analytics에 대한 권한이 부여되어야 합니다. Customer Journey Analytics에 대한 관리 액세스 권한이 있어야 합니다.


## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

- 연결을 만들어 Customer Journey Analytics에 사용할 Experience Platform에서 데이터 세트를 정의합니다.
- 데이터 보기를 만들어 보고 및 분석을 위해 데이터 세트의 데이터를 준비합니다
- 프로젝트를 만들어 모바일 앱의 데이터를 분석할 수 있도록 보고서와 시각화를 작성합니다.

이 주문은 고의로 된 것입니다. Customer Journey Analytics에서 Analysis Workspace의 보고서는 데이터 보기에 따라 다릅니다. 데이터 보기는 연결에 따라 다릅니다.


## 연결 만들기

Customer Journey Analytics의 연결은 보고 및 분석에 사용할 Experience Platform의 데이터 세트(및 이러한 데이터 세트 내의 데이터)를 정의합니다.

1. 앱을 사용하여 Customer Journey Analytics 인터페이스로 이동합니다 ![앱](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) 오른쪽 상단의 메뉴

1. 선택 **[!UICONTROL 연결]** 을 클릭합니다.

1. 다음을 선택하십시오. **[!UICONTROL 목록]** Connections 인터페이스의 탭입니다. 기존 연결 목록이 표시됩니다.

1. 선택 **[!UICONTROL 새 연결 만들기]**.

1. 다음에서 **[!UICONTROL 연결]** > **[!UICONTROL 제목 없는 연결]** 화면, 위치 **[!UICONTROL 연결 설정]**

   1. 입력 **[!UICONTROL 연결 이름]**, 예 `Luma App - AEP Mobile SDK Tutorial Connection`.
   2. 입력 **[!UICONTROL 연결 설명]**, 예 `Connection for the Luma app used in the AEP Mobile SDK tutorial`.

      위치 **[!UICONTROL 데이터 설정]**:

   3. 모바일 앱 데이터를 수집하는 데 사용한 샌드박스 를 선택합니다. 예를 들면 다음과 같습니다 **[!UICONTROL 모바일 및 웹 SDK 교육 과정]**.
   4. 선택 **[!UICONTROL 백만 미만]** 다음에서 **[!UICONTROL 일일 평균 이벤트 수]**.

   5. 선택 **[!UICONTROL 데이터 세트 추가]** Experience Platform에서 Customer Journey Analytics에 사용할 데이터 세트를 선택합니다.

      ![CJA 연결 1](assets/cja-connections-1.png)

   6. 다음에서 **[!UICONTROL 데이터 세트 추가]** 마법사, **[!UICONTROL 데이터 세트 선택]** 단계,

      1. 다음 데이터 세트를 선택하십시오.

         - **[!UICONTROL Luma 모바일 앱 이벤트 데이터 세트]**, 의 일부로 만든 데이터 세트 [데이터 세트 만들기](platform.md#create-a-dataset) Experience Platform 섹션에 있는 마지막 항목이 될 필요가 없습니다.
         - **[!UICONTROL ODE DecisionEvents - *샌드박스 이름*] 의사 결정**
         - **[!UICONTROL AJO 푸시 추적 이벤트 데이터 세트]**

      1. 선택 **[!UICONTROL 다음]**.

         ![CJA 연결 2](assets/cja-connections-2.png)

   7. 다음에서 **[!UICONTROL 데이터 세트 추가]** 마법사, **[!UICONTROL 데이터 세트 설정]** 단계에서는 각 이벤트 데이터 세트에 대한 세부 사항을 정의해야 합니다.
      1. 올바른 설정을 위해 다음 표를 참조하십시오.

         | 데이터 세트 | 개인 ID<br/>① | 타임스탬프<br>② | 데이터 소스 유형 ③ | 모든 새 데이터 ④ 가져오기 | 기존의 모든 데이터 ⑤ 채우기 |
         |---|---|---|---|---|---|
         | Luma 모바일 앱 이벤트 데이터 세트 | identityMap | 타임스탬프 | 모바일 앱 데이터 | 활성화 | 활성화 |
         | ODE DecisionEvents - *샌드박스 이름* 의사 결정 | identityMap | 타임스탬프 | 모바일 앱 데이터 | 활성화 | 활성화 |
         | AJO 푸시 추적 경험 이벤트 데이터 세트 | identityMap | 타임스탬프 | 모바일 앱 데이터 | 활성화 | 활성화 |

      1. 선택 **[!UICONTROL 데이터 세트 추가]**.

         ![CJA 연결 3](assets/cja-connections-3.png)

1. 뒤로 이동 **[!UICONTROL 연결]** > **[!UICONTROL Luma 앱 - AEP 모바일 SDK 튜토리얼 연결]**, 선택 **[!UICONTROL 저장]** 연결을 저장합니다.

   ![CJA 연결 4](assets/cja-connections-4.png)

이제 연결을 정의하고 Customer Journey Analytics이 데이터 세트의 데이터를 자체 내부 데이터베이스에 추가합니다. 이 데이터 수집은 데이터의 양에 따라 시간이 걸릴 수 있습니다. 튜토리얼 앱의 경우, 데이터가 Customer Journey Analytics에 표시될 때까지 2시간 정도 예측합니다.

연결 상태를 보려면:

1. 선택 **[!UICONTROL 연결]** Customer Journey Analytics의 기본 인터페이스에서 다음을 수행합니다.
1. 연결 이름 선택(예: ) **[!UICONTROL Luma 앱 - AEP 모바일 SDK 튜토리얼 연결]**.

다음에서 **[!UICONTROL 연결]** > **[!UICONTROL Luma 앱 - AEP 모바일 SDK 튜토리얼 연결]**, 다음이 표시됩니다.

1. 추가된 총 레코드, 건너뛴 레코드 및 삭제된 레코드에 대한 정보입니다. 다음을 선택하십시오. **[!UICONTROL 모든 데이터 세트]** 연결에 대한 세부 정보를 보려면 적절한 기간을 선택하십시오. 다음을 사용할 수 있습니다. ![캘린더](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Calendar_18_N.svg) 기간을 선택하는 대화 상자를 엽니다.
1. 추가된 레코드, 건너뛴 레코드, 삭제된 레코드 등에 대한 개별 데이터 세트에 대한 정보입니다.

   ![CJA 연결 6](assets/cja-connections-6.png)


## 데이터 보기 만들기

Customer Journey Analytics에 데이터 세트에서 레코드가 추가되면 데이터 보기를 만들어 보고할 데이터의 구성 요소를 정의할 수 있습니다.

데이터 보기는 연결에서 데이터를 해석하는 방법을 결정할 수 있도록 해주는 Customer Journey Analytics과 관련된 컨테이너입니다. 연결에 정의한 데이터 세트에서 표준 및 스키마 필드를 Analysis Workspace의 구성 요소(차원, 지표)로 구성할 수 있습니다.

Customer Journey Analytics의 데이터 보기는 연결에서 데이터를 올바르게 설정하고 정의하는 데 엄청난 유연성을 제공합니다. 이 자습서에서는 보고 및 분석에 필요한 기능만 사용합니다. 다음을 참조하십시오 [데이터 보기](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views) 추가 정보.


데이터 보기를 만들려면 다음을 수행하십시오.

1. 앱을 사용하여 Customer Journey Analytics 인터페이스로 이동합니다 ![앱](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) 오른쪽 상단의 메뉴

1. 선택 **[!UICONTROL 데이터 보기]** 을 클릭합니다.
1. 선택 **[!UICONTROL 새 데이터 보기 만들기]**.
1. 위치 **[!UICONTROL 데이터 보기 >]**, 다음을 확인합니다. **[!UICONTROL 구성]** 탭이 선택되어 있습니다.

   1. 연결 설정 드롭다운 목록에서 연결을 선택합니다. 예를 들면 다음과 같습니다 **[!UICONTROL Luma 앱 - AEP 모바일 SDK 튜토리얼 연결]**.
   1. 데이터 보기의 이름 입력 예: `Luma App - AEP Mobile SDK Tutorial Data view`.
   1. 선택 **[!UICONTROL 저장 및 계속]**.

      ![CJA 데이터 보기 1](assets/cja-dataview-1.png)

1. 다음에서 **[!UICONTROL 구성 요소]** 의 탭 **[!UICONTROL Luma 앱 - AEP 모바일 SDK 튜토리얼 데이터 보기]**, 모바일 앱에 대해 보고할 때 사용할 지표와 차원을 정의할 수 있습니다. 기본적으로 데이터 보기에 대해 많은 표준 지표 및 차원(구성 요소와 함께 지칭됨)이 이미 구성되어 있습니다. 그러나 데이터 보기에는 더 많은 구성 요소가 필요합니다. <br/>스키마 필드를 추가하려면 이전에 정의한 스키마에서 또는 즉시 사용 가능한 스키마(참조) [스키마 만들기](create-schema.md) 단원) (구성 요소(차원 또는 지표)로서:

   1. 스키마 필드 찾기:

      - 를 사용하여 구성 요소 검색 ![검색](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) ***[!UICONTROL 스키마 필드 검색]*** 검색 필드. 예를 들어, `productListAdd`, 또는

        ![CJA 데이터 보기 2a](assets/cja-dataview-2a.png)

      - 내의 스키마 필드로 트래버스 다운 ![폴더](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **[!UICONTROL 이벤트 데이터 세트]** ![펼침](https://spectrum.adobe.com/static/icons/ui_18/ChevronSize100.svg). <br/>예를 들어, ![폴더](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **[!UICONTROL 이벤트 데이터 세트]** ![펼침](https://spectrum.adobe.com/static/icons/ui_18/ChevronSize100.svg) ![폴더](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **[!UICONTROL commerce]** ![펼침](https://spectrum.adobe.com/static/icons/ui_18/ChevronSize100.svg) ![폴더](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **[!UICONTROL 제품 목록 추가]** ![펼침](https://spectrum.adobe.com/static/icons/ui_18/ChevronSize100.svg)

        ![CJA 데이터 보기 2a](assets/cja-dataview-2b.png)

   1. 스키마 필드 창에서 특정 스키마 필드를 드래그하여 **[!UICONTROL 지표]** 또는 **[!UICONTROL DIMENSION]** 목록: [!UICONTROL 포함된 구성 요소] 창.

      ![CJA 데이터 보기 2a](assets/cja-dataview-3.png)

   1. 구성 요소의 설정을 구성할 수 있습니다. 오른쪽 창에서 구성 요소를 선택하고 설정을 구성합니다. <br/>예를 들어 의 이름을 바꿀 수 있습니다 **[!UICONTROL commerce.productListAdds]** 끝 `Product Add To Lists` 사용 **[!UICONTROL 구성 요소 설정]** > **[!UICONTROL 구성 요소 이름]** 오른쪽 창의 필드입니다.

      ![CJA Dataview 3b](assets/cja-dataview-3b.png)

      또는 구성 **[!UICONTROL 포함/제외 값]**.

      ![CJA 데이터 보기 구성 요소 설정](assets/cja-dataview-component-settings.png)

   1. 데이터 보기에 필드를 추가하고 결과 구성 요소를 구성하는 방법을 이해했으므로 아래 표를 사용하여 지표 또는 차원으로 추가할 스키마 필드 목록을 확인하십시오. 사용 **스키마 경로** 특정 스키마 필드를 검색하거나 트래버스하기 위한 아래 표의 열 값입니다. 드래그 앤 드롭한 후 **구성 요소 설정** 구성 요소 수정과 같은 특정 설정이 구성 요소에 필요한지 여부에 대한 테이블의 열 값 **[!UICONTROL 구성 요소 이름]** 또는 정의 **[!UICONTROL 포함/제외 값]**.

      **지표**

      | 구성 요소 이름 | 데이터 세트 | 스키마 데이터 유형 | 스키마 경로 | 구성 요소 설정 |
      |---|---|---|---|---|
      | 닫기 | AJO 푸시 추적 경험 이벤트 데이터 세트, Luma 모바일 앱 이벤트 데이터 세트 | 정수 | _experience.decisioning.<br/>propositionEventType.dismissing | 구성 요소 이름: `Dismiss` |
      | 구독 취소 | AJO 푸시 추적 경험 이벤트 데이터 세트, Luma 모바일 앱 이벤트 데이터 세트 | 정수 | _experience.decisioning.<br/>propositionEventType.unsubscribe | 구성 요소 이름: `Unsubscribe` |
      | 트리거 | AJO 푸시 추적 경험 이벤트 데이터 세트, Luma 모바일 앱 이벤트 데이터 세트 | 정수 | _experience.decisioning.<br/>propositionEventType.trigger | 구성 요소 이름: `Trigger` |
      | 표시 | AJO 푸시 추적 경험 이벤트 데이터 세트, Luma 모바일 앱 이벤트 데이터 세트 | 정수 | _experience.decisioning.<br/>propositionEventType.display | 구성 요소 이름: `Display` |
      | 보내기 | AJO 푸시 추적 경험 이벤트 데이터 세트, Luma 모바일 앱 이벤트 데이터 세트 | 정수 | _experience.decisioning.<br/>propositionEventType.send | 구성 요소 이름: `Send` |
      | 상호 작용 | AJO 푸시 추적 경험 이벤트 데이터 세트, Luma 모바일 앱 이벤트 데이터 세트 | 정수 | _experience.decisioning.<br/>propositionEventType.interact | 구성 요소 이름: `Interact` |
      | 위치 이벤트 | AJO 푸시 추적 경험 이벤트 데이터 세트, Luma 모바일 앱 이벤트 데이터 세트, ODE DecisionEvents - 모바일 및 웹-sdk-courses 의사 결정 | 문자열 | 이벤트 유형 | 구성 요소 이름: `Location Events`<br/><br/>![포함/제외](assets/cja-dataview-include-exclude.png) |
      | 제품 보기 | Luma 모바일 앱 이벤트 데이터 세트 | 더블 | commerce.productViews.value | 구성 요소 이름: `Product Views` |
      | 목록에 제품 추가 | Luma 모바일 앱 이벤트 데이터 세트 | 더블 | commerce.productListAdds.value | 구성 요소 이름: `Product Add To Lists` |
      | 구매 | Luma 모바일 앱 이벤트 데이터 세트 | 더블 | commerce.purchases.value | 구성 요소 이름: `Purchases` |
      | 나중에 저장 | Luma 모바일 앱 이벤트 데이터 세트 | 더블 | commerce.saveForLaters.value | 구성 요소 이름: `Save For Laters` |
      | 앱 상호 작용 | Luma 모바일 앱 이벤트 데이터 세트 | 더블 | _techmarketingdemos.appInformation.<br/>appInteraction.appAction.value | 구성 요소 이름: `App Interactions` |
      | 화면 보기 | Luma 모바일 앱 이벤트 데이터 세트 | 더블 | _techmarketingdemos.appInformation.<br/>appStateDetails.screenView.value | 구성 요소 이름: `Screen Views` |

      {style="table-layout:auto"}

      위치 이벤트 지표에 대한 스키마 필드가 을 사용하는 방법을 확인합니다 **[!UICONTROL 포함/제외 값]** 다음을 포함하는 이벤트 유형 계산 `location`.

      위 표의 모든 스키마 필드를 지표 구성 요소로 추가한 후에는 다음에 대한 데이터 보기 구성이 **[!UICONTROL 지표]** 은(는) 다음과 같아야 합니다.

      ![CJA 데이터 보기 4](assets/cja-dataview-4.png)

      **DIMENSION**

      | 구성 요소 이름 | 데이터 세트 | 스키마 데이터 유형 | 스키마 경로 | 구성 요소 설정 |
      |---|---|---|---|---|
      | 구/군/시 | AJO 푸시 추적 경험 이벤트 데이터 세트, Luma 모바일 앱 이벤트 데이터 세트 | 문자열 | placeContext.geo.city | 구성 요소 이름: `City` |
      | 이벤트 유형 | AJO 푸시 추적 경험 이벤트 데이터 세트, Luma 모바일 앱 이벤트 데이터 세트, ODE DecisionEvents - 모바일 및 웹-sdk-courses 의사 결정 | 문자열 | eventType | 구성 요소 이름: `Event Types` |
      | 결정 옵션 이름 | AJO 푸시 추적 경험 이벤트 데이터 세트, Luma 모바일 앱 이벤트 데이터 세트, ODE DecisionEvents - 모바일 및 웹-sdk-courses 의사 결정 | 문자열 | _experience.decisioning.<br/>propositions.items.name | 구성 요소 이름: `Decision Option Name` |
      | 앱 상호 작용 이름 | Luma 모바일 앱 이벤트 데이터 세트 | 문자열 | _techmarketingdemos.appInformation.<br/>appInteraction.name | 구성 요소 이름: `App Interaction Name` |
      | 화면 이름 | Luma 모바일 앱 이벤트 데이터 세트 | 문자열 | _techmarketingdemos.appInformation.<br/>appStateDetails.screenName | 구성 요소 이름: `Screen Name` |
      | 활동 이름 | ODE DecisionEvents - 모바일 및 웹 SDK 과정 의사 결정 | 문자열 | _experience.decisioning.<br/>propositionDetails.activity.name | 구성 요소 이름: `Activity Name` |
      | 오퍼 이름 | ODE DecisionEvents - 모바일 및 웹 SDK 과정 의사 결정 | 문자열 | _experience.decisioning.<br/>propositionDetails.selections.name | 구성 요소 이름: `Offer Name` |

      {style="table-layout:auto"}

      위 표의 모든 스키마 필드를 차원 구성 요소로 추가한 후에는 다음에 대한 데이터 보기 구성이 **[!UICONTROL DIMENSION]** 은(는) 다음과 같아야 합니다.

      ![CJA 데이터 보기 4](assets/cja-dataview-5.png)

   1. 선택 **[!UICONTROL 저장 및 계속]**.

1. 다음 **[!UICONTROL 설정]** 의 탭 **[!UICONTROL Luma 앱 - AEP 모바일 SDK 튜토리얼 데이터 보기]** 필터 및 세션 설정을 구성할 수 있습니다. 이 자습서에서는 추가 구성이 필요하지 않습니다.

   - 선택 **[!UICONTROL 저장 및 마침]**.

데이터 보기를 정의했으며 보고서 및 시각화 작성을 시작하기 위한 모든 것이 준비되었습니다.

## 프로젝트 만들기

Customer Journey Analytics의 작업 공간 프로젝트를 사용하여 보고서와 시각화를 작성할 수 있습니다. 포괄적인 보고서와 흥미로운 시각화를 구축할 수 있는 다양한 가능성이 있지만 이러한 모든 가능성은 이 자습서의 범위를 벗어납니다. 다음을 참조하십시오 [작업 영역 개요](https://experienceleague.adobe.com/en/docs/customer-journey-analytics-learn/tutorials/analysis-workspace/workspace-projects/analysis-workspace-overview) 및 [새 프로젝트 빌드](https://experienceleague.adobe.com/en/docs/customer-journey-analytics-learn/tutorials/analysis-workspace/workspace-projects/build-a-new-project) 추가 정보.

단원의 이 섹션에서는 다음에 대한 보고서 및 시각화를 표시하는 프로젝트를 만듭니다.

- 앱 사용: 화면 및 앱 상호 작용에 대한 정보 사용.
- Commerce: 제품 보기와 같은 상거래 이벤트를 사용하여 장바구니에 추가 및 구매
- 오퍼: 앱에 표시된 오퍼 이벤트를 사용합니다.
- 스토어 방문: 앱의 (시뮬레이션된) 지오펜스 이벤트 사용.

프로젝트를 만들려면 다음 작업을 수행하십시오.

1. 앱을 사용하여 Customer Journey Analytics 인터페이스로 이동합니다 ![앱](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) 오른쪽 상단의 메뉴

1. 선택 **[!UICONTROL 작업 영역]** 을 클릭합니다.

1. 선택 **[!UICONTROL 프로젝트 만들기]**.

   1. 선택 **[!UICONTROL 빈 작업 영역 프로젝트]** 팝업 대화 상자에서

   1. **[!UICONTROL 만들기]**&#x200B;를 선택합니다.

      ![CJA 프로젝트 - 1](assets/cja-projects-1.png)

1. 이(가) 제공됩니다. **[!UICONTROL 새 프로젝트]** 인터페이스. 이 인터페이스에서는 보고서와 시각화를 빌드합니다.

1. 프로젝트 이름(**[!UICONTROL 새 프로젝트]**) 프로젝트에 대한 고유한 이름을 입력합니다. 예: `Luma App - AEP Mobile SDK Tutorial Project`.
   ![CJA 프로젝트 2](assets/cja-projects-2.png)

1. 프로젝트를 저장하려면 을 선택합니다. **[!UICONTROL 프로젝트]** > **[!UICONTROL 저장]**.
   ![CJA 프로젝트 3](assets/cja-projects-3.png)

1. 다음에서 **[!UICONTROL 저장]** 대화 상자, 다른 필드 모두 무시 및 선택 **[!UICONTROL 저장]**.
   ![CJA 프로젝트 4](assets/cja-projects-4.png)


>[!IMPORTANT]
>
>   정기적으로 프로젝트를 저장해야 합니다. 그렇지 않으면 변경 사항이 손실됩니다. 다음을 사용하여 프로젝트를 빠르게 저장할 수 있습니다. **[!UICONTROL ctrl + s]** (Windows) 또는 **[!UICONTROL ⌘(cmd) + s]** (macOS).

이제 프로젝트를 설정했습니다. 이미 기본 캔버스에 자유 형식 테이블이 포함된 자유 형식 패널이 있습니다. 곧 이 표에 구성 요소를 추가할 예정이지만, 먼저 자유 형식 패널이 올바른 데이터 보기와 올바른 기간을 사용하고 있는지 확인해야 합니다.


1. 드롭다운 목록에서 데이터 보기를 선택합니다. 예를 들어, **[!UICONTROL Luma 앱 - AEP 모바일 SDK 튜토리얼 데이터 보기]**. 데이터 보기가 목록에 표시되지 않으면 을 선택합니다. **[!UICONTROL 모두 표시]** 드롭다운 목록 맨 아래에 있습니다.
   ![CJA 프로젝트 5](assets/cja-projects-5.png)

1. 패널에 적합한 기간을 정의하려면 기본값을 선택합니다 **[!UICONTROL 이번 달]** 팝업 패널에서 시작 날짜와 종료 날짜를 정의합니다. 또는 **[!UICONTROL 사전 설정]**, 좋아요 **[!UICONTROL 지난 6개월]** 및 선택 **[!UICONTROL 적용]**.
   ![CJA 프로젝트 6](assets/cja-projects-6.png)


### 앱 사용

앱이 사용되는 방식을 보고하려고 합니다. 앱 상호 작용을 등록하는 데 필요한 코드와 앱에서 사용되는 화면을 앱에 추가했습니다(참조) [이벤트 추적](events.md) 단원)을 추가하고 이 데이터에 대해 보고하려 합니다.

#### 화면 이름

먼저 앱에서 본 화면을 보고합니다.

1. 이름 바꾸기 **[!UICONTROL 자유 형식]** 패널 대상 `App Usage`.

1. 이름 바꾸기 **[!UICONTROL 자유 형식 테이블]** 끝 `Screen Names`.

1. 선택 **[!UICONTROL 모두 표시]** 아래 **[!UICONTROL 지표]** 목록을 표시합니다.

1. 을(를) 끌어다 놓습니다. **[!UICONTROL 화면 보기]** 구성 요소 [!UICONTROL _드롭 a **지표**여기(또는 기타 구성 요소)_)].
   ![CJA 프로젝트 7](assets/cja-projects-7.png)
이제 자유 형식 테이블에 선택한 기간(일)의 화면 보기가 표시됩니다. 하지만 앱에서 사용되는 다양한 화면의 화면 보기를 표시하려고 합니다.

1. 표시 방법 **[!UICONTROL DIMENSION]** 구성 요소 목록, 선택 ![교차](https://spectrum.adobe.com/static/icons/ui_18/CrossSize100.svg) 제거 ![이벤트](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Event_18_N.svg) **[!UICONTROL 지표]** 구성 요소 레일에서 필터링합니다.
   ![CJA 프로젝트 8](assets/cja-projects-8.png)

1. 선택 **[!UICONTROL 모두 표시]** 아래 **[!UICONTROL DIMENSION]** 목록을 표시합니다.

1. 을(를) 끌어다 놓습니다. **[!UICONTROL 화면 이름]** 의 구성 요소 **[!UICONTROL 일]** 머리글입니다. 작업이 다음을 표시합니다. ![전환](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Switch_18_N.svg) **[!UICONTROL 바꾸기]** 치수의 대체를 나타냅니다.
   ![CJA 프로젝트 9](assets/cja-projects-9.png)

첫 번째 보고서가 준비되었습니다. 앱에서 정의한 다양한 화면 이름에 대한 화면 보기를 표시합니다.

![CJA 프로젝트 10](assets/cja-projects-10.png)

프로젝트를 저장하는 것을 잊지 마십시오!

#### 앱 상호 작용

사용자가 앱과 상호 작용하는 방식에 대해서도 보고하려고 합니다.

1. 선택 ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) 팝업에서 ![자유 형식 테이블](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Table_18_N.svg) 새 자유 형식 테이블을 추가합니다.
   ![CJA 프로젝트 11](assets/cja-projects-11.png)

1. 이름 바꾸기 **[!UICONTROL 자유 형식 테이블 (2)]** 끝 `App Interactions`.

1. 을(를) 끌어다 놓습니다. **[!UICONTROL 앱 상호 작용]** 지표 [!UICONTROL _드롭 a **지표**여기(또는 기타 구성 요소)_)].

1. 을(를) 끌어다 놓습니다. **[!UICONTROL 앱 상호 작용 이름]** 다음에 대한 차원 **[!UICONTROL 일]** 이 차원을 바꿀 헤더입니다.

이제 앱 상호 작용을 보여주는 두 번째 보고서가 준비되었습니다.
![CJA 프로젝트 12](assets/cja-projects-12.png)

주로 를 구현했기 때문에 정보가 제한됩니다 `MobileSDK.shared.sendAppInteractionEvent(actionName: "<actionName>")` 로그인 화면에서만 API를 호출합니다. 이 API 호출을 앱의 더 많은 화면에 추가하면 이 보고서가 더 많은 정보를 얻을 수 있습니다.

프로젝트를 저장하는 것을 잊지 마십시오!


### Commerce

이제 앱에서 발생하는 상거래 이벤트에 대해 별도의 패널에 보고하려고 합니다.

#### Commerce 이벤트

1. 선택 ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) 전류가 아닌 [!UICONTROL 앱 사용] 패널 을 클릭하여 새 패널을 만듭니다.
   ![CJA 프로젝트 13](assets/cja-projects-13.png)

1. 적절한 기간을 선택해야 합니다.

1. 선택 ![자유 형식 테이블](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Table_18_N.svg) **[!UICONTROL 자유 형식 테이블]** 를 클릭하여 새 자유 형식 테이블을 만듭니다.
   ![CJA 프로젝트 14](assets/cja-projects-14.png)

1. 이름 바꾸기 **[!UICONTROL 패널]** 끝 `Commerce`.

1. 이름 바꾸기 **[!UICONTROL 자유 형식 테이블]** 끝 `Commerce Events`.

1. 드래그 앤 드롭 **[!UICONTROL 제품 보기]** 다음에 대한 지표 [!UICONTROL _드롭 a **지표**여기(또는 기타 구성 요소)_)].

1. 을(를) 끌어다 놓습니다. **[!UICONTROL 목록에 제품 추가]** 의 오른쪽에 있는 지표 **[!UICONTROL 제품 보기]** 열 : 자유 형식 테이블에 이 열을 삽입합니다. 확인 **[!UICONTROL + 추가]** 열을 삽입하면 파란색으로 표시됩니다.
   ![CJA 프로젝트 15](assets/cja-projects-15.png)

1. 이전 단계를 반복하여 다음을 추가합니다. **[!UICONTROL 나중을 위해 저장]** 지표 및 **[!UICONTROL 구매]** 지표를 자유 형식 테이블에 추가합니다.

1. 을(를) 끌어다 놓습니다. **[!UICONTROL 월]** 차원 맨 위 **[!UICONTROL 일]** 보고서를 일별에서 월별로 변경하는 차원입니다.

사용자 **[!UICONTROL Commerce 이벤트]** 이제 사용자가 제품을 보고, 위시리스트에 제품을 추가하고, 나중에 사용하기 위해 제품을 저장하거나 제품을 구매한 방법을 보여주는 보고서가 준비되었습니다.
![CJA 프로젝트 16](assets/cja-projects-16.png)

프로젝트를 저장하는 것을 잊지 마십시오!

#### 폴아웃

이전 보고서를 기반으로, 상거래 단계에서 폴아웃을 시각화하려고 합니다. 제품을 본 사용자 수가 장바구니에 제품을 추가했는지 여부입니다. 그리고 장바구니에 제품을 추가한 사용자 수 또한 이러한 제품을 나중에 저장했습니다. 기타 등등.

1. 선택 ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) 다음 범위 내 **[!UICONTROL 상거래]** 패널 및 팝업에서 을 선택합니다. ![폴아웃](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ConversionFunnel_18_N.svg) (폴아웃 시각화를 나타냅니다.)

1. 선택 **[!UICONTROL 제품 보기]** 다음에서 [!UICONTROL *터치포인트 추가*] 드롭다운 목록입니다.
   ![CJA 프로젝트 18](assets/cja-projects-18.png)
또는 을(를) 끌어서 놓을 수 있습니다. **[!UICONTROL 제품 보기]** 차원 아래 **[!UICONTROL 모든 사람]** 차원 위치: **[!UICONTROL 폴아웃]** 시각화.

1. 다음 기간 동안 위 단계를 반복합니다. **[!UICONTROL 목록에 제품 추가]** 및 **[!UICONTROL 구매]** 차원.

사용자 **[!UICONTROL 폴아웃]** 이제 시각화에 제품에 대한 전환 단계의 시각적 표현이 표시됩니다.
![CJA 프로젝트 19](assets/cja-projects-19.png)

프로젝트를 저장하는 것을 잊지 마십시오!


### 오퍼

앱 사용자에게 표시되는 오퍼 수와 오퍼에 대해 보고하려고 합니다.

#### 월별 개요

1. 선택 ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) 현재 Commerce 패널 외부에서 새 패널을 만듭니다.

1. 이름 바꾸기 **[!UICONTROL 패널]** 끝 `Offers`.

1. 적절한 기간을 선택해야 합니다.

1. 선택 ![자유 형식 테이블](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Table_18_N.svg) 자유 형식 테이블 : 새 자유 형식 테이블을 만듭니다.

1. 이름 바꾸기 **[!UICONTROL 자유 형식 테이블]** 끝 `Monthly Overview`.

1. 을(를) 끌어다 놓습니다. **[!UICONTROL 표시]** 다음에 대한 지표 [!UICONTROL _드롭 a **지표**여기(또는 기타 구성 요소)_)].

1. 을(를) 끌어다 놓습니다. **[!UICONTROL 월]** 다음에 대한 차원 **[!UICONTROL 일]** 열 - 차원을 대체합니다.

이제 앱에서 사용자에게 표시되는 월별 오퍼를 보여 주는 보고서가 있습니다.
![CJA 프로젝트 20](assets/cja-projects-20.png)

프로젝트를 저장하는 것을 잊지 마십시오!


#### 사람들에게 제공

또한 어떤 오퍼가 앱 사용자에게 어떤 숫자로 표시되었는지 보여 주는 보고서를 만들 수 있습니다.

1. 선택 ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) 다음 범위 내 **[!UICONTROL 오퍼]** 패널 및 ![자유 형식 테이블](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Table_18_N.svg)팝업에서 새 자유 형식 테이블을 추가합니다.

1. 이름 바꾸기 **[!UICONTROL 자유 형식 테이블 (2)]** 끝 `People`.

1. 을(를) 끌어다 놓습니다. **[!UICONTROL 사람]** 다음에 대한 지표 [!UICONTROL _드롭 a **지표**여기(또는 기타 구성 요소)_)].

1. 을(를) 끌어다 놓습니다. **[!UICONTROL 활동 이름]** 다음에 있음 **[!UICONTROL 일]** 열 - 차원을 대체합니다.

1. 행을 마우스 오른쪽 버튼으로 클릭하고, 에서 정의한 오퍼 결정 중 하나 이상을 식별합니다. [의사 결정 관리를 사용하여 오퍼 만들기 및 표시](journey-optimizer-offers.md) 레슨. 예를 들어, **[!UICONTROL Luma - 모바일 앱 결정]**.

1. 컨텍스트 메뉴에서 을(를) 선택합니다 **[!UICONTROL 분류]** > **[!UICONTROL Dimension]** > **[!UICONTROL 오퍼 이름]**. 이 옵션을 선택하면 활동 이름 차원이 오퍼 이름으로 분류됩니다.
   ![CJA 프로젝트 20b](assets/cja-projects-20b.png)

이제 앱 사용자에게 선택한 기간 동안 이 오퍼 결정에 대한 개별 오퍼가 표시되는 보고서가 있습니다.
![CJA 프로젝트 21](assets/cja-projects-21.png)

프로젝트를 저장하는 것을 잊지 마십시오!


### 방문 횟수 저장

마지막으로 스토어 방문에 대해 보고하려 합니다.

1. 선택 ![추가](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) 을 클릭하여 새 패널을 만듭니다.

1. 이름 바꾸기 **[!UICONTROL 패널]** 끝 `Store Visits`.

1. 적절한 기간을 선택해야 합니다.

1. 선택 ![자유 형식 테이블](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Table_18_N.svg) 자유 형식 테이블 : 새 자유 형식 테이블을 만듭니다.

1. 이름 바꾸기 **[!UICONTROL 자유 형식 테이블]** 끝 `Store Entries / Exits Across Cities`.

1. 을(를) 끌어다 놓습니다. **[!UICONTROL 위치 이벤트]** 다음에 대한 지표 [!UICONTROL _드롭 a **지표**여기(또는 기타 구성 요소)_)]. 이제 보고서에 앱에서 발생한 모든 위치 이벤트의 일일 개요가 표시됩니다. 이 차원을 의 일부로 구체적으로 구성한 방법을 기억하십시오. [데이터 보기](#create-a-data-view).

1. 을(를) 끌어다 놓습니다. **[!UICONTROL 도시]** 다음에 대한 차원 **[!UICONTROL 일]** 열 머리글로 차원을 바꿉니다. 이제 보고서에 위치 이벤트의 도시가 표시됩니다.

1. 연관된 도시가 없는 지리적 위치 이벤트를 제거하려면 을 선택합니다. ![필터](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Filter_18_N.svg), 및 **[!UICONTROL 검색]** 팝업, 끄기 **[!UICONTROL 값 없음 포함]**&#x200B;을 선택한 다음 을 선택합니다. **[!UICONTROL 적용]**.

   ![CJA 프로젝트 22](assets/cja-projects-22.png)

   이 작업은 **[!UICONTROL 값 없음]** 보고서에서 행이 표시됩니다.

1. 표에서 모든 행을 선택하고 마우스 오른쪽 단추를 클릭한 다음 컨텍스트 메뉴에서 분류 > Dimension > 이벤트 유형 을 선택합니다.

이제 매장 위치(에서 이러한 위치를 정의함) 근처에 들어오고 나가는 사용자를 보여주는 보고서가 제공됩니다. [위치](places.md) 단원).

![CJA 프로젝트 23](assets/cja-projects-23.png)

실제로 매장을 방문하는 사람들에 대해 보고하려는 경우, 비콘을 사용할 수 있습니다. 하지만 지리적 위치 데이터에 대한 보고의 개념을 포착했으면 합니다.

## 다음 단계

이제 Customer Journey Analytics을 사용하여 모바일 앱 사용, 상호 작용 등을 보고하고 시각화하는 방법에 대한 기본 지식이 있어야 합니다.

>[!SUCCESS]
>
>
>Adobe Experience Platform Mobile SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하려는 경우 또는 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

다음: **[결론 및 다음 단계](conclusion.md)**
