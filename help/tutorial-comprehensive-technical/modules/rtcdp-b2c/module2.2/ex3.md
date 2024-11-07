---
title: 고객 AI - 점수 대시보드 및 세분화(예측 및 조치 수행)
description: 고객 AI - 점수 대시보드 및 세분화(예측 및 조치 수행)
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 1%

---

# 2.2.3 Customer AI - 채점 대시보드 및 세그멘테이션(예측 및 작업 수행)

고객 AI 인스턴스가 모델 실행을 완료하면 평가되는 성향 점수를 시각화하여 향후 30일 이내에 구매를 수행하는 고객을 예측할 수 있습니다.

![AI](./images/caimodels.png)

>[!NOTE]
>
>**성공** 상태의 Customer AI 인스턴스만 서비스의 인사이트를 미리 볼 수 있습니다.

## 2.2.3.1 성향 예측

이제 고객 AI 인스턴스 모델에서 생성된 예측 성향을 검토해 보겠습니다. 인스턴스 이름을 클릭하여 대시보드를 봅니다.

![AI](./images/caimodels1.png)

Customer AI 대시보드에는 모델이 평가할 점수, 모집단 분포 및 영향력 있는 요인에 대한 요약이 표시됩니다.

![AI 설명](./images/caidescription.png)

![대시보드 요약](./images/caidashboard.png)

영향력 있는 요소를 마우스로 가리키면 데이터 배포의 추가 분석을 볼 수 있습니다.

![영향 요소](./images/caiinfluencefactors.png)

## 2.2.3.2 비즈니스 작업

### 2.2.3.2.1 고객 세그먼트화

Customer AI 대시보드를 사용하면 한 번의 클릭으로 세그먼트를 정의할 수 있습니다. 성향 카드에서 **세그먼트 만들기** 단추를 클릭합니다.

![세그먼트 만들기](./images/caiinfluencefactors1.png)

세그먼트 정의가 자동으로 만들어지는 것을 볼 수 있습니다.

![세그먼트 규칙](./images/caicreatesegment.png)

`--demoProfileLdap-- - Customer AI High Propensity` 명명 규칙에 따라 세그먼트에 이름을 지정하십시오. **저장**&#x200B;을 클릭합니다.

![세그먼트 규칙](./images/caicreatesegment1.png)

이제 실시간 CDP, Journey Orchestration 및 Adobe Target과 같은 을 사용하여 타깃팅에 이 세그먼트를 사용할 수 있습니다.

### 2.2.3.2.2 프로필 개요

고객 AI 성향 점수는 실시간 고객 프로필의 일부가 되므로 개별 고객의 점수를 볼 수 있습니다.

Adobe Experience Platform에서 왼쪽 메뉴에서 **프로필**(으)로 이동한 다음 **찾아보기**&#x200B;를 선택합니다.

수집한 JSON 파일에서 사용할 수 있는 식별자(예: **EMAIL hbirkenshawa@businessweek.com**)를 사용하여 프로필을 검색합니다. **프로필 ID**&#x200B;를 클릭하여 프로필을 엽니다.

![프로필](./images/profile1.png)

그러면 다음과 같은 결과가 표시됩니다.

![프로필](./images/profile2.png)

Customer AI 모델의 출력이 포함된 **특성**(으)로 이동합니다.

![프로필](./images/profile3.png)

아래로 스크롤하여 고객 AI 모델로 계산된 성향 점수를 확인합니다.

![프로필](./images/profile4.png)

다음 단계: [요약 및 이점](./summary.md)

[모듈 2.2로 돌아가기](./intelligent-services.md)

[모든 모듈로 돌아가기](./../../../overview.md)
