---
title: Workfront 증명
description: Workfront 증명
kt: 5342
doc-type: tutorial
exl-id: 5feb9486-bdb4-4d59-941c-09fc2e38163b
source-git-commit: 42f6d8a07baa03a9ab31cff0ef518ae2c5ad930e
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---

# 1.2.2 Workfront을 사용한 증명

>[!IMPORTANT]
>
>이전에 AEM Assets CS 환경에서 AEM CS 프로그램을 구성한 경우 AEM CS 샌드박스가 최대 절전 모드일 수 있습니다. 이러한 샌드박스의 최대 절전 모드 해제 시간이 10~15분 정도 걸리는 점을 감안할 때, 나중에 최대 절전 모드 해제 프로세스를 기다릴 필요가 없도록 지금 시작하는 것이 좋습니다.

## 1.2.2.1 새 승인 흐름 만들기

**Adobe Workfront**(으)로 돌아갑니다. **메뉴** 아이콘을 클릭하고 **증명**&#x200B;을 선택합니다.

![WF](./images/wfp1.png)

**워크플로**(으)로 이동하여 **+ 신규**&#x200B;를 클릭한 다음 **새 템플릿**&#x200B;을(를) 선택하십시오.

![WF](./images/wfp2.png)

**템플릿 이름**&#x200B;을(를) `--aepUserLdap-- - Approval Workflow`(으)로 설정하고 **템플릿 소유자**&#x200B;를 직접 설정합니다.

![WF](./images/wfp3.png)

아래로 스크롤하여 **단계** > **단계 1**&#x200B;에서 **검토자 및 승인자**&#x200B;의 **역할**&#x200B;을(를) 추가하세요.

**만들기**&#x200B;를 클릭합니다.

![WF](./images/wfp4.png)

이제 기본 승인 워크플로를 사용할 준비가 되었습니다.

![WF](./images/wfp5.png)

## 1.2.2.2 새 프로젝트 만들기

**메뉴**&#x200B;를 열고 **프로그램**(으)로 이동합니다.

![WF](./images/wfp6a.png)

이전에 만든 `--aepUserLdap-- CitiSignal Fiber Launch` 프로그램을 클릭합니다.

>[!NOTE]
>
>만들고 실행한 자동화를 사용하여 [Workfront 계획](./../module1.1/ex1.md)에서 연습의 일부로 프로그램을 만들었습니다. 아직 안하셨으면 거기서 안내를 찾으실 수 있습니다

![WF](./images/wfp6b.png)

프로그램에서 **프로젝트**(으)로 이동합니다. **+ 새 프로젝트**&#x200B;를 클릭한 다음 **새 프로젝트**&#x200B;을 선택합니다.

![WF](./images/wfp6.png)

그럼 이걸 보셔야죠 이름을 `--aepUserLdap-- - CitiSignal Fiber Launch`(으)로 변경합니다.

![WF](./images/wfp6c.png)

**프로젝트 세부 정보**(으)로 이동합니다. **설명**&#x200B;에서 **+추가**&#x200B;를 클릭합니다.

![WF](./images/wfp6d.png)

설명을 `The CitiSignal Fiber Launch project is used to plan the upcoming launch of CitiSignal Fiber.`(으)로 설정

**변경 내용 저장**&#x200B;을 클릭합니다.

![WF](./images/wfp6e.png)

이제 프로젝트가 생성되었습니다.

![WF](./images/wfp7.png)

## 1.2.2.3 새 작업 만들기

**작업**(으)로 이동하여 **+ 새 작업**&#x200B;을(를) 클릭합니다.

![WF](./images/wfp7a.png)

작업 이름 `Create assets for Fiber campaign`을(를) 입력하십시오.

**설명** 필드를 `This task is used to track the progress of the creation of the assets for the CitiSignal Fiber Launch Campaign.`(으)로 설정합니다.

**작업 만들기**&#x200B;를 클릭합니다.

![WF](./images/wfp8.png)

그럼 이걸 보셔야죠

![WF](./images/wfp9.png)

**할당** 열에서 고유한 이름을 추가합니다.

![WF](./images/wfp9a.png)

그러면 작업이 사용자에게 할당됩니다.

![WF](./images/wfp9b.png)

## 1.2.2.4 작업에 새 문서를 추가하고 승인 흐름을 거칩니다.

개요 페이지로 돌아가려면 **Workfront** 로고를 클릭하십시오. 그러면 방금 만든 프로젝트가 개요에 표시됩니다. 프로젝트를 클릭하여 엽니다.

![WF](./images/wfp9c.png)

**작업**&#x200B;에서 을(를) 클릭하여 작업을 엽니다.

![WF](./images/wfp9d.png)

**문서**(으)로 이동합니다. **+ 새로 추가**&#x200B;를 클릭한 다음 **문서**&#x200B;을(를) 선택합니다.

![WF](./images/wfp10.png)

데스크톱에 [이 파일](./images/2048x2048.png)을 다운로드하세요.

![WF](./images/2048x2048.png){width="50px" align="left"}

**2048x2048.png** 파일을 선택하고 **열기**&#x200B;를 클릭합니다.

![WF](./images/wfp12.png)

그럼 이걸 드셔보세요 업로드된 문서 위로 마우스를 가져갑니다. **증명 만들기**&#x200B;를 클릭한 다음 **고급 증명**&#x200B;을 선택합니다.

![WF](./images/wfp13.png)

**새 증명** 창에서 **자동화**&#x200B;를 선택한 다음 이전에 만든 워크플로 템플릿을 선택합니다. 워크플로 템플릿의 이름은 `--aepUserLdap-- - Approval Workflow`이어야 합니다. **증명 만들기**&#x200B;를 클릭합니다.

![WF](./images/wfp14.png)

**작업**&#x200B;을 클릭하세요.

![WF](./images/wfp17.png)

**증명 열기** 클릭

![WF](./images/wfp18.png)

이제 증명을 검토할 수 있습니다. 문서를 변경해야 하는 설명을 추가하려면 **설명 추가**&#x200B;를 선택하십시오.

![WF](./images/wfp19.png)

댓글을 입력하고 **게시물**&#x200B;을 클릭하세요. Click **Close**.

![WF](./images/wfp20.png)

이제 역할을 **검토자**&#x200B;에서 **검토자 및 승인자**(으)로 변경해야 합니다. 이렇게 하려면 작업으로 돌아가서 **증명 워크플로**&#x200B;를 클릭합니다.

![WF](./images/wfp21.png)

역할을 **검토자**&#x200B;에서 **검토자 및 승인자**(으)로 변경하십시오.

![WF](./images/wfp22.png)

작업으로 돌아가 증명을 다시 엽니다. 이제 새 버튼 **결정**&#x200B;이 표시됩니다. 클릭합니다.

![WF](./images/wfp23.png)

**변경 필요**&#x200B;를 선택하고 **결정**&#x200B;을 클릭합니다.

![WF](./images/wfp24.png)

**작업** 및 **문서**(으)로 돌아갑니다. 이제 제공된 설명을 고려한 두 번째 이미지를 업로드해야 합니다.

![WF](./images/wfp25.png)

데스크톱에 [이 파일](./images/2048x2048_buynow.png)을 다운로드하세요.

![이 파일](./images/2048x2048_buynow.png){width="50px" align="left"}

작업 보기에서 승인되지 않은 이전 이미지 파일을 선택합니다. **+ 새로 추가**&#x200B;를 클릭하고 **버전**&#x200B;을 선택한 다음 **문서**&#x200B;를 선택합니다.

![WF](./images/wfp26.png)

**2048x2048_buynow.png** 파일을 선택하고 **열기**&#x200B;를 클릭합니다.

![WF](./images/wfp27.png)

그럼 이걸 드셔보세요 **증명 만들기**&#x200B;를 클릭한 다음 **고급 증명**&#x200B;을 다시 선택하십시오.

![WF](./images/wfp28.png)

그러면 이걸 보게 될 거야. Workfront에서 이전 승인 워크플로가 여전히 유효하다고 가정함에 따라 **워크플로 템플릿**&#x200B;이(가) 미리 선택됩니다. **증명 만들기**&#x200B;를 클릭합니다.

![WF](./images/wfp29.png)

**증명 열기**&#x200B;를 선택합니다.

![WF](./images/wfp30.png)

이제 두 버전의 파일이 나란히 표시됩니다.

![WF](./images/wfp31.png)

**결정**&#x200B;을 클릭하고 **승인됨**&#x200B;을 선택한 다음 **결정**&#x200B;을 다시 클릭합니다.

![WF](./images/wfp32.png)

작업 개요로 돌아가려면 **작업 이름**&#x200B;을 클릭하세요.

![WF](./images/wfp33.png)

그런 다음 승인된 자산을 사용하여 작업 보기로 돌아갑니다. 이제 이 자산을 AEM Assets에 공유해야 합니다.

![WF](./images/wfp34.png)

승인된 문서를 선택합니다. **공유 화살표** 아이콘을 클릭하고 `--aepUserLdap-- - CitiSignal AEM`(이)라는 AEM Assets 통합을 선택합니다.

![WF](./images/wfp35.png)

이전에 만든 폴더(`--aepUserLdap-- - CitiSignal Fiber Launch Assets`)를 두 번 클릭합니다.

![WF](./images/wfp36.png)

**폴더 선택**&#x200B;을 클릭합니다.

![WF](./images/wfp37.png)

1~2분 후 문서가 이제 AEM Assets에 게시됩니다. 문서 이름 옆에 AEM 아이콘이 표시됩니다.

![WF](./images/wfp37a.png)

이 작업을 완료하려면 **완료로 표시**&#x200B;를 클릭하십시오.

![WF](./images/wfp37b.png)

그럼 이걸 보셔야죠

![WF](./images/wfp37c.png)

## 1.2.2.5 AEM Assets에서 내 파일 보기

이름이 `--aepUserLdap-- - CitiSignal Fiber Launch Assets`인 AEM Assets CS의 폴더로 이동합니다.

![WF](./images/wfppaem1.png)

이미지를 선택한 다음 **세부 정보**&#x200B;를 선택합니다.

![WF](./images/wfppaem2.png)

그러면 이전에 만든 Workfront과 AEM Assets 간의 통합에 의해 자동으로 채워진 값과 함께 메타데이터 양식이 표시됩니다.

![WF](./images/wfppaem3.png)

[Adobe Workfront을 사용한 워크플로우 관리로 돌아가기](./workfront.md){target="_blank"}

[모든 모듈로 돌아가기](./../../../overview.md){target="_blank"}
