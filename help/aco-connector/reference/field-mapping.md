---
title: ' [!DNL Adobe Commerce Optimizer Connector]  フィードのフィールドマッピング'
description: すべてのフィードの [!DNL Adobe Commerce]  カタログデータから [!DNL Adobe Commerce Optimizer] 取り込みAPI形式への [!DNL Adobe Commerce Optimizer Connector]  フィールドマッピングについて説明します。
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
autotag-review: '2026-06-09T15:49:03.934Z'
TQID: 'https://experienceleague.adobe.com/SOWOnguudhqzX-r66nGUqc-WKet5qq6GRV11ADx0Me4'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e7dae43f-215c-4cdf-90d3-c5a461a6e669id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: e0eb8757-182f-49f3-94a4-1587d16f5094id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 665
ht-degree: 0%

---


# コネクタフィードのフィールドマッピング

このページでは、[!DNL Adobe Commerce Optimizer Connector]が[!DNL Adobe Commerce] カタログフィールドを[!DNL Commerce Optimizer] [!DNL Catalog Data Ingestion API]で必要な形式に変換する方法について説明します。 サポートされているフィードとそのAPI エンドポイントの一覧については、[ コネクタ リファレンス ](connector-reference.md#supported-feeds)を参照してください。

## 特定可能

`products` フィードは、[製品エンドポイント ](https://developer.adobe.com/commerce/services/reference/rest/#tag/Products){target="_blank"}にデータを送信します。

| [!DNL Adobe Commerce] フィールド | [!DNL Commerce Optimizer] API フィールド | メモ |
| ----------------------------------------------- | -------------- | ------- |
| `sku` | `sku` | |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlKey` | `slug` | |
| `productId` | `externalIds[0].id` | `origin`が`"AdobeCommerce"`に修正されました |
| `status` | `status` | 大文字。割り当てられた子がない複合製品の場合は`DISABLED`に設定されます |
| `description` | `description` | |
| `shortDescription` | `shortDescription` | |
| `visibility` | `visibleIn` | コンマ区切りの値が分割され、マッピングされました：`Catalog`→`CATALOG`、`Search`→`SEARCH`、マッピングされていない値がドロップされました |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeyword` | `metaTags/keywords` | 配列に分割された改行区切り文字列 |
| `inStock`, `lowStock`, `weight`, `weightUnit` | `attributes[].code = "aco_ac_attributes"` | JSON エンコードされたオブジェクト `{inStock, lowStock, weight, weightType}`。常に最初の属性エントリとして存在します |
| `attributes[]` | `attributes[]` | `{code, values[], variantReferenceId}`、`inStock`、`lowStock`、`weight`、`weightType`にマッピングされた各エントリは除外されます（`aco_ac_attributes`に入ります） |
| `images[]` | `images[]` | `url`, `label`；マッピングされた標準ロール：`image`→`BASE`, `small_image`→`SMALL`, `thumbnail`→`THUMBNAIL`, `swatch_image`→`SWATCH`；非標準ロールは`customRoles[]`に移動します |
| `categoryData[].categoryPath` | `routes[].path` | |
| `categoryData[].productPosition` | `routes[].position` | |
| `links[].type` + `links[].sku` | `links[]` | `type`個が大文字です。`sku`を含まないエントリは削除されました |
| `parents[].productType` + `parents[].sku` | `links[]` | マッピングされた型：`configurable`→`VARIANT_OF`、`bundle`/`bundle_fixed`→`IN_BUNDLE` |
| `configurable options` | `configurations[]` | `id`→`attributeCode`, `label`; `swatchType`が設定されている場合はオプションタイプ `SWATCH`、それ以外の場合は`CONFIGURABLE`、デフォルトのバリアントが`isDefault`です。値は`variantReferenceId`, `label`, `colorHex`, `imageUrl`です |
| `bundle options` | `bundles[]` | `label`→`group`; `required`; `renderType` `checkbox`/`multi`→`multiSelect: true`; `isDefault`からの既定のSKU; アイテムには`sku`、`qty`、`userDefinedQty` （`qtyMutability`）が含まれます |

## 製品属性メタデータ

`productAttributes` フィードは、[ メタデータエンドポイント ](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata){target="_blank"}にデータを送信します。


| [!DNL Adobe Commerce] フィールド | [!DNL Commerce Optimizer] API フィールド | メモ |
| --------------- | -------------- | ------- |
| `attributeCode` | `code` | |
| `storeViewCode` | `source/locale` | |
| `label` | `label` | |
| `dataType` + `frontendInput` | `dataType` | 以下の変換表を参照してください |
| `visible` | `visibleIn: "PRODUCT_DETAIL"` | `true`の際に配列に追加されました |
| `visibleInSearch` | `visibleIn: "SEARCH_RESULTS"` | `true`の際に配列に追加されました |
| `visibleInListing` | `visibleIn: "PRODUCT_LISTING"` | `true`の際に配列に追加されました |
| `visibleInCompareList` | `visibleIn: "PRODUCT_COMPARE"` | `true`の際に配列に追加されました |
| `filterable` | `filterable` | |
| `sortable` | `sortable` | |
| `searchable` | `searchable` | |
| `searchWeight` | `searchWeight` | |
| `searchTypes` | `searchTypes` | |

### データタイプ変換

コネクターは、上記のマッピングテーブルのCommerce `dataType`および`frontendInput` フィールドからAPI `dataType`を導き出します。 次の表に、コネクタが適用する変換ルールを示します。

| [!DNL Adobe Commerce] `dataType` | [!DNL Adobe Commerce] `frontendInput` | [!DNL Commerce Optimizer] API `dataType` |
| -------------------- | -------------------------- | ------------------- |
| `int` | `boolean` | `BOOLEAN` |
| `int` | `text`または`select` | `TEXT` |
| `int` | その他 | `INTEGER` |
| `decimal` | - | `DECIMAL` |
| `text`, `varchar`, `static`, `datetime` | - | `TEXT` |
| `OBJECT` | - | `OBJECT` |
| その他 | - | `TEXT` |

>[!NOTE]
>
>属性の`dataType`が`OBJECT`に設定されている場合、[製品API](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"}は、属性値を平文の文字列ではなく構造化オブジェクトとして扱います。 クエリ時に、APIは格納された値をJSONとして解析しようとします。 解析が成功した場合、結果は応答のネストされたオブジェクトとして返されます。 **この動作は、スカラー値として表せない構造化データやマルチフィールドデータを保持するなど、カスタム属性を動的に指定する場合に特に便利です**。 手順については、[製品属性を動的に追加する](../../data-export/add-attribute-dynamically.md)を参照してください。

## プライスブック

`priceBooks` フィードは、[価格表エンドポイント ](https://developer.adobe.com/commerce/services/reference/rest/#tag/Price-Books){target="_blank"}にデータを送信します。

他のコネクタフィードとは異なり、`priceBooks` フィードは[!DNL Adobe Commerce]の[!DNL SaaS Data Export] インデクサーによって収集されません。 コネクターは、管理者のweb サイトと顧客グループ設定からこのフィードを生成します。

Web サイトごとに1つの&#x200B;**基本価格表**&#x200B;が作成され、さらにweb サイトと顧客グループのペアごとに1つの&#x200B;**子価格表**&#x200B;が作成されます。

**価格表ID式：**

- **基本** （通常価格）: `priceBookId = websiteCode`
- **子** （顧客グループまたは共有カタログ）: `priceBookId = websiteCode::sha1(customerGroupId)` （`sha1(customerGroupId)`は顧客グループの整数IDのSHA-1 1 16進ダイジェスト）

価格フィードは、価格入力がどの価格表に属しているかを解決する際に、同じ式を使用します。 ストアフロントが顧客セッションの`priceBookId`を解決する方法については、[ ヘッドレスストアフロント統合](../headless-storefront.md#graphql-commerceoptimizer-query)を参照してください。

| 生成フィールド | [!DNL Commerce Optimizer] API フィールド | メモ |
| ---------------- | -------------- | ------- |
| `websiteCode`, `customerGroupId` | `priceBookId` | |
| web サイト名 | `name` | ベースプライスブック：web サイト名。 子：`"Group Name (Website Name)"` |
| `websiteCode` | `parentId` | 子の価格表にのみ表示されます。基準価格表をポイントします |
| Web サイトのベース通貨 | `currency` | 基本価格台帳にのみ表示されます。子どもから継承されます |

## 価格

`prices` フィードは、[価格エンドポイント ](https://developer.adobe.com/commerce/services/reference/rest/#tag/Prices){target="_blank"}にデータを送信します。

| [!DNL Adobe Commerce] フィールド | [!DNL Commerce Optimizer] API フィールド | メモ |
| --------------- | -------------- | ------------------------------------------------------------------------------- |
| `sku` | `sku` | |
| `websiteCode`, `customerGroupId` | `priceBookId` | |
| `regular` | `regular` | |
| `discounts[]` | `discounts[]` | 割引の例：特別価格、カタログルール価格、共有カタログ価格 |
| `tierPrices[]` | `tierPrices[]` | |

## カテゴリ

`categories` フィードは、[ カテゴリエンドポイント ](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="_blank"}にデータを送信します。

空の`urlPath` （論理ルートカテゴリ）を持つ項目はスキップされ、送信されません。

| [!DNL Adobe Commerce] フィールド | [!DNL Commerce Optimizer] API フィールド | メモ |
| --------------- | -------------- | ------- |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlPath` | `slug` | |
| `description` | `description` | |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeywords` | `metaTags/keywords` | 配列に分割された改行区切り文字列 |
| `image` | `images[].url` | 単一要素の配列；`roles: ["BASE"]` |
| `isActive` + `includeInMenu` | `families` | `true`と`[]`の両方が異なる場合は`["top_menu"]` |

>[!MORELIKETHIS]
>
> - [Data Ingestion API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"}を使用して製品と価格データを取り込む – メタデータ、製品、カテゴリ、価格表、価格のカタログデータモデルを学習します
> - [ カタログデータ取り込みREST API リファレンス ](https://developer.adobe.com/commerce/services/reference/rest/){target="_blank"} – 各フィードエンドポイントのリクエストと応答スキーマを確認します
> - [The [!DNL Commerce Optimizer Connector] と [!DNL Adobe Commerce]](../overview.md#how-the-connector-works-with-adobe-commerce)の連携の仕組み – ストア ビュー、web サイト、顧客グループがカタログ ソースと価格表にどのようにマッピングされるかを説明します
> - [の価格表 [!DNL Commerce Optimizer]](/help/optimizer/setup/pricebooks.md) — コネクタの書き出しによって作成された価格表を管理します
> - [ ヘッドレスストアフロント統合](../headless-storefront.md#graphql-commerceoptimizer-query) – 顧客セッション用に`priceBookId`を解決
