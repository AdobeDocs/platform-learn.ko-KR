---
title: 웹 사이트에서 Brand Concierge 구현
description: 웹 사이트에서 Brand Concierge 구현
kt: 5342
doc-type: tutorial
source-git-commit: ea5fa4694205a94f63d277fdcf2018951fa31fbc
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 0%

---

# 1.4.2 웹 사이트에서 Brand Concierge 구현

>[!IMPORTANT]
>
>이 연습을 완료하려면 작업 중인 AEM Assets CS Author 환경 및 AEM CS/EDS 웹 사이트에 액세스할 수 있어야 합니다.
>
>환경이 없는 경우 [Adobe Experience Manager Cloud Service 및 Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}(으)로 이동하세요. 거기에 있는 지침을 따르십시오, 그러면 당신은 이러한 환경에 액세스 할 수 있습니다.

>[!IMPORTANT]
>
>이전에 AEM Assets CS 환경에서 AEM CS 프로그램을 구성한 경우 AEM CS 샌드박스가 최대 절전 모드일 수 있습니다. 이러한 샌드박스의 최대 절전 모드 해제 시간이 10~15분 정도 걸리는 점을 감안할 때, 나중에 최대 절전 모드 해제 프로세스를 기다릴 필요가 없도록 지금 시작하는 것이 좋습니다.

## 1.4.2.1 Brand Concierge - AEM 작성자를 표시하도록 웹 사이트 구성

Brand Concierge이 웹 사이트에 표시되려면 새 페이지에 추가해야 하는 새 사용자 지정 블록을 만들어야 하며, 새 페이지가 웹 사이트 탐색에 추가되었는지 확인해야 합니다.

이제 다음 항목을 이 순서로 구성해야 합니다.

- 웹 사이트에서 Brand Concierge을 로드하는 데 사용할 새 사용자 지정 블록을 만듭니다.
- 웹 사이트에서 Brand Concierge에 대한 새 페이지를 만듭니다.
- 새로 만든 Brand Concierge 페이지에서 새로 만든 사용자 지정 블록을 연결합니다.
- 웹 사이트의 탐색 헤더 파일에서 새로 생성된 Brand Concierge 페이지로 이동하려면 참조를 추가합니다.

### 새 사용자 지정 블록 만들기

새 사용자 지정 블록을 만들려면 웹 사이트에 연결된 GitHub 저장소로 이동합니다.

![차단](./images/block1.png)

#### component-definition.json

**component-definition.json** 파일이 표시될 때까지 아래로 스크롤하여 엽니다

![차단](./images/block8.png)

**pencl** 아이콘을 클릭하여 파일 편집을 시작합니다.

![차단](./images/block8a.png)

**블록**&#x200B;이 표시될 때까지 아래로 스크롤합니다. 구성 요소 **카드**&#x200B;의 닫는 대괄호 아래에 커서를 설정합니다.

![차단](./images/block9.png)

이 코드를 붙여넣고 코드 블록 뒤에 쉼표 **,**&#x200B;을(를) 입력하십시오.

```json
{
  "title": "BrandConcierge",
  "id": "brandconcierge",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/block/v1/block",
        "template": {
          "name": "BrandConcierge",
          "model": "brandconcierge"
        }
      }
    }
  }
},
```

**변경 내용 커밋...**&#x200B;을 클릭합니다.

![차단](./images/block10.png)

**변경 내용 커밋**&#x200B;을 클릭합니다.

![차단](./images/block10a.png)

#### component-models.json

**component-models.json** 파일이 표시될 때까지 아래로 스크롤한 다음 **pencil** 아이콘을 클릭하여 파일 편집을 시작합니다.

![차단](./images/block11.png)

마지막 항목이 표시될 때까지 아래로 스크롤합니다. 마지막 구성 요소의 닫는 대괄호 옆에 커서를 설정합니다.

![차단](./images/block12.png)

쉼표 **,**&#x200B;을(를) 입력한 다음 Enter 키를 누르고 다음 줄에 이 코드를 붙여넣습니다.

```json
{
  "id": "brandconcierge",
  "fields": []
}
```

**변경 내용 커밋...**&#x200B;을 클릭합니다.

![차단](./images/block13.png)

**변경 내용 커밋**&#x200B;을 클릭합니다.

![차단](./images/block13a.png)

#### component-filters.json

**component-filters.json** 파일이 표시될 때까지 아래로 스크롤한 다음 **연필** 아이콘을 클릭하여 파일 편집을 시작합니다.

![차단](./images/block14.png)

그럼 이걸 보셔야죠

![차단](./images/block14a.png)

**section**&#x200B;에서 쉼표 `,`을(를) 입력하고 현재 마지막 줄 뒤에 구성 요소 `"brandconcierge"`의 ID를 붙여 넣으십시오.

**변경 내용 커밋...**&#x200B;을 클릭합니다.

![차단](./images/block15.png)

**변경 내용 커밋**&#x200B;을 클릭합니다.

![차단](./images/block15a.png)

#### brandconcierge.css

블록을 만들 때는 블록 스타일을 위한 파일을 만드는 것이 가장 좋으며 블록 이름은 동일해야 합니다. 이제 해당 파일을 생성해야 하며, 이 파일은 현재 비어 있습니다.

**블록** 폴더로 이동합니다. 그런 다음 **파일 추가**&#x200B;를 클릭하고 **새 파일 만들기**&#x200B;를 선택합니다.

![차단](./images/css1.png)

텍스트 상자에 `brandconcierge/brandconcierge.css`을(를) 입력합니다. 파일은 현재 비어 있을 수 있습니다. **변경 내용 커밋...**&#x200B;을 클릭합니다.

![차단](./images/css2.png)

**변경 내용 커밋**&#x200B;을 클릭합니다.

![차단](./images/css3.png)

#### brandconcierge.js

블록을 생성할 때 블록과 관련된 Javascript용 파일을 생성하는 것이 가장 좋으며 블록의 이름은 동일해야 합니다.

**파일 추가**&#x200B;를 클릭하고 **새 파일 만들기**&#x200B;를 선택합니다.

![차단](./images/js1.png)

텍스트 상자에 `brandconcierge.js`을(를) 입력합니다. 파일은 현재 비어 있을 수 있습니다. **변경 내용 커밋...**&#x200B;을 클릭합니다.

```javascript
export default function decorate(block) {
  block.setAttribute('id', 'brand-concierge-mount');
}
```

![차단](./images/js2.png)

**변경 내용 커밋**&#x200B;을 클릭합니다.

![차단](./images/js3.png)

### 새 페이지 만들기 및 새 사용자 지정 블록 연결

[https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}(으)로 이동합니다. **프로그램**&#x200B;을 클릭하여 엽니다.

![AEMCS](./images/aemcs6.png)

그런 다음 **환경** 탭에서 세 점 **..**&#x200B;을(를) 클릭하고 **세부 정보 보기**&#x200B;를 클릭합니다.

![AEMCS](./images/aemcs9.png)

그러면 환경 세부 정보가 표시됩니다. **작성자** 환경의 URL을 클릭합니다.

>[!NOTE]
>
>환경이 최대 절전 모드일 수 있습니다. 이 경우 먼저 환경의 최대 절전 모드를 해제해야 합니다.

![AEMCS](./images/aemcs10.png)

그러면 AEM 작성자 환경이 표시됩니다. **사이트**(으)로 이동합니다.

![AEMCS](./images/block21.png)

**CitiSignal**(으)로 이동합니다. **만들기**&#x200B;를 클릭하고 **페이지**&#x200B;를 선택합니다.

![AEMCS](./images/block23.png)

**페이지**&#x200B;를 선택하고 **다음**&#x200B;을 클릭합니다.

![AEMCS](./images/block24.png)

다음 값을 입력합니다.

- 제목: **Brand Concierge**
- 이름: **brandconcierge**
- 페이지 제목: **Brand Concierge**

**만들기**&#x200B;를 클릭합니다.

![AEMCS](./images/block25.png)

**열기**&#x200B;를 선택합니다.

![AEMCS](./images/block22.png)

그럼 이걸 보셔야죠

![AEMCS](./images/block26.png)

빈 영역을 클릭하여 **섹션** 구성 요소를 선택합니다. 그런 다음 오른쪽 메뉴에서 더하기 **+** 아이콘을 클릭합니다.

![AEMCS](./images/block27.png)

그러면 사용 가능한 블록 목록에 사용자 지정 블록이 표시됩니다. 클릭하여 선택합니다.

![AEMCS](./images/block28.png)

그러면 이 페이지에 빈 블록이 추가되는 것이 보입니다. 이 블록은 다음 단계에서 추가할 javascript 라이브러리를 사용하여 동적으로 로드됩니다.

**게시**&#x200B;를 클릭합니다.

![AEMCS](./images/block29.png)

**게시**&#x200B;를 다시 클릭합니다.

![AEMCS](./images/block30.png)

이제 새 페이지가 게시되었으며, 다음 단계의 탐색 헤더에 추가할 수 있습니다.

### 탐색 헤더 파일 업데이트

AEM Sites 개요에서 **CitiSignal**(으)로 이동하여 **Header/nav** 파일의 확인란을 선택합니다. **편집**&#x200B;을 클릭합니다.

![AEMCS](./images/nav0.png)

미리 보기 화면에서 **텍스트** 필드를 선택한 다음 화면 오른쪽의 **텍스트** 필드를 클릭하여 편집합니다.

![AEMCS](./images/nav0a.png)

탐색 메뉴에서 `Brand Concierge` 텍스트를 사용하여 새 메뉴 옵션을 만듭니다. 그런 다음 **Brand Concierge** 텍스트를 선택하고 **링크** 아이콘을 클릭합니다.

![AEMCS](./images/nav1.png)

필드 **경로 또는 URL** `/content/CitiSignal/brandconcierge.html`에 대해 입력하고 필드 `Brand Concierge`제목&#x200B;**에 대해**&#x200B;을(를) 입력하십시오. **저장**&#x200B;을 클릭합니다.

![AEMCS](./images/nav3.png)

그럼 이걸 드셔보세요 **완료**&#x200B;를 클릭합니다.

![AEMCS](./images/nav4.png)

그럼 이걸 드셔보세요 **게시**&#x200B;를 클릭합니다.

![AEMCS](./images/nav4a.png)

**게시**&#x200B;를 다시 클릭합니다.

![AEMCS](./images/nav5.png)

이제 새 페이지가 메뉴에 추가됩니다.

## 1.4.2.2 Brand Concierge - GitHub를 표시하도록 웹 사이트 구성

AEM 작성 환경을 사용하여 콘텐츠를 업데이트한 후에는 이제 웹 사이트에 사용되는 GitHub 저장소의 일부 코드를 업데이트해야 합니다.

### Javascript 라이브러리

AEM CS/EDS에서 실행되는 웹 사이트에서 Brand Concierge을 구현하려면 다음 라이브러리가 필요합니다.

- [styleconfigurations.js](./assets/styleconfigurations.js)
- [alloy.js](./assets/alloy.js)
- [brandconciergemain.js](./assets/brandconciergemain.js)

3개의 파일을 모두 데스크톱에 다운로드합니다.

![Brand Concierge](./images/aem0.png)

AEM CS/EDS 웹 사이트의 GitHub 프로젝트로 이동합니다. **스크립트**(으)로 이동합니다.

![Brand Concierge](./images/aem1.png)

**파일 추가**&#x200B;를 클릭한 다음 **파일 업로드**&#x200B;를 선택합니다.

![Brand Concierge](./images/aem3.png)

**파일 선택**&#x200B;을 클릭합니다.

![Brand Concierge](./images/aem3a.png)

데스크톱에서 **styleConfigurations.js, alloy.js 및 brandconciergemain.js** 파일을 모두 선택하고 **열기**&#x200B;를 클릭합니다.

![Brand Concierge](./images/aem4.png)

**변경 내용 커밋**&#x200B;을 클릭합니다.

![Brand Concierge](./images/aem5.png)

### head.html 업데이트

이전 단계에서 3개의 새 라이브러리를 업로드했습니다. 이제 웹 사이트가 로드될 때 이러한 라이브러리를 로드해야 하며, 이렇게 하는 방법은 **head.html** 파일에 이러한 파일에 대한 참조를 추가하는 것입니다.

또한 **head.html** 파일에 지침을 제공하여 라이브러리가 올바른 순서로 로드되도록 해야 합니다.

이렇게 하려면 **코드**&#x200B;를 클릭하여 AEM CS/EDS 웹 사이트의 GitHub 프로젝트로 이동합니다.

![Brand Concierge](./images/aem6.png)

아래로 조금 스크롤하세요. **head.html** 파일을 엽니다.

![Brand Concierge](./images/aem7.png)

이 파일을 편집하려면 **연필** 아이콘을 클릭하십시오.

![Brand Concierge](./images/aem8.png)

그럼 이걸 보셔야죠

![Brand Concierge](./images/aem9.png)

43행까지 아래로 스크롤하여 다음을 붙여넣습니다.

아래 코드에는 업데이트해야 하는 2개의 필드가 있습니다.

>[!IMPORTANT]
>
>- **datastreamId**&#x200B;이(가) 현재 &quot;XXXXX&quot;로 설정되어 있으므로 이전 단계에서 만든 데이터스트림의 ID로 대체해야 합니다.
>- **orgId**&#x200B;은(는) Adobe Experience Cloud 인스턴스의 IMS 조직 ID로 대체해야 합니다.

```javascript
<script src="/scripts/styleconfigurations.js"></script>

<script>
		!function (n, o) {
      o.forEach(function (o) {
        n[o] || ((n.__alloyNS = n.__alloyNS ||
          []).push(o), n[o] = function () {
            var u = arguments; return new Promise(
              function (i, l) { n[o].q.push([i, l, u]) })
          }, n[o].q = [])
      })
    }
      (window, ["alloy"]);
	</script>


<script src="/scripts/alloy.js"></script>

<script>
	alloy("configure", {
		defaultConsent: "in",
        edgeDomain: "edge.adobedc.net",
        edgeBasePath: "ee",
        datastreamId: "XXXXX", // replace datastreamId
        orgId: "--aepImsOrgId--", // replace ims org Id
        debugEnabled: true,
        idMigrationEnabled: false,
        thirdPartyCookiesEnabled: false,
        prehidingStyle: ".personalization-container { opacity: 0 !important }",
    });

window["alloy"]("sendEvent", {
    conversation: {
        fetchConversationalExperience: true
    }
}).then(result => {
    console.log("Conversation experience fetched", result);
    window["alloy"]("bootstrapConversationalExperience", {
        selector: "#brand-concierge-mount",
        src: "/scripts/brandconciergemain.js",
        stylingConfigurations: window.styleConfiguration,
        stickySession: true // create a sticky session cookie with expiration
    })
});
</script>
```

**변경 커밋...**&#x200B;을 클릭합니다.

![Brand Concierge](./images/aem10.png)

**변경 커밋**&#x200B;을 클릭합니다.

![Brand Concierge](./images/aem11.png)

이제 웹 사이트에서 라이브러리를 로드하는 데 필요한 코드를 업데이트했습니다.

![Brand Concierge](./images/aem12.png)

## 1.4.2.3 구성 테스트

이제 GitHub 사용자 계정으로 XXX를 바꾼 후 `main--citisignal-aem-accs--XXX.aem.page` 또는 `main--citisignal-aem-accs--XXX.aem.live`(으)로 이동하여 웹 사이트에서 변경 사항을 테스트할 수 있습니다(이 예제의 경우 `woutervangeluwe`).

이 예에서 전체 URL은 다음과 같이 됩니다.
`https://main--citisignal-aem-accs--woutervangeluwe.aem.page` 및/또는 `https://main--citisignal-aem-accs--woutervangeluwe.aem.live`.

에셋을 먼저 게시해야 하므로 모든 에셋이 올바르게 표시되기까지 시간이 걸릴 수 있습니다.

그럼 이걸 보셔야죠 **Brand Concierge**&#x200B;을(를) 클릭합니다.

![Brand Concierge](./images/aem13.png)

그러면 프롬프트를 입력할 수 있는 이 Brand Concierge이 표시됩니다.

![Brand Concierge](./images/aem14.png)

[Brand Concierge](./brandconcierge.md){target="_blank"}(으)로 돌아가기

[모든 모듈로 돌아가기](./../../../overview.md){target="_blank"}