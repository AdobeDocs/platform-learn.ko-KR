---
title: 기초 - 실시간 고객 프로필 - 세그먼트 만들기 - API
description: 기초 - 실시간 고객 프로필 - 세그먼트 만들기 - API
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 3%

---

# 2.1.5 세그먼트 만들기 - API

이 연습에서는 Postman의 API를 사용하여 Adobe Experience Platform과 Adobe I/O을 사용하여 세그먼트를 만들고 해당 세그먼트의 결과를 데이터 세트로 저장합니다.

## 스토리

실시간 고객 프로필에는 이벤트 데이터 및 기존 세그먼트 멤버십과 함께 모든 프로필 데이터가 표시됩니다. 표시되는 데이터는 Adobe 애플리케이션 및 외부 솔루션에서 어디에서나 가져올 수 있습니다. 이것은 기록의 경험 시스템인 Adobe Experience Platform에서 가장 강력한 보기입니다.

## 2.1.5.1 - Platform API를 통해 세그먼트 만들기

Postman으로 이동합니다.

다음 컬렉션을 찾습니다. **_Adobe Experience Platform 지원**. 이 컬렉션에는 **2 폴더가 표시됩니다. 세그먼테이션**. 이 연습에서는 이러한 요청을 사용합니다.

![세그먼테이션](./images/pmdtl.png)

다음은 API를 통해 세그먼트를 만드는 데 필요한 모든 단계를 수행하는 것입니다. 간단한 세그먼트 &quot;**ldap** - 모든 여성 고객&quot;을 만듭니다.

### 1단계 - 세그먼트 정의 만들기

이름이 **1단계 - 프로필: 세그먼트 정의 만들기**&#x200B;인 요청을 클릭합니다.

![세그먼테이션](./images/s1_call.png)

이 요청의 **본문** 섹션으로 이동하십시오.

![세그먼테이션](./images/s1_body.png)

이 요청의 **본문**&#x200B;에 다음이 표시됩니다.

![세그먼테이션](./images/s1_bodydtl.png)

이 요청에 사용되는 언어는 Profile Query Language 또는 **PQL**&#x200B;입니다.

PQL [여기](https://experienceleague.adobe.com/docs/experience-platform/segmentation/pql/overview.html?lang=en)에서 추가 정보 및 설명서를 찾을 수 있습니다.


주의: **ldap**&#x200B;을(를) 특정 **ldap**(으)로 바꾸어 아래 요청에서 변수 **name**&#x200B;을(를) 업데이트하십시오.

```json
{
    "name" : "ldap - API - All Female Customer",
    "expression" : {"type":"PQL", "format":"pql/json", "value":"{\"nodeType\":\"fnApply\",\"fnName\":\"in\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"gender\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"person\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"List\",\"nodeType\":\"literal\",\"value\":[\"female\"]}]}"},
    "createdBy": "ldap",
    "schema" : { "name" : "_xdm.context.profile"},
    "ttlInDays" : 90
}
```

특정 **ldap**&#x200B;를 추가한 후에는 본문이 다음과 유사해야 합니다.

```json
{
    "name" : "vangeluw - API - All Female Customer",
    "expression" : {"type":"PQL", "format":"pql/json", "value":"{\"nodeType\":\"fnApply\",\"fnName\":\"in\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"gender\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"person\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"List\",\"nodeType\":\"literal\",\"value\":[\"female\"]}]}"},
    "createdBy": "vangeluw",
    "schema" : { "name" : "_xdm.context.profile"},
    "ttlInDays" : 90
}
```

요청의 **헤더** 필드도 확인해야 합니다. **머리글**(으)로 이동합니다. 그러면 다음과 같은 결과가 표시됩니다.

![Postman](./images/s1_h.png)

| 키 | 값 |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>사용 중인 Adobe Experience Platform 샌드박스의 이름을 지정해야 합니다. x-sandbox-name은 `--aepSandboxId--`이어야 합니다.

이제 파란색 **보내기** 단추를 클릭하여 세그먼트를 만들고 그 결과를 봅니다.

![세그먼테이션](./images/s1_bodydtl_results.png)

이 단계 후에는 Platform UI에서 세그먼트 정의를 볼 수 있습니다. 이를 확인하려면 Adobe Experience Platform에 로그인하고 **세그먼트**(으)로 이동하세요.

![세그먼테이션](./images/s1_segmentdef.png)

### 2단계 - 세그먼트 POST 작업 만들기

이전 연습에서는 _스트리밍_ 세그먼트를 만들었습니다. 스트리밍 세그먼트는 지속적으로 자격을 실시간으로 평가합니다. _일괄 처리_ 세그먼트를 만드는 중입니다. 일괄 처리 세그먼트는 자격 측면에서 세그먼트가 표시될 수 있는 모습을 미리 볼 수 있지만 _세그먼트가 실제로 실행되었음을 의미하지는 않습니다_. 현재 _아무도 이 세그먼트에 적합하지 않습니다_. 사람들이 자격을 갖추게 하려면 배치 세그먼트를 실행해야 합니다. 바로 여기에서 수행할 작업입니다.

이제 세그먼트 작업 POST을 살펴보겠습니다.

Postman으로 이동합니다.

![세그먼테이션](./images/pmdtl.png)

Postman 컬렉션에서 이름이 **2단계 - POST 세그먼트 작업**&#x200B;인 요청을 클릭하여 엽니다.

![세그먼테이션](./images/s2_call.png)

요청의 **헤더** 필드도 확인해야 합니다. **머리글**(으)로 이동합니다. 그러면 다음과 같은 결과가 표시됩니다.

![Postman](./images/s2headers.png)

| 키 | 값 |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>사용 중인 Adobe Experience Platform 샌드박스의 이름을 지정해야 합니다. x-sandbox-name은 `--aepSandboxId--`이어야 합니다.

파란색 **보내기** 단추를 클릭합니다.

다음과 유사한 결과가 표시되어야 합니다.

![세그먼테이션](./images/s2_call_response.png)

이 세그먼트 작업은 현재 실행 중이므로 시간이 걸릴 수 있습니다. 3단계에서 이 작업의 상태를 확인할 수 있습니다.


### 3단계 - GET 세그먼트 작업 상태

Postman으로 이동합니다.

![세그먼테이션](./images/pmdtl.png)

Postman 컬렉션에서 이름이 **3단계 - GET 세그먼트 작업 상태**&#x200B;인 요청을 클릭합니다.

![세그먼테이션](./images/s3_call.png)

요청의 **헤더** 필드도 확인해야 합니다. **머리글**(으)로 이동합니다. 그러면 다음과 같은 결과가 표시됩니다.

![Postman](./images/s3headers.png)

| 키 | 값 |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>사용 중인 Adobe Experience Platform 샌드박스의 이름을 지정해야 합니다. x-sandbox-name은 `--aepSandboxId--`이어야 합니다.

파란색 **보내기** 단추를 클릭합니다.

다음과 유사한 결과가 표시되어야 합니다.

![세그먼테이션](./images/s3_status.png)

이 예에서는 작업의 **상태**&#x200B;가 **QUEUED**(으)로 설정되어 있습니다.

**상태**&#x200B;이(가) **성공**(으)로 설정될 때까지 파란색 **보내기** 단추를 몇 분마다 클릭하여 이 요청을 반복합니다.

![세그먼테이션](./images/s3_status_succeeded.png)

상태가 **SUCCEEDED**&#x200B;이면 세그먼트 작업이 실행되었으며 고객이 이제 세그먼트에 대한 자격을 갖습니다.

축하합니다. 세분화 연습을 완료했습니다. 이제 전사적으로 실시간 고객 프로필을 활성화하는 방법에 대해 살펴보겠습니다.

다음 단계: [2.1.6 콜센터에서 실시간 고객 프로필 확인](./ex6.md)

[모듈 2.1로 돌아가기](./real-time-customer-profile.md)

[모든 모듈로 돌아가기](../../../overview.md)
