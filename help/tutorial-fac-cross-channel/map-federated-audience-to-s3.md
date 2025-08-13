---
title: S3에 페더레이션 대상 매핑
seo-title: Map a federated audience to S3 | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: S3에 페더레이션 대상 매핑
description: 이 시각적 연습에서는 개인화된 오프라인 경험을 지원하기 위해 페더레이션 대상을 다운스트림 Real-Time CDP 대상에 매핑합니다.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
hide: true
exl-id: a47b8f7b-7bd0-43a0-bc58-8b57d331b444
source-git-commit: a3c8d8b03472d01f491bf787ed647a696d3a5524
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# Federated Audience를 S3에 매핑하여 데이터 강화를 위한 대상 속성 활용

데이터 웨어하우스의 대상 속성을 활용하여 RTCDP 대상을 사용하는 다운스트림 활성화 워크플로에서 대상의 경험을 강화할 수 있습니다. SecurFinancial의 경우 이러한 페더레이션 속성을 사용하여 오프라인에서 고객 대상의 개인화 경험을 향상시킬 수 있습니다. 아래에서 페더레이션 대상은 사전 구성된 Amazon S3 대상에 매핑됩니다.

## 단계

1. **대상** 포털로 이동합니다.

2. 사전 구성된 Amazon S3 대상 옆에 있는 **3점 메뉴** 단추를 클릭한 다음 **대상 활성화**&#x200B;를 클릭합니다.

   ![활성화-대상](assets/activate-audiences.png)

3. **S3 대상**&#x200B;을 선택한 후 **다음**&#x200B;을 클릭합니다.

   ![select-s3-destination](assets/select-s3-destination.png)

4. 적절한 대상자를 선택합니다. 이 예제에서는 **SecureFinancial 고객 - 대출 없음, 양호한 신용**&#x200B;을(를) 대상으로 지정합니다.

   ![select-s3-audience](assets/select-s3-audience.png)

5. **예약** 섹션에서 기본 설정을 사용하고 **다음**&#x200B;을 클릭합니다.

6. **매핑** 단계에서 중복 제거 키를 선택합니다. 이 예제에서는 `xdm: personalEmail.address`이(가) 포함되어 **중복 제거 키**(으)로 선택됩니다. **다음**&#x200B;을 클릭합니다.

   ![중복 제거 키](assets/deduplication-key.png)

7. 매핑 단계에서 통합 대상 컴포지션의 대상 필드 매핑을 기반으로 데이터 보강 속성을 선택합니다. 미리 선택된 특성을 보려면 **연필(편집)** 아이콘을 클릭하십시오.

   ![edit-attributes](assets/edit-attributes.png)

   ![final-attributes](assets/final-attribution.png)

8. 대상자 매핑을 검토하고 **완료**&#x200B;를 누르십시오.

>[**요약**]
>
> 대상을 성공적으로 빌드하고 S3 대상에 쉽게 활성화했습니다. 플랫폼의 사용자 친화적인 인터페이스를 통해 마케팅 팀은 신속하게 대상을 구축하고 활성화할 수 있으므로 가치 창출 시간이 단축됩니다. 이 방법을 사용하는 고객은 두 달 만에 첫 번째 사용 사례를 활용하게 됩니다.

[여정 빌드](build-journey-federated-audience.md)(으)로 이동할 준비가 되었습니다.
