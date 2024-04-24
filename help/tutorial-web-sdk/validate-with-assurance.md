---
title: Experience Platform 보증을 사용하여 웹 SDK 구현 유효성 검사
description: Adobe Experience Platform Assurance를 사용하여 Platform Web SDK 구현의 유효성을 검사하는 방법을 알아봅니다. 이 단원은 Web SDK를 사용하여 Adobe Experience Cloud 구현 자습서의 일부입니다.
feature: Web SDK,Tags,Assurance
exl-id: 31e381ea-fbaf-495f-a6e9-2ff6c0d36939
source-git-commit: aeff30f808fd65370b58eba69d24e658474a92d7
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 2%

---

# Experience Platform 보증을 사용하여 웹 SDK 구현 유효성 검사

Adobe Experience Platform Assurance는 데이터를 수집하거나 경험을 제공하는 방법을 검사, 증명, 시뮬레이션 및 확인하는 데 도움이 되는 Adobe Experience Cloud의 제품입니다. 자세한 내용 [Adobe 보증](https://experienceleague.adobe.com/en/docs/experience-platform/assurance/home).


## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* 보증 세션 시작
* Platform Edge Network과 주고받은 요청 보기

## 전제 조건

데이터 수집 태그 및 [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} 을(를) 통해 다음 자습서의 이전 단원을 완료했습니다.

* [XDM 스키마 구성](configure-schemas.md)
* [ID 네임스페이스 구성](configure-identities.md)
* [데이터스트림 구성](configure-datastream.md)
* [태그 속성에 설치된 Web SDK 확장](install-web-sdk.md)
* [데이터 요소 만들기](create-data-elements.md)
* [ID 만들기](create-identities.md)
* [태그 규칙 만들기](create-tag-rule.md)
* [디버거를 사용하여 유효성 검사](validate-with-debugger.md)


## 보증 세션 시작 및 보기

보증 세션을 시작하는 방법에는 여러 가지가 있습니다.

### 디버거에서 보증 세션 시작

Adobe Experience Platform Debugger에서 Edge Trace를 활성화할 때마다 백그라운드에서 Assurance 세션이 시작됩니다.

Debugger 단원에서 이 작업을 수행하는 방법 검토:

1. 로 이동 [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html) 디버거를 사용하여 [사이트의 태그 속성을 자신의 개발 속성으로 전환합니다.](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. 의 왼쪽 탐색 **[!UICONTROL Experience Platform 디버거]** 선택 **[!UICONTROL 로그]**
1. 다음 항목 선택 **[!UICONTROL Edge]** 탭을 클릭하고 다음을 선택합니다 **[!UICONTROL 연결]**

   ![연결 에지 추적](assets/analytics-debugger-edgeTrace.png)
1. Edge Trace 가 활성화된 경우 맨 위에 발신 링크 아이콘이 표시됩니다. Assurance를 열려면 아이콘을 선택합니다. 브라우저에서 새 탭이 열립니다.

   ![보증 세션 시작](assets/validate-debugger-start-assurnance.png)


### Assurance 인터페이스에서 Assurance 세션 시작

1. 를 엽니다. [데이터 수집 인터페이스](https://experience.adobe.com/#/data-collection/home){target="_blank"}
1. 왼쪽 탐색에서 Assurance 선택
1. 세션 생성 선택
   ![보증 세션 만들기](assets/assurance-create-session.png)
1. 시작 선택
1. 세션에 이름을 지정하십시오(예: ). `Luma Web SDK validation`
1. 다음으로: **[!UICONTROL 기본 URL]** 입력 `https://luma.enablementadobe.com/`
   ![보증 세션 이름 지정](assets/assurance-name-session.png)
1. 다음 화면에서 다음을 선택합니다. **[!UICONTROL 링크 복사]**
1. 아이콘을 선택하여 클립보드에 링크를 복사합니다.
1. 브라우저에 URL을 붙여 넣으면 특수 URL 매개 변수와 함께 Luma 웹 사이트가 열립니다 `adb_validation_sessionid` 세션을 시작합니다.
1. Assurance 인터페이스에 세션에 성공적으로 연결되었음을 나타내는 메시지가 표시되고 Assurance 인터페이스에 캡처된 이벤트가 표시됩니다.
   ![보증 세션이 연결되었습니다.](assets/assurance-success.png)

## 웹 SDK 구현의 현재 상태 유효성 검사

이 구현 단계에서 볼 수 있는 정보는 제한됩니다. 볼 수 있는 한 가지 값은 플랫폼 Edge Network에서 생성된 Experience Cloud ID(ECID)입니다.

1. Adobe 응답 핸들이라는 이벤트가 있는 행을 선택합니다.
1. 메뉴가 오른쪽에 표시됩니다. 다음 항목 선택 `+` 다음 옆에 서명 `[!UICONTROL ACPExtensionEvent]`
1. 을 선택하여 드릴다운 `[!UICONTROL payload > 0 > payload > 0 > namespace]`. 마지막 항목 아래에 표시된 ID `0` 다음에 해당 `ECID`. 아래에 표시되는 값으로 알 수 있습니다. `namespace` 일치 `ECID`

   ![보증 유효성 확인 ECID](assets/validate-assurance-ecid.png)

   >[!CAUTION]
   >
   >창의 너비로 인해 잘린 ECID 값이 표시될 수 있습니다. 인터페이스에서 핸들 막대를 선택하고 왼쪽으로 드래그하여 전체 ECID를 표시하면 됩니다.

향후 단원에서는 Assurance를 사용하여 데이터 스트림에서 활성화된 Adobe 애플리케이션에 도달하기 위해 완전히 처리된 페이로드를 확인합니다.

이제 페이지에서 실행되는 XDM 개체와 데이터 수집의 유효성을 검사하는 방법에 대한 지식이 있으면 Platform Web SDK를 사용하여 개별 Adobe 애플리케이션을 설정할 수 있습니다.

[다음: ](setup-experience-platform.md)

>[!NOTE]
>
>Adobe Experience Platform Web SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나, 일반적인 피드백을 공유하거나, 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오. [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
