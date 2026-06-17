---
title: フィード テーブル スキーマ リファレンス
description: フィード項目の状態、書き出しステータス、エラーの詳細を追跡するために [!DNL SaaS Data Export] が使用するフィード テーブル スキーマについて説明します。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Services
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
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 416
ht-degree: 0%

---


# フィードテーブルスキーマ参照

すべてのフィードには、[!DNL Adobe Commerce] データベースに専用のMySQL テーブルがあります。 すべてのフィード テーブルは、同じ列構造を共有します。 以下の表は、各フィードのCLI フィード名、インデクサーID、フィードのテーブル名を示しています。

## サポートされているフィード

フィードの実際のリストは、インストールされている[!DNL SaaS Data Export] パッケージによって異なります。


| フィード （`--feed`） | 目的 | インデクサーID | フィードテーブル | 書き出しモード |
| --- | ------------------------------------------------------------------- | --- | --- | --- |
| `products` | 製品カタログ（属性、カテゴリー、画像など） | `catalog_data_exporter_products` | `cde_products_feed` | 即時 |
| `productAttributes` | 属性の定義とメタデータ： 検索スキーマの定義に使用します。 | `catalog_data_exporter_product_attributes` | `cde_product_attributes_feed` | 即時 |
| `categories` | カテゴリデータ | `catalog_data_exporter_categories` | `cde_categories_feed` | 即時 |
| `prices` | 製品価格と、顧客グループの価格と階層の価格 | `catalog_data_exporter_product_prices` | `cde_product_prices_feed` | 即時 |
| `variants` | 設定可能な製品バリエーション | `catalog_data_exporter_product_variants` | `cde_product_variants_feed` | 即時 |
| `scopesWebsite` | ストアビューコード付きのweb サイト | `scopes_website_data_exporter` | `scopes_website_data_exporter` | レガシー |
| `scopesCustomerGroup` | 顧客グループの定義 | `scopes_customergroup_data_exporter` | `scopes_customergroup_data_exporter` | レガシー |
| `productOverrides` | 計算された製品権限 | `catalog_data_exporter_product_overrides` | `cde_product_overrides_feed` | 即時 |
| `categoryPermissions` *（EE）* | 生のカテゴリ権限データ | `catalog_data_exporter_category_permissions` | `cde_category_permissions_feed` | 即時 |
| `orders` | 販売注文のステータス | `sales_order_data_exporter_v2` | `sales_data_exporter_orders_v2` | レガシー |

**書き出しモード**&#x200B;列は、各フィードがデータを収集および送信する方法を示します。

- **即時モードフィード** — データを収集し、コンテンツハッシュ（ハッシュ重複排除）を使用して変更されていない項目をスキップし、同じインデクサー実行で更新を送信します。
- **レガシーモードフィード** （`scopesWebsite`、`scopesCustomerGroup`、`orders`） – 最初にフィード テーブルにアセンブリされたデータを保存し、別のcron ジョブを介して送信します。

[同期モード &#x200B;](../sync-overview.md#synchronization-modes)を参照してください。

## スキーマ

| 列 | タイプ | 説明 |
| --- | --- | ---------------- |
| `id` | INT （PK） | 自動インクリメントのプライマリキー |
| `source_entity_id` | INT | Commerceのソーステーブルのエンティティ ID （例：`catalog_product_entity.entity_id`） |
| `feed_id` | VARCHAR | フィード項目の一意のID。 自動インクリメント値ではなく、項目のID フィールド （例：`sku + storeViewCode`）のハッシュとして計算されます。 |
| `feed_data` | JSON | この項目のフィードペイロード。 エンティティ IDとスコープとしての最小限の情報のみが入力されます。 `PERSIST_EXPORTED_FEED=1`が設定されると、完全なペイロードが保存されます。 |
| `feed_hash` | VARCHAR | 変更検出に使用されるコンテンツハッシュ。 タイムスタンプ （`modifiedAt`、`updatedAt`）を除いて、ペイロードから計算されます。 ハッシュが以前の書き出しと一致する場合、アイテムは再送信されません。 |
| `is_deleted` | TINYINT | ソフト削除マーカー。 Commerceでエンティティが削除された場合は、`1`に設定します。 |
| `modified_at` | TIMESTAMP | このフィード項目が最後に変更された日時 |
| `status` | INT | 前回の書き出し試行からの送信ステータスコード。 [&#x200B; フィード送信とHTTP エラー処理](../sync-overview.md#feed-submission-and-http-error-handling)を参照してください。 |
| `errors` | テキスト | この項目のSaaS サービスから返されるJSON エンコードされたエラーの詳細 |
| `metadata` | JSON | 書き出しフレームワークで使用される内部同期フラグとロック メタデータ情報 |

## 一般的な診断クエリ

次のSQL クエリを使用して、フィード テーブルの状態を直接検査します。 `cde_products_feed`を調査中のフィードのテーブルに置き換えます。 テーブル名の完全なリストについては、[&#x200B; サポートされているフィード &#x200B;](#supported-feeds)を参照してください。

**正常にエクスポートされなかった項目をすべて検索：**

```sql
SELECT source_entity_id, status, errors, modified_at
FROM cde_products_feed
WHERE status != 200
ORDER BY modified_at DESC
LIMIT 50;
```

**すべてのスコープで特定のSKUの書き出しステータスを確認する：**

```sql
SELECT p.sku, f.status, f.modified_at, f.is_deleted, f.feed_data, f.errors
FROM catalog_product_entity p
LEFT JOIN cde_products_feed f ON f.source_entity_id = p.entity_id
WHERE p.sku = 'ADB295';
```


>[!MORELIKETHIS]
>
>- [SaaS データ書き出しとデータの同期](../sync-overview.md)
>- [同期の表示と管理](../data-sync-manage.md)
>- [Commerce CLIを使用してフィードを同期](../data-export-cli-commands.md)
