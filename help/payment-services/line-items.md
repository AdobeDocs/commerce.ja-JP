---
title: 行項目  [!DNL Payment Services]
description: の行項目と  [!DNL Payment Services]  マーチャントダッシュボードで行項目を表示する方法について説明します。
feature: Payments, Paas, Saas
role: User
exl-id: f690ff94-f83d-4525-9d52-1dea25a71060
source-git-commit: 6727102c54e0ac81df289ecd66ec61156662b8b9
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# [!DNL Payment Services] の行項目

[!DNL Payment Services] の品目は、受注に含まれる品目です。 これらのライン・アイテムは、次のような情報を提供します。

* 製品の詳細
* 数量
* 価格（税、割引、その他の関連情報を含む）

この情報は、カスタマーサービス、注文管理、適切な請求に役立ちます。

## 行項目を設定

[!DNL Payment Services] の場合、行項目はデフォルトで有効になっています。 次の手順で設定します。

1. _管理者_ サイドバーで、**[!UICONTROL Stores]**/_[!UICONTROL Settings]_/**[!UICONTROL Configuration]**に移動します。

1. **[!UICONTROL Sales]** に移動し、「**[!UICONTROL Payment Methods]**」を選択します。

1. 「_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_」セクションを展開します。

1. 「_[!UICONTROL Payment Services]_」セクションで、「_[!UICONTROL Line Items]_」セクションを展開します。

1. **[!UICONTROL Line Items Enabled]** の場合は、「`Yes`」を選択して有効（デフォルト）にするか、「`No`」を選択して明細項目を無効にします。

1. 「**[!UICONTROL Save Config]**」をクリックして変更を保存します。

>[!IMPORTANT]
>
> 注文にカスタム料金（手数料の処理など）を追加するサードパーティ拡張機能がある場合は、行項目を無効にする必要がある場合があります。 [!DNL Payment Services] では、標準のCommerce注文コンポーネント（品目、税、配送、割引）に基づいて明細行品目が計算されます。 [!DNL Payment Services] で認識されないサードパーティの手数料は、明細項目の合計と注文の合計の間で不一致が発生する可能性があり、チェックアウトが完了しない可能性があります。

## 行項目の表示

明細品目を表示する手順は、次のとおりです。

1. [PayPal マーチャントダッシュボード ](https://www.paypal.com/merchant/){target=_blank} に移動します。

1. **アクティビティ**/**すべてのトランザクション** をクリックします。

1. 目的の受注を選択し、その明細品目を表示します。

   > 買い物客ダッシュボードビューの行項目の例

   ![ ライン項目ビュー ](assets/paypal-shopper-dashboard-line-items-view.png){width="500" zoomable="yes"}

## ライン項目属性

品目は、注文がAdobe Commerceを通じて行われ、情報が PayPal に送信されると生成され、次の属性を持ちます。

| 属性 | データタイプ | 説明 |
| --- | --- | --- |
| `name` | ストリング！ | 項目名。 複数の数量または税金の端数処理の問題が原因で品目に複数の明細がある場合、品目名はすべての明細で同じですが、端数処理が原因で表示される価格が若干異なる場合があります。 |
| `unit_amount` | オブジェクト！ | 品目の単価または単価。 `currency_code` 属性と `value` 属性が含まれます。 |
| `tax` | オブジェクト | 各単位の品目税。 `currency_code` 属性と `value` 属性が含まれます。 |
| `quantity` | ストリング！ | 品目の数量。 は整数になります。 |
| `description` | 文字列 | 詳細な品目の説明。 |
| `sku` | 文字列 | 商品の最小在庫管理単位（SKU）。 |
| `url` | 文字列 | 購入される品目の `URL`。 バイヤーに表示され、バイヤーのエクスペリエンスで使用されます。 |
| `upc` | オブジェクト | 項目のユニバーサル製品コード（または UPC）。 |
| `category` | 文字列 | 品目カテゴリ タイプ。 |

### `unit_amount` 属性

`unit_amount` オブジェクトには、次の属性が含まれます。

| 属性 | データタイプ | 説明 |
| --- | --- | --- |
| `currency_code` | ストリング！ | 通貨を識別する [3 文字の ISO-4217 通貨コード ](https://developer.paypal.com/api/rest/reference/currency-codes/)。 |
| `value` | ストリング！ | 項目の値を示します。 `currency_code` は、必要な小数点以下の桁数を決定します（存在する場合）。 |

### `tax` 属性

`tax` オブジェクトには、次の属性が含まれます。

| 属性 | データタイプ | 説明 |
| --- | --- | --- |
| `currency_code` | ストリング！ | 通貨を識別する [3 文字の ISO-4217 通貨コード ](https://developer.paypal.com/api/rest/reference/currency-codes/)。 |
| `value` | ストリング！ | 項目の値を示します。 必要な小数点以下の桁数について各 `currency_code` に依存します。 |

### `upc` 属性

`upc` オブジェクトには、次の属性が含まれます。

| 属性 | データタイプ | 説明 |
| --- | --- | --- |
| `type` | ストリング！ | UPC のタイプ。 |
| `code` | ストリング！ | 品目の UPC 製品コード。 |

+++ライン項目の例

```json
{
    "name": "Crown Summit Backpack - 1",
    "unit_amount": {
        "currency_code": "USD",
        "value": "38.50"
    },
    "tax": {
        "currency_code": "USD"
        "value": "3.13"
    },
    "quantity": "1",
    "description": "The Crown Summit Backpack is equally at home in a gym locker, study cube or a pup tent, so be sure yours is packed with books,",
    "sku": "24-MB03",
    "url": "https://magento.test/crown-summit-backpack.html",
    "upc": {
        "type": "UPC-A",
        "code": "000003"
    },
    "category": "PHYSICAL_GOODS"
},
{
    "name": "Crown Summit Backpack - 2",
    "unit_amount": {
        "currency_code": "USD",
        "value": "38.50"
    },
    "tax": {
        "currency_code": "USD",
        "value": "3.14"
    },
    "quantity": "1",
    "description": "The Crown Summit Backpack is equally at home in a gym locker, study cube or a pup tent, so be sure yours is packed with books,",
    "sku": "24-MB03",
    "url": "https://magento.test/crown-summit-backpack.html",
    "upc": {
        "type": "UPC-A",
        "code": "000003"
    },
    "category": "PHYSICAL_GOODS"
}
```

+++

これらのフィールドとその制限事項について詳しくは、[ 行項目に関する PayPal 開発者向けドキュメント ](https://developer.paypal.com/docs/api/orders/v2/#definition-line_item){target=_blank} を参照してください。

## 行項目の管理

Adobe Commerce[ 各行の合計金額に基づいて税金を計算します ](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/taxes/taxes#warning-messages){target=_blank}。同じ品目の複数の数量が注文されている場合や、カタログに税込みの価格が表示されている場合は、丸めの問題が発生する可能性があります。 この場合、合計数量は 2 つの明細に分割できますが、数量は受注品目の合計と等しくなります。

> 販売者ダッシュボード ビューでの丸め問題を含む品目の例

![ ライン項目ビュー ](assets/line-items-example.png){width="600" zoomable="yes"}

+++Adobe Commerceによる行項目の丸め問題の計算方法

[!DNL Payment Services] の品目では、`unit_amount` または `unit_tax` の値が注文の合計金額に対応するように、この丸め問題の残高を計算します。 この端数処理の問題を解決するために、品目を 2 つの明細に分割できます。

* 丸め問題が `unit_amount` に表示されると、マーチャントはこの追加行の価格に違いを表示する必要があります。
* 丸め問題が `unit_tax` に表示される場合、`tax` はグリッドには表示されず、下部には合計としてのみ表示されるので、個々の行項目に違いは表示されません。

+++
