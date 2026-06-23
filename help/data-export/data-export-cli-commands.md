---
title: Commerce CLIを使用したフィードの同期
description: Commerce CLI コマンドを使用して、Adobe Commerce SaaS サービスの [!DNL data export extension] のフィードと同期プロセスを管理する方法を説明します。
autotag-review: '2026-06-17T15:08:59.000Z'
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
TQID: 'https://experienceleague.adobe.com/Vi8hMKOBjTPkSQp0t8DCkjZsJ8s3Q5GSbSXyX2gmWRo'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: ef1a9efc579d8d21c145e6981235489a2e4ea203
workflow-type: tm+mt
source-wordcount: 728
ht-degree: 0%

---

# Commerce CLIを使用したフィードの同期

`magento/saas-export` パッケージの`saas:resync` コマンドを使用すると、[!DNL Adobe Commerce] SaaS サービスのデータ同期を管理できます。

>[!NOTE]
>
>`saas:resync` コマンドは、`products`、`categories`、`priceBooks`などの[!DNL Adobe Commerce Optimizer Connector] フィードにも適用されます。 コネクタフィードとインデクサー名の完全なリストについては、[&#x200B; サポートされているフィード &#x200B;](../aco-connector/reference/connector-reference.md#supported-feeds)を参照してください。

Adobeでは、`saas:resync` コマンドを定期的に使用することはお勧めしません。 コマンドを使用するための一般的なシナリオは次のとおりです。

- 初期同期
- [SaaS データスペース ID](https://experienceleague.adobe.com/ja/docs/commerce-admin/config/services/saas)を変更した後、データを新しいデータスペースに同期する
- トラブルシューティング

`var/log/saas-export.log` ファイルの同期操作を監視します。

## 初期同期

>[!NOTE]
>
>ライブサーチまたは商品レコメンデーションが有効になっている場合、初期同期が自動的に実行されます。 手動コマンドは必要ありません。
>
>[!DNL Adobe Commerce Optimizer Connector]回のデプロイメントの場合、`aco:config:init` コマンドは、すべてのコネクタフィードのインデクサーを無効にすることで、最初の完全な同期をスケジュールします。 [同期を有効にする [!DNL Commerce Optimizer] 統合](../aco-connector/get-started.md#enable-the-adobe-commerce-optimizer-integration)および[同期を [!DNL Commerce Optimizer]](../aco-connector/data-sync-manage.md)に管理するを参照してください。

コマンドラインから`saas:resync`をトリガーする場合、カタログのサイズに応じて、データを更新するのに数分から数時間かかる場合があります。

フィード同期は任意の順序で実行できます。それらの間にはハード依存関係はありません。 次のシーケンスは、最初にスコープデータから始まります。これは、スコープが他のフィードが参照するストアビューを定義するため、論理的な出発点となります。

```shell
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed productAttributes
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed products
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed productoverrides
```

>[!NOTE]
>
>環境では、このシーケンスにすべてのフィードが含まれない場合があります。 完全なフィード リスト、CLI フィード名、およびモジュール要件については、[&#x200B; サポートされているフィード &#x200B;](reference/feed-table-reference.md#supported-feeds)を参照してください。

## コマンドオプション

`saas:resync` コマンドは、様々な同期操作をサポートしています。

- SKUによる部分同期
- 中断された同期を再開
- 同期せずにデータを検証

すべてのコマンドオプションとフラグを表示します。

```shell
bin/magento saas:resync --help
```

例を使用したオプションの説明については、次の節を参照してください。

>[!NOTE]
>
>書き出し処理を管理するための詳細なオプションについては、[書き出し処理のカスタマイズ &#x200B;](customize-export-processing.md)を参照してください。

## `--feed`

必須。 再同期するフィード エンティティを指定します。

`bin/magento saas:resync --help`件のドキュメントのコマンド オプションとフラグ。 環境内で使用可能なすべてのフィードが一覧表示されるわけではありません。 CLI フィード名、インデクサーID、フィード テーブルを含む完全なフィード リストについては、[&#x200B; サポートされているフィード &#x200B;](reference/feed-table-reference.md#supported-feeds)を参照してください。

>[!NOTE]
>
>インストールされているモジュールによって、再同期できるフィードが決まります。 例えば、`productOverrides`にはクラウド、オンプレミス、またはCommerce as a Cloud Serviceの[!DNL Adobe Commerce]が必要であり、`orders`には受注モジュールが必要です。

>[!NOTE]
>
>`saas:resync` コマンドは、新しい項目、更新された項目、以前に書き出せなかった項目のみを送信します。 前回の書き出し以降にコンテンツハッシュが変更されていない項目はスキップされます。

**例：**

```shell
bin/magento saas:resync --feed products
```

## `--by-ids`

IDによって特定のエンティティの一部を再同期します。 `products`、`productAttributes`、`productOverrides`、`inventoryStockStatus`、`prices`、`variants`および`categoryPermissions` フィードをサポートしています。

デフォルトでは、`--by-ids` オプションを使用する場合、製品SKU値を使用して値を指定します。 代わりに製品IDを使用するには、`--id-type=productId` オプションを追加します。

>[!NOTE]
>
>標準の再同期とは異なり、`--by-ids`はハッシュ検証を回避し、最後の書き出し以降にコンテンツが変更されたかどうかに関係なく、指定されたエンティティを接続されたCommerce サービスに強制的に送信します。

**例：**

```shell
bin/magento saas:resync --feed products --by-ids='ADB102,ADB111,ADB112'

bin/magento saas:resync --feed products --by-ids='1,2,3' --id-type='productId'
```

## `--cleanup-feed`

SaaSにデータを再入力して送信する前に、フィード インデクサーテーブルをクリーンアップします。 `products`、`productAttributes`、`productOverrides`、`inventoryStockStatus`、`prices`、`variants`および`categoryPermissions`でのみサポートされています。

`--dry-run` オプションと共に使用すると、操作はすべての項目に対してドライ実行再同期操作を実行します。

>[!WARNING]
>
>`cleanup-feed` オプションで再同期コマンドを使用すると、ローカルフィードの書き出し状態がクリアされ、同期が不完全になる可能性があります。 例えば、[!DNL Adobe Commerce]でのエンティティの削除は、接続されたCommerce サービスに反映されない可能性があります。また、[!DNL Adobe Commerce]で削除または更新されたにもかかわらず、古いエンティティがリモート Commerce サービス インデックスに残る場合もあります。 このオプションは、SaaS データスペースのクリーンアップ後など、環境の完全な再構築に対してのみ使用します。

**例：**

```shell
bin/magento saas:resync --feed products --cleanup-feed
```

## `--continue-resync`

中断された再同期操作を再開します。 `products`、`productAttributes`、`productOverrides` フィードでのみサポートされています。

**例：**

```shell
bin/magento saas:resync --feed productAttributes --continue-resync
```

## `--dry-run`

フィードをSaaSに送信せず、フィードのテーブルに保存せずに、フィードの再インデックスプロセスを実行します。 このオプションは、データセットの問題を特定するのに便利です。

ペイロードを`var/log/saas-export.log`に保存する`EXPORTER_EXTENDED_LOG=1`環境変数を追加します。

**例：**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run
```

### 特定のフィード項目のテスト

特定のフィード項目をテストするには、拡張ログ コレクションに`--by-ids` オプションを追加して、`var/log/saas-export.log` ファイルで生成されたペイロードを確認します。

**例：**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run --by-ids='ADB102,ADB111,ADB112'
```

### すべてのフィード項目をテストする

デフォルトでは、`resync --dry-run`操作中に送信されたフィードには、新しい項目、または以前に書き出せなかった項目のみが含まれます。 処理するフィード内のすべての項目を含めるには、`--cleanup-feed` オプションを使用します。

**例：**

```shell
bin/magento saas:resync --feed products --dry-run --cleanup-feed
```

## `--no-reindex`

インデックス再作成せずに既存のカタログ データを[!DNL Commerce Services]に再送信します。 製品関連のフィードではサポートされていません。

動作は[書き出しモード &#x200B;](sync-overview.md#synchronization-modes)によって異なります。

- レガシーモード：すべてのデータを切り捨てずに再送信します。
- 即時モード：オプションは無視され、更新/失敗のみを同期します。

**例：**

```shell
bin/magento saas:resync --feed productAttributes --no-reindex
```

>[!MORELIKETHIS]
>
> - [&#x200B; ログを確認し、トラブルシューティング &#x200B;](troubleshooting/logging.md) — データ書き出しとSaaS書き出しのエラーを診断します。
> - [&#x200B; トラブルシューティング シナリオ &#x200B;](troubleshooting/troubleshooting-scenarios.md) – 設定ミスと予期しない同期結果を解決します。
> - [同期の仕組み](sync-overview.md) – 同期モードと再試行動作について説明します。
