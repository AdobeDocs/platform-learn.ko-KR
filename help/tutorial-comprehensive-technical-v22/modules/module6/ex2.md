---
title: 실시간 CDP - 세그먼트 빌드 및 작업 수행 - Google DV360과 같은 광고 대상 구성
description: 실시간 CDP - 세그먼트 빌드 및 작업 수행 - Google DV360과 같은 광고 대상 구성
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 40441815-428a-48dc-a12e-91220d4ba307
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 1%

---

# 6.2 Google DV360과 같은 광고 대상 구성

>[!IMPORTANT]
>
>아래 컨텐츠는 FYI로서 제작되었습니다. **NOT** DV360에 대한 새 대상을 구성해야 합니다. 대상이 이미 생성되었으므로 다음 연습에서 사용할 수 있습니다.

이동 [Adobe Experience Platform](https://experience.adobe.com/platform). 로그인하면 Adobe Experience Platform 홈 페이지가 표시됩니다.

![데이터 수집](../module2/images/home.png)

계속하기 전에 **샌드박스**. 선택할 샌드박스의 이름은 다음과 같습니다 ``--aepSandboxId--``. 이 작업은 텍스트를 클릭하여 수행할 수 있습니다 **[!UICONTROL 프로덕션 제품]** 화면 상단에 있는 파란색 줄에 표시됩니다. 적절한 [!UICONTROL 샌드박스]이렇게 하면 화면 변경 사항이 표시되고 이제 전용 화면에 표시됩니다 [!UICONTROL 샌드박스].

![데이터 수집](../module2/images/sb1.png)

왼쪽 메뉴에서 **대상**, 그런 다음 **카탈로그**. 그러면 **대상 카탈로그**.

![RTCDP](./images/rtcdp.png)

in **대상**&#x200B;를 클릭하고 **Google 디스플레이 및 비디오 360** 을 클릭한 다음 **+ 설정**.

![RTCDP](./images/rtcdpgoogle.png)

그러면 이게 보입니다. 클릭 **대상에 연결**.

![RTCDP](./images/rtcdpgooglecreate1.png)

다음 화면에서 Google DV360으로 대상을 구성할 수 있습니다.

![RTCDP](./images/rtcdpgooglecreatedest.png)

필드에 값을 입력합니다 **이름** 및 **설명**.

필드 **계정 ID** 은 **광고주 ID** DV360 계정 여기에서 확인할 수 있습니다.

![RTCDP](./images/rtcdpgoogledv360advid.png)

다음 **계정 유형** 는 로 설정되어야 합니다. **광고주 초대**.

이제 이걸 가지고 있습니다. **다음**&#x200B;을 클릭합니다.

![RTCDP](./images/rtcdpgoogldv360new.png)

>[!NOTE]
>
>Adobe Experience Platform에서 Google DV360으로 데이터를 전송하려면 Google에서 허용 목록 Adobe을 수행해야 합니다. 이 데이터 흐름을 활성화하려면 Google 계정 관리자에게 문의하십시오.

대상을 만들면 이러한 내용이 표시됩니다. 선택적으로 데이터 거버넌스 정책을 선택할 수 있습니다. 다음을 클릭합니다. **저장 및 종료**.

![RTCDP](./images/rtcdpcreatedest1.png)

그러면 사용 가능한 대상 목록이 표시됩니다.
다음 연습에서는 이전 연습에서 작성한 세그먼트를 Google DV360 대상에 연결합니다.

다음 단계: [6.3 조치 수행: 세그먼트를 DV360으로 보내기](./ex3.md)

[모듈 6으로 돌아가기](./real-time-cdp-build-a-segment-take-action.md)

[모든 모듈로 돌아가기](../../overview.md)
