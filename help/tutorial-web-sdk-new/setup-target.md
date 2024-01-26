---
title: Platform Web SDK를 사용하여 Adobe Target 설정
description: Platform Web SDK를 사용하여 Adobe Target을 구현하는 방법에 대해 알아봅니다. 이 단원은 Web SDK를 사용하여 Adobe Experience Cloud 구현 자습서의 일부입니다.
solution: Data Collection, Target
source-git-commit: 324ce76ff9f6b926ca330de1a1e827f8e88dc12d
workflow-type: tm+mt
source-wordcount: '4282'
ht-degree: 0%

---

# Platform Web SDK를 사용하여 Adobe Target 설정

Platform Web SDK를 사용하여 Adobe Target을 구현하는 방법에 대해 알아봅니다. 경험을 전달하는 방법과 추가 매개 변수를 Target에 전달하는 방법을 알아봅니다.

[Adobe Target](https://experienceleague.adobe.com/docs/target/using/target-home.html) 은 사용자의 웹 및 모바일 사이트, 앱 및 기타 디지털 채널의 매출을 극대화하도록 고객의 경험을 조정하고 개인화하는 데 필요한 모든 기능을 제공하는 Adobe Experience Cloud 애플리케이션입니다.


## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* 비동기 태그 포함 코드와 함께 Target을 사용할 때 깜박임을 방지하기 위해 Platform Web SDK 사전 숨김 코드 조각을 추가하는 방법을 이해합니다
* Target 기능을 사용하도록 데이터 스트림 구성
* 페이지가 로드될 때 시각적 개인화 결정 렌더링(이전에는 &quot;글로벌 mbox&quot;라고 함)
* Target에 XDM 데이터 전달 및 Target 매개 변수에 대한 매핑 이해
* 프로필 및 엔티티 매개 변수와 같은 사용자 지정 데이터를 Target에 전달
* Platform Web SDK를 사용하여 Target 구현의 유효성 검사
* Adobe Analytics 요청과 별도로 Target 제안 요청을 보내고 해당 표시 이벤트를 나중에 해결합니다.

>[!TIP]
>
>다음 참조: [Target을 at.js 2.x에서 Platform Web SDK로 마이그레이션](/help/tutorial-migrate-target-websdk/introduction.md) 기존 at.js 구현을 마이그레이션하는 단계별 안내서에 대한 자습서입니다.


## 전제 조건

이 섹션의 학습 내용을 완료하려면 먼저 다음을 수행해야 합니다.

* 데이터 요소 및 규칙 설정을 포함하여 Platform Web SDK의 초기 구성에 대한 모든 단원을 완료합니다.
* 다음 항목이 있는지 확인합니다. [편집자 또는 승인자 역할](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) Adobe Target.
* 설치 [시각적 경험 작성기 Helper 확장 프로그램](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) Google Chrome 브라우저를 사용하는 경우
* Target에서 활동을 설정하는 방법을 이해할 수 있습니다. 새로 고침이 필요한 경우 다음 튜토리얼 및 안내서가 이 단원에 유용합니다.
   * [VEC(시각적 경험 작성기) Helper 확장 프로그램 사용](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html)
   * [Visual Experience Composer 사용](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer.html)
   * [양식 기반 경험 작성기 사용](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer.html)
   * [경험 타깃팅 활동 만들기](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html)

## 깜박임 완화 추가

시작하기 전에 태그 라이브러리를 로드하는 방법에 따라 추가적인 플리커 처리 솔루션이 필요한지 여부를 결정합니다.

>[!NOTE]
>
>이 튜토리얼에서는 [Luma 사이트](https://luma.enablementadobe.com/content/luma/us/en.html) 태그 및 플리커 완화 의 비동기적 구현이 있습니다. 이 섹션은 Platform Web SDK에서 플리커 완화 가 작동하는 방식을 이해하는 데 참조되는 것입니다.


### 비동기 구현

태그 라이브러리가 비동기적으로 로드되면 Target이 콘텐츠 교환을 수행하기 전에 페이지에서 렌더링을 완료할 수 있습니다. 이 동작으로 인해 Target에서 지정한 개인화된 콘텐츠로 대체되기 전에 기본 콘텐츠가 잠깐 나타나는 &quot;깜박임&quot;이라고 하는 것이 나타날 수 있습니다. Adobe 이러한 깜박임을 방지하려면 비동기 태그 포함 코드 바로 앞에 특수 사전 숨김 코드 조각을 추가하는 것이 좋습니다.

이 코드 조각은 이미 Luma 사이트에 있지만 이 코드의 기능을 이해하기 위해 자세히 살펴보겠습니다.

```html
<script>
  !function(e,a,n,t){var i=e.head;if(i){
  if (a) return;
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, ".personalization-container { opacity: 0 !important }", 3000);
</script>
```

코드 조각 사전 숨김은 선택한 항목의 CSS 정의가 있는 페이지 헤드에 스타일 태그를 만듭니다. 이 스타일 태그는 Target에서 응답을 받거나 시간 초과에 도달하면 제거됩니다.

사전 숨김 동작은 코드 조각의 맨 끝에서 두 가지 구성으로 제어됩니다.

* `body { opacity: 0 !important }` Target이 로드될 때까지 사전 숨김에 사용할 CSS 정의를 지정합니다. 기본적으로 전체 페이지가 숨겨집니다. 이 정의를 숨기려는 방법과 함께 미리 숨길 선택기로 업데이트할 수 있습니다. 이 값은 단순히 사전 숨김 스타일 태그에 삽입되기 때문에 여러 정의를 포함할 수 있습니다. 탐색 아래의 콘텐츠를 줄바꿈하는 쉽게 식별할 수 있는 컨테이너 요소가 있는 경우 이 설정을 사용하여 해당 컨테이너 요소로 사전 숨김을 제한할 수 있습니다.
* `3000` 사전 숨김에 대한 시간 제한(밀리초)을 지정합니다. 시간 초과 전에 Target에서 응답을 받지 못하면 사전 숨김 스타일 태그가 제거됩니다. 이 시간 제한에 도달하는 경우는 드뭅니다.

>[!NOTE]
>
>Platform Web SDK용 사전 숨김 코드 조각은 Target at.js 라이브러리와 함께 사용되는 코드 조각과 약간 다릅니다. Platform Web SDK는 의 다른 스타일 ID를 사용하므로 반드시 올바른 코드 조각을 사용하십시오. `alloy-prehiding`. at.js에 대한 사전 숨김 코드 조각이 사용되는 경우 제대로 작동하지 않을 수 있습니다.

코드 조각 사전 숨김은 태그 내에서도 사용할 수 있습니다.

1. 로 이동 **[!UICONTROL 확장]** 태그의 섹션
1. 선택 **[!UICONTROL 구성]** Adobe Experience Platform Web SDK 확장 기능용
1. 다음 항목 선택 **[!UICONTROL 클립보드에 사전 숨김 코드 조각 복사]** 단추

   ![비동기 구현을 위한 Target 사전 숨김 코드 조각](assets/target-flicker-async.png)

   >[!NOTE]
   >
   >Platform Web SDK 확장에서 복사한 기본 사전 숨김 코드 조각에 다음과 같이 사이트에 없는 CSS 정의가 포함될 수 있습니다. `.personalization-container { opacity: 0 !important }`. 사전에 숨기는 코드 조각을 사이트에 맞게 확인하고 수정해야 합니다.

### 동기식 구현

Adobe은 Luma 사이트에 표시된 대로 태그를 비동기식으로 구현할 것을 권장합니다. 그러나 태그 라이브러리가 동기적으로 로드되는 경우 코드 조각 사전 숨김이 필요하지 않습니다. 대신, 사전 숨김 스타일은 Platform Web SDK 확장 설정에 지정됩니다.

동기 구현을 위한 사전 숨김 스타일은 다음과 같이 구성할 수 있습니다.

1. 로 이동 **[!UICONTROL 확장]** 태그의 섹션
1. 다음 항목 선택 **[!UICONTROL 구성]** Platform 웹 SDK 확장에 대한 단추
1. 다음 항목 선택 **[!UICONTROL 사전 숨김 스타일 편집]** 단추

   ![비동기 구현을 위한 Target 사전 숨김 코드 조각](assets/target-flicker-sync.png)

1. 사용할 선택기 및 숨기기 메서드를 포함하도록 CSS를 수정합니다. 예: `body { opacity: 0 !important }` 페이지의 전체 본문을 미리 숨기려는 경우.
1. 변경 사항을 저장하고 라이브러리에 빌드

>[!NOTE]
>
>사전 숨김 스타일 설정은 동기식 구현에만 사용됩니다. 태그의 비동기 구현을 사용하는 경우 이 스타일은 비워 두거나 주석 처리해야 합니다.

Platform Web SDK에서 플리커를 관리하는 방법에 대한 자세한 내용은 안내서 섹션을 참조하십시오. [개인화된 경험에 대한 플리커 관리](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/manage-flicker.html).


## 데이터 스트림 구성

Platform Web SDK에서 Target 활동을 제공하려면 먼저 데이터 스트림 구성에서 Target을 활성화해야 합니다.

데이터 스트림에서 Target을 구성하려면 다음 작업을 수행하십시오.

1. 로 이동 [데이터 수집](https://experience.adobe.com/#/data-collection){target="blank"} 인터페이스
1. 왼쪽 탐색에서 을 선택합니다. **[!UICONTROL 데이터스트림]**
1. 이전에 만든 항목 선택 `Luma Web SDK` 데이터스트림

   ![Luma 웹 SDK 데이터스트림 선택](assets/datastream-luma-web-sdk.png)

1. 선택 **[!UICONTROL 서비스 추가]**
   ![데이터 스트림에 서비스 추가](assets/target-datastream-addService.png)
1. 선택 **[!UICONTROL Adobe Target]** (으)로 **[!UICONTROL 서비스]**
1. 원하는 경우 아래 지침에 따라 Target 구현에 대한 선택적 세부 정보를 입력합니다.
1. 선택 **[!UICONTROL 저장]**

   ![대상 데이터 스트림 구성](assets/target-datastream.png)

### 속성 토큰

Target Premium 고객은 속성을 사용하여 사용자 권한을 관리할 수 있습니다. Target 속성을 사용하면 사용자가 Target 활동을 실행할 수 있는 경계를 설정할 수 있습니다. 다음을 참조하십시오. [Enterprise 권한](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) 자세한 내용은 Target 설명서의 섹션을 참조하십시오.

속성 토큰을 설정하거나 찾으려면 다음으로 이동합니다. **Adobe Target** > **[!UICONTROL 관리]** > **[!UICONTROL 속성]**. 다음 `</>` 아이콘은 구현 코드를 표시합니다. 다음 `at_property` 값은 데이터 스트림에서 사용할 속성 토큰입니다.

![대상 속성 토큰](assets/target-admin-properties.png)

<a id="advanced-pto"></a>

데이터스트림당 하나의 속성 토큰만 지정할 수 있지만, 속성 토큰 재정의를 사용하면 데이터스트림에 정의된 기본 속성 토큰을 대체할 대체 속성 토큰을 지정할 수 있습니다. 에 대한 업데이트 `sendEvent` 데이터스트림을 재정의하려면 작업도 필요합니다.

![ID 목록](assets/advanced-property-token.png)

### 대상 환경 ID

[환경](https://experienceleague.adobe.com/docs/target/using/administer/environments.html) target에서는 모든 개발 단계를 통해 구현을 관리할 수 있습니다. 이 선택적 설정은 각 데이터 스트림에 사용할 Target 환경을 지정합니다.

Adobe은 개발, 스테이징 및 프로덕션 데이터스트림마다 타겟 환경 ID를 다르게 설정하여 작업을 단순화할 것을 권장합니다. 또는 를 사용하여 Target 인터페이스에서 환경을 구성할 수 있습니다. [호스트](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) 기능.

환경 ID를 설정하거나 찾으려면 다음으로 이동합니다. **Adobe Target** > **[!UICONTROL 관리]** > **[!UICONTROL 환경]**.

![Target 환경](assets/target-admin-environments.png)

>[!NOTE]
>
>Target 환경 ID를 지정하지 않으면 프로덕션 Target 환경으로 간주됩니다.

### Target 타사 ID 네임스페이스

이 선택적 설정을 사용하면 Target 타사 ID에 사용할 ID 기호를 지정할 수 있습니다. Target은 단일 ID 기호 또는 네임스페이스에서만 프로필 동기화를 지원합니다. 자세한 내용은 [mbox3rdPartyID에 대한 실시간 프로필 동기화](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) 섹션 을 참조하십시오.

ID 기호는 아래의 ID 목록에 있습니다. **데이터 수집** > **[!UICONTROL 고객]** > **[!UICONTROL ID]**.

![ID 목록](assets/target-identities.png)

Luma 사이트를 사용하는 이 튜토리얼의 목적상 ID 기호 를 사용하십시오 `lumaCrmId` 에 대한 단원 기간 동안 설정 [ID](configure-identities.md).




## 시각적 개인화 결정 렌더링

먼저 Target 및 태그 인터페이스에 사용되는 용어를 이해해야 합니다.

* **활동**: 하나 이상의 대상을 타겟으로 하는 경험 세트입니다. 예를 들어, 간단한 A/B 테스트는 두 개의 경험이 있는 활동일 수 있습니다.
* **경험**: 하나 이상의 위치 또는 결정 범위에 타겟팅된 작업 세트입니다.
* **결정 범위**: Target 경험이 제공되는 위치입니다. 이전 버전의 Target 사용에 익숙한 경우 결정 범위는 &quot;mbox&quot;와 동일합니다.
* **개인화 결정**: 서버에서 결정하는 작업을 적용해야 합니다. 이러한 결정은 대상 기준 및 Target 활동 우선 순위를 기반으로 할 수 있습니다.
* **제안**: Platform Web SDK 응답에서 전달되는 서버의 의사 결정 결과입니다. 예를 들어 배너 이미지를 교체하는 것이 좋습니다.

### 페이지 로드 규칙 업데이트

Target이 데이터 스트림에서 활성화되어 있을 경우 Target의 시각적 개인화 결정은 Platform Web SDK에 의해 전달됩니다. 그러나 _자동으로 렌더링되지 않습니다._. 자동 렌더링을 활성화하려면 전역 페이지 로드 규칙을 수정해야 합니다.

1. 다음에서 [데이터 수집](https://experience.adobe.com/#/data-collection){target="blank"} 인터페이스에서 이 자습서에 사용할 태그 속성을 엽니다.
1. 를 엽니다. `all pages - library load - AA & AT` 규칙
1. 다음 항목 선택 `Adobe Experience Platform Web SDK - Send event` 작업
1. 사용 **[!UICONTROL 시각적 개인화 결정 렌더링]** 확인란 포함

   ![시각적 개인화 결정 렌더링 사용](assets/target-rule-enable-visual-decisions.png)

1. **[!UICONTROL 데이터 스트림 구성 재정의**] 다음 **[!UICONTROL 대상 속성 토큰]** 정적 값으로 또는 데이터 요소로 재정의할 수 있습니다. 에 정의된 속성 토큰만 [**고급 속성 토큰 무시**](#advanced-pto) 의 섹션 **데이터 스트림 구성** 가 결과를 반환합니다.

   ![속성 토큰 재정의](assets/target-property-token-ovrrides.png)

1. 변경 사항을 저장한 다음 라이브러리에 빌드

시각적 개인화 결정 렌더링 설정을 사용하면 Platform Web SDK에서 Target 시각적 경험 작성기 또는 &quot;글로벌 mbox&quot;를 사용하여 지정된 수정 사항을 자동으로 적용합니다.

>[!NOTE]
>
>일반적으로 [!UICONTROL 시각적 개인화 결정 렌더링] 전체 페이지 로드당 하나의 이벤트 보내기 작업에 대해서만 설정을 활성화해야 합니다. 여러 이벤트 보내기 작업에서 이 설정이 활성화되어 있으면 후속 렌더링 요청이 무시됩니다.

사용자 지정 코드를 사용하여 이러한 결정에 대해 직접 렌더링하거나 작업을 수행하려는 경우 [!UICONTROL 시각적 개인화 결정 렌더링] 설정이 비활성화되었습니다. Platform Web SDK는 유연하며 완벽한 제어 기능을 제공하는 이 기능을 제공합니다. 자세한 내용은 안내서를 참조하십시오 [개인화된 콘텐츠 수동 렌더링](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html).


### 시각적 경험 작성기로 Target 활동 설정

이제 기본 구현 부분이 완료되었으므로 Target에서 XT(경험 타깃팅) 활동을 만들어 모든 것이 올바르게 작동하는지 확인하십시오. 다음에 대한 Target 자습서를 참조할 수 있습니다. [경험 타깃팅 활동 만들기](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html) 도움이 필요하면

>[!NOTE]
>
>Google Chrome을 브라우저로 사용하는 경우 [VEC(시각적 경험 작성기) Helper 확장 프로그램](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html?lang=en) 를 사용하면 VEC에서 편집할 사이트를 제대로 로드할 수 있습니다.

1. Target으로 이동
1. 활동 URL에 대한 Luma 홈 페이지를 사용하여 경험 타깃팅 (XT) 활동을 만듭니다

   ![새 XT 활동 만들기](assets/target-xt-create-activity.png)

1. 페이지를 수정합니다. 예를 들어 홈페이지 영웅 배너의 텍스트를 변경합니다.  완료되면 다음을 선택합니다. **[!UICONTROL 저장]** 그러면 **[!UICONTROL 다음]**.

   ![대상 VEC 수정](assets/target-xt-vec-modification.png)

1. 이벤트 이름을 업데이트한 다음 를 선택합니다. **[!UICONTROL 다음]**.

   ![Target VEC 업데이트 이벤트](assets/target-xt-vec-updateevent.png)

1. 적절한 보고서 세트를 가진 보고 소스로 Adobe Analytics 를 선택하고 목표로 주문 지표를 선택합니다

   ![Target VEC 보고 소스](assets/target-xt-vec-reportingsource.png)

   >[!NOTE]
   >
   >Adobe Analytics을 사용하지 않는 경우 보고 소스로 Target 을 선택하고 과 같은 다른 지표를 선택합니다 **참여 > 페이지 보기 수** 대신, 활동을 저장하고 미리 보려면 목표 지표가 필요합니다.

1. 활동 저장
1. 변경 사항이 익숙하다면 활동을 활성화할 수 있습니다. 그렇지 않고 를 활성화하지 않고 경험을 미리 보려면 다음을 복사할 수 있습니다. [QA 미리보기 URL](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html).
1. Luma 홈 페이지를 로드하면 변경 사항이 적용된 것을 볼 수 있습니다
1. 몇 시간 후에 Adobe Analytics에서 Target 활동 데이터 및 전환을 볼 수 있습니다. 자세한 내용은 Target 안내서 를 참조하십시오. [A4T(Analytics for Target) 보고](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/reporting.html?lang=en).



### 디버거를 사용하여 유효성 검사

활동을 설정하면 콘텐츠가 페이지에 렌더링됩니다. 그러나 활성 상태인 활동이 없어도 이벤트 보내기 네트워크 호출을 보고 Target이 제대로 구성되었는지 확인할 수 있습니다.

>[!CAUTION]
>
>Google Chrome을 사용 중이며 [VEC(시각적 경험 작성기) Helper 확장 프로그램](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html?lang=en) 설치되어 있는지 확인합니다. **Target 라이브러리 삽입** 설정이 비활성화되었습니다. 이 설정을 활성화하면 추가 Target 요청이 발생합니다.

1. Adobe Experience Platform Debugger 브라우저 확장 열기
1. 로 이동 [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html) 디버거를 사용하여 [사이트의 태그 속성을 자신의 개발 속성으로 전환합니다.](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. 페이지 다시 로드
1. 다음 항목 선택 **[!UICONTROL 네트워크]** 디버거의 도구
1. 필터링 기준 **[!UICONTROL Adobe Experience Platform 웹 SDK]**
1. 첫 번째 호출에 대한 이벤트 행의 값을 선택합니다.

   ![Adobe Experience Platform 디버거의 네트워크 호출](assets/target-debugger-network.png)

1. 아래에 키가 있습니다. `query` > `personalization` 및  `decisionScopes` 의 값이 `__view__`. 이 범위는 Target의 &quot;글로벌 mbox&quot;에 해당합니다. 이 Platform Web SDK 호출은 Target에 의사 결정을 요청했습니다.

   ![`__view__` decisionScope 요청](assets/target-debugger-view-scope.png)

1. 오버레이를 닫고 두 번째 네트워크 호출에 대한 이벤트 세부 정보를 선택합니다. 이 호출은 Target이 활동을 반환한 경우에만 표시됩니다.
1. Target에서 반환된 활동 및 경험에 대한 세부 사항이 있습니다. 이 Platform Web SDK 호출은 Target 활동이 사용자에게 렌더링되었다는 알림을 보내고 노출을 증가시킵니다.

   ![타겟 활동 노출](assets/target-debugger-activity-impression.png)

## 사용자 지정 결정 범위 설정 및 렌더링

사용자 지정 결정 범위(이전의 &quot;mbox&quot;)는 Target 양식 기반 경험 작성기를 사용하여 구조화된 방식으로 HTML 또는 JSON 콘텐츠를 전달하는 데 사용할 수 있습니다. 이러한 사용자 지정 범위 중 하나에 전달된 콘텐츠는 Platform Web SDK에 의해 자동으로 렌더링되지 않습니다.

### 페이지 로드 규칙에 범위 추가

페이지 로드 규칙을 수정하여 사용자 지정 결정 범위를 추가합니다.

1. 를 엽니다. `all pages - library load - AA & AT` 규칙
1. 다음 항목 선택 `Adobe Experience Platform Web SDK - Send Event` 작업
1. 사용할 범위를 하나 이상 추가합니다. 이 예에서는 를 사용합니다. `homepage-hero`.

   ![사용자 정의 범위](assets/target-rule-custom-scope.png)

1. 변경 사항을 저장하고 라이브러리에 빌드

>[!TIP]
>
>이 자습서에서는 데모용으로 수동으로 정의된 단일 범위를 사용합니다. 특정 페이지에 사용할 수 있는 여러 결정 범위를 사용하려는 경우 페이지 경로에 따라 조건 적으로 범위 배열을 반환하는 데이터 요소를 사용하는 것이 좋습니다. 이 접근 방식은 구현을 단순하고 확장 가능하게 유지하는 데 도움이 됩니다.

### Target의 응답을 처리합니다.

에 대한 콘텐츠를 요청하도록 Platform Web SDK를 구성했으므로 `homepage-hero` 범위, 응답을 사용하여 작업을 수행해야 합니다. Platform Web SDK 태그 확장은 [!UICONTROL 이벤트 전송 완료] 의 응답이 있을 때 새 규칙을 즉시 트리거하는 데 사용할 수 있는 이벤트 [!UICONTROL 이벤트 보내기] 작업이 수신되었습니다.

1. 라는 규칙 만들기 `homepage - send event complete - render homepage-hero`.
1. 규칙에 이벤트를 추가합니다. 사용 **Adobe Experience Platform 웹 SDK** 확장 및 **[!UICONTROL 이벤트 전송 완료]** 이벤트 유형.
1. Luma 홈 페이지(쿼리 문자열이 없는 경로 가 다음과 같음)에 규칙을 제한하는 조건을 추가합니다. `/content/luma/us/en.html`).
1. 규칙에 작업을 추가합니다. 사용 **Adobe Experience Platform 웹 SDK** 확장 및 **제안 적용** 작업 유형.

   ![홈페이지 주인공 규칙 렌더링](assets/target-rule-render-hero.png)

   >[!TIP]
   >
   >기본 이름을 사용하는 대신 규칙 이벤트, 조건 및 작업에 설명 이름을 지정합니다. 강력한 규칙 구성 요소 이름을 사용하면 검색 결과를 더욱 유용하게 사용할 수 있습니다.

1. 입력 `%event.propositions%` 을 제안 필드에 추가합니다. 여기에서는 &quot;이벤트 완료 보내기&quot; 이벤트를 이 규칙의 트리거로 사용합니다.
1. &quot;제안 메타데이터&quot; 섹션에서 다음을 선택합니다. **[!UICONTROL 양식 사용]**
1. 의 경우 **[!UICONTROL 범위]** 필드 입력 `homepage-hero`
1. 의 경우 **[!UICONTROL 선택기]** 필드 입력 `div.heroimage`
1. 대상 **[!UICONTROL 작업 유형]** 선택 **[!UICONTROL HTML 설정]**

   ![홈페이지 주인공 작업 렌더링](assets/target-action-render-hero.png)

1. 변경 사항을 저장하고 라이브러리에 빌드
1. Luma 홈 페이지를 몇 번 로드하십시오. 충분히 새 페이지를 만들 수 있습니다. `homepage-hero` target 인터페이스의 의사 결정 범위 등록입니다.

### 양식 기반 경험 작성기로 Target 활동 설정

이제 사용자 지정 결정 범위를 수동으로 렌더링하는 규칙이 있으므로 Target에서 다른 XT(경험 타깃팅) 활동을 만들 수 있습니다. 이번에는 양식 기반 경험 작성기를 사용합니다.

1. 열기 [Adobe Target](https://experience.adobe.com/target)
1. 이전 단원에 사용된 활동 비활성화
1. 양식 기반 경험 작성기 선택 사항을 사용하여 경험 타깃팅 (XT) 활동 만들기

   ![새 XT 활동 만들기](assets/target-xt-create-form-activity.png)

1. 다음 항목 선택 **`homepage-hero`** 위치 드롭다운 및 **[!UICONTROL HTML 오퍼 만들기]** 콘텐츠 드롭다운에서 위치를 사용할 수 없는 경우 입력할 수 있습니다. Target은 해당 위치 또는 범위에 대한 요청을 받은 후 정기적으로 새 위치 이름을 채웁니다.

   ![새 XT 활동 만들기](assets/target-xt-form-activity.png)

1. 다음 코드를 콘텐츠 상자에 붙여 넣습니다. 이 코드는 다른 배경 이미지가 있는 기본 영웅 배너입니다.

   ```html
   <div class="we-HeroImage jumbotron" style="background-image: url('/content/luma/us/en/women/_jcr_content/root/hero_image.coreimg.jpeg');">
      <div class="container cq-dd-image">
         <div class="we-HeroImage-wrapper">
            <p class="h3">New Luma Yoga Collection</p>
            <strong class="we-HeroImage-title h1">Be active with style&nbsp;</strong>
            <p>
               <a class="btn btn-primary btn-action" href="/content/luma/us/en/products.html" role="button">Shop Now</a>
            </p>
         </div>
      </div>
   </div>
   ```

1. 다음에서 [!UICONTROL 목표 및 설정] 단계, 보고 소스로 Adobe Target 선택 및 [!UICONTROL 참여] > [!UICONTROL 페이지 보기 수] 을(를) 목표로 함
1. 활동 저장
1. 변경 사항이 익숙하다면 활동을 활성화할 수 있습니다. 그렇지 않고 를 활성화하지 않고 경험을 미리 보려면 다음을 복사할 수 있습니다. [QA 미리보기 URL](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html).
1. Luma 홈 페이지를 로드하면 변경 사항이 적용된 것을 볼 수 있습니다

>[!NOTE]
>
>&quot;mbox를 클릭함&quot; 전환 목표가 자동으로 작동하지 않습니다. Platform Web SDK는 사용자 지정 범위를 자동으로 렌더링하지 않으므로 콘텐츠를 적용하기 위해 선택한 위치에 대한 클릭 수를 추적하지 않습니다. &quot;click&quot;을 사용하여 각 범위에 대한 고유한 클릭 추적을 만들 수 있습니다 `eventType` 를 사용 가능으로 `_experience` 를 사용한 세부 사항 `sendEvent` 작업.

### 디버거를 사용하여 유효성 검사

활동을 활성화한 경우 페이지에 콘텐츠가 렌더링되는 것을 볼 수 있습니다. 그러나 라이브가 아닌 경우에도 [!UICONTROL 이벤트 보내기] target이 사용자 지정 범위에 대한 콘텐츠를 요청하고 있는지 확인하기 위한 네트워크 호출입니다.

1. Adobe Experience Platform Debugger 브라우저 확장 프로그램 열기
1. 로 이동 [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html) 디버거를 사용하여 [사이트의 태그 속성을 자신의 개발 속성으로 전환합니다.](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. 페이지 다시 로드
1. 다음 항목 선택 **[!UICONTROL 네트워크]** 디버거의 도구
1. 필터링 기준 **[!UICONTROL Adobe Experience Platform 웹 SDK]**
1. 첫 번째 호출에 대한 이벤트 행의 값을 선택합니다.

   ![Adobe Experience Platform 디버거의 네트워크 호출](assets/target-debugger-network.png)

1. 아래에 키가 있습니다. `query` > `personalization` 및  `decisionScopes` 의 값이 `__view__` 이전과 비슷하지만 지금은 `homepage-hero` 범위가 포함되었습니다. 이 Platform Web SDK 호출은 VEC 및 특정 `homepage-hero` 위치.

   ![`__view__` decisionScope 요청](assets/target-debugger-view-scope.png)

1. 오버레이를 닫고 두 번째 네트워크 호출에 대한 이벤트 세부 정보를 선택합니다. 이 호출은 Target이 활동을 반환한 경우에만 표시됩니다.
1. Target에서 반환된 활동 및 경험에 대한 세부 사항이 있습니다. 이 Platform Web SDK 호출은 Target 활동이 사용자에게 렌더링되었다는 알림을 보내고 노출을 증가시킵니다.

   ![타겟 활동 노출](assets/target-debugger-activity-impression.png)

## Target에 추가 데이터 전달

이 섹션에서는 Target별 데이터를 전달하고 XDM 데이터가 Target 매개 변수에 매핑되는 방식을 자세히 살펴봅니다.

XDM 오브젝트에서 매핑되지 않은 Target에 유용할 수 있는 일부 데이터 포인트가 있습니다. 이러한 특수 Target 매개 변수는 다음과 같습니다.

* [프로필 속성](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/methods/in-page-profile-attributes.html?lang=en)
* [Recommendations 엔티티 속성](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=en)
* [Recommendations 예약 매개 변수](https://experienceleague.adobe.com/docs/target/using/recommendations/plan-implement.html?lang=en#pass-behavioral)
* 다음에 대한 범주 값: [카테고리 친화성](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/category-affinity.html?lang=en)

### Target 매개 변수에 대한 데이터 요소 만들기

먼저 프로필 속성, 엔티티 속성, 카테고리 값에 대한 몇 가지 추가 데이터 요소를 설정한 다음 `data` 비 XDM 데이터를 전달하는 데 사용되는 개체:

* **`target.entity.id`** 매핑됨 `digitalData.product.0.productInfo.sku`
* **`target.entity.name`** 매핑됨 `digitalData.product.0.productInfo.title`
* **`target.user.categoryId`** 다음 사용자 지정 코드를 사용하여 최상위 카테고리에 대한 사이트 URL을 구문 분석합니다.

  ```javascript
  var cat = location.pathname.split(/[/.]+/);
  if (cat[5] == 'products') {
     return (cat[6]);
  } else if (cat[5] != 'html') { 
     return (cat[5]);
  }
  ```

* **`data.content`** 다음 사용자 지정 코드 사용:

  ```javascript
  var data = {
     __adobe: {
        target: {
           "entity.id": _satellite.getVar("target.entity.id"),
           "entity.name": _satellite.getVar("target.entity.name"),
           "profile.loggedIn": _satellite.getVar("user.profile.attributes.loggedIn"),
           "user.categoryId": _satellite.getVar("target.user.categoryId")
        }
     }
  }
  return data;
  ```

### 페이지 로드 규칙 업데이트

XDM 개체 외부의 Target에 대한 추가 데이터를 전달하려면 적용 가능한 규칙을 업데이트해야 합니다. 이 예제에서는 새로운 내용을 포함하기만 하면 됩니다 **data.content** 일반 페이지 로드 규칙 및 제품 페이지 보기 규칙에 대한 데이터 요소입니다.

1. 를 엽니다. `all pages - library load - AA & AT` 규칙
1. 다음 항목 선택 `Adobe Experience Platform Web SDK - Send event` 작업
1. 추가 `data.content` 데이터 필드에 대한 데이터 요소

   ![규칙에 대상 데이터 추가](assets/target-rule-data.png)

1. 변경 사항을 저장하고 라이브러리에 빌드
1. 에 대해 1~4단계를 반복합니다. **제품 보기 - 라이브러리 로드 - AA** 규칙

>[!NOTE]
>
>위의 예에서는 `data` 일부 페이지 유형에서 완전히 채워지지 않은 개체입니다. 태그는 이 상황을 적절하게 처리하며 정의되지 않은 값이 있는 키는 생략합니다. 예를 들어, `entity.id` 및 `entity.name` 는 제품 세부 사항을 제외한 어떤 페이지에서도 전달되지 않습니다.


## 개인화 결정 및 Analytics 수집 이벤트 분할

Luma 사이트의 데이터 레이어는 태그 포함 코드 앞에 완전히 정의됩니다. 이를 통해 단일 호출을 사용하여 개인화된 콘텐츠(예: Adobe Target에서)를 가져오고 분석 데이터(예: Adobe Analytics으로)를 전송할 수 있습니다. 많은 웹 사이트에서 데이터 레이어는 개인화 애플리케이션과 함께 사용하기에 적절할 만큼 충분히 일찍 또는 빠르게 로드될 수 없습니다. 이러한 상황에서는 두 가지를 만들 수 있습니다 `sendEvent` 는 단일 페이지 로드를 호출하고 첫 번째 는 개인화에 사용하고 두 번째 는 analytics에 사용합니다. 이러한 방식으로 이벤트 규칙을 분류하면 Target Decisioning 이벤트를 가능한 한 빨리 실행할 수 있습니다. Analytics 이벤트는 데이터 레이어 개체가 채워질 때까지 대기할 수 있습니다. 이는 Adobe Target에서 를 실행하는 웹 전 SDK 구현과 유사합니다. `target-global-mbox` 페이지 맨 위에서 Adobe Analytics이 `s.t()` 페이지 하단에서 호출


1. 라는 규칙 만들기 `all pages - page top - request decisions`
1. 규칙에 이벤트를 추가합니다. 사용 **코어** 확장 및 **[!UICONTROL 라이브러리가 로드됨 (페이지 상단)]** 이벤트 유형
1. 규칙에 작업을 추가합니다. 사용 **Adobe Experience Platform 웹 SDK** 확장 및 **이벤트 보내기** 작업 유형
1. 선택 **[!UICONTROL 안내식 이벤트 사용]** 다음을 선택합니다. **[!UICONTROL 개인화 요청]**
1. 이렇게 하면 **유형** 다음으로: **[!UICONTROL 의사 결정 제안 가져오기]**

   ![send_decision_request_alone](assets/target-decision-request.png)

1. 을(를) 생성할 때 `Adobe Analytics Send Event rule` 사용 **안내식 이벤트 스타일** 섹션 선택 **[!UICONTROL 페이지 하단 이벤트 - 분석 수집]** 라디오 단추
1. 이렇게 하면 **[!UICONTROL 보류 중인 표시 알림 포함]** decisioning 요청에서 대기 중인 디스플레이 알림이 전송되도록 확인란을 선택했습니다.

![send_decision_request_alone](assets/target-aa-request-guided.png)

>[!TIP]
>
>에 대한 Decisioning 제안을 가져오는 이벤트에 다음에 Adobe Analytics 이벤트가 없는 경우 **안내식 이벤트 스타일** **[!UICONTROL 안내되지 않음 - 모든 필드 표시]**. 모든 옵션을 수동으로 선택해야 하지만 로 이동하면 옵션의 잠금이 해제됩니다. **[!UICONTROL 디스플레이 알림 자동 보내기]** 가져오기 요청과 함께 사용됩니다.


### 디버거를 사용하여 유효성 검사

이제 규칙이 업데이트되었으므로 Adobe Debugger을 사용하여 데이터가 올바르게 전달되는지 확인할 수 있습니다.

1. 다음 위치로 이동 [Luma 데모 사이트](https://luma.enablementadobe.com/content/luma/us/en.html) 전자 메일로 로그인 `test@adobe.com` 및 암호 `test`
1. 제품 세부 사항 페이지로 이동
1. Adobe Experience Platform 디버거 브라우저 확장 을 열고 [태그 속성을 자신의 개발 속성으로 전환합니다.](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. 페이지 다시 로드
1. 다음 항목 선택 **네트워크** 디버거의 도구 및 필터링 기준 **Adobe Experience Platform 웹 SDK**
1. 첫 번째 호출에 대한 이벤트 행의 값을 선택합니다.
1. 아래에 키가 있습니다. `data` > `__adobe` > `target` 제품, 카테고리 및 로그인 상태에 대한 정보로 채워집니다.

   ![`__view__` decisionScope 요청](assets/target-debugger-data.png)

### Target 인터페이스에서 유효성 검사

그런 다음 Target 인터페이스를 살펴보고 데이터가 수신되었고 대상 및 활동에서 사용할 수 있는지 확인합니다. XDM 데이터는 사용자 지정 Target 매개 변수에 자동으로 매핑됩니다. XDM 데이터가 Target에 의해 수신되었고 대상자를 만들어 사용할 수 있는지 확인할 수 있습니다.

1. 열기 [Adobe Target](https://experience.adobe.com/target)
1. 다음 위치로 이동 **[!UICONTROL 대상]** 섹션
1. 대상자를 만들고 **[!UICONTROL 사용자 정의]** 속성 유형
1. 검색 **[!UICONTROL 매개 변수]** 필드 `web`. 드롭다운 메뉴가 웹 페이지 세부 사항과 관련된 모든 XDM 필드로 채워집니다.

   ![Target 사용자 지정 속성에서 유효성 검사](assets/validate-in-target-customattribute.png)

다음으로 로그인 상태 프로필 속성이 전달되었는지 확인합니다.

1. 다음을 선택합니다. **[!UICONTROL 방문자 프로필]** 속성 유형
2. `loggedIn`을 검색합니다. 드롭다운 메뉴에서 속성을 사용할 수 있는 경우 속성이 Target에 올바르게 전달되었습니다. 새 속성을 Target UI에서 사용할 수 있게 되는 데 몇 분이 걸릴 수 있습니다.

   ![Target 프로필에서 유효성 검사](assets/validate-in-target-profile.png)

Target Premium이 있는 경우 엔티티 데이터가 올바르게 전달되었고 제품 데이터가 Recommendations 제품 카탈로그에 기록되었는지 확인할 수도 있습니다.

1. 다음 위치로 이동 **[!UICONTROL Recommendations]** 섹션
1. 선택 **[!UICONTROL 카탈로그 검색]** 왼쪽 탐색
1. Luma 사이트에서 이전에 방문한 제품 SKU 또는 제품 이름을 검색합니다. 제품이 제품 카탈로그에 표시되어야 합니다. 새 제품이 Recommendations 제품 카탈로그에서 검색되는 데 몇 분이 걸릴 수 있습니다.

   ![Target 카탈로그 검색에서 유효성 검사](assets/validate-in-target-catalogsearch.png)

### Assurance를 통해 유효성 검사

또한 Assurance를 사용하여 적절한 위치에서 Target 의사 결정 요청이 올바른 데이터를 가져오고 서버측 변환이 올바르게 발생하는지 확인할 수 있습니다. Target 의사 결정 및 Adobe Analytics 호출이 별도로 전송된 경우에도 캠페인 및 경험 정보가 Adobe Analytics 호출에 포함되어 있는지 확인할 수 있습니다.

1. 열기 [보증](https://experience.adobe.com/assurance)
1. 새 보증 세션을 시작하고 **[!UICONTROL 세션 이름]** 및 입력 **[!UICONTROL 기본 url]** 테스트 중인 사이트 또는 다른 페이지의 경우
1. 클릭 **[!UICONTROL 다음]**

   ![보증 새 세션에서 유효성 검사](assets/validate-in-assurance-newsession.png)

1. 연결 방법을 선택하세요. 이 경우 다음을 사용합니다. **[!UICONTROL 링크 복사]**
1. 링크를 복사하여 새 브라우저 탭에 붙여넣기
1. 클릭 **[!UICONTROL 완료]**

   ![확인 보증 링크를 통해 연결](assets/validate-in-assurance-copylink.png)

1. 보증 세션이 시작되면 이벤트 탭에 이벤트가 채워지는 것을 볼 수 있습니다
1. &quot;tnta&quot;로 필터링
1. 가장 최근 호출을 선택하고 메시지를 확장하여 올바르게 채워졌는지 확인하고 &quot;tnta&quot; 값을 메모하십시오.

   ![보증 대상 히트에서 유효성 검사](assets/validate-in-assurance-targetevent.png)

1. 그런 다음 &quot;tnta&quot; 필터를 유지하고 방금 본 타겟 이벤트 후에 발생하는 analytics.mapping 이벤트를 선택합니다.
1. &quot;context.mappedQueryParams&quot;를 검사합니다.\&lt;yourschemaname>&quot; 값을 확인하려면 이전 target 이벤트에 있는 &quot;tnta&quot; 값과 일치하는 연결된 문자열이 있는 &quot;tnta&quot; 특성이 포함되어 있습니다.

   ![보증 Analytics 히트에서 유효성 검사](assets/validate-in-assurance-analyticsevent.png)

이렇게 하면 Target 의사 결정 호출을 만들 때 이후 전송을 위해 큐에 있던 A4T 정보가 나중에 페이지에서 Analytics 추적 호출이 실행될 때 제대로 전송되었음을 알 수 있습니다.

이 단원을 완료했으므로 Platform Web SDK를 사용하여 Adobe Target을 구현해야 합니다.

[다음: ](setup-consent.md)

>[!NOTE]
>
>Adobe Experience Platform Web SDK에 대해 학습하는 데 시간을 투자해 주셔서 감사합니다. 질문이 있거나, 일반적인 피드백을 공유하거나, 향후 콘텐츠에 대한 제안이 있는 경우 이에 대해 공유하십시오. [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
