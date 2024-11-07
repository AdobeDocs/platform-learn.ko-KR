---
title: Adobe Journey Optimizer - 이메일 메시지에 개인화 적용
description: 이 연습에서는 이메일 콘텐츠 내에서 세그먼트 개인화를 사용하는 방법을 설명합니다
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# 3.4.3 이메일 메시지에 개인화 적용

[Adobe Experience Cloud](https://experience.adobe.com)(으)로 이동하여 Adobe Experience Cloud에 로그인합니다. **Adobe Journey Optimizer**&#x200B;을(를) 클릭합니다.

![AOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

Journey Optimizer의 **Home** 보기로 리디렉션됩니다. 계속하려면 **샌드박스**&#x200B;를 선택해야 합니다. 선택할 샌드박스 이름이 ``--aepTenantId--``입니다. 화면 상단의 파란색 선에 있는 텍스트 **[!UICONTROL 프로덕션]**&#x200B;을(를) 클릭하면 됩니다.

![AOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

## 3.4.3.1 세그먼트 기반 개인화

이 연습에서는 세그먼트 멤버십을 기반으로 개인화된 텍스트로 뉴스레터 이메일 메시지를 개선합니다.

**여정**(으)로 이동합니다. 이전 연습에서 만든 뉴스레터 여정을 찾습니다. `--demoProfileLdap-- - Newsletter` 검색 여정을 클릭하여 엽니다.

![Journey Optimizer](./images/sbp1.png)

그러면 이걸 보게 될 거야. **복제**&#x200B;를 클릭합니다.

![Journey Optimizer](./images/sbp2.png)

**복제**&#x200B;를 클릭합니다.

![Journey Optimizer](./images/sbp3.png)

**전자 메일** 액션을 선택하고 **콘텐츠 편집**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/sbp3a.png)

**전자 메일 Designer**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/sbp4.png)

그러면 이걸 보게 될 거야.

![Journey Optimizer](./images/sbp5.png)

**콘텐츠 구성 요소**&#x200B;를 열고 **텍스트** 구성 요소를 현재 뉴스레터 콘텐츠 아래로 끕니다.

![Journey Optimizer](./images/sbp6.png)

전체 기본 텍스트를 선택하고 삭제합니다. 그런 다음 도구 모음에서 **개인화 추가** 단추를 클릭합니다.

![Journey Optimizer](./images/sbp7.png)

그러면 다음과 같은 결과가 표시됩니다.

![Journey Optimizer](./images/seg1.png)

왼쪽 메뉴에서 **세그먼트 멤버십**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/seg2.png)

>[!NOTE]
>
>이 목록에서 세그먼트를 찾을 수 없는 경우 아래로 조금 스크롤하여 세그먼트 ID를 수동으로 검색하는 방법에 대한 지침을 찾으십시오.

`Luma - Women's Category Interest` 세그먼트를 선택하고 **+** 아이콘을 클릭합니다. 다음과 같이 표시됩니다.

![Journey Optimizer](./images/seg3.png)

그런 다음 첫 번째 줄을 그대로 두고 2행과 3행을 다음 코드로 바꿉니다.

``
    Psssst... a private sale in the women category will launch soon, we will keep you posted
{%else%}
    Thanks for taking the time to read our newsletter. Here is a 10% promo code to use on the website: READER10
{%/if%}
``

그러면 다음 항목이 제공됩니다.

![Journey Optimizer](./images/seg4.png)

코드가 올바른지 확인하려면 **유효성 검사**&#x200B;를 클릭하십시오. **저장**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/sbp8.png)

이제 오른쪽 상단의 **저장** 단추를 클릭하여 이 메시지를 저장할 수 있습니다. 그런 다음 **콘텐츠 시뮬레이션**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/sbp9.png)

이 자습서의 일부로 만든 프로필 중 하나를 선택하고 **미리 보기**&#x200B;를 클릭합니다. 그러면 구성 결과가 표시됩니다.

![Journey Optimizer](./images/sbp10.png)

그러면 이걸 보게 될 거야. 그런 다음 **닫기**&#x200B;를 클릭합니다.

![Journey Optimizer](./images/sbp10fff.png)

왼쪽 상단 모서리의 제목 줄 텍스트 옆에 있는 **화살표**&#x200B;를 클릭하여 메시지 대시보드로 돌아갑니다.

![Journey Optimizer](./images/sbp11.png)

왼쪽 상단 모서리의 화살표를 클릭하여 여정으로 돌아갑니다.

![Journey Optimizer](./images/oc79afff.png)

전자 메일 작업을 닫으려면 **확인**&#x200B;을 클릭하세요.

![Journey Optimizer](./images/oc79bfff.png)

**일정**&#x200B;을(를) **한 번**(으)로 변경하고 **날짜/시간**&#x200B;을(를) 정의하세요. **확인**&#x200B;을 클릭합니다.

>[!NOTE]
>
>메시지 전송 날짜 및 시간은 1시간 이상이어야 합니다.

![Journey Optimizer](./images/sbp18.png)

여정에서 **Publish** 단추를 클릭합니다.

![Journey Optimizer](./images/sbp19.png)

팝업 창에서 **Publish**&#x200B;을 다시 클릭합니다.

![Journey Optimizer](./images/sbp20.png)

이제 기본 뉴스레터 여정이 게시되었습니다. 뉴스레터 이메일 메시지는 일정에 따라 전송되며 마지막 이메일이 전송되는 즉시 여정이 중지됩니다.

![Journey Optimizer](./images/sbp20fff.png)

이 연습을 완료했습니다.

다음 단계: [3.4.4 iOS용 푸시 알림 설정 및 사용](./ex4.md)

[모듈 3.4로 돌아가기](./journeyoptimizer.md)

[모든 모듈로 돌아가기](../../../overview.md)
