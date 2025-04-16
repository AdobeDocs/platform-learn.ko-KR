---
title: Workfront Fusion 시작하기
description: Workfront Fusion 및 Adobe I/O을 사용하여 Adobe Firefly Services API를 쿼리하는 방법 알아보기
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 42e260e0-8af0-4d71-b634-48c1966bd912
source-git-commit: 603e48e0453911177823fe7ceb340f8ca801c5e1
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 1%

---

# 1.2.1 Workfront Fusion 시작하기

Workfront Fusion 및 Adobe I/O을 사용하여 Adobe Firefly Services API를 쿼리하는 방법에 대해 알아봅니다.

## 1.2.1.1 새 시나리오 만들기

[https://experience.adobe.com/](https://experience.adobe.com/)&#x200B;(으)로 이동합니다. **Workfront Fusion**&#x200B;을 엽니다.

![WF Fusion](./images/wffusion1.png)

**시나리오**(으)로 이동합니다.

![WF Fusion](./images/wffusion2.png)

작업용 새 폴더를 만들려면 **+ 아이콘**&#x200B;을(를) 클릭하십시오.

![WF Fusion](./images/wffusion2a.png)

폴더 이름을 `--aepUserLdap--`로 지정하고 **저장**&#x200B;을 선택합니다.

![WF Fusion](./images/wffusion2b.png)

폴더를 선택한 다음 **새 시나리오 만들기**&#x200B;를 선택합니다.

![WF Fusion](./images/wffusion3.png)

빈 시나리오가 나타납니다. **도구**&#x200B;를 선택하고 **여러 변수 설정**&#x200B;을 선택하십시오.

![WF Fusion](./images/wffusion4.png)

**시계** 아이콘을 새로 추가된 **여러 변수 설정**(으)로 이동합니다.

![WF Fusion](./images/wffusion5.png)

화면이 다음과 같아야 합니다.

![WF Fusion](./images/wffusion6.png)

물음표를 마우스 오른쪽 단추로 클릭하고 **모듈 삭제**&#x200B;를 선택합니다.

![WF Fusion](./images/wffusion7.png)

그런 다음 **여러 변수 설정**&#x200B;을 마우스 오른쪽 단추로 클릭하고 **설정**&#x200B;을 선택합니다.

![WF Fusion](./images/wffusion8.png)

## 1.2.1.2 Adobe I/O 인증 구성

이제 Adobe I/O에 대해 인증하는 데 필요한 변수를 구성해야 합니다. 이전 연습에서는 Adobe I/O 프로젝트를 만들었습니다. 이제 Adobe I/O 프로젝트의 변수를 Workfront Fusion에서 정의해야 합니다.

다음 변수를 정의해야 합니다.

| 키 | 값 |
|:-------------:| :---------------:| 
| `CONST_client_id` | Adobe I/O 프로젝트 클라이언트 ID |
| `CONST_client_secret` | Adobe I/O 프로젝트 클라이언트 암호 |
| `CONST_scope` | Adobe I/O 프로젝트 범위 |

[https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)&#x200B;(으)로 이동하여 이름이 `--aepUserLdap-- One Adobe tutorial`인 Adobe I/O 프로젝트를 열어 이러한 변수를 찾습니다.

![WF Fusion](./images/wffusion9.png)

프로젝트에서 **OAuth Serverto-Server**&#x200B;을(를) 선택하여 위의 키에 대한 값을 확인합니다.

![WF Fusion](./images/wffusion10.png)

위의 키와 값을 사용하여 **여러 변수를 설정** 개체를 구성할 수 있습니다. **항목 추가**&#x200B;를 선택합니다.

![WF Fusion](./images/wffusion11.png)

**변수 이름**: **CONST_client_id** 및 해당 **변수 값**&#x200B;을(를) 입력하고 **추가**&#x200B;를 선택합니다.

![WF Fusion](./images/wffusion12.png)

**항목 추가**&#x200B;를 선택합니다.

![WF Fusion](./images/wffusion13.png)

**변수 이름**: **CONST_client_secret** 및 해당 **변수 값**&#x200B;을(를) 입력하고 **추가**&#x200B;를 선택하십시오.

![WF Fusion](./images/wffusion14.png)

**항목 추가**&#x200B;를 선택합니다.

![WF Fusion](./images/wffusion15.png)

**변수 이름**: **CONST_scope** 및 해당 **변수 값**&#x200B;을(를) 입력하고 **추가**&#x200B;를 선택합니다.

![WF Fusion](./images/wffusion16.png)

**확인**&#x200B;을 선택합니다.

![WF Fusion](./images/wffusion17.png)

**여러 변수 설정** 위에 마우스를 놓고 큰 **+** 아이콘을 선택하여 다른 모듈을 추가합니다.

![WF Fusion](./images/wffusion18.png)

화면이 다음과 같아야 합니다.

![WF Fusion](./images/wffusion19.png)

검색 창에서 **http**&#x200B;을(를) 입력하십시오. **HTTP**&#x200B;을(를) 선택하여 엽니다.

![WF Fusion](./images/wffusion21.png)

**요청**&#x200B;을 선택합니다.

![WF Fusion](./images/wffusion20.png)

| 키 | 값 |
|:-------------:| :---------------:| 
| `URL` | `https://ims-na1.adobelogin.com/ims/token/v3` |
| `Method` | `POST` |
| `Body Type` | `x-www-form-urlencoded` |

**항목 추가**&#x200B;를 선택합니다.

![WF Fusion](./images/wffusion22.png)

아래 각 값에 대한 항목을 추가합니다.

| 키 | 값 |
|:-------------:| :---------------:| 
| `client_id` | `CONST_client_id`에 대해 미리 정의된 변수 |
| `client_secret` | `CONST_client_secret`에 대해 미리 정의된 변수 |
| `scope` | `CONST_scope`에 대해 미리 정의된 변수 |
| `grant_type` | `client_credentials` |

`client_id` 구성:

![WF Fusion](./images/wffusion23.png)

`client_secret`에 대한 구성입니다.

![WF Fusion](./images/wffusion25.png)

`scope`에 대한 구성입니다.

![WF Fusion](./images/wffusion26.png)

`grant_type`에 대한 구성입니다.

![WF Fusion](./images/wffusion28.png)

아래로 스크롤하여 **구문 분석 응답**&#x200B;에 대한 상자를 선택합니다. **확인**&#x200B;을 선택합니다.

![WF Fusion](./images/wffusion27.png)

화면이 다음과 같아야 합니다. **한 번 실행**&#x200B;을 선택하세요.

![WF Fusion](./images/wffusion29.png)

시나리오가 실행되면 화면은 다음과 같아야 합니다.

![WF Fusion](./images/wffusion30.png)

**여러 변수 설정** 개체에서 **물음표** 아이콘을 선택하여 해당 개체가 실행될 때 발생한 상황을 확인합니다.

![WF Fusion](./images/wffusion31.png)

**HTTP - 요청 만들기** 개체에서 **물음표** 아이콘을 선택하여 해당 개체가 실행될 때 발생한 상황을 확인합니다. **OUTPUT**&#x200B;에서 Adobe I/O에서 반환되는 **access_token**&#x200B;을(를) 참조하십시오.

![WF Fusion](./images/wffusion32.png)

**HTTP - 요청**&#x200B;을 클릭하고 **+** 아이콘을 선택하여 다른 모듈을 추가합니다.

![WF Fusion](./images/wffusion33.png)

검색 창에서 `tools`을(를) 검색합니다. **도구**&#x200B;를 선택하십시오.

![WF Fusion](./images/wffusion34.png)

**여러 변수 설정**&#x200B;을 선택합니다.

![WF Fusion](./images/wffusion35.png)

**항목 추가**&#x200B;를 선택합니다.

![WF Fusion](./images/wffusion36.png)

**변수 이름**&#x200B;을(를) `bearer_token`(으)로 설정합니다. `access_token`을(를) 동적 **변수 값**(으)로 선택합니다. **추가**&#x200B;를 선택합니다.

![WF Fusion](./images/wffusion37.png)

화면이 다음과 같아야 합니다. **확인**&#x200B;을 선택합니다.

![WF Fusion](./images/wffusion38.png)

**한 번 실행**&#x200B;을 다시 선택하십시오.

![WF Fusion](./images/wffusion39.png)

시나리오가 실행되면 마지막 **여러 변수 설정** 개체에서 **물음표** 아이콘을 선택합니다. access_token이 변수 `bearer_token`에 저장되어 있습니다.

![WF Fusion](./images/wffusion40.png)

그런 다음 첫 번째 개체 **여러 값을 설정**&#x200B;을 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**&#x200B;를 선택합니다.

![WF Fusion](./images/wffusion41.png)

이름을 **Initialize 상수**(으)로 설정합니다. **확인**&#x200B;을 선택합니다.

![WF Fusion](./images/wffusion42.png)

두 번째 개체의 이름을 **Adobe I/O에 인증**(으)로 바꾸십시오. **확인**&#x200B;을 선택합니다.

![WF Fusion](./images/wffusion43.png)

세 번째 개체의 이름을 **전달자 토큰 설정**(으)로 바꾸십시오. **확인**&#x200B;을 선택합니다.

![WF Fusion](./images/wffusion44.png)

화면은 다음과 같아야 합니다.

![WF Fusion](./images/wffusion45.png)

그런 다음 시나리오 이름을 `--aepUSerLdap-- - Adobe I/O Authentication`(으)로 변경합니다.

![WF Fusion](./images/wffusion46.png)

**저장**&#x200B;을 선택합니다.

![WF Fusion](./images/wffusion47.png)

## 다음 단계

[Workfront Fusion 내에서 Adobe API 사용](./ex2.md){target="_blank"}(으)로 이동

[Workfront Fusion을 사용한 Creative 워크플로 자동화로 돌아가기](./automation.md){target="_blank"}

[모든 모듈](./../../../overview.md){target="_blank"}(으)로 돌아가기
