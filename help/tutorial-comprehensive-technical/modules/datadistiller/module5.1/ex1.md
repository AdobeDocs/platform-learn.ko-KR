---
title: Query Service - 사전 요구 사항
description: Query Service - 사전 요구 사항
kt: 5342
doc-type: tutorial
exl-id: b8a404d1-7796-46e3-b245-553acdc753ae
source-git-commit: d9d9a38c1e160950ae755e352a54667c8a7b30f7
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 5.1.1 사전 요구 사항

## PSQL 명령줄 유틸리티 설치

Adobe Experience Platform 설명서에 설명된 지침에 따라 psql 클라이언트를 설치합니다.
[PSQL 설치 안내서](https://experienceleague.adobe.com/docs/experience-platform/query/clients/psql.html)

PSQL을 설치한 후에는 터미널 창에서 아래 명령을 실행하여 **PATH**&#x200B;을(를) 업데이트해야 할 수 있습니다.

macOS의 경우(아래 명령의 XX를 설치한 PSQL의 버전 번호로 바꾸기):

`export PATH=/Library/PostgreSQL/XX/bin:$PATH`

## Power BI 설치

Windows 사용자에게만

[Microsoft Power BI 설치](https://experienceleague.adobe.com/docs/experience-platform/query/clients/power-bi.html)

문서에 언급된 대로 정확한 버전의 **npgsql**&#x200B;을(를) 설치하십시오. 그렇지 않으면 Adobe Experience Platform 쿼리 서비스에 Power BI을 연결할 수 없습니다.

## 타블로 설치

Windows 또는 Mac 사용자용

설명서에 따라 [Tableau Desktop 설치](https://experienceleague.adobe.com/docs/experience-platform/query/clients/tableau.html).

Tableau는 14일 평가판 사용 기간을 자동으로 제공합니다.

14일 이후에 Tableau를 사용하려면 라이선스 키가 필요합니다.

다음 단계: [5.1.2 시작](./ex2.md)

[모듈 5.1로 돌아가기](./query-service.md)

[모든 모듈로 돌아가기](../../../overview.md)
