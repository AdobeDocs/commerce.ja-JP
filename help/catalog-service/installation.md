---
title: インストール
description: ' [!DNL Catalog Service]のインストール方法を学ぶ'
exl-id: 3f8492c3-f76d-49b7-a201-35deace36a1d
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
source-git-commit: 4b6cd45737fa6c3917670d6b66e6849aece39a25
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 0%

---

# オンボーディングとインストール

{{aco-merchandising-services}}

カタログサービスをインストールして、[&#x200B; カタログサービス GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)を使用してCommerce インスタンスから製品データをリクエストおよび受信します。 カタログサービスは、repo.magento.com リポジトリからコンポーザーPHP メタパッケージとして配信されます。

>[!NOTE]
>
>Commerce インスタンスでライブサーチまたは商品レコメンデーションを使用している場合、カタログサービスは、これらのサービスのオンボーディングまたはアップグレード時に自動的にインストールまたは更新されます。 詳しくは、[Live Search](https://experienceleague.adobe.com/ja/docs/commerce/live-search/install)および[製品レコメンデーション &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/product-recommendations/getting-started/install-configure)のインストール手順を参照してください。
>
>Adobe Commerce as a Cloud Serviceを使用している場合は、ご使用の環境で最新バージョンのメタパッケージを利用できます。 サービスの使用を開始するには、[&#x200B; カタログサービスの概要](get-started.md)を参照してください。
>
>Adobe Commerce Optimizerを使用したCommerce ストアフロントの実装については、[&#x200B; マーチャンダイジングサービス開発者ガイド &#x200B;](https://developer-stage.adobe.com/commerce/services/optimizer/)を参照してください。


## 必要システム構成

**必要ソフトウェア構成**

- Adobe Commerce 2.4.4以降
- PHP 8.1、8.2、8.3、8.4
- コンポーザー：2.x

**サポートされているプラットフォーム**

- Adobe Commerce on cloud インフラストラクチャ：2.4.4以降
- Adobe Commerce オンプレミス：2.4.4以降

## エンドポイント

[!DNL Catalog Service]には、オンボーディングに使用できる2つのエンドポイントがあります。

- サンドボックス （`https://catalog-service-sandbox.adobe.io/graphql`） – 本番稼働前のテストと検証に使用
- 実稼動（`https://catalog-service.adobe.io/graphql`） - Commerce マーチャントおよびweb サイトのライブトラフィックに使用されます

すべてのCommerce テストインスタンスは、サンドボックスエンドポイントを使用します。

サンドボックスエンドポイントですべての読み込みテストを実行します。 読み込みテストを開始する前に、[&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=ja#submit-ticket)を送信して、サービスチームが追加のサーバートラフィックを予測できるようにします。

## インストールと設定

Adobe Commerceの[!DNL Catalog Service]を使い始めるには、次の手順が必要です。

- カタログサービス拡張機能（`magento/catalog-service`）をインストールします
- サービスとデータ書き出しの設定
- サービスへのアクセス

### カタログサービス拡張機能のインストール

>[!BEGINSHADEBOX]

**前提条件**

- [repo.magento.com](https://repo.magento.com)にアクセスして、拡張機能をインストールします。 キーの生成と必要な権限の取得については、[認証キーの取得](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)を参照してください。 クラウドインストールについては、[Commerce on Cloud Infrastructure Guide](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/authentication-keys)を参照してください

- Adobe Commerce アプリケーションサーバーのコマンドラインにアクセスします。

>[!ENDSHADEBOX]

Adobe Commerce バージョン 2.4.4以降を実行しているAdobe Commerce インスタンスに、最新バージョンのカタログサービス拡張機能（`magento/catalog-service`）をインストールします。 カタログサービスは、[repo.magento.com](https://repo.magento.com) リポジトリからコンポーザーのメタパッケージとして配信されます。

>[!BEGINTABS]

>[!TAB  クラウド インフラストラクチャ ]

Commerce Cloud インスタンスの[!DNL Catalog Service]をインストールするには、この方法を使用します。

1. ローカルワークステーションで、Adobe Commerce on cloud infrastructure プロジェクトのプロジェクトディレクトリに移動します。

   >[!NOTE]
   >
   >Commerce プロジェクト環境のローカル管理について詳しくは、[Adobe Commerce on Cloud Infrastructure ユーザーガイド &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/cli-branches)の「_CLIを使用した分岐の管理_」を参照してください。

1. Adobe Commerce Cloud CLIを使用して更新する環境ブランチを確認します。

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

1. `composer.json`および`composer.lock` ファイルのコード変更を追加、コミット、クラウド環境にプッシュします。

   ```shell
   git add -A
   git commit -m "Add catalog service module"
   git push origin <branch-name>
   ```

   更新をクラウド環境にプッシュすると、[Commerce クラウド デプロイメント プロセス &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/deploy/process)が開始され、変更が適用されます。 [&#x200B; デプロイ ログ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log)のデプロイメント ステータスを確認します。

>[!TAB  オンプレミス ]

オンプレミス インスタンスの[!DNL Catalog Service]をインストールするには、この方法を使用します。

1. Composerを使用して、カタログサービスモジュールをプロジェクトに追加します。

   ```bash
   composer require magento/catalog-service --no-update
   ```

1. 依存関係を更新し、拡張機能をインストールします。

   ```bash
   composer update  "magento/catalog-service"
   ```

1. Adobe Commerceのアップグレード：

   ```bash
   bin/magento setup:upgrade
   ```

1. キャッシュをクリアします。

   ```bash
   bin/magento cache:clean
   ```

   >[!TIP]
   >
   >場合によっては、特に実稼動環境にデプロイする場合は、コンパイル済みコードの消去は時間がかかることがあるため、避けた方がよいでしょう。 変更を加える前に、システムを必ずバックアップしてください。

>[!ENDTABS]

### サービスとデータ書き出しの設定

[!DNL Catalog Service]をインストールしたら、次のタスクを実行して、カタログサービスをAdobe Commerce インスタンスと統合します。 この統合により、Commerce インスタンス、カタログサービス、およびその他のサポートサービス間のデータ同期と通信が可能になります。 データの同期は、[SaaS データ書き出し拡張機能](../data-export/overview.md)によって処理されます。

1. API キーを指定し、SaaS データスペースを選択して、[Commerce サービスコネクタ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/user-guides/integration-services/saas)を設定します。

   Commerce Services Connectorの設定は、カタログサービス、ライブサーチ、商品レコメンデーションなどのAdobe Commerce サービスを使用するために必要な1回限りのプロセスです。 別のサービス用にコネクタを既に設定している場合は、この手順をスキップしてください。

1. [&#x200B; データ管理ダッシュボード &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)から最初のデータ同期を実行します。

   カタログのサイズによっては、最初の同期に数分から数時間かかる場合があります。 同期ステータスは、データ管理ダッシュボードから監視できます。 最初の同期後、カタログは継続的に製品データを書き出して、サービスを最新の状態に保ちます。

   >[!NOTE]
   >
   >また、Commerce CLIを使用して、コマンドラインから最初の同期を開始することもできます。 [SaaS データ書き出しガイド &#x200B;](../data-export/data-export-cli-commands.md#initial-sync)の&#x200B;_初期同期_&#x200B;を参照してください。

カタログの書き出しが正しく実行されていることを確認するには：

- [cron ジョブが実行中であることを確認します](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues)。
- インデックスが[管理者](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/tools/index-management)から実行されているか、またはCommerce CLI コマンド `bin/magento indexer:info`を使用して実行されていることを確認します。
- `Catalog Attributes Feed, Product Feed, Product Overrides Feed`および`Product Variant Feed`のインデクサーが`Update by Schedule`に設定されていることを確認します。

### データ同期の監視とトラブルシューティング

Commerce Adminから、[Data Management Dashboard](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)を使用して同期プロセスをモニターできます。 [Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting)とログを使用して、プロセスの管理とトラブルシューティングを行います。
