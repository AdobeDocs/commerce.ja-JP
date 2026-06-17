---
title: '[!DNL Adobe Commerce Optimizer Connector]個のヘッドレスストアフロント統合'
description: ' [!DNL Adobe Commerce Optimizer Connector] GraphQL API、価格表ID、バンドルのカートへの追加エンコーディングを使用して、ヘッドレスストアフロントを統合する方法について説明します。'
feature: Storefront, Integration, GraphQL
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
autotag-review: '2026-06-09T16:27:30.102Z'
TQID: 'https://experienceleague.adobe.com/Orif1rROglTQ-3ZkRj5LMF90Y-AdpfTnOgPmJXQjYgc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 237
ht-degree: 0%

---

# ヘッドレスストアフロントの統合

`CommerceAdapter` モジュールは、[!DNL Adobe Commerce]を拡張して、ヘッドレスストアフロントと[!DNL Adobe Commerce Optimizer]のギャップを埋めます。 お客様の価格表のコンテキストを解決するためのGraphQL クエリを提供し、[!DNL Adobe Commerce Optimizer] GraphQL APIで想定されるバンドル製品エンコーディングを適用します。

上位レベルのストアフロントの設定手順については、[!DNL Adobe Commerce Optimizer Connector]概要の[&#x200B; マーチャンダイジングとストアフロントの設定](./overview.md#merchandising-storefronts)を参照してください。

## GraphQL: `commerceOptimizer` クエリ {#graphql-commerceoptimizer-query}

ヘッドレスストアフロントは、`commerceOptimizer` GraphQL クエリを呼び出して、現在のカスタマーセッションの`priceBookId`を取得します。 価格を取得する際に、この値を[[!DNL Adobe Commerce Optimizer] GraphQL API](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api){target="_blank"}に渡します。

```graphql
{
  commerceOptimizer {
    priceBookId
  }
}
```

応答の例：

```json
{
  "data": {
    "commerceOptimizer": {
      "priceBookId": "base::a94a8fe5ccb19ba61c4c0873d391e987982fbbd3"
    }
  }
}
```

`priceBookId`の解決方法：

| セッションの状態 | `priceBookId` |
|-----------------------|---------------------------------------------------------------------|
| ゲスト （ログインしていません） | `websiteCode::sha1(0)`。`0`はゲスト顧客グループ ID |
| ログインしたお客様 | `websiteCode::sha1(customerGroupId)` |

`Store` リクエストヘッダーは、web サイトのスコープと`websiteCode` コンポーネントを決定します。 `sha1(customerGroupId)` コンポーネントは、データの同期中に使用された価格表ID式と一致します。 [価格表](reference/field-mapping.md#price-books)を参照してください。

## バンドル製品：カートに追加する形式 {#bundle-products-add-to-cart-format}

選択した各バンドルオプションの`SKU`と`qty`のみを含むヘッドレスストアフロントから、買い物客がカートにバンドル製品を追加できるようにします。

選択または入力された各オプション値は、次の形式でbase64 エンコードされている必要があります。

```text
base64("bundle_item/" + JSON.stringify({"sku": "<child_sku>", "qty": "<qty>"}))
```

同じ子SKUは、すべてのオプションで1回のみ表示されます。

例（[!DNL JavaScript]）:

```javascript
const encodedOption = btoa(
  'bundle_item/' + JSON.stringify({ sku: 'child-product-sku', qty: '1' })
);
```
