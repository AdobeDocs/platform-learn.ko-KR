---
title: Target 확장과 Decisioning 확장 비교
description: 기능, 함수, 설정 및 데이터 흐름을 포함하여 Target 확장과 Decisioning 확장 간의 차이점에 대해 알아봅니다.
exl-id: 6c854049-4126-45cf-8b2b-683cf29549f3
source-git-commit: 314f0279ae445f970d78511d3e2907afb9307d67
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 1%

---

# Target 확장과 Decisioning 확장 비교

Adobe Journey Optimizer - Decisioning 확장 프로그램은 모바일 앱용 Adobe Target 확장 프로그램과 다릅니다. 다음 표는 마이그레이션 프로세스 중에 초점을 두어야 할 구현 영역을 평가하는 데 도움이 되는 참조입니다.

아래 정보를 검토하고 현재 기술 Target 확장 구현을 평가한 후 다음을 이해할 수 있어야 합니다.

- Adobe Journey Optimizer - Decisioning에서 지원하는 Target 기능
- 어떤 Adobe Target 확장 기능에 Adobe Journey Optimizer - Decisioning 기능이 포함됩니까?
- Target 설정이 Adobe Journey Optimizer에 적용되는 방법 - Decisioning
- Adobe Journey Optimizer - Decisioning 확장을 사용하여 데이터가 흐르는 방식

## 운영상의 차이점

| | Target 확장 | Decisioning 확장 |
|---|---|---|
| 프로세스 | Target 구현을 변경하면 Analytics와 같은 다른 애플리케이션과 비교하여 케이던스 또는 QA 요구 사항이 다른 프로세스를 따를 수 있습니다. | Decisioning 확장 구현을 변경하면 모든 다운스트림 애플리케이션을 고려해야 하며 QA 및 게시 프로세스를 적절하게 조정해야 합니다. |
| 공동 작업 | Target에 대한 데이터는 Target 호출에서 직접 전달할 수 있습니다. Target 보고 소스가 Adobe Analytics(A4T)인 경우 Target 컨텐츠 표시 및 상호 작용을 위해 Target 확장의 적절한 추적 메서드가 호출될 때 Target에 관련된 데이터를 Adobe Analytics에 전달할 수도 있습니다. | Target 보고 소스가 Adobe Analytics(A4T)이고, Adobe Analytics이 데이터 스트림에서 활성화되어 있으며, Target 콘텐츠가 표시되고 상호 작용할 때 Decisioning 확장의 적절한 추적 메서드가 호출되는 경우 Decisioning 확장 호출에서 전달된 데이터는 Target과 Analytics 모두에 전달될 수 있습니다. |

## 기본 차이점

| | Target 확장 | Decisioning 확장 |
|---|---|---|
| 종속성 | Mobile Core SDK에만 종속 | Mobile Core 및 Edge Network SDK에 따라 다름 |
| 라이브러리 기능 | Adobe Target에서만 콘텐츠 가져오기 지원 | Adobe Target 및 Offer Decisioning에서 콘텐츠 가져오기 지원 |
| 요청 | 대상 호출은 대개 다른 네트워크 호출과 독립적입니다 | 대상 네트워크 호출은 Edge SDK의 메시징 과 같은 다른 Edge 기반 솔루션에 대한 네트워크 호출과 함께 큐에 올라가 순차적으로 실행됩니다. |
| Edge Network | 데이터 수집 UI의 [Target 구성](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui)에 지정된 클라이언트 코드(clientcode.tt.omtrdc.net)와 함께 Target 서버 값 또는 Adobe Experience Cloud Edge Network을 사용합니다. | 데이터 수집 UI의 Adobe Experience Platform [Edge Network 구성](https://developer.adobe.com/client-sdks/edge/edge-network/#configure-the-edge-network-extension-in-data-collection-ui)에 지정된 Edge 네트워크 도메인을 사용합니다. |
| 기본 용어 | mbox, 타겟 매개 변수 | Target 매개 변수에 대한 DecisionScope, 맵(Android)/사전(iOS) |
| 기본 콘텐츠 | 네트워크 호출에 실패하거나 오류가 발생하는 경우 반환되는 TargetRequest에 클라이언트측 기본 콘텐츠를 전달할 수 있습니다. | 클라이언트측 기본 컨텐츠 전달을 허용하지 않습니다. 네트워크 호출에 실패하거나 오류가 발생하는 경우 콘텐츠를 반환하지 않습니다. |
| Target 매개 변수 | 요청당 글로벌 TargetParameters 및 mbox당 다른 TargetParameters를 전달할 수 있습니다. | 요청당 글로벌 TargetParameters 전달만 허용 |



## 기능 비교

| 기능 | Target 확장 | Decisioning 확장 프로그램(Edge을 통한 Target) |
|---|---|---|
| 프리페치 모드 | 지원됨 | 지원됨 |
| 실행 모드 | 지원됨 | 지원되지 않음 |
| 사용자 지정 매개 변수 | 지원됨 | 지원됨* |
| 프로필 매개 변수 | 지원됨 | 지원됨* |
| 엔티티 매개 변수 | 지원됨 | 지원됨* |
| 타깃 대상자 | 지원됨 | 지원됨 |
| Real-Time CDP 대상 | 지원되지 않음 | 지원됨 |
| Real-Time CDP 속성 | 지원되지 않음 | 지원됨 |
| 라이프사이클 지표 | 지원됨 | 데이터 수집 규칙을 통해 지원 |
| thirdPartyId (mbox3rdPartyId) | 지원됨 | ID 맵 및 데이터 스트림의 Target 타사 ID 네임스페이스를 통해 지원됨 |
| 알림(표시, 클릭) | 지원됨 | 지원됨 |
| 응답 토큰 | 지원됨 | 지원됨 |
| Analytics for Target (A4T) | 클라이언트측 전용 | 클라이언트측 및 서버측 |
| 모바일 미리 보기(QA 모드) | 지원됨 | Assurance에 대한 제한된 지원 |

>[!IMPORTANT]
>
> \* 요청에 전송된 매개 변수는 요청의 모든 범위에 적용됩니다. 서로 다른 범위에 대해 서로 다른 매개 변수를 설정해야 하는 경우 추가 요청을 수행해야 합니다.



## 주목할 만한 설명선

>[!NOTE]
>
>앱 코드를 Decisioning 확장으로 마이그레이션한 후에도 Target 확장 태그 구성 및 설정을 유지하십시오. 이렇게 하면 앱을 새 버전으로 업데이트하지 않은 고객에게 Target이 계속 작동하도록 하는 데 도움이 됩니다.
>
>Analytics for Target 통합(A4T)을 사용하는 경우 Target 구현을 Decisioning 확장으로 마이그레이션하는 동시에 Edge Bridge 확장 프로그램으로 Analytics 구현도 마이그레이션해야 합니다.





>[!IMPORTANT]
>
> 앱 코드를 Decisioning 확장으로 마이그레이션한 후에도 Target 확장 설정 을 유지합니다. 이렇게 하면 앱을 아직 업데이트하지 않은 사용자에게 Target이 계속 작동하도록 하는 데 도움이 됩니다.

## Decisioning 확장 시스템 다이어그램

다음 다이어그램은 Adobe Journey Optimizer - Decisioning 확장을 사용하는 데이터 흐름을 이해하는 데 도움이 됩니다.

![클라이언트측 모바일 SDK을 통한 Adobe Target Edge Decisioning](assets/diagram.png)


>[!NOTE]
>
>Target 확장에서 Decisioning 확장으로 모바일 Target을 성공적으로 마이그레이션할 수 있도록 지원하기 위해 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)에 게시하여 알려 주십시오.
