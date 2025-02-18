---
title: Real-Time CDP - 대상 구축 및 작업 - Google DV360과 같은 Advertising 대상 구성
description: Real-Time CDP - 대상 구축 및 작업 - Google DV360과 같은 Advertising 대상 구성
kt: 5342
doc-type: tutorial
exl-id: 2498c80f-8ba8-4563-ac37-52f461f706f4
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 1%

---

# 2.3.2 Google DV360과 같은 Advertising 대상 구성

>[!IMPORTANT]
>
>아래 콘텐츠는 부분적으로 FYI용입니다. 이러한 대상이 인스턴스에 이미 있으면 **NOT**&#x200B;에서 DV360에 대한 새 대상을 구성해야 합니다. 이 경우 이미 대상이 생성되었으며 다음 연습에서 사용할 수 있습니다.

[Adobe Experience Platform](https://experience.adobe.com/platform)(으)로 이동합니다. 로그인하면 Adobe Experience Platform 홈페이지에 접속하게 됩니다.

![데이터 수집](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

계속하려면 **샌드박스**&#x200B;를 선택해야 합니다. 선택할 샌드박스 이름이 ``--aepSandboxName--``입니다. 적절한 [!UICONTROL 샌드박스]를 선택하면 화면이 변경되고 이제 전용 [!UICONTROL 샌드박스]에 있게 됩니다.

![데이터 수집](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

왼쪽 메뉴에서 **대상**(으)로 이동한 다음 **카탈로그**(으)로 이동합니다. 그러면 **대상 카탈로그**&#x200B;가 표시됩니다.

![RTCDP](./images/rtcdp.png)

**대상**&#x200B;에서 **Google Display &amp; Video 360**&#x200B;을 클릭한 다음 **+ 설정**&#x200B;을 클릭합니다.

![RTCDP](./images/rtcdpgoogle.png)

그러면 이걸 보게 될 거야. **대상에 연결**&#x200B;을 클릭합니다.

![RTCDP](./images/rtcdpgooglecreate1.png)

다음 화면에서는 대상을 Google DV360으로 구성할 수 있습니다.

![RTCDP](./images/rtcdpgooglecreatedest.png)

**이름** 및 **설명** 필드에 값을 입력하십시오.

필드 **계정 ID**&#x200B;은(는) DV360 계정의 **광고주 ID**&#x200B;입니다. 여기에서 찾을 수 있습니다.

![RTCDP](./images/rtcdpgoogledv360advid.png)

**계정 유형**&#x200B;은(는) **광고주 초대**(으)로 설정해야 합니다.

이제 네가 이걸 가지고있어. **다음**&#x200B;을 클릭합니다.

![RTCDP](./images/rtcdpgoogldv360new.png)

>[!NOTE]
>
>Google에서 Google DV360으로 데이터를 보내려면 AdobeAdobe Experience Platform 를 허용 목록에 추가해야 합니다. 이 데이터 흐름을 활성화하려면 Google 계정 관리자에게 문의하십시오.

대상을 만들면 이 항목이 표시됩니다. 선택적으로 데이터 거버넌스 정책을 선택할 수 있습니다. 그런 다음 **저장 및 종료**&#x200B;를 클릭합니다.

![RTCDP](./images/rtcdpcreatedest1.png)

그러면 사용 가능한 대상 목록이 표시됩니다.
다음 연습에서는 이전 연습에서 빌드한 대상을 Google DV360 대상에 연결합니다.

## 다음 단계

[2.3.3 실행으로 이동: 대상자를 DV360으로 보내기](./ex3.md){target="_blank"}

[실시간 CDP로 돌아가기 - 대상자를 빌드하고 작업 수행](./real-time-cdp-build-a-segment-take-action.md){target="_blank"}

[모든 모듈](./../../../../overview.md){target="_blank"}(으)로 돌아가기
