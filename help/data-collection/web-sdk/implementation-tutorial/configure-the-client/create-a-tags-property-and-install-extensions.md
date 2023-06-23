---
title: Adobe Experience Platform 태그 속성 만들기 및 확장 설치
description: Adobe Experience Platform 태그 속성 만들기 및 확장 설치
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 7403059f-b34c-48e0-9efe-b2db7a9afb27
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 1%

---

# Adobe Experience Platform 태그 속성 만들기 및 확장 설치

이제 페이지 코드에서 데이터 및 이벤트를 데이터 레이어로 푸시하고 있으므로 마케터가 데이터 레이어에서 데이터를 읽고 이 데이터를 Adobe Experience Platform에 보낼 차례입니다. 이 경우 일반적으로 두 개의 JavaScript 라이브러리가 필요합니다.

* Adobe 클라이언트 데이터 레이어: 이전 단계에서 데이터 레이어 배열을 만들고 개체를 데이터 레이어 배열에 푸시했습니다. 데이터에 액세스하려면 Adobe 클라이언트 데이터 레이어 JavaScript 라이브러리를 로드해야 합니다. 이 라이브러리는 데이터 레이어 변경 사항 및 이벤트에 대한 알림을 받고 데이터에 액세스하는 간단한 방법을 제공합니다.
* Adobe Experience Platform Web SDK: 이 JavaScript 라이브러리는 Adobe Experience Platform Edge Network와 통신합니다. SDK는 ID, 동의, 데이터 수집, 개인화, 대상자 등을 처리합니다.

이러한 개별 라이브러리를 웹 사이트에 로드하고 직접 사용할 수 있지만 [Adobe Experience Platform 태그](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html). 태그를 사용하면 HTML에 단일 스크립트를 포함하고 태그 사용자 인터페이스를 사용하여 Adobe 클라이언트 데이터 레이어 및 Adobe Experience Platform Web SDK를 모두 배포할 수 있습니다. 태그를 사용하면 여러 가지 중에서 데이터를 보내는 규칙을 만들 수도 있습니다. 이 자습서에서는 이러한 목적으로 태그를 사용하며, 태그가 작동하는 방식에 대한 기본적인 이해를 갖추고 있다고 가정합니다.

## 태그 내에 속성 만들기

아직 안 하셨으면, [태그 내에 속성 만들기](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html#create-or-configure-a-property).

## Adobe 클라이언트 데이터 레이어 확장 설치

확장 카탈로그로 이동하고 확장을 찾은 다음 각각을 클릭하여 Adobe 클라이언트 데이터 레이어 확장을 설치합니다 [!UICONTROL 설치] 단추를 클릭합니다. 구성 화면이 표시됩니다.

![Adobe 클라이언트 데이터 레이어 확장 설치](../../../assets/implementation-strategy/acdl-extension-installation.png)

이 자습서에서는 기본값을 변경할 필요가 없습니다. [!UICONTROL 저장]을 클릭합니다.

## Adobe Experience Platform 웹 SDK 확장 설치

그런 다음 확장 카탈로그에서 확장을 찾아 해당 확장을 클릭하여 Adobe Experience Platform Web SDK 확장을 설치합니다 [!UICONTROL 설치] 단추를 클릭합니다. 구성 화면이 표시됩니다.

![Adobe Experience Platform Web SDK 확장 설치](../../../assets/implementation-strategy/web-sdk-extension-installation.png)

위치 [데이터 스트림 만들기](../configure-the-server/create-a-datastream.md): Adobe Experience Platform Edge Network가 인바운드 데이터를 보낼 위치를 결정하기 위해 참조하는 데이터 스트림을 만들었습니다. Adobe Experience Platform Web SDK에서 Edge Network로 요청을 수행할 때 Edge Network가 참조해야 하는 데이터 스트림을 지정해야 합니다.

이렇게 하려면 다음을 찾습니다. [!UICONTROL 데이터스트림] 필드 를 만들고 이전에 만든 데이터 스트림을 선택합니다. 에서 보았던 것과 동일한 데이터 스트림 환경이 표시됩니다 [데이터 스트림 만들기](../configure-the-server/create-a-datastream.md).

![데이터 스트림 선택](../../../assets/implementation-strategy/web-sdk-datastream-selection.png)

에서 논의된대로 [데이터 스트림 만들기](../configure-the-server/create-a-dataset.md), 이러한 데이터 세트 환경은 태그 환경과 관련이 있습니다. Adobe Experience Platform Web SDK 확장 설치를 완료했다고 가정하고 확장을 포함하는 태그 라이브러리를 만든 다음 라이브러리를 Tags 개발 환경에 게시합니다. 태그 라이브러리가 웹 페이지에 로드되고 Adobe Experience Platform 웹 SDK 확장이 Edge Network에 요청하면 확장에 [!UICONTROL 개발 환경] 데이터 스트림 환경 ID입니다. Edge Network는 해당 ID를 사용하여 [!UICONTROL 개발 환경] 데이터 스트림 환경 및 데이터를 적절한 Adobe 제품으로 전달합니다.

현재는 개발 데이터스트림 환경, 스테이징 데이터스트림 환경 및 프로덕션 데이터스트림 환경 하나만 있습니다. 따라서 확장 구성 사용자 인터페이스에 사전 선택된 구성 요소와 변경 불가능한 구성 요소가 모두 표시됩니다. 그러나 데이터 스트림 사용자 인터페이스를 사용하여 여러 데이터 스트림 개발 환경(사용자 및 공동 작업자)을 만들 수 있습니다. 여러 개발 데이터 스트림 환경이 있는 경우 이 태그 속성에 사용할 환경을 선택할 수 있습니다.

마지막으로 아래로 스크롤하고 선택을 취소합니다 [!UICONTROL 클릭 데이터 수집 활성화]. 기본적으로 SDK는 자동으로 링크를 추적합니다. 그러나 이 자습서에서는 사용자 지정 링크 정보를 사용하여 고유한 링크 클릭을 추적하는 방법을 보여줍니다.

을(를) 클릭합니다 [!UICONTROL 저장] 단추를 클릭하여 Adobe Experience Platform 웹 SDK 확장 설치를 완료합니다.

적절한 확장이 설치되었습니다. 이제 규칙과 데이터 요소를 만들 차례입니다.
