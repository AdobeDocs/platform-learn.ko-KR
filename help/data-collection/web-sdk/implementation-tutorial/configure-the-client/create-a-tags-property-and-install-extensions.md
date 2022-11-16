---
title: Adobe Experience Platform 태그 속성 만들기 및 확장 설치
description: Adobe Experience Platform 태그 속성 만들기 및 확장 설치
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 7403059f-b34c-48e0-9efe-b2db7a9afb27
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 1%

---

# Adobe Experience Platform 태그 속성 만들기 및 확장 설치

이제 페이지 내 코드가 데이터 및 이벤트를 데이터 계층에 투입하므로 마케터가 데이터 계층에서 데이터를 읽고 이 데이터를 Adobe Experience Platform에 보낼 차례입니다. 이렇게 하려면 일반적으로 두 개의 JavaScript 라이브러리가 필요합니다.

* Adobe 클라이언트 데이터 레이어: 이전 단계에서는 데이터 레이어 배열을 만들고 객체를 해당 배열에 푸시했습니다. 데이터에 액세스하려면 데이터 레이어 변경 사항 및 이벤트에 대한 알림을 받을 수 있는 방법을 제공하고 데이터에 액세스하는 간단한 방법을 제공하는 Adobe 클라이언트 데이터 레이어 JavaScript 라이브러리를 로드해야 합니다.
* Adobe Experience Platform 웹 SDK: 이 JavaScript 라이브러리는 Adobe Experience Platform Edge Network와 통신합니다. SDK는 ID, 동의, 데이터 수집, 개인화, 대상 등을 처리합니다.

이러한 개별 라이브러리를 웹 사이트에 로드하여 직접 사용할 수 있지만, [Adobe Experience Platform 태그](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html). 태그를 사용하여 HTML에 단일 스크립트를 포함하고 태그 사용자 인터페이스를 사용하여 Adobe 클라이언트 데이터 레이어와 Adobe Experience Platform 웹 SDK를 모두 배포할 수 있습니다. 또한 태그를 사용하여 데이터 전송 규칙 등을 만들 수 있습니다. 이 자습서에서는 이 용도로 태그를 사용할 수 있으며 사용자가 태그 작동 방식을 기본적인 방법으로 이해할 수 있다고 가정합니다.

## 태그 내에 속성 만들기

아직 안하셨다면, [태그 내에 속성 만들기](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html#create-or-configure-a-property).

## Adobe 클라이언트 데이터 레이어 확장 설치

확장 카탈로그로 이동하고 확장을 찾은 다음 각 항목을 클릭하여 Adobe 클라이언트 데이터 레이어 확장을 설치합니다 [!UICONTROL 설치] 버튼을 클릭합니다. 구성 화면이 표시됩니다.

![Adobe 클라이언트 데이터 레이어 확장 설치](../../../assets/implementation-strategy/acdl-extension-installation.png)

이 자습서에서는 기본값을 변경할 필요가 없습니다. [!UICONTROL 저장]을 클릭합니다.

## Adobe Experience Platform 웹 SDK 확장 설치

다음으로, 확장 카탈로그에서 확장을 찾고 각각의 를 클릭하여 Adobe Experience Platform 웹 SDK 확장을 설치합니다 [!UICONTROL 설치] 버튼을 클릭합니다. 구성 화면이 표시됩니다.

![Adobe Experience Platform Web SDK 확장 설치](../../../assets/implementation-strategy/web-sdk-extension-installation.png)

in [데이터 스트림 만들기](../configure-the-server/create-a-datastream.md): Adobe Experience Platform Edge Network가 인바운드 데이터를 보낼 위치를 결정하기 위해 참조하는 데이터 스트림을 만들었습니다. Adobe Experience Platform Web SDK에서 Edge 네트워크에 대한 요청을 할 때 어떤 데이터 스트림 Edge 네트워크를 참조해야 하는지 표시해야 합니다.

이렇게 하려면 [!UICONTROL 데이터 스트림] 필드를 입력하고 이전에 만든 데이터 스트림을 선택합니다. 에서 본 것과 동일한 데이터 스트림 환경이 표시됩니다 [데이터 스트림 만들기](../configure-the-server/create-a-datastream.md).

![데이터 스트림 선택](../../../assets/implementation-strategy/web-sdk-datastream-selection.png)

에서 설명한 대로 [데이터 스트림 만들기](../configure-the-server/create-a-dataset.md)와 같은 데이터 세트 환경은 태그 환경과 관련이 있습니다. 잠시 동안 Adobe Experience Platform 웹 SDK 확장 설치를 완료하고 확장을 포함하는 태그 라이브러리를 만든 다음 라이브러리를 태그 개발 환경에 게시한다고 가정합니다. 태그 라이브러리가 웹 페이지에 로드되고 Adobe Experience Platform Web SDK 확장이 Edge 네트워크에 요청을 수행하면 확장 프로그램에는 다음이 포함됩니다 [!UICONTROL 개발 환경] 데이터 스트림 환경 ID. Edge Network는 그 ID를 사용하여 [!UICONTROL 개발 환경] 데이터 스트림 환경을 만들고 데이터를 적절한 Adobe 제품으로 전달합니다.

현재는 개발 데이터 스트림 환경, 하나의 스테이징 데이터 스트림 환경 및 하나의 프로덕션 데이터 스트림 환경만 있습니다. 확장 구성 사용자 인터페이스에 미리 선택되어 변경할 수 없는 모든 구성 요소가 표시됩니다. 그러나 데이터 스트림 사용자 인터페이스를 사용하여 여러 데이터 스트림 개발 환경(사용자용과 동료용 환경, 아마도 공동 작업자용 환경)을 만들 수 있습니다. 개발 데이터 스트림 환경이 여러 개 있는 경우 이 태그 속성에 사용할 개발 데이터 스트림 환경을 선택할 수 있습니다.

마지막으로 아래로 스크롤하여 선택을 취소합니다 [!UICONTROL 클릭 데이터 수집 활성화]. 기본적으로 SDK는 자동으로 링크를 추적합니다. 그러나 이 자습서에서는 사용자 지정 링크 정보를 사용하여 고유한 링크 클릭 수를 추적하는 방법을 보여줍니다.

을(를) 클릭합니다. [!UICONTROL 저장] 단추를 클릭하여 Adobe Experience Platform 웹 SDK 확장 설치를 완료합니다.

적절한 확장이 설치되었습니다. 이제 규칙과 데이터 요소를 만들 차례입니다.
