---
title: '[!DNL Retrieve catalog data with GraphQL]'
description: GraphQLのクエリを使用してカタログデータを取得し、Commerceのエクスペリエンスを強化します。
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
exl-id: 49bbdb3b-bbe9-4777-8ea7-3bd25ae53889
TQID: https://experienceleague.adobe.com/ahutwotbB6Dxg7Tc3WMFd7S-WBMALvOYIUTmB5JKmyM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 268
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
