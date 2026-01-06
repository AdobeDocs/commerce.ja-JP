---
title: '[!DNL Adobe Commerce as a Cloud Service] リリースノート'
description: ' [!DNL Adobe Commerce as a Cloud Service] の最新の機能と改善点について説明します。'
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: 1ce3b6b6b94b1b4e94c0d34c081dec2884d7f0f8
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# リリースノート

以下のリリースノートには、[!DNL Adobe Commerce as a Cloud Service] の更新点が記載されています。 他の製品のリリース情報については、[Adobe Commerce Optimizer](../optimizer/release-notes.md) または [Adobe Commerce オンプレミスおよびAdobe Commerce on Cloud](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview) を参照してください。

[!DNL Adobe Commerce as a Cloud Service] には、最新バージョンのマーチャンダイジングサービス、支払いサービスおよび拡張リリースが含まれています。 次のリンクを使用して、それぞれのリリースノートを表示します。

* サービス
   * [カタログサービス](../catalog-service/release-notes.md)
   * [Live Search](../live-search/release-notes.md)
   * [支払いサービス](../payment-services/release-notes.md)
   * [製品レコメンデーション](../product-recommendations/release-notes.md)
   * [SaaS データ エクスポート](../data-export/release-notes.md)
* 拡張性
   * [ 管理 UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/release-notes/)
   * [API メッシュ ](https://developer.adobe.com/graphql-mesh-gateway/mesh/release)
   * [ イベント ](https://developer.adobe.com/commerce/extensibility/events/release-notes/)
   * [Webhook](https://developer.adobe.com/commerce/extensibility/webhooks/release-notes/)

## 2025 年 11 月

>[!BEGINSHADEBOX]

### 機能強化

* [User Management](./user-management.md) - Admin Consoleの **Product Admin** の役割を変更して、Commerce管理者へのユーザーアクセスを自動的に更新しました。<!-- CCSAAS-3012 -->

* [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads) および [REST](https://developer.adobe.com/commerce/webapi/rest/modules/s3-uploads) の事前署名済み URL を使用して、Amazon S3 に、交渉可能な見積書の添付ファイルや、顧客および顧客アドレスに関連付けられたファイルと画像をアップロードおよび取得する機能が追加されました。 REST では、カテゴリ画像をアップロードすることもできます。<!-- CCSAAS-3250 -->

* 顧客を作成および更新するために、`POST /V1/customers` エンドポイントと `PUT /V1/customers/{customerId}` エンドポイントを [REST API](https://developer.adobe.com/commerce/webapi/rest/reference/) に追加しました。 これらのエンドポイントには管理者認証が必要です。<!-- CCSAAS-3112 -->

* 買い物客のメールアドレスと 1 回限りのパスワード（OTP）を必要とし [`exchangeOtpForCustomerToken` 引き換えに顧客トークンを受け取る、](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/) ミューテーションを追加しました。 このミューテーションは、通常、顧客がメールまたは電話に送信された OTP を使用して認証する必要があるシナリオで使用されます。

* 管理者の [!UICONTROL **メールアドレスを保存**] 設定画面で定義されたアドレスに、`example.com` で終わる値が含まれている場合、Commerceはこのアドレスにメールを送信しません。 代わりに、システムはメールが送信されなかったことをログに記録します。 <!-- CCSAAS-3533 -->

#### カスタム注文属性

* 管理者ユーザーは、管理パネルの注文ビュー、編集、作成画面から直接 [ カスタム注文属性 ](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes) を表示および編集できるようになりました。 この機能強化により、GraphQLを介して作成されたカスタム注文データの管理が向上します。<!-- CEXT-5044 -->

>[!ENDSHADEBOX]
