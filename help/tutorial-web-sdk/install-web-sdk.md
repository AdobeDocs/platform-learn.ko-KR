---
title: Adobe Experience Platform Web SDK 태그 확장 설치 및 구성
description: 데이터 수집 인터페이스에서 Platform Web SDK 태그 확장을 설치하고 구성하는 방법을 알아봅니다. 이 단원은 웹 SDK를 사용하여 Adobe Experience Cloud 구현 자습서의 일부입니다.
feature: Web SDK
exl-id: f30a44bb-99d7-476e-873a-b7802a0fe6aa
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 13%

---

# Adobe Experience Platform Web SDK 태그 확장 설치

데이터 수집 인터페이스에서 Platform Web SDK 태그 확장을 설치하고 구성하는 방법을 알아봅니다. 이 태그 확장은 _전용 태그 확장_ 에 데이터를 보내야 합니다. _모든 Adobe Experience Cloud 애플리케이션_, 포함 [Analytics](setup-analytics.md), [Target](setup-target.md), [Audience Manager](setup-audience-manager.md), Real-time Customer Data Platform 및 Journey Optimizer!

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* 데이터 수집 인터페이스에서 태그 속성 만들기
* Platform Web SDK 태그 확장 설치
* 이전에 만든 데이터 스트림을 확장에 매핑

## 전제 조건

이 자습서에서는 이전 단원을 완료했어야 합니다.

* [권한 구성](configure-permissions.md)
* [XDM 스키마 구성](configure-schemas.md)
* [ID 네임스페이스 구성](configure-identities.md)
* [데이터 스트림 구성](configure-datastream.md)

## Experience Platform 웹 SDK 확장 설치

### 속성 추가

먼저 태그 속성이 있어야 합니다. 속성은 웹 페이지에서 세부 정보를 수집하고 다양한 위치로 전송하는 데 필요한 모든 JavaScript, 규칙 및 기타 기능을 위한 컨테이너입니다.

자습서에 대한 새 태그 속성을 만듭니다.

1. 를 엽니다. [데이터 수집 인터페이스](https://launch.adobe.com/){target=&quot;_blank&quot;}
1. 선택 **[!UICONTROL 태그]** 왼쪽 탐색
1. **[!UICONTROL 새 속성]** 버튼을 선택합니다
   ![새 속성 추가](assets/websdk-property-addNewProperty.png)
1. 로서의 **[!UICONTROL 이름]**, 입력 `Web SDK Course` (회사의 여러 사용자가 이 자습서를 사용하고 있는 경우 끝에 이름을 추가합니다.)
1. 로서의 **[!UICONTROL 도메인]**, 입력 `enablementadobe.com` (나중에 설명)
1. **[!UICONTROL 저장]**을 선택합니다
   ![속성 세부 사항](assets/websdk-property-propertyDetails.png)

## 웹 SDK 확장 추가

이제 XDM 스키마, 데이터 스트림 및 태그 속성을 만들면 Platform Web SDK 확장을 설치할 준비가 되었습니다.

1. 새 태그 속성을 엽니다
1. 이동 **[!UICONTROL 확장]** > **[!UICONTROL 카탈로그]**
1. 검색 대상 `Adobe Experience Platform Web SDK`
1. 선택 **[!UICONTROL 설치]**

   ![웹 SDK 확장 설치](assets/extension-platform-web-sdk.jpg)


## 데이터 스트림에 Platform Web SDK 연결

대부분의 기본 설정을 그대로 두고 필요에 따라 나중에 업데이트합니다. 이제 확장을 데이터 스트림에 연결해야 합니다.

1. 아래 **[!UICONTROL 데이터 스트림]**&#x200B;에서 을(를) 선택합니다. **[!UICONTROL 목록에서 선택]** 입력 방법
1. 이전에 만든 데이터 스트림을 선택합니다. `Luma Web SDK`
1. **[!UICONTROL 저장]**&#x200B;을 선택합니다
   >[!NOTE]
   >
   > 데이터 스트림을 찾을 수 없는 경우 [데이터 스트림 구성](configure-datastream.md) 단원을 수행하고 단계에 따라 하나를 만듭니다.

   ![데이터 스트림 선택](assets/extension-luma-web-sdk-datastream-extension.png)

이제 Platform Web SDK를 설치하고 데이터 스트림에 연결했으므로 만든 스키마로 데이터 요소를 XDM 개체에 매핑하기 시작할 준비가 되었습니다.

>[!NOTE]
>
>이 자습서에서는 하나의 데이터 스트림만 구성하고 모든 태그 환경(개발, 스테이지 및 프로덕션)과 연결합니다. 웹 사이트에서 Platform Web SDK를 구현하는 경우 각 환경에 대해 별도의 데이터 스트림을 구성하고 다음을 사용하여 태그 환경에 매핑해야 합니다 **[!UICONTROL 입력 방법]** > **[!UICONTROL 값 입력]**
>
>![데이터 스트림 선택](assets/extension-luma-web-sdk-datastream-extension-enterValues.png)

>[!NOTE]
>
>에서 CNAME을 구성하지 않은 동안 [!UICONTROL Edge 도메인] 이 단원에서 설정하는 경우, Adobe은 자체 웹 사이트에서 Platform Web SDK를 구현할 때 CNAME을 사용하는 것을 권장합니다. CNAME 구현은 비록 쿠키 수명 측면에서는 어떠한 이점도 제공하지 않지만, 몇 가지 다른 이점이 있습니다. 이러한 이점에는 광고 차단기와 보편적으로 사용되지 않는 브라우저가 추적기로 분류된 도메인으로 데이터가 전송되는 것을 방지한다는 것도 포함됩니다. 이러한 경우 CNAME을 사용하면 이들 도구를 사용하는 사용자의 데이터 수집이 중단되는 것을 방지할 수 있습니다.

확장의 각 섹션에 대한 자세한 내용은 [Adobe Experience Platform 웹 SDK 확장 구성](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/web-sdk-extension-configuration.html)



[다음: ](create-data-elements.md)

>[!NOTE]
>
>Adobe Experience Platform Web SDK에 대한 학습에 시간을 내주셔서 감사합니다. 질문이 있거나 일반 피드백을 공유하거나 향후 컨텐츠에 대한 제안 사항이 있는 경우 해당 정보를 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
