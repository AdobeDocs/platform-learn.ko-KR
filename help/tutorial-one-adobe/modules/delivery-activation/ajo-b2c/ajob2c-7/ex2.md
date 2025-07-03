---
title: Offer Decisioning - 오퍼 및 의사 결정 ID 구성
description: Offer Decisioning - 오퍼 및 의사 결정 ID 구성
kt: 5342
doc-type: tutorial
source-git-commit: 13d790855601fa6f36c1afa0f2d5faad5fc07eb0
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 13%

---

# 3.7.2 오퍼 및 의사 결정 구성

## 3.7.2.1 개인화된 오퍼 만들기

이 연습에서는 4개의 **개인화된 오퍼**&#x200B;를 만듭니다. 이러한 오퍼를 생성할 때 고려해야 할 세부 사항은 다음과 같습니다.

| 이름 | 날짜 범위 | 이메일에 대한 이미지 링크 | 웹용 이미지 링크 | 텍스트 | 우선 순위 | 적격성 | 언어 | 캡핑 빈도 | 이미지 이름 |
|-----|------------|----------------------|--------------------|------|:--------:|--------------|:-------:|:-------:|:-------:|
| `--aepUserLdap-- - AirPods Max` | 오늘 - 1개월 후 | https://bit.ly/4a9RJ5d | Assets 라이브러리에서 선택 | `{{ profile.person.name.firstName }}, 10% discount on AirPods Max` | 25 | 모두 - 여성 고객 | 영어(미국) | 3 | Apple AirPods Max- Female.jpg |
| `--aepUserLdap-- - Galaxy S24` | 오늘 - 1개월 후 | https://bit.ly/3W8yuDv | Assets 라이브러리에서 선택 | `{{ profile.person.name.firstName }}, 5% discount on Galaxy S24` | 15 | 모두 - 여성 고객 | 영어(미국) | 3 | Galaxy S24 - Female.jpg |
| `--aepUserLdap-- - Apple Watch` | 오늘 - 1개월 후 | https://bit.ly/4fGwfxX | https://bit.ly/4fGwfxX | `{{ profile.person.name.firstName }}, 10% discount on Apple Watch` | 25 | 모두 - 남성 고객 | 영어(미국) | 3 | Apple 시계 - Male.jpg |
| `--aepUserLdap-- - Galaxy Watch 7` | 오늘 - 1개월 후 | https://bit.ly/4gTrkeo | Assets 라이브러리에서 선택 | `{{ profile.person.name.firstName }}, 5% discount on Galaxy Watch 7` | 15 | 모두 - 남성 고객 | 영어(미국) | 3 | Galaxy Watch7 - Male.jpg |

{style="table-layout:auto"}

[Adobe Journey Optimizer](https://experience.adobe.com)&#x200B;(으)로 이동하여 Adobe Experience Cloud에 로그인합니다. **Journey Optimizer**&#x200B;을(를) 클릭합니다.

![AOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Journey Optimizer의 **Home** 보기로 리디렉션됩니다. 먼저 올바른 샌드박스를 사용하고 있는지 확인하십시오. 사용할 샌드박스를 `--aepSandboxName--`이라고 합니다. 그러면 샌드박스 **의**&#x200B;홈`--aepSandboxName--` 보기에 있게 됩니다.

![AOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## 다음 단계

Experience Decisioning용 [3.7.3 Web SDK 설치](./ex3.md){target="_blank"}(으)로 이동

[경험 의사 결정](ajo-decisioning.md){target="_blank"}(으)로 돌아가기

[모든 모듈](./../../../../overview.md){target="_blank"}(으)로 돌아가기
