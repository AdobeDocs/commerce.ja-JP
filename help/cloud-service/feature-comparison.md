---
title: Adobe Commerce SaaSとPaaSの比較
description: Adobe CommerceのSaaS モデルとPaaS モデルを比較して、自社のビジネスニーズに最適な導入アプローチを判断します。
feature: App Builder, GraphQL, Integration, Saas
role: Developer, Admin, Leader
level: Intermediate
exl-id: c8c9a0b4-f47c-46ec-bc9d-39dee9641f59
source-git-commit: c9df7fe81bdd29eb37f5081b7063d1e22075756a
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 0%

---

# 機能比較

Adobe Commerceには、次の3つのデプロイメントモデルがあります。

- [!BADGE SaaSのみ]{type=Positive url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"} [Adobe Commerce as a Cloud Service](overview.md) （SaaS）
- [!BADGE PaaSのみ]{type=Informative url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"} [Adobe Commerce on Cloud](https://experienceleague.adobe.com/ja/docs/commerce-on-cloud/user-guide/overview) （PaaS）
- [Adobe Commerce](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/overview) （オンプレミス）

この比較では、SaaS （Software-as-a-Service）モデルとPaaS （Platform-as-a-Service）モデルの違いに焦点を当てています。 これらのモデルは、Commerceの導入に対してさまざまなレベルのカスタマイズ、拡張性、制御を提供します。

>[!NOTE]
>
>オンプレミスモデルは、PaaS モデルと同様の機能を共有するため、SaaSとオンプレミス実装を考慮する場合も、この比較が適用されます。

## ストア管理機能

[Commerce管理UI](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/guide-overview)は、バックエンド ストアの操作、在庫、価格設定、プロモーション、顧客とのやり取りを管理する機能にアクセスするための主要なインターフェイスです。 ただし、[!DNL Adobe Commerce as a Cloud Service]では、[!DNL Adobe Commerce on Cloud]およびオンプレミス プロジェクトで利用できる既知の機能の一部を置き換える独自のソリューションを提供しています。

次の表は、[!DNL Adobe Commerce as a Cloud Service]で使用可能な機能と代替ソリューションを示しています。

<table>
    <thead>
        <tr>
            <th>機能</th>
            <th>PaaS モデル [!BADGE PaaSのみ]{type=Informative url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）およびオンプレミス プロジェクトにのみ適用されます。"}</th>
            <th>SaaS モデル [!BADGE SaaSのみ]{type=Positive url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理されるSaaS インフラストラクチャ）"。}</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>デジタルアセット管理</td>
            <td><a href="https://experienceleague.adobe.com/ja/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management">メディアギャラリー</a></td>
            <td><a href="../aem-assets-integration/overview.md">製品ビジュアル</a></td>
        </tr>
        <tr>
            <td>コンテンツ管理</td>
            <td><a href="https://experienceleague.adobe.com/ja/docs/commerce-admin/content-design/guide-overview">Content Management System （CMS） </a>、<a href="https://experienceleague.adobe.com/ja/docs/commerce-admin/page-builder/guide-overview">Page Builder</a>、<a href="https://experienceleague.adobe.com/ja/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite">URLの書き換え</a></td>
            <td><a href="https://experienceleague.adobe.com/developer/commerce/storefront/merchants/get-started/?lang=ja">ストアフロントビルダー</a></td>
        </tr>
        <tr>
            <td>カタログマーチャンダイジング</td>
            <td><a href="https://experienceleague.adobe.com/ja/docs/commerce-admin/content-design/staging/content-staging"> コンテンツのステージング </a>、<a href="https://experienceleague.adobe.com/ja/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser"> ビジュアルマーチャンダイザー</a></td>
            <td><a href="../catalog-service/overview.md">カタログサービス</a></td>
        </tr>
        <tr>
            <td>支払い</td>
            <td><a href="https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/payments/payments">決済ソリューション</a></td>
            <td><a href="../payment-services/guide-overview.md">決済サービス</a></td>
        </tr>
        <tr>
            <td>B2B機能</td>
            <td>インストール後にフル B2B機能を利用可能</td>
            <td>B2Bのコア機能がプリインストールされています<sup>1</sup></td>
        </tr>
        <tr>
            <td>実験</td>
            <td>特定の階層を対象としたアドオン</td>
            <td>エンゲージメントとコンバージョンを最適化するためのネイティブ A/B テスト</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                <sup>1</sup>企業管理や見積もりなど、<a href="https://experienceleague.adobe.com/ja/docs/commerce-admin/b2b/guide-overview">B2Bのコア機能</a>は、SaaSですぐに利用できます。 ただし、業界固有のカスタマイズには、追加の実装に関する考慮事項が必要な場合があります。
            </td>
        </tr>
    </tfoot>
</table>

## 拡張性とプラットフォーム機能

次の表では、プラットフォームの機能と拡張性機能を比較して、その違いを理解し、導入を開始する前にビジネス要件に最も適したモデルを決定するのに役立ちます。

<table>
    <thead>
        <tr>
            <th>機能</th>
            <th>PaaS モデル [!BADGE PaaSのみ]{type=Informative url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）およびオンプレミス プロジェクトにのみ適用されます。"}</th>
            <th>SaaS モデル [!BADGE SaaSのみ]{type=Positive url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理されるSaaS インフラストラクチャ）"。}</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>プラットフォームの機能</strong></td>
        </tr>
        <tr>
            <td>機能およびセキュリティ更新</td>
            <td>手動によるアップグレードとパッチ適用が必要です。 年間6回のパッチリリースと1回のマイナーリリース。</td>
            <td>バージョンのないSaaS モデルを通じて、Adobeによって自動的にアップグレード</td>
        </tr>
        <tr>
            <td>ホスティングインフラ</td>
            <td>シングルテナント</td>
            <td>マルチテナント</td>
        </tr>
        <tr>
            <td>パフォーマンスと拡張性</td>
            <td>拡張されたアーキテクチャの水平方向の自動スケーリング。 web階層の垂直方向への自動スケーリングは、非スケーリングのアーキテクチャを含むすべてのマーチャントの早期アクセスでロールアウトされます。</td>
            <td>スタック全体で自動的に拡張するマルチテナントクラウドネイティブアプリケーション</td>
        </tr>
        <tr>
            <td>可観測性</td>
            <td>[!DNL New Relic] 環境を監視および管理するためのユーザーのアクセス</td>
            <td>Adobe managed. お客様は、[!DNL OpenTelemetry]個のアプリに[!DNL App Builder]を、ストアフロントにRUM ダッシュボードを使用できます。 [!DNL New Relic] ライセンスは含まれていません。 お客様は、自分の[!DNL API Mesh] アカウントにデータを送信するように[!DNL App Builder]と[!DNL New Relic]を設定できます。</td>
        </tr>
        <tr>
            <td>CDN</td>
            <td>[!DNL Fastly] 含まれる</td>
            <td>Edge CDNのフルマネージドとCommerce Storefrontの緊密な連携。 BYO-CDNもサポートされています。</td>
        </tr>
        <tr>
            <td>セキュリティとコンプライアンス</td>
            <td>SOC2、PCI、ホスティングプロバイダーごとのISO認証、HIPAA</td>
            <td>SOC2、PCI、ISO、GDPR。 HIPAAは現在利用できません。</td>
        </tr>
        <tr>
            <td>災害復旧とSLA</td>
            <td>99.99%のインフラストラクチャ、99.9%のアプリケーション（Managed Services）</td>
            <td>99.9% （インフラストラクチャおよびアプリケーション）、迅速なRPO/RTO</td>
        </tr>
        <tr>
            <td>ホスティング地域</td>
            <td>Azure（24拠点）、AWS（22拠点）、GCP （8拠点、非標準）</td>
            <td>グローバルに利用可能： お住まいの地域の本番環境について詳しくは、カスタマーサービス担当者にお問い合わせください。 需要に応じて展開した追加の場所。</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Commerce管理のカスタマイズ</strong></td>
        </tr>
        <tr>
            <td>Admin Consoleの拡張性</td>
            <td>PHPのカスタマイズとテーマ設定、App Builderの拡張性（推奨）</td>
            <td>App Builderの拡張機能</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>拡張機能</strong></td>
        </tr>
        <tr>
            <td>拡張性モデル</td>
            <td>インプロセス（PHPのカスタマイズ）およびアウトプロセス（推奨：API、イベント、App Builder）</td>
            <td>アウトプロセスのみ（API、イベント、App Builder）</td>
        </tr>
        <tr>
            <td>拡張可能なweb API</td>
            <td>ネイティブのREST/GraphQL拡張性とカスタムリゾルバーを備えたAPI メッシュ</td>
            <td>カスタムリゾルバーを使用したAPI メッシュ</td>
        </tr>
        <tr>
            <td>データモデルの拡張性</td>
            <td>データモデルの完全なカスタマイズ</td>
            <td>コアおよびB2B エンティティのカスタム属性<sup>1</sup></td>
        </tr>
        <tr>
            <td>テクノロジー</td>
            <td>CSS、CLI、HTML、JS、PHP、XML</td>
            <td>CSS、CLI、HTML、JS、Node</td>
        </tr>
        <tr>
            <td>アプリマーケットプレイス</td>
            <td>[!DNL App Builder]個のアプリ用の[Magento Marketplace] （https://marketplace.magento.com/） （PHP拡張機能）および[Exchange Marketplace] （https://commercemarketplace.adobe.com） （推奨）</td>
            <td>[!DNL App Builder] [[!DNL Exchange Marketplace]] （https://commercemarketplace.adobe.com）からのアプリ</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>データとストレージ</strong></td>
        </tr>
        <tr>
            <td>検索インデックスのカスタマイズ</td>
            <td>ネイティブ検索のカスタマイズ</td>
            <td>サードパーティソリューションが必要</td>
        </tr>
        <tr>
            <td>カスタムメールタイプ</td>
            <td>電子メールのフルカスタマイズ</td>
            <td>通常のメールテンプレートのみ</td>
        </tr>
        <tr>
            <td>カスタムデータストレージ</td>
            <td>DB、ファイル、キャッシュ、キュー</td>
            <td>App Builderの状態ライブラリ （ファイルのみ） <sup>2 - <a href="https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/database">App Builderのデータベースストレージ </a>は現在、早期アクセス中です。</sup></td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                <sup>1</sup> SaaSのデータモデル拡張性は、B2B エンティティを含め、製品と顧客を超えた<a href="https://developer.adobe.com/commerce/webapi/graphql/schema/attributes/mutations/"> コアエンティティ </a>の拡張をサポートしています。 ただし、業界固有のデータモデル（たとえば、ディーラー固有の属性）には、追加のアーキテクチャに関する考慮事項が必要になる場合があります。
                <br><br>
                <sup>2</sup> Adobeは、SaaSの永続的なストレージのニーズに対応するために、Document DB統合をアクティブに動作しています。 現在、長期的なデータ保存を必要とする実装では、追加のインフラストラクチャのプロビジョニングと保守が必要になる場合があります。
            </td>
        </tr>
    </tfoot>
</table>

>[!NOTE]
>
>SaaSへの移行を検討する際には、Adobeで次のことをお勧めします。
>
>- 可能な限り、適切な機能をプロセス外の拡張性に移行します。
>- トランジションが必要なサーフェス領域を小さくします。
>- API機能を拡張する場合は[!DNL API Mesh]を検討してください。
>- 継続的なプラットフォームの進化と新機能リリースをモニタリングするAdobe。
>- 利用可能な拡張性オプションに対して、業界固有のデータモデル要件を評価します。

