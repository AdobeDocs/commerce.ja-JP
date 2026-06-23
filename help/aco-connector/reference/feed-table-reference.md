---
title: フィード テーブル スキーマ リファレンス
description: フィード項目の状態、書き出しステータス、エラーの詳細を追跡するために [!DNL Adobe Commerce Optimizer Connector] が使用するフィード テーブル スキーマについて説明します。
autotag-review: '2026-06-23T00:00:00.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 19de20caafd45e3a00896d0d4b29b7e96dfe94e1
workflow-type: tm+mt
source-wordcount: 324
ht-degree: 0%

---


# フィードテーブルスキーマ参照

すべてのフィードには、[!DNL Adobe Commerce] データベースに専用のMySQL テーブルがあります。 すべてのフィード テーブルは、同じ列構造を共有します。

## サポートされているフィード

API エンドポイント、バッチ制限、インデクサー名、フィード テーブル名でサポートされているフィードの完全なリストについては、[&#x200B; コネクタ モジュールとフィード エンドポイント &#x200B;](connector-reference.md#supported-feeds)を参照してください。

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
| `status` | INT | 前回の書き出し試行からの送信ステータスコード。 [&#x200B; フィード送信とエラー処理](../connector-sync-pipeline.md#feed-submission-and-error-handling)を参照してください。 |
| `errors` | テキスト | この項目の[!DNL Commerce Optimizer] APIによって返されたJSON エンコード済みエラーの詳細 |
| `metadata` | JSON | 書き出しフレームワークで使用される内部同期フラグとロック メタデータ情報 |

## 一般的な診断クエリ

次のSQL クエリを使用して、フィード テーブルの状態を直接検査します。 `feed_data`列には、[!DNL Adobe Commerce Optimizer] API形式でデータが格納されます。 `<SKU>`、`<ATTRIBUTE_CODE>`、`<SLUG>`、`<PRICE_BOOK_ID>`などのプレースホルダー値を、お使いの環境の実際の値に置き換えます。

**製品フィード - SKU:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_products_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**製品属性フィード – 属性コード：**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.code') AS 'code',
       JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_attributes_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.code') IN ('<ATTRIBUTE CODE>');
```

**カテゴリーフィード - URL パス別：**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.slug') AS 'slug',
    JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
    f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_categories_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.slug') IN ('<SLUG>');
```

**価格フィード - SKU:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.priceBookId') AS 'price book ID',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_prices_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**価格台帳フィード – 価格台帳ID:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.priceBookId') AS 'price book ID',
    JSON_EXTRACT(f.feed_data, '$.name') AS 'name',
    JSON_EXTRACT(f.feed_data, '$.parentId') AS 'parent price book ID',
    JSON_EXTRACT(f.feed_data, '$.currency') AS 'currency',
    f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_price_books_feed f
WHERE JSON_UNQUOTE(JSON_EXTRACT(f.feed_data, '$.priceBookId'))  IN ('<PRICE_BOOK_ID>');
```

>[!MORELIKETHIS]
>
>- [&#x200B; コネクタ モジュールとフィード エンドポイント &#x200B;](connector-reference.md)
>- [&#x200B; コネクタ同期パイプライン &#x200B;](../connector-sync-pipeline.md)
>- [同期の管理](../data-sync-manage.md)
>- コネクタフィードの[&#x200B; フィールドマッピング &#x200B;](field-mapping.md)
