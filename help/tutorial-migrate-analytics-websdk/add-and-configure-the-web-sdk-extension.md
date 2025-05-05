---
title: 웹 SDK 확장 추가 및 구성
description: Tags 속성에 웹 SDK 확장을 추가 및 구성하여 마이그레이션을 완료하는 데 필요한 기능을 제공하는 방법에 대해 알아봅니다.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16758
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---


# 웹 SDK 확장 추가 및 구성

Tags 속성에서 웹 SDK 확장을 추가 및 구성하여 마이그레이션을 완료하는 데 필요한 기능을 제공하는 방법에 대해 알아봅니다.
확장을 추가하고 구성하려면 다음 단계를 따르십시오.

1. Experience Platform 데이터 수집으로 이동합니다. 이 작업은 다음 두 가지 방법 중 하나로 수행할 수 있습니다.
   1. [Adobe Experience Platform 인터페이스](https://platform.adobe.com/)(으)로 이동한 다음 왼쪽 탐색 아래의 **[!UICONTROL 태그]**&#x200B;를 선택합니다.

      ![태그 1](assets/access-tags-1.jpg)에 액세스
   1. Platform에 액세스할 수 없는 경우에는 창의 오른쪽 상단에 있는 애플리케이션 전환기(9점)를 사용하고 데이터 수집(Experience.Adobe.com에 로그인한 후)을 선택할 수 있습니다.

      ![액세스 태그 2](assets/access-tags-2.jpg)
1. 웹 SDK으로 마이그레이션할 태그 속성을 찾아 선택합니다.
1. 태그 속성의 왼쪽 탐색에서 **[!UICONTROL 확장]**&#x200B;을 선택합니다.
1. 사용 가능한 모든 확장 목록을 보려면 맨 위의 **[!UICONTROL 카탈로그]**&#x200B;를 선택하십시오.
1. **[!UICONTROL Adobe Experience Platform Web SDK]** 확장을 검색하여 선택한 다음 오른쪽의 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

   ![웹 SDK 확장 찾기](assets/find-the-websdk-extension.jpg){style="border:1px solid lightslategray"}

1. 확장 구성 설정이 나타납니다. 데이터스트림 섹션을 찾아 이 마이그레이션에 사용할 Experience Platform 샌드박스를 설정합니다(세 환경 모두의 &quot;환경&quot; 드롭다운). Adobe Analytics만 마이그레이션하고 Adobe Experience Platform으로 데이터를 보내지 않을 경우 **프로덕션** 샌드박스를 선택하십시오. 해당 애플리케이션에서 사용하기 위해 이 행동 분석 데이터를 Experience Platform에게 전송하려는 경우 해당 애플리케이션에 사용할 샌드박스를 선택합니다. 마이그레이션을 완료하고 Platform 서비스 추가/테스트를 완료할 때까지 처음에 개발 샌드박스를 선택하려고 할 수 있습니다.
1. 매우 중요한 것은 프로덕션, 스테이징 및 개발 환경에 대한 이전 단계에서 생성한 데이터스트림을 선택하여 여기 태그의 코드와 설정을 Edge에 연결한다는 것입니다.

   ![데이터 스트림 선택](assets/choose-datastreams.jpg){style="border:1px solid lightslategray"}

1. 아래로 스크롤하여 **ID** 설정이 기본적으로 선택되어 있는지 확인합니다. 웹 SDK으로 마이그레이션할 때 사이트 방문자를 올바르게 식별하는 데 도움이 되므로 이러한 확인란을 선택한 상태로 두십시오. 자세한 내용은 아래 링크를 제공하는 설명서에서 확인할 수 있습니다.

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

>[!NOTE]
>
>이제 Tags 속성에 Web SDK 확장의 기본 설치 및 구성이 포함됩니다. 이 마이그레이션 자습서에서는 웹 SDK 확장의 일부를 사용하여 데이터 요소와 규칙을 만들거나 수정하지만 자습서에서 확장 구성 항목을 더 이상 변경하지 않습니다. 추가 구성 항목은 추가 사용 사례에 사용할 수 있으며 사용해야 합니다. 이러한 구성에 대한 자세한 설명서는 [웹 SDK 태그 확장 구성](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/web-sdk-extension-configuration)을 참조하십시오.
