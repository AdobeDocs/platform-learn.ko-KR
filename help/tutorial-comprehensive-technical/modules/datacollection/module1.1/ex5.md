---
title: 기초 - Adobe Experience Platform 데이터 수집 및 Web SDK 확장 설정 - Adobe Analytics 및 Adobe Audience Manager 구현
description: 기초 - Adobe Experience Platform 데이터 수집 및 Web SDK 확장 설정 - Adobe Analytics 및 Adobe Audience Manager 구현
kt: 5342
doc-type: tutorial
exl-id: a9022269-6db2-46c6-a82b-ec8d5b881a55
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# 1.1.5 - Adobe Analytics 및 Adobe Audience Manager 구현

## 컨텍스트

이제 XDM 데이터가 플랫폼으로 유입되는 것을 알 수 있습니다. [모듈 1.2](./../module1.2/data-ingestion.md)에 있는 XDM과 사용자 지정 변수를 추적하기 위해 고유한 스키마를 구축하는 방법에 대해 자세히 살펴봅니다. 이제 데이터를 Analytics 및 Audience Manager에 전달하도록 데이터 스트림을 설정할 때 어떻게 되는지 살펴보겠습니다.

## 1.1.5.1 Analytics의 매핑 변수

Adobe Experience Platform [!DNL Web SDK]은(는) 특정 값을 자동으로 매핑하므로 가능한 한 빨리 웹 SDK를 통해 Analytics를 새로 구현할 수 있습니다. 자동으로 매핑된 변수는 [여기](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html#data-collection)에 나열됩니다.

Adobe Analytics에 자동으로 매핑되지 않는 XDM 데이터의 경우 [컨텍스트 데이터](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=ko-KR)를 사용하여 [스키마](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=ko-KR)를 일치시킬 수 있습니다. 그런 다음 [처리 규칙](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html)을 사용하여 Analytics에 매핑하여 Analytics 변수를 채울 수 있습니다. 컨텍스트 데이터 및 처리 규칙 은 과거에 Analytics에서 작업한 사용자에게 익숙한 개념이지만 새로운 개념인 경우 지금은 세부 정보에 대해 걱정하지 마십시오.

또한 기본 작업 세트 및 제품 목록을 사용하여 AEP 웹 SDK로 데이터를 전송하거나 검색할 수 있습니다. 이렇게 하려면 [제품](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html?lang=en#data-collection)을 참조하세요.

### 컨텍스트 데이터

Analytics에서 사용하기 위해 XDM 데이터는 점 표기법을 사용하여 변환되고 `contextData`(으)로 사용할 수 있습니다. 다음 값 쌍 목록은 `context data`의 예를 보여 줍니다.

```javascript
{
    "bh": "900",
    "bw": "1680",
    "c": "24",
    "c.a.d.key.[0]": "value1",
    "c.a.d.key.[1]": "value2",
    "c.a.d.object.key1": "value1",
    "c.a.d.object.key2.[0]": "value2",
    "c.a.x.environment.browserdetails.javascriptenabled": "true",
    "c.a.x.environment.type": "browser",
    "cust_hit_time_gmt": "1579781427",
    "g": "http://example.com/home",
    "gn": "home",
    "j": "1.8.5",
    "k": "Y",
    "s": "1680x1050",
    "tnta": "218287:1:0|0,218287:1:0|2,218287:1:0|1,218287:1:0|32767,218287:1:01,218287:1:0|0,218287:1:0|1,218287:1:0|0,218287:1:0|1",
    "user_agent": "Mozilla/5.0 AppleWebKit/537.36 Safari/537.36",
    "v": "Y"
}
```

### 처리 규칙

에지 네트워크에서 수집한 모든 데이터는 [처리 규칙](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html)을 통해 액세스할 수 있습니다. Analytics에서는 처리 규칙을 사용하여 컨텍스트 데이터를 Analytics 변수에 통합할 수 있습니다.

## Experience Platform Edge Network의 1.1.5.2 Audience Manager

서버측 전달은 Audience Manager에 대한 새로운 개념이 아니며 이전과 동일한 프로세스가 적용됩니다. ID를 동기화할 수도 있습니다.

## 1.1.5.3 데이터스트림을 검토하여 Adobe Analytics으로 데이터를 전송합니다

Web SDK에서 수집한 데이터를 Adobe Analytics 및 Adobe Audience Manager으로 전송하려면 다음 단계를 따르십시오.

[https://experience.adobe.com/launch/](https://experience.adobe.com/launch/)(으)로 이동한 다음 **데이터스트림**(으)로 이동합니다.

화면 오른쪽 상단에서 샌드박스 이름을 선택합니다. 이름은 `--aepSandboxName--`이어야 합니다. 이름이 `--aepUserLdap-- - Demo System Datastream`인 특정 데이터 스트림을 엽니다.

![왼쪽 탐색에서 Edge 구성 아이콘을 클릭합니다](./images/edgeconfig1b.png)

그러면 이걸 보게 될 거야. Adobe Analytics을 사용하려면 **+서비스 추가**&#x200B;를 클릭하세요.

![AEP 디버거](./images/aa2.png)

그러면 이걸 보게 될 거야. 서비스 **Adobe Analytics**&#x200B;을(를) 선택한 후 데이터를 보낼 Adobe Analytics의 보고서 세트를 추가해야 합니다. 이 자습서에서는 범위를 벗어납니다. **취소**&#x200B;를 클릭합니다.

![AEP 디버거](./images/aa3.png)

## 1.1.5.4 데이터스트림을 검토하여 Adobe Audience Manager으로 데이터를 전송합니다

그러면 이걸 보게 될 거야. Adobe Audience Manager을 사용하려면 **+서비스 추가**&#x200B;를 클릭하세요.

![AEP 디버거](./images/aa2.png)

그러면 이걸 보게 될 거야. **Adobe Audience Manager** 서비스를 선택하면 그 이후에 Adobe Audience Manager 쿠키 대상 및/또는 URL 대상을 활성화하거나 비활성화할 수 있습니다. 이 자습서에서는 이 구성이 범위를 벗어납니다. **취소**&#x200B;를 클릭합니다.

![AEP 디버거](./images/aam1.png)

다음 단계: [1.1.6 Adobe Target 구현](./ex6.md)

[모듈 1.1로 돌아가기](./data-ingestion-launch-web-sdk.md)

[모든 모듈로 돌아가기](./../../../overview.md)
