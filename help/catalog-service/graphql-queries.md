---
title: '[!DNL Retrieve catalog data with GraphQL]'
description: GraphQL クエリを使用してカタログデータを取得することで、Commerce エクスペリエンスを強化できます。
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
exl-id: 49bbdb3b-bbe9-4777-8ea7-3bd25ae53889
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# GraphQLでのカタログデータの取得 {#graphql-queries}

GraphQL クエリを使用して、商品、価格、その他のデータをAdobe Commerce カタログの SaaS データスペースから取得し、それを使用してAdobe Commerce GraphQLのネイティブなクエリよりも迅速にCommerceのエクスペリエンスをレンダリングします。

カタログサービスには次のクエリが用意されています。

| クエリ | 説明 | 使用状況 |
|-------|-------------|-------|
| `categories` | カテゴリデータを返します。 サブツリー入力オブジェクトが指定されている場合、クエリはサブカテゴリに関する詳細を返します。 | ストアフロントのナビゲーションページとカテゴリページのレンダリングに役立ちます。 [&#x200B; 例を参照。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `products` | 入力として指定された SKU に関する詳細を返します。 | 主に製品の詳細ページや製品比較ページでコンテンツをレンダリングするために使用されます。 [&#x200B; 例を参照。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `productSearch` | 検索条件に一致する製品のリストを返します。 | 検索入力に基づいて検索結果や製品リストページをレンダリングする場合に役立ちます。 [&#x200B; 例を参照。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) |
| `refineProduct` | 複雑な製品に対して実行された製品クエリの結果を絞り込んで、製品バリアントに関する特定の情報を返します。 | 買い物客が製品オプションを選択する際に、更新された製品詳細ページをレンダリングするのに役立ちます。 [&#x200B; 例を参照。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) |
| `variants` | 商品のすべてのバリエーションに関する詳細を返します。 | 複数の API リクエストを送信せずに、製品の詳細にバリアント画像を表示したり、ページを一覧表示したりするのに便利です。 [&#x200B; 例を参照。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/product-variants/) |

これらのクエリの使用について詳しくは、[Catalog Service API ガイド &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/) を参照してください
