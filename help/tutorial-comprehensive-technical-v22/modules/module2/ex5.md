---
title: 기초 - 데이터 수집 - 오프라인 소스에서 데이터 수집
description: 기초 - 데이터 수집 - 오프라인 소스에서 데이터 수집
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 93d9f4ef-9cbd-4310-879e-d69106b70404
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 2%

---

# 2.5 데이터 랜딩 영역

이 연습에서 목표는 Azure Blob 저장소를 사용하여 데이터 랜딩 영역 소스 커넥터를 설정하는 것입니다.

데이터 랜딩 존은 Adobe Experience Platform에서 제공하는 Azure Blob 저장소 인터페이스로, 파일을 플랫폼으로 가져오기 위해 안전한 클라우드 기반 파일 저장소 기능에 액세스할 수 있도록 해줍니다. 데이터 랜딩 존은 SAS 기반 인증을 지원하며, 데이터는 휴식과 전송 중에 표준 Azure Blob 저장 공간 보안 메커니즘으로 보호됩니다. SAS 기반 인증을 사용하면 공용 인터넷 연결을 통해 데이터 랜딩 영역 컨테이너에 안전하게 액세스할 수 있습니다.

>[!NOTE]
>
> Adobe Experience Platform **에서는 엄격한 7일 TTL(Time-to-Live)을 적용합니다** 데이터 랜딩 영역 컨테이너에 업로드된 모든 파일. 7일 후 모든 파일이 삭제됩니다.


## 2.5.1 사전 요구 사항

Blob 또는 파일을 Adobe Experience Platform 데이터 랜딩 영역에 복사하려면 명령줄 유틸리티인 AzCopy를 사용합니다. 를 통해 운영 체제의 버전을 다운로드할 수 있습니다 [https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

![dlz-install-az-copy.png](./images/dlz-install-az-copy.png)

- 다운로드 파일의 압축을 해제합니다

![dlz-install-az-copy.png](./images/dlz1.png)

- 샘플 데이터 파일 다운로드 [global-context-websiteinteractions.csv](../../assets/csv/data-ingestion/global-context-websiteinteractions.csv): 샘플 웹 사이트 상호 작용이 포함되어 있으며 압축을 푼 폴더에 저장합니다 **azcopy**.

![dlz-install-az-copy.png](./images/dlz2.png)

- 터미널 창을 열고 데스크탑의 폴더로 이동합니다. OSX와 같이 다음 컨텐츠(azcopy 및 global-context-websiteinteractions.csv)가 표시됩니다.

![dlz-unzip-azcopy.png](./images/dlz-unzip-azcopy.png)

## 2.5.2 Adobe Experience Platform에 데이터 랜딩 영역 연결

다음 URL로 이동하여 Adobe Experience Platform에 로그인합니다. [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

로그인하면 Adobe Experience Platform 홈 페이지가 표시됩니다.

![데이터 수집](./images/home.png)

계속하기 전에 **샌드박스**. 선택할 샌드박스의 이름은 다음과 같습니다 ``--module2sandbox--``. 이 작업은 텍스트를 클릭하여 수행할 수 있습니다 **[!UICONTROL 프로덕션 제품]** 화면 상단에 있는 파란색 줄에 표시됩니다. 적절한 샌드박스를 선택하면 화면 변경 사항이 표시되고 이제 전용 샌드박스에 있습니다.

![데이터 수집](./images/sb1.png)

왼쪽 메뉴에서 **소스**. 소스 카탈로그에서 **데이터 랜딩**. 설정 **데이터 랜딩 영역** 카드, **...** 을(를) 선택합니다. **자격 증명 보기**.

![dlz-view-credentials.png](./images/dlz-view-credentials.png)

Tp copy 클릭 **사수리**.

![dlz-copy-sas-uri.png](./images/dlz-copy-sas-uri.png)

## 2.5.3 AEP 데이터 랜딩 영역에 csv 파일 복사

이제 AZCopy를 사용하여 Azure 명령줄 도구를 사용하여 Adobe Experience Platform에 데이터를 수집합니다.

azcopy 설치 위치의 터미널을 열고 다음 명령을 실행하여 파일을 AEP의 데이터 랜딩 영역에 복사합니다.

``./azcopy copy <your-local-file> <your SASUri>``

SASUri를 큰따옴표로 묶어야 합니다. 바꾸기 `<your-local-file>` 파일의 로컬 복사본 경로 기준 **global-context-websiteinteractions.csv** azcopy 디렉토리에서 을(를) 바꾸고 `<your SASUri>` 기준 **사수리** Adobe Experience Platform UI에서 복사한 값입니다. 명령은 다음과 같아야 합니다.

```command
./azcopy copy global-context-websiteinteractions.csv "https://sndbxdtlnd2bimpjpzo14hp6.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-xxxxxxx-9843-4973-ae52-xxxxxxxx&sr=c&sp=racwdlm&sig=DN3kdhKzard%2BQwKASKg67Zxxxxxxxxxxxxxxxx"
```

터미널에서 위의 명령을 실행하면 다음과 같은 내용이 표시됩니다.

![dlz-exec-copy-command.png](./images/dlz-exec-copy-command.png)

## 2.5.4 데이터 랜딩 영역에서 파일 조회

Adobe Experience Platform의 데이터 랜딩 영역으로 이동합니다.

선택 **소스**, 검색 **데이터 랜딩** 을 클릭하고 **설정** 버튼을 클릭합니다.

![dlz-inspect-datalanding-zone.png](./images/dlz-inspect-datalanding-zone.png)

이렇게 하면 데이터 랜딩 영역이 열립니다. 방금 데이터 랜딩 영역의 **데이터 선택** 패널.

![dlz-datalending-zone-open.png](./images/dlz-datalanding-zone-open.png)

## 2.5.5 파일 처리

파일을 선택하고 을(를) 선택합니다 **구분 기호** 데이터 형식으로 사용하십시오. 그러면 데이터 미리 보기가 표시됩니다. **다음**&#x200B;을 클릭합니다.

![dlz-datalending-select-file.png](./images/dlz-datalanding-select-file.png)

이제 데이터 집합의 XDM 스키마와 일치하도록 업로드된 데이터 매핑을 시작할 수 있습니다.

선택 **기존 데이터 세트** 데이터 세트를 선택하고 **데모 시스템 - 웹 사이트의 이벤트 데이터 세트(글로벌 v1.1)**. **다음**&#x200B;을 클릭합니다.

![dlz-target-dataset.png](./images/dlz-target-dataset.png)

이제 csv 파일의 수신 소스 데이터를 데이터 세트의 XDM 스키마의 대상 필드에 매핑할 준비가 되었습니다.

![dlz-start-mapping.png](./images/dlz-start-mapping.png)

>[!NOTE]
>
> 매핑에 발생할 수 있는 오류를 신경쓰지 마십시오. 다음 단계에서 매핑을 수정합니다.

## 2.5.6 맵 필드

먼저 **모든 매핑 지우기** 버튼을 클릭합니다. 그런 다음 깨끗한 매핑으로 시작할 수 있습니다.

![dlz-clear-mappings.png](./images/mappings1.png)

다음을 클릭합니다. **새 필드 유형** 그런 다음 **새 필드 추가**.

![dlz-clear-mappings.png](./images/dlz-clear-mappings.png)

를 매핑하려면 **ecid** 소스 필드에서 필드를 선택합니다. **identid.ecid** 을(를) 클릭합니다. **선택**.

![dlz-map-identity.png](./images/dlz-map-identity.png)

다음을 클릭합니다. **대상 필드 매핑**.

![dlz-map-select-target-field.png](./images/dlz-map-select-target-field.png)

필드를 선택합니다 ``--aepTenantId--``스키마 구조의 .identification.core.ecid입니다.

![dlz-map-target-field.png](./images/dlz-map-target-field.png)

다른 필드 두 개를 매핑해야 하는 경우 **+ 새 필드 유형** 후 **새 필드 추가** 및 이 매핑에 대한 필드 추가

| 소스 | target |
|---|---|
| resource.info.pagename | web.webPageDetails.name |
| timestamp | timestamp |
| timestamp | _ID |

![dlz-add-other-mapping.png](./images/dlz-add-other-mapping.png)

화면이 완료되면 아래 화면이 표시됩니다. **다음**&#x200B;을 클릭합니다.

![dlz-mapping-result.png](./images/dlz-mapping-result.png)

**다음**&#x200B;을 클릭합니다.

![dlz-default-scheduling.png](./images/dlz-default-scheduling.png)

**마침을 클릭합니다**.

![dlz-import-finish.png](./images/dlz-import-finish.png)

## 2.5.7 모니터 데이터 흐름

데이터 흐름을 모니터링하려면 다음 위치로 이동하십시오. **소스**, **데이터 흐름** 데이터 흐름을 클릭합니다.

![dlz-monitor-dataflow.png](./images/dlz-monitor-dataflow.png)

데이터를 로드하는 데 2분 정도 걸릴 수 있으며, 성공하면 상태가 표시됩니다. **성공**:

![dlz-monitor-dataflow-result.png](./images/dlz-monitor-dataflow-result.png)

다음 단계: [요약 및 이점](./summary.md)

[모듈 2로 돌아가기](./data-ingestion.md)

[모든 모듈로 돌아가기](../../overview.md)
