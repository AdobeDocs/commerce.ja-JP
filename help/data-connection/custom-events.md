---
title: カスタムイベントの作成
description: カスタムイベントを作成して、Adobe Commerce データを他のAdobe DX 製品に接続する方法を説明します。
role: Admin, Developer
feature: Personalization, Integration, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# カスタムイベントの作成

独自のストアフロントイベントを作成して業界に固有のデータを収集することで、[ イベントプラットフォーム ](events.md) を拡張できます。 カスタムイベントを作成して設定すると、そのイベントは [Adobe Commerce イベントコレクター ](https://github.com/adobe/commerce-events/tree/main/packages/storefront-events-collector) に送信されます。

## カスタムイベントの処理

カスタムイベントは、Adobe Experience Platformでのみサポートされています。 カスタムデータは、Adobe Commerce ダッシュボードおよび指標トラッカーに転送されません。

`custom` イベントの場合、コレクターは以下を行います。

- `ECID` をプライマリ ID として `identityMap` を追加します
- イベントで設定されているセカンダリ ID _if_`personalEmail.address` として `identityMap` に `email` を含めます
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

>[!NOTE]
>
>カスタムイベントを上書きする場合は、重複カウントを避けるために、そのイベントタイプのExperience Platformへのイベント転送をオフにする必要があります。

例：

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

>[!NOTE]
>
> カスタム属性を使用してイベントを上書きすると、デフォルトのAdobe Analytics レポートに影響する場合があります。
