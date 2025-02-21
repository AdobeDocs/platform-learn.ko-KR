---
title: Adobe Experience Platform의 관리 기능
description: Adobe Experience Platform의 관리 기능에 대해 알아보기
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
feature: Sandboxes, Access Control, Alerts
role: Admin
level: Beginner
source-git-commit: c81ae424f501e2aa551a9f64967a71f942c388b4
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 26%

---

# Adobe Experience Platform의 관리 기능

Adobe Experience Platform의 관리 기능에 대해 알아보고 규모에 따라 세분화된 제어를 통해 사용자 및 샌드박스 환경을 관리할 수 있습니다. 라이선스에 대한 사용을 모니터링하고 구현에서 수행된 변경 사항을 추적합니다.

## 권한

사용자 권한을 관리하는 방법을 알아봅니다.

<!-- CARDS
* add-users.md{title=Add users}
* add-developers.md{title=Add developers}
* add-product-administrators.md{title=Add administrators}
* configure-attribute-based-access-control.md
* https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/users-and-permissions{title=Add users to Data Collection}
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Add users">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="add-users.md" title="사용자 추가" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/336081?format=jpeg&nocache=1739899941213" alt="사용자 추가"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="add-users.md" target="_blank" rel="referrer" title="사용자 추가">사용자 추가</a>
                    </p>
                    <p class="is-size-6">Adobe Experience Platform 기반 애플리케이션에서 사용자를 추가하고 권한을 관리하는 방법을 알아봅니다.</p>
                </div>
                <a href="add-users.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">시청</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Add users to Data Collection">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/users-and-permissions" title="데이터 수집에 사용자 추가" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/28734/?format=jpeg&nocache=1739899941476" alt="데이터 수집에 사용자 추가"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/users-and-permissions" target="_blank" rel="referrer" title="데이터 수집에 사용자 추가">데이터 수집에 사용자 추가</a>
                    </p>
                    <p class="is-size-6">회사 직원이 작업을 수행하는 데 필요한 액세스 권한을 가질 수 있도록 Adobe Experience Platform 데이터 수집 기능에 대한 사용자를 추가하고 권한을 관리하는 방법을 알아봅니다.</p>
                </div>
                <a href="https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/users-and-permissions" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Add developers">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="add-developers.md" title="개발자 추가" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3426407?format=jpeg&nocache=1739899941236" alt="개발자 추가"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="add-developers.md" target="_blank" rel="referrer" title="개발자 추가">개발자 추가</a>
                    </p>
                    <p class="is-size-6">Adobe Experience Platform 기반 애플리케이션에 개발자를 추가하고 API 자격 증명에 대한 권한을 부여하는 방법을 알아봅니다</p>
                </div>
                <a href="add-developers.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">시청</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Add administrators">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="add-product-administrators.md" title="관리자 추가" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333860?format=jpeg&nocache=1739899941246" alt="관리자 추가"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="add-product-administrators.md" target="_blank" rel="referrer" title="관리자 추가">관리자 추가</a>
                    </p>
                    <p class="is-size-6">Adobe Experience Platform 및 플랫폼 기반 애플리케이션용 제품 관리자를 추가하는 방법을 알아봅니다.</p>
                </div>
                <a href="add-product-administrators.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">시청</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Configure attribute-based access control">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="configure-attribute-based-access-control.md" title="속성 기반 액세스 제어 구성" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/345641?format=jpeg&nocache=1739899941225" alt="속성 기반 액세스 제어 구성"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="configure-attribute-based-access-control.md" target="_blank" rel="referrer" title="속성 기반 액세스 제어 구성">속성 기반 액세스 제어 구성</a>
                    </p>
                    <p class="is-size-6">특정 Experience Platform 리소스에 대한 액세스를 제한하기 위해 속성 기반 액세스 제어를 구성하는 방법에 대해 알아봅니다.</p>
                </div>
                <a href="configure-attribute-based-access-control.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">시청</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## 샌드박스

샌드박스 환경을 관리하는 방법을 알아봅니다.

<!-- CARDS
* use-sandboxes.md
* copy-objects-between-sandboxes.md
* share-packages-across-orgs.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Use sandboxes">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="use-sandboxes.md" title="샌드박스 사용" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/29838/?format=jpeg&nocache=1739899941687" alt="샌드박스 사용"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="use-sandboxes.md" target="_blank" rel="referrer" title="샌드박스 사용">샌드박스 사용</a>
                    </p>
                    <p class="is-size-6">Experience Platform 샌드박스가 새로운 기능이나 기존 기능을 시험해 보고 빠른 실패 접근 방식으로 작업할 수 있는 격리된 환경을 제공하는 방법을 알아봅니다. 개발 환경을 재설정하고 다시 시작하고 API 호출에 샌드박스를 사용하는 방법을 알아봅니다.</p>
                </div>
                <a href="use-sandboxes.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">시청</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Copy configurations between sandboxes">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="copy-objects-between-sandboxes.md" title="샌드박스 간 구성 복사" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3424763/?format=jpeg&nocache=1739899941676" alt="샌드박스 간 구성 복사"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="copy-objects-between-sandboxes.md" target="_blank" rel="referrer" title="샌드박스 간 구성 복사">샌드박스 간 구성 복사</a>
                    </p>
                    <p class="is-size-6">패키지를 사용하여 Experience Platform 샌드박스 간에 구성을 복사하는 방법을 알아봅니다. 샌드박스에서 스키마, 데이터 세트, 여정 등을 쉽게 복제할 수 있습니다.</p>
                </div>
                <a href="copy-objects-between-sandboxes.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">시청</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Share packages across IMS Orgs">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="share-packages-across-orgs.md" title="IMS 조직 간 패키지 공유" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3435815/?format=jpeg&nocache=1739899941663" alt="IMS 조직 간 패키지 공유"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="share-packages-across-orgs.md" target="_blank" rel="referrer" title="IMS 조직 간 패키지 공유">IMS 조직 간 패키지 공유</a>
                    </p>
                    <p class="is-size-6">패키지를 사용하여 IMS 조직 간에 Experience Platform 구성을 복사하는 방법에 대해 알아봅니다. 여러 IMS 조직 간에 스키마, 데이터 세트, 여정 등을 쉽게 복제하여 다중 지역/다중 브랜드 배포를 지원합니다.</p>
                </div>
                <a href="share-packages-across-orgs.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">시청</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## 라이선스 사용

<!-- CARDS
* https://experienceleague.adobe.com/en/docs/experience-platform/landing/license/license-usage-dashboard
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="License Usage Dashboard">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://experienceleague.adobe.com/en/docs/experience-platform/landing/license/license-usage-dashboard" title="라이선스 사용 대시보드" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://experienceleague.adobe.com/en/docs/experience-platform/landing/license/license-usage-dashboard./media_15ebe5d6a87c210826e7502ba8402e61caa4a8ec8.png?width=400&format=png&optimize=medium" alt="라이선스 사용 대시보드"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://experienceleague.adobe.com/en/docs/experience-platform/landing/license/license-usage-dashboard" target="_blank" rel="referrer" title="라이선스 사용 대시보드">라이선스 사용 대시보드</a>
                    </p>
                    <p class="is-size-6">Adobe Experience Platform UI는 조직의 라이선스 사용에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다.</p>
                </div>
                <a href="https://experienceleague.adobe.com/en/docs/experience-platform/landing/license/license-usage-dashboard" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## 경고

<!-- CARDS
{cta = Watch}
* use-alerts.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Use alerts">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="use-alerts.md" title="경고 사용" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/336218?format=jpeg&nocache=1739899942212" alt="경고 사용"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="use-alerts.md" target="_blank" rel="referrer" title="경고 사용">경고 사용</a>
                    </p>
                    <p class="is-size-6">Adobe Experience Platform에서 알림을 구독하고 관리하는 방법에 대해 알아보십시오. 경고는 다양한 프로세스를 모니터링하여 플랫폼 구현이 원활하게 실행되고 있는지 확인하는 데 도움이 됩니다.</p>
                </div>
                <a href="use-alerts.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">시청</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## 태그

<!-- CARDS
* https://experienceleague.adobe.com/en/docs/experience-platform/administrative-tags/ui/managing-tags
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Managing Unified Tags">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://experienceleague.adobe.com/en/docs/experience-platform/administrative-tags/ui/managing-tags" title="통합 태그 관리" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://experienceleague.adobe.com/en/docs/experience-platform/administrative-tags/ui/managing-tags./media_14b5a89a9bf89cb36a9e78864b1568e59c9d9d86b.png?width=400&format=png&optimize=medium" alt="통합 태그 관리"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://experienceleague.adobe.com/en/docs/experience-platform/administrative-tags/ui/managing-tags" target="_blank" rel="referrer" title="통합 태그 관리">통합 태그 관리</a>
                    </p>
                    <p class="is-size-6">이 문서는 Adobe Experience Cloud의 통합 태그 관리에 대한 정보를 제공합니다.</p>
                </div>
                <a href="https://experienceleague.adobe.com/en/docs/experience-platform/administrative-tags/ui/managing-tags" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->
