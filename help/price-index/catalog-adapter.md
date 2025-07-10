---
title: カタログ アダプタ拡張
description: カタログアダプターを使用したCommerce Services からの価格のレンダリング
seo-title: Catalog Adapter Extension
seo-description: Using Catalog Adapter to render prices from Commerce Services
exl-id: e42101fa-9c30-482c-a649-44dc35376abb
source-git-commit: 74f6cb64724194651c4eeb538c0c69142b01ac5d
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# カタログアダプタ

`[!DNL Catalog Adapter]` 拡張機能は、Commerce アプリケーションに含まれているデフォルトの製品価格インデクサーを無効にし、代わりに [ カタログサービス ](../catalog-service/overview.md) から提供される価格を使用します。

このアダプタは、[SaaS データ書き出し ](../data-export/overview.md) およびAdobe Commerce サービスで動作するように設計されています。 SaaS データのエクスポートは価格の送信を担当し、[!DNL Catalog Adapter] はAdobe Commerceサービスからすべての価格を取得します。

[!DNL Catalog Adapter] を有効にすると、価格のインデックス作成と操作が次のような影響を受けます。

- Adobe Commerce アプリケーションに含まれる価格インデクサーが無効になっています。
- 価格は、SaaS データのエクスポートと [SaaS 価格インデクサー ](price-indexing.md) を使用して管理されます。
- お客様が商品や商品の価格を表示するページを開くと、その価格はAdobe Commerce サービスから取得されます。
- 価格は、[SaaS データ書き出し ](../data-export/overview.md) からのデータを同期してAdobe Commerce サービスに送信されます。
- チェックアウトでは価格が動的に再計算されます。

カタログアダプタ拡張機能を削除または無効にすることで、Commerce アプリケーションで価格インデックスを再度有効にすることができます。

## 要件

- Adobe Commerce 2.4.4 以降
- Adobe Commerce環境で、次のCommerce サービスのいずれかが有効になり設定されている必要があります。

   - [Live Search](../live-search/install.md)
   - [製品レコメンデーション](../product-recommendations/install-configure.md)
   - [カタログサービス](../catalog-service/installation.md)

## インストール

カタログ アダプタ拡張機能は、次のモジュールをインストールする Composer メタパッケージです。

- **Price Indexer Disabler**-Commerce アプリケーションの価格インデックスを無効にして、SaaS 価格インデックスを使用して価格が配信されるようにします。 SaaS 価格インデックス作成拡張機能がインストールされている場合、Commerce アプリケーションの製品価格インデックス作成を有効にすることはできません。
- **価格プロバイダー**-Adobe Commerce サービスの商品の価格を提供します。 検索クエリを作成し、フロントエンドの製品の価格を取得します。
- **カタログサービス検索アダプター** – 商品検索リクエストに応じて、Adobe Commerce アプリケーションからAdobe Commerce サービスに価格を転送します。

## インストール手順

>[!BEGINTABS]

>[!TAB  クラウドインフラストラクチャ ]

このメソッドを使用して、Commerce Cloud インスタンスの [!DNL Catalog Adapter] をインストールします。

1. ローカルワークステーションで、Adobe Commerce on cloud infrastructure プロジェクトのプロジェクトディレクトリに移動します。

   >[!NOTE]
   >
   >Commerce Adobe Commerce プロジェクト環境のローカル管理について詳しくは、[ クラウドインフラストラクチャユーザーガイドの ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches)CLI を使用したブランチの管理 _を参照してください_。

1. Adobe Commerce Cloud CLI を使用して更新する環境ブランチを確認します。

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. カタログアダプタモジュールを追加します。

   ```bash
   composer require magento/catalog-adapter --no-update
   ```

1. パッケージの依存関係を更新します。

   ```bash
   composer update "magento/catalog-adapter"
   ```

1. `composer.json` ファイルと `composer.lock` ファイルのコード変更をコミットしプッシュします。

1. `composer.json` ファイルと `composer.lock` ファイルのコード変更を追加、コミットし、クラウド環境にプッシュします。

   ```shell
   git add -A
   git commit -m "Add catalog adapter module"
   git push origin <branch-name>
   ```

   アップデートをクラウド環境にプッシュすると、[Commerce クラウドデプロイメントプロセスが開始され ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/process) 変更が適用されます。 [ デプロイメントログ ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log) からデプロイメントステータスを確認します。

>[!TAB  オンプレミス ]

オンプレミスのインスタンスに [!DNL Catalog Adapter] をインストールするには、この方法を使用します。

1. Composer を使用して、プロジェクトにカタログアダプタを追加します。

   ```bash
   composer require magento/catalog-adapter --no-update
   ```

1. 依存関係を更新し、拡張機能をインストールします。

   ```bash
   composer update  "magento/catalog-adapter"
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


## Adobe Commerce製品価格インデクサーを再度有効にします。

デフォルトのAdobe Commerce product price indexer に依存するサードパーティアプリケーションがある場合は、次のコマンドを使用して再度有効にすることができます。

```bash
# re-enable Product Price indexer
bin/magento module:disable Magento_PriceIndexerDisabler
# re-index Product Price indexer
bin/magento index:reindex catalog_product_price
```

## ヘッドレスストアフロントシナリオに対する製品価格インデクサーの無効化

ヘッドレス Commerce インスタンスがある場合は、Adobe Commerce product price indexer を無効にして、Adobe Commerce インスタンスの負荷を軽減する必要がある場合があります。 `magento/module-price-indexer-disabler` モジュールをインストールすると、このタスクを完了できます。

```bash
composer require magento/module-price-indexer-disabler
```

## 使用シナリオ

一般的な `[!DNL Catalog Adapter]` シナリオを次に示します。

### Adobe Commerce product price indexer に依存しない

- 必要なサービス（ライブ検索、商品レコメンデーション、カタログサービス）がインストールされている Luma またはAdobe Commerce Core GraphQL マーチャントです
- Adobe Commerce product price indexer に依存するサードパーティの拡張機能との統合はありません。

1. [!DNL Catalog Adapter] のインストール

### Adobe Commerce product price indexer に依存する

- サポートされているサービス（ライブ検索、商品レコメンデーション、カタログサービス）がインストールされている Luma またはAdobe Commerce Core GraphQL マーチャントです
- Adobe Commerce product price indexer に基づくサードパーティの拡張機能を使用します。

1. [!DNL Catalog Adapter] のインストール
1. デフォルトのAdobe Commerce製品価格インデクサーを再度有効にします。

### ヘッドレス Commerce インスタンス

- 必要なサービス（ライブ検索、商品レコメンデーション、カタログサービス）がインストールされたヘッドレス Commerce インスタンスを持つマーチャント
- デフォルトのAdobe Commerce製品価格インデクサーに依存しない

1. `magento/module-price-indexer-disabler` パッケージから [!DNL Catalog Adapter] モジュールをインストールします。
