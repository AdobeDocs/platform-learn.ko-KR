---
title: Microsoft Azure 이벤트 허브에 세그먼트 활성화 - Azure에서 이벤트 허브 설정
description: Microsoft Azure 이벤트 허브에 세그먼트 활성화 - Azure에서 이벤트 허브 설정
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 9434ac83-5554-48bf-838c-7346d571efbf
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 1%

---

# 13.1 Microsoft Azure EventHub 환경 구성

Azure 이벤트 허브는 초당 수백만 개의 이벤트를 수집하여 여러 응용 프로그램으로 스트리밍할 수 있는 확장성이 뛰어난 게시 구독 서비스입니다. 이렇게 하면 연결된 장치 및 애플리케이션에서 생성된 대량의 데이터를 처리하고 분석할 수 있습니다.

## 13.1.1 Azure 이벤트 허브란?

Azure 이벤트 허브는 빅데이터 스트리밍 플랫폼 및 이벤트 수집 서비스입니다. 초당 수백만 개의 이벤트를 받고 처리할 수 있습니다. 이벤트 허브로 전송된 데이터는 모든 실시간 분석 공급자나 일괄 처리/저장소 어댑터를 사용하여 변환하고 저장할 수 있습니다.

이벤트 허브는 **전면 도어** 이벤트 파이프라인의 경우 을 솔루션 아키텍처에서 이벤트 수집이라고 합니다. 이벤트 수집기는 이벤트 게시자(Adobe Experience Platform RTCDP 등)와 이벤트 소비자 사이에 존재하며 이러한 이벤트를 소비하여 이벤트 스트림의 생성을 구분하기 위한 구성 요소 또는 서비스입니다. 이벤트 허브는 시간 보존 버퍼가 있는 통합 스트리밍 플랫폼을 제공하여 이벤트 소비자로부터 이벤트 생성자를 분리합니다.

## 13.1.2 이벤트 허브 네임스페이스 만들기

이동 [https://portal.azure.com/#home](https://portal.azure.com/#home) 을(를) 선택합니다. **리소스 만들기**.

![1-01-open-azure-portal.png](./images/1-01-open-azure-portal.png)

리소스 화면에서 를 입력합니다. **이벤트** 검색 막대에서 을(를) 선택하고 을(를) 선택합니다. **이벤트 허브** 드롭다운에서 다음을 수행합니다.

![1-02-search-event-hubs.png](./images/1-02-search-event-hubs.png)

Click **Create**:

![1-03-event-hub-create.png](./images/1-03-event-hub-create.png)

Azure에서 리소스를 처음 만드는 경우 새 리소스를 만들어야 합니다 **리소스 그룹**. 이미 리소스 그룹이 있는 경우 해당 그룹을 선택하거나 새 그룹을 만들 수 있습니다.

선택 **새로 만들기**, 그룹에 이름 지정 `--demoProfileLdap---aep-enablement`.

![1-04-create-resource-group.png](./images/1-04-create-resource-group.png)

표시된 대로 필드 테스트를 완료합니다.

- 네임스페이스 : 고유한 네임스페이스를 정의하고 다음 패턴을 사용합니다 `--demoProfileLdap---aep-enablement`
- 위치: **서유럽** 암스테르담의 Azure 데이터 센터를 참조합니다.
- 가격 책정 계층: **기본**
- 처리량 단위: **1**

![1-05-create-namespace.png](./images/1-05-create-namespace.png)

클릭 **검토 + 만들기**.

![1-06-namespace-review-create.png](./images/1-06-namespace-review-create.png)

**만들기**&#x200B;를 클릭합니다.

![1-07-namespace-create.png](./images/1-07-namespace-create.png)

리소스 그룹 배포에 성공하면 다음 화면이 표시됩니다. 1~2분 정도 걸릴 수 있습니다.

![1-08-namespace-deploy.png](./images/1-08-namespace-deploy.png)

## 13.1.3 Azure에서 이벤트 허브 설정

이동 [https://portal.azure.com/#home](https://portal.azure.com/#home) 을(를) 선택합니다. **모든 리소스**.

![1-09-all-resources.png](./images/1-09-all-resources.png)

리소스 목록에서 `--demoProfileLdap---aep-enablement` namespace:

![1-10-list-resources.png](./images/1-10-list-resources.png)

in `--demoProfileLdap---aep-enablement` 세부 정보 화면, 선택 **이벤트 허브**:

![1-11-eventhub-namespace.png](./images/1-11-eventhub-namespace.png)

클릭 **+ 이벤트 허브**.

![1-12-add-event-hub.png](./images/1-12-add-event-hub.png)

사용 `--demoProfileLdap---aep-enablement-event-hub` 를 이름으로 지정하고 을(를) 클릭합니다. **만들기**.

![1-13-create-event-hub.png](./images/1-13-create-event-hub.png)

클릭 **이벤트 허브** 를 이벤트 허브 네임스페이스에 추가합니다. 이제 다음을 볼 수 있습니다 **이벤트 허브** 나열됨. 그런 경우라면 다음 연습으로 넘어가십시오.

![1-14-event-hub-list.png](./images/1-14-event-hub-list.png)

## 13.1.4 Azure 저장소 계정 설정

나중에 연습에서 Azure 이벤트 허브 기능을 디버깅하려면 Visual Studio 코드 프로젝트 설정의 일부로 Azure 저장소 계정을 제공해야 합니다. 이제 해당 Azure 저장소 계정을 만듭니다.

이동 [https://portal.azure.com/#home](https://portal.azure.com/#home) 을(를) 선택합니다. **리소스 만들기**.

![1-15-event-hub-storage.png](./images/1-15-event-hub-storage.png)

Enter 키 **저장소** 검색에서 을(를) 선택하고 을(를) 선택합니다. **저장소 계정** 참조하십시오.

![1-16-event-hub-search-storage.png](./images/1-16-event-hub-search-storage.png)

**만들기**&#x200B;를 선택합니다.

![1-17-event-hub-create-storage.png](./images/1-17-event-hub-create-storage.png)

을(를) 지정합니다 **리소스 그룹** (이 연습의 시작 부분에서 만들어짐) `--demoProfileLdap--aepstorage` 저장소 계정 이름으로 사용하고 을 선택합니다. **LRS(로컬 중복 스토리지)**&#x200B;를 클릭한 다음 **검토 + 만들기**.

![1-18-event-hub-create-review-storage.png](./images/1-18-event-hub-create-review-storage.png)

**만들기**&#x200B;를 클릭합니다.

![1-19-event-hub-submit-storage.png](./images/1-19-event-hub-submit-storage.png)

스토리지 계정을 만드는 데 2초 정도 걸립니다.

![1-20-event-hub-deploy-storage.png](./images/1-20-event-hub-deploy-storage.png)

완료되면 화면이 표시됩니다 **리소스로 이동** 버튼을 클릭합니다.

클릭 **Microsoft Azure**.

![1-21-event-hub-deploy-ready-storage.png](./images/1-21-event-hub-deploy-ready-storage.png)

이제 스토리지 계정이 **최근 리소스**.

![1-22-event-hub-deploy-resources-list.png](./images/1-22-event-hub-deploy-resources-list.png)

다음 단계: [13.2 Adobe Experience Platform에서 Azure 이벤트 허브 대상 구성](./ex2.md)

[모듈 13으로 돌아가기](./segment-activation-microsoft-azure-eventhub.md)

[모든 모듈로 돌아가기](./../../overview.md)
