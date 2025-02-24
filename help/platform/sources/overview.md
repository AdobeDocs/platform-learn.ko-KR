---
title: 소스 개요
description: Adobe, 자사 및 서드파티 애플리케이션의 데이터를 Platform의 실시간 고객 프로필 및 데이터 레이크로 손쉽게 수집하는 방법에 대해 알아봅니다.
feature: Sources
role: Data Engineer, Data Architect, Developer
level: Beginner
jira: KT-3800
thumbnail: 29694.jpg
exl-id: e38d643a-27ea-49f4-87c4-eccdb860ea92
source-git-commit: 112e092df6d486d8b9103013bec57d820b8ae6d7
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 10%

---

# 소스 개요

Adobe Experience Platform 인터페이스에서 소스 또는 소스 커넥터를 사용하는 방법을 알아봅니다. 소스는 간편하게 구성 가능한 통합 기능으로, 이를 통해 Adobe, 자사 및 서드파티 애플리케이션에서 플랫폼의 실시간 고객 프로필 및 데이터 레이크로 데이터를 수집할 수 있습니다. 자세한 내용은 [소스 설명서](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=ko)를 참조하세요.

>[!VIDEO](https://video.tv.adobe.com/v/29694?learn=on&enablevpops)

<!--should have a whole section for data prep-->

## 일반적인 유형의 서드파티 Adobe 소스에서 데이터 수집

<!-- CARDS
* ingest-data-from-crm.md
* ingest-data-from-cloud-storage.md
* ingest-data-from-databases.md
* streaming-ingestion-source-connector.md
* streaming-ingestion-http-api.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Ingest Data using CRM Source Connectors">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="ingest-data-from-crm.md" title="CRM Source 커넥터를 사용하여 데이터 수집" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/29711?format=jpeg&nocache=1740415500926" alt="CRM Source 커넥터를 사용하여 데이터 수집"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="ingest-data-from-crm.md" target="_blank" rel="referrer" title="CRM Source 커넥터를 사용하여 데이터 수집">CRM Source 커넥터를 사용하여 데이터 수집</a>
                    </p>
                    <p class="is-size-6">CRM 소스의 데이터를 Adobe Experience Platform의 실시간 고객 프로필 및 데이터 레이크로 손쉽게 일괄 수집하는 방법을 알아봅니다.</p>
                </div>
                <a href="ingest-data-from-crm.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Ingest Data using Cloud Storage Source Connectors">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="ingest-data-from-cloud-storage.md" title="클라우드 스토리지 Source 커넥터를 사용하여 데이터 수집" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/29695?format=jpeg&nocache=1740415500914" alt="클라우드 스토리지 Source 커넥터를 사용하여 데이터 수집"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="ingest-data-from-cloud-storage.md" target="_blank" rel="referrer" title="클라우드 스토리지 Source 커넥터를 사용하여 데이터 수집">클라우드 저장소 Source 커넥터를 사용하여 데이터 수집</a>
                    </p>
                    <p class="is-size-6">이 비디오는 원활하고 확장 가능한 방식으로 클라우드 스토리지 서비스의 데이터를 Adobe Experience Platform의 실시간 고객 프로필 및 데이터 레이크로 손쉽게 일괄 수집하는 방법을 보여 줍니다.</p>
                </div>
                <a href="ingest-data-from-cloud-storage.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Ingest data using a database source connector">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="ingest-data-from-databases.md" title="데이터베이스 소스 커넥터를 사용하여 데이터 수집" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/329317?format=jpeg&nocache=1740415500936" alt="데이터베이스 소스 커넥터를 사용하여 데이터 수집"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="ingest-data-from-databases.md" target="_blank" rel="referrer" title="데이터베이스 소스 커넥터를 사용하여 데이터 수집">데이터베이스 원본 커넥터를 사용하여 데이터 수집</a>
                    </p>
                    <p class="is-size-6">이 비디오는 원활하고 확장 가능한 방식으로 데이터베이스 소스의 데이터를 Adobe Experience Platform의 실시간 고객 프로필 및 Experience 데이터 레이크로 일괄 수집하는 방법을 안내합니다.</p>
                </div>
                <a href="ingest-data-from-databases.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Stream data using Source Connectors">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="streaming-ingestion-source-connector.md" title="Source 커넥터를 사용하여 데이터 스트리밍" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/331943?format=jpeg&nocache=1740415500903" alt="Source 커넥터를 사용하여 데이터 스트리밍"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="streaming-ingestion-source-connector.md" target="_blank" rel="referrer" title="Source 커넥터를 사용하여 데이터 스트리밍">소스 커넥터를 사용하여 데이터 스트리밍</a>
                    </p>
                    <p class="is-size-6">실시간으로 클라우드 스토리지 소스의 데이터를 플랫폼으로 스트리밍하고 고객 참여를 위해 데이터를 실시간으로 사용하는 방법에 대해 알아봅니다.</p>
                </div>
                <a href="streaming-ingestion-source-connector.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Ingest Data using Streaming Connection HTTP API endpoint">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="streaming-ingestion-http-api.md" title="스트리밍 연결 HTTP API 끝점을 사용하여 데이터 수집" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/331028?format=jpeg&nocache=1740415500889" alt="스트리밍 연결 HTTP API 끝점을 사용하여 데이터 수집"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="streaming-ingestion-http-api.md" target="_blank" rel="referrer" title="스트리밍 연결 HTTP API 끝점을 사용하여 데이터 수집">스트리밍 연결 HTTP API 끝점을 사용하여 데이터 수집</a>
                    </p>
                    <p class="is-size-6">이 비디오는 HTTP API 끝점을 사용하여 실시간으로 Adobe Experience Platform에 데이터를 스트리밍하는 방법을 보여 줍니다.</p>
                </div>
                <a href="streaming-ingestion-http-api.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Adobe 소스에서 데이터 수집

<!-- CARDS
* ingest-data-from-adobe-analytics.md
* ingest-data-from-marketo.md
* ingest-data-from-aam.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Ingest data using the Adobe Analytics source connector">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="ingest-data-from-adobe-analytics.md" title="Adobe Analytics 소스 커넥터를 사용하여 데이터 수집" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/29687?format=jpeg&nocache=1740415502122" alt="Adobe Analytics 소스 커넥터를 사용하여 데이터 수집"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="ingest-data-from-adobe-analytics.md" target="_blank" rel="referrer" title="Adobe Analytics 소스 커넥터를 사용하여 데이터 수집">Adobe Analytics 소스 커넥터를 사용하여 데이터 수집</a>
                    </p>
                    <p class="is-size-6">Adobe Analytics Source 커넥터를 사용하면 Adobe Analytics의 데이터를 Adobe Experience Platform의 실시간 고객 프로필 및 경험 데이터 레이크로 손쉽게 스트리밍, 매핑 및 필터링할 수 있습니다.</p>
                </div>
                <a href="ingest-data-from-adobe-analytics.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Ingest data from Marketo Engage">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="ingest-data-from-marketo.md" title="Marketo Engage에서 데이터 수집" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3419550?format=jpeg&nocache=1740415502109" alt="Marketo Engage에서 데이터 수집"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="ingest-data-from-marketo.md" target="_blank" rel="referrer" title="Marketo Engage에서 데이터 수집">Marketo Engage에서 데이터 수집</a>
                    </p>
                    <p class="is-size-6">표준 및 템플릿 워크플로우를 사용하여 소스 커넥터를 사용하여 Marketo Engage에서 데이터를 수집하는 방법에 대해 알아봅니다.</p>
                </div>
                <a href="ingest-data-from-marketo.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Ingest data using the Adobe Audience Manager data connector">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="ingest-data-from-aam.md" title="Adobe Audience Manager Data Connector를 사용하여 데이터 수집" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/331214/?format=jpeg&nocache=1740415502093" alt="Adobe Audience Manager Data Connector를 사용하여 데이터 수집"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="ingest-data-from-aam.md" target="_blank" rel="referrer" title="Adobe Audience Manager Data Connector를 사용하여 데이터 수집">Adobe Audience Manager 데이터 커넥터를 사용하여 데이터 수집</a>
                    </p>
                    <p class="is-size-6">Audience Manager Data Connector를 사용하여 AAM의 트레이트 및 세그먼트를 플랫폼으로 가져오고 다른 풍부한 데이터와 결합하는 방법을 알아봅니다.</p>
                </div>
                <a href="ingest-data-from-aam.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## 문제 해결

<!-- CARDS
* troubleshoot-sftp-connector.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Troubleshoot - Unable to connect to SFTP source connector">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="troubleshoot-sftp-connector.md" title="문제 해결 - SFTP 소스 커넥터에 연결할 수 없음" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3416134?format=jpeg&nocache=1740415502267" alt="문제 해결 - SFTP 소스 커넥터에 연결할 수 없음"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="troubleshoot-sftp-connector.md" target="_blank" rel="referrer" title="문제 해결 - SFTP 소스 커넥터에 연결할 수 없음">문제 해결 - SFTP 원본 커넥터에 연결할 수 없음</a>
                    </p>
                    <p class="is-size-6">SFTP 소스 커넥터와의 연결 문제를 방지하기 위한 모범 사례에 대해 알아봅니다. SFTP 서버를 Adobe Experience Platform에 성공적으로 연결하려면 특정 검사 지점을 검토하십시오.</p>
                </div>
                <a href="troubleshoot-sftp-connector.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

