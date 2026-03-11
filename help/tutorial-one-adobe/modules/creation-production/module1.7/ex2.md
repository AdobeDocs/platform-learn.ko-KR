---
title: 프로그래밍 방식으로 사용자 지정 워크플로우 실행
description: 프로그래밍 방식으로 사용자 지정 워크플로우 실행
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
source-git-commit: a3a78b12f8244c8288eb0fffc82ad769776eb118
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---

# 1.7.2 프로그래밍 방식으로 사용자 지정 워크플로우 실행

## 1.7.2.1 Postman으로 사용자 지정 워크플로우 실행

이전 연습에서 워크플로우를 게시한 후에는 다음과 같은 메시지가 표시됩니다. 샘플 페이로드를 복사하려면 **복사** 단추를 클릭하십시오.

![Firefly 사용자 지정 워크플로](./images/ffcw61.png)

Postman을 열고 **Firefly 사용자 지정 워크플로**&#x200B;라는 이름을 사용하여 새 **컬렉션**&#x200B;을 만듭니다. 그런 다음 **요청 추가**&#x200B;를 클릭합니다.

![Firefly 사용자 지정 워크플로](./images/ffcw62.png)

그러면 새 빈 요청이 표시됩니다. 주소 표시줄에 게시된 워크플로우에서 복사한 페이로드를 붙여 넣습니다.

Postman은 붙여넣은 cURL 명령을 인식하고 페이로드에서 모든 정보를 가져와서 올바른 방식으로 요청에 추가합니다.

![Firefly 사용자 지정 워크플로](./images/ffcw63.png)

이제 이 **Header** 변수가 표시됩니다.

![Firefly 사용자 지정 워크플로](./images/ffcw64.png)

**본문**(으)로 이동하십시오. 여기서 이와 유사한 내용이 표시됩니다.

![Firefly 사용자 지정 워크플로](./images/ffcw65.png)

이제 이 요청의 본문에 필요한 지침을 제공해야 합니다. 프로그래밍 방식으로 파일을 사용하는 경우 사전 서명된 URL을 사용해야 합니다. 이 연습에서는 이 연습에 포함된 3개의 이미지에 대해 아래에 사전 서명된 URL을 찾을 수 있습니다. 이러한 사전 서명된 URL은 Microsoft Azure 스토리지 기능을 사용하여 생성되었습니다. 사전 서명된 URL을 만드는 방법에 대해 자세히 알아보려면 다음을 참조하세요. [Microsoft Azure 및 사전 서명된 URL을 사용하여 Firefly 프로세스를 최적화](./../module1.1/ex2.md).

이 연습에서는 아래 URL을 사용할 수 있으므로 사전 서명된 URL을 직접 새로 만들 필요가 없습니다.

- **airpods.jpg**

```
https://techinsiders.blob.core.windows.net/vangeluw/airpods.jpg?sv=2023-01-03&st=2026-03-11T01%3A22%3A04Z&se=2027-03-12T01%3A22%3A00Z&sr=b&sp=r&sig=MmQi9lS4lm4DJM1BELmZZM7VLa4ln5zYOcuGisLnrz4%3D
```

- **watch.jpg**

```
https://techinsiders.blob.core.windows.net/vangeluw/watch.jpg?sv=2023-01-03&st=2026-03-11T01%3A26%3A54Z&se=2027-03-12T01%3A26%3A00Z&sr=b&sp=r&sig=xCwQ09E%2F%2FT%2B7RLcb31Fum4uUBfsX0xHITKZTz4Ds9Zs%3D
```

- **phone.jpg**

```
https://techinsiders.blob.core.windows.net/vangeluw/phone.png?sv=2023-01-03&st=2026-03-11T01%3A27%3A20Z&se=2027-03-12T01%3A27%3A00Z&sr=b&sp=r&sig=VVbX88P2sFSHHo9lmgoRhXRIXb42c0nDQhM9Z8nUG%2Bc%3D
```

Postman 요청의 일부로 프롬프트를 제공해야 합니다. 다음은 사용할 수 있는 프롬프트입니다.

- **프롬프트 1**:

```
magazine quality photo of a phone on a red pedestal with a pink background surrounded by origami style pink paper hearts
```

- **프롬프트 2**:

```
background hearts fluttering
```

다음은 샘플 페이로드이지만 **node_id** 필드가 워크플로우에 고유하므로 복사하여 다시 사용할 수 없습니다. 따라서 이는 페이로드가 어떻게 표시되어야 하는지 알려 주기 위한 것입니다.

```json
{
    "workflow": {
        "workflowId": "e0c63806-cf7c-442d-8884-26d57e9c0518",
        "inputs": [
            [
                {
                    "node_id": "node_1772156869527_d8mjasues_1_u10dlg",
                    "content": [
                        {
                            "presignedUrl": "https://techinsiders.blob.core.windows.net/vangeluw/airpods.jpg?sv=2023-01-03&st=2026-03-11T01%3A22%3A04Z&se=2027-03-12T01%3A22%3A00Z&sr=b&sp=r&sig=MmQi9lS4lm4DJM1BELmZZM7VLa4ln5zYOcuGisLnrz4%3D",
                            "storageType": "Azure"
                        }
                    ]
                },
                {
                    "node_id": "node_1772157264659_oq2csr2nn_5_fh5hek",
                    "content": "magazine quality photo of a phone on a red pedestal with a pink background surrounded by origami style pink paper hearts"
                },
                {
                    "node_id": "node_1772157397147_qdwxiyktg_8_nm0o2k",
                    "content": "background hearts fluttering"
                }
            ]
        ]
    }
}
```

페이로드를 변경하면 다음과 같이 표시됩니다. 완료되면 **보내기**&#x200B;를 클릭하세요. 그런 다음 **CMD + S** 또는 **CTRL + S**&#x200B;을(를) 사용하여 요청을 **저장**&#x200B;합니다.

![Firefly 사용자 지정 워크플로](./images/ffcw66.png)

이제 응답 페이로드에서 두 개의 링크를 찾을 수 있습니다. 이러한 링크를 사용하면 워크플로우의 **상태**&#x200B;를 쿼리할 수 있으며 상태가 **완료됨**&#x200B;이면 **결과** URL을 사용하여 생성된 이미지 및 비디오를 검색할 수 있습니다.

**상태** URL을 선택하고 복사하십시오.

![Firefly 사용자 지정 워크플로](./images/ffcw67.png)

현재 사용 중인 요청의 세 점을 클릭한 다음 **복제**&#x200B;를 선택합니다.

![Firefly 사용자 지정 워크플로](./images/ffcw69.png)

새 요청에서 요청 유형을 **GET**(으)로 변경하고 URL을 방금 복사한 상태 URL로 바꿉니다.

![Firefly 사용자 지정 워크플로](./images/ffcw70.png)

**본문**&#x200B;에서 모든 항목이 삭제되었는지 확인하십시오. 그런 다음 **보내기**&#x200B;를 클릭합니다. 그러면 상태를 표시하는 유사한 응답 페이로드를 받게 됩니다. 상태가 **완료됨**(으)로 변경될 때까지 이 요청을 다시 보낼 수 있습니다. 요청을 **저장**&#x200B;하려면 **CMD + S** 또는 **CTRL + S**&#x200B;을(를) 사용하는 것을 잊지 마십시오.

![Firefly 사용자 지정 워크플로](./images/ffcw71.png)

처음 **POST** 요청으로 돌아갑니다. 이제 **결과** URL을 복사합니다.

![Firefly 사용자 지정 워크플로](./images/ffcw72.png)

만든 두 번째 요청에서 세 점 **..**&#x200B;을(를) 클릭한 다음 **복제**&#x200B;를 선택합니다.

![Firefly 사용자 지정 워크플로](./images/ffcw73.png)

새 요청에서 복사한 **결과** URL을 붙여 넣은 다음 **보내기**&#x200B;를 클릭합니다. 요청을 **저장**&#x200B;하려면 **CMD + S** 또는 **CTRL + S**&#x200B;을(를) 사용하는 것을 잊지 마십시오.

![Firefly 사용자 지정 워크플로](./images/ffcw74.png)

응답 페이로드에서 아래로 스크롤하여 생성된 이미지 및 비디오에 대한 참조를 찾습니다. 이러한 파일을 열려면 링크를 클릭하십시오.

![Firefly 사용자 지정 워크플로](./images/ffcw75.png)

생성된 이미지입니다.

![Firefly 사용자 지정 워크플로](./images/ffcw76.png)

## 1.7.2.2 Workfront Fusion으로 사용자 지정 워크플로우 실행

[https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}(으)로 이동합니다. **Workfront Fusion**&#x200B;을 엽니다.

![WF Fusion](./images/wffusion1.png)

**시나리오**(으)로 이동합니다. 아직 폴더가 없는 경우 폴더를 만들고 폴더 이름에 대해 `--aepUserLdap--`을(를) 사용합니다. 폴더를 선택한 다음 **새 시나리오 만들기**&#x200B;를 선택합니다.

![WF Fusion](./images/wffusion2.png)

그럼 이걸 보셔야죠

![WF Fusion](./images/wffusion3.png)

이전 연습에서 워크플로우를 게시한 후에는 다음과 같은 메시지가 표시됩니다. 샘플 페이로드를 복사하려면 **복사** 단추를 클릭하십시오.

![Firefly 사용자 지정 워크플로](./images/ffcw61.png)

Workfront Fusion 시나리오로 돌아갑니다. 시나리오에 복사한 페이로드를 붙여넣으려면 **CMD + V** 또는 **CTRL + V**&#x200B;을(를) 사용합니다. Workfront Fusion은 cURL 요청을 자동으로 감지하고 새 **HTTP - 요청 만들기** 모듈을 자동으로 만듭니다.

**clock** 아이콘을 **HTTP - 요청** 모듈로 끌어옵니다.

![WF Fusion](./images/wffusion5.png)

그럼 이걸 보셔야죠 **HTTP - 요청** 모듈을 클릭하여 엽니다.

![WF Fusion](./images/wffusion6.png)

**Header** 변수를 이미 사용할 수 있습니다.

![WF Fusion](./images/wffusion7.png)

아래로 스크롤하여 기본 페이로드를 확인합니다. JSON 페이로드를 아름답게 하기 위해 표시된 대로 **아이콘**&#x200B;을 클릭합니다.

![WF Fusion](./images/wffusion8.png)

Postman으로 돌아가서 첫 번째 **POST** 요청으로 이동합니다. 페이로드를 복사합니다.

![WF Fusion](./images/wffusion9.png)

Workfront Fusion 시나리오로 돌아갑니다. 기존 기본 페이로드를 Postman에서 복사한 페이로드로 바꿉니다. JSON 페이로드를 아름답게 하기 위해 표시된 대로 **아이콘**&#x200B;을 클릭합니다.

**응답 구문 분석**&#x200B;에 대한 확인란을 선택하십시오.

**확인**&#x200B;을 클릭합니다.

![WF Fusion](./images/wffusion10.png)

변경 내용을 저장한 다음 **한 번 실행**&#x200B;을 클릭합니다.

![WF Fusion](./images/wffusion11.png)

시나리오가 실행되면 Postman에서 수행한 것과 유사한 응답을 볼 수 있습니다. 이제 Workfront Fusion에서 이 정보를 사용할 수 있으므로 상태가 완료될 때까지 **상태** URL을 폴링하도록 빌드할 수 있으며, 상태가 완료되면 **결과** URL을 사용하여 생성된 이미지 및 비디오를 수집할 수 있습니다.

![WF Fusion](./images/wffusion12.png)

## 다음 단계

[Firefly 사용자 지정 워크플로우로 돌아가기](./workflowbuilder.md){target="_blank"}

[모든 모듈](./../../../overview.md){target="_blank"}(으)로 돌아가기
