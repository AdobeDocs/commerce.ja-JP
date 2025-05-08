---
title: 互換性  [!DNL Payment Services]
description: ' [!DNL Payment Services]  が国で利用可能かどうか、およびAdobe Commerce版と互換性があるかどうかを説明します。'
role: User
level: Intermediate
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---


# [!DNL Payment Services] の互換性

[!DNL Payment Services] は、Adobe CommerceとMagento Open Sourceで使用できます。 [!DNL Payment Services] は、Adobe Commerce バージョン 2.4.x と互換性を持つようになりました。

## 前提条件

[!DNL Payment Services] を使用するには、まずCommerce インスタンスに接続する必要があります。 **この接続は 1 回だけ設定します**。

1. インスタンスが接続されているかどうかわからない場合は、**System** / サービス / **Commerce サービスコネクタ** に移動し、「サンドボックスキー」セクションと「実稼動キー」セクションの公開 API キーと秘密 API キーの値を確認し、「SaaS ID」セクションの「プロジェクト」フィールドと「データ空間」フィールドを確認します。 これらの値が存在する場合、インスタンスが接続されています。

1. 引き続きインスタンスを接続する必要がある場合は、[Commerce サービスコネクタ ](../landing/saas.md) ページの説明を参照してください。

   >[!TIP]
   >
   > 詳しくは、[Adobe Commerce サービスコネクタ ](https://experienceleague.adobe.com/ja/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector) チュートリアルビデオを参照してください。

1. 既にインスタンスに接続している場合は、[ オンボーディング ](onboard.md) ページに移動して次の手順を実行します。

>[!IMPORTANT]
>
> [!DNL Payment Services] の資格を持つすべてのマーチャントは、**1 つの実稼動データスペース** および **2 つのテストデータスペース** を使用できます。

## 標準と高度な [!DNL Payment Services] エクスペリエンス

[!DNL Payment Services] では、操作する国に応じて、**標準** （エクスプレスチェックアウト）および **詳細** （完全にサポートされている）支払いオプションとオンボーディングフローを提供します。

>[!NOTE]
>
> [!DNL Payment Services] は、他の [ オンボーディング中に利用可能な国 ](../payment-services/payments-options.md) 向けに [ 高速チェックアウト機能 ](../payment-services/production.md#complete-merchant-onboarding) （支払いオプションのサブセット）を提供しています。

### どの [!DNL Payment Services] のオプションが適切ですか？

>[!VIDEO](https://video.tv.adobe.com/v/3447811)

[!DNL Payment Services] 拡張機能の設定について詳しくは、[ 接続 ](connect.md) を参照してください。

>[!BEGINTABS]

>[!TAB  標準（高速チェックアウト） ]

![check](assets/icon-check.png) PayPal チェックアウト

![check](assets/icon-check.png) PayPal の「デビット」ボタンまたは「クレジットカード」ボタン

![ チェック ](assets/icon-check.png) カスタムチェックアウト設定

![ チェック ](assets/icon-check.png) 標準価格

![ チェック ](assets/icon-check.png)**XX か国で利用可能**

[![ 詳細情報 ](assets/learn-more-button.svg)](onboard.md)

>[!TAB  詳細（完全にサポート） ]

![ 小切手 ](assets/icon-check.png) デビットカード

![check](assets/icon-check.png) PayPal クレジット

![ チェック ](assets/icon-check.png) クレジットカードのフィールド

![check](assets/icon-check.png) Appleの「Pay」ボタン

![check](assets/icon-check.png) Googleの「Pay」ボタン

![check](assets/icon-check.png) PayPal 支払いボタン

![check](assets/icon-check.png) Venmo ボタン

![check](assets/icon-check.png) PayPal の「デビット」ボタンまたは「クレジットカード」ボタン

![ チェック ](assets/icon-check.png) 「後払い」ボタン

![ チェック ](assets/icon-check.png) カスタムチェックアウト設定

![ チェック ](assets/icon-check.png) カスタマイズされた価格

![ チェック ](assets/icon-check.png) （L2/L3 の価格機能 – 米国のみ）

![check](assets/icon-check.png)**米国（US）、カナダ（CA）、オーストラリア（AUS）でのみ利用可能です。 フランス（FR）、英国（UK）**

[![ 詳細情報 ](assets/learn-more-button.svg)](onboard.md)

>[!ENDTABS]

リリースおよびバージョン固有の情報について詳しくは、[ ライフサイクルポリシー ](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/lifecycle-policy.html?lang=ja) および [[!DNL Payment Services]  リリースノート ](release-notes.md) ページを参照してください。

すべての手順を取得し、オンボーディングプロセスを開始するには、[ の基本を学ぶ  [!DNL Payment Services]](onboard.md) を参照してください。

### 使用可能なクレジットカードおよび通貨

[!DNL Payment Services] は、（利用可能な [ 国の通貨を受け入れ ](#availability) す。 通貨レートの設定について詳しくは、[ 通貨設定 ](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration.html?lang=ja) を参照してください。

PayPal 製品およびサービスで利用可能な通貨および支払い方法の詳細については、以下のページを参照してください。

* [ サポートされる通貨に関するドキュメント ](https://developer.paypal.com/docs/reports/reference/paypal-supported-currencies/)。

* [ 支払い方法に関するドキュメント ](https://developer.paypal.com/docs/checkout/payment-methods/).
