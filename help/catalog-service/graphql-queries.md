---
title: '[!DNL Retrieve catalog data with GraphQL]'
description: GraphQL クエリを使用してカタログデータを取得することで、Commerce エクスペリエンスを強化できます。
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
source-git-commit: 935f34a8b4317686e67e33b50df3301d746fbd25
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# GraphQLでのカタログデータの取得 {#graphql-queries}

GraphQL クエリを使用して、商品、価格、その他のデータをAdobe Commerce カタログの SaaS データスペースから取得し、それを使用してAdobe Commerce GraphQLのネイティブなクエリよりも迅速にCommerceのエクスペリエンスをレンダリングします。

カタログサービスには次のクエリが用意されています。

| クエリ | 説明 | 使用状況 |
|-------|-------------|-------|
| `categories` | カテゴリデータを返します。 サブツリー入力オブジェクトが指定されている場合、クエリはサブカテゴリに関する詳細を返します。 | ストアフロントのナビゲーションページとカテゴリページのレンダリングに役立ちます。 [ 例を参照。](https://developer.adobe.com/commerce/services/graphql/catalog-service/categories/) |
| `products` | 入力として指定された SKU に関する詳細を返します。 | 主に製品の詳細ページや製品比較ページでコンテンツをレンダリングするために使用されます。 [ 例を参照。](https://developer.adobe.com/commerce/services/graphql/catalog-service/categories/) |
| `productSearch` | 検索条件に一致する製品のリストを返します。 | 検索入力に基づいて検索結果や製品リストページをレンダリングする場合に役立ちます。 [ 例を参照。](https://developer.adobe.com/commerce/services/graphql/catalog-service/products/) |
| `refineProduct` | 複雑な製品に対して実行された製品クエリの結果を絞り込んで、製品バリアントに関する特定の情報を返します。 | 買い物客が製品オプションを選択する際に、更新された製品詳細ページをレンダリングするのに役立ちます。 [ 例を参照。](https://developer.adobe.com/commerce/services/graphql/catalog-service/refine-product/) |
| `variants` | 商品のすべてのバリエーションに関する詳細を返します。 | 複数の API リクエストを送信せずに、製品の詳細にバリアント画像を表示したり、ページを一覧表示したりするのに便利です。 [ 例を参照。](https://developer.adobe.com/commerce/services/graphql/catalog-service/product-variants/) |


これらのクエリの使用について詳しくは、[Catalog Service API ガイド ](https://developer.adobe.com/commerce/services/graphql/catalog-service/) を参照してください

