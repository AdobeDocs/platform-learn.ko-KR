---
title: CMP(동의 관리 플랫폼)를 사용하여 동의 구현
description: 데이터 수집에서 Adobe Experience Platform 웹 SDK 확장을 사용하여 CMP(동의 관리 플랫폼)에서 얻은 동의 데이터를 구현하고 활성화하는 방법을 알아봅니다.
feature: Web SDK, Tags
role: Developer, Data Engineer
doc-type: tutorial
exl-id: bee792c3-17b7-41fb-a422-289ca018097d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '3347'
ht-degree: 1%

---

# Platform Web SDK 확장을 사용하여 CMP(동의 관리 플랫폼)로 동의를 구현합니다

많은 법률 개인 정보 보호 규정에서 데이터 수집, 개인화 및 기타 마케팅 사용 사례와 관련하여 활성 및 특정 동의에 대한 요구 사항을 도입했습니다. 이러한 요구 사항을 충족하기 위해 Adobe Experience Platform을 사용하면 개별 고객 프로필에서 동의 정보를 캡처하고 이러한 환경 설정을 다운스트림 Platform 워크플로우에서 각 고객의 데이터가 사용되는 방식을 결정하는 요소로 사용할 수 있습니다.

>[!NOTE]
>
>Adobe Experience Platform Launch은 데이터 수집 기술 세트로 Adobe Experience Platform에 통합되고 있습니다. 인터페이스에서 이 컨텐츠를 사용하는 동안 알고 있어야 하는 몇 가지 용어 변경 사항이 롤아웃되었습니다.
>
> * 이제 platform launch(클라이언트측)가 **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)**
> * 이제 platform launch 서버 측 **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * 이제 Edge 구성이 제공됩니다. **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)**


이 자습서에서는 데이터 수집에서 Platform Web SDK 확장을 사용하여 CMP(동의 관리 플랫폼)에서 얻은 동의 데이터를 구현하고 활성화하는 방법을 보여줍니다. OneTrust 또는 Sourcepoint를 CMP와 함께 Adobe 표준과 IAB TCF 2.0 동의 표준을 모두 사용하여 이 작업을 수행합니다.

이 자습서에서는 Platform Web SDK 확장을 사용하여 동의 데이터를 Platform에 보냅니다. 웹 SDK에 대한 개요는 다음을 참조하십시오 [이 페이지](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=en).

## 전제 조건

웹 SDK를 사용하기 위한 사전 요구 사항이 나열되어 있습니다 [여기](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/prerequisite.html?lang=en#fundamentals).

해당 페이지에는 &quot;이벤트 데이터 세트&quot;에 대한 요구 사항이 있으며, 꼭 그렇듯, 경험 이벤트 데이터를 보유하기 위한 데이터 세트입니다. 이벤트와 함께 동의 정보를 보내려면 [개인 정보 보호 세부 사항 필드 그룹](https://github.com/adobe/xdm/blob/master/docs/reference/field groups/experience-event/experienceevent-privacy.schema.md)를 경험 이벤트 스키마에 추가해야 합니다.

![](./images/event-schema.png)

플랫폼 동의 표준 v2.0의 경우, XDM 개별 프로필 스키마 및 데이터 세트를 만들려면 Adobe Experience Profile에 액세스해야 합니다. 스키마 만들기에 대한 자습서는 다음을 참조하십시오 [스키마 편집기를 사용하여 스키마 만들기](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en#tutorials) 및 필수 기본 설정 세부 정보 프로파일 필드 그룹에 대한 내용은 [XDM 설명서](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/overview.html?lang=en).

이 자습서에서는 데이터 수집에 대한 액세스 권한이 있고 웹 SDK 확장이 설치되어 있고 개발을 위해 제작 및 빌드된 작업 라이브러리를 사용하여 클라이언트측 태그 속성을 생성했다고 가정합니다. 이러한 항목은 다음 문서에 자세히 설명되어 있습니다.

* [속성 만들기 또는 구성](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html?lang=en#create-or-configure-a-property)
* [라이브러리 개요](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/libraries.html)
* [게시 개요](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html)

또한 [Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) Chrome 확장 프로그램 을 사용하여 구현을 검사하고 확인할 수 있습니다.

자체 사이트에서 CMP를 사용하여 IAB TCF 예를 구현하려면 OneTrust 또는 Sourcepoint와 같은 CMP에 액세스하여 제공된 데이터를 생성해야 하거나, 여기를 따라 수행하여 아래 결과를 볼 수 있습니다.

## Adobe 동의 표준(v1.0 또는 v2.0)에서 웹 SDK 사용

>[!NOTE]
>
>1.0 표준은 v2.0을 위해 단계적으로 지원되지 않습니다. 2.0 표준을 사용하면 수동으로 동의 환경 설정을 적용하는 데 사용할 수 있는 추가 동의 데이터를 추가할 수 있습니다. Platform Web SDK 확장의 아래 스크린샷은 버전에서 만들어졌습니다 [2.4.0](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html?lang=en#version-2.4.0) Adobe 동의 Standard의 v1.0 또는 v2.0과 호환되는 확장 프로그램.

이러한 표준에 대한 자세한 내용은 [고객 동의 기본 설정 지원](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html).

### 1단계: 웹 SDK 확장에서 동의 구성

태그 속성에 Platform Web SDK 확장을 설치하면 확장 구성 화면에서 동의 데이터 주소 지정 옵션을 구성할 수 있습니다.

![](./images/pending.png)

&quot;개인 정보&quot; 섹션은 사용자가 이전에 동의 환경 설정을 제공하지 않은 경우 SDK에 대한 동의 수준을 설정합니다. SDK에서 동의 및 이벤트 데이터 수집에 대한 기본 상태를 설정합니다. 선택한 설정은 &quot;사용자가 아직 명시적 동의 환경 설정을 제공하지 않은 경우 SDK에서 수행할 작업&quot;이라는 질문에 답합니다.

* 에서 - 사용자가 동의 환경 설정을 제공하기 전에 발생하는 이벤트를 수집합니다.
* 출력 - 사용자가 동의 환경 설정을 제공하기 전에 발생하는 이벤트를 삭제합니다.
* 보류 중 - 사용자가 동의 환경 설정을 제공하기 전에 발생하는 이벤트를 큐에 추가합니다.
* 데이터 요소에서 제공

기본 동의 설정이 &quot;In&quot;인 경우, SDK에 명시적인 동의를 기다리지 않고 사용자가 동의 환경 설정을 제공하기 전에 발생하는 이벤트를 수집해야 함을 알려줍니다. 이러한 환경 설정은 일반적으로 CMP에서 처리 및 저장됩니다.

기본 동의 설정이 &quot;Out&quot;인 경우, 사용자 옵트인 환경 설정이 설정되기 전에 발생하는 이벤트를 수집하지 않도록 SDK에 알려줍니다. 동의 기본 설정을 설정하기 전에 발생하는 방문자 활동은 동의가 설정된 후 SDK에서 전송한 데이터에 포함되지 않습니다. 예를 들어, 동의 배너를 선택하기 전에 웹 페이지를 스크롤하여 보고 이 &quot;종료&quot; 설정을 사용하는 경우, 사용자가 나중에 데이터 수집에 대한 명시적 동의를 제공하면 해당 스크롤 활동 및 보기 시간이 전송되지 않습니다.

기본 동의 설정이 &quot;보류 중&quot;이면 SDK는 사용자가 동의 환경 설정을 제공하기 전에 발생하는 모든 이벤트를 큐에 추가하므로 동의 환경 설정이 설정된 후, SDK가 방문 중에 처음 구성된 후에 이벤트를 전송할 수 있습니다.

이 &quot;보류 중&quot; 설정을 사용하면 사용자 옵트인 환경 설정이 필요한 명령(예: 이벤트 명령)을 실행하려고 하면 SDK 내에서 명령이 대기됩니다. 이러한 명령은 사용자의 옵트인 환경 설정을 SDK에 전달할 때까지 처리되지 않습니다.

CMP에서 사용자의 환경 설정을 수집하면 해당 환경 설정을 SDK에 전달할 수 있습니다. 아래의 마지막 섹션에서는 해당 옵트인 데이터를 가져와 웹 SDK 확장에서 사용하는 방법을 알아봅니다.

&quot;데이터 요소에서 제공&quot;을 사용하면 사용자 지정 코드 또는 사이트 또는 데이터 계층에서 CMP로 캡처된 동의 기본 설정 데이터가 포함된 데이터 요소에 액세스할 수 있습니다. 이 용도로 사용되는 데이터 요소는 &quot;in&quot;, &quot;out&quot; 또는 &quot;pending&quot;으로 확인되어야 합니다.

참고: SDK에 대한 이 구성 설정은 사용자의 프로필에 지속되지 않으며, 방문자가 명시적 동의 환경 설정을 제공하기 전에 SDK의 동작을 설정하는 것에 한정됩니다.

웹 SDK 확장 구성에 대한 자세한 내용은 [Platform 웹 SDK 확장 개요](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/web-sdk-extension-configuration.html?lang=en#configure-the-extension) 및 [고객 동의 기본 설정 지원](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html).

이 예제에서는 &quot;보류 중&quot;에 대한 옵션을 선택하고 **저장** 구성 설정을 저장하려면 다음을 수행하십시오.

### 2단계: 동의 기본 설정 통신

SDK의 기본 동작을 설정했으므로 태그를 사용하여 방문자의 명시적 동의 환경 설정을 Platform에 보낼 수 있습니다. Adobe 1.0 또는 2.0 표준을 사용하여 동의 데이터 전송을 태그 규칙에 웹 SDK의 setConsent 작업을 사용하여 쉽게 구현할 수 있습니다.

#### Platform Consent Standard 1.0으로 동의 설정

규칙을 만들어 보여 드리겠습니다. Platform 태그 속성에서 규칙 을 선택한 다음 파란색 규칙 추가 버튼을 선택합니다. 규칙 이름을 &quot;setAdobeConsent&quot;로 지정하고 이벤트를 추가하도록 선택합니다. 이벤트 유형에 대해 &quot;Window Loaded&quot;를 선택하면 웹 사이트에 페이지가 로드될 때마다 이 규칙이 실행됩니다. 그런 다음 &quot;작업&quot; 아래에서 &quot;추가&quot;를 선택하여 작업 구성 화면을 엽니다. 여기서 동의 데이터를 설정합니다. 확장 드롭다운을 선택하고 &quot;Platform Web SDK&quot;를 선택한 다음 &quot;작업 유형&quot;을 선택하고 &quot;동의 설정&quot;을 선택합니다.

&quot;동의 정보&quot;에서 &quot;양식 작성&quot;을 선택합니다. 이 규칙 작업에서는 표시되는 양식을 작성하여 웹 SDK를 사용하여 Adobe 1.0 동의 표준에 대한 동의를 설정합니다.

![](./images/1-0-form.png)

이 동의 설정 작업과 함께 &quot;In&quot;, &quot;Out&quot; 또는 &quot;데이터 요소에 의해 제공됨&quot;을 전달하도록 선택할 수 있습니다. 여기서 데이터 요소는 &quot;in&quot; 또는 &quot;out&quot;으로 확인되어야 합니다.

이 예제에서는 &quot;In&quot;을 선택하여 방문자가 Web SDK에서 Platform으로 데이터를 전송하도록 허용했음을 나타냅니다. 파란색 &quot;변경 내용 유지&quot; 단추를 선택하여 이 작업을 저장한 다음 &quot;저장&quot;을 선택하여 이 규칙을 저장합니다.

참고: 웹 사이트 방문자가 옵트아웃하면 SDK에서 사용자 동의에 대한 설정을 허용하지 않습니다.

태그 규칙은 다양한 기본 제공 또는 사용자 지정에 의해 트리거될 수 있습니다 [events](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/core/overview.html?lang=en) 방문자 세션 중에 적절한 시간에 이 동의 데이터를 전달하는 데 사용할 수 있습니다. 위의 예에서는 window loaded 이벤트를 사용하여 규칙을 트리거했습니다. 이후 섹션에서는 CMP의 동의 기본 설정 이벤트를 사용하여 동의 설정 작업을 트리거합니다. 옵트인 환경 설정을 나타내는 원하는 이벤트에 의해 트리거되는 규칙에서 동의 설정 작업을 사용할 수 있습니다.

#### Platform Consent Standard 2.0으로 동의 설정

플랫폼 동의 표준의 버전 2.0은 [XDM](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/schemas-and-experience-data-model.html?lang=ko-KR) 데이터. 또한 Platform의 프로필 스키마에 개인 정보 필드 그룹을 추가해야 합니다. 자세한 내용은 [플랫폼의 동의 처리](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/adobe/overview.html) Adobe 표준 버전 2.0 및 이 필드 그룹에 대한 자세한 내용을 확인하십시오.

아래 스키마에 표시된 동의 개체의 수집 및 메타데이터 속성에 데이터를 전달하는 사용자 지정 코드 데이터 요소를 만듭니다.

![](./images/collect-metadata.png)

이 기본 설정 세부 정보 필드 그룹에는 [동의 및 기본 설정 XDM 데이터 유형](https://experienceleague.adobe.com/docs/experience-platform/xdm/data-types/consents.html?lang=en#prerequisites) 에는 규칙 작업에서 Platform Web SDK 확장을 사용하여 Platform에 보내는 동의 기본 설정 데이터가 포함됩니다. 현재 Platform Consent Standard 2.0을 구현하는 데 필요한 유일한 속성은 컬렉션 값(val) 및 메타데이터 시간 값이며 위에 빨간색으로 강조 표시되어 있습니다.

이 데이터에 대한 데이터 요소를 만들겠습니다. 데이터 요소 를 선택하고 파란색 데이터 요소 추가 단추를 선택합니다. 이를 &quot;xdm-consent 2.0&quot;이라고 하고 코어 확장을 사용하여 사용자 지정 코드 유형을 선택합니다. 다음 데이터를 입력하거나 복사하여 사용자 지정 코드 편집기 창에 붙여넣을 수 있습니다.

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

시간 필드는 사용자가 마지막으로 동의 환경 설정을 업데이트한 시기를 지정해야 합니다. JavaScript Date 개체의 표준 방법을 사용하여 여기에 타임스탬프를 만들고 있습니다. 저장 을 선택하여 사용자 지정 코드를 저장하고 다시 저장 을 선택하여 데이터 요소를 저장합니다.

다음으로, 규칙 을 선택한 다음 파란색 규칙 추가 단추를 선택하고 이름 &quot;setConsent onLoad - Consent 2.0&quot;을 입력합니다. 규칙 트리거로 Window Loaded 이벤트를 선택한 다음 작업 아래에서 추가를 선택합니다. Platform Web SDK 확장을 선택하고 작업 유형에 대해 동의 설정을 선택합니다. Standard는 Adobe이어야 하며 버전은 2.0이어야 합니다. 값의 경우 Platform에 전송하는 데 필요한 수집 및 시간 값이 포함된 방금 만든 데이터 요소를 사용합니다.

![](./images/2-0-form.png)

이 예제 작업을 검토하기 위해 Platform Web SDK 확장에서 동의 설정 을 호출하고 양식에서 표준 및 버전을 전달하며 이전에 만든 데이터 요소에서 수집 및 시간 값을 전달합니다.

파란색 저장 단추를 선택하고 다시 선택하여 규칙을 저장합니다.

이제 두 개의 규칙이 있습니다. 각 플랫폼 동의 표준에 대해 하나씩. 실제로 사이트에서 한 가지 표준을 선택할 수 있습니다. 다음으로, IAB TCF 2.0 동의 표준을 사용하는 예를 만듭니다.

## IAB TCF 2.0 Consent Standard에서 웹 SDK 사용

에서 IAB 투명성 및 동의 프레임워크 버전 2.0에 대해 자세히 알 수 있습니다 [IAB 유럽 웹 사이트](https://iabeurope.eu/transparency-consent-framework/).

이 표준을 사용하여 동의 기본 설정 데이터를 설정하려면 플랫폼의 경험 이벤트 스키마에 개인 정보 세부 사항 필드 그룹을 추가해야 합니다.

![](./images/consentStrings.png)

이 필드 그룹에는 IAB TCF 2.0 표준에 필요한 동의 기본 설정 필드가 포함되어 있습니다. 스키마 및 필드 그룹에 대한 자세한 내용은 다음을 참조하십시오. [XDM 시스템 개요](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=ko).

### 1단계: 동의 데이터 요소 만들기

IAB TCF 2.0 동의 표준을 사용하여 태그에서 동의 이벤트 데이터를 보내려면 먼저 필수 동의 필드가 있는 xdm 데이터 요소를 설정합니다.

![](./images/data-element.png)

태그 클라이언트측 속성에서 데이터 요소 를 선택하고 파란색 &quot;데이터 요소 추가&quot; 버튼을 선택합니다. 이 예제에서는 이 데이터 요소의 이름을 &quot;xdm-consentStrings&quot;로 지정합니다. 이러한 xdm 필드에는 IAB TCF 2.0 표준에 필요한 사용자 동의 데이터가 포함됩니다.

확장 드롭다운 메뉴에서 &quot;Platform Web SDK&quot;를 선택하고 데이터 요소 유형에 대해 &quot;XDM 개체&quot;를 선택합니다. xdm 매퍼가 나타나야 합니다. 위의 스크린샷에 표시된 대로 &quot;consentStrings&quot; 항목을 선택하고 확장할 수 있습니다.

각 consentStrings를 다음과 같이 설정합니다.

* **`consentStandard`**:  `IAB TCF`
* **`consentStandardVersion`**:  `2.0`
* **`consentStringValue`**:  `%IAB TCF Consent String%`
* **`containsPersonalData`**:  `False` (값 선택 단추에서 선택됨)
* **`gdprApplies`**:  `%IAB TCF Consent GDPR%`

consentStandard 및 consentStandardVersion은 모두 IAB TCF 버전 2.0인 사용 중인 표준에 대한 텍스트 문자열입니다. consentStringValue는 &quot;IAB TCF Consent String&quot;이라는 데이터 요소를 참조합니다. 텍스트 주위에 있는 퍼센트 기호는 데이터 요소의 이름을 나타내며, 잠시 후에 살펴보겠습니다. containsPersonalData 속성은 IAB TCF 2.0 동의 문자열에 &quot;True&quot; 또는 &quot;False&quot;가 있는 개인 데이터가 포함되어 있는지 여부를 나타냅니다. GDPR적용 필드는 GDPR이 적용되는 &quot;true&quot;, GDPR에 대한 &quot;false&quot;가 적용되지 않거나 GDPR이 적용되는지 여부를 알 수 없는 &quot;정의되지 않음&quot;을 나타냅니다. 현재 웹 SDK는 &quot;정의되지 않음&quot;을 &quot;true&quot;로 처리하므로 &quot;gdprApply로 전송된 동의 데이터는 다음과 같습니다. 정의되지 않음&quot;은 방문자가 GDPR이 적용되는 영역에 있는 것처럼 처리됩니다.

자세한 내용은 [동의 설명서](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/iab-tcf/with-launch.html?lang=en#getting-started) 추가 정보 및 태그의 IAB TCF 2.0에 대한 정보.

### 2단계: IAB TCF 2.0 Standard로 동의를 설정하는 규칙 만들기

다음으로, 웹 사이트 방문자가 이 표준에 대한 동의 데이터를 설정 또는 변경할 때 웹 SDK로 동의를 설정하는 규칙을 만듭니다. 이 규칙에서, 같은 CMP에서 이러한 동의 변경 신호를 캡처하는 방법도 보게 됩니다 [OneTrust](https://www.onetrust.com/products/cookie-consent/) 또는 [Sourcepoint](https://www.sourcepoint.com/cmp/).

#### 규칙 이벤트 추가

Platform 태그 속성에서 규칙 섹션을 선택한 다음 파란색 규칙 추가 버튼을 선택합니다. 규칙 setConsent - IAB의 이름을 지정하고 이벤트 아래에서 추가를 선택합니다. 이 이벤트 이름을 tcfapi addEventListener 로 지정하고 편집기 열기 를 선택하여 사용자 지정 코드 편집기를 엽니다.

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

이 코드는 addEventListener라는 함수를 만들고 실행하기만 하면 됩니다. 함수는 창을 확인합니다.__tcfapi 개체가 존재하고 있고 있는 경우 API의 사양에 따라 이벤트 리스너를 추가합니다. 자세한 내용은 [IAB 리포지토리](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework) GitHub에서 사용. 이 이벤트 리스너가 추가되고 웹 사이트 방문자가 동의 및 환경 설정 선택을 완료하면 코드는 tcData tcString에 대한 사용자 지정 변수와 GDPR 영역에 대한 지표를 설정합니다. IAB TCF에 대한 자세한 내용은 IAB를 참조하십시오 [웹 사이트](https://iabeurope.eu/transparency-consent-framework/) 및 [GitHub 리포지토리](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework) 자세한 내용은 이러한 값을 설정한 후에는 코드가 이 규칙을 실행하도록 트리거하는 트리거 함수를 실행합니다.

창가라면__tcfapi 개체가 처음 실행될 때 존재하지 않았습니다. 이 함수가 100밀리초마다 다시 확인하므로 이벤트 리스너를 추가할 수 있습니다. 마지막 코드 행은 코드 줄 위에 정의된 addEventListener 함수를 실행합니다.

요약하기 위해 CMP(또는 사용자 지정) 동의 배너를 사용하여 웹 사이트 방문자가 설정하는 동의 상태를 확인하는 함수를 만들었습니다. 해당 동의 기본 설정이 설정되면 이 코드는 규칙 작업에서 사용할 수 있는 두 개의 사용자 지정 변수(사용자 지정 코드 데이터 요소)를 만듭니다. 위의 코드를 이벤트의 사용자 지정 코드 편집기 창에 붙여넣은 후 파란색 저장 단추를 선택하여 규칙 이벤트를 저장합니다.

이제 이러한 값을 사용하여 Platform으로 전송하도록 동의 규칙 설정 작업을 설정하겠습니다.

#### 규칙 작업 추가

작업 섹션에서 추가 를 선택합니다. 확장의 드롭다운에서 Platform Web SDK를 선택합니다. 작업 유형에서 동의 설정을 선택합니다. 이 작업의 이름을 setConsent로 지정합니다.

동의 정보 아래의 작업 구성에서 양식 작성을 선택합니다. Standard의 경우 IAB TCF를 선택하고 Version에 대해 2.0을 입력합니다. 값의 경우 이벤트의 사용자 지정 변수를 사용하고 [tcData](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20CMP%20API%20v2.md#tcdata) 위의 규칙 이벤트 사용자 지정 함수에서 캡처되었습니다.

GDPR 적용에서 이벤트의 다른 사용자 지정 변수를 사용하고 위의 규칙 이벤트 사용자 지정 함수에서 캡처된 tcData에서도 나오는 %IAB TCF 동의 GDPR%를 입력합니다. 이 웹 사이트 방문자에 대해 GDPR이 확실히 적용되거나 적용되지 않는다는 사실을 알고 있는 경우 사용자 지정 변수(데이터 요소) 선택을 사용하는 대신 적용 가능한 경우 예 또는 아니요 를 선택할 수 있습니다. 데이터 요소에서 조건부 논리를 사용하여 GDPR이 적용되는지 확인하고 적절한 값을 반환할 수도 있습니다.

GDPR의 개인 데이터 포함에서 이 사용자의 데이터에 개인 데이터가 포함되어 있는지 여부를 나타내는 옵션을 선택합니다. 여기에서 데이터 요소는 true 또는 false로 확인되어야 합니다.

![](./images/data-element-2-0.png)

파란색 저장 단추를 선택하여 작업을 저장하고 파란색 저장(또는 라이브러리에 저장) 단추를 선택하여 규칙을 저장합니다. 이 시점에서 IAB TCF 2.0 동의 표준과 함께 웹 SDK 확장을 사용하여 동의를 설정하는 태그의 데이터 요소와 규칙을 성공적으로 구현했습니다.

### 3단계: 라이브러리 및 빌드에 저장

를 사용 중이라면 [작업 라이브러리](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/add-data-elements-rules.html?lang=en#use-the-working-library-feature) 이러한 변경 사항을 이미 저장하고 개발 라이브러리를 빌드해야 합니다.

![](./images/save-library.png)

### 4단계: Inspect 및 데이터 수집 유효성 검사

사이트에서 페이지를 새로 고치고 라이브러리 빌드를 [Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) 태그 메뉴 섹션의 Chrome 확장 프로그램:

![](./images/build-date.png)

또한 표시되는 네트워크 요청의 POST 본문 줄을 선택하여 디버거 Platform Web SDK 섹션에서 Adobe 1.0 또는 2.0 표준에 대한 setConsent 호출을 검사할 수 있습니다 `{"consent":[{"value":{"general":"in"},"version…`:

![](./images/inspect-consent-call.png)

IAB TCF 2.0 표준에 대한 setConsent 호출 및 규칙의 유효성을 검사하기 위해 테스트 사이트의 OneTrust 동의 배너를 사용하여 동의 환경 설정을 지정하고 앞에서 설명한 tcData를 만듭니다.

![](./images/banner.png)

&quot;동의&quot;를 선택한 후 표시되는 네트워크 요청의 POST 본문 줄을 선택하여 디버거 Platform Web SDK 섹션에서 IAB TCF 2.0 표준에 대한 setConsent 호출을 검사할 수 있습니다 `{"consent":[{"value":"someAlphaNumericCharacters…`.

![](./images/inspect-2-0.png)

여기에서는 데이터 요소 및 태그 규칙에서 이전에 설정한 데이터가 표시됩니다. 값 속성에는 이전에 본 인코딩된 tcString 데이터가 포함되어 있습니다.

IAB TCF 2.0 표준을 구현하는 OneTrust, Sourcepoint 및 기타 CMP는 모두 페이지에 유사한 데이터를 생성합니다. 위의 규칙에서 사용자 지정 코드 이벤트를 사용하여 해당 데이터를 캡처하고 태그의 웹 SDK 확장과 함께 사용할 수 있습니다. 사용자 지정 코드는 IAB TCF 2.0 데이터를 생성하는 데 사용되는 CMP와 관계없이 동일합니다. 사용자 지정 코드는 플랫폼 동의 표준(1.0 또는 2.0) 중 하나와 함께 사용할 수도 있습니다.

## Experience Events로 동의 데이터 보내기

이전에 규칙 중 하나의 데이터 요소 필드에서 만든 &quot;xdm-consentStrings&quot; 데이터 요소를 참조하지 않았다는 것을 알고 있었을 것입니다. 이 데이터 요소는 경험 이벤트로 동의 데이터를 전송해야 할 때 사용하기 위한 것입니다.

![](./images/consentStrings-data-element.png)

이 데이터 요소에는 IAB TCF 2.0 표준에 필요한 모든 필드가 포함되어 있으므로 경험 이벤트와 함께 이 xdm 데이터를 전송할 때 데이터 요소를 간단히 참조할 수 있습니다.

![](./images/consentStrings-reference.png)

## 결론

이제 데이터를 검사하고 유효성을 검사했으므로 Platform용 Platform Web SDK 확장을 사용하여 CMP에서 얻은 동의 데이터를 구현하고 활성화하는 방법을 볼 수 있습니다.
