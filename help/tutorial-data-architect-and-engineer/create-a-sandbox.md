---
title: 샌드박스 만들기
seo-title: Create a sandbox | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 샌드박스 만들기
description: 이 단원에서는 자습서의 나머지 부분에서 사용할 수 있는 개발 환경 샌드박스를 만듭니다.
role: Data Architect, Data Engineer
feature: Sandboxes
kt: 4348
thumbnail: 4348-create-a-sandbox.jpg
exl-id: a04afada-52a1-4812-8fa2-14be72e68614
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 2%

---

# 샌드박스 만들기

<!--25min-->

이 단원에서는 나머지 자습서에 사용할 개발 환경 샌드박스를 만듭니다.

샌드박스는 리소스와 데이터를 프로덕션 환경과 혼합하지 않고 기능을 테스트할 수 있는 분리된 환경을 제공합니다. 자세한 내용은 [샌드박스 설명서](https://experienceleague.adobe.com/docs/experience-platform/sandbox/home.html?lang=ko).

**데이터 설계자** 및 **데이터 엔지니어** 은 이 자습서의 외부에 샌드박스를 만들어야 합니다.

연습을 시작하기 전에 샌드박스에 대한 자세한 내용을 보려면 이 짧은 비디오를 시청하십시오.
>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

## 필요한 권한

에서 [권한 구성](configure-permissions.md) 이 단원을 완료하는 데 필요한 모든 액세스 컨트롤을 설정합니다.

<!--
* Permission items **[!UICONTROL Sandbox Administration]** > **[!UICONTROL View Sandboxes]** and **[!UICONTROL Manage Sandboxes]**
* Permission item **[!UICONTROL Sandboxes]** > **[!UICONTROL Prod]**
* User-role access to the `Luma Tutorial Platform` product profile
* Admin-level access to the `Luma Tutorial Platform` product profile
-->

## 샌드박스 만들기

샌드박스를 만들겠습니다.

1. 에 로그인합니다. [Adobe Experience Platform](https://experience.adobe.com/platform) 인터페이스
1. 이동 **[!UICONTROL 샌드박스]** 왼쪽 탐색
1. 선택 **[!UICONTROL 샌드박스 만들기]** 오른쪽 상단에서
   ![샌드박스 만들기 선택](assets/sandbox-createSandbox.png)

1. 선택 **[!UICONTROL 개발]** 로서의 **[!UICONTROL 유형]**
1. 샌드박스 이름을 지정합니다 `luma-tutorial` (끝에 이름을 추가하는 것이 좋습니다.)
1. 자습서에 제목 지정 `Luma Tutorial` (끝에 이름을 추가하는 것이 좋습니다.)
1. **[!UICONTROL 만들기]** 버튼을 선택합니다
   ![샌드박스 만들기](assets/sandbox-nameSandbox.png)
   >[!NOTE]
   >
   >샌드박스 이름 및 제목에 임의의 값을 사용할 수 있지만 자습서 전체에서 이러한 레이블을 참조할 것이므로 제안된 값을 따르는 것이 좋습니다. 이 자습서를 완료하는 조직에 여러 사람이 있는 경우 luma-tutorial-ignatisjrely와 같이 샌드박스 제목 및 이름의 끝에 이름을 추가하는 것이 좋습니다.

샌드박스를 만드는 데 약 30초 정도 걸리며 그 동안 &quot;[!UICONTROL 만들기]&quot; 상태가 표시됩니다. 샌드박스가 완전히 만들어지면 &quot;&quot;으로 표시됩니다.[!UICONTROL 활성]&quot;:
![활성 상태](assets/sandbox-active.png)

샌드박스가 &quot;[!UICONTROL 활성]&quot;을 클릭하여 다음 연습을 계속 진행합니다.

## 제품 프로필에 새 샌드박스 추가

샌드박스가 활성화되면 사용하려면 제품 프로필에 샌드박스를 포함해야 합니다. 제품 프로필에 추가하려면 다음을 수행하십시오.

1. 별도의 브라우저 탭에서, [Admin Console](https://adminconsole.adobe.com)
1. 이동 **[!UICONTROL 제품 > Adobe Experience Platform]**
1. 를 엽니다. `Luma Tutorial Platform` 프로필

   ![제품 프로필 선택](assets/sandbox-selectProfile.png)

1. 로 이동합니다. **[!UICONTROL 권한]** 탭

1. 설정 [!UICONTROL 샌드박스] row, select **[!UICONTROL 편집]**

   ![편집 선택](assets/sandbox-selectSandboxes.png)

1. _제거_ a **[!UICONTROL Prod]** 원래 프로필에 할당한 샌드박스
1. 을(를) 선택합니다 **[!UICONTROL +]** 아이콘을 클릭하여 새 `Luma Tutorial` 오른쪽 열에 샌드박스
1. 선택 **[!UICONTROL 저장]** 업데이트된 권한을 저장하려면

   ![샌드박스를 다른 열로 이동](assets/sandbox-addLumaTutorial.png)

1. Experience Platform을 사용하여 브라우저 탭으로 돌아갑니다
1. 페이지를 다시 로드(또는 Shift-다시 로드)하고 이제 `Luma Tutorial` 샌드박스 또는 샌드박스 드롭다운에 표시되어야 함
1. 로 전환 `Luma Tutorial` 아직 안에 없는 경우 샌드박스

   ![샌드박스 확인](assets/sandbox-confirmDropdown.png)

좋습니다. 샌드박스를 만들어 사용할 준비가 되었습니다 [개발자 콘솔 및 Postman 설정](set-up-developer-console-and-postman.md)!
