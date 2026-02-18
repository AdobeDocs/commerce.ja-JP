---
title: カスタムの自動照合
description: カスタム自動照合が、複雑な照合ロジックを持つマーチャントや、メタデータをAEM Assetsに入力できないサードパーティシステムに依存するマーチャントにとって特に役立つ仕組みを説明します。
feature: CMS, Media, Integration
exl-id: e7d5fec0-7ec3-45d1-8be3-1beede86c87d
source-git-commit: 6e8d266aeaec4d47b82b0779dfc3786ccaa7d83a
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# カスタムの自動照合

デフォルトの自動一致戦略（**OOTB 自動一致**）が特定のビジネス要件に合っていない場合は、「カスタム一致」オプションを選択します。 このオプションは、複雑なマッチングロジックを処理するカスタムマッチャーアプリケーションや、メタデータをAdobe Developer App Builderに入力できないサードパーティシステムからのアセットを開発する [0&rbrace;AEM Assets&rbrace; の使用をサポートします。](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder)

## カスタムの自動照合を設定

1. Commerce管理者から、**[!UICONTROL Store]** /設定/ **[!UICONTROL ADOBE SERVICES]** / **[!UICONTROL AEM Assets Integration]** に移動します。

1. 一致ルールとして「**[!UICONTROL Custom Matcher]**」を選択します。

1. この一致ルールを選択すると、カスタム一致ロジックに必要な **認証パラメーター** および **エンドポイント** を設定するための追加フィールドが表示されます。

### workspace.json

**[!UICONTROL Adobe I/O Workspace Configuration]** フィールドを使用すると、App Builder `workspace.json` 設定ファイルを読み込むことで、カスタムマッチャーを効率的に設定できます。

`workspace.json` ファイルは [1&rbrace;Adobe Developer Console&rbrace; からダウンロードできます。 &#x200B;](https://developer.adobe.com/console)このファイルには、App Builder Workspace のすべての資格情報と設定の詳細が含まれています。

+++例 `workspace.json`

```json
{
  "project": {
    "id": "project_id",
    "name": "project_name",
    "title": "title_name",
    "org": {
      "id": "id",
      "name": "Organization_name",
      "ims_org_id": "ims_id"
    },
    "workspace": {
      "id": "workspace_id",
      "name": "workspace_name_id",
      "title": "workspace_title_id",
      "action_url": "https://action_url.net",
      "app_url": "https://app_url.net",
      "details": {
        "credentials": [
          {
            "id": "credential_id",
            "name": "credential_name_id",
            "integration_type": "oauth_server_to_server",
            "oauth_server_to_server": {
              "client_id": "client_id",
              "client_secrets": ["secret"],
              "technical_account_email": "xx@technical_account_email.com",
              "technical_account_id": "technical_account_id",
              "scopes": [
                "AdobeID",
                "openid",
                "read_organizations",
                "additional_info.projectedProductContext",
                "additional_info.roles",
                "adobeio_api",
                "read_client_secret",
                "manage_client_secrets"
              ]
            }
          }
        ],
        "services": [
          {
            "code": "AdobeIOManagementAPISDK",
            "name": "I/O Management API"
          }
        ],
        "runtime": {
          "namespaces": [
            {
              "name": "namespace_name",
              "auth": "example_auth"
            }
          ]
        },
        "events": {
          "registrations": []
        },
        "mesh": {}
      }
    }
  }
}
```

+++

1. App Builder プロジェクトから `workspace.json` ファイルを「**[!UICONTROL Adobe I/O Workspace Configuration]**」フィールドにドラッグ&amp;ドロップします。 または、をクリックして、ファイルを参照して選択することもできます。

![Workspaceの設定 &#x200B;](../assets/workspace-configuration.png){width="600" zoomable="yes"}

1. システムは自動的に次の処理を行います。

   * JSON 構造を検証します。
   * OAuth 認証情報を抽出して入力します
   * ワークスペースで使用可能な実行時アクションを取得します
   * 「**[!UICONTROL Product to Asset URL]**」フィールドと「**[!UICONTROL Asset to Product URL]**」フィールドのドロップダウンオプションを入力します

1. 各フローのドロップダウンメニューから適切な実行時アクションを選択します。

1. 「**[!UICONTROL Save Config]**」をクリックします。

## カスタムマッチャー API エンドポイント

[App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder){target=_blank} を使用してカスタムマッチャーアプリケーションを作成する場合、アプリケーションは次のエンドポイントを公開する必要があります。

* **App Builder asset to product URL** endpoint
* **App Builder製品からアセットの URL** エンドポイント

### App Builder asset to product URL endpoint

このエンドポイントは、特定のアセットに関連付けられた SKU のリストを取得します。

#### 使用例

```javascript
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

    // Set skip to true if the mapping hasn't changed
    const skipSync = false;

    return {
        statusCode: 200,
        body: {
            asset_id: params.assetId,
            product_matches: [
                {
                    product_sku: "<YOUR-SKU-HERE>",
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_position: 1
                }
            ],
            skip: skipSync
        }
    };
}

exports.main = main;
```

**リクエスト**

```text
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| パラメーター | データタイプ | 説明 |
| --- | --- | --- |
| `assetId` | 文字列 | 更新されたアセット ID を表します。 |
| `eventData` | 文字列 | アセット ID に関連付けられたデータペイロードを返します。 |

**応答**

```json
{
  "asset_id": "{ASSET_ID}",
  "product_matches": [
    {
      "product_sku": "{PRODUCT_SKU_1}",
      "asset_roles": ["thumbnail", "image"]
    },
    {
      "product_sku": "{PRODUCT_SKU_2}",
      "asset_roles": ["thumbnail"]
    }
  ],
  "skip": false
}
```

| パラメーター | データタイプ | 説明 |
| --- | --- | --- |
| `asset_id` | 文字列 | 一致させるアセット ID。 |
| `product_matches` | 配列 | アセットに関連付けられている製品のリスト。 |
| `skip` | ブール値 | （任意） `true` の場合、ルールエンジンはこのアセットの同期をスキップします（製品マッピングは更新されません）。 `false` 省略すると、通常の処理が実行されます。 [&#x200B; 同期処理をスキップ &#x200B;](#skip-sync-processing) を参照してください。 |

### App Builder製品からアセット URL のエンドポイント

このエンドポイントは、特定の SKU に関連付けられたアセットのリストを取得します。

#### 使用例

```javascript
const { Core } = require('@adobe/aio-sdk')

async function main(params) {
    // return asset matches for a product
    // Build your own matching logic here to return the assets that map to the productSku
    // var assetMatches = [];
    // params.productSku
    // ...
    // End of your matching logic

    // Set skip to true if the mapping hasn't changed
    const skipSync = false;

    return {
        statusCode: 200,
        body: {
            product_sku: params.productSku,
            asset_matches: [
                {
                    asset_id: "<YOUR-ASSET-ID-HERE>", // urn:aaid:aem:1aa1d5i2-17h8-40a7-a228-e3ur588deee1
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_format: "image", // can be "image" or "video"
                    asset_position: 1
                }
            ],
            skip: skipSync
        }
    };
}

exports.main = main;
```

**リクエスト**

```text
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| パラメーター | データタイプ | 説明 |
| --- | --- | --- |
| `productSKU` | 文字列 | 更新された製品 SKU を表します。 |
| `eventData` | 文字列 | 製品 SKU に関連付けられているデータペイロードを返します。 |

**応答**

```json
{
  "product_sku": "{PRODUCT_SKU}",
  "asset_matches": [
    {
      "asset_id": "{ASSET_ID_1}",
      "asset_roles": ["thumbnail", "image"],
      "asset_position": 1,
      "asset_format": "image"
    },
    {
      "asset_id": "{ASSET_ID_2}",
      "asset_roles": ["thumbnail"],
      "asset_position": 2,
      "asset_format": "image"
    }
  ],
  "skip": false
}
```

| パラメーター | データタイプ | 説明 |
| --- | --- | --- |
| `product_sku` | 文字列 | 照合する製品 SKU。 |
| `asset_matches` | 配列 | 製品に関連付けられているアセットのリスト。 |
| `skip` | ブール値 | （任意） `true` の場合、ルールエンジンはこの製品の同期をスキップします（アセットマッピングが更新されません）。 `false` 省略すると、通常の処理が実行されます。 [&#x200B; 同期処理をスキップ &#x200B;](#skip-sync-processing) を参照してください。 |

`asset_matches` パラメーターには、次の属性が含まれます。

| 属性 | データタイプ | 説明 |
| --- | --- | --- |
| `asset_id` | 文字列 | アセット ID。 |
| `asset_roles` | 配列 | アセットの役割。 [、](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles)、`thumbnail`、`image` など `small_image` サポートされる `swatch_image`Commerce アセットの役割を使用します。 |
| `asset_format` | 文字列 | アセットの形式。 使用可能な値は `image` および `video` です。 |
| `asset_position` | 数値 | 商品ギャラリー内のアセットの位置。 |

## 同期処理をスキップ

`skip` パラメーターを使用すると、カスタムマッチャーで特定のアセットや製品の同期処理をバイパスできます。

App Builder アプリケーションが応答で `"skip": true` を返しても、ルールエンジンは、そのアセットまたは商品の API リクエストの更新または削除をCommerceに送信しません。 この最適化により、不要な API 呼び出しが減り、パフォーマンスが向上します。
