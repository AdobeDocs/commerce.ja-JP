---
title: カスタムの自動照合
description: カスタム自動照合が、複雑な照合ロジックを持つマーチャントや、メタデータをAEM Assetsに入力できないサードパーティシステムに依存するマーチャントにとって特に役立つ仕組みを説明します。
feature: CMS, Media, Integration
exl-id: e7d5fec0-7ec3-45d1-8be3-1beede86c87d
source-git-commit: ff6affa5bcc4111e14054f3f6b3ce970619ca295
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---

# カスタムの自動照合

デフォルトの自動一致戦略（**OOTB 自動一致**）が特定のビジネス要件に合っていない場合は、「カスタム一致」オプションを選択します。 このオプションは、複雑なマッチングロジックを処理するカスタムマッチャーアプリケーションや、メタデータをAdobe Developer App Builderに入力できないサードパーティシステムからのアセットを開発する [0&rbrace;AEM Assets&rbrace; の使用をサポートします。](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder)

## カスタムの自動照合を設定

1. Commerce管理者から、**[!UICONTROL Store]** /設定/ **[!UICONTROL ADOBE SERVICES]** / **[!UICONTROL AEM Assets Integration]** に移動します。

1. 一致ルールとして「**[!UICONTROL Custom Matcher]**」を選択します。

1. この一致ルールを選択すると、カスタム一致ロジックに必要な **認証パラメーター** および **エンドポイント** を設定するための追加フィールドが表示されます。

## カスタムマッチャー API エンドポイント

[App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder){target=_blank} を使用してカスタムマッチャーアプリケーションを作成する場合、アプリケーションは次のエンドポイントを公開する必要があります。

* **App Builder asset to product URL** endpoint
* **App Builder製品からアセットの URL** エンドポイント

### App Builder asset to product URL endpoint

このエンドポイントは、特定のアセットに関連付けられた SKU のリストを取得します。

#### 使用例

```bash
const { Core } = require('@adobe/aio-sdk')

async function main(params) {

    // Build your own matching logic here to return the products that map to the assetId
    // var productMatches = [];
    // params.assetId
    // params.eventData.assetMetadata['commerce:isCommerce']
    // params.eventData.assetMetadata['commerce:skus'][i]
    // params.eventData.assetMetadata['commerce:roles']
    // params.eventData.assetMetadata['commerce:positions'][i]
    // ...
    // End of your matching logic

    return {
        statusCode: 500,
        body: {
            asset_id: params.assetId,
            product_matches: [
                {
                    product_sku: "<YOUR-SKU-HERE>",
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_position: 1
                }
            ]
        }
    };
}

exports.main = main;
```

**リクエスト**

```bash
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| パラメーター | データタイプ | 説明 |
| --- | --- | --- |
| `assetId` | 文字列 | 更新されたアセット ID を表します |
| `eventData` | 文字列 | `assetId` に関連付けられたデータペイロードを返します |

**応答**

```bash
{
  "asset_id": "{ASSET_ID}",
  "product_matches": [
    {
      "product_sku": "{PRODUCT_SKU_1}",
      "asset_roles": ["thumbnail","image"]
    },
    {
      "product_sku": "{PRODUCT_SKU_2}",
      "asset_roles": ["thumbnail"]
    }
  ]
}
```

### App Builder製品からアセット URL のエンドポイント

このエンドポイントは、特定の SKU に関連付けられたアセットのリストを取得します。

#### 使用例

```bash
const { Core } = require('@adobe/aio-sdk')

async function main(params) {
    // return asset matches for a product
    // Build your own matching logic here to return the assets that map to the productSku
    // var assetMatches = [];
    // params.productSku
    // ...
    // End of your matching logic

    return {
        statusCode: 500,
        body: {
            product_sku: params.productSku,
            asset_matches: [
                {
                    asset_id: "<YOUR-ASSET-ID-HERE>", // urn:aaid:aem:1aa1d5i2-17h8-40a7-a228-e3ur588deee1
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_format: "image", // can be "image" or "video"
                    asset_position: 1
                }
            ]
        }
    };
}

exports.main = main;
```

**リクエスト**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| パラメーター | データタイプ | 説明 |
| --- | --- | --- |
| `productSKU` | 文字列 | 更新された製品 SKU を表します。 |
| `asset_matches` | 文字列 | 特定のア `productSku` ットに関連付けられているすべてのアセットを返します。 |

`asset_matches` パラメーターには、次の属性が含まれます。

| 属性 | データタイプ | 説明 |
| --- | --- | --- |
| `asset_id` | 文字列 | 更新されたアセット ID を表します。 |
| `asset_roles` | 文字列 | 使用可能なすべてのアセットの役割を返します。 [、](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles)、`thumbnail`、`image` など `small_image` サポートされる `swatch_image`Commerce アセットの役割を使用します。 |
| `asset_format` | 文字列 | アセットで使用可能な形式を提供します。 使用可能な値は `image` および `video` です。 |
| `asset_position` | 文字列 | アセットの位置を表示します。 |

**応答**

```bash
{
  "product_sku": "{PRODUCT_SKU}",
  "asset_matches": [
    {
      "asset_id": "{ASSET_ID_1}",
      "asset_roles": ["thumbnail","image"]
    },
    {
      "asset_id": "{ASSET_ID_2}",
      "asset_roles": ["thumbnail"]
    }
  ]
}
```
