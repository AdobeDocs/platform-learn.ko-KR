---
title: 기초 - 데이터 수집 - 오프라인 소스에서 데이터 수집
description: 기초 - 데이터 수집 - 오프라인 소스에서 데이터 수집
kt: 5342
doc-type: tutorial
exl-id: a4909a47-0652-453b-ae65-ba4c261f087c
source-git-commit: 8bdcd03bd38a6da98b82439ad86482cad5f4e684
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 5%

---

# 1.2.4 오프라인 소스에서 데이터 수집

이 연습에서는 플랫폼에서 CRM 데이터와 같은 외부 데이터를 온보딩하는 것을 목표로 합니다.

## 학습 목표

- 테스트 데이터를 생성하는 방법 알아보기
- CSV 수집 방법 알아보기
- 워크플로우를 통해 데이터 수집에 웹 UI를 사용하는 방법을 알아봅니다
- Experience Platform의 데이터 거버넌스 기능 이해

## 리소스

- 모카루: [https://www.mockaroo.com/](https://www.mockaroo.com/)
- Adobe Experience Platform: [https://experience.adobe.com/platform/](https://experience.adobe.com/platform/)

## 작업

- 데모 데이터를 사용하여 CSV 파일을 만듭니다. 사용 가능한 워크플로우를 사용하여 Adobe Experience Platform에서 CSV 파일을 수집합니다.
- Adobe Experience Platform의 데이터 거버넌스 옵션 이해

## 데이터 생성기 도구를 사용하여 CRM 데이터 세트 만들기

이 연습에서는 1000개의 샘플 CRM 데이터 줄이 필요합니다.

[https://www.mockaroo.com/12674210](https://www.mockaroo.com/12674210)(으)로 이동하여 Mockaroo 템플릿을 엽니다.

![데이터 수집](./images/mockaroo.png)

템플릿에서 다음 필드를 확인할 수 있습니다.

- ID
- first_name
- last_name
- 이메일
- 성별
- 생일
- home_latitude
- home_longitude
- country_code
- 도시
- 국가

이러한 모든 필드는 Platform과 호환되는 데이터를 생성하도록 정의되었습니다.

CSV 파일을 생성하려면 **[!UICONTROL 데이터 생성]** 단추를 클릭하십시오. 그러면 1000줄의 데모 데이터가 포함된 CSV 파일이 만들어지고 다운로드됩니다.

![데이터 수집](./images/dd.png)

CSV 파일을 열어 콘텐츠를 시각화합니다.

![데이터 수집](./images/excel.png)

CSV 파일이 준비되면 AEP에서 수집을 진행할 수 있습니다.

### 데이터 세트 확인

[Adobe Experience Platform](https://experience.adobe.com/platform)을 열고 **[!UICONTROL 데이터 세트]**(으)로 이동합니다.

계속하려면 **[!UICONTROL 샌드박스]**&#x200B;를 선택해야 합니다. 선택할 샌드박스 이름이 ``--aepSandboxName--``입니다.

![데이터 수집](./images/sb1.png)

Adobe Experience Platform의 화면 왼쪽에 있는 메뉴에서 **[!UICONTROL 데이터 세트]**&#x200B;를 클릭합니다.

![데이터 수집](./images/menudatasetssb.png)

공유 데이터 세트를 사용합니다. 공유 데이터 세트는 이미 만들어졌으며 **[!UICONTROL 데모 시스템 - CRM용 프로필 데이터 세트(전역 v1.1)]**&#x200B;라고 합니다. 클릭하여 엽니다.

![데이터 수집](./images/emeacrmoverview.png)


개요 화면에서는 세 가지 주요 정보를 볼 수 있습니다.

![데이터 수집](./images/dashboard.png)

먼저 [!UICONTROL 데이터 집합 활동] 대시보드에는 데이터 집합에 있는 총 CRM 레코드 수와 수집된 일괄 처리 및 상태가 표시됩니다

![데이터 수집](./images/batchids.png)

둘째, 페이지에서 아래로 스크롤하여 데이터 일괄 처리가 언제 수집되었는지, 얼마나 많은 레코드가 온보딩되었는지 및 일괄 처리가 정상적으로 온보딩되었는지 여부를 확인할 수 있습니다. **[!UICONTROL 배치 ID]**&#x200B;은(는) 특정 배치 작업의 식별자입니다. **[!UICONTROL 배치 ID]**&#x200B;은(는) 특정 배치가 온보딩되지 않은 이유를 해결하는 데 사용할 수 있으므로 중요합니다.

마지막으로 [!UICONTROL 데이터 세트] 정보 탭에는 [!UICONTROL 데이터 세트 ID](문제 해결 관점에서 중요)와 같은 중요한 정보, 데이터 세트의 이름 및 데이터 세트가 프로필에 대해 활성화되었는지 여부가 표시됩니다.

![데이터 수집](./images/datasetsettings.png)

여기에서 가장 중요한 설정은 데이터 세트와 스키마 간의 링크입니다. 스키마는 수집할 수 있는 데이터와 해당 데이터의 형태를 정의합니다.

이 경우 **[!UICONTROL 프로필]**&#x200B;의 클래스에 대해 매핑되고 필드 그룹이라고도 하는 확장을 구현한 **[!UICONTROL 데모 시스템 - CRM용 프로필 스키마(전역 v1.1)]**&#x200B;를 사용합니다.

![데이터 수집](./images/ds_schemalink.png)

스키마 이름을 클릭하면 이 스키마에 대해 활성화된 모든 필드를 볼 수 있는 [!UICONTROL 스키마] 개요로 이동합니다.

![데이터 수집](./images/schemads.png)

모든 스키마에는 사용자 정의 기본 설명자가 정의되어 있어야 합니다. CRM 데이터 세트의 경우 스키마가 필드 **[!UICONTROL crmId]**&#x200B;을(를) 기본 식별자로 정의했습니다. 스키마를 만들어 [!UICONTROL 실시간 고객 프로필]에 연결하려면 기본 설명자를 참조하는 사용자 지정 [!UICONTROL 필드 그룹]을 정의해야 합니다.

기본 ID가 **[!UICONTROL 데모 시스템 - CRMID]**&#x200B;의 [!UICONTROL 네임스페이스]에 연결된 `--aepTenantId--.identification.core.crmId`에 있습니다.

![데이터 수집](./images/schema_descriptor.png)



[!UICONTROL 실시간 고객 프로필]에서 사용해야 하는 모든 스키마 및 데이터 세트에는 하나의 [!UICONTROL 기본 식별자]가 있어야 합니다. 이 [!UICONTROL 기본 식별자]은(는) 해당 데이터 집합에서 고객의 브랜드별 식별자 사용자입니다. CRM 데이터 세트의 경우 이메일 주소 또는 CRM ID이고, 콜 센터 데이터 세트의 경우 고객의 모바일 번호일 수 있습니다.

모든 데이터 세트에 대해 별도의 특정 스키마를 만들고 브랜드에서 사용하는 현재 솔루션이 작동하는 방식과 일치하도록 모든 데이터 세트에 대한 설명자를 구체적으로 설정하는 것이 좋습니다.

### 워크플로우를 사용하여 CSV 파일을 XDM 스키마에 매핑

이 연습의 목표는 AEP에서 CRM 데이터를 온보딩하는 것입니다. Platform에서 수집되는 모든 데이터는 특정 XDM 스키마에 대해 매핑되어야 합니다. 현재 보유한 항목은 한쪽에 1000개의 줄이 있는 CSV 데이터 세트와 다른 쪽에 있는 스키마에 연결된 데이터 세트입니다. 해당 CSV 파일을 해당 데이터 세트에 로드하려면 매핑이 수행되어야 합니다. 이 매핑 연습을 용이하게 하기 위해 Adobe Experience Platform에서 **[!UICONTROL 워크플로]**&#x200B;를 사용할 수 있습니다.

**[!UICONTROL XDM 스키마에 CSV 매핑]**&#x200B;을 클릭한 다음 **[!UICONTROL 시작]**&#x200B;을 클릭하여 프로세스를 시작합니다.

![데이터 수집](./images/workflows.png)

다음 화면에서는 파일을 수집할 데이터 세트를 선택해야 합니다. 이미 존재하는 데이터 세트를 선택하거나 새 데이터 세트를 만들 수 있습니다. 이 연습에서는 기존 설정을 다시 사용합니다. 아래에 표시된 대로 **[!UICONTROL 데모 시스템 - CRM용 프로필 데이터 세트(전역 v1.1)]**&#x200B;를 선택하고 다른 설정은 기본값으로 설정해 두십시오.

**다음**&#x200B;을 클릭합니다.

![데이터 수집](./images/datasetselection.png)

CSV 파일을 드래그 앤 드롭하거나 **[!UICONTROL 파일 선택]**&#x200B;을 클릭하고 컴퓨터에서 바탕 화면으로 이동한 다음 CSV 파일을 선택하십시오.

![데이터 수집](./images/dragdrop.png)

CSV 파일을 선택하면 즉시 업로드되고 몇 초 안에 파일의 미리보기가 표시됩니다.

**다음**&#x200B;을 클릭합니다.

![데이터 수집](./images/previewcsv.png)

이제 CSV 파일의 열 헤더를 **[!UICONTROL 데모 시스템 - CRM용 프로필 데이터 세트]**&#x200B;의 XDM 속성과 매핑해야 합니다.

Adobe Experience Platform은 [!UICONTROL Source 특성]을(를) [!UICONTROL Target 스키마 필드]와(과) 연결하여 이미 몇 가지 제안을 했습니다.

![데이터 수집](./images/mapschema.png)

[!UICONTROL 스키마 매핑]에 대해 Adobe Experience Platform에서 이미 필드를 함께 연결하려고 했습니다. 그러나 모든 매핑 제안이 올바른 것은 아닙니다. 이제 **대상 필드**&#x200B;를 하나씩 업데이트해야 합니다.

#### 생일

Source 스키마 필드 **birthDate**&#x200B;은(는) 대상 필드 **person.birthDate**&#x200B;에 연결되어야 합니다.

![데이터 수집](./images/tfbd.png)

#### 도시

Source 스키마 필드 **city**&#x200B;은(는) 대상 필드 **homeAddress.city**&#x200B;에 연결되어야 합니다.

![데이터 수집](./images/tfcity.png)

#### 국가

Source 스키마 필드 **country**&#x200B;을(를) 대상 필드 **homeAddress.country**&#x200B;에 연결해야 합니다.

![데이터 수집](./images/tfcountry.png)

#### country_code

Source 스키마 필드 **country_code**&#x200B;을(를) 대상 필드 **homeAddress.countryCode**&#x200B;에 연결해야 합니다.

![데이터 수집](./images/tfcountrycode.png)

#### 이메일

Source 스키마 필드 **전자 메일**&#x200B;은(는) 대상 필드 **personalEmail.address**&#x200B;에 연결해야 합니다.

![데이터 수집](./images/tfemail.png)

#### crmid

Source 스키마 필드 **crmid**&#x200B;을(를) 대상 필드 **`--aepTenantId--`.identification.core.crmId**&#x200B;에 연결해야 합니다.

![데이터 수집](./images/tfemail1.png)

#### first_name

Source 스키마 필드 **first_name**&#x200B;은(는) 대상 필드 **person.name.firstName**&#x200B;에 연결되어야 합니다.

![데이터 수집](./images/tffname.png)

#### 성별

Source 스키마 필드 **gender**&#x200B;은(는) 대상 필드 **person.gender**&#x200B;에 연결되어야 합니다.

![데이터 수집](./images/tfgender.png)

#### home_latitude

Source 스키마 필드 **home_latitude**&#x200B;을(를) 대상 필드 **homeAddress에 연결해야 합니다._schema.latitude**.

![데이터 수집](./images/tflat.png)

#### home_longitude

Source 스키마 필드 **home_longitude**&#x200B;은(는) 대상 필드 **homeAddress에 연결되어야 합니다._schema.longitude**.

![데이터 수집](./images/tflon.png)

#### ID

Source 스키마 필드 **id**&#x200B;을(를) 대상 필드 **_id**&#x200B;에 연결해야 합니다.

![데이터 수집](./images/tfid1.png)

#### last_name

Source 스키마 필드 **last_name**&#x200B;을(를) 대상 필드 **person.name.lastName**&#x200B;에 연결해야 합니다.

![데이터 수집](./images/tflname.png)

이제 이 항목을 사용할 수 있습니다. **마침을 클릭합니다**.

![데이터 수집](./images/overview.png)

**[!UICONTROL 마침]**&#x200B;을 클릭하면 **데이터 흐름** 개요가 표시되고, 몇 분 후 화면을 새로 고쳐 워크플로가 성공적으로 완료되었는지 확인할 수 있습니다. **대상 데이터 세트 이름**&#x200B;을 클릭합니다.

![데이터 수집](./images/dfsuccess.png)

그러면 수집이 처리된 데이터 세트가 표시되고 방금 수집된 [!UICONTROL 일괄 처리 ID]이(가) 표시되며, 1,000개의 레코드가 수집되고 상태는 **[!UICONTROL 성공]**&#x200B;입니다. **[!UICONTROL 데이터 집합 미리 보기]**&#x200B;를 클릭합니다.

![데이터 수집](./images/ingestdataset.png)

이제 로드된 데이터가 올바른지 확인하기 위해 데이터 세트의 작은 샘플이 표시됩니다.

![데이터 수집](./images/previewdata.png)

데이터가 로드되면 데이터 세트에 대한 올바른 데이터 거버넌스 접근 방식을 정의할 수 있습니다.

### 데이터 세트에 데이터 거버넌스 추가

이제 고객 데이터가 수집되었으므로 이 데이터 세트가 사용 및 내보내기 제어에 대해 제대로 제어되는지 확인해야 합니다. **[!UICONTROL 데이터 거버넌스]** 탭을 클릭하고 계약, ID 및 중요, 파트너 에코시스템 및 사용자 지정과 같은 여러 유형의 제한을 설정할 수 있는지 확인합니다.

![데이터 수집](./images/dsgovernance.png)

전체 데이터 세트에 대한 ID 데이터를 제한하겠습니다. 데이터 세트 이름 위에 커서를 놓고 연필 모양의 아이콘을 클릭하여 설정을 편집합니다.

![데이터 수집](./images/pencil.png)

**[!UICONTROL ID 데이터]**(으)로 이동하면 **[!UICONTROL I2]** 옵션이 선택되어 있는 것을 알 수 있습니다. 이는 이 데이터 집합에 있는 모든 정보가 적어도 간접적으로 사용자에게 식별된다고 가정합니다.

**[!UICONTROL 변경 내용 저장]**&#x200B;을 클릭합니다.

![데이터 수집](./images/identity.png)

다른 모듈에서는 데이터 거버넌스와 레이블의 프레임워크를 자세히 설명합니다.

이제 Adobe Experience Platform에서 CRM 데이터를 정상적으로 수집 및 분류했습니다.

다음 단계: [1.2.5 데이터 랜딩 영역](./ex5.md)

[모듈 1.2로 돌아가기](./data-ingestion.md)

[모든 모듈로 돌아가기](../../../overview.md)
