---
title: Adobe Experience Platform Web SDK 태그 확장 설치 및 구성
description: 데이터 수집 인터페이스에서 Platform Web SDK 태그 확장 기능을 설치하고 구성하는 방법을 알아봅니다. 이 수업은 Web SDK를 사용하여 Adobe Experience Cloud 구현 튜토리얼의 일부입니다.
feature: Web SDK, Tags
jira: KT-15404
exl-id: f30a44bb-99d7-476e-873a-b7802a0fe6aa
source-git-commit: 7ccbaaf4db43921f07c971c485e1460a1a7f0334
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 11%

---

# Adobe Experience Platform Web SDK 태그 확장 설치

Adobe Experience Platform Web SDK 태그 확장 기능을 설치하고 구성하는 방법에 대해 알아봅니다. 웹 SDK을 구현하는 가장 쉬운 방법은 Adobe의 태그 관리자인 태그(이전 이름: Launch)를 사용하는 것입니다. Platform Web SDK 태그 확장은 _Analytics_, _Target_, [Audience Manager](setup-analytics.md), Real-Time Customer Data Platform 및 [Journey Optimizer](setup-target.md)을 포함하여 [모든 Adobe Experience Cloud 응용 프로그램](setup-audience-manager.md)에 데이터를 보내는 데 필요한 [유일한 태그 확장](setup-web-channel.md)입니다!

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* 데이터 수집 인터페이스에서 태그 속성 만들기
* Platform Web SDK 태그 확장 설치
* 이전에 만든 데이터스트림을 확장에 매핑

## 전제 조건

이 자습서에서는 이전 단원을 완료했어야 합니다.

* [데이터스트림 구성](configure-datastream.md)

### 태그 속성 추가

먼저 태그 속성이 있어야 합니다. 속성은 웹 페이지에서 세부 정보를 수집하여 여러 위치로 보내는 데 필요한 모든 JavaScript, 규칙 및 기타 기능을 위한 컨테이너입니다.

자습서에 대한 새 태그 속성을 만듭니다.

1. [데이터 수집 인터페이스](https://experience.adobe.com/data-collection/){target="_blank"} 열기
1. 왼쪽 탐색에서 **[!UICONTROL 태그]** 선택
1. **[!UICONTROL 새 속성]** 단추 선택
   ![새 속성 추가](assets/websdk-property-addNewProperty.png)
1. **[!UICONTROL 이름]**(으)로 `Web SDK Course`을(를) 입력하십시오(회사에서 여러 사람이 이 자습서를 수강하는 경우 마지막에 이름을 추가하십시오.)
1. **[!UICONTROL 도메인]**(으)로 `enablementadobe.com` 입력(나중에 설명)
1. **[!UICONTROL 저장]** 선택
   ![속성 세부 정보](assets/websdk-property-propertyDetails.png)

## 웹 SDK 확장 추가

이제 XDM 스키마, 데이터스트림 및 태그 속성이 생성되면 Platform Web SDK 확장을 설치할 준비가 된 것입니다.

1. 새 태그 속성 열기
1. **[!UICONTROL 확장]** > **[!UICONTROL 카탈로그]**(으)로 이동
1. `Adobe Experience Platform Web SDK` 검색
1. **[!UICONTROL 설치]** 선택

   ![웹 SDK 확장 설치](assets/extension-platform-web-sdk.png)


## 데이터 스트림에 확장을 연결합니다.

대부분의 기본 설정을 그대로 두고 필요에 따라 나중에 업데이트합니다. 이제 해야 하는 유일한 작업은 확장을 데이터 스트림에 연결하는 것입니다.

1. **[!UICONTROL 데이터스트림]**&#x200B;에서 **[!UICONTROL 목록에서 선택]** 입력 방법을 선택합니다.
1. 스키마, ID 네임스페이스 및 데이터스트림을 생성한 샌드박스를 선택합니다
1. 이전에 만든 데이터 스트림 `Luma Web SDK`을(를) 선택하십시오.
1. **[!UICONTROL 저장]** 선택

   >[!NOTE]
   >
   > 데이터 스트림을 찾을 수 없는 경우 [데이터 스트림 구성](configure-datastream.md) 단원으로 이동하여 단계를 따라 데이터 스트림을 만드십시오

   ![데이터 스트림 선택](assets/extension-luma-web-sdk-datastream-extension.png)

확장의 각 섹션에 대한 자세한 내용은 [Adobe Experience Platform Web SDK 확장 구성](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/extensions/client/web-sdk/web-sdk-extension-configuration)을 참조하십시오.

>[!NOTE]
>
>이 단원에서 [!UICONTROL Edge 도메인] 설정에서 CNAME을 구성하지 않았지만 Adobe에서는 자체 웹 사이트에서 Platform Web SDK을 구현할 때 CNAME을 사용하는 것을 권장합니다. CNAME 구현은 비록 쿠키 수명 측면에서는 어떠한 이점도 제공하지 않지만, 몇 가지 다른 이점이 있습니다. 이러한 이점에는 광고 차단기와 보편적으로 사용되지 않는 브라우저가 추적기로 분류된 도메인으로 데이터가 전송되는 것을 방지하는 것이 포함됩니다. 이러한 경우 CNAME을 사용하면 이들 도구를 사용하는 사용자의 데이터 수집이 중단되는 것을 방지할 수 있습니다.

>[!NOTE]
>
>이 자습서에서는 하나의 데이터스트림만 구성하고 모든 태그 환경(개발, 스테이지 및 프로덕션)과 연결합니다. 자체 웹 사이트에서 Platform Web SDK을 구현하는 경우 각 환경에 대해 별도의 데이터 스트림을 구성하고 확장 구성에 따라 매핑해야 합니다.

이제 Platform Web SDK을 설치하고 데이터 스트림과 연결했으므로 데이터 수집을 시작할 준비가 되었습니다.

>[!NOTE]
>
>Adobe Experience Platform 웹 SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나 일반적인 피드백을 공유하고 싶거나 향후 콘텐츠에 대한 제안이 있는 경우 이 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=ko)에서 공유하십시오.
