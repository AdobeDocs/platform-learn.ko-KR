---
title: 부트 캠프 - 실제 및 디지털 혼합 - 모바일 앱을 사용하고 비콘 항목을 트리거합니다
description: 부트 캠프 - 실제 및 디지털 혼합 - 모바일 앱을 사용하고 비콘 항목을 트리거합니다
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: c33c973b-db8a-49ce-bd6c-a6c4fbe579a0
source-git-commit: ead28f5631fc430c41e8c756b23dc69ffe19510e
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# 3.1 모바일 앱 사용 및 비콘 항목 트리거

## 모바일 앱 설치

앱을 설치하기 전에 **추적** 사용 중인 iOS 장치 이렇게 하려면 로 이동하십시오. **설정** > **개인 정보 및 보안** > **추적** 그리고 옵션을 **앱에서 추적 요청 허용**.

![DSN](./../uc3/images/app4.png)

Apple App Store으로 이동하여 을 검색합니다. `aepmobile-bootcamp`. 클릭 **설치** 또는 **다운로드**.

![DSN](./../uc3/images/app1.png)

앱이 설치되면 을 클릭합니다 **열기**.

![DSN](./../uc3/images/app2.png)

**확인**&#x200B;을 클릭합니다.

![DSN](./../uc3/images/app9.png)

클릭 **허용**.

![DSN](./../uc3/images/app3.png)

클릭 **동감이에요**.

![DSN](./../uc3/images/app7.png)

클릭 **앱 사용 허용**.

![DSN](./../uc3/images/app8.png)

클릭 **허용**.

![DSN](./../uc3/images/app5.png)

이제 앱의 홈 페이지에서 고객 여정을 확인할 수 있습니다.

![DSN](./../uc3/images/app12.png)

## 고객 여정 흐름

먼저 로그인해야 합니다. **로그인**&#x200B;을 클릭합니다.

![DSN](./images/app13.png)

이전 연습에서 계정을 만든 후 웹 사이트에서 이를 보았습니다. 이제 앱에서 만든 계정의 이메일 주소를 다시 사용하여 로그인해야 합니다.

![데모](./images/pv1.png)

여기에 웹 사이트에서 사용한 이메일 주소를 입력하고 을(를) 클릭합니다 **로그인**.

![DSN](./images/app14.png)

로그인했다는 확인이 표시되면 푸시 알림이 전송됩니다.

![DSN](./images/app15.png)

앱의 홈 페이지로 이동하면 추가 기능이 표시됩니다.

![DSN](./images/app17.png)

먼저, 다음 위치로 이동하십시오. **제품**. 이 예에서 임의의 제품을 클릭합니다 **커피 이동**.

![DSN](./images/app19.png)

이 표시됩니다 **커피 이동** 앱의 제품 페이지.

![DSN](./images/app20.png)

이제 오프라인 저장소 위치에서 비콘 항목 이벤트를 시뮬레이션합니다. 이를 시뮬레이션하는 목표는 매장 내 화면에서 고객 경험을 개인화하는 것입니다. 스토어 내 경험을 시각화하기 위해 스토어에 방금 입력한 고객과 관련된 정보를 동적으로 표시하는 페이지가 생성되었습니다.

계속하기 전에 컴퓨터에서 이 웹 페이지를 여십시오. [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

그러면 다음 내용이 표시됩니다.

![DSN](./images/screen1.png)

다음으로 홈 페이지로 돌아갑니다. 을(를) 클릭합니다. **beacon** 아이콘.

![DSN](./images/app23.png)

그러면 이게 보입니다. 먼저 을 선택합니다. **Bootcamp 화면 비콘** 그런 다음 **시작** 버튼을 클릭합니다. 이렇게 하면 비콘 항목을 시뮬레이션할 수 있습니다.

![DSN](./images/app21.png)

이제, 매장 내 화면을 보세요. 본 마지막 제품이 5초 이내에 표시됩니다.

![DSN](./images/screen2.png)

그런 다음 로 돌아갑니다. **제품**. 이 예에서 임의의 제품을 클릭합니다 **탄 비치블랭킷**.

![DSN](./images/app22.png)

다음으로 홈 페이지로 돌아갑니다. 을(를) 클릭합니다. **beacon** 아이콘.

![DSN](./images/app23.png)

그러면 이게 보입니다. 먼저 을 선택합니다. **Bootcamp 화면 비콘** 그런 다음 **시작** 다시 단추를 누릅니다. 이렇게 하면 비콘 항목을 시뮬레이션할 수 있습니다.

![DSN](./images/app21.png)

이제 다시 매장 내 화면을 보세요. 본 마지막 제품이 5초 이내에 표시됩니다.

![DSN](./images/screen3.png)

이제 웹 사이트에서 프로필 뷰어를 살펴보겠습니다. Adobe Experience Platform에서 고객과의 모든 상호 작용을 수집하여 저장한다는 것을 보여주기 위해 추가된 많은 이벤트를 볼 수 있습니다.

![DSN](./images/screen4.png)

다음 연습에서는 고유한 비콘 시작 여정을 구성하고 테스트합니다.

다음 단계: [3.2 이벤트 만들기](./ex2.md)

[사용자 흐름 3으로 돌아가기](./uc3.md)

[모든 모듈로 돌아가기](../../overview.md)
