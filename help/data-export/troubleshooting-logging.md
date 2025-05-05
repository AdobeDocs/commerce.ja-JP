---
title: ログの確認とトラブルシューティング
description: データの書き出しログと saas [!DNL data export]  書き出しログを使用してエラーのトラブルシューティングを行う方法を説明します。
feature: Services
exl-id: d022756f-6e75-4c2a-9601-31958698dc43
source-git-commit: 22c74c12ddfccdb4e6c4e02c3a15557e1020d5ef
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 0%

---

# ログの確認とトラブルシューティング

[!DNL data export] 拡張機能は、データ収集および同期プロセスを追跡するログを提供します。

## ログ

ログは、Commerce Application Server の `var/log` ディレクトリで利用できます。

| ログ名 | ファイル名 | 説明 |
|-----------------| ----------| -------------|
| SaaS データ エクスポート ログ | `commerce-data-export.log` | エンティティトリガーや完全な再同期イベントなど、データのエクスポート アクティビティに関する情報を提供します。  各ログレコードは特定の構造を持ち、フィード、操作、ステータス、経過時間、プロセス ID、呼び出し元に関する情報を提供します。 |
| SaaS データ エクスポート エラーログ | `data-export-errors.log` | データ同期処理中に発生したエラーのエラーメッセージとスタックトレースを提供します。 |
| SaaS エクスポート ログ | `saas-export.log` | Commerce SaaS サービスに送信されるデータに関する情報を提供します。 |
| SaaS エクスポート エラーログ | `saas-export-errors.log` | Commerce SaaS サービスにデータを送信する際に発生するエラーについて説明します。 |

Adobe Commerce サービスで予期されたデータが表示されない場合は、データエクスポート拡張機能のエラーログを使用して問題の発生場所を特定してください。 また、トラッキングやトラブルシューティングのために、追加データを使用してログを拡張することもできます。 [ 拡張ログ ](#extended-logging) を参照してください。

### ログ形式

各ログレコードの構造は次のとおりです。

```
[<log record datetime>] report.<log level>:
{
   "feed": "<feed name>",
   "operation": "<executed operation>",
   "status": "<status of operation>",
   "elapsed": "<time elapsed from script run>",
   "pid": "<process id that executed `operation`>",
   "caller": "<who called this `operation`>"
} [] []
```

>[!NOTE]
>
>JSON ベースの文字列は、読みやすいように美化されています。

次の表に、ログに記録できる操作タイプを示します。

| 操作 | 説明 | 呼び出し元の例 |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| 完全同期 | 特定のフィードのすべてのデータを収集し、SaaS に送信します。 | `bin/magento saas:resync --feed=products` |
| 部分再インデックス | 特定のフィードで更新されたエンティティのみのデータを収集し、SaaS に送信します。 このログは、更新されたエンティティが存在する場合にのみ表示されます。 | `bin/magento cron:run --group=index` |
| 失敗した項目を再試行 | Commerce アプリケーションまたはサーバーエラーが原因で前回の同期処理に失敗した場合は、特定のフィードの項目を SaaS に再送信します。 このログは、失敗した項目が存在する場合にのみ存在します。 | `bin/magento cron:run --group=saas_data_exporter` （「*_data_exporter」 cron グループのいずれか） |
| 完全同期（レガシー） | レガシ エクスポート モードの特定のフィードに対して、すべてのデータを収集し、SaaS に送信します。 | `bin/magento saas:resync --feed=categories` |
| 部分再インデックス（レガシー） | レガシー書き出しモードの特定のフィードに対して、更新されたエンティティを SaaS に送信します。 このログは、更新されたエンティティが存在する場合にのみ表示されます。 | `bin/magento cron:run --group=index` |
| 部分同期（レガシー） | レガシー書き出しモードの特定のフィードに対して、更新されたエンティティを SaaS に送信します。 このログは、更新されたエンティティが存在する場合にのみ表示されます。 | `bin/magento cron:run --group=saas_data_exporter` （「*_data_exporter」 cron グループのいずれか） |


### ログの例

完全な再同期では、進行状況はデフォルトで 30 秒ごとに追跡され、記録されます。 ログエントリの例を次に示します。

```json
{
   "feed": "prices",
   "operation": "full sync",
   "status": "Progress: 2/5, processed: 200, synced: 100",
   "elapsed": "00:00:00 190 ms",
   "pid": "12824",
   "caller": "bin/magento saas:resync --feed=products"
}
```

この例では、`status` の値が同期操作に関する情報を提供します。

- **`"Progress 2/5"`** は、5 回のイテレーションのうち 2 回が完了したことを示しています。 イテレーションの数は、エクスポートされたエンティティの数によって異なります。
- **`"processed: 200"`** は、200 個の項目が処理されたことを示しています。
- **`"synced: 100"`** は、100 項目が SaaS に送信されたことを示します。 `"synced"` が `"processed"` に等しくないと予想される。 次に例を示します。
   - **`"synced" < "processed"`** れは、以前に同期されたバージョンと比較して、フィードテーブルで項目の変更が検出されなかったことを意味します。 このような項目は、同期操作中は無視されます。
   - 同じエンティティ id （`Product ID` など）に **`"synced" > "processed"`**、異なるスコープに複数の値を含めることができます。 例えば、1 つの製品を 5 つの web サイトに割り当てることができます。 この場合、「1 件の処理済み」項目と「5 件の同期済み」項目が存在する可能性があります。

+++ **例：価格フィードの完全再同期ログ**

```
Price feed full resync:

[2024-03-05T21:00:51.754687+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Initialize","elapsed":"383 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.803178+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Creating batch table `catalog_data_exporter_product_prices_index_batches`. Start position: 30515","elapsed":"434 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.851878+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Batch table `catalog_data_exporter_product_prices_index_batches` created. Total Items: 500, batches: ~1","elapsed":"482 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.852548+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"start processing `500` items in `1` threads with `500` batch size","elapsed":"483 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:52.288369+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Progress 1\/1, processed 500, synced 0","elapsed":"919 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:53.994249+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Progress 1\/1, processed 500, synced 100","elapsed":"00:00:02 625 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:53.995168+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Complete","elapsed":"00:00:02 626 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
```

+++

## New Relicでのログの表示とトラブルシューティング

Adobe Commerce ログをNew Relicに保存する場合は、解析ルールを追加して、読みやすさとクエリエクスペリエンスを向上させることができます。

1. New Relicにログインします。

1. `Logs => Parsing` に移動します。

1. 「`Create parsing rule`」をクリックします。

1. 次の値を追加して、解析ルールを設定します。

   - **NRQL に基づいたログのフィルタリング**

     `filePath LIKE '%commerce-data-export%.log'`

   - **解析ルール**

     `\[%{DATA:timestamp}\] report.%{DATA:logLevel} %{GREEDYDATA:feed:json}`

この例では、特定のフィードのタイプや処理などでNew Relic ログをクエリできるルールを追加します。

**クエリ文字列の例**—`feed.feed:"products" and feed.status:"Complete"`

## トラブルシューティング

Commerce Services のデータが見つからない場合や誤っている場合は、ログを調べて、CommerceからAdobe Commerce Services Platform への同期中に発生したエラーに関するメッセージを確認します。 必要に応じて、拡張ログを使用して、トラブルシューティング用の情報をログに追加します。

- データ書き出しエラーログ（`commerce-data-export-errors.log`）には、収集段階で発生したエラーが記録されます。
- SaaS 書き出しエラーログ（`saas-export-errors.log`）は、送信段階で発生したエラーをキャプチャします。

設定やサードパーティの拡張機能に関連しないエラーが表示された場合は、できるだけ多くの情報を記載した [ サポートチケット ](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) を送信します。

### カタログ同期の問題を解決 {#resolvesync}

データの再同期をトリガーする場合、データが更新され、ライブ検索やレコメンデーションユニットなどの UI コンポーネントに反映されるまで、最大 1 時間かかる場合があります。 カタログとCommerce ストアフロントのデータの間にまだ不一致が発生する場合、またはカタログの同期に失敗した場合は、次を参照してください。

#### データの不一致

1. 検索結果に、該当する製品の詳細ビューを表示します。
1. JSON 出力をコピーし、コンテンツが [!DNL Commerce] カタログの内容と一致することを確認します。
1. コンテンツが一致しない場合は、スペースやピリオドの追加など、カタログの製品に小さな変更を加えます。
1. 再同期を待つか、[ 手動の再同期をトリガーしてください ](#resync)。

#### 同期が実行されていません

同期がスケジュールに従って実行されていない場合や、何も同期されていない場合は、この [KnowledgeBase](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce) の記事を参照してください。

#### 同期できませんでした

カタログ同期のステータスが **失敗** の場合は、[ サポートチケット ](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) を送信します。

## 拡張ログ

環境変数を使用して、トラッキングやトラブルシューティング用の追加データでログを拡張します。 次の例に示すように、data export CLI コマンドを実行する際に、環境変数をコマンドラインに追加します。

### フィードペイロードを確認

フィードを再同期する際に `EXPORTER_EXTENDED_LOG=1` 環境変数を追加して、フィード ペイロードを SaaS 書き出しログに含めます。

```shell script
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed=products
```

操作が完了すると、フィードペイロードを SaaS 書き出しログで確認できるようになります（`var/.log/saas-export.log`）。

### フィードインデックステーブルにペイロードを保持

Commerce SaaS Data Export Extension （`magento/module-data-exporter`） 103.3.0 以降では、即時エクスポートフィードは、インデックステーブルに必要な最小限のデータのみを保持します。 フィードには、すべてのカタログと在庫のステータスフィードが含まれます。

実稼動環境ではペイロードデータをインデックステーブルに保持することは推奨されませんが、開発者環境では便利です。 フィードを再同期する際に `PERSIST_EXPORTED_FEED=1` 環境変数を追加して、フィードペイロードをインデックスに含めます。

```shell script
PERSIST_EXPORTED_FEED=1 bin/magento saas:resync --feed=products
```

### プロファイラーを実行してパフォーマンスが低下する場合のトラブルシューティング

特定のフィードの再インデックスプロセスに不相応な時間がかかる場合は、プロファイラーを実行して、サポートチームに役立つ追加データを収集します。

reindex コマンドを実行する場合は、環境変数 `EXPORTER_PROFILER=1` を追加してプロファイラーを実行します。

```
EXPORTER_PROFILER=1 bin/magento indexer:reindex catalog_data_exporter_products
```

プロファイラーデータは、次の形式でデータ書き出しログ（`var/log/commerce-data-export.log`）に保存されます。

```
<Provider class name>, <# of processed entities>, <execution time im ms>, <memory consumption in Mb>
```
