---
title: カスタムイベントの作成
description: カスタムイベントを作成して、Adobe Commerce データを他のAdobe DX 製品に接続する方法を説明します。
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: db782c0a-8f13-4076-9b17-4c5bf98e9d01
source-git-commit: 81fbcde11da6f5d086c2b94daeffeec60a9fdbcc
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 1%

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

標準イベントの属性のオーバーライドは、Experience Platformでのみサポートされています。 カスタムデータは、Commerce ダッシュボードおよび指標トラッカーに転送されません。

`customContext` を含むイベントの場合、コレクターは、関連するコンテキストで設定されたフィールドを `customContext` のフィールドでオーバーライドします。 オーバーライドのユースケースは、開発者が、既にサポートされているイベントでページの他の部分が設定したコンテキストを再利用および拡張する場合です。

### 例

Adobe Commerce Events SDKを通じて公開された、上書きを含む製品ビュー：

```javascript
mse.publish.productPageView({
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

Experience Platform Edgeで：

```javascript
{
  xdm: {
    eventType: 'commerce.productViews',
    identityMap: {
      ECID: [
        {
          id: 'ecid1234',
          primary: true,
        }
      ]
    },
    commerce: {
      productViews: {
        value : 1,
      }
    },
    productListItems: [{
        SKU: "1234",
        name: "leora summer pants",
        productCategories: [{
            categoryID: "cat_15",
            categoryName: "summer pants",
            categoryPath: "pants/mens/summer",
        }],
    }],
  }
}
```

Luma ベースのストア：

Luma ベースのストアでは、公開イベントがネイティブに実装されています。 したがって、`customContext` を拡張してカスタムデータを設定できます。

例：

```javascript
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
```

カスタムデータの処理について詳しくは、[ カスタムイベントの上書き ](https://github.com/adobe/commerce-events/blob/main/examples/events/custom-event-override.md) を参照してください。

>[!NOTE]
>
> カスタム属性を使用してイベントを上書きすると、デフォルトのAdobe Analytics レポートに影響する場合があります。
