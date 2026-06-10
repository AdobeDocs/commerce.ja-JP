---
title: '[!DNL Adobe Commerce Optimizer Connector]個のモジュールとフィード エンドポイント'
description: ' [!DNL Adobe Commerce]の [!DNL Adobe Commerce Optimizer Connector]  モジュール、カタログフィード API エンドポイント、バッチ制限、およびcore_config_data設定パスについて説明します。'
feature: Integration, Configuration
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
autotag-review: '2026-06-09T15:48:19.494Z'
TQID: 'https://experienceleague.adobe.com/UM6Y-xoQpUDzWpaMe1GRPp4XoAtHBLBsHw388kumN8g'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 6d4493db5e0714577a8800007cc6d2c552578fa4
workflow-type: tm+mt
source-wordcount: 289
ht-degree: 1%

---

# コネクタモジュールとフィードエンドポイント

このリファレンスには、[!DNL Adobe Commerce Optimizer Connector] モジュールパッケージ、サポートされるフィード API エンドポイント、および`core_config_data`に保存されている設定キーパスが一覧表示されます。 これらのコンポーネントが同期中にどのように連携するかを確認するには、[&#x200B; コネクタ同期パイプライン &#x200B;](../connector-sync-pipeline.md)を参照してください。

## モジュール

コネクターには、カタログデータを収集し、[!DNL Commerce Optimizer] APIでサポートされているフォーマットにフィード データをマッピングし、送信とスコープ管理を管理する複数のMagento モジュールが含まれています。 次の表は、各モジュールとその役割をまとめたものです。

| モジュール | 役割 |
| ------ | ---- |
| `DataExporterAdapter` | [!DNL Adobe Commerce]のフィードを[!DNL Adobe Commerce Optimizer] APIで必要な形式にマッピングします。 フィードプールとスキーマ設定を上書きします。 |
| `SaasExportAdapter` | [!DNL Commerce Optimizer]のフィードを取り込みAPIにルーティングし、サポートされていないフィードを送信からブロックします。 |
| `CommerceAcoExporter` | [!DNL Commerce Optimizer]資格情報を管理し、CLI セットアップ コマンドを提供します |
| `CommerceAdapter` | [!DNL Commerce Optimizer] API互換レイヤー（GraphQL、バンドルアドツーカート、設定UI） |
| `PriceBookDataExporter` | Web サイトと顧客グループでインデックス付けされた価格表フィード |
| `SaasPriceBook` | 価格表提出のためのSaaS インフラ |
| `CommerceOptimizerScopeMapper` | web サイトおよびストアビューごとの同期の有効化 |

## サポートされているフィード

コネクタは、複数のフィード タイプを[!DNL Commerce Optimizer] [!DNL Catalog Data Ingestion API]に送信します。 次の表は、[!DNL Adobe Commerce]のエンドポイント、バッチ制限、インデクサー名、フィード テーブルを含む各フィードの一覧です。

| フィード | [!DNL Commerce Optimizer] API エンドポイント | バッチ制限 | AC インデックス名 | フィードテーブル |
| ---- | ----------------------------------- | ----------- | ------------- | ---------- |
| `products` | `POST /v1/catalog/products` | 100 | `catalog_data_exporter_products` | `cde_products_feed` |
| `categories` | `POST /v1/catalog/categories` | 100 | `catalog_data_exporter_categories` | `cde_categories_feed` |
| `productAttributes` | `POST /v1/catalog/products/metadata` | 100 | `catalog_data_exporter_product_attributes` | `cde_product_attributes_feed` |
| `prices` | `POST /v1/catalog/products/prices` | 500 | `catalog_data_exporter_product_prices` | `cde_product_prices_feed` |
| `priceBooks` | `POST /v1/catalog/price-books` | 500 | `data_exporter_price_books` | `cde_price_books_feed` |

`products`、`productAttributes`、`categories`、`prices`のフィードは、[!DNL SaaS Data Export]個のインデクサーによって収集されたデータを再利用します。 コネクタは、web サイトと顧客グループの設定から`priceBooks` フィードを生成し、[!DNL SaaS Data Export] インデクサーに依存しません。

各フィードのフィールドレベルのマッピングの詳細については、 [!DNL Commerce Optimizer Connector]  フィード [&#128279;](field-mapping.md)の フィールドマッピングを参照してください。

## 設定パス

[!DNL Commerce Optimizer Connector]個の資格情報とサービス URLは、`core_config_data`の`aco_exporter/general/` パス接頭辞に格納されます。 `bin/magento aco:config:show`を実行して現在の値を確認します。 このコマンドは、クライアントの秘密鍵を表示しません。

```text
aco_exporter/general/org_id
aco_exporter/general/tenant_id
aco_exporter/general/client_id
aco_exporter/general/client_secret       (encrypted)
aco_exporter/general/type
aco_exporter/general/ingestion_url
aco_exporter/general/optimizer_studio_url
```
