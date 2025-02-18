---
title: Offer Decisioning - 이메일에서 의사 결정 사용
description: 이메일에서 의사 결정 사용
kt: 5342
doc-type: tutorial
exl-id: c94b4ed4-0122-4cfd-a69f-40ae2063d449
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 1%

---

# 3.3.5 이메일에서 의사 결정 사용

이 연습에서는 의사 결정을 사용하여 이메일 및 SMS 게재를 개인화합니다.

**여정**(으)로 이동합니다. 연습 3.1.3에서 만든 여정(`--aepUserLdap-- - Registration Journey`)를 찾습니다. 여정을 클릭하여 엽니다.

![Journey Optimizer](./images/emailoffer1.png)

그러면 이걸 보게 될 거야. **클릭...**&#x200B;을(를) 더 추가한 다음 **새 버전 만들기**&#x200B;를 클릭합니다.

![Journey Optimizer](./images/journey1.png)

**새 버전 만들기**&#x200B;를 클릭합니다.

![Journey Optimizer](./images/journey2.png)

**전자 메일** 작업을 클릭한 다음 **콘텐츠 편집**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/journey3.png)

그러면 메시지 대시보드가 표시됩니다. **전자 메일 본문 편집**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/emailoffer2.png)

그러면 이걸 보게 될 거야. 새 **1:1 열** 구조 구성 요소를 캔버스로 드래그합니다.

![Journey Optimizer](./images/emailoffer6.png)

메뉴에서 **내용**(으)로 이동합니다. **오퍼 결정** 구성 요소를 선택하고 이 구성 요소를 표시된 대로 전자 메일의 콘텐츠 오퍼 자리 표시자로 끌어서 놓습니다. **추가**&#x200B;를 클릭합니다.

![Journey Optimizer](./images/emailoffer7.png)

이메일에 포함할 배치 유형을 선택합니다. **배치** 드롭다운 메뉴에서 **전자 메일 - 이미지**&#x200B;를 선택한 다음 결정 `--aepUserLdap-- - CitiSignal Decision`을(를) 선택합니다. **추가를 클릭합니다**.

![Journey Optimizer](./images/emailoffer8.png)

이제 모든 개인화된 오퍼와 대체 오퍼를 순환할 수 있으며 이러한 모든 오퍼는 이메일 디자이너 내에서 시각화됩니다. **저장**&#x200B;을 클릭합니다.

![Journey Optimizer](./images/emailoffer9.png)

이제 화살표를 클릭하여 이전 화면으로 돌아갑니다.

![Journey Optimizer](./images/emailoffer13.png)

왼쪽 상단 모서리의 화살표를 클릭하여 여정으로 돌아갑니다.

![Journey Optimizer](./images/emailoffer14.png)

**전자 메일** 작업을 닫으려면 **저장**&#x200B;을 클릭하세요.

![Journey Optimizer](./images/emailoffer14a.png)

업데이트된 여정을 게시하려면 **게시**&#x200B;를 클릭하십시오.

![Journey Optimizer](./images/emailoffer14b.png)

**게시**&#x200B;를 다시 클릭하여 확인합니다.

![Journey Optimizer](./images/emailoffer15.png)

이제 메시지가 게시되었습니다.

![Journey Optimizer](./images/emailoffer16.png)

데모 웹 사이트에서 새 계정을 만들면 이제 다음 이메일을 받게 됩니다.

![Journey Optimizer](./images/emailoffer17.png)

이 연습을 완료했습니다.

## 다음 단계

[3.3.6 API를 사용하여 의사 결정 테스트](./ex6.md){target="_blank"}(으)로 이동

[Offer Decisioning](offer-decisioning.md){target="_blank"}로 돌아가기

[모든 모듈](./../../../../overview.md){target="_blank"}(으)로 돌아가기
