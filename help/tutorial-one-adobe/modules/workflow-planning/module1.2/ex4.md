---
title: Workfront 시작하기
description: Workfront 시작하기
kt: 5342
doc-type: tutorial
source-git-commit: 34f37a33e874f55eea37290b5626ab613f575764
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 1%

---

# 1.2.4 Workfront + AEM Sites

[https://experienceplatform.my.workfront.com/](https://experienceplatform.my.workfront.com/){target="_blank"}(으)로 이동하여 Adobe Workfront에 로그인합니다.

그럼 이걸 보게나

![WF](./images/wfb1.png)

## 1.2.4.1 AEM Sites 통합 구성

>[!NOTE]
>
>이 플러그인은 현재 **조기 액세스** 모드이며 아직 일반적으로 사용할 수 없습니다.
>
>이 플러그인은 사용 중인 Workfront 인스턴스에 이미 설치되어 있을 수 있습니다. 이미 설치되어 있는 경우 아래 지침을 검토할 수 있지만 구성에서 변경할 필요가 없습니다.

[https://experience.adobe.com/#/@experienceplatform/aem/extension-manager/universal-editor](https://experience.adobe.com/#/@experienceplatform/aem/extension-manager/universal-editor){target="_blank"}(으)로 이동합니다.

이 플러그인의 **toggle**&#x200B;이(가) **활성화됨**(으)로 설정되어 있는지 확인하십시오. 그런 다음 **톱니바퀴** 아이콘을 클릭합니다.

![WF](./images/wfb8.png)

**확장 구성** 팝업이 표시됩니다. 이 플러그인을 사용하도록 다음 필드를 구성합니다.

| 키 | 값 |
| --------------- | ------------------------------ | 
| **`IMS_ENV`** | **PROD** |
| **`WORKFRONT_INSTANCE_URL`** | **https://experienceplatform.my.workfront.com** |
| **`SHOW_CUSTOM_FORMS`** | **&#39;{&quot;previewUrl&quot;: true, &quot;publishUrl&quot;: true}&#39;** |

**저장**&#x200B;을 클릭합니다.

![WF](./images/wfb8.png)

Workfront UI로 돌아가서 9개 점 **햄버거** 아이콘을 클릭합니다. **설치**&#x200B;를 선택하십시오.

![WF](./images/wfb9.png)

왼쪽 메뉴에서 **사용자 지정 Forms**(으)로 이동하여 **양식**&#x200B;을(를) 선택합니다. **+ 새 사용자 정의 양식**&#x200B;을 클릭합니다.

![WF](./images/wfb10.png)

**작업**&#x200B;을 선택하고 **계속**&#x200B;을 클릭합니다.

![WF](./images/wfb11.png)

그러면 빈 사용자 정의 양식이 표시됩니다. 양식 이름 `Content Fragment & Integration ID`을(를) 입력하십시오.

![WF](./images/wfb12.png)

새 **한 줄 텍스트** 필드를 캔버스로 끌어서 놓습니다.

![WF](./images/wfb13.png)

다음과 같이 새 필드를 구성합니다.

- **레이블**: **콘텐츠 조각**
- **이름**: **`aem_workfront_integration_content_fragment`**

![WF](./images/wfb14.png)

새 **한 줄 텍스트** 필드를 캔버스에 추가하고 다음과 같이 새 필드를 구성합니다.

- **레이블**: **통합 ID**
- **이름**: **`aem_workfront_integration_id`**

**적용**&#x200B;을 클릭합니다.

![WF](./images/wfb15.png)

이제 두 번째 사용자 정의 양식을 구성해야 합니다. **+ 새 사용자 정의 양식**&#x200B;을 클릭합니다.

![WF](./images/wfb10.png)

**작업**&#x200B;을 선택하고 **계속**&#x200B;을 클릭합니다.

![WF](./images/wfb11.png)

그러면 빈 사용자 정의 양식이 표시됩니다. 양식 이름 `Preview & Publish URL`을(를) 입력하십시오.

![WF](./images/wfb16.png)

새 **한 줄 텍스트** 필드를 캔버스로 끌어서 놓습니다.

![WF](./images/wfb17.png)

다음과 같이 새 필드를 구성합니다.

- **레이블**: **미리 보기 URL**
- **이름**: **`aem_workfront_integration_preview_url`**

![WF](./images/wfb18.png)

새 **한 줄 텍스트** 필드를 캔버스에 추가하고 다음과 같이 새 필드를 구성합니다.

- **레이블**: **게시 URL**
- **이름**: **`aem_workfront_integration_publish_url`**

**적용**&#x200B;을 클릭합니다.

![WF](./images/wfb19.png)

그러면 2개의 사용자 정의 양식을 사용할 수 있습니다.

![WF](./images/wfb20.png)

다음 단계: [1.2.2 Workfront 증명](./ex2.md){target="_blank"}

[Adobe Workfront을 사용한 워크플로우 관리로 돌아가기](./workfront.md){target="_blank"}

[모든 모듈로 돌아가기](./../../../overview.md){target="_blank"}
