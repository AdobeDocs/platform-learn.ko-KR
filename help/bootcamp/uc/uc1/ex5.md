---
title: Bootcamp - 실시간 CDP - 세그먼트 구축 및 작업 수행 - DV360으로 세그먼트 보내기
description: Bootcamp - 실시간 CDP - 세그먼트 구축 및 작업 수행 - DV360으로 세그먼트 보내기
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 31f46e37-f1c0-4730-8520-1ccd98df6501
source-git-commit: ead28f5631fc430c41e8c756b23dc69ffe19510e
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---

# 1.5 조치 수행: facebook에 세그먼트 보내기

이동 [Adobe Experience Platform](https://experience.adobe.com/platform). 로그인하면 Adobe Experience Platform 홈 페이지가 표시됩니다.

![데이터 수집](./images/home.png)

계속하기 전에 **샌드박스**. 선택할 샌드박스의 이름은 다음과 같습니다 ``Bootcamp``. 이 작업은 텍스트를 클릭하여 수행할 수 있습니다 **[!UICONTROL 프로덕션 제품]** 화면 상단에 있는 파란색 줄에 표시됩니다. 적절한 [!UICONTROL 샌드박스]이렇게 하면 화면 변경 사항이 표시되고 이제 전용 화면에 표시됩니다 [!UICONTROL 샌드박스].

![데이터 수집](./images/sb1.png)

왼쪽 메뉴에서 **대상**, 그런 다음 **카탈로그**. 그러면 **대상 카탈로그**. in **대상**&#x200B;를 클릭합니다. **세그먼트 활성화** on **Facebook 사용자 지정 대상** 카드.

![RTCDP](./images/rtcdpgoogleseg.png)

대상을 선택합니다 **bootcamp-facebook** 을(를) 클릭합니다. **다음**.

![RTCDP](./images/rtcdpcreatedest2.png)

사용 가능한 세그먼트 목록에서 이전 연습에서 만든 세그먼트를 선택합니다. **다음**&#x200B;을 클릭합니다.

![RTCDP](./images/rtcdpcreatedest3.png)

설정 **매핑** 페이지에서 다음을 확인하십시오 **변형 적용** 확인란이 활성화되어 있습니다. **다음**&#x200B;을 클릭합니다.

![RTCDP](./images/rtcdpcreatedest4a.png)

설정 **세그먼트 예약** 페이지에서 을 선택합니다 **대상자의 기원** 다음으로 설정 **고객으로부터 직접**. **다음**&#x200B;을 클릭합니다.

![RTCDP](./images/rtcdpcreatedest4.png)

마지막으로, **검토** 페이지를 클릭한 다음 **완료**.

![RTCDP](./images/rtcdpcreatedest5.png)

이제 세그먼트가 Facebook 사용자 지정 대상에 연결됩니다. 고객이 이 세그먼트를 사용할 수 있을 때마다 Facebook 측의 사용자 지정 대상에 해당 고객을 포함하도록 Facebook 서버측으로 신호가 전송됩니다.

facebook에서는 Adobe Experience Platform 의 사용자 지정 대상 아래에 있는 세그먼트를 찾을 수 있습니다.

![RTCDP](./images/rtcdpcreatedest5b.png)

이제 Facebook에 사용자 지정 대상이 표시되는 것을 볼 수 있습니다.

![RTCDP](./images/rtcdpcreatedest5a.png)

[사용자 흐름 1로 돌아가기](./uc1.md)

[모든 모듈로 돌아가기](../../overview.md)
