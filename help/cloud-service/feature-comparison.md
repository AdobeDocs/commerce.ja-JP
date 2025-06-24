---
title: Adobe Commerceの SaaS と PaaS の比較
description: Adobe Commerceの SaaS モデルと PaaS モデルを比較して、ビジネスニーズに最適な実装アプローチを決定します。
role: Architect
exl-id: c8c9a0b4-f47c-46ec-bc9d-39dee9641f59
source-git-commit: 0eb74c1e70ac2c7073f8f9387baec4f6d3e90a86
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# 機能の比較

Adobe Commerceには、次の 3 つのデプロイメントモデルがあります。

- [!BADGE SaaS のみ &#x200B;]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"} [Adobe Commerce as a Cloud Service](overview.md) （SaaS）
- [!BADGE PaaS のみ &#x200B;]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeが管理する PaaS インフラストラクチャ）およびオンプレミスプロジェクトにのみ適用されます。"} [Cloud 上のAdobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/overview) （Paa）
- [Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/overview) （オンプレミス）

この比較では、異なるレベルのカスタマイズ、拡張機能、コマース実装の制御を提供する、サービスとしてのソフトウェア（SaaS）とサービスとしてのプラットフォーム（PaaS）モデルの違いに焦点を当てています。

>[!NOTE]
>
>オンプレミスモデルは PaaS モデルと同様の機能を共有するので、この比較は SaaS とオンプレミス実装を検討する場合にも当てはまります。

## ストア管理機能

[Commerce管理 UI](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/guide-overview) は、バックエンドのストアの運営、在庫、価格設定、プロモーション、顧客とのやり取りを管理する機能にアクセスするための主要なインターフェイスです。 ただし、[!DNL Adobe Commerce as a Cloud Service] では、Adobe Commerce on Cloud やオンプレミスプロジェクトで利用できる既知の機能の一部に代わる独自のソリューションを提供しています。

次の表に、[!DNL Adobe Commerce as a Cloud Service] で使用可能な機能と代替ソリューションを示します。

<table>
    <thead>
        <tr>
            <th>PaaS モデル [!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeが管理する PaaS インフラストラクチャ）およびオンプレミスプロジェクトにのみ適用されます。"}</th>
            <th>SaaS モデル [!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用（Adobeが管理する SaaS インフラストラクチャ）"}</th>
            <th>詳細</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management">デジタルアセット管理</a></td>
            <td><a href="../product-visuals/overview.md">製品ビジュアル</a></td>
            <td>Adobe Experience Managerと統合してリッチメディアコンテンツを管理する、堅牢なデジタルアセット管理（DAM）システム。 または、デフォルトのデジタルファイルとアセット管理機能には、デジタルアセットを保存および管理するための基本的なアセット管理ツールが用意されています。</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/guide-overview">コンテンツ管理システム（CMS）</a></td>
            <td rowspan="3"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/merchants/get-started/">Storefront ビルダー</a></td>
            <td rowspan="3">CMSでは、ドキュメントオーサリングやビジュアルエディターを使用して、ストアフロントコンテンツを簡単に作成および管理でき、ネイティブの実験機能も含まれています。</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/guide-overview">ページビルダー</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite">URL の書き換え</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/staging/content-staging">コンテンツのステージング</a></td>
            <td rowspan="2"><a href="../catalog-service/overview.md">カタログサービス</a></td>
            <td rowspan="2">カタログデータを管理し、製品関連のストアフロントエクスペリエンスをレンダリングするための、機能豊富なビューモデル（読み取り専用）サービス。</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser">ビジュアルマーチャンダイザー</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/payments/payments">支払額</a></td>
            <td><a href="../payment-services/guide-overview.md">支払いサービス</a></td>
            <td>安全かつ効率的な取引を容易にする統合決済サービス。</td>
        </tr>
    </tbody>
</table>

## 拡張機能とプラットフォーム機能

次の表に、プラットフォームの機能と拡張機能を比較します。この表を使用すると、違いを理解し、実装開始前にビジネス要件に最適なモデルを見極めるために役立つ、情報に基づいた決定を下すことができます。

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
            <td>B2B 機能</td>
            <td>インストール後に利用可能な完全な B2B 機能</td>
            <td>コア B2B 機能と共にプリインストール <sup>1</sup></td>
        </tr>
        <tr>
            <td>実験</td>
            <td>特定の層用のアドオン</td>
            <td>エンゲージメントとコンバージョンを最適化する A/B テスト</td>
        </tr>
        <tr>
            <td>機能とセキュリティの更新</td>
            <td>手動でのアップグレードとパッチ適用が必要</td>
            <td>自動的にデプロイ</td>
        </tr>
        <tr>
            <td>ホスティングインフラストラクチャ</td>
            <td>シングルテナント</td>
            <td>マルチテナント</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Commerce Admin のカスタマイズ</strong></td>
        </tr>
        <tr>
            <td>拡張可能なコア管理画面</td>
            <td>完全なレイアウトと機能のカスタマイズ</td>
            <td>プリセットフィルター、表示コントロール</td>
        </tr>
        <tr>
            <td>拡張可能な新しい管理画面</td>
            <td>標準の管理 UI 統合と外部アプリ挿入（管理 UI SDK）</td>
            <td>外部アプリの挿入（管理 UI SDK）</td>
        </tr>
        <tr>
            <td>カスタマイズ可能な管理テーマ</td>
            <td>拡張可能なテーマ設定フレームワーク</td>
            <td>テーマ設定フレームワークがありません</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>拡張性</strong></td>
        </tr>
        <tr>
            <td>拡張モデル</td>
            <td>プロセス内（PHP のカスタマイズ）およびプロセス外（API、イベント、App Builder）</td>
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
            <td>コアおよび B2B エンティティ <sup>2</sup> のカスタム属性</td>
        </tr>
        <tr>
            <td>技術</td>
            <td>CSS, CLI, HTML, JS, PHP, XML</td>
            <td>CSS, CLI, HTML, JS, Node</td>
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
            <td>App Builder ステートライブラリ（ファイルのみ） <sup>3</sup></td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                <sup>1</sup> 会社の管理や見積りなどのコア <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/guide-overview">B2B 機能 </a> は、SaaS でそのまま使用できます。 ただし、業界固有のカスタマイズを行う場合は、実装に関する考慮事項も追加する必要があります。
                <br><br>
                <sup>2</sup> SaaS のデータモデル拡張機能は、B2B エンティティを含め、製品および顧客を超える <a href="https://developer.adobe.com/commerce/webapi/graphql/schema/attributes/mutations/"> コアエンティティの拡張 </a> をサポートします。 ただし、業界固有のデータモデル（ディーラー固有の属性など）を使用するには、アーキテクチャに関する追加の考慮事項が必要になる場合があります。
                <br><br>
                <sup>3</sup> Adobeは、SaaS に対する永続的なストレージニーズに対応するために、Document DB 統合を積極的に取り組んでいます。 現在、長期的なデータストレージを必要とする実装では、追加のインフラストラクチャのプロビジョニングと保守が必要になる場合があります。
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
>- API 機能を拡張するには、API メッシュを検討してください。
>- Adobeの継続的なプラットフォーム進化と新機能リリースを監視します。
>- 使用可能な拡張オプションに照らして、業界固有のデータモデル要件を評価します。
>- [ チャネルとポリシーを活用したマーチャンダイジングサービス ](../optimizer/setup/catalog-view.md) の採用を検討します。
