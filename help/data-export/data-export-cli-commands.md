---
title: Commerce CLI を使用したフィードの同期
description: コマンドラインインターフェイスコマンドを使用して、Adobe Commerce向け SaaS サービスのフィードとプロセス  [!DNL data export extension]  管理する方法について説明します。
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# Commerce CLI を使用したフィードの同期

`saas:resync` パッケージの `magento/saas-export` コマンドを使用すると、Adobe Commerce SaaS サービスのデータ同期を管理できます。

Adobeでは、`saas:resync` コマンドを定期的に使用することはお勧めしません。 コマンドを使用する一般的なシナリオは次のとおりです。

- 初期同期
- [SaaS データ空間 ID](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas) を変更した後、データを新しいデータ空間に同期する
- トラブルシューティング

`var/log/saas-export.log` ファイルの同期操作を監視します。

## 初期同期

>[!NOTE]
>
>Live Search または Product Recommendations が有効な場合、初期同期は自動的に実行されます。 手動コマンドは不要です。

コマンドラインから `saas:resync` をトリガーする場合、カタログのサイズに応じて、データの更新に数分から数時間かかる場合があります。

初期同期では、Adobeでは次の順序でコマンドを実行することをお勧めします。

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

- SKU による部分同期
- 中断された同期の再開
- 同期せずにデータを検証

使用可能なすべてのオプションを表示します。

```shell
bin/magento saas:resync --help
```

オプションの説明と例については、次の節を参照してください。


>[!NOTE]
>
>エクスポート処理を管理するための詳細オプションについては、「[ エクスポート処理のカスタマイズ ](customize-export-processing.md)」を参照してください。

## `--by-ids`

特定のエンティティを ID で部分的に再同期します。 `products`、`productAttributes`、`productOverrides`、`inventoryStockStatus`、`prices`、`variants` および `categoryPermissions` フィードをサポートします。

デフォルトでは、「`--by-ids`」オプションを使用する場合、製品 SKU 値を使用して値を指定します。 代わりに製品 ID を使用するには、「`--id-type=ProductID`」オプションを追加します。

**例：**

```shell
bin/magento saas:resync --feed products --by-ids='ADB102,ADB111,ADB112'

bin/magento saas:resync --feed= products --by-ids='1,2,3' --id-type='productId'
```


## `--cleanup-feed`

インデックスを再作成してデータを SaaS に送信する前に、フィードインデクサーテーブルをクリーンアップします。 `products`、`productAttributes`、`productOverrides`、`inventoryStockStatus`、`prices`、`variants` および `categoryPermissions` でのみサポートされます。

`--dry-run` オプションと共に使用すると、操作はすべての項目に対してドライラン再同期操作を実行します。

>[!IMPORTANT]
>
>環境のクリーンアップ後、または `--dry-run` オプションを使用した場合にのみ使用します。 それ以外の場合にクリーンアップ操作を使用すると、データの損失やデータ同期の問題が発生する可能性があります。

**例：**

```shell
bin/magento saas:resync --feed products --cleanup-feed
```

## `--continue-resync`

中断された再同期操作を再開します。 `products`、`productAttributes`、`productOverrides` フィードでのみサポートされます。

**例：**

```shell
bin/magento saas:resync --feed productAttributes --continue-resync
```

## `--dry-run`

フィードを SaaS に送信せずに、またフィード テーブルに保存せずに、フィードの再インデックス プロセスを実行します。 このオプションは、データセットの問題を特定するのに役立ちます。

`EXPORTER_EXTENDED_LOG=1` 環境変数を追加して、ペイロードを `var/log/saas-export.log` に保存します。

**例：**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run
```

### 特定のフィード項目のテスト

`--by-ids` オプションと拡張ログコレクションを追加して特定のフィード項目をテストし、`var/log/saas-export.log` ファイルに生成されたペイロードを確認します。

**例：**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run --by-ids='ADB102,ADB111,ADB112'
```

### すべてのフィード項目のテスト

デフォルトでは、`resync --dry-run` の操作中に送信されるフィードには、新しい項目、または以前に書き出しに失敗した項目のみが含まれます。 処理するフィード内のすべての項目を含めるには、`--cleanup-feed` オプションを使用します。

**例**

```shell
bin/magento saas:resync --feed products --dry-run --cleanup-feed
```

## `--feed`

必須。 再同期するフィード エンティティを指定します。

使用可能なフィード：

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
>お使いの環境で利用できるフィードは、Adobe Commerce環境にインストールされているモジュールによって異なる場合があります。

**例：**

```shell
bin/magento saas:resync --feed products
```

## `--no-reindex`

インデックスを再作成せずに、既存のカタログ データを [!DNL Commerce Services] に再送信します。 製品関連のフィードではサポートされていません。

動作は [ エクスポートモード ](data-synchronization.md#synchronization-modes) によって異なります。

- レガシーモード：すべてのデータをトランケートせずに再送信します。
- 即時モード：オプションは無視され、更新/エラーのみを同期します。

**例：**

```shell
bin/magento saas:resync --feed productAttributes --no-reindex
```

## `--id-type=ProductId`

デフォルトでは、`saas:resync feed` コマンドを `--by-ids` オプションと共に使用した場合に指定されるエンティティは、製品 SKU によって指定されます。 `--id-type=ProductId` オプションを使用して、製品 ID でエンティティを指定します。

```shell
bin/magento saas:resync --feed products --by-ids='1,2,3' --id-type='productId'
```

**例：**

## トラブルシューティング

接続されたCommerce サービスに期待されるデータが表示されない場合は、データの書き出しエラーログを確認し、`saas:resync` コマンドを環境変数と共に使用してペイロードとプロファイラーのデータを確認することで、問題のトラブルシューティングを行います。 [ ログの確認とトラブルシューティング ](troubleshooting-logging.md) を参照してください。
