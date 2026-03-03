---
title: '[!DNL Adobe Commerce as a Cloud Service] リリースノート'
description: ' [!DNL Adobe Commerce as a Cloud Service] の最新の機能と改善点について説明します。'
feature-set: Commerce
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: f0f667254bb8b33905543afe83f17428bc3dbdc2
workflow-type: tm+mt
source-wordcount: '1735'
ht-degree: 0%

---

# リリースノート

以下のリリースノートには、[!DNL Adobe Commerce as a Cloud Service] の更新点が記載されています。

>[!NOTE]
>
>Adobe Commerce オンプレミスまたはAdobe Commerce on cloud infrastructure を使用している場合は、[Adobe Commerce リリースノート ](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview) を参照してください。

## 2026 年 3 月 {#latest}

[!BADGE  サンドボックス ]{type=Caution tooltip="リストされた項目は、現在、サンドボックス環境でのみ使用できます。 Adobeでは、最初にサンドボックス環境で新しいリリースを使用できるようにして、リリースが実稼動環境で使用できるようになる前に、今後の変更をテストするための時間を確保します。"}

次の項目は、現在 [!DNL Adobe Commerce as a Cloud Service] のサンドボックス環境で使用でき、2026 年 3 月 9 日（PT）に実稼動環境にリリースされる予定です。

>[!BEGINSHADEBOX]

### App Builder AI コーディングツールとチュートリアル

[AI コーディング開発者ツール ](./migration/coding-tools.md) を使用して、新しい [!DNL App Builder] アプリケーションを作成し、既存の [!DNL Adobe Commerce] PHP 拡張機能を [!DNL App Builder] アプリケーションに変換できるようになりました。 ツールの使用方法を示すチュートリアルを次に示します。

* [チュートリアルの前提条件](./tutorials/tutorial-prerequisites.md)
* [評価拡張機能のチュートリアル](./tutorials/ratings-extension.md)
* [発送方法拡張のチュートリアル](./tutorials/shipping-method-extension.md)

### 管理者を通じたApp Builder アプリ管理へのアクセス

[!DNL Commerce Admin] には、Commerce インスタンスに関連付けられたアプリを管理するための統合シェルである [App Management](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"} にリンクしたメニュー項目 [!DNL App Builder] 含まれるようになりました。 この追加は、最新の管理 UI SDK アップデートを利用しています。<!-- CEXT-5755 -->

### リクエストエンティティの作成制限の変更

Web サイト、ストア、ストアビューの数の制限は、以前は 50 に制限されていました。 必要に応じて、[ サポートリクエスト ](https://experienceleague.adobe.com/home?support-tab=home#support) を送信して、これらの制限を変更できるようになりました。<!-- ACCS-398 -->

### 構造化エラーコードを使用したストアフロント認証メッセージのカスタマイズ

[`generateCustomerToken` GraphQLのミューテーションで ](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/){target="_blank"} エラーメッセージと共に、入力されたエラーコードが返されるようになりました。これにより、ストアフロントで、エラー理由に応じて特定の UI メッセージを表示できます。 使用可能なエラーコードは、`CUSTOMER_MISSING_EMAIL`、`CUSTOMER_MISSING_PASSWORD`、`CUSTOMER_SIGN_IN_INCORRECT_OR_LOCKED`、`CUSTOMER_ACCOUNT_NOT_CONFIRMED`、`CUSTOMER_GENERIC_ERROR` です。<!-- ACCS-301 -->

### 買い物かごやウィッシュリストの無操作状態に対して自動メールでリマインダーを送信

[ メールリマインダーモジュール ](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/communications/email-reminders/email-reminder-rules) （`Magento_Reminder`）が [!DNL Adobe Commerce as a Cloud Service] でアクティブになり、マーチャントは、買い物かごやウィッシュリストの無操作状態に基づいて顧客にメールをトリガーする、自動リマインダールールを作成できるようになりました。<!-- CCSAAS-4597 -->

### カテゴリ削除イベント Webhook の購読

`observer.catalog_category_delete_before` Webhook が [!DNL Adobe Commerce as a Cloud Service] で使用できるようになりました。 カテゴリが削除される前にロジックを実行する場合に使用します。<!-- CEXT-5862 -->

### 登録された E メールで行われたゲストの注文の追跡

新しいオプションのストアレベル設定（デフォルトで無効）を使用すると、マーチャントは、登録済みの顧客アカウントに一致するメールアドレスを使用して行われたゲストの注文を追跡できます。 有効にすると、登録済みのメールで行われたゲストのチェックアウト注文に引き続きアクセスできるようになり、顧客の注文履歴にも表示されます。

この機能を有効にするには、**ストア**/設定/**設定**/営業/**営業**/**ゲストのチェックアウト** に移動し、「**ゲストによる登録済みメールへの注文のアクセスを許可**」設定を `Yes` に設定します。
<!-- ACCS-289 -->

### 機能強化とバグ修正

このリリースには、選択した次の機能強化、最適化、バグ修正が含まれています。

* 一部の組織管理者が、テナントごとの使用権限を持たずに誤ってテナントインスタンスにアクセスできてしまう問題を修正しました。<!-- ACCS-335 -->

* 共有カタログに変更を加えると、ユーザーが [!DNL Commerce Admin] からログアウトされる可能性がある問題を修正しました。<!-- ACCS-318 -->

* [!DNL Commerce Admin] UI で一部の Webhook フィールドが正しく表示されない問題を修正しました。<!-- CEXT-5874 -->

### 内部（削除予定）

次のようなインフラストラクチャの改善が行われています。

* [!DNL Adobe Commerce] コアを 2.4.8-p3 から 2.4.8-p4 にアップグレードしました。<!-- CCSAAS-4588 -->

* ゲストのチェックアウトセッションの処理を修正して、買い物かごの見積もりがゲストのチェックアウトフロー全体で正しく関連付けられ、維持されるようにしました。<!-- ACCS-261 -->

* GraphQL エラーログを拡張して、例外スタックの完全なトレースをキャプチャし、デバッグ性を向上しました。<!-- ACCS-305 -->

* Company Resolver GraphQL テストスイートを CCSaaS テスト環境に移植しました。<!-- CCSAAS-2122 -->

* PAT devbox CI ビルドの管理シナリオのエラーを修正しました。<!-- ACCS-351 -->

* 製品作成シナリオを PAT トレンドビルドに追加しました。<!-- CCSAAS-4498 -->

* CCSaaS テスト環境に BundleRequisitionList GraphQL テストスイートを移植。<!-- CCSAAS-2113 -->

* CI でのGraphQL API 機能テストの実行を並列化し、フィードバック時間を短縮しました。<!-- CCSAAS-4607 -->

* README ドキュメントを更新しました。<!-- ACCS-404 -->

* CCSaaS リポジトリコンテキスト用のカーソル AI ルールを拡張しました。<!-- PR #1295 -->

* 古い移行ファイルを削除しました。<!-- PR #1296 -->

* パフォーマンスデータ生成中にテンプレート処理を無効にしました。<!-- PR #1297 -->

* Cursor ルールとMagento CLI ドキュメントを追加しました。<!-- PR #1300 -->

* 開発用にローカルデータベースヘルパースクリプトを追加しました。<!-- PR #1305 -->

* カーソルセキュリティコーディングルールが導入されました。<!-- PR #1306 -->

* 変更されたファイルに対してのみ実行するように最適化された CI 静的分析。<!-- PR #1309 -->

{{accs-release}}

>[!ENDSHADEBOX]

## 2026 年 2 月 – リリース #2

[!BADGE  実稼動 ]{type=Neutral tooltip="リストされた項目は、現在、実稼動環境で使用できます。"}

2026 年 2 月 24 日（PT）に、[!DNL Adobe Commerce as a Cloud Service] の実稼動環境にリリースされた項目は次のとおりです。

>[!BEGINSHADEBOX]

### コマースイベントを含んだコンテキストフィールドの送信

[!DNL Adobe Commerce as a Cloud Service] は、イベントペイロードで [ コンテキストフィールド ](https://developer.adobe.com/commerce/extensibility/events/context-fields/) をサポートするようになり、デフォルトでイベントに含まれていないデータを含めることができるようになりました。<!-- CEXT-5713 -->

### 新しい Webhook を使用して引用項目の保存イベントを購読

`observer.sales_quote_item_save_before` Webhook が [!DNL Adobe Commerce as a Cloud Service] で使用できるようになりました。 引用項目を保存する前にロジックを実行する場合に使用します。<!-- ACCS-346 -->

### 機能強化とバグ修正

このリリースには、選択した次の機能強化、最適化、バグ修正が含まれています。

* [!DNL Commerce Admin] 製品リストの表示に関する問題を引き起こす可能性があるエラーを修正しました。 製品リストで、表示される共有カタログの数が制限され、パフォーマンスが向上するようになりました。<!-- CCSAAS-1242 -->

* カスタマイズ可能なギフトカードを買い物かごに追加できないGraphQL エラーを修正しました。<!-- ACCS-313 -->

{{accs-release}}

>[!ENDSHADEBOX]

## 2026 年 2 月 – リリース #1

[!BADGE  実稼動 ]{type=Neutral tooltip="リストされた項目は、現在、実稼動環境で使用できます。"}

2026 年 2 月 10 日（PT）に、[!DNL Adobe Commerce as a Cloud Service] の実稼動環境にリリースされた項目は次のとおりです。

>[!BEGINSHADEBOX]

### 発送方法のカスタマイズと管理レポートの表示

[!DNL Commerce Admin] に次の機能強化が行われました。

* アウトオブプロセスの機能強化 [ 配送用 Webhook ペイロード ](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#payload) に配送先住所のカスタム属性を含めました。 この変更により、マーチャントはカスタム配送方法を実装できます。<!-- ACCS-235 -->

* [ 顧客 ](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/customer-reports)、[ マーケティング ](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/marketing-reports)、[ 製品 ](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/product-reports)、[ 販売 ](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/sales-reports) のレポートを含む、管理レポートへのアクセス権が追加されました。<!-- CCSAAS-3085 -->

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service] で使用できないレポートには、「PaaS のみ」のラベルが付けられます（[!BADGE PaaS のみ ]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeが管理する PaaS インフラストラクチャ）およびオンプレミスプロジェクトにのみ適用されます。"}）。

### REST API を使用したカスタム請求書金額のキャプチャ

請求書 API では、拡張機能属性を使用して [ カスタムキャプチャ金額 ](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#custom-capture-amounts) をサポートするようになりました。<!-- ACCS-186, ACCS-197, ACCS-143 -->

>[!NOTE]
>
>法的な制限により、カスタムキャプチャ金額は、北米（NA）地域および支払い超過キャプチャが許可されているその他の地域でのみ利用できます。

### 機能強化とバグ修正

このリリースには、選択した次の機能強化、最適化、バグ修正が含まれています。

* クーポングリッドフィルターを修正して、API または読み込みによって作成されたすべてのカスタムクーポンを表示するようにしました。<!-- CCSAAS-4509 -->

* [!DNL Storefront Compatibility B2B Package] が `setNegotiableQuoteShippingAddress` に設定されている場合でも、`save_in_address_book` のミューテーションが、手動で入力されたアドレスを顧客のアドレス帳に保存しなかった問題を `true` で修正しました。<!-- LYNX-1031 -->

<!-- The above change will also be covered by the B2B changelog published on February 13, 2026. -->

* アセットの役割に関連するカスタム属性の [!DNL Edge Delivery Services] 値が破損していることが原因で、`no_selection` に製品画像が正しく表示されない問題を修正しました。<!-- ACAP-1206 -->

* null の名または姓の値を持つフェデレーティッドユーザーアカウントがCommerce Admin にアクセスできない問題を修正しました。<!-- ACCS-200 -->

* 地域固有の IMS クライアント ID を自動的に提供することで、アセットセレクター設定を簡略化しました。 マーチャントは、製品カテゴリ画像をアセットにマッピングするためにアセットセレクターを設定するためのサポートチケットを送信する必要がなくなりました。 Commerce リージョンに基づいて専用の IMS クライアント ID が自動的に使用されるようになりました。<!-- ACCS-175 -->

* 様々なパフォーマンスと最適化の改善。<!-- CCSAAS-4485, CCSAAS-4497, ACCS-196 -->

{{accs-release}}

>[!ENDSHADEBOX]

## 2026 年 1 月

[!BADGE  実稼動 ]{type=Neutral tooltip="リストされた項目は、現在、実稼動環境で使用できます。"}

2026 年 1 月 20 日（PT）に、[!DNL Adobe Commerce as a Cloud Service] の実稼動環境にリリースされた項目は次のとおりです。

>[!BEGINSHADEBOX]

### B2B ドロップダウン

B2B ドロップインコンポーネントに次の変更が加えられました。

* [!DNL Commerce Storefront on Edge Delivery Services] には、[B2B ドロップインコンポーネント ](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/) が含まれるようになりました。 次の B2B ドロップダウンが使用できるようになりました。

   * **[会社管理 ](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-management/)** – 会社プロファイル管理を有効にし、Adobe Commerce ストアフロントに対する役割ベースの権限を有効にします。
   * **[会社スイッチャー ](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-switcher/)** - ユーザーが関連付けられている複数の会社を切り替えるための UI コンポーネントを提供します。
   * **[発注書 ](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/purchase-order/)** - B2B 取引の発注書ワークフロー、承認ルールおよび発注履歴を管理します。
   * **[見積管理 ](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/quote-management/)** – 見積依頼、交渉および承認ワークフローを使用して、B2B 顧客に対して交渉可能な見積を有効にします。
   * **[購買依頼リスト ](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/requisition-list/)**：繰返し購入および一括発注のための購買依頼リストを作成および管理するツールを提供します。

* B2B ストアフロント互換性パッケージをリリースしました。 このパッケージは、[!DNL Adobe Commerce] B2B GraphQL スキーマを強化して、B2B システムでの開発の改善を支援します。

<!-- 
* [!DNL Commerce Storefront on Edge Delivery Services] now includes [B2B drop-in components](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/). For a complete list of available B2B drop-in blocks, refer to the [storefront documentation](http://experienceleague.adobe.com/developer/commerce/storefront/merchants/b2b-commerce-blocks/).

* Released the [B2B Storefront Compatibility Package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility-b2b/). This package enhances the [!DNL Adobe Commerce] B2B GraphQL schema to help improve development on B2B systems. -->

### 外部配送トラッカーへのクリック可能なリンク

[ カスタムトラッキング URL を有効にする ](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/delivery/shipping-settings#shipment-tracking-urls) ことで、買い物客のメールに含まれる出荷トラッキング番号をプレーンテキストからクリック可能なリンクに変換します。 この機能は、USPS、UPS、FedEx、および DHL でサポートされています。<!-- See PR #716 in commerce-admin -->

### Google reCAPTCHA Enterprise サポート

[!DNL Adobe Commerce as a Cloud Service] ストアフロントで [reCAPTCHA Enterprise](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/captcha/security-google-recaptcha-enterprise) がサポートされるようになりました。 この機能は、アダプティブリスク分析と機械学習を使用して、自動ボットから人間のユーザーを正確に区別することで、高度なボット保護を提供します。 サイトのセキュリティを強化し、詐欺行為を防ぎ、スパムや虐待を減らして、信頼できるショッピングエクスペリエンスを維持します。<!-- CCSAAS-4242 -->

### インスタンス固有の管理アクセス

Admin Console内の個々の [ インスタンスに ](./user-management.md#add-users) ユーザーアクセスを割り当てる [!DNL Adobe Commerce as a Cloud Service] ことができるようになりました。<!-- CCSAAS-4337 --><!-- See PR #332 -->

### 可観測性

[!DNL App Builder] を使用すると、[!DNL Adobe Commerce as a Cloud Service]OpenTelemetry observability[ が自動的に使用可能になり、](https://developer.adobe.com/commerce/extensibility/observability/) インスタンスをより深く可視化できます。 OpenTelemetry は、パフォーマンスの監視、問題の迅速なトラブルシューティング、ストアフロントの最適化に役立つ指標、ログおよびトレースを提供します。 この機能により、システムの正常性に関するプロアクティブなインサイトが可能になり、顧客の信頼性が向上します。

>[!NOTE]
>
>OpenTelemetry の観測機能を使用するには、[!DNL App Builder] または他のプロセス外の拡張機能（OOPE）ソリューションを使用する必要があります。

### カタログ価格ルールの階層価格

[ カタログ価格ルール ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier#enable-tier-pricing-for-catalog-price-rules) を使用して、階層化された価格割引をカタログルール割引と組み合わせることができるようになりました。 この機能強化により、より動的で競争力のある価格戦略を作成し、プロモーションの割引を適用しながら、一括購入に報いることができます。 その結果、顧客を引き付け、注文価値を高め、コンバージョンを促進する柔軟性が向上します。<!-- See PR #708 in commerce-admin -->

### 機能強化とバグ修正

このリリースに含まれる、選択した次の機能強化、最適化、バグ修正は次のとおりです。

* ファイルを S3 にアップロードする際に発生する可能性があるエラーを修正しました。<!-- CCSAAS-4189 -->

* Commerce管理者にログインする際や REST API にアクセスする際に発生する可能性がある `User is not entitled to access this instance` エラーを修正しました。<!-- CCSAAS-4324 -->

* ニュースレターテンプレートグリッドからニュースレターをプレビューまたはキューに入れる際に発生していたエラーを修正しました。<!-- CCSAAS-4398 -->

* 管理ダッシュボ `404` ドで「[!UICONTROL **データを再読み込み**] ボタンをクリックしたときに発生していたエラーを修正しました。<!-- CCSAAS-4468 -->

* [!DNL AEM Assets integration] が有効になっており、製品に画像が含まれている場合に、製品のカスタム属性が REST API を通じて更新されない問題を解決しました。<!-- ACAP-1178 -->

* 様々なパフォーマンスと最適化の改善 <!-- CCSAAS-4255 --><!-- CCSAAS-4233 --><!-- CCSAAS-4220 --><!-- CCSAAS-4252 --><!-- CCSAAS-4330 --><!-- CCSAAS-3669 --><!-- CCSAAS-4462 -->

{{accs-release}}

>[!ENDSHADEBOX]

## 2025 年 11 月

>[!BEGINSHADEBOX]

### 機能強化

* [User Management](./user-management.md) - Admin Consoleの **Product Admin** の役割を変更して、Commerce管理者へのユーザーアクセスを自動的に更新しました。<!-- CCSAAS-3012 -->

* [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads) および [REST](https://developer.adobe.com/commerce/webapi/rest/modules/s3-uploads) の事前署名済み URL を使用して、Amazon S3 に、交渉可能な見積書の添付ファイルや、顧客および顧客アドレスに関連付けられたファイルと画像をアップロードおよび取得する機能が追加されました。 REST では、カテゴリ画像をアップロードすることもできます。<!-- CCSAAS-3250 -->

* 顧客を作成および更新するために、`POST /V1/customers` エンドポイントと `PUT /V1/customers/{customerId}` エンドポイントを [REST API](https://developer.adobe.com/commerce/webapi/rest/reference/) に追加しました。 これらのエンドポイントには IMS 認証が必要です。<!-- CCSAAS-3112 -->

* 買い物客のメールアドレスと 1 回限りのパスワード（OTP）を必要とし [`exchangeOtpForCustomerToken` 引き換えに顧客トークンを受け取る、](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/) ミューテーションを追加しました。 このミューテーションは、通常、顧客がメールまたは電話に送信された OTP を使用して認証する必要があるシナリオで使用されます。

* 管理者の [!UICONTROL **メールアドレスを保存**] 設定画面で定義されたアドレスに、`example.com` で終わる値が含まれている場合、Commerceはこのアドレスにメールを送信しません。 代わりに、システムはメールが送信されなかったことをログに記録します。 <!-- CCSAAS-3533 -->

#### カスタム注文属性

* 管理者ユーザーは、管理パネルの注文ビュー、編集、作成画面から直接 [ カスタム注文属性 ](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes) を表示および編集できるようになりました。 この機能強化により、GraphQLを介して作成されたカスタム注文データの管理が向上します。<!-- CEXT-5044 -->

>[!ENDSHADEBOX]
