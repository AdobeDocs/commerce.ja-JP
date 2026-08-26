---
source-git-commit: 7d6fa8fa8a93d7d89ca97885f1b9363667a22c7e
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---
# MDEE ログコード リファレンス

ログコード形式：`CDE<group_id>-<log_id>` （例：`CDE01-02`）

ソース：`commerce-data-export`、`commerce-data-export-ee`、`saas-export`

コードは、`error`、`warning`、`critical` レベルのログメッセージにのみ割り当てられます。 `info`、`notice`および`debug` レベルのメッセージは除外されます。

## グループ 01 - データ収集フェーズ

ソースエンティティ（通常はデータプロバイダー）からデータを収集する際に発生するエラーまたは警告に関連するログコード。
- 影響を受けるエンティティは、部分的なデータで処理されるか、エラーが発生した場合は完全にスキップされます。 詳しくは、ログメッセージを参照してください。
- 警告は、サードパーティモジュールによるData Export拡張機能との誤った統合を示す可能性があります。ただし、同期操作は通常は続行されます。

| ログコード | レベル | メッセージ |
|----------|---------|------------------------------------------------------------------------------------------------------------------------------------|
| CDE01-01 | エラー | `CDE01-01 Failed to add stock info to "ac_inventory" attribute for ids "{ids}". Error: {exception_message}` |
| CDE01-02 | 警告 | `CDE01-02 Field "{field}" is missing in row {row_data}` |
| CDE01-03 | 警告 | `CDE01-03 Invalid field "{field}" requested from inventory config {config_data}` |
| CDE01-04 | エラー | `CDE01-04 Was not able to add data to "ac_attribute_set" attribute for ids "{ids}". Error: {exception_message}` |
| CDE01-05 | エラー | `CDE01-05 Unable to sync feed "{feed}" for ids "{ids}". Affected data provider: "{provider}". Error: {exception_message}` |
| CDE01-06 | エラー | `CDE01-06 Unable to sync feed "{feed}" for ids "{ids}". Error: {exception_message}` |
| CDE01-07 | エラー | `CDE01-07 Source entity id is null. Item sync was skip for feed "{feed}". field: "{field}", item: {item}` |
| CDE01-08 | エラー | `CDE01-08 Cannot collect "inStock" for products "{product_ids}": no sales channel data for stores "{store_view_codes}"` |
| CDE01-09 | エラー | `CDE01-09 Cannot get status attribute. Product variants ignore stock status. Error: {exception_message}` |
| CDE01-10 | エラー | `CDE01-10 Unable to retrieve gift card product options for products "{values}". Error: {exception_message}` |
| CDE01-11 | エラー | `CDE01-11 Unable to retrieve gift card shopper input options for products "{values}". Error: {exception_message}` |
| CDE01-12 | 警告 | `CDE01-12 Catalog Permissions: Global Configuration path was not found for path {path}. {config_dump}` |
| CDE01-13 | エラー | `CDE01-13 Catalog Permissions: wrong state in global config. item: {item}, config: {config}` |
| CDE01-14 | エラー | `CDE01-14 Failed to assign UUIDs for type: {type}, ids: {ids}` |
| CDE01-15 | エラー | `CDE01-15 Failed to assign UUIDs for type: {type}, ids: {ids}. duplicates: {duplicates}` |
| CDE01-16 | エラー | `CDE01-16 "{feed_name}" feed sync error: cannot build identifier for "{field}". Item skipped: {item}` |
| CDE01-17 | 警告 | `CDE01-17 Failed to create attribute "{attribute_code}". Will be retried on next sync. Error: {message}` |
| CDE01-18 | 警告 | `CDE01-18 Error on getting datetime for catalog price rule fetch. Using system time. website: "{website_id}", store: "{store_id}"` |
| CDE01-19 | 警告 | `CDE01-19 GiftCard {sku} does not have shopper input options` |
| CDE01-20 | 警告 | `CDE01-20 GiftCard {sku} doesn't have valid options: {options}` |
| CDE01-21 | エラー | `CDE01-21 Unable to resolve url_path for category {id} with path "{path}", url_key "{urk_key}", store "{store}"` |
| CDE01-22 | エラー | `CDE01-22 Unable to resolve url_path for category{id} with path "{path}" for store view "{store}"` |
| CDE01-23 | エラー | `CDE01-23 Unable to assemble "ac_customizable_options" attribute. Error: {exception_message}` |

## グループ 02 - SaaS フェーズへのデータ送信

SaaS エンドポイントにフィードデータを送信する際に発生するエラーまたは警告に関連するログコード。
- 通常、エラーは、HTTP要求、応答処理、データ検証などにおいて、データの受け入れを妨げるエラーを示します。
- 警告は通常、リクエストが自動的に再試行される一時的な条件（レート制限やサーバーエラーなど）を示します。

| ログコード | レベル | メッセージ |
|-----------|---------|---------|
| CDE02-01 | エラー | `CDE02-01 Application error on sending data to SaaS for feed "{feed_name}". Error: {error_message}` |
| CDE02-02 | エラー | `CDE02-02 Unexpected error on sending data to SaaS for feed "{feed_name}". Error: {error_message}` |
| CDE02-03 | 警告 | `CDE02-03 Cannot parse the API response because the request was not successful.` |
| CDE02-04 | エラー | `CDE02-04 Cannot obtain feed metadata for feed name "{feed_name}". Sync terminated. Error: {error_message}` |
| CDE02-05 | エラー | `CDE02-05 Failed to submit feed batch for feed {feed_name}. Error: {error_message}` |
| CDE02-06 | エラー | `CDE02-06 Failed to retry feed items submission for feed {feed_name}. Error: {error_message}` |
| CDE02-07 | 警告 | `CDE02-07 Feed "{feed_name}" sync error: too many requests (HTTP 429). Request will be retried.` |
| CDE02-08 | 警告 | `CDE02-08 Feed "{feed_name}" sync error: Server error (HTTP {http_status_code}). Request will be retried.` |
| CDE02-09 | エラー | `CDE02-09 Feed "{feed_name}" sync error: data validation failed. Check logs. Request will not be retried.` |
| CDE02-10 | 警告 | `CDE02-10 Feed "{feed_name}" sync error: Client error (HTTP {http_status_code}). Request will be retried.` |
| CDE02-11 | 警告 | `CDE02-11 Feed "{feed_name}" sync error: application-level error. Request will be retried.` |
| CDE02-12 | エラー | `CDE02-12 Feed "{feed_name}" sync error API request was not successful (status code: {status_code}).` |
| CDE02-13 | 警告 | `CDE02-13 The zlib-ext is not loaded. Request body can't be compressed and will proceed with regular json` |

## グループ 03 - エンティティ更新時の同期のスケジュール

エンティティの変更に応じて同期をスケジュールまたはトリガーする際に発生するエラーまたは警告に関連するログコード。
- エラーにより、増分同期のスケジュールが妨げられることがあり、多くの場合、リカバリのために完全な再同期または部分的な再同期が必要になります。
- 警告は、サポートされていない入力、識別子の欠落、または設定の問題が原因で、同期操作がスキップまたは延期されたことを示します。

| ログコード | レベル | メッセージ |
|----------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| CDE03-01 | エラー | `CDE03-01 Cannot schedule resync for feeds` |
| CDE03-02 | 警告 | `CDE03-02 Skipping product feed update scheduling. Category path "{category_path}" is wrongly formatted` |
| CDE03-03 | エラー | `CDE03-03 Categories sync error on category "{category_id}" save. Run resync. Error: {error_message}` |
| CDE03-04 | エラー | `CDE03-04 Product sync scheduling error on url key change ({old_url_key} -> {new_url_key}). Run resync. Error: {error_message}` |
| CDE03-05 | エラー | `CDE03-05 Product sync scheduling error on category path change ({old_path} -> {new_path}). Run resync. Error: {error_message}` |
| CDE03-06 | エラー | `CDE03-06 Product sync scheduling error on attribute "{attribute_code}" deletion. Run full resync. Error: {error_message}` |
| CDE03-07 | 警告 | `CDE03-07 Product sync scheduling error on inventory source save for SKUs: {product_skus}. Error: {error_message}` |
| CDE03-08 | エラー | `CDE03-08 Product variants sync scheduling error on product "{sku_or_id}" save. Run resync. Error: {error_message}` |
| CDE03-09 | 警告 | `CDE03-09 The '{feed_name}' feed does not support partial resync by IDs, or an unsupported identifier type was specified.` |
| CDE03-10 | 警告 | `CDE03-10 There are no {id_field}s found to reindex for provided identifiers list: {identifiers}` |
| CDE03-11 | エラー | `CDE03-11 Categories Permissions feed sync scheduling error on category "{category_id_and_name}" delete. Error: {error_message}` |
| CDE03-12 | 警告 | `CDE03-12 Product Overrides sync failed. Marked indexer as invalid. Error: {error_message}` |
| CDE03-13 | エラー | `CDE03-13 Cannot invalidate indexers "{indexer_ids}" for event "{event_name}". Error: {error_message}` |
| CDE03-14 | エラー | `CDE03-14 Failed to read config values. Indexer invalidation skipped. Error: {error_message}` |
| CDE03-15 | エラー | `CDE03-15 Categories Permissions feed sync scheduling error on config save: {error_message}` |
| CDE03-16 | エラー | `CDE03-16 Failed to reindex category permissions global configuration after full reindex: {error_message}` |
| CDE03-17 | 重要な | `CDE03-17 Failed to recreate product override view subscriptions on customer group save: {error_message}` |
| CDE03-18 | 重要な | `CDE03-18 Failed to recreate product override view subscriptions on customer group delete: {error_message}` |
| CDE03-19 | エラー | `CDE03-19 Failed to remove product override view subscriptions during table maintenance: {error_message}` |
| CDE03-20 | エラー | `CDE03-20 Failed to recreate product override view subscriptions after table maintenance: {error_message}` |
| CDE03-21 | エラー | `CDE03-21 Product sync scheduling error on attribute {%s} option change. Run resync. Error: %s` |
| CDE03-22 | 警告 | `CDE03-22 StagedCategoryUrlKeyChangeDetector: no active row at version {version_id} for entity_id(s) [{entity_ids}]; skipping.` |
| CDE03-23 | エラー | `CDE03-23 StagedCategoryUrlKeyChangeDetector: catalog_category url_key attribute not found; failing open.` |
| CDE03-24 | エラー | `CDE03-24 InvalidateProductFeedOnCategoryUrlKeyChange: scheduler failed for path "{path}": {error_message}` |
| CDE03-25 | エラー | `CDE03-25 InvalidateProductFeedOnCategoryUrlKeyChange: gate query failed: {error_message}` |
| CDE03-26 | エラー | `CDE03-26 InvalidateProductFeedOnCategoryUrlKeyChange: unable to expand staged url_key category reindex scope: {error_message}` |
| CDE03-27 | エラー | `CDE03-27 Failed to invalidate indexers after config "{config_section}" change. Error: {error_message}` |
| CDE03-28 | 警告 | `CDE03-28 StagedCategoryUrlKeyChangeDetector: catalog category staging schema is not present; skipping staged url_key change detection.` |

## グループ 04 – 索引付けまたは設定に関連する一般的なエラー

インデックス作成プロセス中または設定ミスによるエラーに関連するログコード。

| ログコード | レベル | メッセージ |
|-----------|---------|---------|
| CDE04-02 | エラー | `CDE04-02 Cannot set indexer to Update On Schedule mode for indexer {indexer_id}. Error: {message}` |
| CDE04-03 | 警告 | `CDE04-03 Partial sync failed for changelog "{changelog_name}". Should be retried. Error: {message}` |
| CDE04-04 | エラー | `CDE04-04 Feed metadata does not contain indexer name. Check di.xml config` |
| CDE04-05 | エラー | `CDE04-05 Cannot load feed indexer for feed` |
| CDE04-06 | エラー | `CDE04-06 Failed to reset MView triggers for "{affected_views}" on index table switch. Run reindex. Error: {message}` |
| CDE04-07 | エラー | `CDE04-07 Error on partial resync for feed "{feed_name}". Error: {message}` |
| CDE04-08 | エラー | `CDE04-08 Error retrying failed items sync for feed "{feed_name}". Error: {message}` |
| CDE04-09 | エラー | `CDE04-09 Error on full resync for feed "{feed_name}". Error: {message}` |
| CDE04-10 | エラー | `CDE04-10 Error during full sync. Message: "{message}". The following IDs were skipped: [{ids}]` |
| CDE04-11 | 警告 | `CDE04-11 Feed "{feed_name}" sync failed. Resync will be run on next cron run. Error: {message}` |
| CDE04-12 | 警告 | `CDE04-12 Partial sync failed for feed "{feed_name}". Retry has been scheduled. Error: {message}` |
| CDE04-13 | エラー | `CDE04-13 Sync completed, but failed to persist status to feed table for "{feed_name}" feed. Error: {message}` |
| CDE04-14 | エラー | `CDE04-14 Cannot delete feed items for feed "{feed_name}" for ids: "{ids}". Error: {message}` |
| CDE04-15 | 警告 | `CDE04-15 Failed to serialize metadata after sync. Error: {message}` |
| CDE04-16 | 警告 | `CDE04-16 Batch table insert query "{query}" returned unexpected result. Expected: {expected_class}, Actual: {actual_type}` |
| CDE04-17 | 警告 | `CDE04-17 Failed to check indexer type when setting schedule mode: {message}` |
| CDE04-18 | 警告 | `CDE04-18 Fixture generator: failed to filter indexer changelog tables from fixture SQL: {message}` |
| CDE04-19 | 警告 | `CDE04-19 The identifier for a feed item is empty. Sync is skipped for the entity.` |
| CDE04-20 | 警告 | `CDE04-20 Unexpected call: feed "{feed_name}" is not locked, trace: {stack_trace}` |
| CDE04-21 | エラー | `CDE04-21 Failed to clean up deleted feed items for feed "{feed_name}". Error: {error_message}` |
