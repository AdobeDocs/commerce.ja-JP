---
title: GraphQL
description: ' [!DNL Live Search] GraphQL Workspace では、ライブデータを使用してクエリを作成できます。'
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '39'
ht-degree: 0%

---

# GraphQL

*GraphQL* ワークスペースを使用すると、管理者は、独自のデータを使用してGraphQL クエリを作成およびテストできます。

このワークスペースでは、[`productSearch`](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/) クエリと [`attributeMetadata`](https://developer.adobe.com/commerce/services/graphql/live-search/attribute-metadata/) クエリをサポートしています。

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

