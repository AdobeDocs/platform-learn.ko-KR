---
title: 유효성 검사 보고서 세트 만들기
description: 이전 구현에서 사이트를 로 마이그레이션할 때 웹 SDK 데이터의 유효성을 검사하는 데 사용할 수 있는 Adobe Analytics에서 보고서 세트를 만듭니다.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16756
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# 유효성 검사 보고서 세트 만들기

이전 구현에서 사이트를 로 마이그레이션할 때 웹 SDK 데이터의 유효성을 검사하는 데 사용할 수 있는 Adobe Analytics에서 보고서 세트를 만듭니다.

Analytics 구현의 크기와 복잡성에 따라 웹 SDK으로 마이그레이션하는 데 시간이 걸릴 수 있습니다. 이 시간 동안에는 데이터가 Adobe Analytics 보고서에 올바르게 유입되는지 확인하여 작업의 유효성을 검사해야 합니다. 프로덕션 데이터나 다른 개발 데이터와 함께 해당 데이터를 보고서 세트에 푸시하지 않고, 이 마이그레이션에 사용할 수 있는 새로운 보고서 세트를 만드는 것이 좋습니다. 다음 단원에서는 개발, 스테이징 및 프로덕션을 위한 새 &quot;데이터스트림&quot;을 만들고 구성하는 작업을 수행합니다. 이렇게 하면 구성에 대한 보고서 세트 ID를 알고 있어야 합니다.

## 새 보고서 세트 만들기

1. Adobe Analytics을 열고 Admin Console의 **보고서 세트** 설정으로 이동합니다.

   ![Admin Console](assets/aa-admin-console.jpg).

1. **[!UICONTROL 보고서 세트 추가]** 선택

   ![보고서 세트 추가](assets/add-report-suite.jpg)

1. 새 보고서 세트를 만들려면 양식을 작성하십시오. 템플릿에서 새 보고서 세트를 만들도록 선택할 수 있지만 빈 템플릿이라도 **기존 보고서 세트 복제** 옵션을 선택하고 Web SDK으로 마이그레이션할 보고서 세트를 선택하는 것이 더 나을 수 있습니다. 이렇게 하면 새로 마이그레이션된 데이터를 테스트할 때와 동일한 이름 및 설정을 가질 수 있으므로 진행할 때 보다 쉽게 확인할 수 있습니다. 모든 필수 필드를 작성하고 새 마이그레이션 개발 보고서 세트를 저장합니다.

   ![새 마이그레이션 개발 보고서 세트](assets/new-websdk-validation-report-suite.jpg)

1. 웹 SDK 구현을 위한 데이터스트림을 설정할 때 다음 단원에서 필요하므로 새 보고서 세트의 ID를 기록해 두십시오. 사이트 제목은 Analysis Workspace에서 사용하여 Analytics 프로젝트에서 마이그레이션 개발 보고서 세트를 선택할 수 있으므로 기억하기 좋습니다.

>[!TIP]
>
>보고서 세트 만들기에 대한 비디오 설명은 [보고서 세트 이해 및 만들기](https://experienceleague.adobe.com/en/docs/analytics-learn/tutorials/intro-to-analytics/analytics-basics/understanding-and-creating-report-suites){target="_blank"}를 참조하십시오.

