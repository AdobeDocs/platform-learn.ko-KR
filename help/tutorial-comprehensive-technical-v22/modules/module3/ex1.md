---
title: Foundation - 실시간 고객 프로필 - 알 수 없음에서 웹 사이트에 알려짐
description: Foundation - 실시간 고객 프로필 - 알 수 없음에서 웹 사이트에 알려짐
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 065d79c5-8979-4992-afb1-4da47bbff74b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 2%

---

# 3.1 알 수 없음에서 웹 사이트에 알려짐

## 컨텍스트

알 수 없음에서 알려진 대로 여정은 고객 여정에서 획득까지 유지되는 것 같이 최근 브랜드들 중에서 가장 중요한 항목 중 하나입니다.

Adobe Experience Platform은 이 여정에서 큰 역할을 합니다. 플랫폼은 의사소통의 두뇌, &quot;기록의 경험 시스템&quot; 입니다.

플랫폼은 고객이 알려진 고객보다 더 광범위한 환경입니다. 웹 사이트의 알 수 없는 방문자도 플랫폼의 관점에서 고객의 경우 알 수 없는 방문자와 같은 모든 동작이 Platform으로 전송됩니다. 이러한 접근 방식 덕분에 이 방문자가 결국 알려진 고객이 되면 브랜드는 그 순간 이전에 발생한 상황을 시각화할 수 있습니다. 이것은 속성 및 경험 최적화 관점에서 도움이 됩니다.

## 고객 여정 흐름

이동 [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Adobe ID으로 로그인하면 다음이 표시됩니다. 웹 사이트 프로젝트를 클릭하여 엽니다.

![DSN](../module0/images/web8.png)

설정 **Screens** 페이지를 클릭한 다음 **실행**.

![DSN](../module1/images/web2.png)

그러면 데모 웹 사이트가 열립니다. URL을 선택하고 클립보드에 복사합니다.

![DSN](../module0/images/web3.png)

새 시크릿 브라우저 창을 엽니다.

![DSN](../module0/images/web4.png)

이전 단계에서 복사한 데모 웹 사이트의 URL을 붙여넣습니다. 그런 다음 Adobe ID을 사용하여 로그인하라는 메시지가 표시됩니다.

![DSN](../module0/images/web5.png)

계정 유형을 선택하고 로그인 프로세스를 완료합니다.

![DSN](../module0/images/web6.png)

그러면 시크릿 브라우저 창에서 로드되는 웹 사이트가 표시됩니다. 모든 데모에서는 신선하고 시크릿 브라우저 창을 사용하여 데모 웹 사이트 URL을 로드해야 합니다.

![DSN](../module0/images/web7.png)

화면 왼쪽 상단 모서리에서 Adobe 로고 아이콘을 클릭하여 프로필 뷰어를 엽니다.

![데모](../module2/images/pv1.png)

를 사용하여 프로필 뷰어 패널 및 실시간 고객 프로필을 봅니다. **Experience Cloud ID** 을 현재 알 수 없는 이 고객에 대한 기본 식별자로 사용하십시오.

![데모](../module2/images/pv2.png)

고객의 행동을 기반으로 수집된 모든 경험 이벤트를 볼 수도 있습니다. 현재 목록이 비어 있지만 곧 변경됩니다.

![데모](../module2/images/pv3.png)

로 이동합니다. **남성** 제품 카테고리. 그런 다음 제품을 클릭합니다 **몬타나 윈드 재킷**.

![데모](../module2/images/pv4.png)

그러면 제품 세부 사항 페이지가 표시됩니다. 유형의 경험 이벤트 **제품 보기** 이제 모듈 1에서 검토한 웹 SDK 구현을 사용하여 Adobe Experience Platform으로 보내졌습니다.

![데모](../module2/images/pv5.png)

Provile Viewer 패널을 열고 **경험 이벤트**.

![데모](../module2/images/pv6.png)

로 돌아갑니다. **여성** 카테고리 페이지를 열고 다른 제품을 클릭합니다. 다른 경험 이벤트가 Adobe Experience Platform에 전송되었습니다.

![데모](../module2/images/pv7.png)

프로필 뷰어 패널을 엽니다. 이제 2개의 경험 이벤트 유형이 표시됩니다 **제품 보기**. 행동은 익명으로 처리되지만 모든 클릭을 추적하고 Adobe Experience Platform에 저장할 수 있습니다. 익명의 고객이 알려지면 Adobe에서는 모든 익명의 행동을 알려진 프로필에 자동으로 병합할 수 있습니다.

![데모](../module2/images/pv8.png)

등록/로그인 페이지로 이동합니다. 클릭 **계정 만들기**.

![데모](../module2/images/pv9.png)

세부 사항을 입력하고 **등록** 그런 다음 이전 페이지로 리디렉션됩니다.

![데모](../module2/images/pv10.png)

프로필 뷰어 패널을 열고 실시간 고객 프로필로 이동합니다. 프로필 뷰어 패널에서는 새로 추가한 이메일 및 휴대폰 식별자와 같이 모든 개인 데이터가 표시됩니다.

![데모](../module2/images/pv11.png)

프로필 뷰어 패널에서 경험 이벤트로 이동합니다. 이전에 본 2개의 제품이 프로필 뷰어 패널에서 표시됩니다. 이제 이러한 두 이벤트가 모두 &#39;알려진&#39; 프로필에도 연결됩니다.

![데모](../module2/images/pv12.png)

이제 데이터를 Adobe Experience Platform에 수집하여 ECID 및 이메일 주소와 같은 식별자에 해당 데이터를 연결했습니다. 이 방법의 목표는 하려는 일의 비즈니스 컨텍스트를 이해하는 것입니다. 다음 연습에서는 모든 데이터 수집을 가능하게 하는 데 필요한 모든 것을 구성합니다.

### 모바일 앱 탐색

알려진 고객이 된 후에는 모바일 앱 사용을 시작할 차례입니다. iPhone에서 모바일 앱을 연 다음, 앱에 로그인합니다.

앱을 더 이상 설치하지 않았거나 설치하는 방법을 기억할 수 없는 경우에는 여기에서 확인하십시오. [0.5 모바일 앱 사용](../module0/ex5.md)

지침에 따라 앱을 설치한 후 Luma 브랜드가 로드되는 앱의 랜딩 페이지가 표시됩니다. 화면의 왼쪽 상단에 있는 계정 아이콘을 클릭합니다.

![데모](./images/app_hp.png)

로그인 화면에서 데스크탑 웹 사이트에서 사용한 이메일 주소로 로그인합니다. **로그인**&#x200B;을 클릭합니다.

![데모](./images/app_acc.png)

앱의 홈 화면으로 이동하여 를 클릭하여 제품을 엽니다.

![데모](./images/app_hp.png)

그러면 제품 세부 사항 페이지가 표시됩니다.

![데모](./images/app_carst.png)

앱의 홈 화면으로 이동하고 화면에서 왼쪽으로 밀면 프로필 뷰어 패널을 볼 수 있습니다. 그러면 방금 본 제품이 **경험 이벤트** 섹션을 참조하십시오.

![데모](./images/app_after_carst.png)

이제 데스크탑 컴퓨터로 돌아가서 홈 페이지를 새로 고치면 제품 역시 표시됩니다.

![데모](./images/lb_x_aftermobile.png)

이제 데이터를 Adobe Experience Platform에 수집하여 ECID 및 이메일 주소와 같은 식별자에 해당 데이터를 연결했습니다. 이 연습의 목적은 여러분이 하려는 일의 비즈니스 맥락에 대해 이해하는 것입니다. 이제 실시간 교차 장치 고객 프로필을 효과적으로 빌드했습니다. 다음 연습에서는 Adobe Experience Platform에서 프로필을 시각화합니다.

다음 단계: [3.2 실시간 고객 프로필 시각화 - UI](./ex2.md)

[모듈 3으로 돌아가기](./real-time-customer-profile.md)

[모든 모듈로 돌아가기](../../overview.md)
