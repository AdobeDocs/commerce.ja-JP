---
title: Commerce CLI を使用したフィードの同期
description: コマンドラインインターフェイスコマンドを使用して、Adobe Commerce向け SaaS サービスのフィードとプロセス  [!DNL data export extension]  管理する方法について説明します。
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
source-git-commit: 086a571b69e8ad76a912c339895409b0037642b9
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---

# Commerce CLI を使用したフィードの同期

`magento/saas-export` パッケージの `saas:resync` コマンドを使用すると、Adobe Commerce SaaS サービスのデータ同期を管理できます。

Adobeでは、`saas:resync` コマンドを定期的に使用することはお勧めしません。 コマンドを使用する一般的なシナリオは次のとおりです。

- 初期同期
- [SaaS データ領域 ID](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas) の変更後、データを新しいデータ領域に同期する
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

特定のエンティティを ID で部分的に再同期します。 `products`、`productAttributes` および `productOverrides` フィードをサポートします。

デフォルトでは、エンティティは製品 SKU で指定されます。 代わりに、`--id-type=ProductID` を使用して製品 ID を使用します。

**例：**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --by-ids='<SKU-1>,<SKU-2>,<SKU-3>'

bin/magento saas:resync --feed='<FEED_NAME>' --by-ids='<ID-1>,<ID-2>,<ID-3>' --id-type='productId'
```

## `--cleanup-feed`

インデックスを再作成して SaaS にデータを送信する前に、フィード インデクサーテーブルをクリーンアップします。 `products`、`productOverrides`、`prices` フィードでのみサポートされます。

>[!IMPORTANT]
>
>環境のクリーンアップ後にのみ使用します。 Commerce サービスでデータ同期の問題が発生する可能性があります。

**例：**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --cleanup-feed
```

## `--continue-resync`

中断された再同期操作を再開します。 `products`、`productAttributes`、`productOverrides` フィードでのみサポートされます。

**例：**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --continue-resync
```

## `--dry-run`

SaaS に送信したり、フィード テーブルに保存したりせずに、フィードの再インデックス プロセスを実行します。 を使用してデータを検証します。

`EXPORTER_EXTENDED_LOG=1` 環境変数を追加して、ペイロードを `var/log/saas-export.log` に保存します。

**例：**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed='<FEED_NAME>' --dry-run
```

## `--feed`

必須。 再同期するフィード エンティティを指定します。

使用可能なフィード：

- `categories`
- `categoryPermissions`
- `inventoryStockStatus`
- `orders`
- `prices`
- `products`
- `productAttributes`
- `productOverrides`
- `scopesWebsite`
- `scopesCustomerGroup`
- `variants`

**例：**

```shell
bin/magento saas:resync --feed='<FEED_NAME>'
```

## `--no-reindex`

インデックスを再作成せずに、既存のカタログ データを [!DNL Commerce Services] に再送信します。 製品関連のフィードではサポートされていません。

動作は [ エクスポートモード ](data-synchronization.md#synchronization-modes) によって異なります。

- レガシーモード：すべてのデータをトランケートせずに再送信します。
- 即時モード：オプションは無視され、更新/エラーのみを同期します。

**例：**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --no-reindex
```

## トラブルシューティング

接続されたCommerce サービスに期待されるデータが表示されない場合は、データの書き出しエラーログを確認し、`saas:resync` コマンドを環境変数と共に使用してペイロードとプロファイラーのデータを確認することで、問題のトラブルシューティングを行います。 [ ログの確認とトラブルシューティング ](troubleshooting-logging.md) を参照してください。
