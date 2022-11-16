---
title: 권한 구성
seo-title: Configure permissions | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 권한 구성
description: 이 단원에서는 Adobe의 Admin Console을 사용하여 Adobe Experience Platform 사용자 권한을 구성합니다.
role: Data Architect, Data Engineer
feature: Access Control
kt: 4348
thumbnail: 4348-configure-permissions.jpg
exl-id: ca01f99e-f10c-4bf0-bef2-b011ac29a565
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 2%

---

# 권한 구성

<!--30min-->

이 단원에서는 [!DNL Adobe's Admin Console].

액세스 제어는 Experience Platform의 주요 개인 정보 보호 기능이며 사람들이 자신의 작업 기능을 수행하는 데 필요한 최소한의 권한으로 권한을 제한하는 것이 좋습니다. 자세한 내용은 [액세스 제어 설명서](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=ko) 추가 정보.

데이터 설계자 및 데이터 엔지니어 는 Adobe Experience Platform의 고급 사용자이며 이 자습서를 완료하고 나중에 일상적인 작업을 수행하려면 많은 권한이 필요합니다. 데이터 설계자는 *기타 플랫폼 사용자* 마케터, 분석 및 데이터 과학자 등의 회사에서 사용할 수 있습니다. 이 단원을 완료하면 이러한 기능을 사용하여 회사의 다른 사용자를 관리하는 방법을 생각해 보십시오.

**데이터 설계자** 종종 이 자습서를 제외한 다른 사용자에 대한 권한을 구성합니다.

>[!IMPORTANT]
>
>Adobe Experience Cloud 제품의 시스템 관리자는 섹션 제목에서 나오는 이 단원의 일부 단계를 완료해야 합니다. 시스템 관리자가 아닌 경우 회사의 관리자에게 연락하여 이러한 작업을 완료하도록 요청하십시오.

## Admin Console 정보

다음 [!DNL Admin Console] 는 모든 Adobe Experience Cloud 제품에 대한 사용자 액세스를 관리하는 데 사용되는 인터페이스입니다. 자세한 내용은 [Adobe Admin Console 설명서](https://helpx.adobe.com/kr/enterprise/using/admin-console.html) 를 참조하십시오. 여기 몇 가지 키가 있습니다 [!DNL Admin Console] 개념:

* A **제품 프로필** 는 특정 Adobe 제품에 연결된 권한, 역할 및 샌드박스 환경의 조합입니다. 단일 Adobe 제품에 대해 여러 제품 프로필을 만들 수 있습니다. 예를 들어 &quot;마케터&quot; 프로필은 일반적인 마케터가 프로덕션 플랫폼 환경에서 주요 작업을 완료하는 데 필요한 권한으로 권한을 제한할 수 있고, &quot;데이터 설계자&quot; 프로필을 사용하여 여러 플랫폼 환경에서 서로 다른 권한을 부여할 수 있습니다. 이 단원에서는 Data Architect 및 데이터 엔지니어가 샌드박스 환경에서 이 자습서를 완료하는 데 필요한 모든 권한이 있는 &quot;Luma 자습서&quot; 제품 프로필을 만듭니다.
* An **통합** 는 *프로젝트* Adobe Developer 콘솔에서 게시할 수 있습니다. Adobe Developer 콘솔은 Adobe API의 인증 및 구성의 중심입니다. 개발자 콘솔에서 통합을 구성하고 [!DNL Postman] 단원.

다음은 플랫폼에 있는 역할에 대한 빠른 요약입니다.

* **사용자** 제품 프로필의 사용자 인터페이스는 제품 프로필에 할당된 권한에 따라 Platform의 사용자 인터페이스에서 작업을 완료할 수 있습니다.
* **개발자** 제품 프로필의 권한에 따라 Platform의 API를 사용하여 작업을 완료할 수 있습니다.
* **제품 프로필 관리자** 편집 가능 *특정 프로필의* 권한 및 사용자, 개발자 및 추가 프로필 관리자 추가
* **제품 관리자** 관리 가능 *모든 제품 프로필* 플랫폼 및 새 제품 프로필 추가
* **시스템 관리자** 제품 관리자를 추가하고 모든 Adobe Experience Cloud 제품에 대한 권한을 기본적으로 관리할 수 있습니다.

## Experience Platform 제품 프로필 만들기(시스템 관리자 또는 제품 관리자 필요)

이 연습에서는 사용자나 시스템 관리자가 Adobe Experience Platform용 제품 프로필을 만들고 해당 제품 프로필에 대한 관리자로 사용자를 추가합니다.

>[!NOTE]
>
>이 자습서를 수행하는 동료에게 도움을 주는 시스템 관리자라면 동료를 *제품 관리자* Adobe Experience Platform용. 제품 관리자는 이러한 단계를 직접 완료하고 나중에 다른 Experience Platform 사용자를 관리할 수 있습니다.

제품 프로필을 만들려면:

1. 에 로그인합니다. [Adobe Admin Console](https://adminconsole.adobe.com)
1. 선택 **[!UICONTROL 제품]** 위쪽 탐색에서
1. 선택 **[!UICONTROL Adobe Experience Platform]** 왼쪽 탐색 영역에서 다음을 확장해야 할 수 있습니다 **[!UICONTROL Experience Cloud]** 섹션)
1. Experience Platform 인스턴스에 이미 여러 개의 프로필이 있을 수 있습니다. 을(를) 선택합니다 **[!UICONTROL 새 프로필]** 다른 단추 추가
   ![새 프로필 추가 를 선택합니다](assets/adminconsole-newProfile.png)
1. 프로필 이름을 지정합니다 `Luma Tutorial Platform` (회사의 여러 사용자가 이 자습서를 사용하고 있는 경우 자습서 참가자 이름을 끝에 추가하고) **[!UICONTROL 다음]** 버튼
   ![프로필 이름을 Luma 자습서 Platform으로 지정합니다](assets/adminconsole-nameProfile.png)
1. 제품 라이센스의 세부 사항에 따라 이 두 번째 항목이 표시될 수도 있고 표시되지 않을 수도 있습니다 **[!UICONTROL 서비스]** 화면. 이 자습서에서는 이러한 서비스를 사용하지 않으므로 선택을 취소하십시오 **[!UICONTROL 모든 서비스 활성화]** to *제거* 모든 서비스를 선택하고 **[!UICONTROL 저장]**.
   ![서비스 사용 안 함](assets/adminconsole-createProfile-services.png)

이제 자습서 참가자를 새로 만든 제품 프로필의 관리자로 추가합니다. If *you* 자습서 참가자인 경우 다음 작업을 건너뜁니다. [Experience Platform 제품 프로필 구성](#configure-experience-platform-product-profile):

1. 을(를) 선택합니다 `Luma Tutorial Platform` 제품 프로필:

   ![프로필을 엽니다.](assets/adminconsole-newProfileInList.png)

1. 을(를) 선택합니다 **[!UICONTROL 관리자]** 탭을 선택한 다음 **[!UICONTROL 관리자 추가]** 버튼:

   ![관리자 탭으로 이동하여 관리 추가 를 선택합니다](assets/adminconsole-addAdmin.png)

1. 워크플로우를 완료하여 자습서 참가자를 관리자로 추가합니다.

이 단계를 완료하면 `Luma Tutorial Platform` 프로필이 한 명의 관리자로 설정되어 있습니다.
![플랫폼 프로필이 생성됨](assets/adminconsole-platform-profileCreated.png)

## Experience Platform 제품 프로필 구성

이제 사용자가 `Luma Tutorial Platform` 제품 프로필에서는 자습서를 완료하는 데 필요한 권한 및 역할을 구성할 수 있습니다.

### 권한 추가

이제 프로필에 개별 권한 항목을 추가합니다.

1. 를 엽니다. `Luma Tutorial Platform` 제품 프로필
1. 을(를) 선택합니다 **[!UICONTROL 권한]** 탭
1. 아래 **[!UICONTROL 샌드박스]**, 추가 **[!UICONTROL Prod]** 샌드박스를 프로필 샌드박스에 추가합니다. 에 액세스할 수 있어야 합니다 [!DNL Prod] 샌드박스를 추가로 만들려면 샌드박스 를 샌드박스로 만듭니다. 다음 단원에서 자습서 샌드박스를 추가하면 [!DNL Prod] 제품 프로필의 샌드박스 를 참조하십시오.
1. 아래 [!UICONTROL 데이터 수집], 추가 [!UICONTROL 소스 관리] 및 [!UICONTROL 소스 보기] 권한 항목.
1. 다음에 대한 모든 권한 항목을 추가합니다.
   1. [!UICONTROL 데이터 모델링]
   1. [!UICONTROL 데이터 관리]
   1. [!UICONTROL 프로필 관리]
   1. [!UICONTROL ID 관리]
   1. [!UICONTROL 샌드박스 관리]
   1. [!UICONTROL 쿼리 서비스]
   1. [!UICONTROL 데이터 수집]
   1. [!UICONTROL 데이터 거버넌스]
   1. [!UICONTROL 대시보드]
   1. [!UICONTROL 경고]

1. 모든 권한 항목을 추가한 후에는 **[!UICONTROL 저장]** 버튼

### 사용자로 자신을 추가합니다

이 시점에서 `Luma Tutorial Platform` 당신이 *전용* Experience Platform 제품 프로필에서는 여전히 Experience Platform의 사용자 인터페이스에 로그인할 수 없습니다. 이를 위해서는 *사용자* 를 입력합니다. 다행히, 네가 *관리* 제품 프로필에서 자신을 *사용자*!

1. 로 이동합니다. **[!UICONTROL 사용자]** 탭
1. 을(를) 선택합니다 **[!UICONTROL 사용자 추가]** 버튼
   ![사용자 추가 선택](assets/adminconsole-addUser.png)
1. 워크플로우를 완료하여 제품 프로필에 사용자로 자신을 추가합니다

### 개발자로서 자신을 추가하십시오

플랫폼 API를 사용하려면 자신을 개발자로 추가하십시오.

1. 로 이동합니다. **[!UICONTROL 개발자]** 탭
1. 을(를) 선택합니다 **[!UICONTROL 개발자 추가]** 버튼
   ![사용자 추가 선택](assets/adminconsole-addDeveloper.png)
1. 워크플로우를 완료하여 제품 프로필에 개발자로 자신을 추가합니다

## 데이터 수집 제품 프로필 만들기(시스템 관리자 또는 제품 관리자 필요)

이 연습에서는 사용자나 회사의 시스템 관리자가 데이터 수집(이전의 Adobe Experience Platform Launch)에 대한 제품 프로필을 만들고 사용자를 제품 프로필 관리자로 추가합니다.

>[!NOTE]
>
>이 자습서를 동료에게 지원하는 시스템 관리자라면 이러한 사용자를 *제품 관리자* 데이터 수집. 제품 관리자는 스스로 이러한 단계를 완료하고 나중에 데이터 수집을 다른 사용자가 관리할 수 있습니다.

제품 프로필을 만들려면:

1. 에서 [!DNL Adobe Admin Console] Adobe Experience Platform 데이터 수집 제품으로 이동합니다
1. 이름이 인 새 프로필 추가 `Luma Tutorial Data Collection` (회사의 여러 사용자가 이 자습서를 사용하고 있는 경우 자습서 참가자 이름을 끝에 추가합니다.)
1. 설정 해제 **[!UICONTROL 속성]** > **[!UICONTROL 자동 포함]** 설정
1. 이 시점에서는 속성 또는 권한을 할당하지 않습니다
1. 이 프로필의 관리자로 자습서 참가자 추가

이 단계를 완료하면 `Luma Tutorial Data Collection` 프로필이 한 명의 관리자로 설정되어 있습니다.
![데이터 수집 프로필이 생성됨](assets/adminconsole-dc-profileCreated.png)

## 데이터 수집 제품 프로필 구성

이제 사용자가 `Luma Tutorial Data Collection` 제품 프로필에서는 자습서를 완료하는 데 필요한 권한 및 역할을 구성할 수 있습니다.

### 권한 추가

이제 프로필에 개별 권한 항목을 추가합니다.

1. 에서 [Adobe Admin Console](https://adminconsole.adobe.com), 이동 **[!UICONTROL 제품]** > **[!UICONTROL 데이터 수집]**
1. 를 엽니다. `Luma Tutorial Data Collection` 프로필
1. 로 이동합니다. **[!UICONTROL 권한]** 탭
1. 열기 **[!UICONTROL 플랫폼]**
1. 사용 가능한 모든 플랫폼을 선택했는지 확인합니다(라이센스를 기반으로 다른 옵션이 표시될 수 있음).
1. 모든 변경 내용을 **[!UICONTROL 저장]**합니다
   ![플랫폼 추가](assets/adminconsole-launch-addPlatforms.png)
1. 열기 **[!UICONTROL 속성]**
1. 다음을 확인합니다. **[!UICONTROL 자동 포함]** 속성을 액세스할 수 없도록 설정/해제(나중에 추가)
1. 모든 변경 내용을 **[!UICONTROL 저장]**합니다
   ![속성 제거](assets/adminconsole-launch-removeProperties.png)
1. 열기 **[!UICONTROL 속성 권한]**
1. 선택 **[!UICONTROL 모두 추가]** 모든 속성 권한을 추가하려면
1. **[!UICONTROL 저장]**
   ![속성 제거](assets/adminconsole-launch-addPropertyRights.png)
1. 열기 **[!UICONTROL 회사 권한]**
1. 추가 **[!UICONTROL 속성 관리]**
1. **[!UICONTROL 저장]**을 선택합니다

   ![속성 제거](assets/adminconsole-launch-companyRights.png)


### 사용자로 자신을 추가합니다

이제 자신을 데이터 수집 프로필에 사용자로 추가합니다.

1. 로 이동합니다. **[!UICONTROL 사용자]** 탭
1. 을(를) 선택합니다 **[!UICONTROL 사용자 추가]** 버튼
   ![사용자 추가 선택](assets/adminconsole-launch-addUser.png)
1. 워크플로우를 완료하여 제품 프로필에 사용자로 자신을 추가합니다

데이터 수집을 위한 개발자로 자신을 추가할 필요는 없습니다.

이제 자습서를 완료하는 데 필요한 거의 모든 권한이 있습니다. 당신이 안에서 만들 수 있는 두 가지 더 많은 변형이 있을 것입니다 [!DNL Adobe Admin Console], 뒤에 하나 포함 [샌드박스 만들기](create-a-sandbox.md)!
