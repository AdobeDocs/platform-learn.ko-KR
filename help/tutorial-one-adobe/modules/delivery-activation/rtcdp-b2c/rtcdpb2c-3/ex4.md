---
title: Real-Time CDP - 대상 구축 및 조치 - 대상을 S3 대상으로 전송
description: Real-Time CDP - 대상 구축 및 조치 - 대상을 S3 대상으로 전송
kt: 5342
doc-type: tutorial
exl-id: 4f858d5d-773e-4aee-949c-6031b7d5ca45
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 3%

---

# 2.3.4 조치 취하기: 대상자를 S3-destination으로 보내기

Adobe Experience Platform에는 Salesforce Marketing Cloud, Oracle Eloqua, Oracle Responsys 및 Adobe Campaign과 같은 이메일 마케팅 대상에 대상을 공유할 수도 있습니다.

FTP 또는 SFTP를 이러한 각 이메일 마케팅 대상에 대한 전용 대상의 일부로 사용하거나, AWS S3를 사용하여 Adobe Experience Platform과 이러한 이메일 마케팅 대상 간에 고객 목록을 교환할 수 있습니다.

이 모듈에서는 AWS S3 버킷을 사용하여 이러한 대상을 구성합니다.

## S3 버킷 만들기

[https://console.aws.amazon.com](https://console.aws.amazon.com)(으)로 이동하여 로그인합니다.

>[!NOTE]
>
>아직 AWS 계정이 없는 경우 개인 이메일 주소를 사용하여 새 AWS 계정을 만드십시오.

![ETL](./images/awshome.png)

로그인하면 **AWS 관리 콘솔**(으)로 리디렉션됩니다.

![ETL](./images/awsconsole.png)

검색 창에서 **s3**&#x200B;을(를) 검색합니다. 첫 번째 검색 결과를 클릭합니다. **S3 - 클라우드의 확장 가능한 저장소**.

![ETL](./images/awsconsoles3.png)

그러면 **Amazon S3** 홈 페이지가 표시됩니다. **버킷 만들기**&#x200B;를 클릭합니다.

![ETL](./images/s3home.png)

**버킷 만들기** 화면에서 `aepmodulertcdp--aepUserLdap--` 이름을 사용하십시오.

![ETL](./images/bucketname.png)

다른 모든 기본 설정은 그대로 둡니다. 아래로 스크롤하여 **버킷 만들기**&#x200B;를 클릭합니다.

![ETL](./images/createbucket.png)

그러면 버킷이 만들어지는 것이 보이고 Amazon S3 홈페이지로 리디렉션됩니다.

![ETL](./images/S3homeb.png)

## S3 버킷에 액세스할 수 있는 권한 설정

다음 단계는 S3 버킷에 대한 액세스를 설정하는 것입니다.

이렇게 하려면 [https://console.aws.amazon.com/iam/home](https://console.aws.amazon.com/iam/home)(으)로 이동하십시오.

AWS 리소스에 대한 액세스는 Amazon Identity and Access Management(IAM)에 의해 제어됩니다.

이제 이 페이지가 표시됩니다.

![ETL](./images/iam.png)

왼쪽 메뉴에서 **사용자**&#x200B;를 클릭합니다. 그러면 **사용자** 화면이 표시됩니다. **사용자 만들기**&#x200B;를 클릭합니다.

![ETL](./images/iammenu.png)

그런 다음 사용자를 구성합니다.

- 사용자 이름: `s3_--aepUserLdap--_rtcdp` 사용

**다음**&#x200B;을 클릭합니다.

![ETL](./images/configuser.png)

그러면 이 권한 화면이 표시됩니다. **직접 정책 첨부**&#x200B;를 클릭합니다.

![ETL](./images/perm1.png)

모든 관련 S3 정책을 보려면 검색어 **s3**&#x200B;을(를) 입력하십시오. **AmazonS3FullAccess** 정책을 선택하십시오. 아래로 스크롤하여 **다음**&#x200B;을 클릭합니다.

![ETL](./images/perm2.png)

구성을 검토합니다. **사용자 만들기**&#x200B;를 클릭합니다.

![ETL](./images/review.png)

그러면 이걸 보게 될 거야. **사용자 보기**&#x200B;를 클릭합니다.

![ETL](./images/review1.png)

**보안 자격 증명**&#x200B;을 클릭한 다음 **액세스 키 만들기**&#x200B;를 클릭합니다.

![ETL](./images/cred.png)

**AWS 외부에서 실행 중인 응용 프로그램**&#x200B;을 선택합니다. 아래로 스크롤하여 **다음**&#x200B;을 클릭합니다.

![ETL](./images/creda.png)

**액세스 키 만들기** 클릭

![ETL](./images/credb.png)

그러면 이걸 보게 될 거야. 비밀 액세스 키를 보려면 **표시**&#x200B;를 클릭하세요.

![ETL](./images/cred1.png)

**비밀 액세스 키**&#x200B;이(가) 표시됩니다.

>[!IMPORTANT]
>
>자격 증명을 컴퓨터의 텍스트 파일에 저장합니다.
>
> - 액세스 키 ID: ...
> - 비밀 액세스 키: ...
>
> **완료**&#x200B;를 클릭하면 자격 증명이 다시 표시되지 않습니다!

**완료**&#x200B;를 클릭합니다.

![ETL](./images/cred2.png)

이제 AWS S3 버킷을 성공적으로 만들었고 이 버킷에 액세스할 수 있는 권한이 있는 사용자를 만들었습니다.

## Adobe Experience Platform에서 대상 구성

[Adobe Experience Platform](https://experience.adobe.com/platform)(으)로 이동합니다. 로그인하면 Adobe Experience Platform 홈페이지에 접속하게 됩니다.

![데이터 수집](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

계속하려면 **샌드박스**&#x200B;를 선택해야 합니다. 선택할 샌드박스 이름이 ``--aepSandboxName--``입니다. 적절한 [!UICONTROL 샌드박스]를 선택하면 화면이 변경되고 이제 전용 [!UICONTROL 샌드박스]에 있게 됩니다.

![데이터 수집](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

왼쪽 메뉴에서 **대상**(으)로 이동한 다음 **카탈로그**(으)로 이동합니다. 그러면 **대상 카탈로그**&#x200B;가 표시됩니다.

![RTCDP](./images/rtcdpmenudest1.png)

**클라우드 저장소**&#x200B;를 클릭한 다음 **Amazon S3** 카드에서 **설정** 단추(또는 환경에 따라 **대상 활성화**&#x200B;에서)를 클릭합니다.

![RTCDP](./images/rtcdp2.png)

계정 유형으로 **액세스 키**&#x200B;을(를) 선택하십시오. 이전 단계에서 제공된 S3 자격 증명을 사용하십시오.

| 액세스 키 ID | 비밀 액세스 키 |
|:-----------------------:| :-----------------------:|
| AKIA..... | 7Icm..... |

**대상에 연결**&#x200B;을 클릭합니다.

![RTCDP](./images/rtcdpsfs3.png)

그러면 이 대상이 현재 연결되어 있다는 시각적 확인이 표시됩니다.

![RTCDP](./images/rtcdpsfs3connected.png)

Adobe Experience Platform이 S3 버킷에 연결할 수 있도록 S3 버킷 세부 사항을 제공해야 합니다.

명명 규칙으로는 다음을 사용하십시오.

| 액세스 키 ID | 비밀 액세스 키 |
|:-----------------------:| :-----------------------:|
| 이름 | `AWS - S3 - --aepUserLdap--` |
| 설명 | `AWS - S3 - --aepUserLdap--` |
| 버킷 이름 | `aepmodulertcdp--aepUserLdap--` |
| 폴더 경로 | /now |

**대상**&#x200B;을 선택하세요.

**파일 형식**&#x200B;에 대해 **CSV**&#x200B;을 선택하고 기본 설정을 변경하지 마십시오.

![RTCDP](./images/rtcdpsfs3connect2.png)

아래로 스크롤합니다. **압축 형식**&#x200B;에 대해 **없음**&#x200B;을 선택하세요. **다음**&#x200B;을 클릭합니다.

![RTCDP](./images/rtcdpsfs3connect3.png)

이제 선택적으로 새 대상에 데이터 거버넌스 정책을 첨부할 수 있습니다. **다음**&#x200B;을 클릭합니다.

![RTCDP](./images/rtcdpsfs3connect2gov.png)

대상 목록에서 이전 연습에서 만든 대상 `--aepUserLdap-- - Interest in Galaxy S24`을(를) 검색하여 선택합니다. **다음**&#x200B;을 클릭합니다.

![RTCDP](./images/s3a.png)

그러면 이걸 보게 될 거야. 원하는 경우 **연필** 아이콘을 클릭하여 일정 및 파일 이름을 편집할 수 있습니다. **다음**&#x200B;을 클릭합니다.

![RTCDP](./images/s3bb.png)

이제 AWS S3으로 내보내기 위해 프로필 속성을 선택할 수 있습니다. **새 필드 추가**&#x200B;를 클릭하고 `--aepTenantId--.identification.core.ecid` 필드가 추가되고 **중복 제거 키**(으)로 표시되는지 확인하십시오.

필요한 경우 다른 프로필 속성을 추가할 수 있습니다.

모든 필드를 추가한 후 **다음**&#x200B;을(를) 클릭합니다.

![RTCDP](./images/s3c.png)

구성을 검토합니다. 구성을 완료하려면 **마침**&#x200B;을 클릭하세요.

![RTCDP](./images/s3g.png)

그런 다음 대상 활성화 화면으로 돌아가면 대상자가 이 대상에 추가된 것을 볼 수 있습니다.

대상 내보내기를 더 추가하려면 **대상 활성화**&#x200B;를 클릭하여 프로세스를 다시 시작하고 대상을 더 추가할 수 있습니다.

![RTCDP](./images/s3j.png)

## 다음 단계

[2.3.5 실행으로 이동: 대상자를 Adobe Target으로 보내기](./ex5.md){target="_blank"}

[실시간 CDP로 돌아가기 - 대상자를 빌드하고 작업 수행](./real-time-cdp-build-a-segment-take-action.md){target="_blank"}

[모든 모듈](./../../../../overview.md){target="_blank"}(으)로 돌아가기
