---
title: テストと検証
description: テストと検証は、 [!DNL Payment Services]  機能が期待どおりに動作し、顧客に最適な支払いオプションを提供するのに役立ちます
exl-id: 95b4615e-73b0-41e8-83e2-e65a0b22f10f
feature: Payments, Checkout, Paas, Saas
source-git-commit: 91a4b8fa7228fb91c8ee0bf0a1623d104f061894
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---

# テストと検証

[!DNL Payment Services] for [!DNL Adobe Commerce] と [!DNL Magento Open Source] を買い物客に公開する前に、実稼動環境でサンドボックス環境 _および_ をテストすることをお勧めします。 テストと検証は、[!DNL Payment Services] の機能が期待どおりに機能し、店舗と顧客に最適な支払いオプションを提供するのに役立ちます。

## サンドボックス環境でのテスト

サンドボックス環境での [!DNL Payment Services] のテストは、実際の銀行やマーチャントではなく、PayPal サンドボックスにのみ接続されるシミュレート環境ですが、重要な検証ステップです。

1. [ クレジットカードフィールド ](payments-options.md#credit-card-fields) または [PayPal 支払いボタン ](payments-options.md#paypal-smart-buttons) のいずれかを使用して、ストアからチェックアウトを成功させます。 テストのためのフェイククレジットカードの使用について詳しくは、[ 資格情報のテスト ](#testing-credentials) を参照してください。
1. 完了したばかりの注文をキャプチャ [ 支払いアクションが `Authorize and Capture`](onboard.md#set-payment-services-as-payment-method) に設定されている場合）、[ 払い戻し ](refunds.md)、または [ 無効 ](voids.md) します。 支払い処理が [ ではなく ](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"} に設定されている場合は、注文の `Authorize` 請求書を作成 `Authorize and Capture` することもできます。
1. 24～48 時間以内に、トランザクションおよびその他の情報を [ 支払いレポート ](payouts.md) で確認します。
1. 注文の詳細については、[ 注文支払いステータスレポート ](order-payment-status.md) を参照してください。

### ローカル開発環境でのテスト

ローカル開発環境で PayPal、PayLater、Venmo の支払い方法をテストするには、インターネットからアクセスできる環境が必要です。 これらの支払い方法では、PayPal がCommerce インスタンスと通信して配送オプションを取得し、合計を計算する必要がある [ サーバーサイドの配送コールバック ](https://developer.paypal.com/docs/multiparty/checkout/standard/customize/shipping-module/) を使用します。

>[!INFO]
>
>インターネットからアクセス可能な URL がないと、発送用コールバックは機能せず、その結果、実稼動環境とは異なるチェックアウトフローが発生します。 正確な結果を得るために、常にアクセス可能な URL を使用してテストする

ローカル環境を公開するには：

1. [ngrok](https://ngrok.com/) などのトンネリングサービスを使用して、ローカル環境用の公開アクセス可能な URL を作成します。

1. ngrok URL に一致するようにCommerceのベース URL 設定を更新します。

   ```bash
   bin/magento config:set web/unsecure/base_url https://your-ngrok-url.ngrok.io/
   bin/magento config:set web/secure/base_url https://your-ngrok-url.ngrok.io/
   bin/magento cache:flush
   ```

1. PayPal、PayLater、または Venmo の支払い方法を使用してテストを完了します。

1. テストが完了したら、元のベース URL 設定を復元します。

エンドポイントの応答時間が 5 秒未満の場合、PayPal はポップアップにエラーメッセージを表示します。

#### Apple ペイ ローカル開発

Apple Pay では、ローカル開発のために追加の設定が必要です。 Apple Pay は、ドメイン登録を使用して、サイトがApple Pay の支払いを受け入れる権限を持っていることを確認します。 つまり、Appleがドメインにアクセスして、ドメイン検証ファイルを `/.well-known/apple-developer-merchantid-domain-association` で検証できる必要があります。

ローカル開発には、お使いの環境が次の要件を満たしている必要があります。

* **公開アクセス可能** なAppleは、インターネットからドメインに到達できる必要があります。
* **HTTPS プロトコル**、Apple Pay はセキュリティで保護された接続でのみ機能します。

[ngrok](https://ngrok.com/) のようなトンネリング サービスを使用すると、両方の要件が満たされます。 上記のように ngrok を設定した後、[ngrok](https://developer.paypal.com/docs/checkout/apm/apple-pay/#link-registeryoursandboxdomains) URL を使用して **サンドボックスドメインを登録** し、PayPal にアクセスします。

### 資格情報のテスト

サンドボックスをテストおよび検証する際は、既存のクレジットカードのアカウントに実際の料金を発生させないように、偽のクレジットカード番号を使用する必要があります。

PayPal のクレジットカードジェネレーターを使用して、テスト用に [ ランダムなクレジットカード情報を生成 ](https://www.paypal.com/us/smarthelp/article/where-can-i-find-test-credit-card-numbers-ts2157) します。

サンドボックスモードでApple Pay をテストするには：

* 偽のクレジットカードと請求情報を含む [0}Apple サンドボックステスターアカウント } を作成します。](https://developer.apple.com/apple-pay/sandbox-testing/#create-a-sandbox-tester-account)
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

### 実稼動環境でのApple Pay のテスト

実稼動モードでApple Pay をテストするには、[ 実稼動ドメインを登録 ](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain) する必要があります。
