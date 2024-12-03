---
title: 지능형 서비스 - 고객 AI 데이터 준비(수집)
description: 고객 AI - 데이터 준비(수집)
kt: 5342
doc-type: tutorial
exl-id: 71405859-cfc6-4991-a0b0-11c94818a0fa
source-git-commit: b53ee64ae8438b8f48f842ed1f44ee7ef3e813fc
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 1%

---

# 2.2.1 Customer AI - 데이터 준비(수집)

인텔리전트 서비스가 마케팅 이벤트 데이터에서 통찰력을 발견하려면 데이터를 의미론적으로 보강하고 표준 구조로 유지 관리해야 합니다. Intelligent Services는 이를 위해 Adobe의 XDM(Experience Data Model) 스키마를 사용합니다.
특히 Intelligent Services에서 사용하는 모든 데이터 세트는 **소비자 경험 이벤트** XDM 스키마를 준수해야 합니다.

## 스키마 만들기

이 연습에서는 **고객 AI** 지능형 서비스에 필요한 **고객 경험 이벤트 mixin**&#x200B;을(를) 포함하는 스키마를 만듭니다.

URL [https://experience.adobe.com/platform](https://experience.adobe.com/platform)로 이동하여 Adobe Experience Platform에 로그인합니다.

로그인하면 Adobe Experience Platform 홈페이지에 접속하게 됩니다.

![데이터 수집](../../datacollection/module1.2/images/home.png)

계속하려면 **샌드박스**&#x200B;를 선택해야 합니다. 선택할 샌드박스 이름이 ``--aepSandboxName--``입니다. 적절한 샌드박스를 선택하면 화면이 변경되고 이제 전용 샌드박스에 있습니다.

![데이터 수집](../../datacollection/module1.2/images/sb1.png)

왼쪽 메뉴에서 **스키마**&#x200B;를 클릭하고 **찾아보기**(으)로 이동합니다. **스키마 만들기**&#x200B;를 클릭합니다.

![새 스키마 만들기](./images/createschemabutton.png)

팝업에서 **수동**&#x200B;을 선택하고 **선택**&#x200B;을 클릭합니다.

![새 스키마 만들기](./images/schmanual.png)

**경험 이벤트**&#x200B;를 선택하고 **다음**&#x200B;을 클릭합니다.

![새 스키마 만들기](./images/xdmee.png)

이제 스키마의 이름을 제공해야 합니다. 스키마 이름으로 `--aepUserLdap-- - Demo System - Customer Experience Event`을(를) 사용하고 **마침**&#x200B;을(를) 클릭합니다.

![새 스키마 만들기](./images/schname.png)

그러면 이걸 보게 될 거야. 필드 그룹 아래의 **+ 추가**&#x200B;를 클릭합니다.

![새 스키마 만들기](./images/xdmee1.png)

이 스키마에 추가할 다음 **필드 그룹**&#x200B;을(를) 검색하고 선택하십시오.

- 고객 경험 이벤트

![새 CEE 스키마](./images/cee1.png)

- IdentityMap

**필드 그룹 추가**&#x200B;를 클릭합니다.

![새 CEE 스키마](./images/cee2.png)

그러면 이걸 보게 될 거야. 그런 다음 스키마 이름을 선택합니다. 이제 **프로필** 토글을 클릭하여 **프로필**&#x200B;에 대한 스키마를 사용하도록 설정해야 합니다.

![새 스키마 만들기](./images/xdmee3.png)

그러면 이걸 보게 될 거야. **이 스키마의 데이터에 대한 확인란을 선택하면 identityMap 필드에 기본 ID가 포함됩니다.** 질문에 답합니다. **사용**&#x200B;을 클릭합니다.

![새 스키마 만들기](./images/xdmee4.png)

이제 이 항목을 사용할 수 있습니다. 스키마를 저장하려면 **저장**&#x200B;을 클릭하세요.

![새 스키마 만들기](./images/xdmee5.png)

## 데이터 세트 만들기

왼쪽 메뉴에서 **데이터 세트**&#x200B;를 클릭하고 **찾아보기**(으)로 이동합니다. **데이터 집합 만들기**&#x200B;를 클릭합니다.

![데이터 집합](./images/createds.png)

**스키마에서 데이터 집합 만들기**&#x200B;를 클릭합니다.

![데이터 집합](./images/createdatasetfromschema.png)

다음 화면에서는 이전 연습에서 만든 데이터 세트(**[!UICONTROL ldap - 데모 시스템 - 고객 경험 이벤트]**)를 선택합니다. **다음**&#x200B;을 클릭합니다.

![데이터 집합](./images/createds1.png)

데이터 집합 이름으로 `--aepUserLdap-- - Demo System - Customer Experience Event Dataset`을(를) 사용합니다. **마침을 클릭합니다**.

![데이터 집합](./images/createds2.png)

이제 데이터 세트가 생성됩니다. **프로필** 전환을 사용하도록 설정합니다.

![데이터 집합](./images/createds3.png)

**사용**&#x200B;을 클릭합니다.

![데이터 집합](./images/createds4.png)

이제 다음 항목이 제공됩니다.

![데이터 집합](./images/createds5.png)

이제 고객 경험 이벤트 데이터 수집을 시작하고 고객 AI 서비스를 사용할 준비가 되었습니다.

## 경험 이벤트 테스트 데이터 다운로드

**스키마** 및 **데이터 집합**&#x200B;이 구성되면 이제 경험 이벤트 데이터를 수집할 준비가 되었습니다. Customer AI는 특정 데이터 요구 사항이 있으므로 외부에서 준비한 데이터를 수집해야 합니다.

이 연습에서 경험 이벤트를 위해 준비된 데이터는 [소비자 경험 이벤트 XDM 필드 그룹](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)의 요구 사항 및 스키마를 준수해야 합니다.

다음 위치에서 데모 데이터가 포함된 zip 파일을 다운로드하십시오. [https://tech-insiders.s3.us-west-2.amazonaws.com/CUSTOM-CAI-EVENTS-WEB.zip](https://tech-insiders.s3.us-west-2.amazonaws.com/CUSTOM-CAI-EVENTS-WEB.zip).

이제 **CUSTOM-CAI-EVENTS-WEB.zip** 파일을 다운로드했습니다. 컴퓨터의 바탕 화면에 파일을 놓고 압축을 해제하면 **CUSTOM-CAI-EVENTS-WEB**(이)라는 폴더가 표시됩니다.

![데이터 집합](./images/ingest.png)

해당 폴더에는 여러 개의 시퀀스 JSON 파일이 있으며, 이 파일은 다음 연습에서 모두 수집해야 합니다.

![데이터 집합](./images/ingest1a.png)

## 경험 이벤트 테스트 데이터 수집

Adobe Experience Platform에서 **데이터 세트**(으)로 이동하여 **[!UICONTROL ldap - 데모 시스템 - 고객 경험 이벤트 데이터 세트]**(으)로 지정된 데이터 세트를 엽니다.

![데이터 집합](./images/ingest1.png)

데이터 집합에서 **파일 선택**&#x200B;을 클릭하여 데이터를 추가합니다.

![데이터 집합](./images/ingest2.png)

팝업에서 **WEBSITE-EE-5.json**&#x200B;까지 **WEBSITE-EE-1.json** 파일을 선택하고 **열기**&#x200B;를 클릭합니다.

![데이터 집합](./images/ingest3.png)

**WEBSITE-EE-6.json** 및 **WEBSITE-EE-7.json** 파일에 대해 이 수집 프로세스를 반복합니다.

데이터가 가져오기되고 **로드 중** 상태에서 새 일괄 처리가 만들어집니다. 파일이 업로드될 때까지 이 페이지에서 나가지 마십시오.

![데이터 집합](./images/ingest4.png)

파일이 업로드되면 일괄 처리 상태가 **로드 중**&#x200B;에서 **처리 중**(으)로 변경됩니다.

![데이터 집합](./images/ingest5.png)

데이터를 수집하고 처리하는 데 10~20분이 걸릴 수 있습니다.

데이터 수집이 성공하면 다양한 업로드의 일괄 처리 상태가 **성공**(으)로 변경됩니다.

![데이터 집합](./images/ingest7.png)

다음 단계: [2.2.2 Customer AI - 새 인스턴스 만들기(구성)](./ex2.md)

[모듈 2.2로 돌아가기](./intelligent-services.md)

[모든 모듈로 돌아가기](./../../../overview.md)
