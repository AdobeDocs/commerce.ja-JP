---
title: 行動イベント
description: 各行動イベントがキャプチャするデータを説明します。
role: Admin, Developer
feature: Personalization, Integration, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '4516'
ht-degree: 0%

---

# [!DNL Data Connection] 行動イベント

以下に、[!DNL Data Connection] 拡張機能のインストール時に使用できるCommerceの行動イベントを示します。 これらのイベントで収集されたデータは、Adobe Experience Platformに送信されます。 また、[ カスタムイベント ](custom-events.md) を作成して、初期設定では提供されていない追加のデータを収集することもできます。

次のイベントで収集されるデータに加えて、Adobe Experience Platform web SDKから提供される [ その他のデータ ](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html) も取得します。

行動イベントは、サイトを閲覧する買い物客から匿名化された行動データを収集します。 これらのイベントで収集されたデータを使用して、特定の買い物客のセットをターゲットとしたプロモーションやキャンペーンを作成できます。

>[!NOTE]
>
>すべての行動イベントには、買い物客のメールアドレス（使用可能な場合）や ECID を含む「[`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html)」フィールドが含まれます。

## ストアフロントイベント

ストアフロントイベントは、サイト上での買い物客のインタラクションからデータをキャプチャし、[`addToCart`](#addtocart)、[`pageView`](#pageview)、[`createAccount`](#createaccount)、[`editAccount`](#editaccount)、[`startCheckout`](#startcheckout)、[`completeCheckout`](#completecheckout)、[`signIn`](#signin)、[`signOut`](#signout) などのイベントを含みます。 ストアフロントイベントは、シンプルで設定可能な製品にのみ適用されます。

### addToCart

| 説明 | XDM イベント名 |
|---|---|
| 商品が買い物かごに追加されたとき、または買い物かご内の商品の数量が増加したときにトリガーされます。 | `commerce.productListAdds` |

#### addToCart から収集したデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `channel` | データのソースに関する情報が含まれます。 `_id` と `_type` の両方に [ 名前空間の値 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html) が含まれています。 |
| `channel._id` | チャネルの一意の識別子（`"https://ns.adobe.com/xdm/channels/web"` など）。 |
| `channel._type` | `"https://ns.adobe.com/xdm/channel-types/web"` などのチャネルデータのソースを識別します。 |
| `commerce.productListAdds` | 商品が買い物かごに追加されたかどうかを示します。 値 `1` は、製品が追加されたことを示します。 |
| `commerce.cart.cartID` | 顧客の買い物かごを識別する一意の ID。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |
| `productListItems` | 買い物かごに追加された製品の配列。 |
| `productListItems.SKU` | 在庫管理単位。 商品の一意の ID。 |
| `productListItems.name` | 商品の表示名または人間が読み取れる名前。 |
| `productListItems.priceTotal` | 商品品目の合計価格。 |
| `productListItems.quantity` | 買い物かごに入っている商品の単位数。 |
| `productListItems.discountAmount` | 適用される割引額を示します。 |
| `productListItems.currencyCode` | `USD` や `EUR` など、使用される [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 通貨コード。 |
| `productListItems.productImageUrl` | 商品のメイン画像 URL。 |
| `productListItems.selectedOptions` | 設定可能な製品に使用されるフィールド。 |
| `productListItems.selectedOptions.attribute` | `size` や `color` など、設定可能な製品の属性を識別します。 |
| `productListItems.selectedOptions.value` | `small` または `black` などの属性の値を識別します。 |

### openCart

| 説明 | XDM イベント名 |
|---|---|
| 新しい買い物かごが作成されたときにトリガーされます。これは、商品が空の買い物かごに追加されたときです。 | `commerce.productListOpens` |

#### openCart から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `channel` | データのソースに関する情報が含まれます。 `_id` と `_type` の両方に [ 名前空間の値 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html) が含まれています。 |
| `channel._id` | チャネルの一意の識別子（`"https://ns.adobe.com/xdm/channels/web"` など）。 |
| `channel._type` | `"https://ns.adobe.com/xdm/channel-types/web"` などのチャネルデータのソースを識別します。 |
| `commerce.productListOpens` | 買い物かごが作成されたかどうかを示します。 値 `1` は、買い物かごが作成されたことを示します。 |
| `commerce.cart.cartID` | 顧客の買い物かごを識別する一意の ID。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |
| `productListItems` | 買い物かごに追加された製品の配列。 |
| `productListItems.SKU` | 在庫管理単位。 商品の一意の ID。 |
| `productListItems.name` | 商品の表示名または人間が読み取れる名前。 |
| `productListItems.priceTotal` | 商品品目の合計価格。 |
| `productListItems.quantity` | 買い物かごに入っている商品の単位数。 |
| `productListItems.discountAmount` | 適用される割引額を示します。 |
| `productListItems.currencyCode` | `USD` や `EUR` など、使用される [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 通貨コード。 |
| `productListItems.productImageUrl` | 商品のメイン画像 URL。 |
| `productListItems.selectedOptions` | 設定可能な製品に使用されるフィールド。 |
| `productListItems.selectedOptions.attribute` | `size` や `color` など、設定可能な製品の属性を識別します。 |
| `productListItems.selectedOptions.value` | `small` または `black` などの属性の値を識別します。 |

### removeFromCart

| 説明 | XDM イベント名 |
|---|---|
| 商品が削除されるたびに、または買い物かご内の商品の数量が減らされるたびにトリガーされます。 | `commerce.productListRemovals` |

#### removeFromCart から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `channel` | データのソースに関する情報が含まれます。 `_id` と `_type` の両方に [ 名前空間の値 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html) が含まれています。 |
| `channel._id` | チャネルの一意の識別子（`"https://ns.adobe.com/xdm/channels/web"` など）。 |
| `channel._type` | `"https://ns.adobe.com/xdm/channel-types/web"` などのチャネルデータのソースを識別します。 |
| `commerce.productListRemovals` | 商品が買い物かごから削除されたかどうかを示します。 値 `1` は、商品が買い物かごから削除されたことを示します。 |
| `commerce.cart.cartID` | 顧客の買い物かごを識別する一意の ID。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |
| `productListItems` | 買い物かごに追加された製品の配列。 |
| `productListItems.SKU` | 在庫管理単位。 商品の一意の ID。 |
| `productListItems.name` | 商品の表示名または人間が読み取れる名前。 |
| `productListItems.priceTotal` | 商品品目の合計価格。 |
| `productListItems.quantity` | 買い物かごに入っている商品の単位数。 |
| `productListItems.discountAmount` | 適用される割引額を示します。 |
| `productListItems.currencyCode` | `USD` や `EUR` など、使用される [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 通貨コード。 |
| `productListItems.productImageUrl` | 商品のメイン画像 URL。 |
| `productListItems.selectedOptions` | 設定可能な製品に使用されるフィールド。 |
| `productListItems.selectedOptions.attribute` | `size` や `color` など、設定可能な製品の属性を識別します。 |
| `productListItems.selectedOptions.value` | `small` または `black` などの属性の値を識別します。 |

### shoppingCartView

| 説明 | XDM イベント名 |
|---|---|
| いずれかの買い物かごページが読み込まれるとトリガーされます。 | `commerce.productListViews` |

#### shoppingCartView から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `channel` | データのソースに関する情報が含まれます。 `_id` と `_type` の両方に [ 名前空間の値 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html) が含まれています。 |
| `channel._id` | チャネルの一意の識別子（`"https://ns.adobe.com/xdm/channels/web"` など）。 |
| `channel._type` | `"https://ns.adobe.com/xdm/channel-types/web"` などのチャネルデータのソースを識別します。 |
| `commerce.productListViews` | 製品リストが表示されたかどうかを示します。 |
| `commerce.cart.cartID` | 顧客の買い物かごを識別する一意の ID。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |
| `commerce.order` | 1 つ以上の商品の保留中の注文に関する情報が含まれます。 |
| `commerce.order.discountAmount` | 注文全体に適用される割引額を示します。 |
| `productListItems` | 買い物かごに追加された製品の配列。 |
| `productListItems.SKU` | 在庫管理単位。 商品の一意の ID。 |
| `productListItems.name` | 商品の表示名または人間が読み取れる名前。 |
| `productListItems.priceTotal` | 商品品目の合計価格。 |
| `productListItems.quantity` | 買い物かごに入っている商品の単位数。 |
| `productListItems.discountAmount` | 適用される割引額を示します。 |
| `productListItems.currencyCode` | `USD` や `EUR` など、使用される [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 通貨コード。 |
| `productListItems.productImageUrl` | 商品のメイン画像 URL。 |
| `productListItems.selectedOptions` | 設定可能な製品に使用されるフィールド。 |
| `productListItems.selectedOptions.attribute` | `size` や `color` など、設定可能な製品の属性を識別します。 |
| `productListItems.selectedOptions.value` | `small` または `black` などの属性の値を識別します。 |

### pageView

| 説明 | XDM イベント名 |
|---|---|
| 任意のページの読み込み時にトリガーされます。 | `web.webpagedetails.pageViews` |

#### pageView から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `channel` | データのソースに関する情報が含まれます。 `_id` と `_type` の両方に [ 名前空間の値 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html) が含まれています。 |
| `channel._id` | チャネルの一意の識別子（`"https://ns.adobe.com/xdm/channels/web"` など）。 |
| `channel._type` | `"https://ns.adobe.com/xdm/channel-types/web"` などのチャネルデータのソースを識別します。 |
| `web.webPageDetails.pageViews` | ページが読み込まれたかどうかを示します。 `1` の `value` は、ページが読み込まれたことを示します。 |
| `web.webPageDetails.URL` | 基準となる、または通常の web ページの URL。 これは、ページに到達するために使用される実際の URL であり、`Web Link` を使用して記録されます。 |
| `web.webPageDetails.name` | Web ページの基準となる名前。 この名前は、必ずしもページのタイトルやページコンテンツに直接関連付けられたものではなく、分類目的でサイトのページを整理するために使用されます。 |
| `web.webReferrer.URL` | サイトへのリンクをクリックする前に買い物客が訪問した Web ページの URL。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |

### productPageView

| 説明 | XDM イベント名 |
|---|---|
| 任意の製品ページの読み込み時にトリガーされます。 | `commerce.productViews` |

#### productPageView から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `channel` | データのソースに関する情報が含まれます。 `_id` と `_type` の両方に [ 名前空間の値 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html) が含まれています。 |
| `channel._id` | チャネルの一意の識別子（`"https://ns.adobe.com/xdm/channels/web"` など）。 |
| `channel._type` | `"https://ns.adobe.com/xdm/channel-types/web"` などのチャネルデータのソースを識別します。 |
| `commerce.productViews` | 製品が表示されたかどうかを示します。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |
| `productListItems` | 買い物かごに追加された製品の配列。 |
| `productListItems.SKU` | 在庫管理単位。 商品の一意の ID。 |
| `productListItems.name` | 商品の表示名または人間が読み取れる名前。 |
| `productListItems.priceTotal` | 商品品目の合計価格。 |
| `productListItems.quantity` | 買い物かごに入っている商品の単位数。 |
| `productListItems.discountAmount` | 適用される割引額を示します。 |
| `productListItems.currencyCode` | `USD` や `EUR` など、使用される [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 通貨コード。 |
| `productListItems.productImageUrl` | 商品のメイン画像 URL。 |
| `productListItems.selectedOptions` | 設定可能な製品に使用されるフィールド。 |
| `productListItems.selectedOptions.attribute` | `size` や `color` など、設定可能な製品の属性を識別します。 |
| `productListItems.selectedOptions.value` | `small` または `black` などの属性の値を識別します。 |

### startCheckout

| 説明 | XDM イベント名 |
|---|---|
| 買い物客がチェックアウトボタンをクリックするとトリガーされます。 | `commerce.checkouts` |

#### startCheckout から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `channel` | データのソースに関する情報が含まれます。 `_id` と `_type` の両方に [ 名前空間の値 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html) が含まれています。 |
| `channel._id` | チャネルの一意の識別子（`"https://ns.adobe.com/xdm/channels/web"` など）。 |
| `channel._type` | `"https://ns.adobe.com/xdm/channel-types/web"` などのチャネルデータのソースを識別します。 |
| `commerce.checkouts` | チェックアウトプロセス中にアクションが発生したかどうかを示します。 |
| `commerce.cart.cartID` | 顧客の買い物かごを識別する一意の ID。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |
| `productListItems` | 買い物かごに追加された製品の配列。 |
| `productListItems.SKU` | 在庫管理単位。 商品の一意の ID。 |
| `productListItems.name` | 商品の表示名または人間が読み取れる名前。 |
| `productListItems.priceTotal` | 商品品目の合計価格。 |
| `productListItems.quantity` | 買い物かごに入っている商品の単位数。 |
| `productListItems.discountAmount` | 適用される割引額を示します。 |
| `productListItems.currencyCode` | `USD` や `EUR` など、使用される [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 通貨コード。 |
| `productListItems.productImageUrl` | 商品のメイン画像 URL。 |
| `productListItems.selectedOptions` | 設定可能な製品に使用されるフィールド。 |
| `productListItems.selectedOptions.attribute` | `size` や `color` など、設定可能な製品の属性を識別します。 |
| `productListItems.selectedOptions.value` | `small` または `black` などの属性の値を識別します。 |

### completeCheckout

| 説明 | XDM イベント名 |
|---|---|
| 買い物客が注文を行ったときにトリガーされます。 | `commerce.purchases` |

#### completeCheckout から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `channel` | データのソースに関する情報が含まれます。 `_id` と `_type` の両方に [ 名前空間の値 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html) が含まれています。 |
| `channel._id` | チャネルの一意の識別子（`"https://ns.adobe.com/xdm/channels/web"` など）。 |
| `channel._type` | `"https://ns.adobe.com/xdm/channel-types/web"` などのチャネルデータのソースを識別します。 |
| `commerce.purchases` | 注文が受理されたかどうかを示します。 |
| `commerce.order` | 1 つ以上の商品に対して行われた注文に関する情報を含みます。 |
| `commerce.order.purchaseID` | この購入または契約の販売者によって割り当てられた一意の ID。 ID が一意であるという保証はありません。 |
| `commerce.order.payments` | この注文の支払いのリスト。 |
| `commerce.order.payments.paymentTransactionID` | この支払トランザクションの一意の ID。 |
| `commerce.order.payments.paymentAmount` | 支払いの値。 |
| `commerce.order.payments.paymentType` | この注文の支払い方法。 オプションは、`cash`、`credit_card`、`debit_card`、`gift_card`、`check`、`paypal`、`wire_transfer`、`credit_card_reference`、`other` です。 |
| `commerce.order.payments.currencyCode` | `USD` や `EUR` など、使用される [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 通貨コード。 |
| `commerce.order.taxAmount` | 最終支払の一部として購入者が支払った税額。 |
| `commerce.order.discountAmount` | 注文全体に適用される割引額を示します。 |
| `commerce.order.createdDate` | コマースシステムで新しい注文が作成された日時。 例：`2022-10-15T20:20:39+00:00`。 |
| `commerce.shipping` | 1 つ以上の商品に関する配送の詳細。 |
| `commerce.shipping.shippingMethod` | お客様が選択した配送方法（通常配送、優先配送、店舗での受け取りなど）。 |
| `commerce.shipping.shippingAmount` | お客様が配送用に支払う必要があった金額。 |  | `shipping` | 1 つ以上の商品に関する配送の詳細。 |
| `commerce.shipping.currencyCode` | `USD` や `EUR` など、使用される [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 通貨コード。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |
| `personalEmail` | 個人の電子メールアドレス。 |
| `personalEmail.address` | 例えば、技術的アドレス `name@domain.com`、RFC2822 および後続の標準で一般的に定義されています。 |
| `productListItems` | 買い物かごに追加された製品の配列。 |
| `productListItems.SKU` | 在庫管理単位。 商品の一意の ID。 |
| `productListItems.name` | 商品の表示名または人間が読み取れる名前。 |
| `productListItems.priceTotal` | 商品品目の合計価格。 |
| `productListItems.quantity` | 買い物かごに入っている商品の単位数。 |
| `productListItems.discountAmount` | 適用される割引額を示します。 |
| `productListItems.productImageUrl` | 商品のメイン画像 URL。 |
| `productListItems.selectedOptions` | 設定可能な製品に使用されるフィールド。 |
| `productListItems.selectedOptions.attribute` | `size` や `color` など、設定可能な製品の属性を識別します。 |
| `productListItems.selectedOptions.value` | `small` または `black` などの属性の値を識別します。 |

## 顧客プロファイルイベント

ストアフロントから取得したプロファイルイベントには、`signIn`、`signOut`、`createAccount`、`editAccount` などのアカウント情報が含まれます。 このデータは、新規登録割引オファーの送信、アカウント変更の確認など、セグメントを適切に定義したり、マーケティングキャンペーンを実行したりするために必要な、主な顧客詳細の入力に使用されます。 [ サーバーサイド ](events-backoffice.md#customer-profile-events) から取り込まれた類似のプロファイルイベントがあります。

### ログイン

| 説明 | XDM イベント名 |
|---|---|
| 買い物客がログインを試みたときにトリガーされます。 | `userAccount.login` |

>[!NOTE]
>
> このイベントは、特定のアクションが試行されたときにトリガーされます。 アクションが成功したことを示すものではありません。

#### サインインから収集したデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `channel` | データのソースに関する情報が含まれます。 `_id` と `_type` の両方に [ 名前空間の値 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html) が含まれています。 |
| `channel._id` | チャネルの一意の識別子（`"https://ns.adobe.com/xdm/channels/web"` など）。 |
| `channel._type` | `"https://ns.adobe.com/xdm/channel-types/web"` などのチャネルデータのソースを識別します。 |
| `person` | 個別のアクター、担当者または所有者。 |
| `person.accountID` | ユーザーアカウント ID をキャプチャします。 |
| `person.accountType` | ユーザーアカウントのタイプをキャプチャします（`Personal`、`Company` など）。該当する場合。 |
| `person.personalEmailID` | 例えば、技術的アドレス `name@domain.com`、RFC2822 および後続の標準で一般的に定義されています。 |
| `personalEmail` | 連絡先の詳細（メールおよび関連情報）を取得します。 |
| `personalEmail.address` | 例えば、技術的アドレス `name@domain.com`、RFC2822 および後続の標準で一般的に定義されています。 |
| `userAccount` | ロイヤルティの詳細、環境設定、ログインプロセス、その他のアカウント環境設定を示します。 |
| `userAccount.login` | 訪問者がログインしようとしたかどうかを示します。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |

### signOut

| 説明 | XDM イベント名 |
|---|---|
| 買い物客がログアウトを試みたときにトリガーされます。 | `userAccount.logout` |

>[!NOTE]
>
> このイベントは、特定のアクションが試行されたときにトリガーされます。 アクションが成功したことを示すものではありません。

#### ログアウトから収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `channel` | データのソースに関する情報が含まれます。 `_id` と `_type` の両方に [ 名前空間の値 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html) が含まれています。 |
| `channel._id` | チャネルの一意の識別子（`"https://ns.adobe.com/xdm/channels/web"` など）。 |
| `channel._type` | `"https://ns.adobe.com/xdm/channel-types/web"` などのチャネルデータのソースを識別します。 |
| `userAccount` | ロイヤルティの詳細、環境設定、ログインプロセス、その他のアカウント環境設定を示します。 |
| `userAccount.logout` | 訪問者がログアウトを試みたかどうかを示します。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |

### createAccount

| 説明 | XDM イベント名 |
|---|---|
| 買い物客がアカウントを作成しようとしたときにトリガーされます。 | `userAccount.createProfile` |

>[!NOTE]
>
> このイベントは、特定のアクションが試行されたときにトリガーされます。 アクションが成功したことを示すものではありません。

#### createAccount から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `channel` | データのソースに関する情報が含まれます。 `_id` と `_type` の両方に [ 名前空間の値 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html) が含まれています。 |
| `channel._id` | チャネルの一意の識別子（`"https://ns.adobe.com/xdm/channels/web"` など）。 |
| `channel._type` | `"https://ns.adobe.com/xdm/channel-types/web"` などのチャネルデータのソースを識別します。 |
| `person` | 個別のアクター、担当者または所有者。 |
| `person.accountID` | ユーザーアカウント ID をキャプチャします。 |
| `person.accountType` | ユーザーアカウントのタイプをキャプチャします（`Personal`、`Company` など）。該当する場合。 |
| `person.personalEmailID` | 例えば、技術的アドレス `name@domain.com`、RFC2822 および後続の標準で一般的に定義されています。 |
| `personalEmail` | 連絡先の詳細（メールおよび関連情報）を取得します。 |
| `personalEmail.address` | 例えば、技術的アドレス `name@domain.com`、RFC2822 および後続の標準で一般的に定義されています。 |
| `userAccount` | ロイヤルティの詳細、環境設定、ログインプロセス、その他のアカウント環境設定を示します。 |
| `userAccount.updateProfile` | ユーザーがアカウントプロファイルを更新したかどうかを示します。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |

### editAccount

| 説明 | XDM イベント名 |
|---|---|
| 買い物客がアカウントを編集しようとしたときにトリガーされます。 | `userAccount.updateProfile` |

>[!NOTE]
>
> このイベントは、特定のアクションが試行されたときにトリガーされます。 アクションが成功したことを示すものではありません。

#### editAccount から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `channel` | データのソースに関する情報が含まれます。 `_id` と `_type` の両方に [ 名前空間の値 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html) が含まれています。 |
| `channel._id` | チャネルの一意の識別子（`"https://ns.adobe.com/xdm/channels/web"` など）。 |
| `channel._type` | `"https://ns.adobe.com/xdm/channel-types/web"` などのチャネルデータのソースを識別します。 |
| `person` | 個別のアクター、担当者または所有者。 |
| `person.accountID` | ユーザーアカウント ID をキャプチャします。 |
| `person.accountType` | ユーザーアカウントのタイプをキャプチャします（`Personal`、`Company` など）。該当する場合。 |
| `person.personalEmailID` | 例えば、技術的アドレス `name@domain.com`、RFC2822 および後続の標準で一般的に定義されています。 |
| `personalEmail` | 連絡先の詳細（メールおよび関連情報）を取得します。 |
| `personalEmail.address` | 例えば、技術的アドレス `name@domain.com`、RFC2822 および後続の標準で一般的に定義されています。 |
| `userAccount` | ロイヤルティの詳細、環境設定、ログインプロセス、その他のアカウント環境設定を示します。 |
| `userAccount.updateProfile` | ユーザーがアカウントプロファイルを更新したかどうかを示します。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |

## イベントを検索

検索イベントは、買い物客の意図に関連するデータを提供します。 買い物客の意図に関するインサイトは、買い物客が商品をどのように検索しているか、何をクリックしているか、最終的に購入または放棄するかをマーチャントが確認するのに役立ちます。 このデータの使用方法の例として、上位の製品を検索しても製品を購入しない既存の買い物客をターゲットにする場合があります。 これらのイベントにアクセスするには、[[!DNL Live Search]](../live-search/install.md) 拡張機能をインストールする必要があります。

`searchRequestSent` イベントと `searchResponseReceived` イベントの両方にある `searchRequest.id` フィールドと `searchResponse.id` フィールドを使用して、検索リクエストを対応する検索応答に相互参照します。

### searchRequestSent

| 説明 | XDM イベント名 |
|---|---|
| <br><br>Enter キーを押し、_すべて表示_<br><br> 検索結果ページの次のイベントがトリガー：<br><br> フィルターの選択、並べ替え順の変更（_並べ替え順_）、並べ替え方向の変更（昇順または降順）、ページあたりの結果数の変更（_ページごとの#表示_）、次のページに移動、前のページに移動、別のページに移動 | `searchRequest` |

>[!NOTE]
>
>B2B 拡張機能がインストールされているAdobe Commerce Enterprise Edition では、検索イベントはサポートされていません。

#### searchRequestSent から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `channel` | データのソースに関する情報が含まれます。 `_id` と `_type` の両方に [ 名前空間の値 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html) が含まれています。 |
| `channel._id` | チャネルの一意の識別子（`"https://ns.adobe.com/xdm/channels/web"` など）。 |
| `channel._type` | `"https://ns.adobe.com/xdm/channel-types/web"` などのチャネルデータのソースを識別します。 |
| `searchRequest` | 検索リクエストが送信されたかどうかを示します。 |
| `searchRequest.id` | この特定の検索リクエストの一意の ID。 |
| `searchRequest.value` | リクエストの定量化可能な値。 |
| `siteSearch` | 検索に関する情報が含まれます。 |
| `siteSearch.filter` | 検索結果を制限するためにフィルターが適用されたかどうかを示します。 |
| `siteSearch.filter.attribute` （フィルター） | 検索結果に含めるかどうかを決定するために使用される項目のファセット。 |
| `siteSearch.filter.isRange` | true の場合、値は、値の許容範囲のエンドポイントを示します。 |
| `siteSearch.filter.value` | 検索結果に含まれる項目を決定するために使用される属性値。 |
| `siteSearch.sort` | 検索結果の並べ替え方法を示します。 |
| `siteSearch.sort.attribute` （並べ替え） | 検索結果で項目を並べ替えるために使用される属性。 |
| `siteSearch.sort.order` | 検索結果を返す順序。 |
| `siteSearch.query` | 検索された語句。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |

### searchResponseReceived

| 説明 | XDM イベント名 |
|---|---|
| Live Search が「入力中に検索」ポップオーバーまたは検索結果ページの結果を返したときにトリガーされます。 | `searchResponse` |

>[!NOTE]
>
>B2B 拡張機能がインストールされているAdobe Commerce Enterprise Edition では、検索イベントはサポートされていません。

#### searchResponseReceived から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `channel` | データのソースに関する情報が含まれます。 `_id` と `_type` の両方に [ 名前空間の値 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html) が含まれています。 |
| `channel._id` | チャネルの一意の識別子（`"https://ns.adobe.com/xdm/channels/web"` など）。 |
| `channel._type` | `"https://ns.adobe.com/xdm/channel-types/web"` などのチャネルデータのソースを識別します。 |
| `searchResponse` | 検索応答が受信されたかどうかを示します。 |
| `searchResponse.id` | この特定の検索応答の一意の ID。 |
| `searchResponse.value` | 応答の定量化可能な値。 |
| `siteSearch.numberOfResults` | 返される製品の数。 |
| `siteSearch.suggestions` | 検索クエリに類似したカタログにある製品およびカテゴリの名前を含む文字列の配列。 |
| `productListItems` | 買い物かごに追加された製品の配列。 |
| `productListItems.SKU` | 在庫管理単位。 商品の一意の ID。 |
| `productListItems.name` | 商品の表示名または人間が読み取れる名前。 |
| `productListItems.productImageUrl` | 商品のメイン画像 URL。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |

## B2B イベント

Adobe Commerceの ![B2B](../assets/b2b.svg) B2B マーチャントの場合、これらのイベントにアクセスするには、`experience-platform-connector-b2b` 拡張機能を [ インストール ](install.md#install-the-b2b-extension) する必要があります。

B2B イベントには、購買依頼リストが作成、追加または削除されたかどうかなど、[ 購買依頼リスト ](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html) 情報が含まれます。 購買依頼リストに固有のイベントを追跡することで、顧客が頻繁に購入する製品を確認し、そのデータに基づいてキャンペーンを作成できます。

### createRequisitionList

| 説明 | XDM イベント名 |
|---|---|
| 買い物客が購買依頼リストを作成するとトリガーされます。 | `commerce.requisitionListOpens` |

#### createRequisitionList から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `channel` | データのソースに関する情報が含まれます。 `_id` と `_type` の両方に [ 名前空間の値 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html) が含まれています。 |
| `channel._id` | チャネルの一意の識別子（`"https://ns.adobe.com/xdm/channels/web"` など）。 |
| `channel._type` | `"https://ns.adobe.com/xdm/channel-types/web"` などのチャネルデータのソースを識別します。 |
| `commerce.requisitionListOpens` | 新規購買依頼リストの初期化を示します。 |
| `commerce.requisitionList` | 顧客によって作成された要求リストのプロパティ。 |
| `commerce.requisitionList.ID` | 購買依頼リストの一意の ID です。 |
| `commerce.requisitionList.name` | 顧客によって指定された要求リストの名前。 |
| `commerce.requisitionList.description` | 顧客によって指定された要求リストの説明。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |

### addToRequisitionList

| 説明 | XDM イベント名 |
|---|---|
| 買い物客が既存の購買依頼リストに製品を追加するとき、またはリストの作成中にトリガーされます。 | `commerce.requisitionListAdds` |

#### addToRequisitionList から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `channel` | データのソースに関する情報が含まれます。 `_id` と `_type` の両方に [ 名前空間の値 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html) が含まれています。 |
| `channel._id` | チャネルの一意の識別子（`"https://ns.adobe.com/xdm/channels/web"` など）。 |
| `channel._type` | `"https://ns.adobe.com/xdm/channel-types/web"` などのチャネルデータのソースを識別します。 |
| `commerce.requisitionListAdds` | 1 つ以上の製品を購買依頼リストに追加することを示します。 |
| `commerce.requisitionList` | 顧客によって作成された要求リストのプロパティ。 |
| `commerce.requisitionList.ID` | 購買依頼リストの一意の ID です。 |
| `commerce.requisitionList.name` | 顧客によって指定された要求リストの名前。 |
| `commerce.requisitionList.description` | 顧客によって指定された要求リストの説明。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |
| `productListItems` | 購買依頼リストに追加された製品の配列。 |
| `productListItems.SKU` | 在庫管理単位。 商品の一意の ID。 |
| `productListItems.name` | 商品の表示名または人間が読み取れる名前。 |
| `productListItems.priceTotal` | 商品品目の合計価格。 |
| `productListItems.quantity` | 買い物かごに入っている商品の単位数。 |
| `productListItems.discountAmount` | 適用される割引額を示します。 |
| `productListItems.currencyCode` | `USD` や `EUR` など、使用される [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 通貨コード。 |
| `productListItems.selectedOptions` | 設定可能な製品に使用されるフィールド。 |
| `productListItems.selectedOptions.attribute` | `size` や `color` など、設定可能な製品の属性を識別します。 |
| `productListItems.selectedOptions.value` | `small` または `black` などの属性の値を識別します。 |

### removeFromRequisitionList

| 説明 | XDM イベント名 |
|---|---|
| 買い物客が購入リストから商品を削除するとトリガーされます。 | `commerce.requisitionListRemovals` |

#### removeFromRequisitionList から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `channel` | データのソースに関する情報が含まれます。 `_id` と `_type` の両方に [ 名前空間の値 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html) が含まれています。 |
| `channel._id` | チャネルの一意の識別子（`"https://ns.adobe.com/xdm/channels/web"` など）。 |
| `channel._type` | `"https://ns.adobe.com/xdm/channel-types/web"` などのチャネルデータのソースを識別します。 |
| `commerce.requsitionListRemovals` | 購買依頼リストから 1 つ以上の製品の削除を示します。 |
| `commerce.requisitionList` | 顧客によって作成された要求リストのプロパティ。 |
| `commerce.requisitionList.ID` | 購買依頼リストの一意の ID です。 |
| `commerce.requisitionList.name` | 顧客によって指定された要求リストの名前。 |
| `commerce.requisitionList.description` | 顧客によって指定された要求リストの説明。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |
| `productListItems` | 購買依頼リストに追加された製品の配列。 |
| `productListItems.SKU` | 在庫管理単位。 商品の一意の ID。 |
| `productListItems.name` | 商品の表示名または人間が読み取れる名前。 |
| `productListItems.priceTotal` | 商品品目の合計価格。 |
| `productListItems.quantity` | 買い物かごに入っている商品の単位数。 |
| `productListItems.discountAmount` | 適用される割引額を示します。 |
| `productListItems.currencyCode` | `USD` や `EUR` など、使用される [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 通貨コード。 |
| `productListItems.selectedOptions` | 設定可能な製品に使用されるフィールド。 |
| `productListItems.selectedOptions.attribute` | `size` や `color` など、設定可能な製品の属性を識別します。 |
| `productListItems.selectedOptions.value` | `small` または `black` などの属性の値を識別します。 |

### deleteRequisitionList

| 説明 | XDM イベント名 |
|---|---|
| 買い物客が購入リストを削除するとトリガーされます。 | `commerce.requisitionListDeletes` |

#### deleteRequisitionList から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `channel` | データのソースに関する情報が含まれます。 `_id` と `_type` の両方に [ 名前空間の値 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html) が含まれています。 |
| `channel._id` | チャネルの一意の識別子（`"https://ns.adobe.com/xdm/channels/web"` など）。 |
| `channel._type` | `"https://ns.adobe.com/xdm/channel-types/web"` などのチャネルデータのソースを識別します。 |
| `commerce.requisitionListDeletes` | 購買依頼リストが削除されたことを示します。 |
| `commerce.requisitionList` | 顧客によって作成された要求リストのプロパティ。 |
| `commerce.requisitionList.ID` | 購買依頼リストの一意の ID です。 |
| `commerce.requisitionList.name` | 顧客によって指定された要求リストの名前。 |
| `commerce.requisitionList.description` | 顧客によって指定された要求リストの説明。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |
