---
title: GraphQL
description: ' [!DNL Live Search] GraphQL Workspace では、ライブデータを使用してクエリを作成できます。'
exl-id: d32edf42-1fb0-40f9-89e5-798b39521b77
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '39'
ht-degree: 0%

---

# GraphQL

*GraphQL* ワークスペースを使用すると、管理者は、独自のデータを使用してGraphQL クエリを作成およびテストできます。

このワークスペースでは、[`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) クエリと [`attributeMetadata`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/attribute-metadata/) クエリをサポートしています。

![GraphQL Workspace](assets/graphql.png)

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
