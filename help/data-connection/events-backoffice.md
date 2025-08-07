---
title: バックオフィスイベント
description: バックオフィスイベントがそれぞれキャプチャするデータを説明します。
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: 65cf8150-1a14-4d4c-aa0c-1545109e4fe7
source-git-commit: 1750aee715946d3a871e021cbbee687f54d1ff09
workflow-type: tm+mt
source-wordcount: '3618'
ht-degree: 0%

---

# バックオフィスイベントの [!DNL Data Connection] スト

[!DNL Data Connection] 拡張機能のインストール時に使用できるCommerce バックオフィスイベントの一覧を次に示します。 これらのイベントで収集されたデータは、Adobe Experience Platformに送信されます。 また、[ カスタムイベント ](custom-events.md) を作成して、初期設定では提供されていない追加のデータを収集することもできます。

次のイベントで収集されるデータに加えて、Adobe Experience Platform web SDKから提供される [ その他のデータ ](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html) も取得します。

バックオフィスイベントには、サーバーサイドのデータが含まれます。 このデータは、注文が行われた、キャンセルされた、払い戻された、出荷された、完了したなどの [ 注文ステータス ](#order-status) 情報を含みます。 サーバーサイドのデータには、アカウントが作成、更新、削除されたかどうかなど、[ 顧客プロファイルイベント ](#customer-profile-events) 情報も含まれます。

>[!NOTE]
>
>すべてのバックオフィスイベントには、買い物客のメールアドレス（使用可能な場合）、ECID を含む「[`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html)」フィールドが含まれます。

## 注文ステータス

注文ステータスデータには、買い物客の注文の 360 ビューが表示されます。 この表示により、マーケティングキャンペーンを開発する際に、マーチャントは注文ステータス全体をより適切にターゲット設定または分析できます。 例えば、特定の製品カテゴリのトレンドを見つけ、1 年の様々な時期に好成績を上げることができます。 例えば、寒い時期によく売れる冬服や、買い物客が長年にわたって興味を持っている特定の商品カラーなどです。 さらに、注文ステータスデータを使用すると、以前の注文に基づいてコンバージョンする買い物客の傾向を把握することで、生涯顧客価値を計算できます。

### orderPlaced

| 説明 | XDM イベント名 |
|---|---|
| 買い物客が注文を行ったときにトリガーされます。 | `commerce.backofficeOrderPlaced` |

#### orderPlaced から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `commerce.order` | 注文に関する情報が含まれます。 |
| `commerce.order.purchaseID` | この購入または契約の販売者によって割り当てられた一意の ID。 ID が一意であるという保証はありません。 |
| `commerce.order.payments` | この注文の支払いのリスト。 |
| `commerce.order.payments.paymentTransactionID` | この支払トランザクションの一意の ID。 |
| `commerce.order.payments.paymentAmount` | 支払いの値。 |
| `commerce.order.payments.paymentType` | この注文の支払い方法。 カウントされ、カスタム値が許可されます。 |
| `commerce.order.payments.currencyCode` | [ や ](https://en.wikipedia.org/wiki/ISO_4217) など、使用される `USD`ISO 4217`EUR` 通貨コード。 |
| `commerce.order.taxAmount` | 最終支払の一部として購入者が支払った税額。 |
| `commerce.order.discountAmount` | 注文全体に適用される割引額を示します。 |
| `commerce.order.createdDate` | コマースシステムで新しい注文が作成された日時。 例：`2022-10-15T20:20:39+00:00`。 |
| `commerce.order.currencyCode` | 注文合計に使用される ISO 4217 通貨コード。 |
| `commerce.shipping` | 1 つ以上の商品に関する配送の詳細。 |
| `commerce.shipping.shippingMethod` | お客様が選択した配送方法（通常配送、優先配送、店舗での受け取りなど）。 |
| `commerce.shipping.shippingAmount` | お客様が配送用に支払う必要があった金額。 |
| `commerce.shipping.currencyCode` | 配送合計に使用される ISO 4217 通貨コード。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |
| `commerce.billing.address` | 請求先住所。 |
| `commerce.billing.address.street1` | プライマリの番地レベルの情報、アパート番号、通り番号、通り名 |
| `commerce.billing.address.street2` | 番地レベルの情報の追加フィールド。 |
| `commerce.billing.address.city` | 市区町村の名前。 |
| `commerce.billing.address.state` | 州の名前。 これは自由形式フィールドです。 |
| `commerce.billing.address.postalCode` | 場所の郵便番号。 郵便番号は、すべての国で利用できるわけではありません。 一部の国では、郵便番号の一部のみが含まれます。 |
| `commerce.billing.address.country` | 政府が管理する領土の名前。 `xdm:countryCode` 以外の場合、これは自由形式のフィールドで、どの言語でも国名を持つことができます。 |
| `personalEmail` | 個人の電子メールアドレス。 |
| `personalEmail.address` | 例えば、技術的アドレス `name@domain.com`、RFC2822 および後続の標準で一般的に定義されています。 |
| `productListItems` | 順序の商品の配列。 |
| `productListItems.id` | この商品エントリの品目識別子。 |
| `productListItems.SKU` | 在庫管理単位。 商品の一意の ID。 |
| `productListItems.name` | 商品の表示名または人間が読み取れる名前。 |
| `productListItems.priceTotal` | 商品品目の合計価格。 |
| `productListItems.quantity` | 買い物かごに入っている商品の単位数。 |
| `productListItems.discountAmount` | 適用される割引額を示します。 |
| `productListItems.currencyCode` | [ や ](https://en.wikipedia.org/wiki/ISO_4217) など、使用される `USD`ISO 4217`EUR` 通貨コード。 |
| `productListItems.selectedOptions` | 設定可能な製品に使用されるフィールド。 |
| `productListItems.selectedOptions.attribute` | `size` や `color` など、設定可能な製品の属性を識別します。 |
| `productListItems.selectedOptions.value` | `small` または `black` などの属性の値を識別します。 |
| `productListItems.categories` | 商品のカテゴリに関する情報が含まれます。 |
| `productListItems.categories.id` | カテゴリの一意の ID。 |
| `productListItems.categories.name` | カテゴリの名前。 |
| `productListItems.categories.path` | カテゴリへのパス。 |
| `productListItems.productImageUrl` | 商品のメイン画像 URL。 |

### orderInvoiced

| 説明 | XDM イベント名 |
|---|---|
| 商人が支払を要求する請求書を送信したときにトリガーされます。 | `commerce.backofficeOrderInvoiced` |

#### orderInvoiced から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `commerce.order` | 注文に関する情報が含まれます。 |
| `commerce.order.purchaseID` | この購入または契約の販売者によって割り当てられた一意の ID。 ID が一意であるという保証はありません。 |
| `commerce.order.priceTotal` | すべての割引および税金が適用された後のこの注文の合計金額。 |
| `commerce.order.currencyCode` | 注文合計に使用される ISO 4217 通貨コード。 |
| `commerce.order.purchaseOrderNumber` | この購入または契約の購入者によって割り当てられた一意の ID。 |
| `commerce.order.payments` | この注文の支払いのリスト。 |
| `commerce.order.payments.currencyCode` | [ や ](https://en.wikipedia.org/wiki/ISO_4217) など、使用される `USD`ISO 4217`EUR` 通貨コード。 |
| `commerce.order.payments.paymentType` | この注文の支払い方法。 カウントされ、カスタム値が許可されます。 |
| `commerce.order.payments.paymentAmount` | 支払いの値。 |
| `commerce.shipping` | 1 つ以上の商品に関する配送の詳細。 |
| `commerce.shipping.shippingMethod` | お客様が選択した配送方法（通常配送、優先配送、店舗での受け取りなど）。 |
| `commerce.shipping.shippingAmount` | お客様が配送用に支払う必要があった金額。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |
| `personalEmail` | 個人の電子メールアドレス。 |
| `personalEmail.address` | 例えば、技術的アドレス `name@domain.com`、RFC2822 および後続の標準で一般的に定義されています。 |
| `productListItems` | 順序の商品の配列。 |
| `productListItems.id` | この商品エントリの品目識別子。 |
| `productListItems.SKU` | 在庫管理単位。 商品の一意の ID。 |
| `productListItems.name` | 商品の表示名または人間が読み取れる名前。 |
| `productListItems.priceTotal` | 商品品目の合計価格。 |
| `productListItems.quantity` | 買い物かごに入っている商品の単位数。 |
| `productListItems.discountAmount` | 適用される割引額を示します。 |
| `productListItems.categories` | 商品のカテゴリに関する情報が含まれます。 |
| `productListItems.categories.id` | カテゴリの一意の ID。 |
| `productListItems.categories.name` | カテゴリの名前。 |
| `productListItems.categories.path` | カテゴリへのパス。 |

### orderItemsShipped

| 説明 | XDM イベント名 |
|---|---|
| 注文が出荷されたときにトリガーされます。 | `commerce.backofficeOrderItemsShipped` |

#### orderItemsShipped から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `commerce.order` | 注文に関する情報が含まれます。 |
| `commerce.order.purchaseID` | この購入または契約の販売者によって割り当てられた一意の ID。 ID が一意であるという保証はありません。 |
| `commerce.order.payments` | この注文の支払いのリスト。 |
| `commerce.order.payments.paymentTransactionID` | この支払トランザクションの一意の ID。 |
| `commerce.order.payments.paymentAmount` | 支払いの値。 |
| `commerce.order.payments.paymentType` | この注文の支払い方法。 カウントされ、カスタム値が許可されます。 |
| `commerce.order.payments.currencyCode` | [ や ](https://en.wikipedia.org/wiki/ISO_4217) など、使用される `USD`ISO 4217`EUR` 通貨コード。 |
| `commerce.order.priceTotal` | すべての割引および税金が適用された後のこの注文の合計金額。 |
| `commerce.order.purchaseOrderNumber` | この購入または契約の購入者によって割り当てられた一意の ID。 |
| `commerce.order.currencyCode` | [ や ](https://en.wikipedia.org/wiki/ISO_4217) など、使用される `USD`ISO 4217`EUR` 通貨コード。 |
| `commerce.order.lastUpdatedDate` | コマースシステムで特定の注文レコードが最後に更新された時間。 |
| `commerce.shipping` | 1 つ以上の商品に関する配送の詳細。 |
| `commerce.shipping.shippingMethod` | お客様が選択した配送方法（通常配送、優先配送、店舗での受け取りなど）。 |
| `commerce.shipping.shippingAmount` | お客様が配送用に支払う必要があった金額。 |
| `commerce.shipping.address` | 物理的な配送先住所。 |
| `commerce.shipping.address.street1` | プライマリの番地レベルの情報、アパート番号、通り番号、通り名。 |
| `commerce.shipping.address.street2` | オプションの住所情報 2 行目。 |
| `commerce.shipping.address.city` | 市区町村の名前。 |
| `commerce.shipping.address.state` | 都道府県の名前。 これは自由形式フィールドです。 |
| `commerce.shipping.address.postalCode` | 場所の郵便番号。 郵便番号は、すべての国で利用できるわけではありません。 一部の国では、郵便番号の一部のみが含まれます。 |
| `commerce.shipping.address.country` | 政府が管理する領土の名前。 `xdm:countryCode` 以外の場合、これは自由形式のフィールドで、どの言語でも国名を持つことができます。 |
| `commerce.shipping.currencyCode` | [ や ](https://en.wikipedia.org/wiki/ISO_4217) など、使用される `USD`ISO 4217`EUR` 通貨コード。 |
| `commerce.shipping.trackingNumber` | 注文品目出荷に対して出荷配送業者によって提供される追跡番号。 |
| `commerce.shipping.trackingURL` | 注文項目の配送ステータスをトラッキングする URL。 |
| `commerce.shipping.shipDate` | 注文から 1 つ以上の品目が出荷された日付。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |
| `commerce.billing.address` | 請求先住所。 |
| `commerce.billing.address.street1` | プライマリの番地レベルの情報、アパート番号、通り番号、通り名 |
| `commerce.billing.address.street2` | 番地レベルの情報の追加フィールド。 |
| `commerce.billing.address.city` | 市区町村の名前。 |
| `commerce.billing.address.state` | 州の名前。 これは自由形式フィールドです。 |
| `commerce.billing.address.postalCode` | 場所の郵便番号。 郵便番号は、すべての国で利用できるわけではありません。 一部の国では、郵便番号の一部のみが含まれます。 |
| `commerce.billing.address.country` | 政府が管理する領土の名前。 `xdm:countryCode` 以外の場合、これは自由形式のフィールドで、どの言語でも国名を持つことができます。 |
| `personalEmail` | 個人の電子メールアドレス。 |
| `personalEmail.address` | 例えば、技術的アドレス `name@domain.com`、RFC2822 および後続の標準で一般的に定義されています。 |
| `productListItems` | 順序の商品の配列。 |
| `productListItems.SKU` | 在庫管理単位。 商品の一意の ID。 |
| `productListItems.name` | 商品の表示名または人間が読み取れる名前。 |
| `productListItems.priceTotal` | 商品品目の合計価格。 |
| `productListItems.quantity` | 買い物かごに入っている商品の単位数。 |
| `productListItems.discountAmount` | 適用される割引額を示します。 |
| `productListItems.currencyCode` | [ や ](https://en.wikipedia.org/wiki/ISO_4217) など、使用される `USD`ISO 4217`EUR` 通貨コード。 |
| `productListItems.selectedOptions` | 設定可能な製品に使用されるフィールド。 |
| `productListItems.selectedOptions.attribute` | `size` や `color` など、設定可能な製品の属性を識別します。 |
| `productListItems.selectedOptions.value` | `small` または `black` などの属性の値を識別します。 |
| `productListItems.categories` | 商品のカテゴリに関する情報が含まれます。 |
| `productListItems.categories.id` | カテゴリの一意の ID。 |
| `productListItems.categories.name` | カテゴリの名前。 |
| `productListItems.categories.path` | カテゴリへのパス。 |

### orderCancelled

| 説明 | XDM イベント名 |
|---|---|
| 買い物客が注文をキャンセルするとトリガーされます。 | `commerce.backofficeOrderCancelled` |

#### orderCancelled から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `commerce.order` | 注文に関する情報が含まれます。 |
| `commerce.order.purchaseID` | この購入または契約の販売者によって割り当てられた一意の ID。 ID が一意であるという保証はありません。 |
| `commerce.order.purchaseOrderNumber` | この購入または契約の購入者によって割り当てられた一意の ID。 |
| `commerce.order.cancelDate` | 買い物客が注文をキャンセルした日時。 |
| `commerce.order.lastUpdatedDate` | コマースシステムで特定の注文レコードが最後に更新された時間。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |
| `personalEmail` | 個人の電子メールアドレス。 |
| `personalEmail.address` | 例えば、技術的アドレス `name@domain.com`、RFC2822 および後続の標準で一般的に定義されています。 |

### orderLineItemRefunded

| 説明 | XDM イベント名 |
|---|---|
| 買い物客が返された項目に対して返金されたときにトリガーされます。 | `commerce.backofficeCreditMemoIssued` |

#### orderLineItemRefunded から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `commerce.order` | 注文に関する情報が含まれます。 |
| `commerce.order.purchaseID` | この購入または契約の販売者によって割り当てられた一意の ID。 ID が一意であるという保証はありません。 |
| `commerce.order.lastUpdatedDate` | コマースシステムで特定の注文レコードが最後に更新された時間。 |
| `commerce.order.purchaseOrderNumber` | この購入または契約の購入者によって割り当てられた一意の ID。 |
| `commerce.refunds` | この注文の払い戻しのリスト。 |
| `commerce.refunds.transactionID` | この払戻の一意の ID。 |
| `commerce.refunds.refundAmount` | 払い戻しの金額。 |
| `commerce.refunds.refundPaymentType` | この注文の支払い方法。 カウントされ、カスタム値が許可されます。 |
| `commerce.refunds.currencyCode` | [ や ](https://en.wikipedia.org/wiki/ISO_4217) など、使用される `USD`ISO 4217`EUR` 通貨コード。 |
| `personalEmail` | 個人の電子メールアドレス。 |
| `personalEmail.address` | 例えば、技術的アドレス `name@domain.com`、RFC2822 および後続の標準で一般的に定義されています。 |
| `productListItems` | 順序の商品の配列。 |
| `productListItems.SKU` | 在庫管理単位。 商品の一意の ID。 |
| `productListItems.name` | 商品の表示名または人間が読み取れる名前。 |
| `productListItems.priceTotal` | 商品品目の合計価格。 |
| `productListItems.quantity` | 買い物かごに入っている商品の単位数。 |
| `productListItems.discountAmount` | 適用される割引額を示します。 |
| `productListItems.currencyCode` | [ や ](https://en.wikipedia.org/wiki/ISO_4217) など、使用される `USD`ISO 4217`EUR` 通貨コード。 |
| `productListItems.selectedOptions` | 設定可能な製品に使用されるフィールド。 |
| `productListItems.selectedOptions.attribute` | `size` や `color` など、設定可能な製品の属性を識別します。 |
| `productListItems.selectedOptions.value` | `small` または `black` などの属性の値を識別します。 |
| `productListItems.categories` | 商品のカテゴリに関する情報が含まれます。 |
| `productListItems.categories.id` | カテゴリの一意の ID。 |
| `productListItems.categories.name` | カテゴリの名前。 |
| `productListItems.categories.path` | カテゴリへのパス。 |

### orderItemsReturnInitiated

| 説明 | XDM イベント名 |
|---|---|
| 買い物客が項目を返すようリクエストしたときにトリガーされます。 | `commerce.backofficeOrderItemsReturnInitiated` |

#### orderItemsReturnInitiated から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `commerce.order` | 注文に関する情報が含まれます。 |
| `commerce.order.purchaseID` | この購入または契約の販売者によって割り当てられた一意の ID。 ID が一意であるという保証はありません。 |
| `commerce.order.returns` | この注文の RMA （商品返品承認）情報。 |
| `commerce.order.returns.returnID` | この RMA （返品承認）の一意の ID。 |
| `commerce.order.returns.returnStatus` | 保留、クローズなど、RMA （返品承認）のステータス。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |
| `personalEmail` | 個人の電子メールアドレス。 |
| `personalEmail.address` | 例えば、技術的アドレス `name@domain.com`、RFC2822 および後続の標準で一般的に定義されています。 |
| `productListItems` | 順序の商品の配列。 |
| `productListItems.SKU` | 在庫管理単位。 商品の一意の ID。 |
| `productListItems.name` | 商品の表示名または人間が読み取れる名前。 |
| `productListItems.quantity` | 買い物かごに入っている商品の単位数。 |
| `productListItems.selectedOptions` | 設定可能な製品に使用されるフィールド。 |
| `productListItems.selectedOptions.attribute` | `size` や `color` など、設定可能な製品の属性を識別します。 |
| `productListItems.selectedOptions.value` | `small` または `black` などの属性の値を識別します。 |
| `productListItems.categories` | 商品のカテゴリに関する情報が含まれます。 |
| `productListItems.categories.id` | カテゴリの一意の ID。 |
| `productListItems.categories.name` | カテゴリの名前。 |
| `productListItems.categories.path` | カテゴリへのパス。 |
| `productListItems.returnItem` | この品目の RMA （返品承認）情報。 |
| `productListItems.returnItem.returnStatus` | 返される項目のステータス（保留中、承認済みなど）。 |
| `productListItems.returnItem.returnReason` | このアイテムに対して返品が要求される理由。 |
| `productListItems.returnItem.returnItemCondition` | 返品を要求する品目の条件。 |
| `productListItems.returnItem.returnResolution` | 返金、交換など、返品される商品のリクエストされた解決。 |
| `productListItems.returnItem.returnQuantityRequested` | 買い物客が返すようにリクエストした、この項目の数。 |
| `productListItems.returnItem.returnQuantityAuthorized` | 返すことができる、このアイテムの番号です。 |
| `productListItems.returnItem.eturnQuantityReceived` | 返された項目の受信数。 |
| `productListItems.returnItem.returnQuantityApproved` | 返品が完全に完了し、承認されたこの品目の番号。 |

### orderItemReturnComplete

| 説明 | XDM イベント名 |
|---|---|
| 買い物客が返品をリクエストした項目が完了するとトリガーされます。 | `commerce.backofficeOrderItemsReturnCompleted` |

#### orderItemReturnCompleted から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `commerce.order` | 注文に関する情報が含まれます。 |
| `commerce.order.purchaseID` | この購入または契約の販売者によって割り当てられた一意の ID。 ID が一意であるという保証はありません。 |
| `commerce.order.returns` | この注文の RMA （商品返品承認）情報。 |
| `commerce.order.returns.returnID` | この RMA （返品承認）の一意の ID。 |
| `commerce.order.returns.returnStatus` | 保留、クローズなど、RMA （返品承認）のステータス。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |
| `personalEmail` | 個人の電子メールアドレス。 |
| `personalEmail.address` | 例えば、技術的アドレス `name@domain.com`、RFC2822 および後続の標準で一般的に定義されています。 |
| `productListItems` | 順序の商品の配列。 |
| `productListItems.SKU` | 在庫管理単位。 商品の一意の ID。 |
| `productListItems.name` | 商品の表示名または人間が読み取れる名前。 |
| `productListItems.selectedOptions` | 設定可能な製品に使用されるフィールド。 |
| `productListItems.selectedOptions.attribute` | `size` や `color` など、設定可能な製品の属性を識別します。 |
| `productListItems.selectedOptions.value` | `small` または `black` などの属性の値を識別します。 |
| `productListItems.categories` | 商品のカテゴリに関する情報が含まれます。 |
| `productListItems.categories.id` | カテゴリの一意の ID。 |
| `productListItems.categories.name` | カテゴリの名前。 |
| `productListItems.categories.path` | カテゴリへのパス。 |
| `productListItems.returnItem` | この品目の RMA （返品承認）情報。 |
| `productListItems.returnItem.returnStatus` | 返される項目のステータス（保留中、承認済みなど）。 |
| `productListItems.returnItem.returnReason` | このアイテムに対して返品が要求される理由。 |
| `productListItems.returnItem.returnItemCondition` | 返品を要求する品目の条件。 |
| `productListItems.returnItem.returnResolution` | 返金、交換など、返品される商品のリクエストされた解決。 |
| `productListItems.returnItem.returnQuantityRequested` | 買い物客が返すようにリクエストした、この項目の数。 |
| `productListItems.returnItem.returnQuantityAuthorized` | 返すことができる、このアイテムの番号です。 |
| `productListItems.returnItem.eturnQuantityReceived` | 返された項目の受信数。 |
| `productListItems.returnItem.returnQuantityApproved` | 返品が完全に完了し、承認されたこの品目の番号。 |

### orderShipmentCompleted

| 説明 | XDM イベント名 |
|---|---|
| 出荷の完了時にトリガーされます。 | `commerce.backofficeOrderShipmentCompleted` |

#### orderShipmentCompleted から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `commerce.order` | 注文に関する情報が含まれます。 |
| `commerce.order.purchaseID` | この購入または契約の販売者によって割り当てられた一意の ID。 ID が一意であるという保証はありません。 |
| `commerce.order.payments` | この注文の支払いのリスト。 |
| `commerce.order.payments.paymentTransactionID` | この支払トランザクションの一意の ID。 |
| `commerce.order.payments.paymentAmount` | 支払いの値。 |
| `commerce.order.payments.paymentType` | この注文の支払い方法。 カウントされ、カスタム値が許可されます。 |
| `commerce.order.payments.currencyCode` | [ や ](https://en.wikipedia.org/wiki/ISO_4217) など、使用される `USD`ISO 4217`EUR` 通貨コード。 |
| `commerce.order.taxAmount` | 最終支払の一部として購入者が支払った税額。 |
| `commerce.order.createdDate` | コマースシステムで新しい注文が作成された日時。 例：`2022-10-15T20:20:39+00:00`。 |
| `commerce.shipping` | 1 つ以上の商品に関する配送の詳細。 |
| `commerce.shipping.shippingMethod` | お客様が選択した配送方法（通常配送、優先配送、店舗での受け取りなど）。 |
| `commerce.shipping.shippingAmount` | お客様が配送用に支払う必要があった金額。 |
| `commerce.shipping.shipDate` | 注文から 1 つ以上の品目が出荷された日付。 |
| `commerce.shipping.address` | 物理的な配送先住所。 |
| `commerce.shipping.address.street1` | プライマリの番地レベルの情報、アパート番号、通り番号、通り名。 |
| `commerce.shipping.address.street2` | オプションの住所情報 2 行目。 |
| `commerce.shipping.address.city` | 市区町村の名前。 |
| `commerce.shipping.address.state` | 都道府県の名前。 これは自由形式フィールドです。 |
| `commerce.shipping.address.postalCode` | 場所の郵便番号。 郵便番号は、すべての国で利用できるわけではありません。 一部の国では、郵便番号の一部のみが含まれます。 |
| `commerce.shipping.address.country` | 政府が管理する領土の名前。 `xdm:countryCode` 以外の場合、これは自由形式のフィールドで、どの言語でも国名を持つことができます。 |
| `commerce.billing.address` | 請求先住所。 |
| `commerce.billing.address.street1` | プライマリの番地レベルの情報、アパート番号、通り番号、通り名 |
| `commerce.billing.address.street2` | 番地レベルの情報の追加フィールド。 |
| `commerce.billing.address.city` | 市区町村の名前。 |
| `commerce.billing.address.state` | 州の名前。 これは自由形式フィールドです。 |
| `commerce.billing.address.postalCode` | 場所の郵便番号。 郵便番号は、すべての国で利用できるわけではありません。 一部の国では、郵便番号の一部のみが含まれます。 |
| `commerce.billing.address.country` | 政府が管理する領土の名前。 `xdm:countryCode` 以外の場合、これは自由形式のフィールドで、どの言語でも国名を持つことができます。 |
| `personalEmail` | 個人の電子メールアドレス。 |
| `personalEmail.address` | 例えば、技術的アドレス `name@domain.com`、RFC2822 および後続の標準で一般的に定義されています。 |
| `productListItems` | 順序の商品の配列。 |
| `productListItems.SKU` | 在庫管理単位。 商品の一意の ID。 |
| `productListItems.name` | 商品の表示名または人間が読み取れる名前。 |
| `productListItems.priceTotal` | 商品品目の合計価格。 |
| `productListItems.quantity` | 買い物かごに入っている商品の単位数。 |
| `productListItems.discountAmount` | 適用される割引額を示します。 |
| `productListItems.currencyCode` | [ や ](https://en.wikipedia.org/wiki/ISO_4217) など、使用される `USD`ISO 4217`EUR` 通貨コード。 |
| `productListItems.selectedOptions` | 設定可能な製品に使用されるフィールド。 |
| `productListItems.selectedOptions.attribute` | `size` や `color` など、設定可能な製品の属性を識別します。 |
| `productListItems.selectedOptions.value` | `small` または `black` などの属性の値を識別します。 |
| `productListItems.categories` | 商品のカテゴリに関する情報が含まれます。 |
| `productListItems.categories.id` | カテゴリの一意の ID。 |
| `productListItems.categories.name` | カテゴリの名前。 |
| `productListItems.categories.path` | カテゴリへのパス。 |

## 顧客プロファイルイベント

サーバーサイドから取得したプロファイルイベントには、`accountCreated`、`accountUpdated`、`accountDeleted` などのアカウント情報が含まれます。 このデータは、新規登録割引オファーの送信、アカウント変更の確認など、セグメントを適切に定義したり、マーケティングキャンペーンを実行したりするために必要な、主な顧客詳細の入力に使用されます。 [ ストアフロント ](events.md#customer-profile-events) から取り込まれた類似のプロファイルイベントがあります。

>[!NOTE]
>
>各顧客プロファイルイベントには、「[`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html)」フィールドも含まれます。このフィールドには、プロファイルのプライマリ識別子としてシステム生成のCommerce顧客 ID と、セカンダリ識別子として使用されるメール ID が含まれます。 [ 詳細情報 ](custom-identities.md) 顧客プロファイルの ID を強化するカスタム ID 属性の作成方法。

### accountCreated

| 説明 | XDM イベント名 |
|---|---|
| 買い物客がアカウントを作成しようとしたときにトリガーされます。 | `userAccount.backofficeCreateProfile` |

#### accountCreated から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `person` | 顧客に関する情報が含まれます。 |
| `person.name` | 顧客の名前に関する情報が含まれます。 |
| `person.name.firstName` | 顧客の名が含まれます。 |
| `person.name.lastName` | 顧客の姓が含まれます。 |
| `personalEmail` | 個人の電子メールアドレス。 |
| `personalEmail.address` | 例えば、技術的アドレス `name@domain.com`、RFC2822 および後続の標準で一般的に定義されています。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |

### accountUpdated

| 説明 | XDM イベント名 |
|---|---|
| 買い物客がアカウントを編集しようとしたときにトリガーされます。 | `userAccount.backofficeUpdateProfile` |

#### accountUpdated から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `person` | 顧客に関する情報が含まれます。 |
| `person.name` | 顧客の名前に関する情報が含まれます。 |
| `person.name.firstName` | 顧客の名が含まれます。 |
| `person.name.lastName` | 顧客の姓が含まれます。 |
| `personalEmail` | 個人の電子メールアドレス。 |
| `personalEmail.address` | 例えば、技術的アドレス `name@domain.com`、RFC2822 および後続の標準で一般的に定義されています。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |

### accountDeleted

| 説明 | XDM イベント名 |
|---|---|
| 買い物客がアカウントを削除しようとするとトリガーされます。 | `userAccount.backofficeDeleteProfile` |

#### accountDeleted から収集されたデータ

次の表に、このイベントについて収集されるデータを示します。

| フィールド | 説明 |
|---|---|
| `person` | 顧客に関する情報が含まれます。 |
| `person.name` | 顧客の名前に関する情報が含まれます。 |
| `person.name.firstName` | 顧客の名が含まれます。 |
| `person.name.lastName` | 顧客の姓が含まれます。 |
| `personalEmail` | 個人の電子メールアドレス。 |
| `personalEmail.address` | 例えば、技術的アドレス `name@domain.com`、RFC2822 および後続の標準で一般的に定義されています。 |
| `commerce.commerceScope` | イベントが発生した場所（ストア表示、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境 ID。 ハイフンで区切られた 32 桁の英数字 ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード。 Web サイトごとに多数のストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストア表示コード。 1 つのストアに対して多数のストア表示を設定できます。 |
| `commerce.commerceScope.websiteCode` | 一意の Web サイトコード。 1 つの環境に多数の web サイトを含めることができます。 |
