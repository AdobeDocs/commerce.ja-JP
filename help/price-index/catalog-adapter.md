---
title: カタログアダプタ拡張機能
description: カタログアダプタを使用したCommerce サービスからの価格のレンダリング
seo-title: Catalog Adapter Extension
seo-description: Using Catalog Adapter to render prices from Commerce Services
exl-id: e42101fa-9c30-482c-a649-44dc35376abb
TQID: https://experienceleague.adobe.com/WnL4dJbZV0acHT5kpEAOyTVjhzW23RjHbQFVdDl4HDk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 758
ht-degree: 0%

---

# カタログアダプタ

`[!DNL Catalog Adapter]`拡張機能は、Commerce アプリケーションに含まれるデフォルトの製品価格インデクサーを無効にし、代わりに[&#x200B; カタログサービス &#x200B;](../catalog-service/overview.md)が提供する価格を使用します。

アダプターは、[SaaS データ書き出し](../data-export/overview.md)およびAdobe Commerce サービスと連携するように設計されています。 SaaS データ書き出しは価格の送信を担当し、[!DNL Catalog Adapter]はAdobe Commerce サービスからすべての価格を取得します。

[!DNL Catalog Adapter]を有効にすると、価格インデックスと操作は次の方法で影響を受けます。

- Adobe Commerce アプリケーションに含まれている価格インデクサーが無効になっています。
- 価格は、SaaS データの書き出しと[SaaS価格インデクサー](price-indexing.md)を使用して管理されます。
- お客様が商品、カテゴリ、または商品の価格を表示するその他のページを開くと、価格はAdobe Commerce サービスから取得されます。
- 価格は、[SaaS データ書き出し](../data-export/overview.md)からのデータを同期してAdobe Commerce サービスに送信されます。
- チェックアウトでは、価格が動的に再計算されます。

カタログアダプタ拡張機能を削除または無効にすることで、Commerce アプリケーションで価格インデックスを再度有効にできます。

## 要件定義

- Adobe Commerce 2.4.4以降
- Adobe Commerce環境では、次のいずれかのCommerce サービスを有効にして設定する必要があります。

   - [ライブサーチ](../live-search/install.md)
   - [商品レコメンデーション](../product-recommendations/install-configure.md)
   - [カタログサービス](../catalog-service/installation.md)

## インストール

Catalog Adapter拡張機能は、次のモジュールをインストールするComposer メタパッケージです。

- **価格インデクサー無効化** – このモジュールは、Commerce アプリケーションの価格インデックスを無効化して、価格がSaaS価格インデックスを介して配信されるようにします。 SaaS価格インデックス拡張機能がインストールされている場合、Commerce アプリケーションの製品価格インデックスをオンにすることはできません。
- **価格プロバイダー** – このモジュールは、Adobe Commerce サービスの商品の価格を提供します。 検索クエリを形成し、フロントエンドの商品の価格を取得します。
- **カタログサービス検索アダプタ** – このモジュールは、商品検索リクエストに応じて、Adobe Commerce アプリケーションからAdobe Commerce サービスに価格を転送します。

## インストール手順

>[!BEGINTABS]

>[!TAB  クラウド インフラストラクチャ ]

Commerce Cloud インスタンスの[!DNL Catalog Adapter]をインストールするには、この方法を使用します。

1. ローカルワークステーションで、Adobe Commerce on cloud infrastructure プロジェクトのプロジェクトディレクトリに移動します。

   >[!NOTE]
   >
   >Commerce プロジェクト環境のローカル管理について詳しくは、_Adobe Commerce on Cloud Infrastructure ユーザーガイド_&#x200B;の「[CLIを使用した分岐の管理](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches)」を参照してください。

1. Adobe Commerce Cloud CLIを使用して更新する環境ブランチを確認します。

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. カタログアダプターモジュールを追加します。

   ```bash
   composer require magento/catalog-adapter --no-update
   ```

1. パッケージの依存関係を更新します。

   ```bash
   composer update "magento/catalog-adapter"
   ```

1. `composer.json`および`composer.lock` ファイルのコード変更をコミットしてプッシュします。

1. `composer.json`および`composer.lock` ファイルのコード変更を追加、コミット、クラウド環境にプッシュします。

   ```shell
   git add -A
   git commit -m "Add catalog adapter module"
   git push origin <branch-name>
   ```

   更新をクラウド環境にプッシュすると、[Commerce クラウド デプロイメント プロセス &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/process)が開始され、変更が適用されます。 [&#x200B; デプロイ ログ &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log)のデプロイメント ステータスを確認します。

>[!TAB  オンプレミス ]

オンプレミス インスタンスの[!DNL Catalog Adapter]をインストールするには、この方法を使用します。

1. Composerを使用してプロジェクトにカタログアダプタを追加します。

   ```bash
   composer require magento/catalog-adapter --no-update
   ```

1. 依存関係を更新し、拡張機能をインストールします。

   ```bash
   composer update  "magento/catalog-adapter"
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


## Adobe Commerce製品価格インデクサーを再度有効にする

デフォルトのAdobe Commerce製品価格インデクサーに依存するサードパーティアプリケーションがある場合は、次のコマンドを使用して再度有効にできます。

```bash
# re-enable Product Price indexer
bin/magento module:disable Magento_PriceIndexerDisabler
# re-index Product Price indexer
bin/magento index:reindex catalog_product_price
```

## ヘッドレスストアフロントシナリオの製品価格インデクサーを無効にする

ヘッドレス Commerce インスタンスを使用している場合は、Adobe Commerce インスタンスの負荷を軽減するために、Adobe Commerce製品価格インデクサーを無効にする必要がある場合があります。 このタスクは、`magento/module-price-indexer-disabler` モジュールをインストールすることで完了できます。

```bash
composer require magento/module-price-indexer-disabler
```

## 使用シナリオ

`[!DNL Catalog Adapter]`の一般的なシナリオを次に示します。

### Adobe Commerce製品価格インデクサーに依存しない

- 必要なサービス（ライブサーチ、商品レコメンデーション、カタログサービス）がインストールされているLumaまたはAdobe Commerce Core GraphQLのマーチャント
- Adobe Commerceの製品価格インデックスに依存するサードパーティ製の拡張機能との統合はありません

1. [!DNL Catalog Adapter]をインストールします。

### Adobe Commerce製品価格インデクサーへの依存

- サポート対象のサービス（ライブサーチ、商品レコメンデーション、カタログサービス）がインストールされているLumaまたはAdobe Commerce Core GraphQLのマーチャント
- Adobe Commerceの商品価格インデクサーに依存するサードパーティ製の拡張機能を使用している

1. [!DNL Catalog Adapter]をインストールします。
1. デフォルトのAdobe Commerce製品価格インデクサーを再度有効にします。

### ヘッドレス Commerce インスタンス

- 必要なサービス（ライブサーチ、商品レコメンデーション、カタログサービス）がインストールされたヘッドレスCommerceインスタンスを持つマーチャント
- デフォルトのAdobe Commerce製品価格インデクサーに依存しない

1. [!DNL Catalog Adapter] パッケージから`magento/module-price-indexer-disabler` モジュールをインストールします。
