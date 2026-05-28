---
title: カスタムイベントの作成
description: カスタムイベントを作成して、Adobe Commerce データを他のAdobe DX製品に接続する方法を説明します。
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: db782c0a-8f13-4076-9b17-4c5bf98e9d01
TQID: https://experienceleague.adobe.com/D1fAIJRYegeZakCdJLB6F1HME4rUQaeoUjMFNgmqpzs
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 371
ht-degree: 0%

---

# カスタムイベントの作成

独自のストアフロントイベントを作成して、業界固有のデータを収集することで、[&#x200B; イベントプラットフォーム &#x200B;](events.md)を拡張できます。 カスタムイベントを作成して設定すると、[Adobe Commerce Events Collector](https://github.com/adobe/commerce-events/tree/main/packages/storefront-events-collector)に送信されます。

## カスタムイベントの処理

カスタムイベントは、Adobe Experience Platformでのみサポートされています。 カスタムデータは、Adobe Commerce ダッシュボードや指標トラッカーには転送されません。

任意の`custom` イベントの場合、コレクター：

- `identityMap`を`ECID`のプライマリ IDとして追加します
- `email`がセカンダリ ID _として`identityMap`に含まれます（_ `personalEmail.address`がイベントで設定されている場合）
- Edgeに転送する前に、`xdm` オブジェクト内でイベント全体をラップします

例：

Adobe Commerce Events SDKを通じて公開されたカスタムイベント：

```javascript
mse.publish.custom({
    commerce: {
        saveForLaters: {
            value: 1,
        },
    },
});
```

Experience Platform Edgeでは、

```javascript
{
  xdm: {
    identityMap: {
      ECID: [
        {
          id: 'ecid1234',
          primary: true
        }
      ],
      email: [
        {
          id: "runs@safari.ke",
          primary: false
        }
      ]
    },
    commerce: {
        saveForLaters: {
            value: 1
        }
    }
  }
}
```

>[!NOTE]
>
> カスタムイベントを使用すると、デフォルトのAdobe Analytics レポートに影響する場合があります。

## イベントの上書き（カスタム属性）の処理

`customContext`を持つ任意のイベントセットの場合、コレクターは、イベントペイロードのフィールドを`custom context`のフィールドから上書きまたは拡張します。 オーバーライドのユースケースは、開発者が既にサポートされているイベントでページの他の部分によって設定されたコンテキストを再利用および拡張したい場合です。

イベントの上書きは、Experience Platformに転送する場合にのみ適用されます。 Adobe CommerceおよびSensei Analytics イベントには適用されません。 Adobe Commerce Events Collector [README](https://github.com/adobe/commerce-events/blob/e34bcfc0deca8d5ac1f9310fc1ee4c1becf4ffbb/packages/storefront-events-collector/README.md)は、追加情報を提供します。

>[!NOTE]
>
>Experience Platform イベントペイロードのカスタム属性で`productListItems`を強化する場合は、SKUを使用して商品を一致させます。 この要件は、`product-page-view` イベントには適用されません。

### 使用状況

```javascript
const mse = window.magentoStorefrontEvents;

mse.publish.productPageView(customCtx);
```

### 例1

次の使用例は、イベントの公開時にカスタム コンテキストを追加します。

```javascript
magentoStorefrontEvents.publish.productPageView({
    productListItems: [
        {
            productCategories: [
                {
                    categoryID: "cat_15",
                    categoryName: "summer pants",
                    categoryPath: "pants/mens/summer",
                },
            ],
        },
    ],
});
```

### 例2

次の使用例は、イベントを公開する前にカスタム コンテキストを追加します。

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  productListItems: [
    {
      productCategories: [
        {
          categoryID: "cat_15",
          categoryName: "summer pants",
          categoryPath: "pants/mens/summer",
        },
      ],
    },
  ],
});

mse.publish.productPageView();
```

### 例3

次の使用例は、パブリッシャーでカスタムコンテキストを設定し、以前にAdobe Client Data Layerで設定したカスタムコンテキストを上書きします。

この例では、`pageView` イベントには、`web.webPageDetails.name` フィールドに&#x200B;**カスタムページ名2**&#x200B;が含まれます。

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  web: {
    webPageDetails: {
      name: 'Custom Page Name 1'
    },
  },
});

mse.publish.pageView({
  web: {
    webPageDetails: {
      name: 'Custom Page Name 2'
    },
  },
});
```

### 例4

次の使用例は、複数の製品を含む`productListItems`件のイベントにカスタム コンテキストを追加します。

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  productListItems: [
    {
      SKU: "24-WB01", //Match SKU to override correct product in event payload
      productCategory: "Hand Bag", //Custom attribute added to event payload
      name: "Strive Handbag (CustomName)" //Override existing attribute with custom value in event payload
    },
    {
      SKU: "24-MB04",
      productCategory: "Backpack Bag",
      name: "Strive Backpack (CustomName)"
    },
  ],
});

mse.publish.shoppingCartView();
```

Luma ベースのストア：

Luma ベースのストアは公開イベントをネイティブに実装するので、`customContext`を拡張してカスタムデータを設定できます。

例：

```javascript
mse.context.setCustom({
  web: {
    webPageDetails: {
      name: 'Custom Page Name'
    },
  },
});
```

>[!NOTE]
>
> カスタム属性を使用してイベントを上書きすると、デフォルトのAdobe Analytics レポートに影響する場合があります。
