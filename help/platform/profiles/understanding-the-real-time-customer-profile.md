---
title: 실시간 고객 프로필 이해
description: 이 비디오에서는 Adobe Experience Platform에서 실시간 고객 프로필을 조합하고 업데이트하는 방법과 이러한 프로필에 액세스하여 사용하는 방법을 설명합니다.
feature: Profiles
role: Data Engineer, Data Architect, Developer
level: Beginner
jira: KT-2701
thumbnail: 27251.jpg
exl-id: 6ef5b589-f874-4687-bee3-9650c993f383
source-git-commit: 112e092df6d486d8b9103013bec57d820b8ae6d7
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 13%

---

# 실시간 고객 프로필 개요

이 비디오에서는 Adobe Experience Platform에서 실시간 고객 프로필을 조합하고 업데이트하는 방법과 이러한 프로필에 액세스하여 사용하는 방법을 설명합니다. 자세한 내용은 [실시간 고객 프로필 설명서](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=ko)를 참조하세요.

>[!VIDEO](https://video.tv.adobe.com/v/27251?learn=on&enablevpops)

## 아키텍처 및 기능

<!-- CARDS
* overview-diagram.md
* create-merge-policies.md
* union-schemas-overview.md
* create-a-computed-attribute-for-sum-of-purchases.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Overview Diagram of Real-Time Customer Profile">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="overview-diagram.md" title="실시간 고객 프로필 개요 다이어그램" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/33600?format=jpeg&nocache=1740415066741" alt="실시간 고객 프로필 개요 다이어그램"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="overview-diagram.md" target="_blank" rel="referrer" title="실시간 고객 프로필 개요 다이어그램">실시간 고객 프로필의 개요 다이어그램</a>
                    </p>
                    <p class="is-size-6">이 비디오에서는 Adobe Experience Platform의 실시간 고객 프로필 기능을 보여 주는 개요 다이어그램을 소개합니다.</p>
                </div>
                <a href="overview-diagram.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Create merge policies">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="create-merge-policies.md" title="병합 정책 만들기" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/330433?format=jpeg&nocache=1740415066765" alt="병합 정책 만들기"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="create-merge-policies.md" target="_blank" rel="referrer" title="병합 정책 만들기">병합 정책 만들기</a>
                    </p>
                    <p class="is-size-6">이 비디오는 Adobe Experience Platform에서 병합 정책을 만드는 방법을 보여 줍니다. 병합 정책은 플랫폼이 고객 프로필을 만들기 위해 다양한 소스의 데이터 세트를 결합할 때 사용할 데이터를 결정하고 우선 순위를 매기는 데 사용하는 규칙입니다.</p>
                </div>
                <a href="create-merge-policies.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Union schemas overview">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="union-schemas-overview.md" title="결합 스키마 개요" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/329940?format=jpeg&nocache=1740415066755" alt="결합 스키마 개요"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="union-schemas-overview.md" target="_blank" rel="referrer" title="결합 스키마 개요">결합 스키마 개요</a>
                    </p>
                    <p class="is-size-6">실시간 고객 프로필을 통해 고객 여정의 각 단계에서 채널 간 개인화를 규모에 맞게 확장할 수 있습니다. 스키마와 해당 데이터 세트를 모두 활성화하여 실시간 고객 프로필에 대해 배치 또는 스트리밍 데이터를 활성화할 수 있습니다.</p>
                </div>
                <a href="union-schemas-overview.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Create a computed attribute for the sum of purchases">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="create-a-computed-attribute-for-sum-of-purchases.md" title="구매 합계에 대한 계산된 속성 만들기" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3425899?format=jpeg&nocache=1740415066775" alt="구매 합계에 대한 계산된 속성 만들기"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="create-a-computed-attribute-for-sum-of-purchases.md" target="_blank" rel="referrer" title="구매 합계에 대한 계산된 속성 만들기">구매 합계에 대한 계산된 속성 만들기</a>
                    </p>
                    <p class="is-size-6">계산된 속성을 사용하여 여러 판매 채널에서 사용자가 구매한 금액을 합산하는 방법에 대해 알아봅니다.</p>
                </div>
                <a href="create-a-computed-attribute-for-sum-of-purchases.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## 프로필 데이터 수집 및 관리

<!-- CARDS
* bring-data-into-the-real-time-customer-profile.md
* delete-profiles.md
* update-a-specific-attribute-with-upsert.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Bring Data into Real-Time Customer Profile">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="bring-data-into-the-real-time-customer-profile.md" title="실시간 고객 프로필로 데이터 가져오기" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/27301?format=jpeg&nocache=1740415067018" alt="실시간 고객 프로필로 데이터 가져오기"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="bring-data-into-the-real-time-customer-profile.md" target="_blank" rel="referrer" title="실시간 고객 프로필로 데이터 가져오기">실시간 고객 프로필로 데이터 가져오기</a>
                    </p>
                    <p class="is-size-6">실시간 고객 프로필을 통해 고객 여정의 각 단계에서 채널 간 개인화를 규모에 맞게 확장할 수 있습니다. 스키마와 해당 데이터 세트를 모두 활성화하여 실시간 고객 프로필에 대해 배치 또는 스트리밍 데이터를 활성화할 수 있습니다.</p>
                </div>
                <a href="bring-data-into-the-real-time-customer-profile.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Delete profiles">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="delete-profiles.md" title="프로필 삭제" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3429807/?format=jpeg&nocache=1740415067005" alt="프로필 삭제"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="delete-profiles.md" target="_blank" rel="referrer" title="프로필 삭제">프로필 삭제</a>
                    </p>
                    <p class="is-size-6">Real-Time Customer Profile API를 사용하여 프로필 스토어에서 데이터를 삭제하는 방법을 알아봅니다. 프로필 API를 사용하면 데이터 레이크 또는 ID 그래프에 영향을 주지 않고 프로필 스토어에서 데이터를 제거할 수 있습니다. 이 기능은 ID 그래프 문제를 해결하고 일부 프로필에만 영향을 주는 데이터 수집에서 가끔 발생하는 오류를 수정할 때 유용합니다.</p>
                </div>
                <a href="delete-profiles.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">시청</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Update specific profile attributes using `upsert`">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="update-a-specific-attribute-with-upsert.md" title="&apos;업데이트&apos;를 사용하여 특정 프로필 속성 업데이트" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3416133/?format=jpeg&nocache=1740415067029" alt="&apos;업데이트&apos;를 사용하여 특정 프로필 속성 업데이트"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="update-a-specific-attribute-with-upsert.md" target="_blank" rel="referrer" title="&apos;업데이트&apos;를 사용하여 특정 프로필 속성 업데이트">'업데이트'를 사용하여 특정 프로필 속성 업데이트</a>
                    </p>
                    <p class="is-size-6">Adobe Experience Platform의 '업데이트' 기능을 사용하여 프로필의 특정 속성을 업데이트하는 방법을 알아봅니다.</p>
                </div>
                <a href="update-a-specific-attribute-with-upsert.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">시청</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## 계정 프로필

<!-- CARDS
* view-account-profiles.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="View account profiles">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="view-account-profiles.md" title="계정 프로필 보기" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/338251?format=jpeg&nocache=1740415067214" alt="계정 프로필 보기"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="view-account-profiles.md" target="_blank" rel="referrer" title="계정 프로필 보기">계정 프로필 보기</a>
                    </p>
                    <p class="is-size-6">Real-Time CDP B2B edition에서 계정 프로필을 보는 방법을 알아봅니다.</p>
                </div>
                <a href="view-account-profiles.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->