---
title: ' [!DNL Payment Services]の互換性'
description: お客様の国で [!DNL Payment Services] が利用できるかどうか、およびAdobe Commerce版との互換性について説明します。
role: User
level: Intermediate
feature: Payments, Checkout, Paas, Saas
exl-id: 4bef8429-5053-424d-806a-9e8b96295b1b
source-git-commit: c532d72cb4aa7c920af790d345cce3ae6cbd2281
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# [!DNL Payment Services]の互換性

[!DNL Payment Services]は、Adobe CommerceとMagento Open Sourceで利用できます。 [!DNL Payment Services]は、Adobe Commerce バージョン 2.4.xと互換性があります。

## 前提条件

[!DNL Payment Services]を使用するには、まずCommerce インスタンスを接続する必要があります。 **この接続は1回だけ設定しました**。

1. インスタンスが接続されているかどうかわからない場合は、**System** > Services > **Commerce Services Connector**&#x200B;に移動し、「サンドボックスキー」セクションと「実稼動キー」セクション、および「SaaS識別子」セクションの「プロジェクトとデータスペース」フィールドで公開および非公開のAPI キー値を確認します。 これらの値が存在する場合は、インスタンスが接続されます。

1. 引き続きインスタンスを接続する必要がある場合は、[Commerce Services Connector](../landing/saas.md) ページの手順を参照してください。

   >[!TIP]
   >
   > 詳しくは、[Adobe Commerce Services Connector](https://experienceleague.adobe.com/ja/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector)のチュートリアルビデオを参照してください。

1. 既にインスタンスを接続している場合は、次の手順を実行するために[&#x200B; オンボーディング &#x200B;](onboard.md) ページに移動します。

>[!IMPORTANT]
>
> [!DNL Payment Services]の資格を持つすべてのマーチャントは、**1つの実稼動データスペース**&#x200B;と&#x200B;**2つのテストデータスペース**&#x200B;を使用できます。

## 標準と高度な[!DNL Payment Services] エクスペリエンス

[!DNL Payment Services]では、お客様が事業を展開している国に応じて、**標準** （Express Checkout）および&#x200B;**詳細** （完全サポート）の支払いオプションとオンボーディングフローを提供しています。

>[!NOTE]
>
> [!DNL Payment Services]様は、オンボーディング中に他の[利用可能な国の](../payment-services/payments-options.md)Express チェックアウト機能[&#x200B; （支払いオプションのサブセット）を提供しています](../payment-services/production.md#complete-merchant-onboarding)。

### どの[!DNL Payment Services] オプションが適していますか？

>[!VIDEO](https://video.tv.adobe.com/v/3447811)

[拡張機能の設定について詳しくは、](connect.md)Connect[!DNL Payment Services]を参照してください。

>[!BEGINTABS]

>[!TAB 標準（Express チェックアウト） ]

![check](assets/icon-check.png) PayPal チェックアウト

![check](assets/icon-check.png) PayPal デビットカードまたはクレジットカードのボタン

![check](assets/icon-check.png) カスタムチェックアウト設定

![check](assets/icon-check.png)標準価格

![check](assets/icon-check.png) **XXか国で利用可能**

[![詳細情報](assets/learn-more-button.svg)](onboard.md)

>[!TAB 詳細（完全サポート） ]

![check](assets/icon-check.png) デビットカード

![check](assets/icon-check.png) PayPal クレジット

![check](assets/icon-check.png) クレジットカード情報フィールド

![check](assets/icon-check.png) Apple Pay ボタン

![check](assets/icon-check.png) Google Pay ボタン

![check](assets/icon-check.png) PayPal支払いボタン

![check](assets/icon-check.png) Venmo ボタン

![check](assets/icon-check.png) PayPal デビットカードまたはクレジットカードのボタン

![後で支払いボタンを確認](assets/icon-check.png)する

![check](assets/icon-check.png) カスタムチェックアウト設定

![check](assets/icon-check.png) カスタマイズされた価格

![check](assets/icon-check.png) （L2/L3の価格設定機能 – 米国のみ）

![check](assets/icon-check.png) **米国（米国）、カナダ（CA）、オーストラリア（AUS）でのみ利用可能です。 フランス （FR）、イギリス （UK）**

[![詳細情報](assets/learn-more-button.svg)](onboard.md)

>[!ENDTABS]

詳しいリリースおよびバージョン固有の情報については、[&#x200B; ライフサイクルポリシー](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/lifecycle-policy.html?lang=ja)および[[!DNL Payment Services]  リリースノート &#x200B;](release-notes.md)のページを参照してください。

完全な手順を入手し、オンボーディングプロセスを開始するには、[入門 [!DNL Payment Services]](onboard.md)を参照してください。

### 利用可能なクレジットカードと通貨

[!DNL Payment Services]は、使用可能な国の通貨を受け入れます。 通貨レートの設定について詳しくは、[通貨設定](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration.html?lang=ja)を参照してください。

PayPalの商品やサービスで利用可能な通貨や支払い方法について詳しくは、次のページを参照してください。

* [&#x200B; サポートされている通貨ドキュメント &#x200B;](https://developer.paypal.com/docs/reports/reference/paypal-supported-currencies/)。

* [支払い方法に関するドキュメント &#x200B;](https://developer.paypal.com/docs/checkout/payment-methods/)。
