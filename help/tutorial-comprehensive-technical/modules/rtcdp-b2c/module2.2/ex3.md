---
title: 고객 AI - 점수 대시보드 및 세분화(예측 및 조치 수행)
description: 고객 AI - 점수 대시보드 및 세분화(예측 및 조치 수행)
kt: 5342
doc-type: tutorial
exl-id: 4dd8489a-65e4-489a-9228-3c642b10e761
source-git-commit: b53ee64ae8438b8f48f842ed1f44ee7ef3e813fc
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# 2.2.3 Customer AI - 채점 대시보드 및 세그멘테이션(예측 및 작업 수행)

고객 AI 인스턴스가 모델 실행을 완료하면 평가되는 성향 점수를 시각화하여 향후 30일 이내에 구매를 수행하는 고객을 예측할 수 있습니다.

![AI](./images/caiinstancesummary1.png)

>[!NOTE]
>
>**성공** 상태의 Customer AI 인스턴스만 서비스의 인사이트를 미리 볼 수 있습니다.

## 성향 예측

이제 고객 AI 인스턴스 모델에서 생성된 예측 성향을 검토해 보겠습니다. 인스턴스 이름을 클릭하여 대시보드를 봅니다.

![AI](./images/caimodels1.png)

Customer AI 대시보드에는 모델이 평가할 점수, 모집단 분포 및 영향력 있는 요인에 대한 요약이 표시됩니다.

![AI 설명](./images/caidescription.png)

영향력 있는 요소를 마우스로 가리키면 데이터 배포의 추가 분석을 볼 수 있습니다.

![영향 요소](./images/caiinfluencefactors.png)

## 비즈니스 작업

### 고객 세그먼트화

Customer AI 대시보드를 사용하면 한 번의 클릭으로 세그먼트를 정의할 수 있습니다. 성향 카드에서 **세그먼트 만들기** 단추를 클릭합니다.

![세그먼트 만들기](./images/caiinfluencefactors1.png)

세그먼트 정의가 자동으로 만들어지는 것을 볼 수 있습니다.

![세그먼트 규칙](./images/caicreatesegment.png)

`--aepUserLdap-- - Customer AI High Propensity` 명명 규칙에 따라 세그먼트에 이름을 지정하십시오. **Publish**&#x200B;을(를) 클릭합니다.

![세그먼트 규칙](./images/caicreatesegment1.png)

이제 Real-time CDP, Journey Optimizer 및 Adobe Target과 같은 을 사용하여 타깃팅에 이 세그먼트를 사용할 수 있습니다.

## 정리

불필요한 데모 데이터가 사용자 환경에 보관되지 않도록 하려면 이 연습을 성공적으로 완료한 후 데이터 집합 `--aepUserLdap-- - Demo System - Customer Experience Event Dataset`을(를) 삭제하십시오. 데모 데이터를 삭제하지 않으면 AEP 인스턴스에 비용이 발생합니다.

![프로필](./images/cleanup.png)

다음 단계: [요약 및 이점](./summary.md)

[모듈 2.2로 돌아가기](./intelligent-services.md)

[모든 모듈로 돌아가기](./../../../overview.md)
