---
title: Bootcamp - Real-time CDP - 대상자를 빌드하고 조치 수행 - 대상자를 DV360으로 보내기
description: Bootcamp - Real-time CDP - 대상 구축 및 작업 - 대상을 DV360으로 전송
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
feature: Destinations
exl-id: 31f46e37-f1c0-4730-8520-1ccd98df6501
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# 1.5 조치 취하기: 대상자를 Facebook으로 보내기

[Adobe Experience Platform](https://experience.adobe.com/platform)(으)로 이동합니다. 로그인하면 Adobe Experience Platform 홈페이지에 접속하게 됩니다.

![데이터 수집](./images/home.png)

계속하려면 **샌드박스**&#x200B;를 선택해야 합니다. 선택할 샌드박스 이름이 ``Bootcamp``입니다. 화면 상단의 파란색 선에 있는 텍스트 **[!UICONTROL 프로덕션]**&#x200B;을(를) 클릭하면 됩니다. 적절한 [!UICONTROL 샌드박스]를 선택하면 화면이 변경되고 이제 전용 [!UICONTROL 샌드박스]에 있게 됩니다.

![데이터 수집](./images/sb1.png)

왼쪽 메뉴에서 **대상**(으)로 이동한 다음 **카탈로그**(으)로 이동합니다. 그러면 **대상 카탈로그**&#x200B;가 표시됩니다. **대상**&#x200B;에서 **Facebook 사용자 지정 대상** 카드의 **대상 활성화**&#x200B;를 클릭합니다.

![RTCDP](./images/rtcdpgoogleseg.png)

대상 **bootcamp-facebook**&#x200B;을(를) 선택하고 **다음**&#x200B;을 클릭합니다.

![RTCDP](./images/rtcdpcreatedest2.png)

사용 가능한 대상 목록에서 이전 연습에서 만든 대상을 선택합니다. **다음**&#x200B;을 클릭합니다.

![RTCDP](./images/rtcdpcreatedest3.png)

**매핑** 페이지에서 **변환 적용** 확인란이 활성화되어 있는지 확인하십시오. **다음**&#x200B;을 클릭합니다.

![RTCDP](./images/rtcdpcreatedest4a.png)

**대상자 일정** 페이지에서 **대상자의 원본**&#x200B;을(를) 선택하고 **고객에서 직접**(으)로 설정합니다. **다음**&#x200B;을 클릭합니다.

![RTCDP](./images/rtcdpcreatedest4.png)

마지막으로 **검토** 페이지에서 **마침**&#x200B;을 클릭합니다.

![RTCDP](./images/rtcdpcreatedest5.png)

이제 대상자가 Facebook 사용자 지정 대상자에 연결됩니다. 고객이 이 대상에 적격일 때마다 Facebook 측의 사용자 정의 대상에 해당 고객을 포함하라는 신호가 Facebook 서버측으로 전송됩니다.

facebook의 Adobe Experience Platform 대상은 사용자 지정 대상 아래에 있습니다.

![RTCDP](./images/rtcdpcreatedest5b.png)

이제 Facebook에서 사용자 지정 대상이 표시되는 것을 볼 수 있습니다.

![RTCDP](./images/rtcdpcreatedest5a.png)

[사용자 흐름 1로 돌아가기](./uc1.md)

[모든 모듈로 돌아가기](../../overview.md)
