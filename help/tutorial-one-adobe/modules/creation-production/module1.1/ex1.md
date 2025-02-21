---
title: Firefly 서비스 시작하기
description: Postman 및 Adobe I/O을 사용하여 Adobe Firefly Services API를 쿼리하는 방법에 대해 알아봅니다
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: 6ef4ce94dbbcd65ab30bcfad24f4ddd746c26b82
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---

# 1.1.1 Firefly 서비스 시작하기

Postman 및 Adobe I/O을 사용하여 Adobe Firefly Services API를 쿼리하는 방법에 대해 알아봅니다.

## 1.1.1.1 필수 구성 요소

이 연습을 계속하려면 [Adobe I/O 프로젝트](./../../../modules/getting-started/gettingstarted/ex6.md)의 설정을 완료해야 하며 [Postman](./../../../modules/getting-started/gettingstarted/ex7.md) 또는 [PostBuster](./../../../modules/getting-started/gettingstarted/ex8.md)와 같이 API와 상호 작용하는 응용 프로그램을 구성해야 합니다.

## 1.1.1.1 firefly.adobe.com

[https://firefly.adobe.com](https://firefly.adobe.com)&#x200B;(으)로 이동합니다. **프로필** 아이콘을 클릭하고 올바른 **계정**&#x200B;에 로그인했는지 확인하십시오. 올바른 계정 번호는 `--aepImsOrgName--`입니다. 필요한 경우 **프로필 전환**&#x200B;을 클릭하여 해당 계정으로 전환합니다.

![Postman](./images/ffui1.png){zoomable="yes"}

`Horses in a field` 프롬프트를 입력하고 **생성**&#x200B;을 클릭합니다.

![Postman](./images/ffui2.png){zoomable="yes"}

그러면 이와 비슷한 것을 볼 수 있을 겁니다.

![Postman](./images/ffui3.png){zoomable="yes"}

그런 다음 브라우저에서 **개발자 도구**&#x200B;를 엽니다.

![Postman](./images/ffui4.png){zoomable="yes"}

그럼 이걸 보셔야죠 **네트워크** 탭으로 이동합니다.

![Postman](./images/ffui5.png){zoomable="yes"}

검색어 **생성**&#x200B;을 입력한 다음 **생성**&#x200B;을 다시 클릭합니다. 그러면 이름이 **generate-async**&#x200B;인 요청이 표시됩니다. 선택한 다음 **페이로드**(으)로 이동하십시오. 그러면 요청 세부 정보가 표시됩니다.

![Postman](./images/ffui6.png){zoomable="yes"}

여기에 표시되는 요청은 Firefly Services의 서버측 백엔드에 전송된 요청입니다. 여기에는 몇 가지 중요한 매개 변수가 포함되어 있습니다.

- **prompt**: Firefly에서 생성할 이미지 종류를 요청하는 메시지입니다.

- **시드**: 이 요청에서 시드가 무작위로 생성되었습니다. Firefly에서 이미지를 생성할 때마다 기본적으로 시드 라는 난수를 선택하여 프로세스를 시작합니다. 이 난수는 각 이미지를 고유하게 만드는 요소에 기여하며, 매우 다양한 이미지를 생성하려는 경우에 유용합니다. 그러나 여러 요청에 대해 서로 유사한 이미지를 생성하려는 경우가 있을 수 있습니다. 예를 들어 Firefly에서 Firefly의 다른 옵션(예: 스타일 사전 설정, 참조 이미지 등)을 사용하여 수정할 이미지를 생성하는 경우 이후 HTTP 요청에서 해당 이미지의 시드를 사용하여 이후 이미지의 무작위성을 제한하고 원하는 이미지에 로그인합니다.

![Postman](./images/ffui7.png){zoomable="yes"}

UI를 다시 살펴보십시오. **종횡비**&#x200B;을(를) **가로(4:3)**(으)로 변경합니다.

![Postman](./images/ffui8.png){zoomable="yes"}

**효과**&#x200B;까지 아래로 스크롤하고 **테마**&#x200B;로 이동한 다음 **만화책**&#x200B;과 같은 효과를 선택하십시오.

![Postman](./images/ffui9.png){zoomable="yes"}

브라우저에서 **개발자 도구**&#x200B;를 다시 엽니다. 그런 다음 **생성**&#x200B;을 클릭하고 전송되는 네트워크 요청을 검사합니다.

![Postman](./images/ffui10.png){zoomable="yes"}

이제 네트워크 요청의 세부 사항을 검사할 때 다음을 볼 수 있습니다.

- **프롬프트**&#x200B;이(가) 이전 요청과 비교하여 변경되지 않았습니다.
- **시드**&#x200B;이(가) 이전 요청과 비교하여 변경되지 않았습니다.
- **크기**&#x200B;이(가) **종횡비**&#x200B;의 변경에 따라 변경되었습니다.
- **스타일**&#x200B;이 추가되었으며 선택한 **comic_book** 효과에 대한 참조가 있습니다.

![Postman](./images/ffui11.png){zoomable="yes"}

다음 연습에서는 **seed** 숫자 중 하나를 사용해야 합니다. 선택의 시드 번호를 적으십시오.

다음 연습에서는 Firefly Services를 사용하여 유사한 작업을 수행한 다음 UI 대신 API를 사용합니다. 이 예제에서 시드 번호는 **45781**&#x200B;입니다.

## 1.1.1.3 Adobe I/O - access_token

**Adobe IO - OAuth** 컬렉션에서 이름이 **POST - 액세스 토큰 가져오기**&#x200B;인 요청을 선택하고 **전송**&#x200B;을 선택합니다. 응답에는 새 **accesstoken**&#x200B;이(가) 포함되어야 합니다.

![Postman](./images/ioauthresp.png){zoomable="yes"}

## 1.1.1.4 Firefly 서비스 API, 텍스트 2 이미지

유효하고 새로운 access_token이 있으므로 첫 번째 요청을 Firefly Services API로 전송할 준비가 되었습니다.

**FF - Firefly 서비스 기술 내부자** 컬렉션에서 **POST - Firefly - T2I V3**(이)라는 요청을 선택합니다.

![Firefly](./images/ff1.png){zoomable="yes"}

응답에서 이미지 URL을 복사하여 웹 브라우저에서 열어 이미지를 봅니다.

![Firefly](./images/ff2.png){zoomable="yes"}

`horses in a field`을(를) 묘사하는 멋진 이미지를 볼 수 있습니다.

![Firefly](./images/ff3.png){zoomable="yes"}

요청 **POST - Firefly - T2I V3**&#x200B;의 **본문**&#x200B;에서 필드 `"promptBiasingLocaleCode": "en-US"` 아래에 다음을 추가하고 변수 `XXX`을(를) Firefly Services UI에서 임의로 사용한 시드 번호 중 하나로 바꿉니다. 이 예제에서 **seed** 숫자는 `45781`입니다.

```json
,
  "seeds": [
    XXX
  ]
```

**보내기**&#x200B;를 클릭합니다. 그러면 Firefly 서비스에서 생성한 새 이미지가 포함된 응답을 받게 됩니다. 이미지를 열어 봅니다.

![Firefly](./images/ff4.png){zoomable="yes"}

그런 다음 사용된 **seed**&#x200B;을(를) 기반으로 약간의 차이가 있는 새 이미지가 표시됩니다.

![Firefly](./images/ff5.png){zoomable="yes"}

그런 다음 요청의 **본문**&#x200B;에서 **POST - Firefly - T2I V3**&#x200B;을(를) **시드** 개체 아래에 **스타일** 개체를 붙여 넣으십시오. 이렇게 하면 생성된 이미지의 스타일이 **comic_book**(으)로 변경됩니다.

```json
,
  "contentClass": "art",
  "styles": {
    "presets": [
      "comic_book"
    ],
    "strength": 50
  }
```

## 다음 단계

[Microsoft Azure 및 사전 서명된 URL을 사용하여 Firefly 프로세스 최적화](./ex2.md){target="_blank"}(으)로 이동

[Adobe Firefly 서비스 개요](./firefly-services.md){target="_blank"}(으)로 돌아가기

[모든 모듈](./../../../overview.md){target="_blank"}(으)로 돌아가기
