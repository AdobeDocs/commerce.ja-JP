---
title: '[!DNL Catalog Service and API Mesh]'
description: '[!DNL API Mesh] for Adobe Commerceを使用すると、共通のGraphQL エンドポイントを介して複数のデータソースを統合できます。'
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
exl-id: 903f4f96-6dba-4c45-8106-76d9845544ec
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# [!DNL Catalog Service and API Mesh]

Adobe Developer App Builderの [API メッシュ ](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) を使用すると、デベロッパーはAdobe I/O Runtimeを使用して、プライベートまたはサードパーティの API およびその他のインターフェイスをAdobe製品と統合できます。

![ カタログのアーキテクチャ図 ](assets/catalog-service-architecture-mesh.png)

カタログサービスで API メッシュを使用するには、API メッシュをインスタンスに接続し、カタログサービスに接続するための設定を提供する API メッシュソース [CommerceCatalogServiceGraph](https://github.com/adobe/api-mesh-sources/blob/main/connectors/) を追加する必要があります。

## API メッシュを接続して設定します。

1. [API メッシュ開発者ガイド ](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/) の _メッシュを作成する_ 手順に従って、Adobe Commerce インスタンスに API メッシュを接続します。

   API メッシュを初めて使用する場合は、メッシュを作成する前に [ はじめに ](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/) プロセスを完了してください。

1. 次の形式を使用して、プロジェクトの Catalog Service API キーを含む `variables.json` などの JSON ファイルを作成します。

   ```json
   {
       "CATALOG_SERVICE_API_KEY":"your_api_key"
   }
   ```

1. `CommerceCatalogServiceGraph`Adobe I/O拡張可能 CLI[ を使用して、](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/#install-the-aio-cli) ソースをメッシュに追加します。

   ```bash
   aio api-mesh source install "CommerceCatalogServiceGraph" -f variables.json
   ```

   `-f variables.json` オプションは、設定の更新に必要な Catalog Service API キー値を提供します。

このコマンドを実行すると、API メッシュを介してカタログサービスが実行されます。 `aio api-mesh get` コマンドを使用して、更新されたメッシュの設定を表示します。

## API メッシュの例

API メッシュを使用すると、外部データソースを使用してAdobe Commerce インスタンスを強化できます。 また、既存のCommerce データを設定して新しい機能を有効にすることもできます。

### 階層価格を有効にする

この例では、API メッシュを使用して、Adobe Commerceで階層価格を有効にします。
`name`、`endpoint`、`x-api-key` の値を置き換えます。

```json
{
  "meshConfig": {
    "sources": [
      {
        "name": "<Commerce Instance Name>",
        "handler": {
          "graphql": {
            "endpoint": "<Adobe Commerce GraphQL endpoint>"
          }
        },
        "transforms": [
            {
                "prefix": {
                    "includeRootOperations": true,
                    "value": "Core_"
                }
            }
        ]
      },
      {
        "name": "CommerceCatalogServiceGraph",
        "handler": {
          "graphql": {
            "endpoint": "https://commerce.adobe.io/catalog-service/graphql/",
            "operationHeaders": {
              "Magento-Store-View-Code": "{context.headers['magento-store-view-code']}",
              "Magento-Website-Code": "{context.headers['magento-website-code']}",
              "Magento-Store-Code": "{context.headers['magento-store-code']}",
              "Magento-Environment-Id": "{context.headers['magento-environment-id']}",
              "Magento-Customer-Group": "{context.headers['magento-customer-group']}"
            },
            "schemaHeaders": {
              "x-api-key": "<YOUR API-KEY>"
            }
          }
        }
      }
    ],
    "additionalTypeDefs": "extend interface ProductView {\n  price_tiers: [Core_TierPrice]\n}\n extend type SimpleProductView {\n  price_tiers: [Core_TierPrice]\n}\n extend type ComplexProductView {\n  price_tiers: [Core_TierPrice]\n}\n",
    "additionalResolvers": [
        {  
            "targetTypeName": "ProductView",
            "targetFieldName": "price_tiers",
            "sourceName": "MagentoStageCore",
            "sourceTypeName": "Query",
            "sourceFieldName": "Core_products",
            "requiredSelectionSet": "{\n    items {\n  sku\n    price_tiers {\n        quantity,\n        final_price {\n          value\n          currency\n        }\n      }\n    }\n  }",
            "sourceArgs": {
                "filter.sku.eq": "{root.sku}"
            },
            "result": "items[0].price_tiers"
        },
        {  
            "targetTypeName": "SimpleProductView",
            "targetFieldName": "price_tiers",
            "sourceName": "MagentoStageCore",
            "sourceTypeName": "Query",
            "sourceFieldName": "Core_products",
            "requiredSelectionSet": "{\n    items {\n  sku\n    price_tiers {\n        quantity,\n        final_price {\n          value\n          currency\n        }\n      }\n    }\n  }",
            "sourceArgs": {
                "filter.sku.eq": "{root.sku}"
            },
            "result": "items[0].price_tiers"
        },
        {  
            "targetTypeName": "ComplexProductView",
            "targetFieldName": "price_tiers",
            "sourceName": "MagentoStageCore",
            "sourceTypeName": "Query",
            "sourceFieldName": "Core_products",
            "requiredSelectionSet": "{\n    items {\n  sku\n    price_tiers {\n        quantity,\n        final_price {\n          value\n          currency\n        }\n      }\n    }\n  }",
            "sourceArgs": {
                "filter.sku.eq": "{root.sku}"
            },
            "result": "items[0].price_tiers"
        }
    ]
   }
}
```

設定が完了したら、メッシュに対して階層化された価格のクエリを実行します。

```graphql
query {
  products(skus: ["24-MB04"]) {
    sku
    description
    price_tiers {
        quantity
        final_price {
          value
          currency
        }
      }
    ... on SimpleProductView {
      id
       
      price {
        final {
          amount {
            value
          }
        }
      }
    }
  }
}
```

### エンティティ ID を取得

このメッシュは、`entityId` を ProductView インタフェースに追加します。 `name`、`endpoint`、`x-api-key` の値を置き換えます。

```json
{
    "meshConfig": {
      "sources": [
        {
          "name": "<Commerce Instance Name>",
          "handler": {
            "graphql": {
              "endpoint": "<Adobe Commerce GraphQL endpoint>"
            }
          },
          "transforms": [
              {
                  "prefix": {
                      "includeRootOperations": true,
                        "value": "Core_"
                  }
              }
          ]
        },
        {
          "name": "CommerceCatalogServiceGraph",
          "handler": {
            "graphql": {
              "endpoint": "https://catalog-service.adobe.io/graphql",
              "operationHeaders": {
                "Magento-Store-View-Code": "{context.headers['magento-store-view-code']}",
                "Magento-Website-Code": "{context.headers['magento-website-code']}",
                "Magento-Store-Code": "{context.headers['magento-store-code']}",
                "Magento-Environment-Id": "{context.headers['magento-environment-id']}",
                "x-api-key": "<YOUR_CATALOG_SERVICE_API_KEY>",
                "Magento-Customer-Group": "{context.headers['magento-customer-group']}"
              },
              "schemaHeaders": {
                "x-api-key": "<YOUR_CATALOG_SERVICE_API_KEY>"
              }
            }
          }
        }
      ],
      "additionalTypeDefs": "extend interface ProductView {\n  entityId: String\n}\n extend type SimpleProductView {\n  entityId: String\n}\n extend type ComplexProductView {\n  entityId: String\n}\n",
      "additionalResolvers": [
        {  
            "targetTypeName": "ComplexProductView",
            "targetFieldName": "entityId",
            "sourceName": "MagentoCore",
            "sourceTypeName": "Query",
            "sourceFieldName": "Core_products",
            "requiredSelectionSet": "{ sku\n }",
            "sourceSelectionSet": "{\n    items {\n  sku\n uid\n  }\n    }",
            "sourceArgs": {
                "filter.sku.eq": "{root.sku}"
            },
            "result": "items[0].uid",
            "resultType": "String"
          },
          {
            "targetTypeName": "SimpleProductView",
            "targetFieldName": "entityId",
            "sourceName": "MagentoCore",
            "sourceTypeName": "Query",
            "sourceFieldName": "Core_products",
            "requiredSelectionSet": "{ sku\n }",
            "sourceSelectionSet": "{\n items {\n  sku\n uid\n }}",
            "sourceArgs": {
                "filter.sku.eq": "{root.sku}"
            },
            "result": "items[0].uid",
            "resultType": "String"
          }
      ]
    }
  }
```

`entityId` をクエリできるようになりました。

```graphql
query {
  products(skus: ["MH07"]){
    sku
    name
    id
    entityId
  }
}
```
