---
title: '[!DNL Adobe Commerce Optimizer Connector] フィードのフィールドマッピング'
description: すべてのフィードの[!DNL Adobe Commerce] カタログデータから[!DNL Adobe Commerce Optimizer]取り込みAPI形式への[!DNL Adobe Commerce Optimizer Connector] フィールドマッピングについて説明します。
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
autotag-review: '2026-06-09T15:49:03.934Z'
TQID: 'https://experienceleague.adobe.com/SOWOnguudhqzX-r66nGUqc-WKet5qq6GRV11ADx0Me4'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
    internal-label: Data modeling
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 2%
---

# コネクタフィードのフィールドマッピング

このページでは、[!DNL Adobe Commerce Optimizer Connector]が[!DNL Adobe Commerce] カタログフィールドを[!DNL Commerce Optimizer] [!DNL Catalog Data Ingestion API]で必要な形式に変換する方法について説明します。 サポートされているフィードとそのAPI エンドポイントの一覧については、[&#x200B; コネクタ リファレンス &#x200B;](connector-reference.md#supported-feeds)を参照してください。

## 特定可能

`products` フィードは、[製品エンドポイント &#x200B;](https://developer.adobe.com/commerce/services/reference/rest/#tag/Products){target="_blank"}にデータを送信します。

| [!DNL Adobe Commerce] フィールド | [!DNL Commerce Optimizer] API フィールド | マッピングの詳細 |
| ----------------------------------------------- | -------------- | ------- |
| `sku` | `sku` | |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlKey` | `slug` | |
| `productId` | `externalIds[0].id` | `origin`を`"AdobeCommerce"`に設定 |
| `status` | `status` | ステータスを大文字に変換します。 ステータスが欠落している場合、または設定可能またはバンドル製品にオプション値がない場合は、`DISABLED`を使用します。 |
| `description` | `description` | 説明が見つからない場合は、空の文字列を使用します。 |
| `shortDescription` | `shortDescription` | 短い説明がない場合は、空の文字列を使用します。 |
| `visibility` | `visibleIn` | コンマ区切りの値を分割し、`Catalog`を`CATALOG`に、`Search`を`SEARCH`にマッピングします。 他の値をドロップします。 |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeyword` | `metaTags/keywords` | 改行で区切られたキーワードを配列に分割し、空白をトリミングします。 |
| `inStock`, `lowStock`, `weight`, `weightUnit` | `attributes[].code = "aco_ac_attributes"` | 常に`aco_ac_attributes` エントリを最初の属性として追加します。 そのJSON値には、`inStock`と`lowStock`が文字列として含まれます。 これらの値が使用可能な場合は、`weight`と`weightType`が含まれます。 |
| `attributes[]` | `attributes[]` | 使用可能な場合、各エントリを属性コード、文字列値、一致するバリアント参照IDにマッピングします。 `inStock`、`lowStock`、`categories`、`weight`、`weightType`をスキップします。 在庫関連の値は`aco_ac_attributes`に含まれています。 カテゴリはルートとしてエクスポートされます。 |
| `images[]` | `images[]` | URLのない画像をスキップします。<br>`url`、`label` （欠落している場合は空）、`sortOrder` （整数、デフォルトは`0`）を書き出します。<br>画像を`sortOrder`順に昇順で並べ替えます。<br>標準の役割：`image` ～ `BASE`、`small_image` ～ `SMALL`、`thumbnail` ～ `THUMBNAIL`、および`swatch_image` ～ `SWATCH`をマッピングします。 他の役割を`customRoles[]`として書き出します。 |
| `categoryData[].categoryPath` | `routes[].path` | 空のカテゴリパスを持つエントリをスキップします。 |
| `categoryData[].productPosition` | `routes[].position` | 製品位置が見つからない場合は、`0`を使用します。 |
| `links[].type` + `links[].sku` | `links[]` | `type`個が大文字です。`sku`を含まないエントリは削除されました |
| `parents[].productType` + `parents[].sku` | `links[]` | `configurable`を`VARIANT_OF`に、`bundle`または`bundle_fixed`を`IN_BUNDLE`にマップします。 他の製品タイプを大文字に変換します。 SKUなしで親をスキップします。 |
| `configurable options` | `configurations[]` | IDと1つ以上の値を持つオプションを書き出します。<br>`id`を`attributeCode`にマップします。 `swatchType`が存在する場合は`type`を`SWATCH`に、それ以外の場合は`CONFIGURABLE`に設定します。<br> デフォルト値のIDを`defaultVariantReferenceId`として使用します。<br>各値を`variantReferenceId`、`label`、`colorHex`、および`imageUrl`にマッピングします。 |
| `bundle options` | `bundles[]` | 1つ以上の項目を含むオプションを書き出します。<br> オプションラベルを`group`として使用します。ラベルが空の場合は`Bundle group`として使用します。 `required`を出力にコピーします。<br> レンダータイプ `checkbox`と`multi`に対して`multiSelect`を`true`に設定します。<br> デフォルトのSKUを`defaultItemSkus`に一覧表示します。 各項目には、`sku`、`qty` （デフォルトは`0`）および`userDefinedQty` （`qtyMutability`からデフォルトは`false`）が含まれます。 |

## 製品属性メタデータ

`productAttributes` フィードは、[&#x200B; メタデータエンドポイント &#x200B;](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata){target="_blank"}にデータを送信します。

| [!DNL Adobe Commerce] フィールド | [!DNL Commerce Optimizer] API フィールド | マッピングの詳細 |
| --------------- | -------------- | ------- |
| `attributeCode` | `code` | |
| `storeViewCode` | `source/locale` | |
| `label` | `label` | |
| `dataType` + `frontendInput` | `dataType` | 以下の変換表を参照してください |
| `dataType`と`frontendInput` | `dataType` | 以下の変換ルールを使用します。 |
| `visible`, `visibleInSearch`, `visibleInListing`, `visibleInCompareList` | `visibleIn[]` | フラグが`true`の場合、対応する値が追加されます：<br>`visible` → `PRODUCT_DETAIL`<br>`visibleInSearch` → `SEARCH_RESULTS`<br>`visibleInListing` → `PRODUCT_LISTING`<br>`visibleInCompareList` → `PRODUCT_COMPARE` |
| `filterable` | `filterable` | |
| `sortable` | `sortable` | |
| `searchable` | `searchable` | |
| `searchWeight` | `searchWeight` | |
| `searchTypes` | `searchTypes` | |

### データタイプ変換

`dataType`が`int`の場合、コネクタは`frontendInput`を確認します。 その他のデータ型の場合、`frontendInput`は変換に影響しません。

| 入力`dataType` | 入力`frontendInput` | 出力`dataType` |
| ---------------- | --------------------- | ----------------- |
| `int` | `boolean` | `BOOLEAN` |
| `int` | `text`または`select` | `TEXT` |
| `int` | 欠落している値を含む、その他の値 | `INTEGER` |
| `decimal` | 未使用 | `DECIMAL` |
| `text`, `varchar`, `static`, `datetime` | 未使用 | `TEXT` |
| `OBJECT` | 未使用 | `OBJECT` |
| その他の値 | 未使用 | `TEXT` |

>[!NOTE]
>
>属性が`OBJECT` データタイプを使用すると、[Products API](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"}は、その格納された値をJSONとして解析しようとします。 解析が成功した場合、APIは値をネストされたオブジェクトとして返します。 単一の値として表せない構造化属性データに`OBJECT`を使用します。 手順については、[製品属性を動的に追加する](../../data-export/add-attribute-dynamically.md)を参照してください。

## プライスブック

`priceBooks` フィードは、[価格表エンドポイント &#x200B;](https://developer.adobe.com/commerce/services/reference/rest/#tag/Price-Books){target="_blank"}にデータを送信します。

他のコネクタフィードとは異なり、`priceBooks` フィードは[!DNL Adobe Commerce]の[!DNL SaaS Data Export] インデクサーによって収集されません。 コネクターは、管理者のweb サイトと顧客グループ設定からこのフィードを生成します。

各web サイトについて、コネクターは顧客グループごとに1つの基本価格表と1つの子価格表を作成します。

`priceBookId`に次の数式を使用します。

- 通常価格の基本価格帳：`priceBookId = websiteCode`。
- 顧客グループの子価格表：`priceBookId = websiteCode::sha1(customerGroupId)`。`sha1(customerGroupId)`は、顧客グループの整数IDのSHA-1 1 16進ダイジェストです。

価格フィードでは、同じ数式を使用して、各価格入力を価格表に割り当てます。 ストアフロントが顧客セッションの`priceBookId`を解決する方法について詳しくは、[&#x200B; ヘッドレスストアフロント統合](../headless-storefront.md#graphql-commerceoptimizer-query)を参照してください。


| Source フィールドまたは値 | [!DNL Commerce Optimizer] API フィールド | マッピングの詳細 |
| ---------------- | -------------- | ------- |
| `websiteCode` | `parentId` | このフィールドを子価格表に追加します。 この値は、基準価格表を識別します。 |
| web サイト名 | `name` | 基本価格帳にweb サイト名を使用します。 子の価格表に`Customer group name (Website name)`を使用します。 |
| `websiteCode` | `parentId` | 子の価格表にのみ表示されます。基準価格表をポイントします |
| Web サイトのベース通貨 | `currency` | このフィールドは、基本価格帳にのみ含まれます。 子どもの価格表は省略します。 |

## 価格

`prices` フィードは[!DNL Adobe Commerce] データを[価格エンドポイント &#x200B;](https://developer.adobe.com/commerce/services/reference/rest/#tag/Prices){target="_blank"}に送信します。

| フィード入力フィールド | [!DNL Commerce Optimizer] API フィールド | マッピングの詳細 |
| --------------- | -------------- | ------------------------------------------------------------------------------- |
| `sku` | `sku` | SKUを変更せずに渡します。 |
| `websiteCode`, `customerGroupCode` | `priceBookId` | `websiteCode`を`customerGroupCode`の顧客グループ IDのSHA-1 ハッシュと組み合わせます。 `customerGroupCode`が`0`の場合、`websiteCode`のみを使用します。 |
| `regular` | `regular` | 通常価格を変えずに通過します。 |
| `discounts[]` | `discounts[]` | ソース値が`null`の場合、空の配列が書き出されます。<br>値が`0`から`100`の間の場合、`code`が`special_price`と`percentage`に設定されているエントリでは、`percentage`から`100 - percentage`に設定されます。 その範囲内または範囲外の`0`に設定します。<br>価格ベースの特別価格を含むその他のエントリを変更せずに渡します。 |
| `tierPrices[]` | `tierPrices[]` | ソース値が見つからない場合、または`null`の場合は、空の配列を使用します。 |

## カテゴリ

`categories` フィードは[!DNL Adobe Commerce] データを[&#x200B; カテゴリーエンドポイント &#x200B;](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="_blank"}に送信します。

空の`urlPath` （論理ルートカテゴリ）を持つ項目はスキップされ、送信されません。

| [!DNL Adobe Commerce] フィールド | [!DNL Commerce Optimizer] API フィールド | マッピングの詳細 |
| --------------- | -------------- | ------- |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlPath` | `slug` | |
| `description` | `description` | |
| `position` | `position` | 存在する場合は、カテゴリの位置を書き出します。 フィールドが見つからない場合は、フィールドを省略します。 |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeywords` | `metaTags/keywords` | 配列に分割された改行区切り文字列 |
| `image` | `images[].url` | 単一要素の配列；`roles: ["BASE"]` |
| `isActive` + `includeInMenu` | `families` | `true`と`[]`の両方が異なる場合は`["top_menu"]` |

| `metaKeywords` | `metaTags/keywords` |改行区切りのキーワードを配列に分割し、空白をトリミングします。 |
| `image` | `images[].url` | `image`が存在する場合、`BASE`の役割を持つ1つの画像を書き出します。 画像が空または見つからない場合は、空の配列を書き出します。 |
| `isActive` + `includeInMenu` | `families` |両方の値が`true`の場合にのみ`top_menu`を追加します。 それ以外の場合は、空の配列を書き出します。 |
| `attributes[]` | `attributes[]` |空でない`attributeCode`を含むエントリを`{code, values[]}`としてエクスポートします。 値を文字列に変換します。 対象となるエントリが存在しない場合、`attributes`を省略します。 |

>[!MORELIKETHIS]
>
> - [Data Ingestion API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"}を使用して製品と価格データを取り込む – メタデータ、製品、カテゴリ、価格表、価格のカタログデータモデルを学習します
> - [&#x200B; カタログデータ取り込みREST API リファレンス &#x200B;](https://developer.adobe.com/commerce/services/reference/rest/){target="_blank"} – 各フィードエンドポイントのリクエストと応答スキーマを確認します
> - [The [!DNL Commerce Optimizer Connector] と [!DNL Adobe Commerce]](../overview.md#how-the-connector-works-with-adobe-commerce)の連携の仕組み – ストア ビュー、web サイト、顧客グループがカタログ ソースと価格表にどのようにマッピングされるかを説明します
> - [の価格表 [!DNL Commerce Optimizer]](/help/optimizer/setup/pricebooks.md) — コネクタの書き出しによって作成された価格表を管理します
> - [&#x200B; ヘッドレスストアフロント統合](../headless-storefront.md#graphql-commerceoptimizer-query) – 顧客セッション用に`priceBookId`を解決
