---
title: CMP(동의 관리 플랫폼)로 동의 구현
description: 데이터 수집에서 Adobe Experience Platform Web SDK 확장을 사용하여 CMP(동의 관리 플랫폼)에서 얻은 동의 데이터를 구현하고 활성화하는 방법을 알아봅니다.
feature: Web SDK, Tags
level: Intermediate
doc-type: tutorial
exl-id: bee792c3-17b7-41fb-a422-289ca018097d
source-git-commit: e2594d3b30897001ce6cb2f6908d75d0154015eb
workflow-type: tm+mt
source-wordcount: '3178'
ht-degree: 0%

---

# Platform Web SDK 확장을 사용하여 CMP(동의 관리 플랫폼)로 동의 구현

많은 법적 개인 정보 보호 규정에서는 데이터 수집, 개인화 및 기타 마케팅 사용 사례와 관련하여 적극적이고 구체적인 동의에 대한 요구 사항을 도입했습니다. 이러한 요구 사항을 충족하기 위해 Adobe Experience Platform에서는 개별 고객 프로필에서 동의 정보를 캡처하고 이러한 환경 설정을 다운스트림 플랫폼 워크플로우에서 각 고객의 데이터가 사용되는 방식을 결정하는 요소로 사용할 수 있습니다.

>[!NOTE]
>
>Adobe Experience Platform Launch은 데이터 수집 기술군으로 Adobe Experience Platform에 통합되고 있습니다. 이 콘텐츠를 사용하는 동안 알아야 하는 몇 가지 용어 변경 사항이 인터페이스에 롤아웃되었습니다.
>
> * Platform launch(Client Side)가 이제 **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)**&#x200B;입니다.
> * 이제 platform launch 서버측이 **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**&#x200B;입니다.
> * 이제 Edge 구성이 **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)**&#x200B;입니다.

이 튜토리얼에서는 데이터 수집에서 Platform Web SDK 확장을 사용하여 CMP(동의 관리 플랫폼)에서 얻은 동의 데이터를 구현하고 활성화하는 방법을 보여 줍니다. OneTrust 또는 Sourcepoint를 CMP로 사용하여 Adobe 표준과 IAB TCF 2.0 동의 표준을 모두 사용하여 이를 수행합니다.

이 자습서에서는 Platform Web SDK 확장을 사용하여 동의 데이터를 Platform으로 보냅니다. 웹 SDK에 대한 개요는 [이 페이지](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)를 참조하십시오.

## 전제 조건

웹 SDK를 사용하기 위한 필수 구성 요소가 [여기](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/prerequisite.html#fundamentals)에 나열되어 있습니다.

해당 페이지에는 &quot;이벤트 데이터 세트&quot;에 대한 요구 사항이 있으며, 소리처럼 이는 경험 이벤트 데이터를 보관할 수 있는 데이터 세트입니다. 이벤트와 함께 동의 정보를 보내려면 [IAB TCF 2.0 동의 세부 정보](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/iab/dataset.html) 필드 그룹을 경험 이벤트 스키마에 추가해야 합니다.

![](./images/event-schema.png)

Platform 동의 표준 v2.0의 경우 XDM 개별 프로필 스키마 및 데이터 세트를 만들려면 Adobe Experience Platform에 액세스해야 합니다. 스키마 만들기에 대한 자습서는 [스키마 편집기를 사용하여 스키마 만들기](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html#tutorials)를 참조하고, 필수 동의 및 환경 설정 세부 정보 필드 그룹은 [동의 및 환경 설정 데이터를 캡처하도록 데이터 집합 구성](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/adobe/dataset.html)을 참조하십시오.

이 자습서에서는 데이터 수집에 액세스할 수 있고 Web SDK 확장이 설치된 클라이언트측 태그 속성과 개발용으로 생성 및 구축된 작업 라이브러리를 만들었다고 가정합니다. 이 주제들은 다음 문서에 자세히 설명되어 있습니다.

* [속성 만들기 또는 구성](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html?lang=en#create-or-configure-a-property)
* [라이브러리 개요](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/libraries.html)
* [게시 개요](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html)

또한 [Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) Chrome 확장을 사용하여 구현을 검사하고 확인합니다.

사용자 사이트의 CMP로 IAB TCF 예제를 구현하려면 OneTrust 또는 Sourcepoint와 같은 CMP에 액세스하여 해당 데이터가 제공하는 데이터를 생성해야 합니다. 또는 여기 를 따라가서 아래 결과를 확인할 수 있습니다.

## Adobe 동의 표준(v1.0 또는 v2.0)에서 Web SDK 사용

>[!NOTE]
>
>1.0 표준은 v2.0을 위해 단계적으로 폐지되고 있습니다. 2.0 표준을 사용하면 동의 환경 설정을 수동으로 적용하는 데 사용할 수 있는 추가 동의 데이터를 추가할 수 있습니다. Platform Web SDK 확장의 아래 스크린샷은 Adobe 동의 표준의 v1.0 또는 v2.0과 호환되는 확장 버전 [2.4.0](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html#version-2.4.0)에서 찍은 것입니다.

이러한 표준에 대한 자세한 내용은 [고객 동의 환경 설정 지원](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html)을 참조하십시오.

### 1단계: 웹 SDK 확장에서 동의 구성

Tags 속성에 Platform Web SDK 확장을 설치한 후 확장 구성 화면에서 동의 데이터 주소 지정 옵션을 구성할 수 있습니다.

![](./images/pending.png)

&quot;개인 정보&quot; 섹션은 사용자가 이전에 동의 환경 설정을 제공하지 않은 경우 SDK에 대한 동의 수준을 설정합니다. SDK에서의 동의 및 이벤트 데이터 수집에 대한 기본 상태를 설정합니다. 선택한 설정은 &quot;사용자가 명시적 동의 환경 설정을 아직 제공하지 않은 경우 SDK는 어떻게 해야 합니까?&quot;라는 질문에 대한 답을 제공합니다.

* 에서 - 사용자가 동의 환경 설정을 제공하기 전에 발생하는 이벤트를 수집합니다.
* 아웃 - 사용자가 동의 환경 설정을 제공하기 전에 발생하는 이벤트를 삭제합니다.
* 보류 중 - 사용자가 동의 환경 설정을 제공하기 전에 발생하는 이벤트를 큐에 추가합니다.
* 데이터 요소에서 제공

기본 동의 설정이 &quot;시작&quot;인 경우 명시적인 동의를 기다리지 않고 사용자가 동의 환경 설정을 제공하기 전에 발생하는 이벤트를 수집해야 한다고 SDK에 알려줍니다. 이러한 환경 설정은 일반적으로 CMP에서 처리 및 저장됩니다.

기본 동의 설정이 &quot;종료&quot;인 경우 사용자 옵트인 환경 설정이 설정되기 전에 발생하는 이벤트를 수집하지 않아야 함을 SDK에 알려줍니다. 동의 환경 설정을 설정하기 전에 발생하는 방문자 활동은 동의가 설정된 후 SDK에서 보내는 데이터에 포함되지 않습니다. 예를 들어 동의 배너를 선택하기 전에 웹 페이지를 스크롤하여 보는 경우 이 &quot;종료&quot; 설정이 사용되면 나중에 사용자가 데이터 수집에 대한 명시적 동의를 제공하는 경우 해당 스크롤 활동 및 보기 시간이 전송되지 않습니다.

기본 동의 설정이 &quot;보류 중&quot;인 경우 SDK는 사용자가 동의 환경 설정을 제공하기 전에 발생하는 모든 이벤트를 큐에 추가하므로 동의 환경 설정이 설정된 후 방문 중에 SDK가 처음 구성된 후에 이벤트를 전송할 수 있습니다.

이 &quot;보류 중&quot; 설정을 사용하면 사용자 옵트인 환경 설정이 필요한 명령(예: 이벤트 명령)을 실행하려고 하면 SDK 내에서 명령이 큐에 대기됩니다. 이러한 명령은 사용자의 옵트인 환경 설정을 SDK에 전달할 때까지 처리되지 않습니다.

CMP가 사용자의 환경 설정을 수집하면 SDK에 해당 환경 설정을 전달할 수 있습니다. 아래 뒷부분 섹션에서는 해당 옵트인 데이터를 가져와 웹 SDK 확장과 함께 사용하는 방법에 대해 알아봅니다.

&quot;데이터 요소에서 제공&quot;을 사용하면 사용자 지정 코드 또는 사이트 또는 데이터 레이어의 CMP로 캡처된 동의 환경 설정 데이터가 포함된 데이터 요소에 액세스할 수 있습니다. 이 용도로 사용되는 데이터 요소는 &quot;in&quot;, &quot;out&quot; 또는 &quot;pending&quot;으로 확인되어야 합니다.

참고: SDK에 대한 이 구성 설정은 사용자의 프로필에 유지되지 않습니다. 이는 방문자가 명시적 동의 환경 설정을 제공하기 전에 SDK의 동작을 설정하는 것과 관련이 있습니다.

Web SDK 확장 구성에 대한 자세한 내용은 [Platform Web SDK 확장 개요](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/web-sdk-extension-configuration.html?lang=en#configure-the-extension) 및 [고객 동의 환경 설정 지원](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html)을 참조하십시오.

이 예제에서는 &quot;보류 중&quot; 옵션을 선택하고 **저장**&#x200B;을 선택하여 구성 설정을 저장하겠습니다.

### 2단계: 동의 환경 설정 전달

이제 SDK의 기본 동작을 설정했으므로 태그를 사용하여 방문자의 명시적 동의 환경 설정을 Platform에 전송할 수 있습니다. Adobe 1.0 또는 2.0 표준을 사용하여 동의 데이터를 전송하는 작업은 태그 규칙에서 Web SDK의 `setConsent` 작업을 사용하여 쉽게 구현할 수 있습니다.

#### Platform Consent Standard 1.0으로 동의 설정

이를 입증할 수 있는 규칙을 만들어 보겠습니다. Platform 태그 속성에서 규칙을 선택한 다음 파란색 규칙 추가 단추에서 를 선택합니다. 규칙 이름을 &quot;setAdobeConsent&quot;로 지정하고 이벤트를 추가하도록 선택하겠습니다. 이벤트 유형에 대해 웹 사이트에 페이지가 로드될 때마다 이 규칙을 트리거하는 &quot;Window Loaded&quot;를 선택합니다. 그런 다음 &quot;Actions&quot; 아래에서 &quot;Add&quot; 를 선택하여 작업 구성 화면을 엽니다. 여기서 동의 데이터를 설정합니다. &quot;확장&quot; 드롭다운을 선택하고 &quot;Platform Web SDK&quot;를 선택한 다음 &quot;작업 유형&quot;을 선택하고 &quot;동의 설정&quot;을 선택합니다.

&quot;동의 정보&quot;에서 &quot;양식 작성&quot;을 선택합니다. 이 규칙 작업에서는 표시되는 양식을 채워 Web SDK를 사용하여 Adobe 1.0 동의 표준에 대한 동의를 설정합니다.

![](./images/1-0-form.png)

이 동의 설정 작업으로 &quot;시작&quot;, &quot;종료&quot; 또는 &quot;데이터 요소에서 제공&quot;을 전달하도록 선택할 수 있습니다. 여기서 데이터 요소는 &quot;in&quot; 또는 &quot;out&quot;으로 확인되어야 합니다.

이 예제에서는 방문자가 Web SDK에서 플랫폼으로 데이터를 전송하는 것에 동의했음을 나타내기 위해 &quot;In&quot;을 선택합니다. 파란색 &quot;변경 사항 유지&quot; 버튼을 선택하여 이 작업을 저장한 다음 &quot;저장&quot;을 선택하여 이 규칙을 저장합니다.

참고: 웹 사이트 방문자가 옵트아웃하면 SDK에서에 대한 사용자 동의를 설정할 수 없습니다.

태그 규칙은 다양한 기본 제공 또는 사용자 지정 [이벤트](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/core/overview.html)에 의해 트리거될 수 있으며, 이 이벤트는 방문자 세션 중 적절한 시간에 이 동의 데이터를 전달하는 데 사용할 수 있습니다. 위의 예에서는 window loaded 이벤트를 사용하여 규칙을 트리거했습니다. 이후 섹션에서는 CMP의 동의 환경 설정 이벤트를 사용하여 동의 설정 작업을 트리거합니다. 옵트인 환경 설정 지정을 나타내는 원하는 이벤트에 의해 트리거되는 규칙에서 동의 설정 작업을 사용할 수 있습니다.

#### Platform Consent Standard 2.0으로 동의 설정

Platform 동의 표준 버전 2.0은 [XDM](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/schemas-and-experience-data-model.html) 데이터와 함께 작동합니다. 또한 동의 및 환경 설정 세부 사항 필드 그룹을 플랫폼의 프로필 스키마에 추가해야 합니다. Adobe 표준 버전 2.0 및 이 필드 그룹에 대한 자세한 내용은 [플랫폼의 동의 처리](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/adobe/overview.html)를 참조하십시오.

사용자 지정 코드 데이터 요소를 만들어 아래 스키마에 표시된 동의 오브젝트의 컬렉션 및 메타데이터 속성에 데이터를 전달합니다.

![](./images/collect-metadata.png)

이 동의 및 환경 설정 세부 정보 필드 그룹에는 규칙 작업에서 Platform Web SDK 확장을 사용하여 Platform으로 보내는 동의 환경 설정 데이터를 포함할 [동의 및 환경 설정 XDM 데이터 형식](https://experienceleague.adobe.com/docs/experience-platform/xdm/data-types/consents.html#prerequisites)에 대한 필드가 포함되어 있습니다. 현재, 플랫폼 동의 표준 2.0을 구현하는 데 필요한 유일한 속성은 수집 값(val) 및 위에서 빨간색으로 강조 표시된 메타데이터 시간 값입니다.

이 데이터에 대한 데이터 요소를 만들어 보겠습니다. Data Elements 를 선택하고 파란색 데이터 요소 추가 버튼을 클릭합니다. 이 &quot;xdm-consent 2.0&quot;을 호출하고 코어 확장을 사용하면 사용자 지정 코드 유형을 선택합니다. 사용자 지정 코드 편집기 창에 다음 데이터를 입력하거나 복사하여 붙여넣을 수 있습니다.

```js
var dateString = new Date().toISOString();

return {
  collect: {
    val: "y"
  },
  metadata: {
    time: dateString
  }
}
```

시간 필드는 사용자가 마지막으로 동의 환경 설정을 업데이트한 시기를 지정해야 합니다. JavaScript 날짜 개체에 표준 방법을 사용하는 예로 여기에서 타임스탬프를 만들고 있습니다. 저장 을 선택하여 사용자 지정 코드를 저장하고 저장 을 다시 선택하여 데이터 요소를 저장합니다.

그런 다음 규칙을 선택하고 파란색 규칙 추가 버튼을 선택한 다음 &quot;setConsent onLoad - Consent 2.0&quot;이라는 이름을 입력합니다. Window Loaded 이벤트를 규칙 트리거로 선택한 다음 작업에서 추가를 선택합니다. Platform Web SDK 확장을 선택하고 작업 유형에서 동의 설정을 선택합니다. 표준은 Adobe 버전이어야 하며 버전은 2.0이어야 합니다. 값의 경우, 방금 만든 데이터 요소에는 플랫폼으로 전송하는 데 필요한 수집 및 시간 값이 포함되어 있습니다.

![](./images/2-0-form.png)

이 예제 작업을 검토하기 위해 Platform 웹 SDK 확장에서 동의 설정 을 호출하고 양식에서 표준 및 버전을 전달하는 동시에 이전에 만든 데이터 요소에서 수집 및 시간에 대한 값을 전달합니다.

파란색 저장 버튼을 선택한 다음 다시 규칙을 저장합니다.

이제 각 플랫폼 동의 표준에 대해 하나씩, 두 개의 규칙이 있습니다. 실제로 사이트에서 하나의 표준을 선택할 수 있습니다. 다음으로 IAB TCF 2.0 동의 표준을 사용하는 예를 만듭니다.

## IAB TCF 2.0 동의 표준과 함께 Web SDK 사용

[IAB 유럽 웹 사이트](https://iabeurope.eu/transparency-consent-framework/)에서 IAB 투명성 및 동의 프레임워크 버전 2.0에 대해 자세히 알아볼 수 있습니다.

이 표준을 사용하여 동의 환경 설정 데이터를 설정하려면 IAB TCF 2.0 동의 세부 정보 스키마 필드 그룹을 플랫폼의 경험 이벤트 스키마에 추가해야 합니다.

![](./images/consentStrings.png)

이 필드 그룹에는 IAB TCF 2.0 표준에 필요한 동의 환경 설정 필드가 포함되어 있습니다. 스키마 및 필드 그룹에 대한 자세한 내용은 [XDM 시스템 개요](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=ko-KR)를 참조하십시오.

### 1단계: 동의 데이터 요소 만들기

IAB TCF 2.0 동의 표준을 사용하여 태그에서 동의 이벤트 데이터를 보내기 위해 먼저 필수 동의 필드로 xdm 데이터 요소를 설정합니다.

![](./images/data-element.png)

태그 클라이언트측 속성에서 데이터 요소 를 선택하고 파란색 &quot;데이터 요소 추가&quot; 버튼을 클릭합니다. 이 예제에서는 데이터 요소의 이름을 &quot;xdm-consentStrings&quot;로 지정합니다. 이러한 xdm 필드에는 IAB TCF 2.0 표준에 필요한 사용자 동의 데이터가 포함됩니다.

확장 드롭다운 메뉴에서 &quot;Platform Web SDK&quot;를 선택하고 데이터 요소 유형에 대해 &quot;XDM 개체&quot;를 선택합니다. 위의 스크린샷에 표시된 대로 &quot;consentStrings&quot; 항목을 선택하고 확장할 수 있는 xdm 매퍼가 표시되어야 합니다.

다음과 같이 각 consentStrings를 설정합니다.

* **`consentStandard`**: `IAB TCF`
* **`consentStandardVersion`**: `2.0`
* **`consentStringValue`**: `%IAB TCF Consent String%`
* **`containsPersonalData`**: `False`(값 선택 단추에서 선택됨)
* **`gdprApplies`**: `%IAB TCF Consent GDPR%`

`consentStandard` 및 `consentStandardVersion` 필드는 모두 사용 중인 표준(IAB TCF 버전 2.0)의 텍스트 문자열입니다. `consentStringValue`이(가) &quot;IAB TCF 동의 문자열&quot;이라는 데이터 요소를 참조합니다. 텍스트를 둘러싼 퍼센트 기호는 데이터 요소의 이름을 나타내며 잠시 후 살펴보도록 하겠습니다. `containsPersonalData` 필드는 IAB TCF 2.0 동의 문자열에 &quot;True&quot; 또는 &quot;False&quot;가 있는 개인 데이터가 포함되어 있는지 여부를 나타냅니다. `gdprApplies` 필드는 GDPR이 적용되는 경우 &quot;true&quot;를, GDPR이 적용되지 않는 경우 &quot;false&quot;를, GDPR이 적용되는지 여부를 알 수 없는 경우 &quot;정의되지 않음&quot;을 나타냅니다. 현재 웹 SDK는 &quot;정의되지 않음&quot;을 &quot;true&quot;로 처리하므로 &quot;gdprApply: 정의되지 않음&quot;으로 전송된 동의 데이터는 방문자가 GDPR이 적용되는 영역에 있는 것처럼 처리됩니다.

이러한 속성과 태그의 IAB TCF 2.0에 대한 자세한 내용은 [동의 설명서](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/iab-tcf/with-launch.html#getting-started)를 참조하십시오.

### 2단계: IAB TCF 2.0 표준으로 동의를 설정하는 규칙 만들기

다음으로, 웹 사이트 방문자가 이 표준에 대한 동의 데이터를 설정하거나 변경할 때 웹 SDK와의 동의를 설정하는 규칙을 만듭니다. 이 규칙에서는 [OneTrust](https://www.onetrust.com/products/cookie-consent/) 또는 [Sourcepoint](https://www.sourcepoint.com/cmp/)와 같은 CMP에서 이러한 동의 변경 신호를 캡처하는 방법도 알아봅니다.

#### 규칙 이벤트 추가

Platform 태그 속성에서 규칙 섹션을 선택한 다음 파란색 규칙 추가 단추에서 를 선택합니다. 규칙 이름을 setConsent - IAB로 지정하고 이벤트에서 추가를 선택하겠습니다. 이 이벤트의 이름을 tcfapi addEventListener 로 지정하고 편집기 열기 를 선택하여 사용자 지정 코드 편집기를 엽니다.

다음 코드를 복사하여 편집기 창에 붙여넣습니다.

```js
// Wait for window.__tcfapi to be defined, then trigger when the customer has completed their consent and preferences.
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && (tcData.eventStatus === "useractioncomplete" || tcData.eventStatus === "tcloaded")) {
        // save the tcData.tcString properties in data elements
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF Consent GDPR", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn't defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

이 코드는 `addEventListener`이라는 함수를 만들고 실행합니다. 함수는 `window.__tcfapi` 개체가 있는지 확인하고 있으면 API의 사양에 따라 이벤트 리스너를 추가합니다. GitHub의 [IAB 저장소](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework)에서 이러한 사양에 대해 자세히 알아볼 수 있습니다. 이 이벤트 수신기가 성공적으로 추가되고 웹 사이트 방문자가 동의 및 환경 설정 선택을 완료한 경우, 코드는 `tcData.tcString`에 대한 태그 사용자 지정 변수와 GDPR 영역에 대한 지표를 설정합니다. IAB TCF에 대한 자세한 내용은 IAB [웹 사이트](https://iabeurope.eu/transparency-consent-framework/) 및 [GitHub 저장소](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework)를 참조하십시오. 이러한 값을 설정한 후 코드는 이 규칙이 실행되도록 트리거하는 트리거 함수를 실행합니다.

이 함수를 처음 실행할 때 `window.__tcfapi` 개체가 없으면 이 함수는 100밀리초마다 개체를 다시 확인하므로 이벤트 리스너를 추가할 수 있습니다. 마지막 코드 행은 그 위의 코드 행에 정의된 `addEventListener` 함수를 실행합니다.

요약하자면, CMP(또는 사용자 지정) 동의 배너를 사용하여 웹 사이트 방문자가 설정하는 동의 상태를 확인하는 기능을 만들었습니다. 동의 환경 설정이 설정되면 이 코드는 규칙 작업에 사용할 수 있는 두 개의 사용자 지정 변수(사용자 지정 코드 데이터 요소)를 만듭니다. 위의 코드를 이벤트의 사용자 지정 코드 편집기 창에 붙여넣은 후 파란색 저장 버튼을 선택하여 규칙 이벤트를 저장합니다.

이제 이러한 값을 사용하여 플랫폼으로 전송하는 동의 규칙 설정 작업을 설정해 보겠습니다.

#### 규칙 작업 추가

작업 섹션에서 추가 를 선택합니다. 확장 아래의 드롭다운에서 Platform Web SDK 를 선택합니다. 작업 유형에서 동의 설정을 선택합니다. 이 작업의 이름을 setConsent로 지정하겠습니다.

동의 정보 아래의 작업 구성에서 양식 작성을 선택합니다. [표준]의 경우 [IAB TCF]를 선택하고 [버전]의 경우 2.0을 입력합니다. 값의 경우 이벤트의 사용자 지정 변수를 사용하고 위의 규칙 이벤트 사용자 지정 함수에서 캡처한 [tcData](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20CMP%20API%20v2.md#tcdata)에서 가져온 `%IAB TCF Consent String%`을(를) 입력합니다.

GDPR 적용 아래에서 이벤트의 다른 사용자 지정 변수를 사용하고 위의 규칙 이벤트 사용자 지정 함수에서 캡처한 `tcData`에서 가져온 `%IAB TCF Consent GDPR%`을(를) 입력합니다. GDPR이 이 웹 사이트 방문자에게 확실히 적용되거나 적용되지 않는 경우 사용자 지정 변수(데이터 요소) 선택 사항을 사용하는 대신 해당하는 경우 예 또는 아니오를 선택할 수 있습니다. 데이터 요소에서 조건부 논리를 사용하여 GDPR이 적용되는지 확인하고 적절한 값을 반환할 수도 있습니다.

GDPR 개인 데이터 포함 아래에서 이 사용자의 데이터에 개인 데이터가 포함되어 있는지 여부를 나타내는 옵션을 선택합니다. 여기서 데이터 요소는 true 또는 false로 확인되어야 합니다.

![](./images/data-element-2-0.png)

작업을 저장하려면 파란색 저장 버튼을 선택하고 규칙을 저장하려면 파란색 저장(또는 라이브러리에 저장) 버튼을 선택합니다. 이 시점에서 IAB TCF 2.0 동의 표준과 함께 Web SDK 확장을 사용하여 동의를 설정하기 위해 태그의 데이터 요소와 규칙을 성공적으로 구현했습니다.

### 3단계: Save to Library and Build

[작업 라이브러리](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/add-data-elements-rules.html#use-the-working-library-feature) 필수 구성 요소를 사용하는 경우 이러한 변경 내용을 이미 저장하고 개발 라이브러리를 빌드했습니다.

![](./images/save-library.png)

### 4단계: Inspect 및 데이터 수집 유효성 검사

사이트에서 페이지를 새로 고치고 태그 메뉴 섹션의 [Debugger](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) Chrome 확장에서 라이브러리 빌드를 확인합니다.

![](./images/build-date.png)

또한 `{"consent":[{"value":{"general":"in"},"version…`이(가) 표시되는 네트워크 요청의 Adobe 본문 줄에서 을 선택하여 디버거 플랫폼 웹 SDK 섹션에서 POST 1.0 또는 2.0 표준에 대한 setConsent 호출을 검사할 수도 있습니다.

![](./images/inspect-consent-call.png)

IAB TCF 2.0 표준에 대한 setConsent 호출과 규칙의 유효성을 검사하기 위해 테스트 사이트에서 OneTrust 동의 배너를 사용하여 동의 환경 설정을 지정하고 앞에서 설명한 tcData를 만듭니다.

![](./images/banner.png)

&quot;동의함&quot;을 선택하면 `{"consent":[{"value":"someAlphaNumericCharacters…`이(가) 표시되는 네트워크 요청의 POST 본문 줄에서 을 선택하여 디버거 Platform Web SDK 섹션에서 IAB TCF 2.0 표준에 대한 setConsent 호출을 검사할 수 있습니다.

![](./images/inspect-2-0.png)

여기서는 데이터 요소 및 태그 규칙에서 이전에 설정한 데이터를 확인합니다. 값 속성에는 이전에 보았던 인코딩된 tcString 데이터가 포함됩니다.

IAB TCF 2.0 표준을 구현하는 OneTrust, Sourcepoint 및 기타 CMP는 모두 유사한 데이터를 생성합니다. 위에서 만든 규칙의 사용자 지정 코드 이벤트를 사용하여 해당 데이터를 캡처하고 태그의 Web SDK 확장과 함께 사용할 수 있습니다. 사용자 지정 코드는 IAB TCF 2.0 데이터를 생성하는 데 사용되는 CMP에 관계없이 동일합니다. 사용자 지정 코드는 플랫폼 동의 표준(1.0 또는 2.0) 중 하나와 함께 사용할 수도 있습니다.

## 경험 이벤트를 사용하여 동의 데이터 보내기

앞에서 만든 &quot;xdm-consentStrings&quot; 데이터 요소를 두 규칙의 데이터 요소 필드에서 참조하지 않았을 수 있습니다. 이 데이터 요소는 경험 이벤트와 함께 동의 데이터를 보내야 할 때 사용됩니다.

![](./images/consentStrings-data-element.png)

이 데이터 요소에는 IAB TCF 2.0 표준에 필요한 모든 필드가 포함되어 있으므로 경험 이벤트와 함께 이 xdm 데이터를 전송할 때 데이터 요소를 간단히 참조할 수 있습니다.

![](./images/consentStrings-reference.png)

## 결론

데이터를 검사하고 유효성을 검사했으므로 Platform용 Platform Web SDK 확장을 사용하여 CMP에서 얻은 동의 데이터를 구현하고 활성화하는 방법에 대해 알아보십시오.
