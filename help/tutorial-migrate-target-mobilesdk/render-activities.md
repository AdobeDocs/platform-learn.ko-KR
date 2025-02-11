---
title: Target 활동 렌더링 - Adobe Target에서 Adobe Journey Optimizer으로 마이그레이션 - Decisioning Mobile 확장
description: Adobe Target 구현을 at.js 2.x에서 Adobe Experience Platform Web SDK으로 마이그레이션하는 방법에 대해 알아봅니다. 주제에는 라이브러리 개요, 구현 차이점 및 기타 주목할 만한 설명선이 포함됩니다.
exl-id: 39569088-a254-4e64-9956-0c6e1a8ed2a5
source-git-commit: 314f0279ae445f970d78511d3e2907afb9307d67
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Target 활동 렌더링

일부 Target 구현에서는 지역 mbox(이제 &quot;범위&quot;라고 함)를 사용하여 양식 기반 경험 작성기를 사용하는 활동의 콘텐츠를 전달할 수 있습니다. at.js Target 구현에서 mbox를 사용하는 경우 다음을 수행해야 합니다.

* `getOffer()` 또는 `getOffers()`을(를) 사용하는 at.js 구현의 모든 참조를 동일한 Platform Web SDK 메서드로 업데이트합니다.
* 노출이 계산되도록 `propositionDisplay` 이벤트를 트리거하는 코드를 추가하십시오.

## 요청 시 콘텐츠 요청 및 적용

+++ Android 예

>[!BEGINTABS]

>[!TAB SDK 타깃팅]

```Java
// Mboxes for Target activities
final DecisionScope decisionScope1 = DecisionScope("myTargetMbox1");
final DecisionScope decisionScope2 = new DecisionScope("myTargetMbox2");
 
final List<DecisionScope> decisionScopes = new ArrayList<>();
decisionScopes.add(decisionScope1);
decisionScopes.add(decisionScope2);
 
// Prefetch the Target mboxes
Optimize.updatePropositions(decisionScopes,
                            new HashMap<String, Object>() {
                                {
                                    put("xdmKey", "xdmValue");
                                }
                            },
                            new HashMap<String, Object>() {
                                {
                                    put("dataKey", "dataValue");
                                }
                            },
                            new AdobeCallbackWithOptimizeError<Map<DecisionScope, OptimizeProposition>>() {
                                @Override
                                public void fail(AEPOptimizeError optimizeError) {
                                    // Log in case of error
                                    Log.d("Target Prefetch error", optimizeError.title);
                                }
 
                                @Override
                                public void call(Map<DecisionScope, OptimizeProposition> propositionsMap) {
                                    // Retrieve cached propositions if prefetch succeeds
                                    Optimize.getPropositions(scopes, new AdobeCallbackWithError<Map<DecisionScope, OptimizeProposition>>() {
                                        @Override
                                      public void fail(final AdobeError adobeError) {
                                              // handle error
                                        }
 
                                        @Override
                                        public void call(Map<DecisionScope, OptimizeProposition> propositionsMap) {
                                              if (propositionsMap != null && !propositionsMap.isEmpty()) {
                                                // get the propositions for the given decision scopes
                                                if (propositionsMap.contains(decisionScope1)) {
                                                      final OptimizeProposition proposition1 = propsMap.get(decisionScope1)
                                                      // read proposition1 offers and display them
                                                }
                                                if (propositionsMap.contains(decisionScope2)) {
                                                      final OptimizeProposition proposition2 = propsMap.get(decisionScope2)
                                                      // read proposition2 offers and display them
                                                }
                                              }
                                        }
                                      });
                                }
                            });
```

>[!ENDTABS]

+++

+++ iOS 예

>[!BEGINTABS]

>[!TAB SDK 타깃팅]

```Swift
// Mboxes for Target activities
let decisionScope1 = DecisionScope(name: "myTargetMbox1")
let decisionScope2 = DecisionScope(name: "myTargetMbox2")
 
// Prefetch the Target mboxes
Optimize.updatePropositions(for: [decisionScope1, decisionScope2]
                            withXdm: ["xdmKey": "xdmValue"]
                            andData: ["dataKey": "dataValue"]) { data, error in
            if let error = error as? AEPOptimizeError {
                // handle error
                return
            }
            // Retrieve cached propositions if prefetch succeeds
            Optimize.getPropositions(for: [decisionScope1, decisionScope2]) { propositionsDict, error in
                if let error = error {
                    // handle error
                    return
                }
 
                if let propositionsDict = propositionsDict {
                    // get the propositions for the given decision scopes
 
                    if let proposition1 = propositionsDict[decisionScope1] {
                        // read proposition1 offers and display them
                    }
 
                    if let proposition2 = propositionsDict[decisionScope2] {
                        // read proposition2 offers and display them
                    }
                }
            }
        }
```

>[!ENDTABS]

+++


Target의 양식 기반 작성기를 사용하여 만들어 지역 mbox에 전달된 활동은 Platform Web SDK에서 자동으로 렌더링할 수 없습니다. at.js와 유사하게, 특정 Target 위치에 전달된 오퍼는 요청 시 렌더링해야 합니다.



다음으로 Platform Web SDK을 사용하여 [Target 매개 변수를 전달](send-parameters.md)하는 방법에 대해 알아봅니다.

>[!NOTE]
>
>Target 확장에서 Decisioning 확장으로 모바일 Target을 성공적으로 마이그레이션할 수 있도록 지원하기 위해 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)에 게시하여 알려 주십시오.
