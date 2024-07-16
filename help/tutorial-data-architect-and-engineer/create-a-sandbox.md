---
title: 샌드박스 만들기
seo-title: Create a sandbox | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 샌드박스 만들기
description: 이 단원에서는 자습서의 나머지 부분에서 사용할 수 있는 개발 환경 샌드박스를 만듭니다.
role: Data Architect, Data Engineer
feature: Sandboxes
jira: KT-4348
thumbnail: 4348-create-a-sandbox.jpg
exl-id: a04afada-52a1-4812-8fa2-14be72e68614
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 2%

---

# 샌드박스 만들기

<!--25min-->

이 단원에서는 자습서의 나머지 부분에서 사용할 개발 환경 샌드박스를 만듭니다.

샌드박스는 프로덕션 환경과 리소스 및 데이터를 혼합하지 않고 기능을 사용해 볼 수 있는 격리된 환경을 제공합니다. 자세한 내용은 [샌드박스 설명서](https://experienceleague.adobe.com/docs/experience-platform/sandbox/home.html?lang=ko-KR)를 참조하세요.

**데이터 설계자** 및 **데이터 엔지니어**&#x200B;는 이 자습서 외부에서 샌드박스를 만들어야 합니다.

연습을 시작하기 전에 이 짧은 비디오를 통해 샌드박스에 대해 자세히 알아보십시오.
>[!VIDEO](https://video.tv.adobe.com/v/29838/?learn=on)

## 권한 필요

[권한 구성](configure-permissions.md) 단원에서 이 단원을 완료하는 데 필요한 모든 액세스 제어를 설정합니다.

<!--
* Permission items **[!UICONTROL Sandbox Administration]** > **[!UICONTROL View Sandboxes]** and **[!UICONTROL Manage Sandboxes]**
* Permission item **[!UICONTROL Sandboxes]** > **[!UICONTROL Prod]**
* User-role access to the `Luma Tutorial Platform` product profile
* Admin-level access to the `Luma Tutorial Platform` product profile
-->

## 샌드박스 만들기

샌드박스를 만들어 보겠습니다.

1. [Adobe Experience Platform](https://experience.adobe.com/platform) 인터페이스에 로그인
1. 왼쪽 탐색 영역에서 **[!UICONTROL 샌드박스]**(으)로 이동
1. 오른쪽 상단에서 **[!UICONTROL 샌드박스 만들기]** 선택
   ![샌드박스 만들기 선택](assets/sandbox-createSandbox.png)

1. **[!UICONTROL Type]**(으)로 **[!UICONTROL Development]** 선택
1. 샌드박스 이름을 `luma-tutorial`로 지정합니다. (이름을 끝에 추가하는 것이 좋습니다.)
1. 튜토리얼 제목을 `Luma Tutorial`로 지정합니다(끝에 이름을 추가해 보십시오.).
1. **[!UICONTROL 만들기]** 단추 선택
   ![샌드박스 만들기](assets/sandbox-nameSandbox.png)
   >[!NOTE]
   >
   >샌드박스 이름 및 제목에 임의의 값을 사용할 수 있지만 튜토리얼 전체에서 이러한 레이블을 참조할 때 제안된 값을 유지하는 것이 좋습니다. 조직에 이 자습서를 완료하는 여러 사람이 있는 경우 샌드박스 제목과 이름 끝에 이름을 추가해 보십시오(예: luma-tutorial-ignatiusjreilly).

샌드박스를 만드는 데 약 30초 정도 걸리며 이 시간 동안 &quot;[!UICONTROL 만들기]&quot; 상태가 표시됩니다. 샌드박스가 완전히 만들어지면 &quot;[!UICONTROL 활성]&quot;으로 표시됩니다.
![활성 상태](assets/sandbox-active.png)

다음 연습을 계속하기 전에 샌드박스가 &quot;[!UICONTROL 활성]&quot;일 때까지 기다리십시오.

## 역할에 새 샌드박스 추가

샌드박스가 활성화되면 이를 사용하려면 해당 샌드박스를 역할에 포함해야 합니다. 역할에 추가하려면(시스템 관리자 또는 제품 관리자 권한 필요):

1. [!UICONTROL 권한] 화면으로 이동
1. `Luma Tutorial Platform` 역할 열기
1. 역할에서 `Prod` 샌드박스를 선택적으로 _제거_&#x200B;합니다.
1. `Luma Tutorial` 샌드박스 추가
1. **[!UICONTROL 저장]** 선택
1. [!UICONTROL 샌드박스] 행에서 **[!UICONTROL 편집]**&#x200B;을 선택합니다.

   ![Luma 자습서 추가](assets/sandbox-addLumaTutorial.png)

1. 페이지를 다시 로드하거나 Shift 키를 누른 상태로 다시 로드하면 이제 `Luma Tutorial` 샌드박스에 있거나 샌드박스 드롭다운에 표시됩니다
1. 아직 없는 경우 `Luma Tutorial` 샌드박스로 전환합니다.

   ![샌드박스 확인](assets/sandbox-confirmDropdown.png)

좋습니다. 샌드박스를 만들고 [Developer Console 및 Postman을 설정](set-up-developer-console-and-postman.md)할 준비가 되었습니다.
