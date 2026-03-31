---
title: Commerce CLIを使用したフィードの同期
description: コマンドライン インターフェイス コマンドを使用して、Adobe Commerce SaaS サービスの [!DNL data export extension] のフィードとプロセスを管理する方法を説明します。
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
source-git-commit: a05f716200fbf2af74b8488ae66053a56e7037a0
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Commerce CLIを使用したフィードの同期

`saas:resync` パッケージの`magento/saas-export` コマンドを使用すると、Adobe Commerce SaaS サービスのデータ同期を管理できます。

Adobeでは、`saas:resync` コマンドを定期的に使用することはお勧めしません。 コマンドを使用するための一般的なシナリオは次のとおりです。

- 初期同期
- [SaaS データスペース ID](https://experienceleague.adobe.com/ja/docs/commerce-admin/config/services/saas)を変更した後、データを新しいデータスペースに同期する
- トラブルシューティング

`var/log/saas-export.log` ファイルの同期操作を監視します。

## 初期同期

>[!NOTE]
>
>ライブサーチまたは商品レコメンデーションが有効になっている場合、初期同期が自動的に実行されます。 手動コマンドは必要ありません。

コマンドラインから`saas:resync`をトリガーする場合、カタログのサイズに応じて、データを更新するのに数分から数時間かかる場合があります。

初期同期では、Adobeでは、次の順序でコマンドを実行することをお勧めします。

```shell
bin/magento saas:resync --feed productattributes
bin/magento saas:resync --feed products
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed productoverrides
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed categoryPermissions
```

## CLI コマンドを使用した同期

`saas:resync` コマンドは、様々な同期操作をサポートしています。

- SKUによる部分同期
- 中断された同期を再開
- 同期せずにデータを検証

利用可能なすべてのオプションを表示します。

```shell
bin/magento saas:resync --help
```

例を使用したオプションの説明については、次の節を参照してください。


>[!NOTE]
>
>書き出し処理を管理するための詳細なオプションについては、[書き出し処理のカスタマイズ &#x200B;](customize-export-processing.md)を参照してください。

## `--by-ids`

IDによって特定のエンティティの一部を再同期します。 `products`、`productAttributes`、`productOverrides`、`inventoryStockStatus`、`prices`、`variants`および`categoryPermissions` フィードをサポートしています。

デフォルトでは、`--by-ids` オプションを使用する場合、製品SKU値を使用して値を指定します。 代わりに製品IDを使用するには、`--id-type=ProductID` オプションを追加します。

**例：**

```shell
bin/magento saas:resync --feed products --by-ids='ADB102,ADB111,ADB112'

bin/magento saas:resync --feed= products --by-ids='1,2,3' --id-type='productId'
```


## `--cleanup-feed`

SaaSにデータを再入力して送信する前に、フィード インデクサーテーブルをクリーンアップします。 `products`、`productAttributes`、`productOverrides`、`inventoryStockStatus`、`prices`、`variants`および`categoryPermissions`でのみサポートされています。

`--dry-run` オプションと共に使用すると、操作はすべての項目に対してドライ実行再同期操作を実行します。

>[!WARNING]
>
>`cleanup-feed` オプションで再同期コマンドを使用すると、ローカルフィードの書き出し状態がクリアされ、同期が不完全になる可能性があります。 例えば、Adobe Commerceでのエンティティの削除は、接続されたCommerce サービスに反映されない場合や、古いエンティティがAdobe Commerceで削除または更新されたにもかかわらず、リモートのCommerce サービスインデックスに残る場合があります。 このオプションは、SaaS データ領域のクリーンアップ後など、環境の完全な再構築に対してのみ使用します。

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

ペイロードを`EXPORTER_EXTENDED_LOG=1`に保存する`var/log/saas-export.log`環境変数を追加します。

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

**例**

```shell
bin/magento saas:resync --feed products --dry-run --cleanup-feed
```

## `--feed`

必須。 再同期するフィード エンティティを指定します。

利用可能なフィード：

- `categories`
- `categoryPermissions`
- `orders`
- `prices`
- `products`
- `productAttributes`
- `productOverrides`
- `scopesWebsite`
- `scopesCustomerGroup`
- `variants`

>[!NOTE]
>
>Adobe Commerce環境にインストールされているモジュールによって、環境で使用できるフィードが異なる場合があります。

**例：**

```shell
bin/magento saas:resync --feed products
```

## `--no-reindex`

インデックス再作成せずに既存のカタログ データを[!DNL Commerce Services]に再送信します。 製品関連のフィードではサポートされていません。

動作は[書き出しモード &#x200B;](data-synchronization.md#synchronization-modes)によって異なります。

- レガシーモード：すべてのデータを切り捨てずに再送信します。
- 即時モード：オプションは無視され、更新/失敗のみを同期します。

**例：**

```shell
bin/magento saas:resync --feed productAttributes --no-reindex
```

## `--id-type=ProductId`

デフォルトでは、`saas:resync feed` オプションで`--by-ids` コマンドを使用する際に指定されたエンティティは、製品SKUで指定されます。 製品IDでエンティティを指定するには、`--id-type=ProductId` オプションを使用します。

```shell
bin/magento saas:resync --feed products --by-ids='1,2,3' --id-type='productId'
```

**例：**

## トラブルシューティング

接続されたCommerce サービスに期待されるデータが表示されない場合は、データ書き出しエラーログを確認し、環境変数で`saas:resync` コマンドを使用してペイロードとプロファイラーデータを確認して、問題をトラブルシューティングします。 [&#x200B; ログの確認とトラブルシューティング &#x200B;](troubleshooting-logging.md)を参照してください。
