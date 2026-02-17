---
title: 오케스트레이션된 캠페인 만들기
description: 오케스트레이션된 캠페인 만들기
kt: 5342
doc-type: tutorial
exl-id: f3ca3230-db30-4e41-91f1-9324b12211a6
source-git-commit: 53be5cf34db144e346f9810359b583072743382f
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 2%

---

# 3.8.2 오케스트레이션된 캠페인 만들기

## 3.8.2.1 오케스트레이션된 캠페인 만들기

**캠페인**(으)로 이동합니다. **캠페인 만들기**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc1.png)

**오케스트레이션 - 마케팅**&#x200B;을 선택하고 **확인**&#x200B;을 클릭합니다.

![AJO OC](./images/ajooc2.png)

캠페인 이름 `--aepUserLdap-- - CitiSignal Family Account Optimization Campaign`을(를) 입력하고 **저장**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc3.png)

그럼 이걸 보셔야죠 **+** 아이콘을 클릭합니다.

![AJO OC](./images/ajooc4.png)

**포크**&#x200B;를 선택합니다.

![AJO OC](./images/ajooc5.png)

### 대상 1 작성

**+** 아이콘을 클릭한 다음 **대상자 빌드**&#x200B;를 선택합니다.

![AJO OC](./images/ajooc6.png)

**타겟팅 차원**&#x200B;에 대한 폴더를 열려면 클릭하세요.

![AJO OC](./images/ajooc7.png)

**`--aepUserLdap--_citisignal_recipients`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc8.png)

**대상 만들기**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc9.png)

**조건 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc10.png)

**recipient_type**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc11.png)

**`account_holder`**&#x200B;값&#x200B;**필드에**&#x200B;을(를) 입력하고 **계산**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc12.png)

**프로필 대상**&#x200B;에 대한 숫자가 표시됩니다. 표시된 대로 회색 영역 내 아무 곳이나 클릭합니다.

![AJO OC](./images/ajooc13.png)

**조건 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc14.png)

**`citisignal_accounts`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc15.png)

**`account_status`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc16.png)

**`active`**&#x200B;값&#x200B;**필드에**&#x200B;을(를) 입력하십시오. 그런 다음 표시된 대로 회색 영역 내 아무 곳이나 클릭합니다.

![AJO OC](./images/ajooc17.png)

**조건 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc18.png)

**`citisignal_mobile_subscriptions`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc19.png)

**`subscription_id`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc20.png)

**집계 데이터**&#x200B;에 대해 전환기를 사용하도록 설정하십시오. 그런 다음 다음을 선택합니다.

- **집계 함수**: **개수**
- **연산자**: **다음보다 크거나 같음**
- **값**: **1**

**확인**&#x200B;을 클릭합니다.

![AJO OC](./images/ajooc21.png)

그럼 이걸 보셔야죠 **확인**&#x200B;을 클릭합니다.

![AJO OC](./images/ajooc22.png)

### 대상 2 작성

다른 경로의 다음 노드에서 **+** 아이콘을 클릭합니다.

![AJO OC](./images/ajooc23.png)

**대상자 빌드**&#x200B;를 선택합니다.

![AJO OC](./images/ajooc24.png)

**타겟팅 차원**&#x200B;에 대한 폴더를 열려면 클릭하세요.

![AJO OC](./images/ajooc25.png)

**`--aepUserLdap--_mobile_subscriptions`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc26.png)

**대상 만들기**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc27.png)

**조건 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc28.png)

**subscription_status**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc29.png)

**`active`**&#x200B;값&#x200B;**필드에**&#x200B;을(를) 입력하십시오. 그런 다음 **조건 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc30.png)

**`is_upgrade_eligible`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc31.png)

**값**&#x200B;을(를) **true**(으)로 설정

![AJO OC](./images/ajooc32.png)

이 대상자에 적합한 예상 프로필을 보려면 **계산**&#x200B;을 클릭하세요. 그런 다음 **확인**&#x200B;을 클릭합니다

![AJO OC](./images/ajooc33.png)

### 분할

**+** 아이콘을 클릭한 다음 **분할**&#x200B;을 선택합니다.

![AJO OC](./images/ajooc34.png)

필드 **Label**&#x200B;을(를) **90/10 처리 대 제어**(으)로 변경하십시오. 개체 **하위 집합**&#x200B;을(를) 열려면 클릭하세요.

![AJO OC](./images/ajooc35.png)

**제한 사용**&#x200B;에 대해 전환기를 사용하도록 설정하고 **제한 크기**&#x200B;을(를) **10 최신**(으)로 설정합니다.

![AJO OC](./images/ajooc36.png)

**세그먼트 추가**&#x200B;를 클릭하면 **결과** 개체가 추가됩니다.

**저장**&#x200B;을 클릭합니다.

![AJO OC](./images/ajooc37.png)

### 대상자 저장

**+** 아이콘을 클릭한 다음 **대상자 저장**&#x200B;을 선택합니다.

![AJO OC](./images/ajooc38.png)

필드 **대상 레이블**&#x200B;을(를) **`--aepUserLdap-- - Control Group`**(으)로 설정합니다. **대상 매핑 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc39.png)

**타깃팅 차원**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc40.png)

**`account_id`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc41.png)

### 데이터 보강: 인터넷 구독

**+** 아이콘을 클릭합니다.

![AJO OC](./images/ajooc42.png)

**데이터 보강**&#x200B;을 선택합니다.

![AJO OC](./images/ajooc43.png)

그럼 이걸 보셔야죠 **보강 데이터 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc44.png)

**`Targeting dimension`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc44a.png)

**`citisignal_accounts`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc45.png)

**`citisignal_internet_subscriptions`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc45a.png)

**`account_id`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc46.png)

그럼 이걸 보셔야죠 **특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc47.png)

**`subscription_status`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc48.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc49.png)

**`connection_type`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc50.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc51.png)

**`service_city`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc52.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc53.png)

**`avg_dowload_usage_gb`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc54.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc55.png)

**`data_cap_gb`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc56.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc57.png)

**`advertised_speed_mbps`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc58.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc59.png)

**`monthly_recurring_charge`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc60.png)

**저장**&#x200B;을 클릭합니다.

![AJO OC](./images/ajooc61.png)

위로 스크롤하여 필드 **레이블**&#x200B;을(를) `Enrichment: Internet Subscription`(으)로 변경합니다.

![AJO OC](./images/ajooc61a.png)

### 데이터 보강: 모바일 장치 구독

다음 노드에서 **+** 아이콘을 클릭하고 **데이터 보강**&#x200B;을 선택합니다.

![AJO OC](./images/ajooc62.png)

필드 **Label**&#x200B;을(를) `Enrichment: Mobile Devices Subscription`(으)로 변경한 다음 **데이터 보강 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc63.png)

**타깃팅 차원**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc64.png)

**`citisignal_mobile_subscriptions`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc65.png)

**`account_id`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc66.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc67.png)

**`subscription_id`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc68.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc69.png)

**`phone_number`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc70.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc71.png)

**`renewal_eligibility_date`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc72.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc73.png)

**`line_user_recipient_id`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc74.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc75.png)

**`is_upgrade_eligible`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc76.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc77.png)

**`current_device_id`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc78.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc79.png)

**`contract_start_date`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc80.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc81.png)

**`citisignal_equipment_subscriptions`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc82.png)

**`model`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc83.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc86.png)

**`citisignal_equipment_subscriptions`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc87.png)

**`manufacturer`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc88.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc89.png)

**`citisignal_equipment_subscriptions`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc90.png)

**`device_age_months`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc91.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc92.png)

**`citisignal_equipment_subscriptions`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc93.png)

**`is_upgrade_eligible`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc94.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc95.png)

**`citisignal_equipment_subscriptions`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc96.png)

**`recommended_upgrade_product_id`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc97.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc98.png)

**`citisignal_equipment_subscriptions`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc99.png)

**`monthly_payment`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc100.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc101.png)

**`citisignal_equipment_subscriptions`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc102.png)

**정렬 사용**&#x200B;에 대해 스위치를 사용하도록 설정하십시오. **편집** 아이콘을 클릭합니다.

![AJO OC](./images/ajooc103.png)

**`phone_number`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc104.png)

그럼 이걸 드셔보세요

![AJO OC](./images/ajooc105.png)




그럼 이걸 드셔보세요 **저장**&#x200B;을 클릭합니다.

![AJO OC](./images/ajooc80a.png)














![AJO OC](./images/ajooc103.png)


## 다음 단계

[Adobe Journey Optimizer: 오케스트레이션된 캠페인](./ajocampaigns.md){target="_blank"}(으)로 돌아가기

[모든 모듈](./../../../../overview.md){target="_blank"}(으)로 돌아가기
