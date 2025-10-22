---
title: API メッシュを使用した課税価格の表示
description: Adobe Commerceおよびカタログサービスに  [!DNL API Mesh]  を使用して、税を含む価格を表示します。
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
exl-id: ca62c653-29b9-45cf-b2d4-8cb693b08aac
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Adobe Developer App Builderの API メッシュで課税価格を表示

[API メッシュ &#x200B;](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) を使用すると、デベロッパーはAdobe I/O Runtimeを使用して、プライベートまたはサードパーティの API およびその他のインターフェイスをAdobe製品と統合できます。

このトピックでは、API メッシュを使用して、税金が設定された製品詳細ページに製品価格を表示します。

## 税率の設定

製品の詳細ページに表示するには、税金を設定する必要があります。

1. [&#x200B; 税率を設定します &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/taxes/tax-rules.html?lang=ja)。
1. 税金を [&#x200B; カタログに表示 &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/taxes/display-settings.html?lang=ja#step-1%3A-configure-catalog-prices-display-settings) できるようにして、`Including and Excluding Tax` または `Including Tax` に設定します。

製品の詳細ページを確認して、カタログサービスが機能していることを確認します。

![&#x200B; 製品詳細ページに表示される税金 &#x200B;](assets/display-tax.png)

## API メッシュの設定

まだ行っていない場合は、API メッシュとカタログサービスをインスタンスに接続します。 『 API メッシュ デベロッパーガイド』の [&#x200B; はじめに &#x200B;](https://developer.adobe.com/graphql-mesh-gateway/gateway/getting-started/) のトピックの詳細な手順を参照してください。

`mesh.json` ファイルで、`name`、`endpoint`、`x-api-key` の値を

```json
{
    "meshConfig": {
      "sources": [
        {
          "name": "<NAME OF MESH>",
          "handler": {
            "graphql": {
              "endpoint": "<COMMERCE INSTANCE GQL ENDPOINT URL>"
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
              "endpoint": "https://catalog-service-sandbox.adobe.io/graphql/",
              "operationHeaders": {
                "Magento-Store-View-Code": "{context.headers['magento-store-view-code']}",
                "Magento-Website-Code": "{context.headers['magento-website-code']}",
                "Magento-Store-Code": "{context.headers['magento-store-code']}",
                "Magento-Environment-Id": "{context.headers['magento-environment-id']}",
                "x-api-key": "API_KEY",
                "Magento-Customer-Group": "{context.headers['magento-customer-group']}"
              },
              "schemaHeaders": {
                "x-api-key": "<YOUR API_KEY>"
              }
            }
          }
        }
      ],
      "additionalTypeDefs": "extend type ComplexProductView {\n  priceWithTaxes: Core_PriceRange\n}\n extend type SimpleProductView {\n  priceWithTaxes: Core_PriceRange\n}\n",
      "additionalResolvers": [
            {  
              "targetTypeName": "ComplexProductView",
              "targetFieldName": "priceWithTaxes",
              "sourceName": "MagentoQACore",
              "sourceTypeName": "Query",
              "sourceFieldName": "Core_products",
              "requiredSelectionSet": "{\n items {\n sku, \n price_range {\n minimum_price {\n final_price {\n value\n currency\n }\n }\n }\n }\n }",
                "sourceArgs": {
                    "filter.sku.eq": "{root.sku}"
                },
                "result": "items[0].price_range"
            },
            {  
              "targetTypeName": "SimpleProductView",
              "targetFieldName": "priceWithTaxes",
              "sourceName": "MagentoQACore",
              "sourceTypeName": "Query",
              "sourceFieldName": "Core_products",
              "requiredSelectionSet": "{\n items {\n sku, \n price_range {\n minimum_price {\n final_price {\n value\n currency\n }\n }\n }\n }\n }",
                "sourceArgs": {
                    "filter.sku.eq": "{root.sku}"
                },
                "result": "items[0].price_range"
            }
        ]
     }
  }
```

この `mesh.json` 設定ファイルは次のとおりです。

* Commerce コアアプリケーションを、そのクエリまたはタイプの先頭に「Core_」を付加するように変換します。 これにより、カタログサービスとの名前の競合の可能性を防ぐことができます。
* `ComplexProductView` という新しいフィールドを使用して、`SimpleProductView` 型および `priceWithTaxes` 型を拡張します。
* 新しいフィールドのカスタムリゾルバーを追加します。

[&#x200B; ファイルで &#x200B;](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/#create-a-mesh-1)create コマンド `mesh.json` を使用してメッシュを作成します。

### GraphQL クエリ

GraphQLを使用して新しい `priceWithTaxes` データを取得できます。

クエリの例：

```graphql
query {
    products(skus:[MH07]) {
        __typename
        id
        sku
        name
        description
        shortDescription
        addToCartAllowed
        url
        ... on ComplexProductView {
            priceWithTaxes {
              minimum_price {
                final_price {
                  value
                }
              }
              maximum_price {
                final_price {
                  value
                }
              }
            }
            priceRange {
                maximum {
                    final {
                        amount {
                            value
                            currency
                        }
                    }
                    regular {
                        amount {
                            value
                            currency
                        }
                    }
                    roles
                }
                minimum {
                    final {
                        amount {
                            value
                            currency
                        }
                    }
                    regular {
                        amount {
                            value
                            currency
                        }
                    }
                    roles
                }
            }
        }
    }
}
```

クエリ応答：

```json
{
  "data": {
    "products": [
      {
        "__typename": "ComplexProductView",
        "id": "VFVnd053AFpHVm1ZWFZzZEEAWkRWa09Ua3hNVFl0WTJJd015MDBaRGMwTFRnME16a3RNak01TVRVNE9ESTBOemd4AGJXRnBibDkzWldKemFYUmxYM04wYjNKbABZbUZ6WlEAVFVGSE1EQTFPRFEyTVRjeA",
        "sku": "MH07",
        "name": "Hero Hoodie13",
        "description": "<p>Gray and black color blocking sets you apart as the Hero Hoodie keeps you warm on the bus, campus or cold mean streets. Slanted outsize front pockets keep your style real . . . convenient.</p>\r\n<p>* Full-zip gray and black hoodie.<br />* Ribbed hem.<br />* Standard fit.<br />* Drawcord hood cinch.<br />* Water-resistant coating.</p>",
        "shortDescription": "",
        "addToCartAllowed": true,
        "url": "http://commerce_url/hero-hoodie.html",
        "priceWithTaxes": {
          "minimum_price": {
            "final_price": {
              "value": 8.330001
            }
          },
          "maximum_price": {
            "final_price": {
              "value": 13355.524701
            }
          }
        },
        "priceRange": {
          "maximum": {
            "final": {
              "amount": {
                "value": 39.02,
                "currency": "USD"
              }
            },
            "regular": {
              "amount": {
                "value": 54,
                "currency": "USD"
              }
            },
            "roles": [
              "visible"
            ]
          },
          "minimum": {
            "final": {
              "amount": {
                "value": 39.02,
                "currency": "USD"
              }
            },
            "regular": {
              "amount": {
                "value": 54,
                "currency": "USD"
              }
            },
            "roles": [
              "visible"
            ]
          }
        }
      }
    ]
  },
  "extensions": {}
}
```
