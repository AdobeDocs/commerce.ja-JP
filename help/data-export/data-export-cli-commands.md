---
title: SaaS データ書き出しコマンドライン インターフェイス
description: コマンドラインインターフェイスコマンドを使用して、Adobe Commerce向け SaaS サービスのフィードとプロセス  [!DNL data export extension]  管理する方法について説明します。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# SaaS データ書き出しコマンドライン インターフェイス リファレンス

開発者およびシステム管理者は、[Adobe Commerce コマンドラインツール ](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/config-cli) （CLI）を使用して SaaS データエクスポートの同期処理を管理できます。 `saas:resync` コマンドは `magento/saas-export` パッケージに含まれています。

Adobeでは、`saas:resync` コマンドを定期的に使用することはお勧めしません。 コマンドを使用する一般的なシナリオは次のとおりです。

- 初期同期
- [SaaS データ空間 ID](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas) が変更されたため、新しいデータ空間にデータを同期する必要があります。
- トラブルシューティング

## 初期同期

>[!NOTE]
>Live Search または Product Recommendations を使用している場合は、初期同期を実行する必要はありません。 サービスをCommerce インスタンスに接続すると、プロセスが自動的に開始されます。

コマンドラインから `saas:resync` をトリガーする場合、カタログのサイズに応じて、データの更新に数分から数時間かかる場合があります。

初期同期では、Adobeでは次の順序でコマンドを実行することをお勧めします。

```bash
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

## コマンドの例

`saas:resync` のコマンドを使用する前に、[ オプションの説明 ](#command-options) を確認してください。

- エンティティフィードの完全再同期を実行します。

  ```
  bin/magento saas:resync --feed='<FEED_NAME>' 1
  ```

  既に正常に書き出されたフィードは再同期されません。

- 指定したフィードとクリーンアップのデータを完全に再同期する

  ```
  bin/magento saas:resync --feed='FEED_NAME' --cleanup-feed
  ```

  [!DNL Data Space ID Cleanup] 操作を実行した後にのみ使用します。

- すぐにエクスポートフィードを使用するには、フィードテーブルのインデックスデータを切り捨てずに、接続されたCommerce サービスにすべてのデータを再送信します

  ```
   bin/magento saas:resync --feed='FEED_NAME' --no-reindex
  ```

- 使用可能なコマンドおよびオプションと説明を一覧表示します。

  ```
  bin/magento saas:resync --help
  ```

## コマンドオプション

`saas:resync` 操作を管理するには、次のオプションを使用できます。

>[!NOTE]
>
>`saas:resync` コマンドは、バッチサイズを増やし、マルチスレッド処理を追加して、データのエクスポートコマンドを改善する高度なオプションもサポートしています。 [ エクスポート処理のカスタマイズ ](customize-export-processing.md) を参照してください。

### `feed`

この必須オプションは、再同期するフィードエンティティ（`products` など）を指定します。

`feed` のオプション値には、使用可能な任意のエンティティフィードを含めることができます。

- `products`：製品データフィード
- `productAttributes`：製品属性データフィード
- `categories`：カテゴリデータフィード
- `variants`：設定可能な製品バリエーションデータフィード
- `prices`：製品価格データフィード
- `categoryPermissions`：カテゴリ権限データフィード
- `productOverrides`：製品権限データフィード
- `inventoryStockStatus`：在庫状況データフィード
- `scopesWebsite`：ストアおよびストアビューのデータフィードを使用する web サイト
- `scopesCustomerGroup`：顧客グループデータフィード
- `orders`：受注データ・フィード

インストールされている ](../landing/saas.md)0}Commerce サービス } によっては、`saas:resync` コマンドで使用できるフィードのセットが異なる場合があります。[

### `no-reindex`

このオプションは、インデックスを再作成せずに、既存のカタログ データを [!DNL Commerce Services] に再送信します。 このオプションを指定しない場合、コマンドはデータを同期する前に完全な再インデックスを実行します。

このオプションの動作は、フィードが [ レガシーまたは即時エクスポートモード ](data-synchronization.md#synchronization-modes) でエクスポートされるかどうかによって異なります。

- 従来のエクスポートフィードの場合、同期処理では、フィードテーブル内のインデックス付きデータは切り捨てられません。 代わりに、すべてのデータをAdobe Commerce サービスに再送信します。
- 即時エクスポートフィードの場合、このオプションは指定されている場合は無視されます。 これらのフィードの場合、再同期プロセスではインデックスが切り捨てられず、以前に失敗した更新や項目のみが再同期されます。

### `cleanup`

このオプションは、同期前にフィードインデクサーテーブルをクリーンアップします。 指定した場合、SaaS データの書き出しにより、指定したフィードの完全再同期が実行され、フィード テーブル内の既存のデータがすべてクリーンアップされます。

Adobeでは、[!DNL Data Space ID Cleanup] の操作を実行した後にのみ、このコマンドを使用することをお勧めします。

>[!WARNING]
>
>**このオプションを定期的に使用しないでください**。 Adobe Commerce サービスでデータ同期の問題が発生する可能性があります。 例えば、`cleanup` オプションを使用すると、`delete product event` がAdobe Commerce サービスに反映されない可能性があります。

## トラブルシューティング

接続されたCommerce サービスに期待されるデータが表示されない場合は、データの書き出しエラーログを確認し、`saas:resync` コマンドを環境変数と共に使用してペイロードとプロファイラーのデータを確認することで、問題のトラブルシューティングを行います。 [ ログの確認とトラブルシューティング ](troubleshooting-logging.md) を参照してください。
