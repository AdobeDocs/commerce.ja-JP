---
title: テストと検証
description: テストと検証は、 [!DNL Payment Services]  機能が期待どおりに動作し、顧客に最適な支払いオプションを提供するのに役立ちます
exl-id: 95b4615e-73b0-41e8-83e2-e65a0b22f10f
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# テストと検証

[!DNL Payment Services] for [!DNL Adobe Commerce] と [!DNL Magento Open Source] を買い物客に公開する前に、実稼動環境でサンドボックス環境 _および_ をテストすることをお勧めします。 テストと検証は、[!DNL Payment Services] の機能が期待どおりに機能し、店舗と顧客に最適な支払いオプションを提供するのに役立ちます。

## サンドボックス環境でのテスト

サンドボックス環境での [!DNL Payment Services] のテストは、実際の銀行やマーチャントではなく、PayPal サンドボックスにのみ接続されるシミュレート環境ですが、重要な検証ステップです。

1. [ クレジットカードフィールド ](payments-options.md#credit-card-fields) または [PayPal 支払いボタン ](payments-options.md#paypal-smart-buttons) のいずれかを使用して、ストアからチェックアウトを成功させます。 テストのためのフェイククレジットカードの使用について詳しくは、[ 資格情報のテスト ](#testing-credentials) を参照してください。
1. 完了したばかりの注文をキャプチャ [ 支払いアクションが `Authorize and Capture`](onboard.md#set-payment-services-as-payment-method) に設定されている場合）、[ 払い戻し ](refunds.md)、または [ 無効 ](voids.md) します。 支払い処理が `Authorize and Capture` ではなく `Authorize` に設定されている場合は、注文の [ 請求書を作成 ](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"} することもできます。
1. 24～48 時間以内に、トランザクションおよびその他の情報を [ 支払いレポート ](payouts.md) で確認します。
1. 注文の詳細については、[ 注文支払いステータスレポート ](order-payment-status.md) を参照してください。

### 資格情報のテスト

サンドボックスをテストおよび検証する際は、既存のクレジットカードのアカウントに実際の料金を発生させないように、偽のクレジットカード番号を使用する必要があります。

PayPal のクレジットカードジェネレーターを使用して、テスト用に [ ランダムなクレジットカード情報を生成 ](https://www.paypal.com/us/smarthelp/article/where-can-i-find-test-credit-card-numbers-ts2157) します。

サンドボックスモードでApple Pay をテストするには：

* 偽のクレジットカードと請求情報を含む ](https://developer.apple.com/apple-pay/sandbox-testing/#create-a-sandbox-tester-account)0}Apple サンドボックステスターアカウント } を作成します。[
* [ サンドボックスドメインを登録 ](https://developer.paypal.com/docs/checkout/apm/apple-pay/#link-registeryoursandboxdomains)。

>[!NOTE]
>
>PayPal のサンドボックス支払い処理は遅いことがあり、サービスが停止することがあります。 この状況は、ライブ製品の支払い処理の速度と効率を示すものではありません。

## 実稼動環境でテスト

この機能を買い物客に公開する前に、実際のクレジットカードや銀行を使用して、実稼動環境で [!DNL Payment Services] をテストすることを強くお勧めします。 サンドボックスで [!DNL Payment Services] をテストすることは重要ですが、実稼動環境でテストすることが、[!DNL Payment Services] が期待どおりに動作することを確認するための最も簡単な方法です。

次の 2 つの方法のいずれかで、実稼動環境で [!DNL Payment Services] をテストできます。

* 買い物客から注文されないことがわかっている時間を選択します。
* 買い物客は一時的にアクセスできませんが、テスト用にアクセスできる web ストアを使用します。

実際のクレジットカードと PayPal アカウントを使用して実稼動テストを完了し、キャプチャや払い戻しを含む支払いのライフサイクル全体をテストします。 テスト中にチェックアウトと支払いのフロー全体を完了すると、ライブの買い物客が [!DNL Payment Services] の機能を使用している場合の機能の仕組みをより明確に把握できます。

また、実稼動テストで使用する支払い方法の銀行取引明細書に表示される情報が正しく、期待どおりのものであること（ビジネスの説明を含む）も確認する必要があります。

実稼動モードでApple Pay をテストするには、[ 実稼動ドメインを登録 ](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain) する必要があります。
