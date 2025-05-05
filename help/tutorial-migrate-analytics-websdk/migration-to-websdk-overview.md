---
title: 태그를 사용하여 Adobe Analytics을 Web SDK으로 마이그레이션
description: Web SDK으로 마이그레이션하는 동안 수행할 단계와 그 과정에서 내려져야 할 결정에 대해 알아봅니다.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16755
exl-id: e578b669-42b4-46ae-b6e6-6688e5c5c772
source-git-commit: d6471c8e383e22fed4ad5870952d0d0470f593db
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 0%

---

# 태그를 사용하여 Adobe Analytics을 Web SDK으로 마이그레이션

Experience Platform 태그(이전의 Launch)의 Analytics 확장 기능을 사용하여 Adobe Analytics 구현을 Tags의 Web SDK 확장 기능을 사용하여 웹 SDK으로 마이그레이션하는 단계에 대해 알아봅니다. Tags의 Adobe Analytics 확장을 사용하면 &quot;AppMeasurement.js&quot; 코드가 백그라운드에서 사용됩니다. 따라서 이 자습서는 AppMeasurement을 Web SDK으로 마이그레이션하는 자습서로 생각할 수 있지만, 이 자습서는 Tags에 완전히 포함되어 있으며 JavaScript 구현으로 이동하거나 JavaScript 구현에서 이동하는 것은 포함하지 않습니다(Tags UI 내에서 사용되는 코드 제외). JavaScript 구현의 마이그레이션에 대해서는 [설명서](https://experienceleague.adobe.com/ko/docs/analytics/implementation/aep-edge/web-sdk/appmeasurement-to-web-sdk)를 참조하세요.

>[!NOTE]
>
>다음과 유사한 마이그레이션 튜토리얼을 사용할 수 있습니다.
>
> * [Adobe Target](../tutorial-migrate-target-websdk/introduction.md)
> * [Adobe Audience Manager](https://experienceleague.adobe.com/ko/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk)

>[!CAUTION]
>
> Platform Web SDK은 여러 Adobe 애플리케이션을 지원하므로 주어진 페이지의 모든 Adobe 라이브러리를 동시에 마이그레이션해야 합니다. 예를 들어 단일 페이지 _에서 Web SDK for Target과 Analytics용 AppMeasurement의 혼합 구현은 지원되지 않습니다_. 하지만 페이지 A의 웹 SDK과 페이지 B의 AppMeasurement이 있는 at.js 등의 서로 다른 페이지에 대한 혼합 구현이 지원됩니다.

## 이 자습서에서 얻을 수 있는 이점

Analytics 구현을 마이그레이션하는 단계로 들어가기 전에 Analytics용 _구현_&#x200B;을 변경/업데이트하는 작업을 정확히 이해하는 것이 중요합니다. 이 자습서를 마칠 때 보고서를 시작하고 모든 것이 동일하면 &quot;내가 왜 그 모든 작업을 수행했습니까?&quot;라고 자문할 수 있습니다. Analytics 구현을 위해 웹 SDK을 사용할 때의 이점에 대해 간략히 설명하는 다른 문서가 있지만 몇 가지는 다음과 같습니다.

1. 자사 디바이스 ID 지원
1. 향상된 성능
1. Adobe Experience Platform 애플리케이션 사용(새로운 사용 사례 활성화)으로 이동하여 향후 구현 증명

웹 SDK이 어떻게 유용할 수 있는지 자세히 알려면 Adobe Analytics 담당자에게 문의하십시오. 이 자습서를 진행하면서 마이그레이션을 수행하는 _방법_&#x200B;에 집중하겠습니다.

>[!IMPORTANT]
>
>이 구현 마이그레이션을 수행하는 주요 이유 중 하나는 Customer Journey Analytics, Real-Time CDP 또는 Journey Optimizer과 같은 Adobe Experience Platform 애플리케이션을 사용할 준비를 하는 것입니다(위#3 설명된 대로). 이러한 목적으로 웹 사이트 데이터를 사용하는 경우 이 자습서에는 포함되지 않은 추가 단계가 포함되지만, 이 자습서는 구현의 추가 진행에 대한 필수 조건이 됩니다. 따라서 이 자습서를 완료한 다음 동일한 웹 사이트 데이터를 Experience Platform에게 전송하는 데 필요한 단계를 계속 수행할 수 있습니다.

## 마이그레이션 메서드

이 마이그레이션 프로세스를 수행하는 데는 여러 가지 방법이 있을 수 있지만, 여기서 두 가지 사항에 대해 설명해야 합니다.

**메서드 1:** 기존 Tags 속성을 Web SDK으로 업데이트하여 새 데이터 요소를 만들고 속성에 이미 있는 규칙을 변경합니다.

**메서드 2:** 새 속성을 만든 다음(기존 속성을 복사하거나 새 속성을 만들어) Adobe Analytics 확장 대신 Web SDK을 사용하여 해당 새 속성을 구성할 수도 있습니다.

**이 마이그레이션 자습서에서는 메서드 1을 사용합니다.** 이 방법으로 속성과 연결된 포함 코드가 개발, 스테이징 및 프로덕션 사이트에 이미 포함되어 있으므로 포함 코드를 변경할 필요가 없습니다. 메서드 2로 진행하려면 새 속성의 **환경** 섹션에서 각 환경에 대한 새 포함 코드를 가져와 사이트의 헤드 섹션에 배치하는 것을 잊지 마십시오.

>[!NOTE]
>
>이 마이그레이션 중에 Tags의 기존 속성을 편집하는 것뿐이지만 주의하는 것이 좋습니다. 따라서 마이그레이션을 시작하기 전에 현재 속성의 복사본을 만드는 것이 좋습니다. 그렇게 하면 언제든지 복사본으로 이동하여 변경 전 상황을 보고 코드를 가져올 수 있습니다.
>혹시 모르니까 조심하는 게 좋을 거야. 가서 당신의 재산을 복사하세요. 네가 돌아올 때까지 여기서 기다릴게.

## Analytics 구현을 웹 SDK으로 마이그레이션하는 단계

단계를 거치면서 이해해야 할 몇 가지 주의 사항이 있습니다.

1. 먼저, 이 모든 단계가 필요할 수도 있고 필요하지 않을 수도 있습니다. 예를 들어 사용자 지정 코드 마이그레이션에 대한 단원이 있습니다. 사용자 지정 코드(플러그인 사용 포함)를 사용하지 않는 태그 구현이 있는 경우에는 이 단원이 필요하지 않습니다. 대부분의 사용자에게 필요한 단원을 포함시키려고 시도했으므로, 마이그레이션 중에 사이트를 조정할 필요가 있는지 단원 전체를 읽으십시오.
1. 또한 모든 사용자가 사용하는 사용 사례의 100%를 다루는 마이그레이션 튜토리얼을 만들 수 있는 방법도 없습니다. 앞의 항목에서 언급했듯이 대부분의 사람들에게 필요한 교훈을 포함시키려고 했으며, 이는 주요 사용 사례의 대부분을 차지합니다. 그러나 이 자습서에서 다루지 않는 사용 사례는 틀림없이 있을 것입니다. 이 경우 포함된 단원이 사용 사례에 맞게 마이그레이션하는 방법을 잘 보여 주는지 확인하십시오. [Experience League 커뮤니티에서 동료에게 데이터 수집을 요청](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/ct-p/adobe-launch-community?profile.language=ko)할 수도 있습니다.

마이그레이션 프로세스에는 다음과 같은 주요 단계가 포함됩니다.

1. 마이그레이션 유효성 검사 보고서 세트를 만듭니다.
1. 데이터 스트림을 만들고 구성합니다.
1. Tags(이전 Adobe Launch)에서 Web SDK 확장 기능을 추가하고 구성합니다.
1. 웹 SDK을 통해 데이터를 전송할 새 데이터 요소를 만듭니다.
1. 웹 SDK 데이터 요소 및 작업을 사용하도록 기본 페이지 로드 규칙을 마이그레이션합니다.
1. 규칙 또는 플러그인의 사용자 지정 코드를 마이그레이션합니다.
1. Publish 구현 변경 사항.
1. 변경 사항을 디버깅하고 유효성을 검사하고 기본 페이지 로드 규칙 및 이와 관련된 변수의 유효성을 검사하는 방법을 이해합니다. 그런 다음 변경 작업을 수행할 때 마이그레이션 내내 이 유효성 검사를 계속해야 합니다.
1. 추가 페이지 로드 규칙 마이그레이션
1. 사용자 지정 링크 규칙을 마이그레이션합니다.
1. 전체 유효성 검사 후 Analytics 확장에 대한 참조를 제거하고 확장 자체를 제거합니다.
1. 모든 변경 사항을 적용한 다음 라이브러리를 스테이징에 푸시한 다음 프로덕션에 푸시합니다.
1. 모든 것이 완료되면 다시 테스트하십시오. 이전 Analytics 코드에 대한 참조를 제거하여 변경했으며 모든 것이 계속 제대로 작동하는지 확인해야 하므로 이 작업이 필요합니다.

>[!NOTE]
>
>Web SDK으로 Analytics를 마이그레이션하는 데 도움이 되도록 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-analytics-to-web-sdk-using/m-p/732308?profile.language=ko#M604){target="_blank"}에 게시하여 알려 주십시오.

