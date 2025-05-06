---
title: オンボーディングとインストール
description: インストール方法を説明しま  [!DNL Catalog Service]。
exl-id: 3f8492c3-f76d-49b7-a201-35deace36a1d
badgePaas: label="PaaS のみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeが管理する PaaS インフラストラクチャ）およびオンプレミスプロジェクトにのみ適用されます。"
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%

---

# オンボーディングとインストール

カタログサービスをインストールし、[Catalog Service GraphQL API](https://developer.adobe.com/commerce/services/graphql/catalog-service/) を使用してCommerce インスタンスから商品データをリクエストし、受け取ります。 カタログサービスは、repo.magento.com リポジトリからコンポーザメタパッケージとして提供されます。

>[!NOTE]
>
>Commerce インスタンスで Live Search または Product Recommendations を使用している場合、サービスのオンボーディングまたはアップグレードの際に、カタログサービスが自動的にインストールまたは更新されます。 詳しくは、[Live Search](https://experienceleague.adobe.com/en/docs/commerce/live-search/install) および [Product Recommendations](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/getting-started/install-configure) のインストール手順を参照してください。



## 必要システム構成

**ソフトウェア要件**

- Adobe Commerce 2.4.4 以降
- PHP 8.1、8.2、8.3、8.4
- コンポーザー：2.x

**サポートされているプラットフォーム**

- クラウドインフラストラクチャー上のAdobe Commerce:2.4.4 以降
- Adobe Commerce オンプレミス：2.4.4 以降

## エンドポイント

[!DNL Catalog Service] には、オンボーディングに使用できる 2 つのエンドポイントがあります。

- サンドボックス（`https://catalog-service-sandbox.adobe.io/graphql`） – 運用開始前のテストと検証に使用
- 実稼動（`https://catalog-service.adobe.io/graphql`） - Commerceのマーチャントおよび web サイトのライブトラフィックに使用します。

すべてのCommerce テストインスタンスは、サンドボックス エンドポイントを使用します。

サンドボックスエンドポイントですべての負荷テストを実行します。 負荷テストを開始する前に、[ サポートチケット ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) を送信して、サービスチームが追加のサーバートラフィックを予測できるようにします。

## インストールと設定

Adobe Commerceの [!DNL Catalog Service] を使い始めるには、次の手順が必要です。

- カタログサービス拡張機能（`magento/catalog-service`）のインストール
- サービスとデータの書き出しの設定
- サービスへのアクセス

### カタログサービス拡張機能のインストール

>[!BEGINSHADEBOX]

**前提条件**

- [repo.magento.com](https://repo.magento.com) にアクセスして、拡張機能をインストールします。 キーの生成と必要な権限の取得については、[ 認証キーの取得 ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) を参照してください。 クラウドインストールについては、[Commerce on Cloud Infrastructure ガイドを参照してください ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/authentication-keys)

- Adobe Commerce アプリケーションサーバーのコマンドラインにアクセスします。

>[!ENDSHADEBOX]

Adobe Commerce バージョン 2.4.4 以降が稼働しているAdobe Commerce インスタンスに、最新バージョンのカタログサービス拡張機能（`magento/catalog-service`）をインストールします。 カタログサービスは、[repo.magento.com](https://repo.magento.com) リポジトリからコンポーザメタパッケージとして提供されます。

>[!BEGINTABS]

>[!TAB  クラウドインフラストラクチャ ]

このメソッドを使用して、Commerce Cloud インスタンスの [!DNL Catalog Service] をインストールします。

1. ローカルワークステーションで、Adobe Commerce on cloud infrastructure プロジェクトのプロジェクトディレクトリに移動します。

   >[!NOTE]
   >
   >Commerce Adobe Commerce プロジェクト環境のローカル管理について詳しくは、_クラウドインフラストラクチャユーザーガイドの [CLI を使用したブランチの管理 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches) を参照してください_。

1. Adobe Commerce Cloud CLI を使用して更新する環境ブランチを確認します。

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. カタログサービスモジュールを追加します。

   ```bash
   composer require magento/catalog-service --no-update
   ```

1. パッケージの依存関係を更新します。

   ```bash
   composer update "magento/catalog-service"
   ```

1. `composer.json` ファイルと `composer.lock` ファイルのコード変更をコミットしプッシュします。

1. `composer.json` ファイルと `composer.lock` ファイルのコード変更を追加、コミットし、クラウド環境にプッシュします。

   ```shell
   git add -A
   git commit -m "Add catalog service module"
   git push origin <branch-name>
   ```

   アップデートをクラウド環境にプッシュすると、[Commerce クラウドデプロイメントプロセスが開始され ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/process) 変更が適用されます。 [ デプロイメントログ ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log) からデプロイメントステータスを確認します。

>[!TAB  オンプレミス ]

オンプレミスのインスタンスに [!DNL Catalog Service] をインストールするには、この方法を使用します。

1. Composer を使用して、Catalog Service モジュールをプロジェクトに追加します。

   ```bash
   composer require magento/catalog-service --no-update
   ```

1. 依存関係を更新し、拡張機能をインストールします。

   ```bash
   composer update  "magento/catalog-service"
   ```

1. Adobe Commerceをアップグレード :

   ```bash
   bin/magento setup:upgrade
   ```

1. キャッシュをクリアする：

   ```bash
   bin/magento cache:clean
   ```

   >[!TIP]
   >
   >場合によっては（特に実稼動環境にデプロイする場合）、コンパイル済みのコードは時間がかかるので、クリアしないようにしたい場合があります。 変更を加える前に、システムを必ずバックアップしてください。

>[!ENDTABS]

### サービスとデータの書き出しの設定

[!DNL Catalog Service] をインストールしたら、次のタスクを実行してカタログサービスをAdobe Commerce インスタンスに統合します。 この統合により、Commerce インスタンス、カタログサービスおよびその他のサポートサービス間のデータ同期と通信が可能になります。 データ同期は、[SaaS データ書き出し拡張機能 ](../data-export/overview.md) で処理されます。

1. API キーを指定し、SaaS データ空間を選択して [&#128279;](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas)0&rbrace;Commerce サービスコネクタ &rbrace; を設定します。

   Commerce Services Connector のセットアップは、カタログサービス、ライブ検索、商品レコメンデーションなどのAdobe Commerce サービスを使用するために必要な 1 回限りのプロセスです。 別のサービス用にコネクタを既に設定している場合は、この手順をスキップします。

1. [ データ管理ダッシュボード ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard) から初期データ同期を実行します。

   カタログのサイズに応じて、最初の同期に数分から数時間かかる場合があります。 同期ステータスは、データ管理ダッシュボードから監視できます。 最初の同期の後、カタログは、サービスを最新の状態に保つために、継続的に製品データを書き出します。

   >[!NOTE]
   >
   >Commerce CLI を使用して、コマンドラインから初期同期を開始することもできます。 [SaaS データ書き出しガイド ](../data-export/data-export-cli-commands.md#initial-sync) の _初期同期_ を参照してください。

カタログの書き出しが正しく実行されていることを確認するには：

- [cron ジョブが実行中であることを確認 ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues)
- インデクサーが [ 管理者 ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) から、またはCommerce CLI コマンド `bin/magento indexer:info` ールを使用して実行されていることを確認します。
- `Catalog Attributes Feed, Product Feed, Product Overrides Feed` と `Product Variant Feed` のインデクサーが `Update by Schedule` に設定されていることを確認します。

### データ同期の監視とトラブルシューティング

Commerce Admin から、[Data Management Dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard) を使用して同期プロセスを監視できます。 [Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting) とログを使用して、プロセスの管理とトラブルシューティングを行います。

### サービスへのアクセス

[!DNL Catalog Service] GraphQL API には、` https://catalog-service.adobe.io/graphql` エンドポイントから HTTPS 経由で POST コマンドを使用してアクセスできます。

GraphQL クエリでは、管理者でAdobe Commerce サービスコネクタ設定に追加した公開 API キーを含む、複数の HTTP ヘッダーを指定する必要があります。 詳しくは、[ ストアフロントサービスGraphQL](https://developer.adobe.com/commerce/services/graphql/) ドキュメントを参照してください。

### ファイアウォール設定

ファイアウォールを通過する [!DNL Catalog Service] を許可するには、`commerce.adobe.io` を許可リストに追加します。

## カタログサービスと API メッシュ

Adobe Developer App Builderの [API メッシュ ](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) を使用すると、デベロッパーはAdobe IO を使用して、プライベートまたはサードパーティの API およびその他のインターフェイスをAdobe製品と統合できます。

インストールと設定について詳しくは、[[!DNL Catalog Service]  および API メッシュ ](mesh.md) に関するトピックを参照してください。

## データ管理ダッシュボード

データの同期について詳 [!DNL Catalog Service] くは、[ データ管理ダッシュボード ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard) を参照してください。
