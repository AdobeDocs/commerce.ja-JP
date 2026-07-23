---
title: '[!DNL Adobe Commerce as a Cloud Service] リリースノート'
description: ' [!DNL Adobe Commerce as a Cloud Service]の最新の機能と改善点について説明します。'
feature-set: Commerce
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
nudge: true
autotag-review: '2026-06-18T16:04:15.842Z'
TQID: 'https://experienceleague.adobe.com/MmwdYWe5Et9m0BvtrVYNK2jiJ3fZBnUe2K6xMdIbMUk'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: ba9e5be9-7de1-4f71-a5d2-baead0e425eeid: c1256247-af4b-46d8-9dca-0c654ecfa157id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2: id: adedf3b3-e153-47a3-ae73-b5d65067b544
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: d095671a-1355-40aa-8b5f-06c33c68080bid: e1e0219c-f879-479f-8427-888ed2a6e9c2id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: b05e2183cc0e4b8352a150df9dabfc9dfdb31750
workflow-type: tm+mt
source-wordcount: 5265
ht-degree: 0%

---

# リリースノート

次のリリースノートには、[!DNL Adobe Commerce as a Cloud Service]の更新が含まれています。

>[!NOTE]
>
>Adobe Commerce オンプレミスまたはAdobe Commerce オンクラウドインフラストラクチャを使用している場合は、[Adobe Commerce リリースノート ](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview)を参照してください。

## 2026年7月 – リリース #1 {#latest}

<!-- [!BADGE Production]{type=Neutral tooltip="The items listed are currently available in Production environments."} -->

[!BADGE  サンドボックス ]{type=Caution tooltip="リストされている項目は、現在サンドボックス環境でのみ使用できます。 Adobeでは、サンドボックス環境で新しいリリースを最初に使用できるようになりました。これにより、本番環境でリリースを利用できるようになる前に、今後の変更をテストする時間を確保できます。"}

以下の項目は現在、サンドボックス環境でのみ使用でき、2026年7月28日に実稼動環境に移行する予定です。

>[!BEGINSHADEBOX]

### RESTを使用した注文の編集

>[!IMPORTANT]
>
>この機能はデフォルトで無効になっています。 有効にするには、Adobe Commerce カスタマーサクセスマネージャーにお問い合わせいただくか、サポートチケットを作成してください。

新しいREST API エンドポイントは、[!DNL Commerce Admin] [!UICONTROL **注文を編集**]&#x200B;機能をレプリケートし、統合がプログラムで注文を編集できるようにします。

| メソッド | エンドポイント | 説明 |
| --- | --- | --- |
| `POST` | `/V1/orders/{orderId}/edit/start` | 注文を新しい編集可能なカートにコピーし、カート IDを返します。 |
| `POST` | `/V1/orders/{orderId}/edit/submit` | 変更したカートを新しい注文として送信し、元の注文をキャンセルします。 |

`edit/start`を呼び出した後、標準カート REST エンドポイントを使用して返されたカートを変更し、`edit/submit`を呼び出します。 新しい注文は、カートを通じて上書きしない限り、元の注文の支払い方法を継承し、キャンセルされた元の注文のリンクされた代替品として作成されます。 両方のエンドポイントには`Magento_Sales::actions_edit` ACL リソースが必要です。<!-- ACCS-1284 -->

### 会社ごとの注文と請求書のフィルタリング

`GET /V1/orders`および`GET /V1/invoices`のREST API エンドポイントで、`company_id`および`company_name`によるフィルタリングがサポートされるようになりました。これにより、B2B統合で1回のリクエストで特定の企業の注文または請求書を取得できるようになりました。<!-- ACCS-1111, CCSAAS-5076 -->

### ファイルごとにより多くのクーポンコードをインポート

ファイルごとの一括クーポンの読み込み上限は、Adobe Commerce カスタマーサクセスマネージャーに連絡するか、サポートチケットを作成することで調整できます。<!-- CCSAAS-5176 -->

### APIを介したカスタムメールテンプレートの管理

次の新しいREST API エンドポイントを使用すると、統合で[ カスタムメールテンプレート ](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/custom-email/)のリスト、取得、作成が可能になります。

| メソッド | エンドポイント | 説明 |
| --- | --- | --- |
| `GET` | `/V1/custom-email/templates` | カスタムメールテンプレートを一覧表示し、各テンプレートのID、コード、件名、タイプを返します。 |
| `GET` | `/V1/custom-email/templates/{id}` | 本文とスタイルを含む単一のテンプレートを取得します。 |
| `POST` | `/V1/custom-email/templates` | カスタムメールテンプレートを作成し、サーバーに割り当てられたIDを返します。 |

IDを手動で検索する代わりに、`POST /V1/custom-email/send` エンドポイントで返されたテンプレート IDを使用します。

すべての`custom-email` エンドポイントには、`Marketing > Communications > Email template` [役割リソース ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/user-accounts/permissions-user-roles#step-2assign-resources)へのアクセスが必要です。<!-- CCSAAS-5089, CCSAAS-5090 -->

### REST APIを使用したフルオーダーチェーンの管理

>[!IMPORTANT]
>
>この機能は実験的な機能であり、Adobe Commerce カスタマーサクセスマネージャーに連絡するか、サポートチケットを作成して有効にする必要があります。

新しい`orderChain`REST API エンドポイントを使用すると、統合はIDを使用して注文を変更し、編集された注文のチェーン全体を自動的に解決できます。

| メソッド | エンドポイント | 説明 |
| --- | --- | --- |
| `POST` | `/V1/orderChain/{orderId}/invoice` | 注文の請求書を作成し、注文チェーン全体で請求書に品目を解決します。 |
| `POST` | `/V1/orderChain/{id}/cancel` | チェーン内の現在の注文をキャンセルします。 |
| `POST` | `/V1/orderChain/{id}/hold` | 注文を保留にします。 |
| `POST` | `/V1/orderChain/{id}/unhold` | 注文から保留を削除します。 |
| `POST` | `/V1/orderChain/{id}/emails` | 注文のメール通知を送信する。 |
| `POST` | `/V1/orderChain/{id}/comments` | 注文にコメントを追加します。 |
| `GET` | `/V1/orderChain/{id}/comments` | 注文コメントを取得します。 |
| `GET` | `/V1/orderChain/{id}/statuses` | 現在の注文ステータスを取得します。 |

請求書、出荷、クレジットメモ、返品のフィルタリングをサポートする`GET` エンドポイントで、`order_original_id`によるフィルタリングがサポートされるようになりました。 `order_original_id`でフィルタリングすると、1つの注文だけでなく、注文チェーン全体に関する詳細が返されます。 この機能をサポートするエンドポイントの例は`GET /V1/invoices`です。<!-- ACCS-1004, ACCS-1005 -->

### カスタム属性値による注文グリッドの検索

>[!IMPORTANT]
>
>この機能はデフォルトで無効になっています。 有効にするには、Adobe Commerce カスタマーサクセスマネージャーにお問い合わせいただくか、サポートチケットを作成してください。

注文カスタム属性に保存された値によって[!DNL Commerce Admin]注文グリッドをフィルタリングできるようになりました。 [!UICONTROL **カスタム属性**] フィルターは、注文グリッドフィルター行<!-- ACCS-923 -->で使用できます。

### カート商品に対してノミネートされた在庫ソースを設定します

新しい`setNominatedSourceOnCartItems` GraphQLの変異は、特定の在庫ソースをカート商品に割り当て、実店舗での受け取り（BOPIS）や実店舗からの出荷などのシナリオをサポートします。 この突然変異は`cart_id`と項目のリストを受け入れ、それぞれに`cart_item_uid`と`source_code`が付き、構造化エラーコード `UNKNOWN_SOURCE`、`SOURCE_DISABLED`、`NOT_ENOUGH_QTY`または`SKU_SOURCE_CONFLICT`が付いた`rejected_items`を返します。 カート内の各SKUは、1つのノミネートされたソースに解決され、nullまたは空の`source_code`を渡すと、ノミネーションがクリアされます。<!-- ACCS-932 -->

### リマインダールールに一致するカートのイベントの購読

新しい`observer.reminder_matched_carts` イベントは、メールリマインダールールが一致するロジックを実行し、一致したカートに関する情報を含んだ後に発行されます。 統合により、ネイティブのリマインダーメールに頼るのではなく、このイベントを購読し、マーケティングプラットフォームなどの外部システムにデータを転送することができます。<!-- CCSAAS-5173 -->

### 領域またはテンプレート別にトランザクションメールを抑制

新しい&#x200B;[!UICONTROL **電子メール抑制**]&#x200B;設定（[!UICONTROL **店舗**] > [!UICONTROL **設定**] > [!UICONTROL **Adobe サービス**] > [!UICONTROL **電子メール抑制**]）を使用すると、管理者はトランザクション電子メールの送信を選択的に停止できます。 [!DNL Commerce]機能領域（カスタマーアカウント、Order Management、返品、チェックアウト、マーケティング、B2Bなど）またはテンプレート IDの正確なリストでメールを抑制できます。<!-- ACCS-1025 -->

### 管理画面での注文変更履歴の表示

[!DNL Commerce Admin]の注文詳細ページに、元の注文と、その後の編集で作成されたすべての子注文を含む注文の完全な変更チェーンが表示されるようになりました。 加盟店は、注文間を移動したり、キャンセルされた注文の表示を切り替えたり、関連するすべての請求書、出荷、クレジットメモ、注文コメントにチェーンビュー内からアクセスしたりできます。<!-- ACCS-968 -->

>[!NOTE]
>
>この機能を有効にするには、Adobe Commerce カスタマーサクセスマネージャーにお問い合わせください。

### [!DNL AEM Assets]の同期済みアセットの表示

[!DNL AEM Assets]統合には、[!UICONTROL **Sync Status**] ページ （[!UICONTROL **Stores**] > [!UICONTROL **AEM Assets**] > [!UICONTROL **Sync Status**]）が含まれ、フィルタリング、前回の同期日などの並べ替え可能な列、失敗した同期のエラー詳細など、同期されたすべてのアセットのアセット中心のリストビューが表示されるようになりました。<!-- ACAP-1246 -->

### 機能強化とバグ修正

このリリースには、次の選択した機能強化、最適化、およびバグ修正が含まれています。

* 大規模な共有カタログは、管理者での管理が容易になり、読み込み時間が短縮され、タイムアウトの可能性も減りました。<!-- CCSAAS-4946, CCSAAS-4925, CCSAAS-1245, CCSAAS-1246 -->

* 設定可能な製品を含む注文の出荷を作成する際に発生した出荷作成エラーを修正しました。<!-- ACCS-1095 -->

* 左側のナビゲーションメニューが消える可能性がある[!DNL Commerce Admin]の問題を修正しました。<!-- ACCS-1035 -->

* 共有カタログでの割り当てと割り当て解除のパフォーマンスが向上しました。<!-- ACCS-1324, CCSAAS-5177, CCSAAS-5190, CCSAAS-5192 -->

* [!DNL AEM Assets]統合のパフォーマンスが向上しました。<!-- ACAP-1242 -->

* [!DNL Commerce Admin]の設定可能な製品にシンプルな製品SKUを追加する際に発生する可能性があるエラーを修正しました。<!-- ACCS-1132 -->

* メッセージキューが古いレコードを大量に蓄積すると、新しいメッセージの処理を停止する可能性がある問題を修正しました。<!-- ACCS-1292 -->

* 「共有カタログで使用できないSKU」エラーで管理者注文の作成が失敗する問題を修正しました。<!-- ACCS-1318 -->

* バンドル製品の作成時または編集時に発生したクラッシュを解決しました。<!-- CCSAAS-5211 -->

* 実店舗での受け取りまたは実店舗からの配送を使用する商品について、注文時に指定されたソースで在庫が予約されない問題を修正しました。<!-- ACCS-1374 -->

* 古いカスタム料金がカートクエリの応答からクリアされるようになりました。<!-- ACCS-1400 -->

* カタログの書き出し中に製品アセットの役割の属性がロケールデータを失う[!DNL AEM Assets]統合の問題を解決しました。<!-- ACCS-1401 -->

* [!DNL Dynamic Media]が有効になっていないことを示す統合を保存する際に受け取る警告を改善しました。<!-- ACAP-1298 -->

* イベントを購読する際に、イベント名とエイリアスフィールドが小文字になるように検証されるようになりました。<!-- CEXT-6164 -->

* 条件付きWebhookを保存すると、Webhook正規表現ルールパターンが検証されるようになりました。<!-- CEXT-6287 -->

{{accs-release}}

>[!ENDSHADEBOX]

## 2026年6月 – リリース #1

[!BADGE 本番]{type=Neutral tooltip="リストされている項目は、現在、実稼動環境で使用できます。"}

<!-- [!BADGE Sandbox]{type=Caution tooltip="The items listed are currently only available in Sandbox environments. Adobe makes new releases available in Sandbox environments first to provide time to test upcoming changes before the release is available on Production environments."} -->

2026年6月4日に実稼動環境に公開されたアイテムは次のとおりです。

>[!BEGINSHADEBOX]

### 管理画面でのカスタムクーポンコードの追加と編集

販売者は、手動カート価格ルールで[!DNL Commerce Admin]から直接カスタムクーポンコード ](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-coupon#method-3-custom-coupon-codes)を[作成および編集できるようになりました。 新しい「[!UICONTROL **カスタムクーポンを追加**]」ボタンは、カート価格ルールの編集時に「[!UICONTROL **クーポンコードを管理**]」セクションで使用できます。<!-- CCSAAS-4508 -->

### デフォルトキャリアとカスタムキャリアを使用して出荷を追跡

[!DNL Commerce Admin]のデフォルトおよびカスタムの配送業者に対して注文追跡が信頼性が向上し、加盟店が一貫した購入後の追跡体験を提供できるようになりました。 以前は、UPSやFedExなどの通信事業者を選択し、トラッキング IDを適用すると、トラッキングリンクが表示されない可能性がありました。この動作を復元するために加盟店の操作は必要ありません。 トラッキングリンクのサポートは、[!DNL App Builder Integration Starter Kit]で作成された[ カスタムキャリア ](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-reference/)でも利用できます。<!-- ACCS-891 -->

### 製品属性グリッドでの属性入力タイプの表示

新しい&#x200B;[!UICONTROL **属性タイプ**]&#x200B;列が（[!UICONTROL **Stores**] > _[!UICONTROL Attributes]_>[!UICONTROL **Product**]）の製品属性グリッドに表示され、拡張機能によって提供されたタイプを含む、各製品属性の入力タイプ（テキストフィールド、ドロップダウン、yes/noなど）が表示されるようになりました。 これにより、大規模な属性セットを操作する際の属性の識別と管理が容易になります。<!-- ACCS-925 -->

### カスタムメールの返信先ヘッダーをカスタマイズする

販売者は、[POST /rest/V1/custom-email/send](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/custom-email/) エンドポイントで使用される&#x200B;[!UICONTROL **Reply-To**] ヘッダーを設定できるようになりました。これにより、顧客からの返信を送信者とは別のアドレスにルーティングできます。<!-- ACCS-1037 -->

### 大規模な共有カタログ環境で、製品編集ページで階層価格を表示します

多数の共有カタログを持つマーチャントは、[!DNL Commerce Admin]の製品編集ページの読み取り専用&#x200B;[!UICONTROL **階層の価格**] タブにアクセスできるようになりました。<!-- CCSAAS-4922 -->

### 機能強化とバグ修正

このリリースには、次の選択した機能強化、最適化、およびバグ修正が含まれています。

* POST `V1/async/custom-email/send` REST エンドポイントで`UnstructuredArray`検証エラーが返される問題を修正しました。 非同期エンドポイントは、同期POST `V1/custom-email/send` エンドポイントと一貫して機能するようになりました。<!-- ACCS-921 -->

* ペイロードにカスタム属性を含めずにRESTを使用してエンティティを更新する際に、会社などのエンティティのカスタム シリアル化可能な属性が意図せずクリアされる問題を修正しました。 カスタム属性が指定されていない場合に保持されるようになりました。<!-- ACCS-946 -->

* `X-Adobe-Company` ヘッダーがリクエストに存在する場合にゲスト GraphQLのログインを妨げる「consumer is not authorized」エラーを解決しました。<!-- ACCS-949 -->

* PUT `V1/customers/companies` REST エンドポイントを介して顧客を会社に割り当てた後、[!DNL Commerce Admin]の会社を編集または削除すると、「そのようなエンティティはありません」エラーで失敗する可能性がある問題を修正しました。<!-- ACCS-856 -->

* 古い受注グリッドのステータスに関する問題を解決しました。<!-- CCSAAS-4915 -->

* ダウンロード可能な製品のサンプルおよびリンクとして添付されたファイルが、製品編集ページからアクセスしたときに`404` エラーを返す[!DNL Commerce Admin]の問題を修正しました。<!-- CCSAAS-4394 -->

* 設定可能な製品を含む注文の出荷を作成する際に発生する可能性がある「未定義の配列キー「simple_sku」エラーを修正しました。<!-- CCSAAS-4877 -->

* `guestOrderByToken` GraphQL クエリは、内部サーバーエラーではなく、形式が正しくないトークンで呼び出された場合に、より有益なエラーメッセージを返すようになりました。<!-- CCSAAS-4921 -->

* お客様の注文を読み込めなくなったときに、`customer` GraphQL クエリが、より情報の多いエラーメッセージを返すようになりました。<!-- ACCS-867 -->

* GET `V1/customers/{customerId}` REST エンドポイントが`assistance_allowed`設定フィールドを返すようになりました。<!-- USF-4132 -->

{{accs-release}}

>[!ENDSHADEBOX]

## 2026年5月 – リリース #1

[!BADGE 本番]{type=Neutral tooltip="リストされている項目は、現在、実稼動環境で使用できます。"}

2026年5月7日（PT）に実稼動環境に公開されたアイテムは次のとおりです。

>[!BEGINSHADEBOX]

### プログラマティック OTP認証用のreCAPTCHAをスキップする

新しいコンフィギュレーションオプションを使用すると、[`exchangeOtpForCustomerToken`](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/) GraphQLの変異に対するreCAPTCHA検証をスキップできます。 これにより、フォーム入力なしでワンタイムパスワード（OTP）交換がプログラムによって開始されるB2B パンチアウトワークフローが可能になり、reCAPTCHA検証が不要になります。 この機能は、2026年3月リリースで導入された[1回限りのコードログイン ](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/customer-accounts/manage/login-as-customer){target="_blank"}機能に基づいて構築されています。 reCAPTCHAが顧客ログインに対して有効になっている場合、`exchangeOtpForCustomerToken`の突然変異では、デフォルトでreCAPTCHAが引き続き必要になります。 このオプションを有効にするには、Adobe Commerce カスタマーサクセスマネージャーにお問い合わせください。<!-- ACCS-850 -->

### 部分的に請求された注文の編集

[!UICONTROL **編集**] ボタンは、部分的に請求された注文の&#x200B;[!UICONTROL **注文表示**]&#x200B;画面で利用できるようになりました。これにより、まだ処理中の注文を柔軟に変更できます。 以前は、未請求項目が残っている場合でも、請求書を含む注文を編集できませんでした。 注文の任意の項目を引き続き請求できる限り、注文を編集できます。 以前の編集制限に依存しているカスタム統合を持つマーチャントは、ワークフローをレビューする必要があります。<!-- ACCS-849 -->

### 機能強化とバグ修正

このリリースには、次の選択した機能強化、最適化、およびバグ修正が含まれています。

* `GET /V1/products` REST API リストエンドポイントで`stock_item`拡張機能の属性が返されない問題を修正しました。 これで、応答が文書化されたAPI コントラクトと一致するようになりました。<!-- ACCS-819 -->

* 電子メールのパスワードリセットリンクが404 エラーを返す問題を修正しました。<!-- ACCS-797 -->

* 日付範囲フィルターを使用する企業の注文履歴クエリのパフォーマンスが向上しました。<!-- ACCS-859 -->

* B2B企業のユーザーが、ユーザーが会社に入社する前からピア注文を確認できる問題を修正しました。<!-- ACCS-859 -->

* `trigger_recollect`が有効になっている引用符を読み込む際にREST APIのパフォーマンスに影響を与える可能性があるチェックアウトタイムアウトの問題を解決しました。<!-- CCSAAS-4904 -->

* [!DNL Commerce Admin]で注文を送信した後に発生する可能性があるページ読み込みの問題を修正しました。<!-- CCSAAS-4413 -->

* 同じタイムスタンプを持つ注文で、受注グリッドに古い注文ステータス情報が表示される場合がある問題を修正しました。<!-- CCSAAS-4890 -->

{{accs-release}}

>[!ENDSHADEBOX]

## 2026年4月 – リリース #3

[!BADGE 本番]{type=Neutral tooltip="リストされている項目は、現在、実稼動環境で使用できます。"}

2026年4月27日（PT）に実稼動環境に公開されたアイテムは次のとおりです。

>[!BEGINSHADEBOX]

### 機能強化とバグ修正

このリリースには、次の選択した機能強化、最適化、およびバグ修正が含まれています。

* 状態の割り当てで設定されたすべての注文ステータスを取得するための`GET /V1/order-statuses` REST API エンドポイントを追加しました。<!-- CEXT-6100 -->

* 注文、買い物かご、請求書、クレジットメモ、会社などのエンティティの`custom_attributes`がREST スキーマに表示されない問題を解決しました。<!-- CCSAAS-4818 -->

* 非同期バルク API コンシューマーの重複メッセージ処理エラー（`MessageLockException`）を解決しました。<!-- CCSAAS-4805 -->

* フィルターオプションで属性が有効になっている場合、製品属性の数が[!DNL Commerce Admin]製品グリッドで範囲フィルターの開始点/終了点としてレンダリングされるようになりました。<!-- ACCS-761 -->

* [!DNL AEM Assets]の使用時にカート放棄リマインダーメールで商品画像が表示されない問題を修正しました。<!-- ACCS-798 -->

* ダウンロード可能な製品にファイル、サンプル、またはリンクを追加する際に、誤った「最大アップロードサイズ」エラーが表示される問題を修正しました。<!-- ACCS-813 -->

* 複数の共有カタログに割り当てられた製品を保存するとエラーが発生する問題を修正しました。<!-- ACCS-788 -->

* 注文履歴クエリが遅くなり、多くの注文を持つ企業でデータベースのメモリ不足エラーが発生する可能性がある問題を修正しました。<!-- ACCS-808 -->

* ファイルの読み込みの検証が失敗する問題を修正しました。<!-- CCSAAS-4364 -->

* [!DNL Adobe Commerce as a Cloud Service]管理者ではサポートされていないため、**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**の&#x200B;**[!UICONTROL Catalog]**セクションから&#x200B;**[!UICONTROL Recently Viewed/Compared Products]**設定を削除しました。<!-- ACCS-793 -->

>[!ENDSHADEBOX]

## 2026年4月 – リリース #2

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

[電子メールリマインダールール ](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/communications/email-reminders/email-reminder-rules#rule-repeatability)は、元のトリガー条件が適用されなくなった後に同じルールを顧客に再適用できる、オプションのルール再利用性設定をサポートするようになりました。

例えば、買い物かごを放棄した後、購入を完了し、後で新しい買い物かごを放棄した場合、ルールは再度トリガーできます。 この設定がないと、元のトリガーをクリアしたお客様は、同じルールの今後の一致から完全に除外されます。

### 決済サービスのトランザクションレポートを表示

[[!DNL Payment Services]](https://experienceleague.adobe.com/en/docs/commerce/payment-services/get-started/production)が有効になっている場合、[!DNL Commerce Admin]で[ ダッシュボード UI](../payment-services/payments-home.md)が利用できるようになり、支払いトランザクションの表示と管理のために[ トランザクションレポート ](../payment-services/reporting.md#transactions-report-view)にアクセスできるようになりました。<!-- PAY-6510 -->

### 機能強化とバグ修正

このリリースには、次の選択した機能強化、最適化、およびバグ修正が含まれています。

* 管理UI SDKで大規模な共有カタログを使用する際に発生する可能性がある、共有カタログ割り当て会社ページの500 エラーを修正しました。<!-- CCSAAS-4783 -->

* 顧客が会社に割り当てられる前に注文が行われた場合、会社の顧客が自分の注文を確認できない問題を修正しました。<!-- ACCS-746 -->

>[!ENDSHADEBOX]

## 2026年4月

[!BADGE 本番]{type=Neutral tooltip="リストされている項目は、現在、実稼動環境で使用できます。"}

2026年4月1日に実稼動環境に公開されたアイテムは次のとおりです。

>[!BEGINSHADEBOX]

### 製品へのファイルの追加

[!DNL Adobe Commerce as a Cloud Service]は、ファイルタイプの製品属性を使用して製品](./product-files.md)にファイルを[追加できるようになりました。 CSVで外部URLを指定することで、製品編集ページ、REST APIを介してプログラムでファイルを手動でアップロードしたり、一括アップロードしたりできます。<!-- ACCS-535, ACCS-565 -->

### GraphQLで価格と在庫アラートのサブスクリプション状況を確認する

新しいGraphQLのクエリ [`isSubscribedProductAlertStock`](https://developer.adobe.com/commerce/webapi/graphql/schema/products/queries/is-subscribed-product-alert-stock/){target="_blank"}と[`isSubscribedProductAlertPrice`](https://developer.adobe.com/commerce/webapi/graphql/schema/products/queries/is-subscribed-product-alert-price/){target="_blank"}により、ストアフロントで、買い物客が既に商品の在庫情報や価格情報を購読しているかどうかを判断できます。<!-- ACCS-334 -->

### 負の値をサポートする数値製品属性を作成します

新しい`numeric` [製品属性入力タイプ ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types)を使用すると、販売者は負の値をサポートする10進数属性を作成できます。<!-- ACCS-600 -->

### 1つのGraphQL リクエストで複数のフォームのreCAPTCHA設定をクエリする

[`recaptchaFormConfigs` クエリ ](https://developer.adobe.com/commerce/webapi/graphql/schema/store/queries/recaptcha-form-configs/)は、1回のリクエストで複数のフォーム タイプの設定の詳細を返すことができます。<!-- ACCS-628 -->

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

管理者は、[!DNL Commerce Admin]およびREST APIを通じて、顧客の偽装のために[1回限りのコード ](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/customer-accounts/manage/login-as-customer)を生成できるようになりました。 1回限りのコードは、`generateCustomerToken`または`exchangeOtpForCustomerToken`個のGraphQLの変異を介して顧客アクセストークンと交換でき、出品者が支援するショッピング シナリオのパスワードなし「顧客としてログイン」フローを有効にします。<!-- ACCS-404 -->

APIを使用してこの機能を実装する方法については、[REST API](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/login-as-customer/)および[GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/)のドキュメントを参照してください。

### REST APIによるギフトカードアカウントの管理

[ ギフトカードアカウント ](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/gift-card-accounts/)は、REST APIを通じて作成、更新、削除、およびクエリできるようになりました。 さらに、JSON一括読み込みサポートは`/V1/import/json` エンドポイントを通じて利用でき、サードパーティ統合でギフトカードをプログラムで同期できるようになります。<!-- ACCS-476 -->

### REST APIを介したトランザクションメールのトリガー

新しいREST API エンドポイント （`POST /V1/custom-email/send`）を使用すると、電子メールテンプレート ID、受信者メール、テンプレート変数を指定して、必要に応じてトランザクションメール ](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/custom-email/)を[トリガーできます。 APIは、複雑なメールコンテンツのテンプレート変数として、ネストされた配列をサポートしています。<!-- ACCS-325, ACCS-481 -->

### すぐに使用できる送料無料のget-rates webhookを購入する

`plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` Webhookは、[!DNL Adobe Commerce as a Cloud Service]のAdmin Webhook リストで利用できるようになりました。 [ カスタム配送方法](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#shipping-methods)の実装に使用します。<!-- ACCS-478 -->

### 製品属性を使用したPDFやその他のファイルのアップロード

新しい「ファイル」 [属性入力タイプ ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types)を使用すると、PDFなどのファイルを個々の製品にアップロードできる属性セットを作成できます。 [!UICONTROL **Stores**] > [!UICONTROL **Configuration**] > [!UICONTROL _Catalog_] > [!UICONTROL **製品ファイル属性**]&#x200B;に移動して、許可されたファイル拡張子と最大ファイルサイズを設定できます。<!-- ACCS-535, ACCS-565 -->

### 会社のカスタム属性の設定

管理者は、[!DNL Commerce Admin]の会社編集ページで、会社のカスタム属性を管理できるようになりました。 カスタム属性は、[!DNL Adobe Commerce as a Cloud Service]の管理UIから設定、保存、検証できます。

会社のカスタム属性を設定するには、[!UICONTROL **Customers**] > [!UICONTROL **Companies**]&#x200B;に移動し、会社を選択して編集ページを開きます。 次に、[!UICONTROL **カスタム属性**] タブを選択して、新しい属性を追加します。
<!-- ACCS-294 -->

### GraphQLで価格と在庫のアラートを購読する

EDS ストアフロントが[価格と在庫アラート ](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/product-alerts/alert-setup)で機能するようになりました。<!-- ACCS-334 -->

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

* 管理者統合のGET `/V1/directory/countries`およびGET `/V1/directory/countries/:countryId` REST API エンドポイントを再度有効にし、クライアントが有効な国と地域のデータを検索できるようにしました。<!-- ACCS-518 -->

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

[AI コーディング開発者ツール ](https://developer.adobe.com/commerce/extensibility/developer-agent/){target="_blank"}を使用して、新しい[!DNL App Builder] アプリケーションを作成し、既存の[!DNL Adobe Commerce]のPHP拡張機能を[!DNL App Builder] アプリケーションに変換できるようになりました。 ツールの使用方法を示すために、次のチュートリアルを利用できます。

* [チュートリアルの前提条件](./tutorials/tutorial-prerequisites.md)
* [評価拡張機能のチュートリアル](./tutorials/ratings-extension.md)
* [出荷方法の拡張機能チュートリアル](./tutorials/shipping-method-extension.md)

### 管理者からApp Builder アプリ管理にアクセス

[!DNL Commerce Admin]には、Commerce インスタンスに関連付けられた[!DNL App Builder]個のアプリを管理するための統合シェルである[App Management](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}にリンクするメニュー項目が含まれるようになりました。 この機能は、管理者UI SDKの最新アップデートによって強化されています。<!-- CEXT-5755 -->

### 要求エンティティ作成制限の変更

web サイト、実店舗、実店舗の閲覧数は、以前は50に制限されていました。 必要に応じて、[ サポートリクエスト ](https://experienceleague.adobe.com/home?support-tab=home#support)を送信して、これらの制限を変更できるようになりました。<!-- ACCS-398 -->

### 構造化されたエラーコードを使用して、ストアフロント認証メッセージをカスタマイズする

[`generateCustomerToken` GraphQLの突然変異](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/){target="_blank"}は、入力されたエラーコードをエラーメッセージとともに返すようになり、ストアフロントでエラーの理由ごとに特定のUI メッセージを表示できるようになりました。 使用可能なエラーコードは、`CUSTOMER_MISSING_EMAIL`、`CUSTOMER_MISSING_PASSWORD`、`CUSTOMER_SIGN_IN_INCORRECT_OR_LOCKED`、`CUSTOMER_ACCOUNT_NOT_CONFIRMED`および`CUSTOMER_GENERIC_ERROR`です。<!-- ACCS-301 -->

### カートやウィッシュリストが非アクティブな場合の自動メールリマインダーの送信

[電子メールリマインダーモジュール ](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/communications/email-reminders/email-reminder-rules) （`Magento_Reminder`）が[!DNL Adobe Commerce as a Cloud Service]でアクティブになりました。これにより、加盟店は、カートとウィッシュリストの非アクティブな状態に基づいて顧客に電子メールをトリガーする、自動リマインダールールを作成できます。<!-- CCSAAS-4597 -->

### カテゴリ削除イベント webhookの購読

`observer.catalog_category_delete_before` Webhookが[!DNL Adobe Commerce as a Cloud Service]で利用できるようになりました。 カテゴリが削除される前にロジックを実行する場合に使用します。<!-- CEXT-5862 -->

### 登録済みの電子メールによるゲスト注文の追跡

新しいオプションのストアレベル設定では、登録済みの顧客アカウントと一致するメールアドレスを使用して注文が行われた場合、顧客は[ ゲスト注文を追跡できます](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/checkout/checkout-guest#allow-guest-order-access-for-registered-emails)。<!-- ACCS-289 -->

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

[!DNL Adobe Commerce as a Cloud Service]では、イベントペイロードで[ コンテキストフィールド ](https://developer.adobe.com/commerce/extensibility/events/context-fields/)がサポートされるようになりました。これにより、デフォルトでイベントに含まれていないデータを含めることができます。<!-- CEXT-5713 -->

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

* 発送先住所のカスタム属性を含めるように、[shipping webhook ペイロード ](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#payload)のプロセスを強化しました。 この変更により、販売者はカスタム配送方法を実装できるようになります。<!-- ACCS-235 -->

* [顧客](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/customer-reports)、[ マーケティング ](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/marketing-reports)、[製品](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/product-reports)、および[販売](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/sales-reports)のレポートを含む管理者レポートへのアクセスを追加しました。<!-- CCSAAS-3085 -->

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service]で使用できないレポートは、PaaSとしてのみラベル付けされます（[!BADGE PaaSのみ]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"}）。

### REST APIを使用してカスタム請求金額を取得します

請求書APIで、拡張機能の属性を使用して[ カスタムキャプチャ金額](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#custom-capture-amounts)がサポートされるようになりました。<!-- ACCS-186, ACCS-197, ACCS-143 -->

>[!NOTE]
>
>法的な制限により、カスタムキャプチャ金額は、北米（NA）地域および支払い超過キャプチャが許可されているその他の地域でのみ使用できます。

### 機能強化とバグ修正

このリリースには、次の選択した機能強化、最適化、およびバグ修正が含まれています。

* クーポングリッドフィルターを修正して、APIまたは読み込みによって作成されたすべてのカスタムクーポンを表示しました。<!-- CCSAAS-4509 -->

* `save_in_address_book`が`true`に設定されている場合でも、`setNegotiableQuoteShippingAddress`の突然変異が手動で入力されたアドレスを顧客のアドレス帳に保存しなかった[!DNL Storefront Compatibility B2B Package]の問題を修正しました。<!-- LYNX-1031 -->

<!-- The above change will also be covered by the B2B changelog published on February 13, 2026. -->

* アセットの役割に関連するカスタム属性の`no_selection`値が破損しているため、[!DNL Edge Delivery Services]で製品画像が正しく表示されない問題を解決しました。<!-- ACAP-1206 -->

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

* [!DNL Commerce Storefront on Edge Delivery Services]には、[B2B ドロップインコンポーネント ](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/)が含まれています。 次のB2B ドロップインを使用できるようになりました。

  * **[会社管理](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-management/)** - Adobe Commerce ストアフロントの会社プロファイル管理とロールベースの権限を有効にします。
  * **[会社スイッチャー](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-switcher/)** - ユーザーが関連付けられている複数の会社を切り替えるためのUI コンポーネントを提供します。
  * **[発注](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/purchase-order/)** - B2B トランザクションの発注ワークフロー、承認ルール、発注履歴を管理します。
  * **[見積もり管理](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/quote-management/)** – 見積もり要求、交渉、承認ワークフローを使用して、B2B顧客に対して交渉可能な見積もりを有効にします。
  * **[購買リスト ](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/requisition-list/)** - リピート購入と一括注文の購買リストを作成および管理するためのツールを提供します。

* B2B Storefront互換性パッケージをリリース。 このパッケージは、[!DNL Adobe Commerce] B2B GraphQL スキーマを強化して、B2B システムの開発を改善するのに役立ちます。

<!-- 
* [!DNL Commerce Storefront on Edge Delivery Services] now includes [B2B drop-in components](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/). For a complete list of available B2B drop-in blocks, refer to the [storefront documentation](http://experienceleague.adobe.com/developer/commerce/storefront/merchants/b2b-commerce-blocks/).

* Released the [B2B Storefront Compatibility Package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility-b2b/). This package enhances the [!DNL Adobe Commerce] B2B GraphQL schema to help improve development on B2B systems. 
-->

### クリック可能な外部シッピングトラッカーへのリンク

カスタムトラッキング URL](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/delivery/shipping-settings#shipment-tracking-urls)を有効にして、買い物客のメールに含まれる出荷追跡番号をプレーンテキストからクリック可能なリンクに[変換します。 この機能は、USPS、UPS、FedEx、およびDHLでサポートされています。<!-- See PR #716 in commerce-admin -->

### Google reCAPTCHA Enterprise サポート

[!DNL Adobe Commerce as a Cloud Service]のストアフロントで[reCAPTCHA Enterprise](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/captcha/security-google-recaptcha-enterprise)がサポートされるようになりました。 この機能は、適応型リスク分析とマシンラーニング（機械学習）を使用して、自動化されたボットと人間のユーザーを正確に区別することで、高度なボット保護を実現します。 サイトのセキュリティを強化し、不正なアクティビティを防止し、迷惑メールや悪用を低減することで、信頼できるショッピング体験を維持できます。<!-- CCSAAS-4242 -->

### インスタンス固有の管理者アクセス

Admin Consoleの個々の[!DNL Adobe Commerce as a Cloud Service] インスタンスに[ ユーザーのアクセス権](./user-management.md#add-users)を割り当てることができるようになりました。<!-- CCSAAS-4337 -->
<!-- See PR #332 -->

### 可観測性

[!DNL App Builder]を使用すると、[OpenTelemetry observability](https://developer.adobe.com/commerce/extensibility/observability/)で[!DNL Adobe Commerce as a Cloud Service] インスタンスをより詳細に可視化できます。これは自動的に使用できるようになりました。 OpenTelemetryは、パフォーマンスの監視、問題の迅速なトラブルシューティング、ストアフロントの最適化に役立つ指標、ログ、トレースを提供します。 この機能により、システムの健全性に関する先見的なインサイトが可能になり、顧客の信頼性を向上させます。

>[!NOTE]
>
>OpenTelemetry オブザーバビリティを使用するには、[!DNL App Builder]またはその他のプロセス外拡張機能（OOPE）製品を使用する必要があります。

### カタログ価格ルールの階層価格

[ カタログ価格ルール ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier#enable-tier-pricing-for-catalog-price-rules)を使用して、階層制の価格割引とカタログ ルール割引を組み合わせることができるようになりました。 この機能強化により、より動的で競争力のある価格戦略を構築し、一括購入に特典を提供すると同時に、プロモーション割引を適用することができます。 その結果、顧客を惹きつけ、注文額を増やし、コンバージョンを促進するための柔軟性が高まります。<!-- See PR #708 in commerce-admin -->

### 機能強化とバグ修正

このリリースに含まれる以下の選択された機能強化、最適化、およびバグ修正：

* S3にファイルをアップロードする際に発生する可能性があるエラーを解決しました。<!-- CCSAAS-4189 -->

* Commerce管理者にログインするか、REST APIにアクセスする際に発生する可能性がある`User is not entitled to access this instance` エラーを解決しました。<!-- CCSAAS-4324 -->

* ニュースレターテンプレートグリッドからニュースレターをプレビューまたはキューに入れる際に発生するエラーを修正しました。<!-- CCSAAS-4398 -->

* 管理者ダッシュボードの「[!UICONTROL **データを再読み込み**]」ボタンをクリックしたときに発生した`404` エラーを修正しました。<!-- CCSAAS-4468 -->

* [!DNL AEM Assets integration]が有効になっていて、製品に画像がある場合に、REST APIを介して製品カスタム属性を更新できない問題を解決しました。<!-- ACAP-1178 -->

* さまざまなパフォーマンスと最適化の改善。
<!-- CCSAAS-4255 -->
<!-- CCSAAS-4233 -->
<!-- CCSAAS-4220 -->
<!-- CCSAAS-4252 -->
<!-- CCSAAS-4330 -->
<!-- CCSAAS-3669 -->
<!-- CCSAAS-4462 -->

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

* 管理者ユーザーは、管理パネルの注文表示、編集、作成画面から直接[ カスタム注文属性](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes)を表示および編集できるようになりました。 この機能強化により、GraphQLで作成されたカスタム注文データの管理が改善されます。<!-- CEXT-5044 -->

>[!ENDSHADEBOX]
