---
title: 기초 - 데이터 수집 - 오프라인 소스에서 데이터 수집
description: 기초 - 데이터 수집 - 오프라인 소스에서 데이터 수집
kt: 5342
doc-type: tutorial
exl-id: 21b84a77-4115-4ba7-b847-b236aa14bbdd
source-git-commit: 2f53c8da2cbe833120fa6555c65b8b753bfa4f8d
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 2%

---

# 1.2.5 데이터 랜딩 영역

이 연습의 목표는 Azure Blob 저장소를 사용하여 데이터 랜딩 영역 Source 커넥터를 설정하는 것입니다.

데이터 랜딩 영역 은 Adobe Experience Platform에서 프로비저닝한 Azure Blob 스토리지 인터페이스로, 파일을 플랫폼으로 가져올 수 있는 안전한 클라우드 기반 파일 스토리지 시설에 액세스할 수 있습니다. 데이터 랜딩 영역 은 SAS 기반 인증을 지원하며 표준 Azure Blob 저장 공간 보안 메커니즘을 통해 데이터를 보호합니다. SAS 기반 인증을 사용하면 공용 인터넷 연결을 통해 데이터 랜딩 영역 컨테이너에 안전하게 액세스할 수 있습니다.

>[!NOTE]
>
> Adobe Experience Platform **데이터 랜딩 영역 컨테이너에 업로드된 모든 파일에 엄격한 7일 TTL(time-to-live)**&#x200B;을 적용합니다. 모든 파일은 7일 후에 삭제됩니다.


## 전제 조건

블롭이나 파일을 Adobe Experience Platform 데이터 랜딩 영역에 복사하려면 명령줄 유틸리티인 AzCopy를 사용합니다. [https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10)을(를) 통해 운영 체제용 버전을 다운로드하고 해당 페이지에서 아래로 스크롤하여 **AzCopy 휴대용 이진 파일을 다운로드**&#x200B;한 다음 OS에 적합한 버전을 선택할 수 있습니다.

![dlz-install-az-copy.png](./images/dlzinstallazcopy.png)

- 다운로드한 파일의 압축 풀기

![dlz-install-az-copy.png](./images/dlz1.png)

- 샘플 웹 사이트 상호 작용이 포함된 샘플 데이터 파일 [global-context-websiteinteractions.csv](./../../../assets/csv/data-ingestion/global-context-websiteinteractions.csv)을(를) 다운로드하여 **azcopy**&#x200B;의 압축을 푼 폴더에 저장합니다.

![dlz-install-az-copy.png](./images/dlz2.png)

- 터미널 창을 열고 데스크탑의 폴더로 이동하면 OSX와 같은 다음 콘텐츠(azcopy 및 global-context-websiteinteractions.csv)가 표시됩니다.

![dlz-unzip-azcopy.png](./images/dlzunzipazcopy.png)

## 1.2.5.2 Adobe Experience Platform에 데이터 랜딩 영역 연결

URL [https://experience.adobe.com/platform](https://experience.adobe.com/platform)로 이동하여 Adobe Experience Platform에 로그인합니다.

로그인하면 Adobe Experience Platform 홈페이지에 접속하게 됩니다.

![데이터 수집](./images/home.png)

계속하려면 **샌드박스**&#x200B;를 선택해야 합니다. 선택할 샌드박스 이름이 ``--aepSandboxName--``입니다.  적절한 샌드박스를 선택하면 화면이 변경되고 이제 전용 샌드박스에 있습니다.

![데이터 수집](./images/sb1.png)

왼쪽 메뉴에서 **소스**(으)로 이동합니다. 소스 카탈로그에서 **데이터 랜딩**&#x200B;을 검색합니다.

![데이터 수집](./images/sourcesdlz.png)

**데이터 랜딩 영역** 카드를 클릭하면 오른쪽 탭에 자격 증명이 표시됩니다.

![dlz-view-credentials.png](./images/dlzviewcredentials.png)

표시된 대로 아이콘을 클릭하여 **SASUri**&#x200B;를 복사합니다.

![dlz-copy-sas-uri.png](./images/dlzcopysasuri.png)

## AEP 데이터 랜딩 영역에 csv 파일 복사

이제 AZCopy를 사용하여 Azure 명령줄 도구를 사용하여 Adobe Experience Platform에 데이터를 수집합니다.

azcopy 설치 위치의 터미널을 열고 다음 명령을 실행하여 AEP의 데이터 랜딩 영역에 파일을 복사합니다.

``./azcopy copy <your-local-file> <your SASUri>``

큰 따옴표로 SASUri를 둘러싸야 합니다. `<your-local-file>`을(를) azcopy 디렉터리에서 **global-context-websiteinteractions.csv** 파일의 로컬 복사본 경로로 바꾸고, `<your SASUri>`을(를) Adobe Experience Platform UI에서 복사한 **SASUri** 값으로 바꿉니다. 명령은 다음과 같아야 합니다.

```command
./azcopy copy global-context-websiteinteractions.csv "https://sndbxdtlnd2bimpjpzo14hp6.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-xxxxxxx-9843-4973-ae52-xxxxxxxx&sr=c&sp=racwdlm&sig=DN3kdhKzard%2BQwKASKg67Zxxxxxxxxxxxxxxxx"
```

터미널에서 위의 명령을 실행하면 다음이 표시됩니다.

![dlz-exec-copy-command.png](./images/dlzexeccopycommand.png)

## 데이터 랜딩 구역에서 파일 조회

Adobe Experience Platform의 데이터 랜딩 영역으로 이동합니다.

**소스**&#x200B;를 선택하고 **데이터 랜딩**&#x200B;을 검색한 다음 **설정** 단추를 클릭합니다.

![dlz-inspect-datalanding-zone.png](./images/dlzinspectdatalandingzone.png)

이렇게 하면 데이터 랜딩 영역이 열립니다. 데이터 랜딩 영역의 **데이터 선택** 패널에 방금 업로드한 파일이 표시됩니다.

![dlz-datalanding-zone-open.png](./images/dlzdatalandingzoneopen.png)

## 파일 처리

파일을 선택하고 **구분**&#x200B;을(를) 데이터 형식으로 선택합니다. 그러면 데이터 미리보기가 표시됩니다. **다음**&#x200B;을 클릭합니다.

![dlz-datalanding-select-file.png](./images/dlzdatalandingselectfile.png)

이제 데이터 세트의 XDM 스키마와 일치하도록 업로드된 데이터 매핑을 시작할 수 있습니다.

**기존 데이터 세트**&#x200B;를 선택하고 데이터 세트 **데모 시스템 - 웹 사이트에 대한 이벤트 데이터 세트(전역 v1.1)**&#x200B;를 선택합니다. **다음**&#x200B;을 클릭합니다.

![dlz-target-dataset.png](./images/dlztargetdataset.png)

이제 csv 파일에서 들어오는 소스 데이터를 데이터 세트의 XDM 스키마에서 대상 필드에 매핑할 준비가 되었습니다.

![dlz-start-mapping.png](./images/dlzstartmapping.png)

>[!NOTE]
>
> 매핑의 잠재적 오류에 신경 쓰지 마십시오. 다음 단계에서 매핑을 수정합니다.

## 필드 매핑

먼저 **모든 매핑 지우기** 단추를 클릭합니다. 그런 다음 클린 매핑으로 시작할 수 있습니다.

![dlz-clear-mappings.png](./images/mappings1.png)

**새 필드 형식**&#x200B;을 클릭한 다음 **새 필드 추가**&#x200B;를 선택합니다.

![dlz-clear-mappings.png](./images/dlzclearmappings.png)

**ecid** 소스 필드를 매핑하려면 필드 **id.ecid**&#x200B;을(를) 선택하고 **선택**&#x200B;을(를) 클릭합니다.

![dlz-map-identity.png](./images/dlzmapidentity.png)

**대상 필드 매핑**&#x200B;을(를) 클릭합니다.

![dlz-map-select-target-field.png](./images/dlzmapselecttargetfield.png)

스키마 구조에서 필드 ``--aepTenantId--``.identification.core.ecid를 선택합니다.

![dlz-map-target-field.png](./images/dlzmaptargetfield.png)

두 개의 다른 필드를 매핑해야 합니다. **+ 새 필드 유형**, **새 필드 추가**&#x200B;를 차례로 클릭하고 이 매핑에 대한 필드를 추가하십시오.

| 소스 | 대상 |
|---|---|
| resource.info.pagename | web.webPageDetails.name |
| 타임스탬프 | 타임스탬프 |
| 타임스탬프 | _ID |

![dlz-add-other-mapping.png](./images/dlzaddothermapping.png)

화면을 완료하면 아래 화면과 같이 표시됩니다. **다음**&#x200B;을 클릭합니다.

![dlz-mapping-result.png](./images/dlzmappingresult.png)

**다음**&#x200B;을 클릭합니다.

![dlz-default-scheduling.png](./images/dlzdefaultscheduling.png)

**마침을 클릭합니다**.

![dlz-import-finish.png](./images/dlzimportfinish.png)

## 데이터 흐름 모니터링

데이터 흐름을 모니터링하려면 **원본**, **데이터 흐름**(으)로 이동하여 데이터 흐름을 클릭하세요.

![dlz-monitor-dataflow.png](./images/dlzmonitordataflow.png)

데이터를 로드하는 데 2분 정도 걸릴 수 있습니다. 성공하면 **성공** 상태가 표시됩니다.

![dlz-monitor-dataflow-result.png](./images/dlzmonitordataflowresult.png)

다음 단계: [요약 및 이점](./summary.md)

[모듈 1.2로 돌아가기](./data-ingestion.md)

[모든 모듈로 돌아가기](../../../overview.md)
