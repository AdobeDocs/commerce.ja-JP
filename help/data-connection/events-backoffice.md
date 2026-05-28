---
title: バックオフィスイベント
description: 各バックオフィスイベントがどのようなデータを取得するかをご確認ください。
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: 65cf8150-1a14-4d4c-aa0c-1545109e4fe7
TQID: https://experienceleague.adobe.com/ARHjckt-D38iqChgfJpiVGXO8Pz2YN6Oj5HFWmwCVEA
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 3714
ht-degree: 0%

---

# [!DNL Data Connection] バックオフィスイベント

次に、[!DNL Data Connection]拡張機能のインストール時に使用できるCommerce バックオフィスイベントを示します。 これらのイベントで収集されたデータは、Adobe Experience Platformに送信されます。 [&#x200B; カスタムイベント &#x200B;](custom-events.md)を作成して、標準提供されていない追加データを収集することもできます。

次のイベントが収集するデータに加えて、Adobe Experience Platform Web SDKが提供する[その他のデータ &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html)も取得できます。

バックオフィスイベントには、サーバーサイドのデータが含まれます。 このデータには、注文が行われたか、キャンセルされたか、返金されたか、出荷されたか、完了したかなどの[注文状況](#order-status)情報が含まれます。 サーバーサイドのデータには、アカウントが作成、更新、削除されたかどうかなど、[顧客プロファイルイベント &#x200B;](#customer-profile-events)の情報も含まれます。

>[!NOTE]
>
>すべてのバックオフィスイベントには、買い物客の電子メールアドレス（使用可能な場合）、およびECIDを含む[`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html) フィールドが含まれます。

## 注文ステータス

注文状況データには、買い物客の注文が360表示されます。 このビューにより、マーケティング施策を策定する際に、注文全体の状況をより適切にターゲティングまたは分析できます。 例えば、特定の商品カテゴリーのトレンドを発見し、年のさまざまな時期に優れたパフォーマンスを発揮できるようにします。 例えば、寒い時期に売れる冬服や、買い物客が長年にわたって興味を持っている特定の商品色です。 さらに、注文状況データは、過去の注文にもとづいて買い物客のコンバージョン傾向を把握することで、生涯顧客価値の計算に役立ちます。

### orderPlaced

| 説明 | XDM イベント名 |
|---|---|
| 顧客が注文したときにトリガーされます。 | `commerce.backofficeOrderPlaced` |

#### orderPlacedから収集されたデータ

次の表に、このイベントで収集されたデータを示します。

| フィールド | 説明 |
|---|---|
| `commerce.order` | 注文に関する情報が含まれます。 |
| `commerce.order.purchaseID` | この購入または契約に対して販売者によって割り当てられた一意のID。 IDが一意である保証はありません。 |
| `commerce.order.payments` | この注文の支払のリスト。 |
| `commerce.order.payments.paymentTransactionID` | この支払いトランザクションの一意のID。 |
| `commerce.order.payments.paymentAmount` | 支払いの価値。 |
| `commerce.order.payments.paymentType` | この注文の支払い方法。 カウントされ、カスタム値を使用できます。 |
| `commerce.order.payments.currencyCode` | [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)通貨コード （例：`USD`または`EUR`）。 |
| `commerce.order.taxAmount` | 購入者が最終支払いの一部として支払った税額。 |
| `commerce.order.discountAmount` | 注文全体に適用される割引額を示します。 |
| `commerce.order.createdDate` | コマースシステムで新しい注文が作成された日時。 例：`2022-10-15T20:20:39+00:00`。 |
| `commerce.order.currencyCode` | 注文合計に使用されるISO 4217通貨コード。 |
| `commerce.shipping` | 1つ以上の製品の配送詳細情報。 |
| `commerce.shipping.shippingMethod` | 標準配送、迅速配送、店舗での受け取りなど、顧客が選択した配送方法。 |
| `commerce.shipping.shippingAmount` | 顧客が配送料として支払った金額。 |
| `commerce.shipping.currencyCode` | 配送合計に使用されるISO 4217通貨コード。 |
| `commerce.commerceScope` | イベントが発生した場所（ストアビュー、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境ID。 ハイフンで区切られた32桁の英数字ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード： Web サイトごとに多くのストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストアビューコード。 ストアごとに多くのストアビューを設定できます。 |
| `commerce.commerceScope.websiteCode` | 固有のweb サイトコード： 環境内に多くのweb サイトを持つことができます。 |
| `commerce.billing.address` | 請求先住所。 |
| `commerce.billing.address.street1` | プライマリの住所レベル情報、アパート番号、住所、および住所 |
| `commerce.billing.address.street2` | ストリートレベル情報の追加フィールド。 |
| `commerce.billing.address.city` | 市の名前。 |
| `commerce.billing.address.state` | 州の名前。 これは自由形式のフィールドです。 |
| `commerce.billing.address.postalCode` | 場所の郵便番号。 郵便番号はすべての国で利用できるわけではありません。 一部の国では、郵便番号の一部しか含まれていません。 |
| `commerce.billing.address.country` | 政府が管理する地域の名前。 `xdm:countryCode`以外の自由形式フィールドで、国名を任意の言語で使用できます。 |
| `personalEmail` | 個人のメールアドレス。 |
| `personalEmail.address` | テクニカルアドレス （例：`name@domain.com`）は、RFC2822およびそれ以降の規格で一般的に定義されています。 |
| `productListItems` | 注文の商品の配列。 |
| `productListItems.id` | この製品エントリの行項目識別子。 |
| `productListItems.SKU` | 在庫保管単位。 製品の一意のID。 |
| `productListItems.name` | 製品の表示名または読みやすい名前。 |
| `productListItems.priceTotal` | 製品品目の合計価格です。 |
| `productListItems.quantity` | カート内の商品ユニットの数。 |
| `productListItems.discountAmount` | 適用された割引金額を示します。 |
| `productListItems.currencyCode` | [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)通貨コード （例：`USD`または`EUR`）。 |
| `productListItems.selectedOptions` | 設定可能な製品に使用されるフィールド。 |
| `productListItems.selectedOptions.attribute` | `size`や`color`など、設定可能な製品の属性を識別します。 |
| `productListItems.selectedOptions.value` | `small`や`black`などの属性の値を識別します。 |
| `productListItems.categories` | 製品カテゴリに関する情報が含まれます。 |
| `productListItems.categories.id` | カテゴリの一意のID。 |
| `productListItems.categories.name` | カテゴリの名前。 |
| `productListItems.categories.path` | カテゴリへのパス。 |
| `productListItems.productImageUrl` | 製品のメイン画像URL。 |

### orderInvoiced

| 説明 | XDM イベント名 |
|---|---|
| 加盟店が支払いを要求する請求書を送信したときにトリガーされます。 | `commerce.backofficeOrderInvoiced` |

#### orderInvoicedから収集されたデータ

次の表に、このイベントで収集されたデータを示します。

| フィールド | 説明 |
|---|---|
| `commerce.order` | 注文に関する情報が含まれます。 |
| `commerce.order.purchaseID` | この購入または契約に対して販売者によって割り当てられた一意のID。 IDが一意である保証はありません。 |
| `commerce.order.priceTotal` | すべての割引と税金が適用された後の、この注文の合計価格。 |
| `commerce.order.currencyCode` | 注文合計に使用されるISO 4217通貨コード。 |
| `commerce.order.purchaseOrderNumber` | この購入または契約に対して購入者によって割り当てられた一意のID。 |
| `commerce.order.payments` | この注文の支払のリスト。 |
| `commerce.order.payments.currencyCode` | [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)通貨コード （例：`USD`または`EUR`）。 |
| `commerce.order.payments.paymentType` | この注文の支払い方法。 カウントされ、カスタム値を使用できます。 |
| `commerce.order.payments.paymentAmount` | 支払いの価値。 |
| `commerce.shipping` | 1つ以上の製品の配送詳細情報。 |
| `commerce.shipping.shippingMethod` | 標準配送、迅速配送、店舗での受け取りなど、顧客が選択した配送方法。 |
| `commerce.shipping.shippingAmount` | 顧客が配送料として支払った金額。 |
| `commerce.commerceScope` | イベントが発生した場所（ストアビュー、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境ID。 ハイフンで区切られた32桁の英数字ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード： Web サイトごとに多くのストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストアビューコード。 ストアごとに多くのストアビューを設定できます。 |
| `commerce.commerceScope.websiteCode` | 固有のweb サイトコード： 環境内に多くのweb サイトを持つことができます。 |
| `personalEmail` | 個人のメールアドレス。 |
| `personalEmail.address` | テクニカルアドレス （例：`name@domain.com`）は、RFC2822およびそれ以降の規格で一般的に定義されています。 |
| `productListItems` | 注文の商品の配列。 |
| `productListItems.id` | この製品エントリの行項目識別子。 |
| `productListItems.SKU` | 在庫保管単位。 製品の一意のID。 |
| `productListItems.name` | 製品の表示名または読みやすい名前。 |
| `productListItems.priceTotal` | 製品品目の合計価格です。 |
| `productListItems.quantity` | カート内の商品ユニットの数。 |
| `productListItems.discountAmount` | 適用された割引金額を示します。 |
| `productListItems.categories` | 製品カテゴリに関する情報が含まれます。 |
| `productListItems.categories.id` | カテゴリの一意のID。 |
| `productListItems.categories.name` | カテゴリの名前。 |
| `productListItems.categories.path` | カテゴリへのパス。 |

### orderItemsShipped

| 説明 | XDM イベント名 |
|---|---|
| 注文商品の発送時にトリガーされます。 | `commerce.backofficeOrderItemsShipped` |

#### orderItemsShippedから収集されたデータ

次の表に、このイベントで収集されたデータを示します。

| フィールド | 説明 |
|---|---|
| `commerce.order` | 注文に関する情報が含まれます。 |
| `commerce.order.purchaseID` | この購入または契約に対して販売者によって割り当てられた一意のID。 IDが一意である保証はありません。 |
| `commerce.order.payments` | この注文の支払のリスト。 |
| `commerce.order.payments.paymentTransactionID` | この支払いトランザクションの一意のID。 |
| `commerce.order.payments.paymentAmount` | 支払いの価値。 |
| `commerce.order.payments.paymentType` | この注文の支払い方法。 カウントされ、カスタム値を使用できます。 |
| `commerce.order.payments.currencyCode` | [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)通貨コード （例：`USD`または`EUR`）。 |
| `commerce.order.priceTotal` | すべての割引と税金が適用された後の、この注文の合計価格。 |
| `commerce.order.purchaseOrderNumber` | この購入または契約に対して購入者によって割り当てられた一意のID。 |
| `commerce.order.currencyCode` | [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)通貨コード （例：`USD`または`EUR`）。 |
| `commerce.order.lastUpdatedDate` | 特定の注文レコードがコマースシステムで最後に更新された時間。 |
| `commerce.shipping` | 1つ以上の製品の配送詳細情報。 |
| `commerce.shipping.shippingMethod` | 標準配送、迅速配送、店舗での受け取りなど、顧客が選択した配送方法。 |
| `commerce.shipping.shippingAmount` | 顧客が配送料として支払った金額。 |
| `commerce.shipping.address` | 物理的な配送先住所。 |
| `commerce.shipping.address.street1` | プライマリの住所、アパート番号、住所、住所の名前。 |
| `commerce.shipping.address.street2` | オプションのストリート情報2行目。 |
| `commerce.shipping.address.city` | 市の名前。 |
| `commerce.shipping.address.state` | 州の名前。 これは自由形式のフィールドです。 |
| `commerce.shipping.address.postalCode` | 場所の郵便番号。 郵便番号はすべての国で利用できるわけではありません。 一部の国では、郵便番号の一部しか含まれていません。 |
| `commerce.shipping.address.country` | 政府が管理する地域の名前。 `xdm:countryCode`以外の自由形式フィールドで、国名を任意の言語で使用できます。 |
| `commerce.shipping.currencyCode` | [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)通貨コード （例：`USD`または`EUR`）。 |
| `commerce.shipping.trackingNumber` | 注文品出荷に対して配送業者が提供する追跡番号。 |
| `commerce.shipping.trackingURL` | 注文商品の配送状況を追跡するURL。 |
| `commerce.shipping.shipDate` | 注文の1つ以上の品目が出荷された日付。 |
| `commerce.commerceScope` | イベントが発生した場所（ストアビュー、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境ID。 ハイフンで区切られた32桁の英数字ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード： Web サイトごとに多くのストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストアビューコード。 ストアごとに多くのストアビューを設定できます。 |
| `commerce.commerceScope.websiteCode` | 固有のweb サイトコード： 環境内に多くのweb サイトを持つことができます。 |
| `commerce.billing.address` | 請求先住所。 |
| `commerce.billing.address.street1` | プライマリの住所レベル情報、アパート番号、住所、および住所 |
| `commerce.billing.address.street2` | ストリートレベル情報の追加フィールド。 |
| `commerce.billing.address.city` | 市の名前。 |
| `commerce.billing.address.state` | 州の名前。 これは自由形式のフィールドです。 |
| `commerce.billing.address.postalCode` | 場所の郵便番号。 郵便番号はすべての国で利用できるわけではありません。 一部の国では、郵便番号の一部しか含まれていません。 |
| `commerce.billing.address.country` | 政府が管理する地域の名前。 `xdm:countryCode`以外の自由形式フィールドで、国名を任意の言語で使用できます。 |
| `personalEmail` | 個人のメールアドレス。 |
| `personalEmail.address` | テクニカルアドレス （例：`name@domain.com`）は、RFC2822およびそれ以降の規格で一般的に定義されています。 |
| `productListItems` | 注文の商品の配列。 |
| `productListItems.SKU` | 在庫保管単位。 製品の一意のID。 |
| `productListItems.name` | 製品の表示名または読みやすい名前。 |
| `productListItems.priceTotal` | 製品品目の合計価格です。 |
| `productListItems.quantity` | カート内の商品ユニットの数。 |
| `productListItems.discountAmount` | 適用された割引金額を示します。 |
| `productListItems.currencyCode` | [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)通貨コード （例：`USD`または`EUR`）。 |
| `productListItems.selectedOptions` | 設定可能な製品に使用されるフィールド。 |
| `productListItems.selectedOptions.attribute` | `size`や`color`など、設定可能な製品の属性を識別します。 |
| `productListItems.selectedOptions.value` | `small`や`black`などの属性の値を識別します。 |
| `productListItems.categories` | 製品カテゴリに関する情報が含まれます。 |
| `productListItems.categories.id` | カテゴリの一意のID。 |
| `productListItems.categories.name` | カテゴリの名前。 |
| `productListItems.categories.path` | カテゴリへのパス。 |

### orderCanceled

| 説明 | XDM イベント名 |
|---|---|
| 買い物客が注文をキャンセルしたときにトリガーされます。 | `commerce.backofficeOrderCancelled` |

#### orderCanceledから収集されたデータ

次の表に、このイベントで収集されたデータを示します。

| フィールド | 説明 |
|---|---|
| `commerce.order` | 注文に関する情報が含まれます。 |
| `commerce.order.purchaseID` | この購入または契約に対して販売者によって割り当てられた一意のID。 IDが一意である保証はありません。 |
| `commerce.order.purchaseOrderNumber` | この購入または契約に対して購入者によって割り当てられた一意のID。 |
| `commerce.order.cancelDate` | 買い物客が注文をキャンセルした日時。 |
| `commerce.order.lastUpdatedDate` | 特定の注文レコードがコマースシステムで最後に更新された時間。 |
| `commerce.commerceScope` | イベントが発生した場所（ストアビュー、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境ID。 ハイフンで区切られた32桁の英数字ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード： Web サイトごとに多くのストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストアビューコード。 ストアごとに多くのストアビューを設定できます。 |
| `commerce.commerceScope.websiteCode` | 固有のweb サイトコード： 環境内に多くのweb サイトを持つことができます。 |
| `personalEmail` | 個人のメールアドレス。 |
| `personalEmail.address` | テクニカルアドレス （例：`name@domain.com`）は、RFC2822およびそれ以降の規格で一般的に定義されています。 |

### orderLineItemRefunded

| 説明 | XDM イベント名 |
|---|---|
| 買い物客が返品された商品に対して返金されたときにトリガーされます。 | `commerce.backofficeCreditMemoIssued` |

#### orderLineItemRefundedから収集されたデータ

次の表に、このイベントで収集されたデータを示します。

| フィールド | 説明 |
|---|---|
| `commerce.order` | 注文に関する情報が含まれます。 |
| `commerce.order.purchaseID` | この購入または契約に対して販売者によって割り当てられた一意のID。 IDが一意である保証はありません。 |
| `commerce.order.lastUpdatedDate` | 特定の注文レコードがコマースシステムで最後に更新された時間。 |
| `commerce.order.purchaseOrderNumber` | この購入または契約に対して購入者によって割り当てられた一意のID。 |
| `commerce.refunds` | この注文の返金リスト。 |
| `commerce.refunds.transactionID` | この返品の一意のID。 |
| `commerce.refunds.refundAmount` | 返金の値。 |
| `commerce.refunds.refundPaymentType` | この注文の支払い方法。 カウントされ、カスタム値を使用できます。 |
| `commerce.refunds.currencyCode` | [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)通貨コード （例：`USD`または`EUR`）。 |
| `personalEmail` | 個人のメールアドレス。 |
| `personalEmail.address` | テクニカルアドレス （例：`name@domain.com`）は、RFC2822およびそれ以降の規格で一般的に定義されています。 |
| `productListItems` | 注文の商品の配列。 |
| `productListItems.SKU` | 在庫保管単位。 製品の一意のID。 |
| `productListItems.name` | 製品の表示名または読みやすい名前。 |
| `productListItems.priceTotal` | 製品品目の合計価格です。 |
| `productListItems.quantity` | カート内の商品ユニットの数。 |
| `productListItems.discountAmount` | 適用された割引金額を示します。 |
| `productListItems.currencyCode` | [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)通貨コード （例：`USD`または`EUR`）。 |
| `productListItems.selectedOptions` | 設定可能な製品に使用されるフィールド。 |
| `productListItems.selectedOptions.attribute` | `size`や`color`など、設定可能な製品の属性を識別します。 |
| `productListItems.selectedOptions.value` | `small`や`black`などの属性の値を識別します。 |
| `productListItems.categories` | 製品カテゴリに関する情報が含まれます。 |
| `productListItems.categories.id` | カテゴリの一意のID。 |
| `productListItems.categories.name` | カテゴリの名前。 |
| `productListItems.categories.path` | カテゴリへのパス。 |

### orderItemsReturnInitiated

| 説明 | XDM イベント名 |
|---|---|
| 買い物客が商品の返品をリクエストしたときにトリガーされます。 | `commerce.backofficeOrderItemsReturnInitiated` |

#### orderItemsReturnInitiatedから収集されたデータ

次の表に、このイベントで収集されたデータを示します。

| フィールド | 説明 |
|---|---|
| `commerce.order` | 注文に関する情報が含まれます。 |
| `commerce.order.purchaseID` | この購入または契約に対して販売者によって割り当てられた一意のID。 IDが一意である保証はありません。 |
| `commerce.order.returns` | この注文のRMA （返品商品認証）情報。 |
| `commerce.order.returns.returnID` | このRMA （Return Merchandise Authorization）の一意のID。 |
| `commerce.order.returns.returnStatus` | 保留中、クローズなど、RMA （返品承認）のステータス。 |
| `commerce.commerceScope` | イベントが発生した場所（ストアビュー、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境ID。 ハイフンで区切られた32桁の英数字ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード： Web サイトごとに多くのストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストアビューコード。 ストアごとに多くのストアビューを設定できます。 |
| `commerce.commerceScope.websiteCode` | 固有のweb サイトコード： 環境内に多くのweb サイトを持つことができます。 |
| `personalEmail` | 個人のメールアドレス。 |
| `personalEmail.address` | テクニカルアドレス （例：`name@domain.com`）は、RFC2822およびそれ以降の規格で一般的に定義されています。 |
| `productListItems` | 注文の商品の配列。 |
| `productListItems.SKU` | 在庫保管単位。 製品の一意のID。 |
| `productListItems.name` | 製品の表示名または読みやすい名前。 |
| `productListItems.quantity` | カート内の商品ユニットの数。 |
| `productListItems.selectedOptions` | 設定可能な製品に使用されるフィールド。 |
| `productListItems.selectedOptions.attribute` | `size`や`color`など、設定可能な製品の属性を識別します。 |
| `productListItems.selectedOptions.value` | `small`や`black`などの属性の値を識別します。 |
| `productListItems.categories` | 製品カテゴリに関する情報が含まれます。 |
| `productListItems.categories.id` | カテゴリの一意のID。 |
| `productListItems.categories.name` | カテゴリの名前。 |
| `productListItems.categories.path` | カテゴリへのパス。 |
| `productListItems.returnItem` | この商品のRMA （返品承認）情報。 |
| `productListItems.returnItem.returnStatus` | 返されたアイテムのステータス（保留中、承認済みなど）。 |
| `productListItems.returnItem.returnReason` | この項目の返品が要求される理由。 |
| `productListItems.returnItem.returnItemCondition` | 返品が要求される品目の条件。 |
| `productListItems.returnItem.returnResolution` | 返金、交換など、返品される商品のリクエストされた解決。 |
| `productListItems.returnItem.returnQuantityRequested` | 買い物客が返品を要求したこの商品の番号。 |
| `productListItems.returnItem.returnQuantityAuthorized` | 返す権限を持つこのアイテムの番号。 |
| `productListItems.returnItem.eturnQuantityReceived` | 受け取った返品件数。 |
| `productListItems.returnItem.returnQuantityApproved` | 返品処理が完全に完了して承認されたこの品目の数。 |

### orderItemReturnCompleted

| 説明 | XDM イベント名 |
|---|---|
| 買い物客が返品を要求した商品が完了したときにトリガーされます。 | `commerce.backofficeOrderItemsReturnCompleted` |

#### orderItemReturnCompletedから収集されたデータ

次の表に、このイベントで収集されたデータを示します。

| フィールド | 説明 |
|---|---|
| `commerce.order` | 注文に関する情報が含まれます。 |
| `commerce.order.purchaseID` | この購入または契約に対して販売者によって割り当てられた一意のID。 IDが一意である保証はありません。 |
| `commerce.order.returns` | この注文のRMA （返品商品認証）情報。 |
| `commerce.order.returns.returnID` | このRMA （Return Merchandise Authorization）の一意のID。 |
| `commerce.order.returns.returnStatus` | 保留中、クローズなど、RMA （返品承認）のステータス。 |
| `commerce.commerceScope` | イベントが発生した場所（ストアビュー、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境ID。 ハイフンで区切られた32桁の英数字ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード： Web サイトごとに多くのストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストアビューコード。 ストアごとに多くのストアビューを設定できます。 |
| `commerce.commerceScope.websiteCode` | 固有のweb サイトコード： 環境内に多くのweb サイトを持つことができます。 |
| `personalEmail` | 個人のメールアドレス。 |
| `personalEmail.address` | テクニカルアドレス （例：`name@domain.com`）は、RFC2822およびそれ以降の規格で一般的に定義されています。 |
| `productListItems` | 注文の商品の配列。 |
| `productListItems.SKU` | 在庫保管単位。 製品の一意のID。 |
| `productListItems.name` | 製品の表示名または読みやすい名前。 |
| `productListItems.selectedOptions` | 設定可能な製品に使用されるフィールド。 |
| `productListItems.selectedOptions.attribute` | `size`や`color`など、設定可能な製品の属性を識別します。 |
| `productListItems.selectedOptions.value` | `small`や`black`などの属性の値を識別します。 |
| `productListItems.categories` | 製品カテゴリに関する情報が含まれます。 |
| `productListItems.categories.id` | カテゴリの一意のID。 |
| `productListItems.categories.name` | カテゴリの名前。 |
| `productListItems.categories.path` | カテゴリへのパス。 |
| `productListItems.returnItem` | この商品のRMA （返品承認）情報。 |
| `productListItems.returnItem.returnStatus` | 返されたアイテムのステータス（保留中、承認済みなど）。 |
| `productListItems.returnItem.returnReason` | この項目の返品が要求される理由。 |
| `productListItems.returnItem.returnItemCondition` | 返品が要求される品目の条件。 |
| `productListItems.returnItem.returnResolution` | 返金、交換など、返品される商品のリクエストされた解決。 |
| `productListItems.returnItem.returnQuantityRequested` | 買い物客が返品を要求したこの商品の番号。 |
| `productListItems.returnItem.returnQuantityAuthorized` | 返す権限を持つこのアイテムの番号。 |
| `productListItems.returnItem.eturnQuantityReceived` | 受け取った返品件数。 |
| `productListItems.returnItem.returnQuantityApproved` | 返品処理が完全に完了して承認されたこの品目の数。 |

### orderShipmentCompleted

| 説明 | XDM イベント名 |
|---|---|
| 出荷が完了したときにトリガーされます。 | `commerce.backofficeOrderShipmentCompleted` |

#### orderShipmentCompletedから収集されたデータ

次の表に、このイベントで収集されたデータを示します。

| フィールド | 説明 |
|---|---|
| `commerce.order` | 注文に関する情報が含まれます。 |
| `commerce.order.purchaseID` | この購入または契約に対して販売者によって割り当てられた一意のID。 IDが一意である保証はありません。 |
| `commerce.order.payments` | この注文の支払のリスト。 |
| `commerce.order.payments.paymentTransactionID` | この支払いトランザクションの一意のID。 |
| `commerce.order.payments.paymentAmount` | 支払いの価値。 |
| `commerce.order.payments.paymentType` | この注文の支払い方法。 カウントされ、カスタム値を使用できます。 |
| `commerce.order.payments.currencyCode` | [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)通貨コード （例：`USD`または`EUR`）。 |
| `commerce.order.taxAmount` | 購入者が最終支払いの一部として支払った税額。 |
| `commerce.order.createdDate` | コマースシステムで新しい注文が作成された日時。 例：`2022-10-15T20:20:39+00:00`。 |
| `commerce.shipping` | 1つ以上の製品の配送詳細情報。 |
| `commerce.shipping.shippingMethod` | 標準配送、迅速配送、店舗での受け取りなど、顧客が選択した配送方法。 |
| `commerce.shipping.shippingAmount` | 顧客が配送料として支払った金額。 |
| `commerce.shipping.shipDate` | 注文の1つ以上の品目が出荷された日付。 |
| `commerce.shipping.address` | 物理的な配送先住所。 |
| `commerce.shipping.address.street1` | プライマリの住所、アパート番号、住所、住所の名前。 |
| `commerce.shipping.address.street2` | オプションのストリート情報2行目。 |
| `commerce.shipping.address.city` | 市の名前。 |
| `commerce.shipping.address.state` | 州の名前。 これは自由形式のフィールドです。 |
| `commerce.shipping.address.postalCode` | 場所の郵便番号。 郵便番号はすべての国で利用できるわけではありません。 一部の国では、郵便番号の一部しか含まれていません。 |
| `commerce.shipping.address.country` | 政府が管理する地域の名前。 `xdm:countryCode`以外の自由形式フィールドで、国名を任意の言語で使用できます。 |
| `commerce.billing.address` | 請求先住所。 |
| `commerce.billing.address.street1` | プライマリの住所レベル情報、アパート番号、住所、および住所 |
| `commerce.billing.address.street2` | ストリートレベル情報の追加フィールド。 |
| `commerce.billing.address.city` | 市の名前。 |
| `commerce.billing.address.state` | 州の名前。 これは自由形式のフィールドです。 |
| `commerce.billing.address.postalCode` | 場所の郵便番号。 郵便番号はすべての国で利用できるわけではありません。 一部の国では、郵便番号の一部しか含まれていません。 |
| `commerce.billing.address.country` | 政府が管理する地域の名前。 `xdm:countryCode`以外の自由形式フィールドで、国名を任意の言語で使用できます。 |
| `personalEmail` | 個人のメールアドレス。 |
| `personalEmail.address` | テクニカルアドレス （例：`name@domain.com`）は、RFC2822およびそれ以降の規格で一般的に定義されています。 |
| `productListItems` | 注文の商品の配列。 |
| `productListItems.SKU` | 在庫保管単位。 製品の一意のID。 |
| `productListItems.name` | 製品の表示名または読みやすい名前。 |
| `productListItems.priceTotal` | 製品品目の合計価格です。 |
| `productListItems.quantity` | カート内の商品ユニットの数。 |
| `productListItems.discountAmount` | 適用された割引金額を示します。 |
| `productListItems.currencyCode` | [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)通貨コード （例：`USD`または`EUR`）。 |
| `productListItems.selectedOptions` | 設定可能な製品に使用されるフィールド。 |
| `productListItems.selectedOptions.attribute` | `size`や`color`など、設定可能な製品の属性を識別します。 |
| `productListItems.selectedOptions.value` | `small`や`black`などの属性の値を識別します。 |
| `productListItems.categories` | 製品カテゴリに関する情報が含まれます。 |
| `productListItems.categories.id` | カテゴリの一意のID。 |
| `productListItems.categories.name` | カテゴリの名前。 |
| `productListItems.categories.path` | カテゴリへのパス。 |

## 顧客プロファイルイベント

サーバーサイドからキャプチャされたプロファイルイベントには、`accountCreated`、`accountUpdated`、`accountDeleted`などのアカウント情報が含まれます。 これらのデータは、セグメントの定義やマーケティング施策の実行に必要な顧客の詳細情報（サインアップ割引オファーの送信やアカウント変更確認の送信など）を提供するのに役立ちます。 [&#x200B; ストアフロント &#x200B;](events.md#customer-profile-events)からキャプチャされた類似のプロファイルイベントがあります。

>[!NOTE]
>
>各顧客プロファイルイベントには、[`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html) フィールドも含まれます。このフィールドには、プロファイルのプライマリ IDとして生成されたシステムのCommerce Customer IDと、セカンダリ IDとして使用される電子メール IDが含まれます。 顧客プロファイル IDを強化するためのカスタム ID属性の作成方法を[学習](custom-identities.md)します。

### accountCreated

| 説明 | XDM イベント名 |
|---|---|
| 買い物客がアカウントを作成しようとしたときにトリガーされます。 | `userAccount.backofficeCreateProfile` |

#### accountCreatedから収集されたデータ

次の表に、このイベントで収集されたデータを示します。

| フィールド | 説明 |
|---|---|
| `person` | 顧客に関する情報が含まれます。 |
| `person.name` | 顧客の名前に関する情報が含まれます。 |
| `person.name.firstName` | 顧客の名前が含まれます。 |
| `person.name.lastName` | 顧客の姓が含まれます。 |
| `personalEmail` | 個人のメールアドレス。 |
| `personalEmail.address` | テクニカルアドレス （例：`name@domain.com`）は、RFC2822およびそれ以降の規格で一般的に定義されています。 |
| `commerce.commerceScope` | イベントが発生した場所（ストアビュー、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境ID。 ハイフンで区切られた32桁の英数字ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード： Web サイトごとに多くのストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストアビューコード。 ストアごとに多くのストアビューを設定できます。 |
| `commerce.commerceScope.websiteCode` | 固有のweb サイトコード： 環境内に多くのweb サイトを持つことができます。 |

### accountUpdated

| 説明 | XDM イベント名 |
|---|---|
| 買い物客がアカウントを編集しようとしたときにトリガーされます。 | `userAccount.backofficeUpdateProfile` |

#### accountUpdatedから収集されたデータ

次の表に、このイベントで収集されたデータを示します。

| フィールド | 説明 |
|---|---|
| `person` | 顧客に関する情報が含まれます。 |
| `person.name` | 顧客の名前に関する情報が含まれます。 |
| `person.name.firstName` | 顧客の名前が含まれます。 |
| `person.name.lastName` | 顧客の姓が含まれます。 |
| `personalEmail` | 個人のメールアドレス。 |
| `personalEmail.address` | テクニカルアドレス （例：`name@domain.com`）は、RFC2822およびそれ以降の規格で一般的に定義されています。 |
| `commerce.commerceScope` | イベントが発生した場所（ストアビュー、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境ID。 ハイフンで区切られた32桁の英数字ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード： Web サイトごとに多くのストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストアビューコード。 ストアごとに多くのストアビューを設定できます。 |
| `commerce.commerceScope.websiteCode` | 固有のweb サイトコード： 環境内に多くのweb サイトを持つことができます。 |

### accountDeleted

| 説明 | XDM イベント名 |
|---|---|
| 買い物客がアカウントを削除しようとしたときにトリガーされます。 | `userAccount.backofficeDeleteProfile` |

#### accountDeletedから収集されたデータ

次の表に、このイベントで収集されたデータを示します。

| フィールド | 説明 |
|---|---|
| `person` | 顧客に関する情報が含まれます。 |
| `person.name` | 顧客の名前に関する情報が含まれます。 |
| `person.name.firstName` | 顧客の名前が含まれます。 |
| `person.name.lastName` | 顧客の姓が含まれます。 |
| `personalEmail` | 個人のメールアドレス。 |
| `personalEmail.address` | テクニカルアドレス （例：`name@domain.com`）は、RFC2822およびそれ以降の規格で一般的に定義されています。 |
| `commerce.commerceScope` | イベントが発生した場所（ストアビュー、ストア、web サイトなど）を示します。 |
| `commerce.commerceScope.environmentID` | 環境ID。 ハイフンで区切られた32桁の英数字ID。 |
| `commerce.commerceScope.storeCode` | 一意のストアコード： Web サイトごとに多くのストアを持つことができます。 |
| `commerce.commerceScope.storeViewCode` | 一意のストアビューコード。 ストアごとに多くのストアビューを設定できます。 |
| `commerce.commerceScope.websiteCode` | 固有のweb サイトコード： 環境内に多くのweb サイトを持つことができます。 |
