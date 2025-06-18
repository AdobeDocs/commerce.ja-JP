---
title: カスタムの自動照合
description: カスタム自動照合が、複雑な照合ロジックを持つマーチャントや、製品ビジュアルのメタデータをAEM Assetsに入力できないサードパーティシステムに依存するマーチャントにとって、特に便利な方法を説明します。
feature: CMS, Media, Integration
source-git-commit: 3ecc429003490235211a812af064d1b10d053e38
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# カスタムの自動照合

デフォルトの自動一致戦略（**OOTB 自動一致**）が特定のビジネス要件に合っていない場合は、「カスタム一致」オプションを選択します。 このオプションでは、複雑なマッチングロジックを処理するカスタムマッチャーアプリケーションの開発 ](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder)0}Adobe Developer App Builder} の使用、または製品ビジュアルのメタデータをAEM Assetsに入力できないサードパーティシステムからのアセットの開発がサポートされます。[

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
 
async function main (params) {
    // return the products that map to the assetId
    return {
        statusCode: 200,
        body: {
          asset_id: "urn:aaid:aem:1aa1d4a0-18b8-40a7-a228-e0ab588deee1",
          product_matches: [
            {
              product_sku: "SKU1",
              asset_roles: ["thumbnail"],
              asset_position: [1]
            }
          ]
        }
   }
}
 
exports.main = main
```

**リクエスト**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| パラメーター | データタイプ | 説明 |
| --- | --- | --- |
| `assetId` | 文字列 | 更新されたアセット ID を表します |

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
 
async function main (params) {
    // return asset matches for a product
    return {
        statusCode: 200,
        body: {
          product_sku: params.productSku, //SKU-1
          asset_matches: [
            {
              asset_id: "urn:aaid:aem:1aa1d4a0-18b8-40a7-a228-e0ab588deee1",
              asset_roles: ["thumbnail","image"]
            }
          ]
        }
      }
}
 
exports.main = main
```

**リクエスト**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| パラメーター | データタイプ | 説明 |
| --- | --- | --- |
| `productSKU` | 文字列 | 更新された製品 SKU を表します |

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

>[!TIP]
>
> `asset_roles` キーでは、`thumbnail`、`image`、`small_image`、`swatch_image` など ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles) サポートされる [Commerce アセットの役割を使用します。
