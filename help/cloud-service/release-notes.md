---
title: '[!DNL Adobe Commerce as a Cloud Service] リリースノート'
description: ' [!DNL Adobe Commerce as a Cloud Service] の最新の機能と改善点について説明します。'
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: fb4c497c9efc184ffb6bd884cb2f37ad9cc87b02
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 0%

---

# リリースノート

以下のリリースノートには、[!DNL Adobe Commerce as a Cloud Service] の更新点が記載されています。

>[!NOTE]
>
>Adobe Commerce オンプレミスまたはAdobe Commerce on cloud infrastructure を使用している場合は、[Adobe Commerce リリースノート &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview) を参照してください。

## 2026 年 1 月 {#latest}

[!BADGE &#x200B; サンドボックス &#x200B;]{type=Caution tooltip="リストされた項目は、現在、サンドボックス環境でのみ使用できます。 Adobeでは、最初にサンドボックス環境で新しいリリースを使用できるようにして、リリースが実稼動環境で使用できるようになる前に、今後の変更をテストするための時間を提供します。"}

次の項目は、現在、[!DNL Adobe Commerce as a Cloud Service] のサンドボックス環境でのみ使用できます。 このリリースは、2026 年 1 月 20 日（PT）に実稼動環境に移行する予定です。

>[!BEGINSHADEBOX]

### 認証の機能強化

Adobe IMS管理者認証用のアクセストークンは、POST リクエストを通じてのみ受け入れられるようになりました。<!-- CCSAAS-4421 -->

### B2B ドロップダウン

B2B ドロップインコンポーネントに次の変更が加えられました。

* [!DNL Commerce Storefront on Edge Delivery Services] には、[B2B ドロップインコンポーネント &#x200B;](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/) が含まれるようになりました。 次の B2B ドロップダウンが使用できるようになりました。

   * **会社管理** – 会社プロファイル管理を有効にし、Adobe Commerce ストアフロントに対する役割ベースの権限を有効にします。
   * **会社スイッチャー** - ユーザーが関連付けられている複数の会社を切り替えるための UI コンポーネントを提供します。
   * **発注書** - B2B 取引の発注書ワークフロー、承認ルールおよび発注履歴を管理します。
   * **見積管理** – 見積依頼、交渉および承認ワークフローを使用して、B2B 顧客に対して交渉可能な見積を有効にします。
   * **購買依頼リスト**：繰返し購入および一括発注のための購買依頼リストを作成および管理するツールを提供します。

     >[!NOTE]
     >
     >B2B ドロップインコンポーネントに関する詳細なドキュメントは、この機能が実稼動環境に昇格した場合に利用できます。

* B2B ストアフロント互換性パッケージをリリースしました。 このパッケージは、[!DNL Adobe Commerce] B2B GraphQL スキーマを強化して、B2B システムでの開発の改善を支援します。

<!-- 
* [!DNL Commerce Storefront on Edge Delivery Services] now includes [B2B drop-in components](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/). For a complete list of available B2B drop-in blocks, refer to the [storefront documentation](http://experienceleague.adobe.com/developer/commerce/storefront/merchants/b2b-commerce-blocks/).

* Released the [B2B Storefront Compatibility Package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility-b2b/). This package enhances the [!DNL Adobe Commerce] B2B GraphQL schema to help improve development on B2B systems. -->

### 外部配送トラッカーへのクリック可能なリンク

[&#x200B; カスタムトラッキング URL を有効にする &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/delivery/shipping-settings#shipment-tracking-urls) ことで、買い物客のメールに含まれる出荷トラッキング番号をプレーンテキストからクリック可能なリンクに変換します。 この機能は、USPS、UPS、FedEx、および DHL でサポートされています。<!-- See PR #716 in commerce-admin -->

### Google reCAPTCHA Enterprise サポート

[!DNL Adobe Commerce as a Cloud Service] ストアフロントで [reCAPTCHA Enterprise](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/captcha/security-google-recaptcha-enterprise) がサポートされるようになりました。 この機能は、アダプティブリスク分析と機械学習を使用して、自動ボットから人間のユーザーを正確に区別することで、高度なボット保護を提供します。 サイトのセキュリティを強化し、詐欺行為を防ぎ、スパムや虐待を減らして、信頼できるショッピングエクスペリエンスを維持します。<!-- CCSAAS-4242 -->

### インスタンス固有の管理アクセス

Admin Console内の個々の [&#x200B; インスタンスに &#x200B;](./user-management.md#add-users) ユーザーアクセスを割り当てる [!DNL Adobe Commerce as a Cloud Service] ことができるようになりました。<!-- CCSAAS-4337 --><!-- See PR #332 -->

### 可観測性

自動的に使用可能になった [!DNL Adobe Commerce as a Cloud Service]OpenTelemetry observability[&#x200B; により、](https://developer.adobe.com/commerce/extensibility/observability/) インスタンスをより詳細に可視化します。 OpenTelemetry は、パフォーマンスの監視、問題の迅速なトラブルシューティング、ストアフロントの最適化に役立つ指標、ログおよびトレースを提供します。 この機能により、システムの正常性に関するプロアクティブなインサイトが可能になり、顧客の信頼性が向上します。

### カタログ価格ルールの階層価格

[&#x200B; カタログ価格ルール &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier#enable-tier-pricing-for-catalog-price-rules) を使用して、階層化された価格割引をカタログルール割引と組み合わせることができるようになりました。 この機能強化により、より動的で競争力のある価格戦略を作成でき、プロモーション割引を適用すると同時に一括購入にやりがいを与えることができます。 その結果、顧客を引き付け、注文価値を高め、コンバージョンを促進する柔軟性が向上します。<!-- See PR #708 in commerce-admin -->

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

* 顧客を作成および更新するために、`POST /V1/customers` エンドポイントと `PUT /V1/customers/{customerId}` エンドポイントを [REST API](https://developer.adobe.com/commerce/webapi/rest/reference/) に追加しました。 これらのエンドポイントには管理者認証が必要です。<!-- CCSAAS-3112 -->

* 買い物客のメールアドレスと 1 回限りのパスワード（OTP）を必要とし [`exchangeOtpForCustomerToken` 引き換えに顧客トークンを受け取る、](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/) ミューテーションを追加しました。 このミューテーションは、通常、顧客がメールまたは電話に送信された OTP を使用して認証する必要があるシナリオで使用されます。

* 管理者の [!UICONTROL **メールアドレスを保存**] 設定画面で定義されたアドレスに、`example.com` で終わる値が含まれている場合、Commerceはこのアドレスにメールを送信しません。 代わりに、システムはメールが送信されなかったことをログに記録します。 <!-- CCSAAS-3533 -->

#### カスタム注文属性

* 管理者ユーザーは、管理パネルの注文ビュー、編集、作成画面から直接 [&#x200B; カスタム注文属性 &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes) を表示および編集できるようになりました。 この機能強化により、GraphQLを介して作成されたカスタム注文データの管理が向上します。<!-- CEXT-5044 -->

>[!ENDSHADEBOX]
