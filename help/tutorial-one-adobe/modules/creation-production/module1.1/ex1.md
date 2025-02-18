---
title: Firefly 서비스 시작하기
description: Postman 및 Adobe I/O을 사용하여 Adobe Firefly Services API를 쿼리하는 방법에 대해 알아봅니다
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: b083a817700320e8e45645702c2868423c1fae99
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# 1.1.1 Firefly 서비스 시작하기

Postman 및 Adobe I/O을 사용하여 Adobe Firefly Services API를 쿼리하는 방법에 대해 알아봅니다.

## 1.1.1.1 사전 요구 사항

이 연습을 계속하려면 [Adobe I/O 프로젝트](./../../../modules/getting-started/gettingstarted/ex6.md)의 설정을 완료해야 하며 [Postman](./../../../modules/getting-started/gettingstarted/ex7.md) 또는 [PostBuster](./../../../modules/getting-started/gettingstarted/ex8.md)와 같이 API와 상호 작용하는 응용 프로그램을 구성해야 합니다.

## 1.1.1.2 Adobe I/O - access_token

**Adobe IO - OAuth** 컬렉션에서 이름이 **POST - 액세스 토큰 가져오기**&#x200B;인 요청을 선택하고 **전송**&#x200B;을 선택합니다. 응답에는 새 **accesstoken**&#x200B;이(가) 포함되어야 합니다.

![Postman](./images/ioauthresp.png){zoomable="yes"}

## 1.1.1.3 Firefly 서비스 API, 텍스트 2 이미지

유효하고 새로운 access_token이 있으므로 첫 번째 요청을 Firefly Services API로 전송할 준비가 되었습니다.

**FF - Firefly 서비스 기술 내부자** 컬렉션에서 **POST - Firefly - T2I V3**(이)라는 요청을 선택합니다.

![Firefly](./images/ff1.png){zoomable="yes"}

응답에서 이미지 URL을 복사하여 웹 브라우저에서 열어 이미지를 봅니다.

![Firefly](./images/ff2.png){zoomable="yes"}

`horses in a field`을(를) 묘사하는 멋진 이미지를 볼 수 있습니다.

![Firefly](./images/ff3.png){zoomable="yes"}

다음 연습을 계속하기 전에 언제든지 API 요청을 재생하십시오.

## 다음 단계

[Microsoft Azure 및 사전 서명된 URL을 사용하여 Firefly 프로세스 최적화](./ex2.md){target="_blank"}(으)로 이동

[Adobe Firefly 서비스 개요](./firefly-services.md){target="_blank"}(으)로 돌아가기

[모든 모듈](./../../../overview.md){target="_blank"}(으)로 돌아가기
