---
title: Target 활동 검색 - 모바일 앱의 Adobe Target 구현을 Adobe Journey Optimizer - Decisioning 확장으로 마이그레이션합니다.
description: Adobe Target에서 Adobe Journey Optimizer - Decisioning Mobile 확장 기능으로 마이그레이션할 때 Adobe Target 활동을 검색하는 방법을 알아봅니다.
exl-id: 39569088-a254-4e64-9956-0c6e1a8ed2a5
source-git-commit: b8baa6d48b9a99d2d32fad2221413b7c10937191
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# Target 활동 검색

Target 모바일 구현은 지역 mbox(이제 &quot;범위&quot;라고 함)를 사용하여 Target의 양식 기반 경험 작성기를 사용하는 활동의 콘텐츠를 전달합니다. 네트워크 호출에 범위를 포함하도록 모바일 애플리케이션을 업데이트해야 합니다.

Target에서 반환하는 콘텐츠(&quot;오퍼&quot;라고도 함)는 일반적으로 최종 고객 경험을 렌더링하기 위해 애플리케이션에서 소비해야 하는 텍스트 또는 JSON으로 구성됩니다. Target의 오퍼를 사용하여 다음을 수행할 수 있습니다.

* 애플리케이션에서 기능 플래그 활성화
* 대체 텍스트 또는 이미지 제공

애플리케이션의 Target 확장 및 Decisioning 확장 버전 모두에서 실행해야 하는 활동이 있는 경우 철저하게 테스트하십시오. 앱의 다른 버전에 대해 서로 다른 오퍼를 사용해야 하는 경우 인터페이스의 타깃팅 옵션을 사용하여 다른 버전에 다른 오퍼를 전달하는 것이 좋습니다.

항상 오류 조건에 적합한 경험을 표시하기 위해 오류 처리를 포함해야 합니다.


## 요청 시 콘텐츠 요청 및 적용

+++ Android 예

>[!BEGINTABS]

>[!TAB SDK 최적화]

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

>[!TAB SDK 최적화]

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



다음으로 [Decisioning 확장을 사용하여 Target 매개 변수를 전달](send-parameters.md)하는 방법을 알아봅니다.

>[!NOTE]
>
>Target 확장에서 Decisioning 확장으로 모바일 Target을 성공적으로 마이그레이션할 수 있도록 지원하기 위해 최선을 다하고 있습니다. 마이그레이션에 문제가 발생하거나 이 안내서에 중요한 정보가 누락된 것 같은 느낌이 드는 경우 [이 커뮤니티 토론](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)에 게시하여 알려 주십시오.
