---
title: 기초 - 데이터 수집 - 데이터 세트 구성
description: 기초 - 데이터 수집 - 데이터 세트 구성
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 5afd987b-ccf8-414d-98aa-a485d6130c2e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 7%

---

# 2.3 데이터 세트 구성

이 연습에서는 프로필 정보 및 고객 동작을 캡처하고 저장하도록 필요한 데이터 세트를 구성합니다. 여기에서 만드는 모든 데이터 세트는 이전 단계에서 빌드한 스키마 중 하나를 사용합니다.

## Story

질문에 대한 답변을 정의한 후 **이 고객은 누구입니까?** 및 **이 고객은 무엇을 합니까?** 유사하게, 이제 Adobe Experience Platform으로 전송된 데이터를 받고 유효성 검사를 위해 해당 정보를 사용하는 버킷을 만들어야 합니다.

## 2.3.1 - 데이터 세트 만들기

이제 2개의 데이터 세트를 만들어야 합니다.

- 1개의 데이터 세트에 응답하는 정보를 캡처합니다 **이 고객은 누구입니까?** - 질문.
- 1개의 데이터 세트에 응답하는 정보를 캡처합니다 **이 고객은 무엇을 합니까?** - 질문.

다음 URL로 이동하여 Adobe Experience Platform에 로그인합니다. [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

로그인하면 Adobe Experience Platform 홈 페이지가 표시됩니다.

![데이터 수집](./images/home.png)

계속하기 전에 **[!UICONTROL 샌드박스]**. 선택할 샌드박스의 이름은 다음과 같습니다 ``--module2sandbox--``. 이 작업은 텍스트를 클릭하여 수행할 수 있습니다 **[!UICONTROL 프로덕션 제품]** 화면 상단에 있는 파란색 줄에 표시됩니다. 적절한 [!UICONTROL 샌드박스]이렇게 하면 화면 변경 사항이 표시되고 이제 전용 화면에 표시됩니다 [!UICONTROL 샌드박스].

![데이터 수집](./images/sb1.png)

Adobe Experience Platform에서 **[!UICONTROL 데이터 세트]** 을 클릭합니다.  그러면 다음 내용이 표시됩니다.

![데이터 수집](./images/menudatasets.png)

먼저 데이터 세트를 만들어 웹 사이트 등록 정보를 캡처합니다.

새 데이터 세트를 만들어야 합니다. 새 데이터 세트를 만들려면 버튼을 클릭합니다 **[!UICONTROL + 데이터 집합 만들기]**.

![데이터 수집](./images/createdataset.png)

을 클릭한 후 **[!UICONTROL + 데이터 집합 만들기]** 버튼, 다음 화면이 표시됩니다.

![데이터 수집](./images/datasetsetup.png)

이전 단계에서 정의한 스키마에서 데이터 세트를 정의해야 합니다. 을(를) 클릭합니다. **[!UICONTROL 스키마에서 데이터 집합 만들기]** - 선택 사항입니다.

![데이터 수집](./images/datasetfromschema.png)

다음 화면에서 1에서 만든 스키마를 선택해야 합니다. `--demoProfileLdap-- - Demo System - Profile Schema for Website`.

![데이터 수집](./images/schemaselection.png)

스키마를 선택한 후 **[!UICONTROL 다음]** 계속하십시오.

![데이터 수집](./images/next.png)

데이터 세트에 이름을 지정하겠습니다.

데이터 세트 이름으로 다음 항목을 사용합니다.

`--demoProfileLdap-- - Demo System - Profile Dataset for Website`

예를 들어 ldap의 경우 **[!UICONTROL vangeluw]**, 스키마 이름이어야 합니다.

**[!UICONTROL vangeluw - 데모 시스템 - 웹 사이트용 프로필 데이터 세트]**

그러면 다음과 같은 이점이 있습니다.

![데이터 수집](./images/datasetname.png)

클릭 **[!UICONTROL 완료]** 데이터 세트 구성을 완료합니다.

![데이터 수집](./images/finish.png)

이제 다음을 확인할 수 있습니다.

![데이터 수집](./images/dsoverview1.png)

로 돌아갑니다. [!UICONTROL 데이터 세트] 개요. 이제 만든 데이터 세트가 개요에 표시됩니다.

![데이터 수집](./images/dsoverview2.png)

그런 다음 웹 사이트 상호 작용을 캡처하도록 두 번째 데이터 세트를 구성합니다.

새 데이터 세트를 만들어야 합니다. 새 데이터 세트를 만들려면 버튼을 클릭합니다 **[!UICONTROL + 데이터 집합 만들기]**.

![데이터 수집](./images/createdataset.png)

을 클릭한 후 **[!UICONTROL + 데이터 집합 만들기]** 버튼, 다음 화면이 표시됩니다.

![데이터 수집](./images/datasetsetup.png)

이전 단계에서 정의한 스키마에서 데이터 세트를 정의해야 합니다. 을(를) 클릭합니다. **[!UICONTROL 스키마에서 데이터 집합 만들기]** - 선택 사항입니다.

![데이터 수집](./images/datasetfromschema.png)

다음 화면에서 2.2에서 만든 스키마를 선택해야 합니다. `--demoProfileLdap-- - Demo System - Event Schema for Website`.

![데이터 수집](./images/schemaselectionee.png)

스키마를 선택한 후 **[!UICONTROL 다음]** 계속하십시오.

![데이터 수집](./images/next.png)

데이터 세트에 이름을 지정하겠습니다.

데이터 세트 이름으로 다음 항목을 사용합니다.

`--demoProfileLdap-- - Demo System - Event Dataset for Website`

예를 들어 ldap의 경우 **[!UICONTROL vangeluw]**, 스키마 이름이어야 합니다.

**[!UICONTROL vangeluw - 데모 시스템 - 웹 사이트에 대한 이벤트 데이터 세트]**

그러면 다음과 같은 이점이 있습니다.

![데이터 수집](./images/datasetnameee.png)

클릭 **[!UICONTROL 완료]** 데이터 세트 구성을 완료합니다.

![데이터 수집](./images/finish.png)

그러면 다음 내용이 표시됩니다.

![데이터 수집](./images/finish1.png)

로 돌아갑니다. [!UICONTROL 데이터 세트] 개요 화면.

![데이터 수집](./images/datasetsoverview.png)

이제 데이터 세트를 Adobe Experience Platform의 실시간 고객 프로필에 포함하도록 활성화해야 합니다.

데이터 세트를 엽니다. `--demoProfileLdap--` - 데모 시스템 - 웹 사이트용 프로필 데이터 세트를 클릭하여 클릭합니다.

을(를) 찾습니다 [!UICONTROL 프로필] 화면의 오른쪽에서 아이콘을 전환합니다.

![데이터 수집](./images/ds1.png)

을(를) 클릭합니다. [!UICONTROL 프로필] 에 대해 이 데이터 세트를 사용하도록 설정 전환 [!UICONTROL 프로필].

![데이터 수집](./images/ds2.png)

을(를) 클릭합니다. **[!UICONTROL 활성화]**.

![데이터 수집](./images/ds3.png)

이제 데이터 세트에 대해 를 사용할 수 있습니다 [!UICONTROL 프로필].

데이터 세트 개요로 돌아가서 데이터 세트를 엽니다 `--demoProfileLdap-- - Demo System - Event Dataset` 을 클릭하여 웹 사이트를 참조하십시오.

을(를) 찾습니다 [!UICONTROL 프로필] 화면의 오른쪽에서 아이콘을 전환합니다.

![데이터 수집](./images/ds4.png)

을(를) 클릭합니다. [!UICONTROL 프로필] 활성화 [!UICONTROL 프로필].

![데이터 수집](./images/ds2.png)

클릭 **[!UICONTROL 활성화]**.

![데이터 수집](./images/ds5.png)

이제 데이터 세트에 대해 를 사용할 수 있습니다 [!UICONTROL 프로필].

다음 단계: [2.4 오프라인 소스에서 데이터 수집](./ex4.md)

[모듈 2로 돌아가기](./data-ingestion.md)

[모든 모듈로 돌아가기](../../overview.md)
