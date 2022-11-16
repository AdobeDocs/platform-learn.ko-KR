---
title: 기초 - 실시간 고객 프로필 - 세그먼트 만들기 - API
description: 기초 - 실시간 고객 프로필 - 세그먼트 만들기 - API
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 3f537efd-7281-4c0c-b809-97f266a2a337
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 3%

---

# 3.5 세그먼트 만들기 - API

이 연습에서는 Adobe Experience Platform의 API를 사용하여 Postman 및 Adobe I/O을 사용하여 세그먼트를 만들고 해당 세그먼트의 결과를 데이터 세트로 저장합니다.

## Story

실시간 고객 프로필에서는 모든 프로필 데이터가 이벤트 데이터 및 기존 세그먼트 멤버십과 함께 표시됩니다. 표시되는 데이터는 Adobe 애플리케이션 및 외부 솔루션에서 가져온 것입니다. 경험 기록 시스템인 Adobe Experience Platform에서 가장 강력한 보기입니다.

## 연습 3.5.1 - 플랫폼 API를 통해 세그먼트 만들기

Postman으로 이동합니다.

컬렉션을 찾습니다. **_Adobe Experience Platform 지원**. 이 컬렉션에는 폴더가 표시됩니다 **2. 세그먼테이션**. 이 연습에서는 이러한 요청을 사용할 것입니다.

![세그먼테이션](./images/pmdtl.png)

다음으로 API를 통해 세그먼트를 만드는 데 필요한 모든 단계를 수행합니다. 간단한 세그먼트를 만듭니다. &quot;**ldap** 모든 여성 고객.

### 1단계 - 세그먼트 정의 만들기

이름이 지정된 요청을 클릭합니다. **1단계 - 프로필: 세그먼트 정의 만들기**.

![세그먼테이션](./images/s1_call.png)

다음 작업을 수행합니다. **본문** 섹션을 참조하십시오.

![세그먼테이션](./images/s1_body.png)

에서 **본문** 이 요청의 경우 다음 내용이 표시됩니다.

![세그먼테이션](./images/s1_bodydtl.png)

이 요청에 사용되는 언어를 프로필 쿼리 언어라고 합니다. 또는 **PQL**.

PQL에 대한 자세한 정보 및 설명서를 찾을 수 있습니다 [여기](https://experienceleague.adobe.com/docs/experience-platform/segmentation/pql/overview.html?lang=en).


주의: 변수를 업데이트하십시오 **이름** 아래 요청에서 **ldap** 특정 **ldap**.

```json
{
    "name" : "ldap - API - All Female Customer",
    "expression" : {"type":"PQL", "format":"pql/json", "value":"{\"nodeType\":\"fnApply\",\"fnName\":\"in\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"gender\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"person\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"List\",\"nodeType\":\"literal\",\"value\":[\"female\"]}]}"},
    "createdBy": "ldap",
    "schema" : { "name" : "_xdm.context.profile"},
    "ttlInDays" : 90
}
```

특정 **ldap**&#x200B;로 지정하는 경우 본문은 다음과 유사해야 합니다.

```json
{
    "name" : "vangeluw - API - All Female Customer",
    "expression" : {"type":"PQL", "format":"pql/json", "value":"{\"nodeType\":\"fnApply\",\"fnName\":\"in\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"gender\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"person\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"List\",\"nodeType\":\"literal\",\"value\":[\"female\"]}]}"},
    "createdBy": "vangeluw",
    "schema" : { "name" : "_xdm.context.profile"},
    "ttlInDays" : 90
}
```

또한 **Header** - 요청 필드. 이동 **머리글**. 그러면 다음 내용이 표시됩니다.

![Postman](./images/s1_h.png)

| 키 | 값 |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>사용 중인 Adobe Experience Platform 샌드박스의 이름을 지정해야 합니다. x-sandbox-name은 `--aepSandboxId--`.

이제 파란색 **보내기** 버튼을 클릭하여 세그먼트를 만들고 그 결과를 확인합니다.

![세그먼테이션](./images/s1_bodydtl_results.png)

이 단계 후에는 플랫폼 UI에서 세그먼트 정의를 볼 수 있습니다. 이를 확인하려면 Adobe Experience Platform에 로그인하고 **세그먼트**.

![세그먼테이션](./images/s1_segmentdef.png)

### 2단계 - 세그먼트 POST 작업 만들기

이전 연습에서 _스트리밍_ 세그먼트. 스트리밍 세그먼트는 지속적으로 자격 조건을 실시간으로 평가합니다. 여기서 하는 일은 _배치_ 세그먼트. 배치 세그먼트를 통해 자격 측면에서 세그먼트의 모습을 미리 볼 수 있습니다. _세그먼트가 실제로 실행되었다는 의미가 아닙니다_. 현재, _이 세그먼트는 아무도 사용할 수 없습니다._. 사람들에게 자격을 부여하려면 배치 세그먼트를 실행해야 합니다. 이 작업이 바로 여기에서 수행할 작업입니다.

이제 POST 작업을 살펴보겠습니다.

Postman으로 이동합니다.

![세그먼테이션](./images/pmdtl.png)

Postman 컬렉션에서 **2단계 - POST 세그먼트 작업** 열려고

![세그먼테이션](./images/s2_call.png)

또한 **Header** - 요청 필드. 이동 **머리글**. 그러면 다음 내용이 표시됩니다.

![Postman](./images/s2headers.png)

| 키 | 값 |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>사용 중인 Adobe Experience Platform 샌드박스의 이름을 지정해야 합니다. x-sandbox-name은 `--aepSandboxId--`.

파란색 클릭 **보내기** 버튼을 클릭합니다.

다음과 유사한 결과가 표시됩니다.

![세그먼테이션](./images/s2_call_response.png)

현재 이 세그먼트 작업이 실행 중이며 시간이 좀 걸릴 수 있습니다. 3단계에서는 이 작업의 상태를 확인할 수 있습니다.


### 3단계 - GET 세그먼트 작업 상태

Postman으로 이동합니다.

![세그먼테이션](./images/pmdtl.png)

Postman 컬렉션에서 **3단계 - GET 세그먼트 작업 상태**.

![세그먼테이션](./images/s3_call.png)

또한 **Header** - 요청 필드. 이동 **머리글**. 그러면 다음 내용이 표시됩니다.

![Postman](./images/s3headers.png)

| 키 | 값 |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>사용 중인 Adobe Experience Platform 샌드박스의 이름을 지정해야 합니다. x-sandbox-name은 `--aepSandboxId--`.

파란색 클릭 **보내기** 버튼을 클릭합니다.

다음과 유사한 결과가 표시됩니다.

![세그먼테이션](./images/s3_status.png)

이 예에서 **상태** 작업 중 이(가) **큐에 있음**.

파란색을 클릭하여 이 요청을 반복합니다 **보내기** 몇 분마다 **상태** 가 로 설정되어 있습니다. **성공**.

![세그먼테이션](./images/s3_status_succeeded.png)

상태가 **성공**, 세그먼트 작업이 실행되었으며 이제 고객이 세그먼트에 대한 자격을 갖습니다.

세분화 연습을 완료했습니다. 이제 실시간 고객 프로필을 전사적으로 활성화하는 방법을 살펴보겠습니다.

다음 단계: [3.6 콜 센터에서 실시간 고객 프로필 활용 사례 보기](./ex6.md)

[모듈 3으로 돌아가기](./real-time-customer-profile.md)

[모든 모듈로 돌아가기](../../overview.md)
