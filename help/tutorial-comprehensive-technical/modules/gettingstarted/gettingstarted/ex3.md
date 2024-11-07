---
title: 시작하기 - 데이터 스트림 만들기
description: 시작하기 - 데이터 스트림 만들기
kt: 5342
doc-type: tutorial
source-git-commit: 7d2f5f842559b2d6d9f115f3993268a4b36a0fe0
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 1%

---

# 0.3 데이터 스트림 만들기

[https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)(으)로 이동합니다. 이전 연습이 끝나면 이제 두 개의 데이터 수집 속성이 있습니다. 하나는 웹용, 다른 하나는 모바일용 입니다.

![DSN](./images/launchprop.png)

이러한 속성을 사용할 준비가 거의 되었지만 이러한 속성을 사용하여 데이터 수집을 시작하려면 먼저 데이터 스트림을 설정해야 합니다. 데이터 스트림의 개념과 연습 1.2에서 데이터 스트림이 의미하는 바에 대한 자세한 정보를 얻을 수 있습니다.

지금은 다음 단계를 따르십시오.

## 0.3.1 웹용 데이터스트림 만들기

**[!UICONTROL 데이터스트림]** 또는 **[!UICONTROL 데이터스트림(Beta)]**&#x200B;을 클릭합니다.

![왼쪽 탐색에서 Edge 구성 아이콘을 클릭합니다](./images/edgeconfig1a.png)

화면 오른쪽 상단에서 샌드박스 이름을 선택합니다. 이름은 `--aepSandboxId--`이어야 합니다.

![왼쪽 탐색에서 Edge 구성 아이콘을 클릭합니다](./images/edgeconfig1b.png)

**[!UICONTROL 새 데이터 스트림]**&#x200B;을 클릭합니다.

![왼쪽 탐색에서 Edge 구성 아이콘을 클릭합니다](./images/edgeconfig1.png)

**[!UICONTROL 친숙한 이름]**&#x200B;에 대해, 선택적 설명에 대해 `--demoProfileLdap-- - Demo System Datastream`을(를) 입력하십시오. 이벤트 스키마의 경우 **데모 시스템 - 웹 사이트에 대한 이벤트 스키마(전역 v1.1)**&#x200B;를 선택합니다. **저장**&#x200B;을 클릭합니다.

![Edge 구성 이름 지정 및 저장](./images/edgeconfig2.png)

그러면 이걸 보게 될 거야. **서비스 추가**&#x200B;를 클릭합니다.

![Edge 구성 이름 지정 및 저장](./images/edgeconfig3.png)

추가 필드를 표시할 서비스 **[!UICONTROL Adobe Experience Platform]**&#x200B;을(를) 선택하십시오. 그러면 이걸 보게 될 거야.

이벤트 데이터 세트의 경우 **데모 시스템 - 웹 사이트의 이벤트 데이터 세트(전역 v1.1)**&#x200B;를 선택하고 프로필 데이터 세트의 경우 **데모 시스템 - 웹 사이트의 프로필 데이터 세트(전역 v1.1)**&#x200B;를 선택합니다. **저장**&#x200B;을 클릭합니다.

![Edge 구성 이름 지정 및 저장](./images/edgeconfig4.png)

이제 이 항목을 볼 수 있습니다.

![Edge 구성 이름 지정 및 저장](./images/edgeconfig5.png)

이제 다 됐습니다. [모듈 1.1](./../../../modules/datacollection/module1.1/data-ingestion-launch-web-sdk.md)에서 Web SDK와 모든 기능을 구성하는 방법에 대해 자세히 알아봅니다.

왼쪽 메뉴에서 **[!UICONTROL 태그]**&#x200B;를 클릭합니다.

검색 결과를 필터링하여 두 개의 데이터 수집 속성을 확인합니다. **Web**&#x200B;의 속성을 클릭하여 엽니다.

![Edge 구성 이름 지정 및 저장](./images/edgeconfig10a.png)

그러면 이걸 보게 될 거야. **확장**&#x200B;을 클릭합니다.

![Edge 구성 이름 지정 및 저장](./images/edgeconfig11.png)

Adobe Experience Platform 웹 SDK 확장에서 **구성**&#x200B;을 클릭합니다.

![Edge 구성 이름 지정 및 저장](./images/edgeconfig12.png)

그러면 이걸 보게 될 거야. **데이터스트림**&#x200B;의 경우 현재 1로 설정된 더미 값이 표시됩니다. 이제 **목록에서 선택** 라디오 단추를 클릭해야 합니다. 드롭다운 목록에서 이전에 생성한 데이터 스트림을 선택합니다.

![Edge 구성 이름 지정 및 저장](./images/edgeconfig13.png)

**데이터 스트림**&#x200B;을(를) 선택했는지 확인하십시오. 팁: `--demoProfileLdap--`을(를) 입력하여 드롭다운에서 결과를 쉽게 필터링할 수 있습니다.

![Edge 구성 이름 지정 및 저장](./images/edgeconfig14.png)

**데이터 수집**&#x200B;이 표시될 때까지 아래로 스크롤합니다. **클릭 데이터 수집 사용**&#x200B;에 대한 확인란이 활성화되어 있지 않은지 확인하십시오. 변경 내용을 저장하려면 **저장**&#x200B;을 클릭하세요.

![Edge 구성 이름 지정 및 저장](./images/edgeconfig14a.png)

**게시 흐름**(으)로 이동합니다.

![Edge 구성 이름 지정 및 저장](./images/edgeconfig15.png)

**Main**&#x200B;의 **..**&#x200B;을(를) 클릭한 다음 **편집**&#x200B;을(를) 클릭합니다.

![Edge 구성 이름 지정 및 저장](./images/edgeconfig16.png)

**변경된 모든 리소스 추가**&#x200B;를 클릭한 다음 **개발을 위한 저장 및 빌드**&#x200B;를 클릭합니다.

![Edge 구성 이름 지정 및 저장](./images/edgeconfig17.png)

변경 사항이 이제 게시되고 있으며 몇 분 후에 준비됩니다.

## 0.3.2 모바일용 데이터스트림 만들기

[https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)(으)로 이동합니다.

**[!UICONTROL 데이터스트림]** 또는 **[!UICONTROL 데이터스트림(Beta)]**&#x200B;을 클릭합니다.

![왼쪽 탐색에서 데이터 스트림 아이콘 클릭](./images/edgeconfig1a.png)

화면 오른쪽 상단에서 샌드박스 이름을 선택합니다. 이름은 `--aepSandboxId--`이어야 합니다.

![왼쪽 탐색에서 Edge 구성 아이콘을 클릭합니다](./images/edgeconfig1b.png)

**[!UICONTROL 새 데이터 스트림]**&#x200B;을 클릭합니다.

![왼쪽 탐색에서 데이터 스트림 아이콘 클릭](./images/edgeconfig1.png)

**[!UICONTROL 친숙한 이름]**&#x200B;에 대해, 선택적 설명에 대해 `--demoProfileLdap-- - Demo System Datastream (Mobile)`을(를) 입력하십시오. 이벤트 스키마의 경우 **데모 시스템 - 모바일 앱용 이벤트 스키마(전역 v1.1)**&#x200B;를 선택하십시오. **저장**&#x200B;을 클릭합니다.

**[!UICONTROL 저장]**&#x200B;을 클릭합니다.

![데이터 스트림 이름 지정 및 저장](./images/edgeconfig2m.png)

그러면 이걸 보게 될 거야. **서비스 추가**&#x200B;를 클릭합니다.

![데이터 스트림 이름 지정 및 저장](./images/edgeconfig3m.png)

추가 필드를 표시할 서비스 **[!UICONTROL Adobe Experience Platform]**&#x200B;을(를) 선택하십시오. 그러면 이걸 보게 될 거야.

이벤트 데이터 세트의 경우 **데모 시스템 - 모바일 앱용 이벤트 데이터 세트(전역 v1.1)**&#x200B;를 선택하고 프로필 데이터 세트의 경우 **데모 시스템 - 모바일 앱용 프로필 데이터 세트(전역 v1.1)**&#x200B;를 선택합니다. **저장**&#x200B;을 클릭합니다.

![데이터 스트림 구성 이름 지정 및 저장](./images/edgeconfig4m.png)

그러면 이걸 보게 될 거야.

![데이터 스트림 구성 이름 지정 및 저장](./images/edgeconfig5m.png)

이제 모바일용 Adobe Experience Platform 데이터 수집 클라이언트 속성에서 데이터 스트림을 사용할 준비가 되었습니다.

**태그**(으)로 이동하여 검색 결과를 필터링하여 두 개의 데이터 수집 속성을 확인하세요. **Mobile**&#x200B;의 속성을 클릭하여 엽니다.

![Edge 구성 이름 지정 및 저장](./images/edgeconfig10am.png)

그러면 이걸 보게 될 거야. **확장**&#x200B;을 클릭합니다.

![Edge 구성 이름 지정 및 저장](./images/edgeconfig11m.png)

**Adobe Experience Platform Edge Network** 확장에서 **구성**&#x200B;을 클릭합니다.

![Edge 구성 이름 지정 및 저장](./images/edgeconfig12m.png)

그러면 이걸 보게 될 거야. 이제 방금 구성한 올바른 샌드박스 및 데이터 스트림을 선택해야 합니다. 사용할 샌드박스는 `--aepSandboxId--`이고 데이터 스트림은 `--demoProfileLdap-- - Demo System Datastream (Mobile)`입니다.

**Edge Network 도메인**&#x200B;의 경우 기본 도메인인 **edge.adobedc.net**&#x200B;을(를) 사용하십시오.

변경 내용을 저장하려면 **저장**&#x200B;을 클릭하세요.

![Edge 구성 이름 지정 및 저장](./images/edgeconfig13m.png)

**게시 흐름**(으)로 이동합니다.

![Edge 구성 이름 지정 및 저장](./images/edgeconfig15m.png)

**Main** 옆에 있는 **..**&#x200B;을 클릭한 다음 **편집**&#x200B;을 클릭합니다.

![Edge 구성 이름 지정 및 저장](./images/edgeconfig16m.png)

**변경된 모든 리소스 추가**&#x200B;를 클릭한 다음 **개발을 위한 저장 및 빌드**&#x200B;를 클릭합니다.

![Edge 구성 이름 지정 및 저장](./images/edgeconfig17m.png)

변경 사항이 이제 게시되고 있으며 몇 분 후에 준비됩니다.

다음 단계: [0.4 웹 사이트 사용](./ex4.md)

[모듈 0으로 돌아가기](./getting-started.md)

[모든 모듈로 돌아가기](./../../../overview.md)