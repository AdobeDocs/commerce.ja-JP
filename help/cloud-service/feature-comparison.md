---
title: Adobe Commerceの SaaS と PaaS の比較
description: Adobe Commerceの SaaS モデルと PaaS モデルを比較して、ビジネスニーズに最適な実装アプローチを決定します。
feature: App Builder, GraphQL, Integration, Saas
role: Developer, Admin, Leader
level: Intermediate
exl-id: c8c9a0b4-f47c-46ec-bc9d-39dee9641f59
source-git-commit: 5e4481dfd7259a07bda58a1e945b086e9f1c1805
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# 機能の比較

Adobe Commerceには、次の 3 つのデプロイメントモデルがあります。

- [!BADGE SaaS のみ &#x200B;]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"} [Adobe Commerce as a Cloud Service](overview.md) （SaaS）
- [!BADGE PaaS のみ &#x200B;]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeが管理する PaaS インフラストラクチャ）およびオンプレミスプロジェクトにのみ適用されます。"} [Cloud 上のAdobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/overview) （Paa）
- [Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/overview) （オンプレミス）

この比較では、SaaS （software-as-a-service）モデルと PaaS （platform-as-a-service）モデルの違いに焦点を当てています。 これらのモデルにより、Commerce実装に対する様々なレベルのカスタマイズ、拡張機能、制御が提供されます。

>[!NOTE]
>
>オンプレミスモデルは PaaS モデルと同様の機能を共有するので、この比較は SaaS とオンプレミス実装を検討する場合にも当てはまります。

## ストア管理機能

[Commerce管理 UI](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/guide-overview) は、バックエンドのストアの運営、在庫、価格設定、プロモーション、顧客とのやり取りを管理する機能にアクセスするための主要なインターフェイスです。 ただし、[!DNL Adobe Commerce as a Cloud Service] は、[!DNL Adobe Commerce on Cloud] ンプレミスプロジェクトやオンプレミスプロジェクトで利用できる既知の機能の一部に代わる独自のソリューションを提供しています。

次の表に、[!DNL Adobe Commerce as a Cloud Service] で使用可能な機能と代替ソリューションを示します。

<table>
    <thead>
        <tr>
            <th>機能</th>
            <th>PaaS モデル [!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeが管理する PaaS インフラストラクチャ）およびオンプレミスプロジェクトにのみ適用されます。"}</th>
            <th>SaaS モデル [!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用（Adobeが管理する SaaS インフラストラクチャ）"}</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>デジタルアセット管理</td>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management">メディアギャラリー</a></td>
            <td><a href="../aem-assets-integration/overview.md">製品ビジュアル</a></td>
        </tr>
        <tr>
            <td>コンテンツ管理</td>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/guide-overview"> コンテンツ管理システム（CMS） </a>、<a href="https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/guide-overview"> ページビルダー </a>、<a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite">URL の書き換え </a></td>
            <td><a href="https://experienceleague.adobe.com/developer/commerce/storefront/merchants/get-started/">Storefront ビルダー</a></td>
        </tr>
        <tr>
            <td>カタログマーチャンダイジング</td>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/staging/content-staging"> コンテンツのステージング </a>、<a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser"> ビジュアルマーチャンダイザー </a></td>
            <td><a href="../catalog-service/overview.md">カタログサービス</a></td>
        </tr>
        <tr>
            <td>支払額</td>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/payments/payments">支払いソリューション</a></td>
            <td><a href="../payment-services/guide-overview.md">支払いサービス</a></td>
        </tr>
        <tr>
            <td>B2B 機能</td>
            <td>インストール後に利用可能な完全な B2B 機能</td>
            <td>コア B2B 機能と共にプリインストール <sup>1</sup></td>
        </tr>
        <tr>
            <td>実験</td>
            <td>特定の層用のアドオン</td>
            <td>エンゲージメントとコンバージョンを最適化するネイティブ A/B テスト</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                <sup>1</sup> 会社の管理や見積りなどのコア <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/guide-overview">B2B 機能 </a> は、SaaS でそのまま使用できます。 ただし、業界固有のカスタマイズを行う場合は、実装に関する考慮事項も追加する必要があります。
            </td>
        </tr>
    </tfoot>
</table>

## 拡張機能とプラットフォーム機能

次の表に、プラットフォームの機能と拡張機能を比較します。この表を参照すると、違いを理解し、実装を開始する前にビジネス要件に最適なモデルを判断するのに役立ちます。

<table>
    <thead>
        <tr>
            <th>機能</th>
            <th>PaaS モデル [!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeが管理する PaaS インフラストラクチャ）およびオンプレミスプロジェクトにのみ適用されます。"}</th>
            <th>SaaS モデル [!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用（Adobeが管理する SaaS インフラストラクチャ）"}</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Platform の機能</strong></td>
        </tr>
        <tr>
            <td>機能とセキュリティの更新</td>
            <td>手動でのアップグレードとパッチ適用が必要です。 年に 6 つのパッチリリースと 1 つのマイナーリリース。</td>
            <td>バージョンレス SaaS モデルを通じてAdobeにより自動アップグレード</td>
        </tr>
        <tr>
            <td>ホスティングインフラストラクチャ</td>
            <td>シングルテナント</td>
            <td>マルチテナント</td>
        </tr>
        <tr>
            <td>パフォーマンスと拡張性</td>
            <td>スケーリングされたアーキテクチャに対応する水平方向の自動スケーリング。 Web 階層の垂直方向の自動スケーリングは、拡張されていないアーキテクチャを含むすべてのマーチャントの早期アクセスで展開されます。</td>
            <td>スタック全体での完全な自動スケーリングを備えたマルチテナントクラウドネイティブアプリケーション</td>
        </tr>
        <tr>
            <td>可観測性</td>
            <td>[!DNL New Relic] お客様が環境を監視および管理するためのアクセス</td>
            <td>Adobeの管理 お客様は、[!DNL OpenTelemetry] for [!DNL App Builder] アプリと RUM ダッシュボードをストアフロントに使用できます。 [!DNL New Relic] ライセンスは含まれていません。 顧客は、[!DNL API Mesh] と [!DNL App Builder] を設定して、自分の [!DNL New Relic] アカウントにデータを送信できます。</td>
        </tr>
        <tr>
            <td>CDN</td>
            <td>[!DNL Fastly] included</td>
            <td>Edge CDN をCommerce ストアフロントと緊密に連結して完全に管理する。 BYO-CDN もサポートされています。</td>
        </tr>
        <tr>
            <td>セキュリティとコンプライアンス</td>
            <td>ホスティングプロバイダーごとの SOC2、PCI、ISO 認定、HIPAA</td>
            <td>SOC2、PCI、ISO、GDPR。 HIPAA は現在利用できません。</td>
        </tr>
        <tr>
            <td>災害復旧と SLA</td>
            <td>99.99% のインフラストラクチャ、99.9% のアプリケーション（Managed Services）</td>
            <td>99.9% （インフラストラクチャとアプリケーション）、RPO/RTO の短縮</td>
        </tr>
        <tr>
            <td>ホスティング地域</td>
            <td>Azure （24 か所）、AWS（22 か所）、GCP （標準ではなく 8 か所）</td>
            <td>グローバルに利用可能。 お住まいの地域の実稼動環境について詳しくは、カスタマーサービス担当者にお問い合わせください。 追加の場所は、需要に基づいてロールアウトされます。</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Commerce Admin のカスタマイズ</strong></td>
        </tr>
        <tr>
            <td>Admin Console の拡張機能</td>
            <td>PHP のカスタマイズとテーマ設定、App Builderの拡張性（推奨）</td>
            <td>App Builder拡張機能</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>拡張性</strong></td>
        </tr>
        <tr>
            <td>拡張モデル</td>
            <td>プロセス内（PHP のカスタマイズ）およびプロセス外（推奨：API、イベント、App Builder）</td>
            <td>アウトオブプロセスのみ（API、イベント、App Builder）</td>
        </tr>
        <tr>
            <td>拡張可能な web API</td>
            <td>ネイティブの REST/GraphQL拡張機能とカスタムリゾルバーを含む API メッシュ</td>
            <td>API メッシュとカスタムリゾルバー</td>
        </tr>
        <tr>
            <td>データモデル拡張機能</td>
            <td>データモデルの完全なカスタマイズ</td>
            <td>コアおよび B2B エンティティのカスタム属性 <sup>1</sup></td>
        </tr>
        <tr>
            <td>技術</td>
            <td>CSS, CLI, HTML, JS, PHP, XML</td>
            <td>CSS, CLI, HTML, JS, Node</td>
        </tr>
        <tr>
            <td>アプリのマーケットプレイス</td>
            <td>[!DNL Magento Marketplace] アプリケーションの場合、[[!DNL Exchange Marketplace]] （https://marketplace.magento.com/） （PHP 拡張）および [[!DNL App Builder]] （https://commercemarketplace.adobe.com） （推奨）</td>
            <td>[!DNL App Builder] [[!DNL Exchange Marketplace]] （https://commercemarketplace.adobe.com）のアプリ</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>データとストレージ</strong></td>
        </tr>
        <tr>
            <td>検索インデックスのカスタマイズ</td>
            <td>ネイティブ検索のカスタマイズ</td>
            <td>サードパーティのソリューションが必要</td>
        </tr>
        <tr>
            <td>カスタム E メール タイプ</td>
            <td>メールの完全なカスタマイズ</td>
            <td>標準のメールテンプレートのみ</td>
        </tr>
        <tr>
            <td>カスタムデータストレージ</td>
            <td>DB, ファイル，キャッシュ，キュー</td>
            <td>App Builder ステートライブラリ（ファイルのみ） <sup>2 - <a href="https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/database">App Builderのデータベースストレージ </a> は現在、早期アクセス中です。</sup></td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                <sup>1</sup> SaaS のデータモデル拡張機能では、B2B エンティティなど、製品および顧客を超えた <a href="https://developer.adobe.com/commerce/webapi/graphql/schema/attributes/mutations/"> コアエンティティの拡張 </a> がサポートされています。 ただし、業界固有のデータモデル（ディーラー固有の属性など）を使用するには、アーキテクチャに関する追加の考慮事項が必要になる場合があります。
                <br><br>
                <sup>2</sup> Adobeは、SaaS に対する永続的なストレージニーズに対応するために、Document DB の統合に積極的に取り組んでいます。 現在、長期的なデータストレージを必要とする実装では、追加のインフラストラクチャのプロビジョニングと保守が必要になる場合があります。
            </td>
        </tr>
    </tfoot>
</table>

>[!NOTE]
>
>SaaS への移行を検討する場合、Adobeでは次の点を推奨します。
>
>- 可能な場合は、適切な機能をプロセス外の拡張機能に移行します。
>- トランジションが必要なサーフェス領域を減らします。
>- API 機能を拡張する場合は、[!DNL API Mesh] を検討してください。
>- Adobeの継続的なプラットフォーム進化と新機能リリースを監視します。
>- 使用可能な拡張オプションに照らして、業界固有のデータモデル要件を評価します。
>- [&#x200B; カタログビューとポリシーを活用したマーチャンダイジングサービス &#x200B;](../optimizer/setup/catalog-view.md) の採用を検討します。
