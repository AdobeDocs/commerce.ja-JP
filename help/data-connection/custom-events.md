---
title: カスタムイベントの作成
description: カスタムイベントを作成して、Adobe Commerce データを他のAdobe DX 製品に接続する方法を説明します。
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: db782c0a-8f13-4076-9b17-4c5bf98e9d01
source-git-commit: 25d796da49406216f26d12e3b1be01902dfe9302
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# カスタムイベントの作成

独自のストアフロントイベントを作成して業界に固有のデータを収集することで、[ イベントプラットフォーム ](events.md) を拡張できます。 カスタムイベントを作成して設定すると、そのイベントは [Adobe Commerce イベントコレクター ](https://github.com/adobe/commerce-events/tree/main/packages/storefront-events-collector) に送信されます。

## カスタムイベントの処理

カスタムイベントは、Adobe Experience Platformでのみサポートされています。 カスタムデータは、Adobe Commerce ダッシュボードおよび指標トラッカーに転送されません。

`custom` イベントの場合、コレクターは以下を行います。

- `identityMap` をプライマリ ID として `ECID` を追加します
- イベントで設定されているセカンダリ ID`email`if`identityMap`_として_ に `personalEmail.address` を含めます
- Edgeに転送する前に、`xdm` オブジェクト内でイベント全体をラップします

例：

Adobe Commerce イベント SDKを通じて公開されたカスタムイベント：

```javascript
mse.publish.custom({
    commerce: {
        saveForLaters: {
            value: 1,
        },
    },
});
```

Experience Platform Edgeで：

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
> カスタムイベントを使用すると、デフォルトのAdobe Analytics レポートに影響する可能性があります。

## イベントの上書きの処理（カスタム属性）

`customContext` を含むイベントセットの場合、コレクターが `custom context` のフィールドからイベントペイロードのフィールドを上書きまたは拡張します。 オーバーライドのユースケースは、開発者が、既にサポートされているイベントでページの他の部分が設定したコンテキストを再利用および拡張する場合です。

イベントの上書きは、Experience Platformへの転送時にのみ適用されます。 これらは、Adobe CommerceおよびSensei analytics イベントには適用されません。 Adobe Commerce イベントコレクター [README](https://github.com/adobe/commerce-events/blob/e34bcfc0deca8d5ac1f9310fc1ee4c1becf4ffbb/packages/storefront-events-collector/README.md) には、追加情報が記載されています。

>[!NOTE]
>
>Experience Platform イベントペイロードでカスタム属性を使用して `productListItems` を拡張する場合は、SKU を使用して商品を照合します。 この要件は、`product-page-view` のイベントには適用されません。

### 使用状況

```javascript
const mse = window.magentoStorefrontEvents;

mse.publish.productPageView(customCtx);
```

### 例 1 - `productCategories` の追加

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

### 例 2 - イベントを公開する前にカスタムコンテキストを追加

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

### 例 3 - パブリッシャーで設定されたカスタムコンテキストが、Adobe Client Data Layer で以前に設定されたカスタムコンテキストを上書きします

この例では、`pageView` イベントの **フィールドに** カスタムページ名 2`web.webPageDetails.name` が表示されます。

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

### 例 4 – 複数の製品を持つイベントの `productListItems` にカスタムコンテキストを追加

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

>[!NOTE]
>
> カスタム属性を使用してイベントを上書きすると、デフォルトのAdobe Analytics レポートに影響する場合があります。
