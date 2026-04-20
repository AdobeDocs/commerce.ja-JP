---
title: ログの確認とトラブルシューティング
description: データ書き出しとsaas書き出しのログを使用して [!DNL data export]  エラーをトラブルシューティングする方法について説明します。
feature: Services
exl-id: d022756f-6e75-4c2a-9601-31958698dc43
source-git-commit: c86e66a675f9a53a6ec7b79540ff85d10186bf3f
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 0%

---

# ログの確認とトラブルシューティング

[!DNL data export]拡張機能には、データ収集と同期プロセスを追跡するためのログが用意されています。

>[!NOTE]
>
>また、管理画面の[&#x200B; データフィード同期ステータスダッシュボード &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)から、製品データとカテゴリーデータのデータエクスポートフィードの正常性とパフォーマンスを追跡することもできます。

## ログ

ログは、Commerce アプリケーションサーバーの`var/log` ディレクトリで利用できます。

| ログ名 | ファイル名 | description |
|-----------------| ----------| -------------|
| SaaS データ書き出しログ | `commerce-data-export.log` | トリガーイベントや完全再同期イベントなどのデータ書き出しアクティビティに関する情報を提供します。  各ログレコードは特定の構造を持ち、フィード、操作、ステータス、経過時間、プロセス ID、発信者に関する情報を提供します。 |
| SaaS データ書き出しエラーログ | `data-export-errors.log` | データ同期プロセス中に発生するエラーのエラーメッセージとスタックトレースを提供します。 |
| SaaS書き出しログ | `saas-export.log` | Commerce SaaS サービスに送信されるデータに関する情報を提供します。 |
| SaaS書き出しエラーログ | `saas-export-errors.log` | Commerce SaaS サービスにデータを送信する際に発生するエラーに関する情報を提供します。 |

Adobe Commerce サービスに期待されるデータが表示されない場合は、データ書き出し拡張機能のエラーログを使用して、問題が発生した場所を確認します。 また、追跡とトラブルシューティングのために追加のデータを使用してログを拡張することもできます。 [拡張ログ &#x200B;](#extended-logging)を参照してください。

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
>JSON ベースの文字列は、読みやすいように美しくなっています。

次の表に、ログに記録できる操作タイプを示します。

| 操作 | 説明 | 呼び出し元の例 |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| 完全同期 | 特定のフィードのために、あらゆるデータを収集してSaaSに送信します。 | `bin/magento saas:resync --feed=products` |
| 部分再インデックス | SaaSにデータを収集して送信し、特定のフィードで更新されたエンティティのみを対象とします。 このログは、更新されたエンティティが存在する場合にのみ存在します。 | `bin/magento cron:run --group=index` |
| 失敗した項目を再試行 | Commerce アプリケーションまたはサーバーエラーが原因で以前の同期処理が失敗した場合、特定のフィードの項目をSaaSに再送信します。 このログは、失敗した項目が存在する場合にのみ表示されます。 | `bin/magento cron:run --group=saas_data_exporter` （任意の「*_data_exporter」 cron グループ） |
| 完全同期（レガシー） | レガシー書き出しモードで、特定のフィードのために、すべてのデータを収集してSaaSに送信します。 | `bin/magento saas:resync --feed=categories` |
| 部分的なインデックス再作成（レガシー） | レガシー書き出しモードで、特定のフィードの更新されたエンティティをSaaSに送信します。 このログは、更新されたエンティティが存在する場合にのみ存在します。 | `bin/magento cron:run --group=index` |
| 部分同期（レガシー） | レガシー書き出しモードで、特定のフィードの更新されたエンティティをSaaSに送信します。 このログは、更新されたエンティティが存在する場合にのみ存在します。 | `bin/magento cron:run --group=saas_data_exporter` （任意の「*_data_exporter」 cron グループ） |


### ログの例

完全再同期では、デフォルトで進行状況が追跡され、30秒ごとに記録されます。 次に、ログエントリの例を示します。

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

この例では、`status`値は同期操作に関する情報を提供します。

- **`"Progress 2/5"`**&#x200B;は、5回のイテレーションのうち2回が完了したことを示します。 反復の数は、書き出されたエンティティの数によって異なります。
- **`"processed: 200"`**&#x200B;は、200件の項目が処理されたことを示します。
- **`"synced: 100"`**&#x200B;は、100件の項目がSaaSに送信されたことを示します。 `"synced"`が`"processed"`と等しくないことが予想されます。 例を次に示します。
   - **`"synced" < "processed"`**&#x200B;は、以前に同期されたバージョンと比較して、フィード テーブルがアイテムの変更を検出しなかったことを意味します。 このような項目は、同期操作中は無視されます。
   - **`"synced" > "processed"`**&#x200B;同じエンティティ id （例：`Product ID`）で、異なるスコープに複数の値を持つことができます。 例えば、ひとつの商品を5つのweb サイトに割り当てることができます。 この場合、「1個の処理済み」項目と「5個の同期済み」項目がある可能性があります。

+++ **例：価格フィードの完全な再同期ログ**

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

New RelicにAdobe Commerce ログを保存する場合は、解析ルールを追加して、読みやすさとクエリエクスペリエンスを向上させることができます。

1. New Relicにログインします。

1. `Logs => Parsing`に移動します。

1. `Create parsing rule`をクリックします。

1. 次の値を追加して、解析ルールを設定します。

   - **NRQL**&#x200B;に基づいてログをフィルタリング

     `filePath LIKE '%commerce-data-export%.log'`

   - **ルールを解析**

     `\[%{DATA:timestamp}\] report.%{DATA:logLevel}: %{GREEDYDATA:feed:json}`

次の例では、特定のフィードの種類や操作などによってNew Relic ログをクエリできるルールを追加します。

**クエリ文字列の例**—`feed.feed:"products" and feed.status:"Complete"`

## トラブルシューティング

Commerce サービスでデータが欠落または正しくない場合は、Adobe CommerceからCommerce Services プラットフォームへの同期中に発生したエラーに関するメッセージをログで確認します。 必要に応じて、拡張ログを使用してログに追加情報を追加し、トラブルシューティングを行います。

- データ書き出しエラーログ （`commerce-data-export-errors.log`）は、収集フェーズで発生したエラーをキャプチャします。
- SaaS書き出しエラーログ （`saas-export-errors.log`）は、送信段階で発生したエラーをキャプチャします。

設定またはサードパーティの拡張機能に関連しないエラーが表示された場合は、できるだけ多くの情報を含む[&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)を送信してください。

### カタログ同期の問題を解決する {#resolvesync}

データ再同期をトリガーすると、データが更新され、ライブサーチやレコメンデーションユニットなどのUI コンポーネントに反映されるまでに、最大1時間かかる場合があります。 Commerce ストアフロントで引き続きカタログとデータの間に不一致が表示される場合、またはカタログの同期に失敗した場合は、次を参照してください。

#### データの不一致

1. 検索結果に該当する製品の詳細ビューを表示します。
1. JSON出力をコピーし、コンテンツが[!DNL Commerce] カタログ内のコンテンツと一致することを確認します。
1. コンテンツが一致しない場合は、スペースやピリオドの追加など、カタログ内の商品に軽微な変更を加えます。
1. 再同期を待つか、CLIまたは管理者ダッシュボードから手動再同期をトリガーします。

#### Syncが実行されていません

同期がスケジュールで実行されていないか、何も同期されていない場合は、この[KnowledgeBase](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce)記事を参照してください。

#### 同期できませんでした

カタログ同期のステータスが&#x200B;**失敗**&#x200B;の場合は、[&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket)を送信します。

## 拡張ログ

環境変数を使用して、追跡とトラブルシューティング用の追加データを含むログを拡張します。 次の例に示すように、data export CLI コマンドを実行する際に、環境変数をコマンドラインに追加します。

### フィードペイロードの確認

フィードの再同期時に`EXPORTER_EXTENDED_LOG=1`環境変数を追加して、SaaS エクスポートログにフィードペイロードを含めます。

```shell script
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed=products
```

操作が完了すると、フィード ペイロードはSaaS エクスポート ログ （`var/.log/saas-export.log`）でレビューできます。

### フィード インデックス テーブルのペイロードを保持

Commerce SaaS Data Export Extension （`magento/module-data-exporter`） 103.3.0以降では、即時の書き出しフィードは、インデックステーブルに必要な最小限のデータのみを保持します。 フィードには、すべてのカタログおよび在庫の在庫ステータスフィードが含まれます。

インデックステーブルにペイロードデータを保持することは、実稼動環境では推奨されませんが、開発者環境では便利です。 フィードの再同期時に`PERSIST_EXPORTED_FEED=1`環境変数を追加して、フィード ペイロードをインデックスに含めます。

```shell script
PERSIST_EXPORTED_FEED=1 bin/magento saas:resync --feed=products
```

### プロファイラーを実行してパフォーマンスの低下をトラブルシューティング

特定のフィードのインデックス再作成プロセスに不合理な時間が要する場合は、プロファイラーを実行して、サポートチームに役立つ追加データを収集します。

reindex コマンドの実行時に`EXPORTER_PROFILER=1`環境変数を追加して、プロファイラーを実行します。

```
EXPORTER_PROFILER=1 bin/magento indexer:reindex catalog_data_exporter_products
```

プロファイラーデータは、データ書き出しログ （`var/log/commerce-data-export.log`）に次の形式で保存されます。

```
<Provider class name>, <# of processed entities>, <execution time im ms>, <memory consumption in Mb>
```
