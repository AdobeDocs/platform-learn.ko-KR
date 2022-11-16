---
title: 앱 다운로드를 추적하기 위한 데이터 요소 및 규칙 만들기
description: 앱 다운로드를 추적하기 위한 데이터 요소 및 규칙 만들기
feature: Web SDK
exl-id: 8012ba48-38ac-4fb5-9876-8f57d1c5da5d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 5%

---

# 앱 다운로드를 추적하기 위한 데이터 요소 및 규칙 만들기

미리 알림으로, 사용자가 [!UICONTROL 앱 다운로드] 링크를 누르면 다음과 같이 데이터 레이어로 푸시됩니다.

```js
window.adobeDataLayer.push({
  "event": "downloadAppClicked",
  "eventInfo": {
    "web": {
      "webInteraction": {
        "URL": "https://example.com/download",
        "name": "App Download",
        "type": "download"
      }
    }
  }
});
```

이(가) `eventInfo` 키: 데이터 계층에 이 데이터를 이벤트와 함께 전달하지만, _not_ 데이터 레이어 내에서 데이터를 유지합니다. 링크 클릭의 경우, 클릭하면 페이지에서 나중에 발생할 수 있는 다른 이벤트에는 적용할 수 없으므로 클릭한 링크에 대한 정보를 데이터 레이어에 추가하는 것은 유용하지 않습니다.

이 구현의 경우, (1) 데이터 레이어의 계산된 상태 및 (2) 의 컨텐츠가 포함된 경험 이벤트를 Adobe Experience Platform에 보낼 수 있습니다 `eventInfo`.

이렇게 하려면 이 두 청크를 병합하는 데이터 요소를 만들어야 합니다.

## 데이터 요소 만들기

적절한 데이터 요소를 만들려면:

1. 클릭 [!UICONTROL 데이터 요소] 왼쪽 메뉴에 있습니다.
1. 그런 다음 [!UICONTROL 새 데이터 요소 만들기] 링크를 클릭합니다.
1. 데이터 요소 이름을 입력합니다, `computedStateAndEventInfo`.
1. 대상 [!UICONTROL 확장] 필드, 선택 [!UICONTROL 코어] 아직 선택되지 않은 경우
1. 대상 [!UICONTROL 데이터 요소 유형] 필드, 선택 **[!UICONTROL 병합된 개체]**. 이 데이터 요소를 사용하면 여러 개체를 병합할 수 있습니다. 병합된 결과는 데이터 요소에 의해 반환됩니다.
1. 병합에 포함할 첫 번째 개체를 추가합니다. Enter 키 `%event.fullState%` 에서 [!UICONTROL 개체(필수)] 필드. 에 의해 트리거된 규칙 내에서 사용되는 경우 [!UICONTROL 푸시된 데이터] 규칙 이벤트에서 규칙이 트리거될 때 Adobe 클라이언트 데이터 레이어의 계산된 상태를 참조합니다.
1. 을(를) 클릭합니다.  **[!UICONTROL 다른 추가]** 명령.
1. 두 번째 개체를 추가합니다. Enter 키 `%event.eventInfo%` 에서 [!UICONTROL 개체(필수)] 필드. 에 의해 트리거된 규칙 내에서 사용되는 경우 [!UICONTROL 푸시된 데이터] 규칙 이벤트, 이 이벤트는 `eventInfo` Adobe 클라이언트 데이터 레이어에 푸시된 부분.
1. 를 클릭하여 데이터 요소를 저장합니다. [!UICONTROL 저장] 버튼을 클릭합니다.
   ![computedStateAndEventInfo 데이터 요소](../assets/computed-state-and-event-info-data-element.png)

데이터 요소가 완료되었습니다.

## 규칙 만들기

클릭 추적을 위한 규칙을 만들려면 [!UICONTROL 앱 다운로드] 링크:

1. 클릭 **[!UICONTROL 규칙]** 왼쪽 메뉴에 있습니다.
1. **[!UICONTROL 규칙 추가]**&#x200B;를 클릭합니다.
1. Enter 키 **_클릭한 앱 링크 다운로드_** 에서 [!UICONTROL 이름] 필드.

## 이벤트 추가

1. 을(를) 클릭합니다. **[!UICONTROL 추가]** 버튼 아래 [!UICONTROL 이벤트]. 이제 이벤트 보기에 표시됩니다.
1. 대상 [!UICONTROL 확장] 필드, 선택 **[!UICONTROL Adobe 클라이언트 데이터 레이어]**.
1. 대상 [!UICONTROL 이벤트 유형] 필드, 선택 **[!UICONTROL 푸시된 데이터]**.
1. **[!UICONTROL 변경사항 유지]**를 클릭합니다.
   ![클릭한 앱 이벤트 다운로드](../assets/download-app-clicked-event.png)
왜냐하면 `downloadAppClicked` 이벤트가 데이터 레이어에 푸시되면 **[!UICONTROL 특정 이벤트]** 무선 [!UICONTROL 다음 사항] 및 유형 **_downloadAppClicked_** 로 [!UICONTROL 등록할 이벤트/키]  표시되는 텍스트 필드입니다.

## 작업 추가

이제 규칙 보기로 돌아왔습니다.

1. **[!UICONTROL 작업]** 아래의 [!UICONTROL 추가] 버튼을 클릭합니다.
1. 이제 작업 보기에 있어야 합니다. 대상 [!UICONTROL 확장] 필드, 선택 **[!UICONTROL Adobe Experience Platform Web SDK]**. 대상 [!UICONTROL 작업 유형] 필드, 선택 **[!UICONTROL 이벤트 보내기]**.
1. 에서 [!UICONTROL 유형] 오른쪽에 있는 필드에서 `web.webinteraction.linkClicks`.
1. 대상 [!UICONTROL XDM 데이터] 필드에서 오른쪽의 데이터 요소 선택기 단추 를 클릭하고 를 선택합니다 **[!UICONTROL computedStateAndEventInfo]**. 최근 만든 데이터 요소입니다.
1. 이 규칙의 경우(만든 다른 규칙과 달리) **[!UICONTROL 문서가 언로드됨]** 확인란을 선택합니다.
   ![문서가 확인란을 언로드합니다.](../assets/document-will-unload.png)
1. 를 클릭하여 작업을 저장합니다 **[!UICONTROL 변경 내용 유지]** 버튼을 클릭합니다.

>[!TIP]
>
>다음 [!UICONTROL 문서가 기능을 언로드합니다.] 는 사용자가 링크를 클릭할 때 페이지에서 나가도록 SDK에 알려줍니다. 이것은 요청이 백그라운드에서 계속 실행되고 서버에 도달하기 때문에 사용자가 페이지에서 멀리 탐색하더라도 SDK에서 요청을 수행할 수 있도록 허용하므로 중요합니다. 이 확인란을 선택 취소하면 이 방식으로 요청이 수행되지 않으므로 현재 문서가 언로드될 때 취소될 수 있습니다.
>
>&quot;그거 좋겠네. 그러면 이 옵션이 항상 활성화되지 않는 이유는 무엇입니까?&quot;
>
>글쎄요, 좀 복잡하지만 이 기능을 사용할 때 SDK는 [`sendBeacon`](https://developer.mozilla.org/ko-KR/docs/Web/API/Navigator/sendBeacon) 요청을 전송하려면 을 사용하여 요청을 보낼 때 `sendBeacon`인 경우 브라우저에서는 SDK(또는 그 밖의 것)가 서버에서 반환된 데이터에 액세스할 수 없습니다. SDK가 모든 요청에 이 기능을 사용하는 경우 SDK가 서버에서 데이터를 수신할 수 없습니다. 이러한 이유로 다음을 확인하는 것이 중요합니다 [!UICONTROL 문서가 언로드됨] 현재 문서가 언로드될 때만 확인란을 선택합니다. 이 경우 응답 데이터를 삭제할 수 있습니다.

## 규칙을 저장합니다

이제 규칙이 완료되어야 합니다.

1. 클릭 **[!UICONTROL 저장]** 오른쪽 상단 모서리에서
   ![클릭한 앱 링크 다운로드 규칙](../assets/download-app-link-clicked-rule.png)

[다음: ](publish-the-library.md)

>[!NOTE]
>
>데이터 수집에 시간을 내어 주셔서 감사합니다. 질문이 있거나 일반 피드백을 공유하거나 향후 컨텐츠에 대한 제안 사항이 있는 경우 해당 정보를 공유하십시오 [Experience League 커뮤니티 토론 게시물](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)