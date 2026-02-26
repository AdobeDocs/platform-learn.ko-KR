---
title: 오케스트레이션된 캠페인 만들기
description: 오케스트레이션된 캠페인 만들기
kt: 5342
doc-type: tutorial
exl-id: f3ca3230-db30-4e41-91f1-9324b12211a6
source-git-commit: 72aee2daa489f00dfc753e6986f0cab2271c6a7f
workflow-type: tm+mt
source-wordcount: '1112'
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

**프로필 매핑 필드**&#x200B;을(를) **`--aepUserLdap--_citisignal_recipients - account_id`**(으)로 설정합니다.

![AJO OC](./images/ajooc41a.png)

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

**`avg_bandwidth_usage_gb`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

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

**`citisignal_accounts`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc65.png)

**`citisignal_mobile_subscriptions`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc65a.png)

**`phone_number`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc66.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc67.png)

**`citisignal_equipment_subscriptions`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc68.png)

**`model`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc68a.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc69.png)

**`citisignal_equipment_subscriptions`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc69a.png)

**`recommended_device_model`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc70.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc71.png)

**`citisignal_equipment_subscriptions`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc71a.png)

**`is_upgrade_eligible`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc72.png)

이제 테스트 실행을 통해 진행 상황을 테스트하고 캠페인에서 사용할 수 있는 데이터를 확인할 수 있습니다.

변경 내용을 저장한 다음 **시작**&#x200B;을 클릭합니다.

![AJO OC](./images/ajooctest1.png)

시간이 좀 지나면 이걸 볼 수 있을 거야. **결과 미리 보기**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooctest2.png)

그러면 이와 비슷한 것을 볼 수 있을 겁니다. Click **Close**.

![AJO OC](./images/ajooctest3.png)

**데이터 보강: 모바일 장치 구독** 노드로 돌아갑니다.

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc73.png)

**`account_id`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc74.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc75.png)

**`subscription_id`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc76.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc77.png)

**`renewal_eligibility_date`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc78.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc79.png)

**`line_user_recipient_id`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc80.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc81.png)

**`current_device_id`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc82.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc86.png)

**`contract_start_date`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc87.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc89.png)

**`citisignal_equipment_subscriptions`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc90.png)

**`manufacturer`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc91.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc92.png)

**`citisignal_equipment_subscriptions`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc93.png)

**`device_age_months`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc94.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc95.png)

**`citisignal_equipment_subscriptions`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc96.png)

**`trade_in_value`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc97.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc98.png)

**`citisignal_equipment_subscriptions`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc99.png)

**`monthly_payment`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc100.png)

### 데이터 보강: 모바일 장치 구독

그럼 이걸 드셔보세요 **저장**&#x200B;을 클릭합니다. 그런 다음 **+** 아이콘을 클릭하여 새 노드를 추가하고 **데이터 보강**&#x200B;을(를) 선택합니다.

![AJO OC](./images/ajooc101.png)

그럼 이걸 보셔야죠 **보강 데이터 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc102.png)

**타깃팅 차원**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc103.png)

**`citisignal_offer_eligibility`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc104.png)

**`citisignal_offers`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc105.png)

**`offer_name`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc106.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc107.png)

**`citisignal_offers`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc108.png)

**`offer_code`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc109.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc110.png)

**`citisignal_offers`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc111.png)

**`offer_description`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc112.png)

**특성 추가**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc110.png)

**`citisignal_offers`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc113.png)

**`offer_description`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc114.png)

**정렬 사용**&#x200B;을 켭니다.

![AJO OC](./images/ajooc115.png)

**`citisignal_offers`**(으)로 드릴다운합니다.

![AJO OC](./images/ajooc116.png)

**`offer_priority`**&#x200B;을(를) 선택하고 **확인**&#x200B;을(를) 클릭합니다.

![AJO OC](./images/ajooc117.png)

이제 캠페인을 테스트할 수 있습니다. **시작**&#x200B;을 클릭합니다.

![AJO OC](./images/ajooc118.png)

시간이 좀 지나면 이걸 볼 수 있을 거야. **결과**&#x200B;를 클릭한 다음 **결과 미리 보기**&#x200B;를 선택합니다.

![AJO OC](./images/ajooc120.png)

그러면 이와 비슷한 것을 볼 수 있을 겁니다.

![AJO OC](./images/ajooc121.png)

### 이메일 활동

**+** 아이콘을 클릭한 다음 **전자 메일**&#x200B;을(를) 선택합니다.

![AJO OC](./images/ajooc122.png)

**전자 메일 편집**&#x200B;을 클릭합니다.

![AJO OC](./images/ajooc123.png)

**작업**(으)로 이동합니다.

![AJO OC](./images/ajooc124.png)

이전에 만든 **전자 메일 채널 구성**&#x200B;을 선택한 다음 **콘텐츠 편집**&#x200B;을 클릭합니다.

![AJO OC](./images/ajooc125.png)

**제목 줄**&#x200B;에 대해 다음을 붙여 넣으십시오.

`{{target.--aepUserLdap--_citisignal_recipients.first_name}}, Your CitiSignal Family Account Summary`

**전자 메일 본문 편집**&#x200B;을 클릭합니다.

![AJO OC](./images/ajooc126.png)

데스크톱에 [family_account_review.zip](./assets/family_account_review.zip) 파일을 다운로드합니다.

![AJO OC](./images/ajooc127.png)

**HTML 가져오기**&#x200B;를 클릭합니다.

![AJO OC](./images/ajooc128.png)

을(를) 클릭하여 파일을 선택합니다.

![AJO OC](./images/ajooc129.png)

**`family_account_review.zip`** 파일을 선택하십시오.

![AJO OC](./images/ajooc130.png)

**다음**&#x200B;을 클릭합니다.

![AJO OC](./images/ajooc131.png)

그럼 이걸 보셔야죠

![AJO OC](./images/ajooc132.png)

## 다음 단계

[Adobe Journey Optimizer: 오케스트레이션된 캠페인](./ajocampaigns.md){target="_blank"}(으)로 돌아가기

[모든 모듈](./../../../../overview.md){target="_blank"}(으)로 돌아가기
