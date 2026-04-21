---
title: '[!DNL Retrieve catalog data with GraphQL]'
description: GraphQLのクエリを使用してカタログデータを取得し、Commerceのエクスペリエンスを強化します。
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
exl-id: 49bbdb3b-bbe9-4777-8ea7-3bd25ae53889
source-git-commit: a4c3a24deb77a9aadc7954b46d171b4d4edea6ba
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# GraphQLによるカタログデータの取得 {#graphql-queries}

GraphQLのクエリを使用すると、Adobe Commerce CatalogのSaaS データスペースから商品、価格などのデータを取得し、ネイティブのAdobe Commerce GraphQL クエリよりも迅速にCommerce エクスペリエンスをレンダリングできます。

{{aco-merchandising-services}}

カタログサービスには、次のクエリが用意されています。

| クエリ | 説明 | 使用状況 |
|-------|-------------|-------|
| `categories` | カテゴリデータを返します。 サブツリー入力オブジェクトが指定されている場合、クエリはサブカテゴリに関する詳細を返します。 | ストアフロントのナビゲーションやカテゴリーページのレンダリングに便利です。 [例を参照してください。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `products` | 入力として指定されたSKUの詳細を返します。 | 主に、製品詳細ページと製品比較ページでコンテンツをレンダリングするために使用します。 [例を参照してください。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `productSearch` | 検索条件に一致する商品のリストを返します。 | 検索結果と、検索入力に基づく商品リストページのレンダリングに便利です。 [例を参照してください。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) |
| `refineProduct` | 複雑な製品に対して実行される製品クエリの結果を絞り込み、製品バリエーションに関する特定の情報を返します。 | 買い物客が商品オプションを選択したときに、更新された商品詳細ページをレンダリングするのに便利です。 [例を参照してください。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) |
| `variants` | 製品のすべてのバリエーションに関する詳細を返します。 | 複数のAPI リクエストを送信することなく、製品詳細またはリストページにバリエーション画像を表示するのに便利です。 [例を参照してください。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/product-variants/) |

これらのクエリの使用方法について詳しくは、[Storefront Services GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)を参照してください。
