---
title: Target 확장과 Decisioning 확장 비교
description: 기능, 함수, 설정 및 데이터 흐름을 포함하여 Target 확장과 Decisioning 확장 간의 차이점에 대해 알아봅니다.
source-git-commit: 78d04d625aa55ce5eb76615c220b49aefd958431
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 1%

---

# Target 확장과 Decisioning 확장 비교

Adobe Journey Optimizer - Decisioning 확장 프로그램은 모바일 앱용 Adobe Target 확장 프로그램과 다릅니다. 다음 표는 마이그레이션 프로세스 중에 초점을 두어야 할 구현 영역을 평가하는 데 도움이 되는 참조입니다.

아래 정보를 검토하고 현재 기술 Target 확장 구현을 평가한 후 다음을 이해할 수 있어야 합니다.

- Adobe Journey Optimizer - Decisioning에서 지원하는 Target 기능
- 어떤 Adobe Target 확장 기능에 Adobe Journey Optimizer - Decisioning 기능이 포함됩니까?
- Target 설정이 Adobe Journey Optimizer에 적용되는 방법 - Decisioning
- Adobe Target 확장과 Adobe Journey Optimizer - Decisioning 확장의 데이터 흐름이 어떻게 다른지

Platform Web SDK를 처음 사용하는 경우 걱정하지 마십시오. 아래 항목은 이 자습서 전체에서 자세히 다룹니다.

## 기능 비교

| 기능 | Target 확장 | Decisioning 확장 프로그램(Edge을 통한 Target) |
|---|---|---|
| 프리페치 모드 | 지원됨 | 지원됨 |
| 실행 모드 | 지원됨 | 지원되지 않음 |
| 사용자 지정 매개 변수 | 지원됨 | mbox당 매개 변수는 지원되지 않습니다. |
| 시작 대상자 | 지원됨 | 지원됨 |
| 모바일 라이프사이클 지표를 사용한 대상자 세분화 | 지원됨 | 데이터 수집 규칙을 통해 지원 |
| thirdPartyId (mbox3rdPartyId) | ID 맵과 데이터 스트림의 네임스페이스 구성을 통해 지원됩니다 |
| 알림(표시, 클릭) | 지원됨 | 지원됨 |
| 응답 토큰 | 지원됨 | 지원됨 |
| 다이내믹 오퍼 | 지원됨 | 지원됨 |
| Analytics for Target (A4T) | 클라이언트측 전용 | 클라이언트측 및 서버측 |
| 모바일 미리 보기(QA 모드) | 지원됨 | 제한된 지원 |



## 주목할 만한 설명선

>[!NOTE]
>
>지정된 페이지에 대한 기존 AppMeasurement Adobe Analytics 구현을 유지하면서 Target을 Platform Web SDK로 마이그레이션하는 기능은 지원되지 않습니다.
>
> at.js(및 AppMeasurement.js) 구현을 Platform Web SDK에 한 번에 한 페이지씩 마이그레이션할 수 있습니다. 이 방법을 사용하는 경우 `configure` 명령을 사용하여 [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) 및 [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) 옵션을 `true`(으)로 설정하는 것이 좋습니다.

## Target 확장 함수 및 그에 해당하는 Decisioning 확장 함수

많은 Target 확장 기능에는 아래 표에 요약된 의사 결정 확장을 사용하는 동일한 접근 방식이 있습니다. [함수](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/)에 대한 자세한 내용은 Adobe Target 개발자 안내서를 참조하십시오.

| Target 확장 | Decisioning 확장 |
| --- | --- | 
| |  |

## Target 확장 설정 및 이에 상응하는 Decisioning 확장 기능

...의 다양한 설정으로 Target 확장을 구성하고 다운로드할 수 있습니다.

| Target 확장 | Decisioning 확장 |
| --- | --- | 
| |  |


## 시스템 다이어그램 비교

다음 다이어그램은 Adobe Journey Optimizer - Decisioning 확장을 사용하는 Target 구현과 Adobe Target 확장을 사용하는 구현 간의 데이터 흐름 차이를 이해하는 데 도움이 됩니다.

### Target 확장 시스템 다이어그램



### Decisioning 확장 시스템 다이어그램




>[!NOTE]
>
>Target 확장에서 Decisioning 확장으로 모바일 Target을 성공적으로 마이그레이션할 수 있도록 지원하기 위해 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)에 게시하여 알려 주십시오.
