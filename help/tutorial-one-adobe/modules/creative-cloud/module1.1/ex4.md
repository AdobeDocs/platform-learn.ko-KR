---
title: Firefly 맞춤형 모델 API
description: Firefly 맞춤형 모델 API 작업
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 330f4492-d0df-4298-9edc-4174b0065c9a
source-git-commit: 219945c74c620b9a4b93cb2b7462137118d42d33
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---

# 1.1.4 Firefly 사용자 지정 모델 API

## 1.1.4.1 사용자 지정 모델 구성

[https://firefly.adobe.com/](https://firefly.adobe.com/)(으)로 이동합니다. **사용자 지정 모델**&#x200B;을 클릭합니다.

![Firefly 사용자 지정 모델](./images/ffcm1.png){zoomable="yes"}

이 메시지가 표시됩니다. 계속하려면 **동의**&#x200B;를 클릭하세요.

![Firefly 사용자 지정 모델](./images/ffcm2.png){zoomable="yes"}

그럼 이걸 보셔야죠 **모델 교육**&#x200B;을 클릭합니다.

![Firefly 사용자 지정 모델](./images/ffcm3.png){zoomable="yes"}

다음 필드를 구성합니다.

- **이름**: `--aepUserLdap-- - Citi Signal Router Model` 사용
- **교육 모드**: **제목(기술 미리 보기) 선택**
- **개념**: `router` 입력
- **저장 위치**: 드롭다운 목록을 열고 **+ 새 프로젝트 만들기** 클릭

![Firefly 사용자 지정 모델](./images/ffcm4.png){zoomable="yes"}

새 프로젝트에 이름을 지정하십시오. `--aepUserLdap-- - Custom Models`. **만들기**&#x200B;를 클릭합니다.

![Firefly 사용자 지정 모델](./images/ffcm5.png){zoomable="yes"}

그럼 이걸 보셔야죠 **만들기**&#x200B;를 클릭합니다.

![Firefly 사용자 지정 모델](./images/ffcm6.png){zoomable="yes"}

이제 교육할 사용자 정의 모델에 대한 참조 이미지를 제공해야 합니다. **컴퓨터에서 이미지 선택**&#x200B;을 클릭합니다.

![Firefly 사용자 지정 모델](./images/ffcm7.png){zoomable="yes"}

참조 이미지 [여기](https://tech-insiders.s3.us-west-2.amazonaws.com/CitiSignal_router.zip)를 다운로드하십시오. 다운로드 파일의 압축을 풀고 해당 파일을 제공합니다.

![Firefly 사용자 지정 모델](./images/ffcm8.png){zoomable="yes"}

다운로드 이미지 파일이 포함된 폴더로 이동합니다. 모두 선택하고 **열기**&#x200B;를 클릭합니다.

![Firefly 사용자 지정 모델](./images/ffcm9.png){zoomable="yes"}

그러면 이미지가 로드되는 것을 볼 수 있습니다.

![Firefly 사용자 지정 모델](./images/ffcm10.png){zoomable="yes"}

몇 분 후에 이미지가 올바르게 로드됩니다. 일부 이미지에 오류가 있는 것은 이미지의 캡션이 생성되지 않았거나 너무 길지 않기 때문입니다. 오류가 있는 각 이미지를 검토하고 요구 사항을 충족하고 이미지를 설명하는 캡션을 입력합니다.

![Firefly 사용자 지정 모델](./images/ffcm11.png){zoomable="yes"}

모든 이미지에 요구 사항을 충족하는 캡션이 추가되더라도 샘플 프롬프트를 제공해야 합니다. &#39;router&#39;라는 단어를 사용하는 프롬프트를 입력하십시오. 이를 완료하면 모델 교육을 시작할 수 있습니다. **교육**&#x200B;을 클릭합니다.

![Firefly 사용자 지정 모델](./images/ffcm12.png){zoomable="yes"}

그러면 이걸 보게 될 거야. 모델을 교육하는 데 20~30분 이상 걸릴 수 있습니다.

![Firefly 사용자 지정 모델](./images/ffcm13.png){zoomable="yes"}

20~30분 후 모델이 이제 교육되어 게시될 수 있습니다. **게시**&#x200B;를 클릭합니다.

![Firefly 사용자 지정 모델](./images/ffcm14.png){zoomable="yes"}

**게시**&#x200B;를 다시 클릭합니다.

![Firefly 사용자 지정 모델](./images/ffcm15.png){zoomable="yes"}

**사용자 지정 모델 공유** 팝업을 닫습니다.

![Firefly 사용자 지정 모델](./images/ffcm16.png){zoomable="yes"}

## 1.1.4.2 UI에서 맞춤형 모델 사용

[https://firefly.adobe.com/cme/train](https://firefly.adobe.com/cme/train)(으)로 이동합니다. 사용자 정의 모델을 클릭하여 엽니다.

![Firefly 사용자 지정 모델](./images/ffcm19.png){zoomable="yes"}

**미리 보기 및 테스트**&#x200B;를 클릭합니다.

![Firefly 사용자 지정 모델](./images/ffcm17.png){zoomable="yes"}

그런 다음 실행되기 전에 입력한 샘플 프롬프트가 표시됩니다.

![Firefly 사용자 지정 모델](./images/ffcm18.png){zoomable="yes"}

## 1.1.4.3 Firefly Services 사용자 지정 모델 API에 대해 사용자 지정 모델 활성화

사용자 지정 모델이 교육되면 API를 통해서도 사용할 수 있습니다. 연습 1.1.1에서는 API를 통해 Firefly Services와 상호 작용하기 위해 Adobe I/O 프로젝트를 이미 구성했습니다.

[https://firefly.adobe.com/cme/train](https://firefly.adobe.com/cme/train)(으)로 이동합니다. 사용자 정의 모델을 클릭하여 엽니다.

![Firefly 사용자 지정 모델](./images/ffcm19.png){zoomable="yes"}

세 점 **..**&#x200B;을(를) 클릭한 다음 **공유**&#x200B;를 클릭합니다.

![Firefly 사용자 지정 모델](./images/ffcm20.png){zoomable="yes"}

Firefly 사용자 지정 모델에 액세스하려면 Adobe I/O 프로젝트의 **기술 계정 ID**&#x200B;에 사용자 지정 모델을 공유해야 합니다.

**기술 계정 ID**&#x200B;를 검색하려면 [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)(으)로 이동하십시오. 프로젝트를 열려면 클릭하세요. 프로젝트 이름은 `--aepUserLdap-- Firefly`입니다.

![Firefly 사용자 지정 모델](./images/ffcm24.png){zoomable="yes"}

**OAuth 서버 간**&#x200B;을 클릭합니다.

![Firefly 사용자 지정 모델](./images/ffcm25.png){zoomable="yes"}

**기술 계정 ID**&#x200B;를 복사하려면 클릭하세요.

![Firefly 사용자 지정 모델](./images/ffcm23.png){zoomable="yes"}

**기술 계정 ID**&#x200B;를 붙여넣고 **편집하려면 초대**&#x200B;를 클릭하세요.

![Firefly 사용자 지정 모델](./images/ffcm21.png){zoomable="yes"}

이제 **기술 계정 ID**&#x200B;에서 사용자 지정 모델에 액세스할 수 있습니다.

![Firefly 사용자 지정 모델](./images/ffcm22.png){zoomable="yes"}

## 1.1.4.4 Firefly Services 사용자 지정 모델 API와 상호 작용

연습 1.1.1 Firefly 서비스 시작에서 이 파일 [postman-ff.zip](./../../../assets/postman/postman-ff.zip)을(를) 로컬 데스크톱에 다운로드한 다음 Postman에서 해당 컬렉션을 가져왔습니다.

Postman을 열고 **FF - 사용자 지정 모델 API** 폴더로 이동합니다.

![Firefly 사용자 지정 모델](./images/ffcm30.png){zoomable="yes"}

**1 요청을 엽니다. FF - getCustomModels** 및 **보내기**&#x200B;를 클릭합니다.

![Firefly 사용자 지정 모델](./images/ffcm31.png){zoomable="yes"}

이전에 만든 사용자 지정 모델(`--aepUserLdap-- - Citi Signal Router Model`)이 응답의 일부로 표시됩니다. 필드 **assetId**&#x200B;은(는) 다음 요청에서 참조되는 사용자 지정 모델의 고유 식별자입니다.

![Firefly 사용자 지정 모델](./images/ffcm32.png){zoomable="yes"}

**2 요청을 엽니다.** 비동기 이미지를 생성합니다. 이 예에서는 사용자 정의 모델을 기반으로 2개의 변형을 생성하도록 요청합니다. 이 경우 `a white router on a volcano in Africa`인 프롬프트를 자유롭게 업데이트하십시오.

**보내기**&#x200B;를 클릭합니다.

![Firefly 사용자 지정 모델](./images/ffcm33.png){zoomable="yes"}

응답에 필드 **jobId**&#x200B;이(가) 있습니다. 이 2개의 이미지를 생성하는 작업이 현재 실행 중이며 다음 요청을 사용하여 상태를 확인할 수 있습니다.

![Firefly 사용자 지정 모델](./images/ffcm34.png){zoomable="yes"}

요청 **3을(를) 엽니다. CM 상태**&#x200B;을(를) 가져오고 **보내기**&#x200B;를 클릭합니다. 그런 다음 상태가 실행 중으로 설정되어 있는지 확인해야 합니다.

![Firefly 사용자 지정 모델](./images/ffcm35.png){zoomable="yes"}

몇 분 후 **3 요청에 대해 다시**&#x200B;보내기&#x200B;**를 클릭하세요. CM 상태**&#x200B;을(를) 가져옵니다. 그런 다음 상태가 **성공**(으)로 변경되고 출력의 일부로 두 개의 이미지 URL이 표시됩니다. 두 파일을 모두 열려면 를 클릭합니다.

![Firefly 사용자 지정 모델](./images/ffcm36.png){zoomable="yes"}

이 예에서 생성된 첫 번째 이미지입니다.

![Firefly 사용자 지정 모델](./images/ffcm37.png){zoomable="yes"}

이 예에서 생성된 두 번째 이미지입니다.

![Firefly 사용자 지정 모델](./images/ffcm38.png){zoomable="yes"}

이제 이 연습을 완료했습니다.

## 다음 단계

[요약 및 혜택](./summary.md){target="_blank"}(으)로 이동

[Photoshop API 작업](./ex3.md){target="_blank"}(으)로 돌아가기

[Adobe Firefly 서비스 개요](./firefly-services.md){target="_blank"}(으)로 돌아가기
