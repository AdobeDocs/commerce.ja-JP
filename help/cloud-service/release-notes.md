---
title: '[!DNL Adobe Commerce as a Cloud Service] リリースノート'
description: ' [!DNL Adobe Commerce as a Cloud Service]の最新の機能と改善点について説明します。'
feature-set: Commerce
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: 78e270c4fffe0b1c0fef621dd5bb24295b34ced6
workflow-type: tm+mt
source-wordcount: '2590'
ht-degree: 0%

---

# リリースノート

次のリリースノートには、[!DNL Adobe Commerce as a Cloud Service]の更新が含まれています。

>[!NOTE]
>
>Adobe Commerce オンプレミスまたはAdobe Commerce オンクラウドインフラストラクチャを使用している場合は、[Adobe Commerce リリースノート &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/release/notes/overview)を参照してください。

## 2026年4月 – リリース #2 {#latest}

[!BADGE 本番]{type=Neutral tooltip="リストされている項目は、現在、実稼動環境で使用できます。"}

<!-- [!BADGE Sandbox]{type=Caution tooltip="The items listed are currently only available in Sandbox environments. Adobe makes new releases available in Sandbox environments first to provide time to test upcoming changes before the release is available on Production environments."} -->

2026年4月16日（PT）に実稼動環境に公開されたアイテムは次のとおりです。

>[!BEGINSHADEBOX]

### Webhookによるカスタム見積もり合計の実装

`plugin.magento.out_of_process_totals_collector.api.get_total_modifications.execute` [Webhook](https://developer.adobe.com/commerce/extensibility/webhooks/)が[!DNL Adobe Commerce as a Cloud Service]で利用できるようになりました。 プロセス外の拡張性を使用して、カスタム見積もり合計の変更を実装する場合に使用します。<!-- CEXT-5896 -->

### 再利用可能なメールリマインダールール（実験的）

>[!IMPORTANT]
>
>この機能は実験的な機能であり、Adobe Commerce カスタマーサクセスマネージャーに連絡するか、サポートチケットを作成して有効にする必要があります。

[電子メールリマインダールール &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/marketing/communications/email-reminders/email-reminder-rules#rule-repeatability)は、元のトリガー条件が適用されなくなった後に同じルールを顧客に再適用できる、オプションのルール再利用性設定をサポートするようになりました。

例えば、買い物かごを放棄した後、購入を完了し、後で新しい買い物かごを放棄した場合、ルールは再度トリガーできます。 この設定がないと、元のトリガーをクリアしたお客様は、同じルールの今後の一致から完全に除外されます。

### 決済サービスのトランザクションレポートを表示

[[!DNL Payment Services]](https://experienceleague.adobe.com/ja/docs/commerce/payment-services/get-started/production)が有効になっている場合、[で](../payment-services/payments-home.md) ダッシュボード UI[!DNL Commerce Admin]が利用できるようになり、支払いトランザクションの表示と管理のために[&#x200B; トランザクションレポート &#x200B;](../payment-services/reporting.md#transactions-report-view)にアクセスできるようになりました。<!-- PAY-6510 -->

### 機能強化とバグ修正

このリリースには、次の選択した機能強化、最適化、およびバグ修正が含まれています。

* 管理UI SDKで大規模な共有カタログを使用する際に発生する可能性がある、共有カタログ割り当て会社ページの500 エラーを修正しました。<!-- CCSAAS-4783 -->

* 顧客が会社に割り当てられる前に注文が行われた場合、会社の顧客が自分の注文を確認できない問題を修正しました。<!-- ACCS-746 -->

{{accs-release}}

>[!ENDSHADEBOX]

## 2026年4月

[!BADGE 本番]{type=Neutral tooltip="リストされている項目は、現在、実稼動環境で使用できます。"}

2026年4月1日に実稼動環境に公開されたアイテムは次のとおりです。

>[!BEGINSHADEBOX]

### 製品へのファイルの追加

[!DNL Adobe Commerce as a Cloud Service]は、ファイルタイプの製品属性を使用して製品[にファイルを](./product-files.md)追加できるようになりました。 CSVで外部URLを指定することで、製品編集ページ、REST APIを介してプログラムでファイルを手動でアップロードしたり、一括アップロードしたりできます。<!-- ACCS-535, ACCS-565 -->

### GraphQLで価格と在庫アラートのサブスクリプション状況を確認する

新しいGraphQLのクエリ [`isSubscribedProductAlertStock`](https://developer.adobe.com/commerce/webapi/graphql/schema/products/queries/is-subscribed-product-alert-stock/){target="_blank"}と[`isSubscribedProductAlertPrice`](https://developer.adobe.com/commerce/webapi/graphql/schema/products/queries/is-subscribed-product-alert-price/){target="_blank"}により、ストアフロントで、買い物客が既に商品の在庫情報や価格情報を購読しているかどうかを判断できます。<!-- ACCS-334 -->

### 負の値をサポートする数値製品属性を作成します

新しい`numeric` [製品属性入力タイプ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/catalog/product-attributes/attributes-input-types)を使用すると、販売者は負の値をサポートする10進数属性を作成できます。<!-- ACCS-600 -->

### 1つのGraphQL リクエストで複数のフォームのreCAPTCHA設定をクエリする

[`recaptchaFormConfigs` クエリ &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/store/queries/recaptcha-form-configs/)は、1回のリクエストで複数のフォーム タイプの設定の詳細を返すことができます。<!-- ACCS-628 -->

### 新しいB2B権限ですべての会社の注文を表示する

新しい`view_all_company_orders` [会社の役割](https://developer.adobe.com/commerce/webapi/rest/b2b/roles/)により、B2B会社のお客様は、管理者ユーザーが作成した過去の注文を含め、社内のすべての注文を表示できます。<!-- ACCS-675 -->

### 機能強化とバグ修正

このリリースには、次の選択した機能強化、最適化、およびバグ修正が含まれています。

* 適用可能なカスタム属性を使用して、注文および会社REST APIの結果をフィルタリングできるようになりました。会社スコープの注文検索などのシナリオをサポートします。<!-- ACCS-633 -->

* ブラウザー開発者コンソールに表示される可能性があるエラーを解決しました。<!-- CCSAAS-4650 -->

* 注文コメントを含むゲスト注文をキャンセルする際に発生する可能性があるエラーを修正しました。<!-- ACCS-674 -->

* 多くの関連アイテムを含むグループ化された製品を購買リストに追加する際に発生する可能性があるエラーを修正しました。<!-- ACCS-627 -->

>[!ENDSHADEBOX]

## 2026年3月 – リリース #2

[!BADGE 本番]{type=Neutral tooltip="リストされている項目は、現在、実稼動環境で使用できます。"}

2026年3月24日（PT）に実稼動環境に公開されたアイテムは次のとおりです。

>[!BEGINSHADEBOX]

### ワンタイムコードを使用して顧客としてログイン

管理者は、[およびREST APIを通じて、顧客の偽装のために](https://experienceleague.adobe.com/ja/docs/commerce-admin/customers/customer-accounts/manage/login-as-customer)1回限りのコード [!DNL Commerce Admin]を生成できるようになりました。 1回限りのコードは、`generateCustomerToken`または`exchangeOtpForCustomerToken`個のGraphQLの変異を介して顧客アクセストークンと交換でき、出品者が支援するショッピング シナリオのパスワードなし「顧客としてログイン」フローを有効にします。<!-- ACCS-404 -->

APIを使用してこの機能を実装する方法については、[REST API](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/login-as-customer/)および[GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/)のドキュメントを参照してください。

### REST APIによるギフトカードアカウントの管理

[&#x200B; ギフトカードアカウント &#x200B;](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/gift-card-accounts/)は、REST APIを通じて作成、更新、削除、およびクエリできるようになりました。 さらに、JSON一括読み込みサポートは`/V1/import/json` エンドポイントを通じて利用でき、サードパーティ統合でギフトカードをプログラムで同期できるようになります。<!-- ACCS-476 -->

### REST APIを介したトランザクションメールのトリガー

新しいREST API エンドポイント （`POST /V1/custom-email/send`）を使用すると、電子メールテンプレート ID、受信者メール、テンプレート変数を指定して、必要に応じてトランザクションメール [を](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/custom-email/)トリガーできます。 APIは、複雑なメールコンテンツのテンプレート変数として、ネストされた配列をサポートしています。<!-- ACCS-325, ACCS-481 -->

### すぐに使用できる送料無料のget-rates webhookを購入する

`plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` Webhookは、[!DNL Adobe Commerce as a Cloud Service]のAdmin Webhook リストで利用できるようになりました。 [&#x200B; カスタム配送方法](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#shipping-methods)の実装に使用します。<!-- ACCS-478 -->

### 製品属性を使用したPDFやその他のファイルのアップロード

新しい「ファイル」 [属性入力タイプ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/catalog/product-attributes/attributes-input-types)を使用すると、PDFなどのファイルを個々の製品にアップロードできる属性セットを作成できます。 [!UICONTROL **Stores**] > [!UICONTROL **Configuration**] > [!UICONTROL _Catalog_] > [!UICONTROL **製品ファイル属性**]&#x200B;に移動して、許可されたファイル拡張子と最大ファイルサイズを設定できます。<!-- ACCS-535, ACCS-565 -->

### 会社のカスタム属性の設定

管理者は、[!DNL Commerce Admin]の会社編集ページで、会社のカスタム属性を管理できるようになりました。 カスタム属性は、[!DNL Adobe Commerce as a Cloud Service]の管理UIから設定、保存、検証できます。

会社のカスタム属性を設定するには、[!UICONTROL **Customers**] > [!UICONTROL **Companies**]&#x200B;に移動し、会社を選択して編集ページを開きます。 次に、[!UICONTROL **カスタム属性**] タブを選択して、新しい属性を追加します。
<!-- ACCS-294 -->

### GraphQLで価格と在庫のアラートを購読する

EDS ストアフロントが[価格と在庫アラート &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/inventory/configuration/product-alerts/alert-setup)で機能するようになりました。<!-- ACCS-334 -->

さらに、価格と在庫アラートを購読および購読解除するための新しいGraphQLの突然変異がいくつかあります。

+++新しいGraphQL変異

```graphql
mutation {
  subscribeProductAlertStock(input: { sku: "ADB111" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertStock(input: { sku: "ADB111" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertStockAll {
    success
    message
  }
}
```

```graphql
mutation {
  subscribeProductAlertPrice(input: { sku: "ADB112" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertPrice(input: { sku: "ADB115" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertPriceAll {
    success
    message
  }
}
```

+++

### 機能強化とバグ修正

このリリースには、次の選択した機能強化、最適化、およびバグ修正が含まれています。

* [!UICONTROL Sales] > [!UICONTROL View Orders]会社の役割が期待どおりに機能するようになりました。<!-- ACCS-604 -->

* `last_login_at`の顧客拡張機能の属性がREST APIを通じて利用できるようになりました。これにより、統合は各顧客の最新のログイン日を取得できるようになります。<!-- ACCS-555 -->

* [!DNL AEM Assets]統合フォームの提案に関する問題を修正しました。<!-- ACCS-209 -->

* 共有カタロググリッドで一括会社の割り当てと割り当て解除アクションがエラーを引き起こす可能性がある問題を修正しました。<!-- CCSAAS-4614 -->

* 同じ商品が異なる数量またはカスタム価格で再びカートに追加されたときに、カスタムカートの価格が上書きされる問題を修正しました。<!-- ACCS-529 -->

* リクエストリスト項目のUIDが、買い物かごおよびウィッシュリスト項目のUIDと一致するようになりました。<!-- ACCS-349 -->

* 大規模な共有カタログで発生する可能性がある製品編集ページのタイムアウトを修正しました。<!-- CCSAAS-4657 -->

* GET `/V1/directory/countries`およびGET `/V1/directory/countries/:countryId`のREST API エンドポイントを管理者統合に対して再度有効にし、クライアントが有効な国と地域のデータを検索できるようにしました。<!-- ACCS-518 -->

* ユーザーが大規模な共有カタログを持っている場合にREST APIで発生する可能性があるタイムアウトの問題を修正しました。<!-- ACCS-4657 -->

* ブロックされたB2B企業が引き続き商品をカートに追加できる問題を修正しました。<!-- ACCS-552 -->

* お客様または会社のグリッドに大量のデータがある場合、書き出しボタンを使用してエラーを防止できなくなります。<!-- ACCS-320 -->

* 添付ファイルサイズが正しく表示されない問題を修正しました。<!-- ACCS-566 -->

* [!DNL Commerce Admin]で「ファイル」属性タイプを作成および削除する際の問題を修正しました。<!-- ACCS-605, ACCS-606 -->

>[!ENDSHADEBOX]


## 2026年3月 – リリース #1

[!BADGE 本番]{type=Neutral tooltip="リストされている項目は、現在、実稼動環境で使用できます。"}

以下の項目は、2026年3月9日に[!DNL Adobe Commerce as a Cloud Service]の実稼動環境にリリースされました。

>[!BEGINSHADEBOX]

### App BuilderのAI コーディングツールとチュートリアル

[AI コーディング開発者ツール &#x200B;](https://developer.adobe.com/commerce/extensibility/developer-agent/){target="_blank"}を使用して、新しい[!DNL App Builder] アプリケーションを作成し、既存の[!DNL Adobe Commerce]のPHP拡張機能を[!DNL App Builder] アプリケーションに変換できるようになりました。 ツールの使用方法を示すために、次のチュートリアルを利用できます。

* [チュートリアルの前提条件](./tutorials/tutorial-prerequisites.md)
* [評価拡張機能のチュートリアル](./tutorials/ratings-extension.md)
* [出荷方法の拡張機能チュートリアル](./tutorials/shipping-method-extension.md)

### 管理者からApp Builder アプリ管理にアクセス

[!DNL Commerce Admin]には、Commerce インスタンスに関連付けられた[個のアプリを管理するための統合シェルである](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}App Management[!DNL App Builder]にリンクするメニュー項目が含まれるようになりました。 この機能は、管理者UI SDKの最新アップデートによって強化されています。<!-- CEXT-5755 -->

### 要求エンティティ作成制限の変更

web サイト、実店舗、実店舗の閲覧数は、以前は50に制限されていました。 必要に応じて、[&#x200B; サポートリクエスト &#x200B;](https://experienceleague.adobe.com/home?lang=ja&support-tab=home#support)を送信して、これらの制限を変更できるようになりました。<!-- ACCS-398 -->

### 構造化されたエラーコードを使用して、ストアフロント認証メッセージをカスタマイズする

[`generateCustomerToken` GraphQLの突然変異](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/){target="_blank"}は、入力されたエラーコードをエラーメッセージとともに返すようになり、ストアフロントでエラーの理由ごとに特定のUI メッセージを表示できるようになりました。 使用可能なエラーコードは、`CUSTOMER_MISSING_EMAIL`、`CUSTOMER_MISSING_PASSWORD`、`CUSTOMER_SIGN_IN_INCORRECT_OR_LOCKED`、`CUSTOMER_ACCOUNT_NOT_CONFIRMED`および`CUSTOMER_GENERIC_ERROR`です。<!-- ACCS-301 -->

### カートやウィッシュリストが非アクティブな場合の自動メールリマインダーの送信

[電子メールリマインダーモジュール &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/marketing/communications/email-reminders/email-reminder-rules) （`Magento_Reminder`）が[!DNL Adobe Commerce as a Cloud Service]でアクティブになりました。これにより、加盟店は、カートとウィッシュリストの非アクティブな状態に基づいて顧客に電子メールをトリガーする、自動リマインダールールを作成できます。<!-- CCSAAS-4597 -->

### カテゴリ削除イベント webhookの購読

`observer.catalog_category_delete_before` Webhookが[!DNL Adobe Commerce as a Cloud Service]で利用できるようになりました。 カテゴリが削除される前にロジックを実行する場合に使用します。<!-- CEXT-5862 -->

### 登録済みの電子メールによるゲスト注文の追跡

新しいオプションのストアレベル設定では、登録済みの顧客アカウントと一致するメールアドレスを使用して注文が行われた場合、顧客は[&#x200B; ゲスト注文を追跡できます](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/point-of-purchase/checkout/checkout-guest#allow-guest-order-access-for-registered-emails)。<!-- ACCS-289 -->

### 機能強化とバグ修正

このリリースには、次の選択した機能強化、最適化、およびバグ修正が含まれています。

* 一部の組織の管理者が、テナントごとの使用権限を持たずにテナントインスタンスに誤ってアクセスする問題を修正しました。<!-- ACCS-335 -->

* 共有カタログを変更すると、ユーザーが[!DNL Commerce Admin]からログアウトする可能性がある問題を修正しました。<!-- ACCS-318 -->

* [!DNL Commerce Admin] UIで一部のWebhook フィールドが正しく表示されない問題を修正しました。<!-- CEXT-5874 -->

>[!ENDSHADEBOX]

## 2026年2月 – リリース #2

[!BADGE 本番]{type=Neutral tooltip="リストされている項目は、現在、実稼動環境で使用できます。"}

以下の項目は、2026年2月24日に[!DNL Adobe Commerce as a Cloud Service]の実稼動環境にリリースされました。

>[!BEGINSHADEBOX]

### コマースイベントを使用したコンテキストフィールドの送信

[!DNL Adobe Commerce as a Cloud Service]では、イベントペイロードで[&#x200B; コンテキストフィールド &#x200B;](https://developer.adobe.com/commerce/extensibility/events/context-fields/)がサポートされるようになりました。これにより、デフォルトでイベントに含まれていないデータを含めることができます。<!-- CEXT-5713 -->

### 新しいWebhookを使用して見積もり項目の保存イベントを購読する

`observer.sales_quote_item_save_before` Webhookが[!DNL Adobe Commerce as a Cloud Service]で利用できるようになりました。 見積もり項目を保存する前にロジックを実行する場合に使用します。<!-- ACCS-346 -->

### 機能強化とバグ修正

このリリースには、次の選択した機能強化、最適化、およびバグ修正が含まれています。

* [!DNL Commerce Admin]製品リストの表示の問題を引き起こす可能性のあるエラーを修正しました。 製品リストでは、パフォーマンスを向上させるために、表示される共有カタログの数が制限されるようになりました。<!-- CCSAAS-1242 -->

* カスタマイズ可能なギフトカードをカートに追加できない可能性があるGraphQLのエラーを修正しました。<!-- ACCS-313 -->

>[!ENDSHADEBOX]

## 2026年2月 – リリース #1

[!BADGE 本番]{type=Neutral tooltip="リストされている項目は、現在、実稼動環境で使用できます。"}

以下の項目は、2026年2月10日に[!DNL Adobe Commerce as a Cloud Service]の実稼動環境にリリースされました。

>[!BEGINSHADEBOX]

### 配送方法のカスタマイズと管理者レポートの表示

[!DNL Commerce Admin]に対して次の機能強化が行われました：

* 発送先住所のカスタム属性を含めるように、[shipping webhook ペイロード &#x200B;](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#payload)のプロセスを強化しました。 この変更により、販売者はカスタム配送方法を実装できるようになります。<!-- ACCS-235 -->

* [顧客](https://experienceleague.adobe.com/ja/docs/commerce-admin/start/reporting/customer-reports)、[&#x200B; マーケティング &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/start/reporting/marketing-reports)、[製品](https://experienceleague.adobe.com/ja/docs/commerce-admin/start/reporting/product-reports)、および[販売](https://experienceleague.adobe.com/ja/docs/commerce-admin/start/reporting/sales-reports)のレポートを含む管理者レポートへのアクセスを追加しました。<!-- CCSAAS-3085 -->

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service]で使用できないレポートは、PaaSとしてのみラベル付けされます（[!BADGE PaaSのみ]{type=Informative url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"}）。

### REST APIを使用してカスタム請求金額を取得します

請求書APIで、拡張機能の属性を使用して[&#x200B; カスタムキャプチャ金額](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/order-management/invoices#custom-capture-amounts)がサポートされるようになりました。<!-- ACCS-186, ACCS-197, ACCS-143 -->

>[!NOTE]
>
>法的な制限により、カスタムキャプチャ金額は、北米（NA）地域および支払い超過キャプチャが許可されているその他の地域でのみ使用できます。

### 機能強化とバグ修正

このリリースには、次の選択した機能強化、最適化、およびバグ修正が含まれています。

* クーポングリッドフィルターを修正して、APIまたは読み込みによって作成されたすべてのカスタムクーポンを表示しました。<!-- CCSAAS-4509 -->

* [!DNL Storefront Compatibility B2B Package]が`setNegotiableQuoteShippingAddress`に設定されている場合でも、`save_in_address_book`の突然変異が手動で入力されたアドレスを顧客のアドレス帳に保存しなかった`true`の問題を修正しました。<!-- LYNX-1031 -->

<!-- The above change will also be covered by the B2B changelog published on February 13, 2026. -->

* アセットの役割に関連するカスタム属性の[!DNL Edge Delivery Services]値が破損しているため、`no_selection`で製品画像が正しく表示されない問題を解決しました。<!-- ACAP-1206 -->

* nullの名または姓の値を持つフェデレーションユーザーアカウントがCommerce管理者にアクセスできない問題を解決しました。<!-- ACCS-200 -->

* 地域固有のIMS クライアント IDを自動的に提供することで、アセットセレクターの設定を簡素化しました。 マーチャントは、製品カテゴリ画像とアセットをマッピングするためにアセットセレクターを設定するサポートチケットを送信する必要がなくなりました。 Commerce リージョンに基づいて、専用のIMS クライアント IDが自動的に使用されるようになりました。<!-- ACCS-175 -->

* さまざまなパフォーマンスと最適化の改善。<!-- CCSAAS-4485, CCSAAS-4497, ACCS-196 -->

>[!ENDSHADEBOX]

## 「Generative AI tool deployment - internal study

[!BADGE 本番]{type=Neutral tooltip="リストされている項目は、現在、実稼動環境で使用できます。"}

以下の項目は、2026年1月20日に[!DNL Adobe Commerce as a Cloud Service]の実稼動環境にリリースされました。

>[!BEGINSHADEBOX]

### B2B ドロップイン

B2B ドロップインコンポーネントに次の変更が加えられました。

* [!DNL Commerce Storefront on Edge Delivery Services]には、[B2B ドロップインコンポーネント &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/?lang=ja)が含まれています。 次のB2B ドロップインを使用できるようになりました。

   * **[会社管理](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-management/?lang=ja)** - Adobe Commerce ストアフロントの会社プロファイル管理とロールベースの権限を有効にします。
   * **[会社スイッチャー](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-switcher/?lang=ja)** - ユーザーが関連付けられている複数の会社を切り替えるためのUI コンポーネントを提供します。
   * **[発注](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/purchase-order/?lang=ja)** - B2B トランザクションの発注ワークフロー、承認ルール、発注履歴を管理します。
   * **[見積もり管理](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/quote-management/?lang=ja)** – 見積もり要求、交渉、承認ワークフローを使用して、B2B顧客に対して交渉可能な見積もりを有効にします。
   * **[購買リスト &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/requisition-list/?lang=ja)** - リピート購入と一括注文の購買リストを作成および管理するためのツールを提供します。

* B2B Storefront互換性パッケージをリリース。 このパッケージは、[!DNL Adobe Commerce] B2B GraphQL スキーマを強化して、B2B システムの開発を改善するのに役立ちます。

<!-- 
* [!DNL Commerce Storefront on Edge Delivery Services] now includes [B2B drop-in components](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/?lang=ja). For a complete list of available B2B drop-in blocks, refer to the [storefront documentation](http://experienceleague.adobe.com/developer/commerce/storefront/merchants/b2b-commerce-blocks/).

* Released the [B2B Storefront Compatibility Package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility-b2b/?lang=ja). This package enhances the [!DNL Adobe Commerce] B2B GraphQL schema to help improve development on B2B systems. -->

### クリック可能な外部シッピングトラッカーへのリンク

カスタムトラッキング URL[を有効にして、買い物客のメールに含まれる出荷追跡番号をプレーンテキストからクリック可能なリンクに](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/delivery/shipping-settings#shipment-tracking-urls)変換します。 この機能は、USPS、UPS、FedEx、およびDHLでサポートされています。<!-- See PR #716 in commerce-admin -->

### Google reCAPTCHA Enterprise サポート

[!DNL Adobe Commerce as a Cloud Service]のストアフロントで[reCAPTCHA Enterprise](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/security/captcha/security-google-recaptcha-enterprise)がサポートされるようになりました。 この機能は、適応型リスク分析とマシンラーニング（機械学習）を使用して、自動化されたボットと人間のユーザーを正確に区別することで、高度なボット保護を実現します。 サイトのセキュリティを強化し、不正なアクティビティを防止し、迷惑メールや悪用を低減することで、信頼できるショッピング体験を維持できます。<!-- CCSAAS-4242 -->

### インスタンス固有の管理者アクセス

Admin Consoleの個々の[&#x200B; インスタンスに](./user-management.md#add-users) ユーザーのアクセス権[!DNL Adobe Commerce as a Cloud Service]を割り当てることができるようになりました。<!-- CCSAAS-4337 --><!-- See PR #332 -->

### 可観測性

[!DNL App Builder]を使用すると、[!DNL Adobe Commerce as a Cloud Service]OpenTelemetry observability[で](https://developer.adobe.com/commerce/extensibility/observability/) インスタンスをより詳細に可視化できます。これは自動的に使用できるようになりました。 OpenTelemetryは、パフォーマンスの監視、問題の迅速なトラブルシューティング、ストアフロントの最適化に役立つ指標、ログ、トレースを提供します。 この機能により、システムの健全性に関する先見的なインサイトが可能になり、顧客の信頼性を向上させます。

>[!NOTE]
>
>OpenTelemetry オブザーバビリティを使用するには、[!DNL App Builder]またはその他のプロセス外拡張機能（OOPE）製品を使用する必要があります。

### カタログ価格ルールの階層価格

[&#x200B; カタログ価格ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/catalog/products/pricing/product-price-tier#enable-tier-pricing-for-catalog-price-rules)を使用して、階層制の価格割引とカタログ ルール割引を組み合わせることができるようになりました。 この機能強化により、より動的で競争力のある価格戦略を構築し、一括購入に特典を提供すると同時に、プロモーション割引を適用することができます。 その結果、顧客を惹きつけ、注文額を増やし、コンバージョンを促進するための柔軟性が高まります。<!-- See PR #708 in commerce-admin -->

### 機能強化とバグ修正

このリリースに含まれる以下の選択された機能強化、最適化、およびバグ修正：

* S3にファイルをアップロードする際に発生する可能性があるエラーを解決しました。<!-- CCSAAS-4189 -->

* Commerce管理者にログインするか、REST APIにアクセスする際に発生する可能性がある`User is not entitled to access this instance` エラーを解決しました。<!-- CCSAAS-4324 -->

* ニュースレターテンプレートグリッドからニュースレターをプレビューまたはキューに入れる際に発生するエラーを修正しました。<!-- CCSAAS-4398 -->

* 管理者ダッシュボードの「`404` データを再読み込み&#x200B;[!UICONTROL **」ボタンをクリックしたときに発生した**] エラーを修正しました。<!-- CCSAAS-4468 -->

* [!DNL AEM Assets integration]が有効になっていて、製品に画像がある場合に、REST APIを介して製品カスタム属性を更新できない問題を解決しました。<!-- ACAP-1178 -->

* 様々なパフォーマンスと最適化の改善。<!-- CCSAAS-4255 --><!-- CCSAAS-4233 --><!-- CCSAAS-4220 --><!-- CCSAAS-4252 --><!-- CCSAAS-4330 --><!-- CCSAAS-3669 --><!-- CCSAAS-4462 -->

>[!ENDSHADEBOX]

## 2025年11月

>[!BEGINSHADEBOX]

### 機能強化

* [User management](./user-management.md) - Commerce管理者へのユーザーアクセス権を自動的に更新するように、Admin Consoleの&#x200B;**Product Admin**&#x200B;の役割を変更しました。<!-- CCSAAS-3012 -->

* [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads)および[REST](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/s3-uploads)で、事前に署名されたURLを使用して、交渉可能な見積もり添付ファイルおよびお客様とお客様のアドレスに関連付けられたファイルと画像をAmazon S3にアップロードして取得する機能を追加しました。 RESTでは、カテゴリ画像をアップロードすることもできます。<!-- CCSAAS-3250 -->

* `POST /V1/customers`および`PUT /V1/customers/{customerId}` エンドポイントを[REST API](https://developer.adobe.com/commerce/webapi/rest/reference/)に追加して、顧客を作成および更新しました。 これらのエンドポイントにはIMS認証が必要です。<!-- CCSAAS-3112 -->

* 買い物客の電子メールアドレスとワンタイムパスワード（OTP）が必要で、引き換えに顧客トークンを受け取る[`exchangeOtpForCustomerToken`の変異](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/)を追加しました。 この突然変異は、通常、顧客が電子メールまたは電話に送信されたOTPを使用して認証する必要があるシナリオで使用されます。

* 管理画面の&#x200B;[!UICONTROL **メールアドレスの保存**]&#x200B;設定画面で定義されたアドレスに`example.com`で終わる値が含まれている場合、Commerceはこのアドレスにメールを送信しません。 代わりに、電子メールが送信されなかったことがログに記録されます。 <!-- CCSAAS-3533 -->

#### カスタム注文属性

* 管理者ユーザーは、管理パネルの注文表示、編集、作成画面から直接[&#x200B; カスタム注文属性](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes)を表示および編集できるようになりました。 この機能強化により、GraphQLで作成されたカスタム注文データの管理が改善されます。<!-- CEXT-5044 -->

>[!ENDSHADEBOX]
