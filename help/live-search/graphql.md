---
title: GraphQL
description: ' [!DNL Live Search] GraphQL ワークスペースでは、ライブデータを使用してクエリを作成できます。'
exl-id: d32edf42-1fb0-40f9-89e5-798b39521b77
TQID: https://experienceleague.adobe.com/y-aM85yTrJA6JNXlJeacXEOkr8l-Bwij9gdVCgNGEqY
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 58
ht-degree: 0%

---

# GraphQL

*GraphQL* ワークスペースを使用すると、管理者は自分のデータを使用してGraphQL クエリを作成およびテストできます。

このワークスペースは、[`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/)および[`attributeMetadata`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/attribute-metadata/) クエリをサポートしています。

![GraphQL workspace](assets/graphql.png)

```graphql
query productSearch {
  productSearch(phrase: "a306") {
    total_count
    items {
      product {
        sku
        name
      }
    }
    facets {
      title
    }
  }
}
```

変数：

```json
{
  "Magento-Environment-Id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "Magento-Website-Code": "base",
  "Magento-Store-Code": "base",
  "Magento-Store-View-Code": "default",
  "X-Api-Key": "search_gql"
}
```
