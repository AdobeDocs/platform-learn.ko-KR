---
title: Content Production Agent
description: Content Production Agent
kt: 5342
doc-type: tutorial
exl-id: cb1bf6f0-f329-4e38-ba64-36ffdc3b8bd4
source-git-commit: 7ea3bdc9557ea9e88ddd9693f9ffbfbc634857f8
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 1%

---

# 1.6.1 AEM 에이전트 시작하기

>[!IMPORTANT]
>
>이 연습을 완료하려면 EDS 환경이 있는 작업 중인 AEM Sites 및 Assets CS에 액세스할 수 있어야 하며 사용 중인 IMS Org에 대해 다양한 AEM 에이전트를 활성화해야 합니다.
>
>아직 이러한 환경이 없다면 연습 [Adobe Experience Manager Cloud Service 및 Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}로 이동하십시오. 거기에 있는 지침을 따르십시오, 그러면 당신은 이러한 환경에 액세스 할 수 있습니다.

>[!IMPORTANT]
>
>이전에 AEM Sites 및 Assets CS 환경에서 AEM CS 프로그램을 구성한 경우 AEM CS 샌드박스가 최대 절전 모드일 수 있습니다. 이러한 샌드박스의 최대 절전 모드 해제 시간이 10~15분 정도 걸리는 점을 감안할 때, 나중에 최대 절전 모드 해제 프로세스를 기다릴 필요가 없도록 지금 시작하는 것이 좋습니다.

## 1.6.1.1 검색 에이전트

Adobe Experience Manager(AEM) Discovery Agent는 사용자가 자연어 프롬프트를 사용하여 Assets, 콘텐츠 조각, 적응형 Forms 등 콘텐츠를 찾고, 검색하고, 활용할 수 있도록 해주는 AEM as a Cloud Service 내의 AI 기반 도구입니다. 저장소에서 의도를 이해하고 검색하여 수동, 클릭 수가 많거나 복잡한 필터링이 필요하지 않습니다.

**검색 에이전트**&#x200B;을(를) 사용하려면 먼저 Adobe Experience Manager에서 일부 태그를 만든 다음 해당 태그를 사용하여 일부 자산에 태그를 지정합니다. 이를 통해 AI Assistant를 사용하여 에셋을 쉽고 비즈니스 친화적으로 검색할 수 있습니다.

[https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}(으)로 이동합니다. 선택해야 하는 조직은 `--aepImsOrgName--`입니다.

### Assets에서 태그 만들기 및 사용

Cloud Manager 프로그램(`--aepUserLdap-- - CitiSignal AEM+ACCS`)을 열려면 클릭하세요.

![AEM 에이전트](./images/aemagents1.png)

환경의 URL을 클릭하여 엽니다.

![AEM 에이전트](./images/aemagents2.png)

**hammer** 아이콘을 클릭합니다.

![AEM 에이전트](./images/aemagents3.png)

**일반**&#x200B;에서 **태그 지정**&#x200B;을 클릭합니다.

![AEM 에이전트](./images/aemagents4.png)

그럼 이걸 보셔야죠 **만들기**&#x200B;를 클릭한 다음 **네임스페이스 만들기**&#x200B;를 선택합니다.

![AEM 에이전트](./images/aemagents5.png)

**제목** 필드에 `CitiSignal`을(를) 입력합니다. **만들기**&#x200B;를 클릭합니다.

![AEM 에이전트](./images/aemagents6.png)

**CitiSignal** 네임스페이스를 클릭하여 드릴다운합니다. **만들기**&#x200B;를 클릭한 다음 **태그 만들기**&#x200B;를 선택합니다.

![AEM 에이전트](./images/aemagents7.png)

**제목** 필드에 `Campaign`을(를) 입력합니다. **제출을 클릭합니다**.

![AEM 에이전트](./images/aemagents8.png)

**Campaign** 태그를 클릭하여 선택합니다. **만들기**&#x200B;를 클릭한 다음 **태그 만들기**&#x200B;를 선택합니다.

![AEM 에이전트](./images/aemagents9.png)

**제목** 필드에 `Winter 2026`을(를) 입력합니다. **제출을 클릭합니다**.

![AEM 에이전트](./images/aemagents10.png)

**Campaign** 태그를 클릭하여 선택합니다. **만들기**&#x200B;를 클릭한 다음 **태그 만들기**&#x200B;를 선택합니다.

![AEM 에이전트](./images/aemagents11.png)

**제목** 필드에 `Spring 2026`을(를) 입력합니다. **제출을 클릭합니다**.

![AEM 에이전트](./images/aemagents12.png)

이제 이 항목을 사용할 수 있습니다.

![AEM 에이전트](./images/aemagents13.png)

**Adobe Experience Manager**&#x200B;을 클릭한 다음 **Assets**&#x200B;을 클릭합니다.

![AEM 에이전트](./images/aemagents14.png)

**파일**&#x200B;을 클릭합니다.

![AEM 에이전트](./images/aemagents15.png)

**CitiSignal** 폴더를 두 번 클릭하여 엽니다.

![AEM 에이전트](./images/aemagents16.png)

**만들기**&#x200B;를 클릭한 다음 **파일**&#x200B;을 선택합니다.

![AEM 에이전트](./images/aemagents17.png)

[citisignal-images-campaign.zip](./assets/citisignal-images-campaign.zip) 파일을 다운로드하여 바탕 화면에 압축 해제합니다.

![AEM 에이전트](./images/aemagents17a.png)

을(를) 선택합니다. 방금 다운로드한 3개의 파일을 **열기**&#x200B;를 클릭합니다.

![AEM 에이전트](./images/aemagents18.png)

**업로드**&#x200B;를 클릭합니다.

![AEM 에이전트](./images/aemagents19.png)

그럼 이걸 보셔야죠

![AEM 에이전트](./images/aemagents20.png)

첫 번째 이미지를 선택한 다음 **속성**&#x200B;을 클릭합니다.

![AEM 에이전트](./images/aemagents21.png)

태그 아래의 **폴더** 아이콘을 클릭합니다.

![AEM 에이전트](./images/aemagents22.png)

**2026년 봄** 태그를 선택하고 **선택**&#x200B;을 클릭합니다. 다음 이미지에 대해 이 프로세스를 반복합니다.

- citissignal_lion.png
- citissignal_leopard.png
- citissignal_gorilla.png
- citisignal_rabbit.png

![AEM 에이전트](./images/aemagents23.png)

모든 이미지에 대해 해당 태그를 선택하면 **Experience Manager Assets**(으)로 이동합니다.

![AEM 에이전트](./images/aemagents24.png)

사용 중인 저장소를 선택합니다.

![AEM 에이전트](./images/aemagents25.png)

**Assets**(으)로 이동하여 **CitiSignal** 폴더를 엽니다.

![AEM 에이전트](./images/aemagents26.png)

첫 번째 이미지를 엽니다.

![AEM 에이전트](./images/aemagents27.png)

**승인됨**&#x200B;을 선택한 다음 **저장**&#x200B;을 클릭합니다.

![AEM 에이전트](./images/aemagents28.png)

**태그**&#x200B;에서 이전에 선택한 태그를 볼 수 있습니다.

![AEM 에이전트](./images/aemagents29.png)

4개의 이미지가 모두 승인되도록 이 프로세스를 반복합니다.

![AEM 에이전트](./images/aemagents30.png)

그런 다음 **내 작업 영역**(으)로 이동하여 **AI Assistant**&#x200B;를 엽니다.

![AEM 에이전트](./images/aemagents31.png)

다음 메시지를 입력하고 **보내기**&#x200B;를 클릭합니다.

```javascript
find all assets tagged with 'Spring 2026'
```

![AEM 에이전트](./images/aemagents32.png)

여러 AEM Assets CS 환경에 액세스할 수 있는 경우 다음과 같은 메시지가 표시됩니다. 사용할 환경에 대해 제안된 답변을 클릭한 다음 **보내기**&#x200B;를 클릭합니다.

![AEM 에이전트](./images/aemagents34.png)

그러면 비슷한 대답을 볼 수 있습니다. 아이콘을 클릭하여 AI Assistant를 전체 화면으로 확장합니다.

![AEM 에이전트](./images/aemagents35.png)

답변을 검토하십시오.

![AEM 에이전트](./images/aemagents36.png)

AI Assistant 창에서 을 클릭하여 이러한 에셋을 볼 수 있습니다.

![AEM 에이전트](./images/aemagents37.png)

그런 다음 AEM Assets CS에서 해당 특정 이미지로 바로 이동합니다.

![AEM 에이전트](./images/aemagents38.png)

그런 다음 사용 가능한 다른 메타데이터를 검토할 수도 있습니다.

![AEM 에이전트](./images/aemagents39.png)

## 1.6.1.2 Experience 프로덕션 에이전트

### 콘텐츠 업데이트

콘텐츠 업데이트 스킬은 콘텐츠 조각, 페이지, 양식 및 에셋을 포함한 기존 콘텐츠를 쉽게 업데이트합니다. 에이전트는 경험을 정확하고 최신 상태로 유지하기 위해 콘텐츠 요소를 업데이트, 제거, 대체 또는 추가하는 등의 작업을 수행할 수 있습니다. 입력은 자연어 설명이 될 수 있으며, Jira PDF 및 스크린샷과 함께 사용할 경우 입력도 제공할 수 있습니다.

AI Assistant 화면으로 돌아갑니다.

![AEM 에이전트](./images/aemagents40.png)

다음 메시지를 입력하고 **보내기**&#x200B;를 클릭합니다.

`Generate multiple social media formats (Instagram 1080x1920, Facebook 1200x630, Twitter 1200x675) for the third image`

![AEM 에이전트](./images/aemagents40a.png)

몇 분 후에 유사한 응답이 표시됩니다.

![AEM 에이전트](./images/aemagents41.png)

생성된 이미지를 검토합니다.

![AEM 에이전트](./images/aemagents42.png)

### 양식 만들기

양식 작성 기술을 사용하면 개발이나 IT 팀에 의존하지 않고 자연어 프롬프트를 통해 적응형 양식을 작성할 수 있습니다. 이 기능은 브랜드 일관성을 유지하면서 양식 개발을 가속화하고 비즈니스 사용자가 깊이 있는 기술 제품 지식 없이도 양식을 만들 수 있도록 합니다.


## 다음 단계

[AEM 및 에이전트](./aemagents.md){target="_blank"}(으)로 돌아가기

[모든 모듈로 돌아가기](./../../../overview.md){target="_blank"}
