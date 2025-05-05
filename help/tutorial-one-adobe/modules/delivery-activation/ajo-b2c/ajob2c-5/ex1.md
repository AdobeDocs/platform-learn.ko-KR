---
title: AJO 번역 서비스 시작하기
description: AJO 번역 서비스 시작하기
kt: 5342
doc-type: tutorial
exl-id: ec032c58-c5c2-48d2-bdd3-ff860bc4a35a
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# 3.5.1 번역 제공자

## 3.5.1.1 Microsoft Azure Translator 구성

[https://portal.azure.com/#home](https://portal.azure.com/#home)(으)로 이동합니다.

![번역](./images/transl1.png)

검색 창에서 `translators`을(를) 입력합니다. 그런 다음 **+ 만들기**&#x200B;를 클릭합니다.

![번역](./images/transl2.png)

**번역기 만들기**&#x200B;를 선택하십시오.

![번역](./images/transl3.png)

**구독 ID** 및 **리소스 그룹**&#x200B;을 선택하세요.
**지역**&#x200B;을(를) **전역**(으)로 설정합니다.
**가격 책정 계층**&#x200B;을(를) **무료 F0**(으)로 설정합니다.

**검토 + 만들기**&#x200B;를 선택합니다.

![번역](./images/transl4.png)

**만들기**&#x200B;를 선택합니다.

![번역](./images/transl5.png)

**리소스로 이동**&#x200B;을 선택합니다.

![번역](./images/transl6.png)

왼쪽 메뉴에서 **리소스 관리** > **키 및 끝점**&#x200B;으로 이동합니다. 키를 복사하려면 를 클릭합니다.

![번역](./images/transl7.png)

## 3.5.1.2 로케일 사전

[https://experience.adobe.com/](https://experience.adobe.com/)(으)로 이동합니다. **Journey Optimizer**&#x200B;을(를) 클릭합니다.

![번역](./images/ajolp1.png)

왼쪽 메뉴에서 **번역**(으)로 이동한 다음 **로케일 사전**(으)로 이동합니다. 이 메시지가 표시되면 **기본 로케일 추가**&#x200B;를 클릭하세요.

![번역](./images/locale1.png)

그럼 이걸 보셔야죠

![번역](./images/locale2.png)

## 3.5.1.3 AJO에서 번역 제공자 구성

[https://experience.adobe.com/](https://experience.adobe.com/)(으)로 이동합니다. **Journey Optimizer**&#x200B;을(를) 클릭합니다.

![번역](./images/ajolp1.png)

왼쪽 메뉴에서 **번역**(으)로 이동한 다음 **공급자**(으)로 이동합니다. **공급자 추가**&#x200B;를 클릭합니다.

![번역](./images/transl8.png)

**공급자**&#x200B;에서 **Microsoft Translator**&#x200B;를 선택하세요. 번역 공급업체의 사용을 활성화하려면 확인란을 선택하십시오. Microsoft Azure 번역기에서 복사한 키를 붙여넣습니다. 그런 다음 **자격 증명 유효성 검사**&#x200B;를 클릭합니다.

![번역](./images/transl9.png)

그러면 자격 증명의 유효성을 성공적으로 검사해야 합니다. 있는 경우 아래로 스크롤하여 번역할 언어를 선택합니다.

![번역](./images/transl10.png)

`[en-US] English`, `[es] Spanish`, `[fr] French`, `[nl] Dutch`을(를) 선택하십시오.

![번역](./images/transl11.png)

위로 스크롤하여 **저장**&#x200B;을 클릭합니다.

![번역](./images/transl12.png)

**번역 공급자**&#x200B;를 사용할 준비가 되었습니다.

![번역](./images/transl13.png)

## 3.5.1.4 번역 프로젝트 구성

[https://experience.adobe.com/](https://experience.adobe.com/)(으)로 이동합니다. **Journey Optimizer**&#x200B;을(를) 클릭합니다.

![번역](./images/ajolp1.png)

왼쪽 메뉴에서 **번역**(으)로 이동한 다음 **로케일 사전**(으)로 이동합니다. 이 메시지가 표시되면 **프로젝트 만들기**&#x200B;를 클릭하세요.

![번역](./images/ajoprovider1.png)

이름 `--aepUserLdap-- - Translations`을(를) 입력하고 **Source 로케일**&#x200B;을(를) `[en-US] English - United States`(으)로 설정하고 확인란을 선택하여 **승인된 번역 자동 게시**&#x200B;와 **검토 워크플로우 활성화**&#x200B;를 모두 사용하도록 설정합니다. **+ 로케일 추가**&#x200B;를 클릭합니다.

![번역](./images/ajoprovider1a.png)

`fr`을(를) 검색하고 `[fr] French`에 대한 확인란을 활성화한 다음 **Microsoft Translator**&#x200B;에 대한 확인란을 활성화하십시오. **+ 로케일 추가**&#x200B;를 클릭합니다.

![번역](./images/ajoprovider2.png)

`es`을(를) 검색하고 `[es] Spanish`에 대한 확인란을 활성화한 다음 **Microsoft Translator**&#x200B;에 대한 확인란을 활성화하십시오. **+ 로케일 추가**&#x200B;를 클릭합니다.

![번역](./images/ajoprovider3.png)

`nl`을(를) 검색하고 `[nl] Spanish`에 대한 확인란을 활성화한 다음 **Microsoft Translator**&#x200B;에 대한 확인란을 활성화하십시오. **+ 로케일 추가**&#x200B;를 클릭합니다.

![번역](./images/ajoprovider6.png)

**저장**&#x200B;을 클릭합니다.

![번역](./images/ajoprovider8.png)

**번역** 프로젝트를 사용할 준비가 되었습니다.

![번역](./images/ajoprovider9.png)

## 3.5.1.5 언어 설정 구성

**채널** > **일반 설정** > **언어 설정**(으)로 이동합니다. **언어 설정 만들기**&#x200B;를 클릭합니다.

![Journey Optimizer](./images/camploc6.png)

이름 `--aepUserLdap--_translations`을(를) 사용합니다. **번역 프로젝트**&#x200B;을(를) 선택하십시오. 그런 다음 **편집** 아이콘을 클릭합니다.

![Journey Optimizer](./images/camploc7.png)

이전 단계에서 생성한 번역 프로젝트를 선택합니다. **선택**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/camploc8.png)

그럼 이걸 보셔야죠 **대체 환경 설정**&#x200B;을(를) **영어 - 미국**(으)로 설정합니다. **프로필 언어 기본 설정 특성 선택**&#x200B;을 클릭하여 선택합니다. 그러면 고객 프로필에서 번역을 로드하는 데 사용할 필드가 결정됩니다. 그런 다음 **편집** 아이콘을 클릭하여 사용할 필드를 선택합니다.

![Journey Optimizer](./images/camploc9.png)

검색 창에서 **기본 언어**&#x200B;를 입력한 다음 **기본 언어** 필드를 선택합니다.

![Journey Optimizer](./images/camploc10.png)

**영어 - 미국** 및 **네덜란드어**&#x200B;에 대한 **편집** 아이콘을 클릭하여 구성을 검토하십시오.

![Journey Optimizer](./images/camploc11.png)

다음은 **영어 - 미국**&#x200B;에 대한 구성입니다. **취소**&#x200B;를 클릭합니다.

![Journey Optimizer](./images/camploc12.png)

**네덜란드어**&#x200B;에 대한 구성을 보려면 클릭하세요. **취소**&#x200B;를 클릭합니다.

![Journey Optimizer](./images/camploc13.png)

위로 스크롤하여 **제출**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/camploc14.png)

이제 언어 설정이 구성되었습니다.

![Journey Optimizer](./images/camploc15.png)

이 연습을 완료했습니다.

## 다음 단계

[3.5.2 캠페인 만들기](./ex2.md)(으)로 이동

[Adobe Journey Optimizer: 번역 서비스](./ajotranslationsvcs.md){target="_blank"}로 돌아가기

[모든 모듈](./../../../../overview.md){target="_blank"}(으)로 돌아가기
