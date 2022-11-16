---
title: 태그 속성 구성
description: 에서 태그 속성을 구성하는 방법을 알아봅니다 [!UICONTROL 데이터 수집] 인터페이스.
exl-id: 0c4b00cc-34e3-4d08-945e-3fd2bc1b6ccf
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 10%

---

# 태그 속성 구성

에서 태그 속성을 구성하는 방법을 알아봅니다 [!UICONTROL 데이터 수집] 인터페이스.

Adobe Experience Platform의 태그는 Adobe의 차세대 태그 관리 기능입니다. 태그를 통해 관련 고객 경험을 강화하는 데 필요한 모든 분석, 마케팅 및 광고 태그를 고 관리하는 간단한 방법을 고객에게 제공합니다. 추가 정보 [태그](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html) 를 참조하십시오.

## 전제 조건

단원을 완료하려면 태그 속성을 만들 수 있는 권한이 있어야 합니다. 또한 태그를 기준선으로 이해할 수 있는 것도 유용합니다.

>[!NOTE]
>
> 이제 platform launch(클라이언트측)가 [태그](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ko-KR)

## 학습 목표

이 단원에서는 다음 작업을 수행합니다.

* 모바일 태그 확장을 설치하고 구성합니다.
* SDK 설치 지침을 생성합니다.

## 초기 설정

1. 새 모바일 태그 속성을 만듭니다.
   1. 에서 [데이터 수집 인터페이스](https://experience.adobe.com/data-collection/){target=&quot;_blank&quot;}, 선택 **[!UICONTROL 태그]** 왼쪽 탐색
   1. 선택 **[!UICONTROL 새 속성]**

      ![태그 속성 만들기](assets/mobile-tags-new-property.png).
   1. 대상 **[!UICONTROL 이름]**, 입력 `Mobile SDK Course`.
   1. 대상 **[!UICONTROL 플랫폼]**, 선택 **[!UICONTROL 모바일]**.
   1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

      ![태그 속성 구성](assets/mobile-tags-property-config.png)

      >[!NOTE]
      >
      > 이 자습서에서 수행하는 것과 같은 에지 기반 모바일 sdk 구현에 대한 기본 동의 설정은 [!UICONTROL 동의 확장] 그리고 [!UICONTROL 개인 정보 보호] 태그 속성 구성에서 를 설정합니다. 이 단원의 뒷부분에서 동의 확장을 추가하고 구성합니다. 자세한 내용은 [설명서](https://aep-sdks.gitbook.io/docs/resources/privacy-and-gdpr).


1. 새 속성을 엽니다.
1. 라이브러리 만들기:

   1. 이동 **[!UICONTROL 게시 흐름]** 을 클릭합니다.
   1. 선택 **[!UICONTROL 라이브러리 추가]**.

      ![라이브러리 추가 를 선택합니다](assets/mobile-tags-create-library.png)

   1. 대상 **[!UICONTROL 이름]**, 입력 `Initial Build`.
   1. 대상 **[!UICONTROL 환경]**, 선택 **[!UICONTROL 개발]**.
   1. 선택  **[!UICONTROL 변경된 모든 리소스 추가]**.
   1. 선택 **[!UICONTROL 저장 및 개발에 빌드]**.

      ![라이브러리 빌드](assets/mobile-tags-save-library.png)

   1. 마지막으로, **[!UICONTROL 작업 라이브러리]**.
      ![을(를) 작업 라이브러리로 선택합니다](assets/mobile-tags-working-library.png)
1. 선택 **[!UICONTROL 확장]**.

   Mobile Core 및 프로필 확장이 미리 설치되어 있어야 합니다.

1. 선택 **[!UICONTROL 카탈로그]**.

   ![초기 설정](assets/mobile-tags-starting.png)

1. 를 사용하십시오 [!UICONTROL 검색] 다음 확장을 설치하고 설치하는 기능. 이러한 확장 중 어느 것도 구성을 필요로 하지 않습니다.
   * 신원
   * AEP Assurance

## 확장 구성

1. 설치 **동의** 확장.

   이 자습서를 사용하려면 을(를) 선택합니다. **[!UICONTROL 보류 중]**. 에서 동의 확장에 대해 자세히 알아보십시오 [설명서](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network).

   ![동의 설정](assets/mobile-tags-extension-consent.png)

1. 설치 **Adobe Experience Platform Edge Network** 확장.

   에서 **[!UICONTROL Edge 구성]** 드롭다운에서 만든 데이터 스트림을 선택합니다. [이전 단계](create-datastream.md).

1. 선택 **[!UICONTROL 라이브러리 및 빌드에 저장]**.

   ![edge 네트워크 설정](assets/mobile-tags-extension-edge.png)


## SDK 설치 지침 생성

1. 선택 **[!UICONTROL 환경]**.

1. 을(를) 선택합니다 **[!UICONTROL 개발]** install 아이콘.

   ![환경 홈 화면](assets/mobile-tags-environments.png)

1. 선택 **[!UICONTROL iOS]**.

1. 선택 **[!UICONTROL Swift]**.

   ![설치 지침](assets/mobile-tags-install-instructions.png)

1. 설치 지침은 구현에 적합한 시작 지점을 제공합니다.

   추가 정보를 찾을 수 있습니다 [여기](https://aep-sdks.gitbook.io/docs/getting-started/get-the-sdk).

   * **[!UICONTROL 환경 파일 ID]**: 이 고유 ID는 개발 환경을 가리킵니다. 이 값을 확인하십시오. 프로덕션/스테이징/개발에는 모두 서로 다른 ID 값이 있습니다.
   * **[!UICONTROL Podfile]**: CocoaPod는 SDK 버전 및 다운로드를 관리하는 데 사용됩니다. 자세한 내용은 [설명서](https://cocoapods.org/).
   * **[!UICONTROL 초기화 코드]**: 이 코드 블록은 필요한 SDK를 가져오고 launch에서 확장을 등록하는 방법을 보여 줍니다.

>[!NOTE]
>설치 지침은 시작 지점으로 간주되어야 하며 최종 설명서가 아닙니다. 최신 SDK 버전 및 코드 샘플은 [설명서](https://aep-sdks.gitbook.io/docs/).

## 모바일 태그 아키텍처

이전의 Launch인 태그의 웹 버전에 익숙한 경우 모바일의 차이점을 이해하는 것이 중요합니다.

웹에서 태그 속성이 JavaScript로 렌더링된 후(일반적으로) 클라우드에서 호스팅됩니다. 해당 JS 파일은 웹 사이트에서 직접 참조됩니다.

모바일 태그 속성에서, 규칙 및 구성은 클라우드에서 호스팅되는 JSON 파일에 렌더링됩니다. JSON 파일은 모바일 앱에서 Mobile Core 확장에서 다운로드하여 읽습니다. 확장은 함께 작동하는 별도의 SDK입니다. 태그 속성에 확장을 추가하는 경우 앱도 업데이트해야 합니다. 확장 설정을 변경하거나 규칙을 만드는 경우 업데이트된 태그 라이브러리를 게시하면 해당 변경 사항이 앱에 반영됩니다.

다음: **[SDK 설치](install-sdks.md)**

>[!NOTE]
>
>Adobe Experience Platform Mobile SDK에 대한 학습에 시간을 내주셔서 감사합니다. 질문이 있거나 일반 피드백을 공유하거나 향후 컨텐츠에 대한 제안 사항이 있는 경우 해당 정보를 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)