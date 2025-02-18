---
title: AJO 번역 서비스로 캠페인 만들기
description: AJO 번역 서비스로 캠페인 만들기
kt: 5342
doc-type: tutorial
exl-id: 536caf45-c614-48e8-adbb-6dc67d1a9606
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 0%

---

# 3.5.2 캠페인 만들기

[https://experience.adobe.com/](https://experience.adobe.com/)(으)로 이동합니다. **Journey Optimizer**&#x200B;을(를) 클릭합니다.

![번역](./images/ajolp1.png)

Journey Optimizer의 **Home** 보기로 리디렉션됩니다. 먼저 올바른 샌드박스를 사용하고 있는지 확인하십시오. 사용할 샌드박스를 `--aepSandboxName--`이라고 합니다.

![AOP](./images/ajolp2.png)

>[!NOTE]
>
>연습 [연습 3.1.2.1](./../ajob2c-1/ex2.md) 및 [연습 3.1.2.2](./../ajob2c-1/ex2.md)의 일부로 머리글 및 바닥글 조각을 이미 만든 경우 연습 3.5.2.3 파이버 캠페인 만들기 로 앞으로 이동하십시오. 머리글 및 바닥글 조각을 다시 만들지 마십시오.

## 3.5.2.1 헤더 조각 만들기

왼쪽 메뉴에서 **조각**&#x200B;을 클릭합니다. 조각은 Journey Optimizer 내의 재사용 가능한 구성 요소로서 중복을 방지하고, 이메일 메시지의 머리글이나 바닥글 변경과 같이 모든 메시지에 영향을 미치는 향후 변경 사항을 용이하게 합니다.

**조각 만들기**&#x200B;를 클릭합니다.

![AOP](./images/fragm1.png)

이름 `--aepUserLdap-- - CitiSignal - Header`을(를) 입력하고 **유형: 시각적 조각**&#x200B;을(를) 선택합니다. **만들기**&#x200B;를 클릭합니다.

![AOP](./images/fragm2.png)

그러면 이걸 보게 될 거야. 왼쪽 메뉴에서 이메일(행 및 열) 구조를 정의하는 데 사용할 수 있는 구조 구성 요소를 찾을 수 있습니다.

메뉴에서 캔버스로 **1:1 열**&#x200B;을(를) 끌어서 놓습니다. 로고 이미지의 자리 표시자가 됩니다.

![Journey Optimizer](./images/fragm3.png)

그런 다음 콘텐츠 구성 요소를 사용하여 이러한 블록 내에 콘텐츠를 추가할 수 있습니다. 첫 번째 행의 첫 번째 셀에 **Image** 구성 요소를 끌어서 놓습니다. **찾아보기**&#x200B;를 클릭합니다.

![Journey Optimizer](./images/fragm4.png)

그러면 AEM Assets 미디어 라이브러리를 보여주는 팝업이 열립니다. **citi-signal-images** 폴더로 이동하고 **CitiSignal-Logo-White.png** 이미지를 클릭하여 선택하고 **선택**&#x200B;을 클릭합니다.

>[!NOTE]
>
>AEM Assets 라이브러리에 Citi Signal 이미지가 없으면 [여기](./../../../../assets/ajo/CitiSignal-images.zip)에서 찾을 수 있습니다. 데스크톱에 다운로드하고 **citi-signal-images** 폴더를 만든 다음 해당 폴더의 모든 이미지를 업로드하세요.

![Journey Optimizer](./images/fragm5.png)

그러면 이걸 보게 될 거야. 이미지가 흰색이며 아직 표시되지 않습니다. 이제 이미지가 올바르게 표시되도록 배경색을 정의해야 합니다. **스타일**&#x200B;을 클릭한 다음 **배경색** 상자를 클릭합니다.

![Journey Optimizer](./images/fragm6.png)

팝업에서 **16진수** 색상 코드를 **#8821F4**(으)로 변경한 다음 **100%** 필드를 클릭하여 포커스를 변경합니다. 그러면 이미지에 새 색상이 적용된 것을 볼 수 있습니다.

![Journey Optimizer](./images/fragm7.png)

현재 이미지도 약간 너무 큽니다. **너비** 전환기를 **40%**(으)로 이동하여 너비를 변경해 보겠습니다.

![Journey Optimizer](./images/fragm8.png)

이제 헤더 조각이 준비되었습니다. **저장**&#x200B;을 클릭한 다음 화살표를 클릭하여 이전 화면으로 돌아갑니다.

![Journey Optimizer](./images/fragm9.png)

조각을 사용하려면 먼저 게시해야 합니다. **게시**&#x200B;를 클릭합니다.

![Journey Optimizer](./images/fragm10.png)

몇 분 후에 조각 상태가 **Live**(으)로 변경되었습니다.
다음으로, 이메일 메시지의 바닥글에 대한 새 조각을 만들어야 합니다. **조각 만들기**&#x200B;를 클릭합니다.

![Journey Optimizer](./images/fragm11.png)

## 3.5.2.2 바닥글 조각 만들기

**조각 만들기**&#x200B;를 클릭합니다.

![Journey Optimizer](./images/fragm11.png)

이름 `--aepUserLdap-- - CitiSignal - Footer`을(를) 입력하고 **유형: 시각적 조각**&#x200B;을(를) 선택합니다. **만들기**&#x200B;를 클릭합니다.

![Journey Optimizer](./images/fragm12.png)

그러면 이걸 보게 될 거야. 왼쪽 메뉴에서 이메일(행 및 열) 구조를 정의하는 데 사용할 수 있는 구조 구성 요소를 찾을 수 있습니다.

메뉴에서 캔버스로 **1:1 열**&#x200B;을(를) 끌어서 놓습니다. 바닥글 콘텐츠의 자리 표시자가 됩니다.

![Journey Optimizer](./images/fragm13.png)

그런 다음 콘텐츠 구성 요소를 사용하여 이러한 블록 내에 콘텐츠를 추가할 수 있습니다. 첫 번째 행의 첫 번째 셀에 **HTML** 구성 요소를 끌어서 놓습니다. 구성 요소를 클릭하여 선택한 다음 **&lt;/>** 아이콘을 클릭하여 HTML 소스 코드를 편집합니다.

![Journey Optimizer](./images/fragm14.png)

그러면 이걸 보게 될 거야.

![Journey Optimizer](./images/fragm15.png)

아래 HTML 코드 조각을 복사하여 Journey Optimizer의 **HTML 편집** 창에 붙여 넣습니다.

```html
<!--[if mso]><table cellpadding="0" cellspacing="0" border="0" width="100%"><tr><td style="text-align: center;" ><![endif]-->
<table style="width: auto; display: inline-block;">
  <tbody>
    <tr class="component-social-container">
      <td style="padding: 5px">
        <a style="text-decoration: none;" href="https://www.facebook.com" data-component-social-icon-id="facebook">
        
        </a>
      </td>
      <td style="padding: 5px">
        <a style="text-decoration: none;" href="https://x.com" data-component-social-icon-id="twitter">
        
        </a>
      </td>
      <td style="padding: 5px">
        <a style="text-decoration: none;" href="https://www.instagram.com" data-component-social-icon-id="instagram">
         
        </a>
      </td>
    </tr>
  </tbody>
</table>
<!--[if mso]></td></tr></table><![endif]-->
```

그럼 이걸로 드셔보세요 7, 12 및 17행에서 이제 AEM Assets 라이브러리의 자산을 사용하여 이미지 파일을 삽입해야 합니다.

![Journey Optimizer](./images/fragm16.png)

커서가 7행에 있는지 확인한 다음 왼쪽 메뉴에서 **Assets**&#x200B;을(를) 클릭합니다. **자산 선택기 열기**&#x200B;를 클릭하여 이미지를 선택합니다.

![Journey Optimizer](./images/fragm17.png)

**citi-signal-images** 폴더를 열고 **Icon_Facebook.png** 이미지를 클릭하여 선택합니다. **선택**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/fragm18.png)

커서가 12행에 있는지 확인한 다음 **자산 선택기 열기**&#x200B;를 클릭하여 이미지를 선택합니다.

![Journey Optimizer](./images/fragm19.png)

**citi-signal-images** 폴더를 열고 **Icon_X.png** 이미지를 클릭하여 선택합니다. **선택**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/fragm20.png)

커서가 17행에 있는지 확인한 다음 **자산 선택기 열기**&#x200B;를 클릭하여 이미지를 선택합니다.

![Journey Optimizer](./images/fragm21.png)

**citi-signal-images** 폴더를 열고 **Icon_Instagram.png** 이미지를 클릭하여 선택합니다. **선택**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/fragm22.png)

그러면 이걸 보게 될 거야. **저장**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/fragm23.png)

그러면 편집기로 돌아갑니다. 배경과 이미지 파일이 모두 흰색이므로 아이콘이 아직 표시되지 않습니다. 배경색을 변경하려면 **스타일**(으)로 이동하여 **배경색** 확인란을 클릭하세요.

![Journey Optimizer](./images/fragm24.png)

**16진수** 색 코드를 **#000000**(으)로 변경합니다.

![Journey Optimizer](./images/fragm25.png)

정렬을 가운데로 변경합니다.

![Journey Optimizer](./images/fragm26.png)

바닥글에 다른 부분을 추가하겠습니다. 방금 만든 HTML 구성 요소 위에 **이미지** 구성 요소를 끌어서 놓습니다. **찾아보기**&#x200B;를 클릭합니다.

![Journey Optimizer](./images/fragm27.png)

**`CitiSignal_Footer_Logo.png`** 이미지 파일을 클릭하여 선택하고 **선택**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/fragm28.png)

**스타일**(으)로 이동한 다음 **배경색** 확인란을 클릭합니다. 검정색으로 다시 변경하겠습니다. **16진수** 색 코드를 **#000000**(으)로 변경합니다.

![Journey Optimizer](./images/fragm29.png)

너비를 **20%**(으)로 변경하고 정렬이 가운데로 설정되어 있는지 확인하십시오.

![Journey Optimizer](./images/fragm30.png)

그런 다음 만든 HTML 구성 요소 아래에 **Text** 구성 요소를 끌어다 놓습니다. **찾아보기**&#x200B;를 클릭합니다.

![Journey Optimizer](./images/fragm31.png)

자리 표시자 텍스트를 대체하여 아래 텍스트를 복사하여 붙여넣습니다.

```
1234 N. South Street, Anywhere, US 12345

Unsubscribe

©2024 CitiSignal, Inc and its affiliates. All rights reserved.
```

**텍스트 맞춤**&#x200B;을 가운데로 설정합니다.

![Journey Optimizer](./images/fragm32.png)

**글꼴 색**&#x200B;을(를) 흰색, **#FFFFFF**(으)로 변경합니다.

![Journey Optimizer](./images/fragm33.png)

**배경색**&#x200B;을(를) 검정색, **#000000**(으)로 변경합니다.

![Journey Optimizer](./images/fragm34.png)

바닥글에서 **구독 취소** 텍스트를 선택하고 메뉴 막대에서 **링크** 아이콘을 클릭합니다. **Type**&#x200B;을(를) **외부 옵트아웃/구독 취소**(으)로 설정하고 URL을 **https://aepdemo.net/unsubscribe.html**(구독 취소 링크에 빈 URL을 사용할 수 없음)로 설정합니다.

![Journey Optimizer](./images/fragm35.png)

그럼 이걸로 드셔보세요 이제 바닥글이 준비되었습니다. **저장**&#x200B;을 클릭한 다음 화살표를 클릭하여 이전 페이지로 돌아갑니다.

![Journey Optimizer](./images/fragm36.png)

전자 메일에 사용할 수 있도록 바닥글을 게시하려면 **게시**&#x200B;를 클릭하세요.

![Journey Optimizer](./images/fragm37.png)

몇 분 후에 바닥글의 상태가 **Live**(으)로 변경됩니다.

![Journey Optimizer](./images/fragm38.png)

## 3.5.2.3 파이버 캠페인 만들기

이제 캠페인을 만듭니다. 들어오는 경험 이벤트 또는 대상 항목 또는 종료에 의존하여 1개의 특정 고객에 대한 여정을 트리거하는 이전 연습의 이벤트 기반 여정과 달리, 캠페인은 뉴스레터, 일회성 프로모션 또는 일반 정보와 같은 고유한 콘텐츠나 생일 캠페인 및 미리 알림과 같이 정기적으로 전송되는 유사한 콘텐츠로 전체 대상을 한 번 타겟팅합니다.

메뉴에서 **캠페인**(으)로 이동하여 **캠페인 만들기**&#x200B;를 클릭합니다.

![Journey Optimizer](./images/oc43.png)

**예약됨 - 마케팅**&#x200B;을 선택하고 **만들기**&#x200B;를 클릭합니다.

![Journey Optimizer](./images/campaign1.png)

캠페인 생성 화면에서 다음을 구성합니다.

- **이름**: `--aepUserLdap-- - CitiSignal Fiber`.
- **설명**: 파이버 캠페인
- **ID 유형**: 전자 메일로 변경

![Journey Optimizer](./images/campaign2.png)

**작업**(으)로 스크롤합니다. **Action**&#x200B;에 대해 **전자 메일**&#x200B;을(를) 선택하십시오.

![Journey Optimizer](./images/campaign3.png)

기존 **전자 메일 구성**&#x200B;을(를) 선택하십시오. 2분 정도 후에 콘텐츠를 편집할 수 있습니다.

![Journey Optimizer](./images/campaign3a.png)

**대상**&#x200B;까지 스크롤합니다. **대상 선택**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/campaign2b.png)

**대상**&#x200B;에 대해 [1.3.3에서 만든 대상을 선택합니다. `--aepUserLdap-- - CitiSignal Eligible for Fiber`(으)로 이름이 지정된 통합 컴포지션 만들기](./../../datacollection/dc1.3/ex3.md)입니다. **저장**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/campaign2a.png)

**일정**(으)로 스크롤합니다. **일정**&#x200B;에 대해 **특정 날짜 및 시간에**&#x200B;을(를) 선택하고 선택한 시간을 설정하십시오.

![Journey Optimizer](./images/campaign4.png)

이제 이메일 메시지 자체를 만들 수 있습니다. 위로 스크롤한 다음 **콘텐츠 편집**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/campaign5.png)

그러면 이걸 보게 될 거야. **제목 줄**&#x200B;에 대해 다음 항목을 사용하십시오.

```
{{profile.person.name.firstName}}, here's your Fiber offer!
```

**전자 메일 본문 편집**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/campaign6.png)

**처음부터 디자인**&#x200B;을 선택하세요.

![Journey Optimizer](./images/campaign7.png)

그러면 이걸 보게 될 거야. 왼쪽 메뉴에서 이메일(행 및 열) 구조를 정의하는 데 사용할 수 있는 구조 구성 요소를 찾을 수 있습니다.

캔버스에 **1:1 열**&#x200B;을 4번 끌어다 놓으십시오. 이렇게 하면 다음 구조가 제공됩니다.

![Journey Optimizer](./images/campaign8.png)

왼쪽 메뉴에서 **조각**(으)로 이동합니다. 이전에 만든 헤더를 캔버스의 첫 번째 구성 요소로 드래그합니다. 이전에 만든 바닥글을 캔버스의 마지막 구성 요소로 드래그합니다.

![Journey Optimizer](./images/campaign9.png)

왼쪽 메뉴에서 **+** 아이콘을 클릭합니다. 캔버스에 콘텐츠를 추가하려면 **콘텐츠**(으)로 이동하십시오.

![Journey Optimizer](./images/campaign10.png)

두 번째 행에 **Text** 구성 요소를 끌어서 놓습니다.

![Journey Optimizer](./images/campaign11.png)

구성 요소 **에서 기본 텍스트를 선택하십시오. 여기에 텍스트를 입력하십시오.**&#x200B;을(를) 아래 텍스트로 바꿉니다. 정렬을 **가운데 맞춤**(으)로 변경합니다.

```javascript
Hi {{profile.person.name.firstName}}

As a CitiSignal customer, you're in pole position to discover our new Fiber offering. Have a look at the below offer and update your contract!

Stay connected.
```

![Journey Optimizer](./images/campaign12.png)

**이미지** 구성 요소를 세 번째 행에 끌어서 놓습니다. **찾아보기**&#x200B;를 클릭합니다.

![Journey Optimizer](./images/campaign13.png)

이전 모듈의 일부로 만든 AEM Assets 저장소를 선택합니다. 해당 리포지토리의 이름은 `--aepUserLdap-- - Citi Signal dev`이어야 합니다. `--aepUserLdap-- - Workfront Assets` 폴더를 열려면 클릭하세요.

![Journey Optimizer](./images/campaign15a.png)

**2048x2048_buynow.png** 이미지를 클릭하여 선택하고 **선택**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/campaign14.png)

이제 기본 뉴스레터 이메일이 준비되었습니다. **저장**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/ready.png)

왼쪽 상단 모서리의 제목 줄 텍스트 옆에 있는 **화살표**&#x200B;를 클릭하여 캠페인 대시보드로 돌아갑니다.

![Journey Optimizer](./images/campaign19.png)

활성화하려면 **검토**&#x200B;를 클릭하세요.

![Journey Optimizer](./images/campaign20.png)

그러면 이 오류가 발생할 수 있습니다. 이 경우 대상자가 평가될 때까지 최대 24시간 대기한 다음 캠페인을 다시 활성화해야 할 수 있습니다. 나중에 실행하기 위해 캠페인의 일정을 업데이트해야 할 수도 있습니다.

![Journey Optimizer](./images/campaign21a.png)

**활성화**&#x200B;를 클릭합니다.

![Journey Optimizer](./images/campaign21.png)

활성화하면 캠페인이 실행되도록 예약됩니다.

![Journey Optimizer](./images/campaign22.png)

이 연습을 완료했습니다.

## 다음 단계

[3.5.3 메일로 이동](./ex3.md)

[Adobe Journey Optimizer: 번역 서비스](./ajotranslationsvcs.md){target="_blank"}로 돌아가기

[모든 모듈](./../../../../overview.md){target="_blank"}(으)로 돌아가기
