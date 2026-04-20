---
title: 検証
description: テストと検証により、 [!DNL Payment Services] 関数が期待どおりに機能し、顧客に最適な支払いオプションを提供できるようになります
exl-id: 95b4615e-73b0-41e8-83e2-e65a0b22f10f
feature: Payments, Checkout, Paas, Saas
source-git-commit: 14c4178338859d55a7391139033d51d1aa6f7678
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---

# 検証

[!DNL Payment Services]と[!DNL Adobe Commerce]の[!DNL Magento Open Source]を買い物客に公開する前に、実稼動環境のサンドボックス環境&#x200B;_と_&#x200B;でテストすることをお勧めします。 テストと検証は、[!DNL Payment Services]機能が期待どおりに機能し、ストアと顧客に最適な支払いオプションを提供するのに役立ちます。

## サンドボックス環境でのテスト

サンドボックス環境で[!DNL Payment Services]をテストすることは、実際の銀行やマーチャントではなく、PayPal サンドボックスにのみ接続されたシミュレート環境であるにもかかわらず、重要な検証ステップです。

1. [&#x200B; クレジットカードのフィールド &#x200B;](payments-options.md#credit-card-fields)または[PayPal支払いボタン &#x200B;](payments-options.md#paypal-payment-buttons)のいずれかを使用して、ストアから正常にチェックアウトを完了します。 偽造クレジットカードをテストに使用する方法について詳しくは、[資格情報のテスト &#x200B;](#testing-credentials)を参照してください。
1. 決済アクションが[に`Authorize and Capture`](production.md#set-payment-services-as-payment-method)に設定されている場合、注文が完了したばかりの注文を[払い戻し](refunds.md)または[void](voids.md)取り込みます。 支払いアクションが[ではなく](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"}に設定されている場合、注文の請求書`Authorize`を`Authorize and Capture`作成することもできます。
1. 24 ～ 48時間以内に、[支払いレポート &#x200B;](payouts.md)でトランザクションおよびその他の情報を表示します。
1. 注文の詳細については、[注文支払い状況レポート &#x200B;](order-payment-status.md)を参照してください。

### ローカル開発環境でのテスト

ローカル開発環境でPayPal、PayLater、Venmoの支払い方法をテストするには、インターネットからアクセスできる環境が必要です。 これらの支払い方法では、[&#x200B; サーバーサイドの配送コールバック &#x200B;](https://developer.paypal.com/docs/multiparty/checkout/standard/customize/shipping-module/)を使用します。このコールバックでは、PayPalがCommerce インスタンスと通信して配送オプションを取得し、合計を計算する必要があります。

>[!INFO]
>
>インターネットにアクセス可能なURLがないと、出荷コールバックは機能せず、実稼動とは異なるチェックアウトフローが発生します。 常にアクセス可能なURLを使用してテストを行い、正確な結果を得ることができます。

ローカル環境を公開するには：

1. [ngrok](https://ngrok.com/)のようなトンネリングサービスを使用して、ローカル環境用の公開アクセス可能なURLを作成します。

1. ngrok URLに一致するように、Commerceのベース URL設定を更新します。

   ```bash
   bin/magento config:set web/unsecure/base_url https://your-ngrok-url.ngrok.io/
   bin/magento config:set web/secure/base_url https://your-ngrok-url.ngrok.io/
   bin/magento cache:flush
   ```

1. PayPal、PayLater、Venmoの決済方法を使ってテストを完了しましょう。

1. テストが完了したら、元のベース URL設定を復元します。

エンドポイントの応答時間が5秒未満の場合、PayPalはポップアップにエラーメッセージを表示します。

#### Apple有料ローカル開発

Apple Payでは、ローカル開発用に追加の設定が必要です。 Apple Payでは、ドメイン登録を使用して、サイトがApple Payの支払いを受け入れることを承認されていることを確認します。 つまり、`/.well-known/apple-developer-merchantid-domain-association`でドメイン確認ファイルを検証するには、Appleがドメインにアクセスできる必要があります。

ローカル開発を行うには、次の要件を満たす必要があります。

* **一般にアクセス可能**。Appleは、インターネットからドメインにアクセスできる必要があります。
* **HTTPS プロトコル**、Apple Payは安全な接続でのみ機能します。

[ngrok](https://ngrok.com/)のようなトンネリングサービスを使用すると、両方の要件を満たすことができます。 前述のようにngrokを設定した後、[&#x200B; サンドボックスドメイン &#x200B;](https://developer.paypal.com/docs/checkout/apm/apple-pay/#link-registeryoursandboxdomains)を&#x200B;**ngrok** URLを使用してPayPalに登録します。

### 資格情報のテスト

サンドボックスのテストと検証を行う際には、既存のクレジットカード口座に実際の料金を請求しないように、偽のクレジットカード番号を使用する必要があります。

PayPalのクレジットカード ジェネレーターを使用して、[&#x200B; テスト用にランダムなクレジットカード情報](https://www.paypal.com/us/smarthelp/article/where-can-i-find-test-credit-card-numbers-ts2157)を生成します。

Apple Payをサンドボックスモードでテストするには：

* [Apple サンドボックス テスターアカウント &#x200B;](https://developer.apple.com/apple-pay/sandbox-testing/#create-a-sandbox-tester-account)を作成し、偽のクレジットカード情報と請求情報を入力します。
* [&#x200B; サンドボックスドメインを登録](https://developer.paypal.com/docs/checkout/apm/apple-pay/#link-registeryoursandboxdomains)。

>[!NOTE]
>
>PayPalのサンドボックス決済処理は遅くなることがあり、サービスがダウンすることがあります。 この状況は、ライブ製品決済処理のスピードと効率を示すものではありません。

## 本番環境でのテスト

この機能を買い物客に公開する前に、実際のクレジットカードと銀行を使用して、実稼動環境で[!DNL Payment Services]をテストすることを強くお勧めします。 サンドボックスで[!DNL Payment Services]をテストすることは重要ですが、実稼動環境でのテストは、[!DNL Payment Services]が期待どおりに動作することを確認するための最も愚かな方法です。

実稼動環境で[!DNL Payment Services]をテストするには、次の2つの方法のいずれかを使用します。

* 買い物客が注文しない時間を選択します。
* 一時的に買い物客がアクセスできないが、テストにはアクセスできるweb ストアを利用する。

実際のクレジットカードやPayPal アカウントで本番環境のテストを完了し、キャプチャや返金を含む支払いのライフサイクル全体をテストします。 テスト中にチェックアウトと支払いフロー全体を完了すると、ライブの買い物客が使用している場合に、[!DNL Payment Services]機能がどのように機能するかを明確に把握できます。

また、本番テストで使用する支払い方法に関する銀行取引明細書に記載されている情報が正しく、期待されるものであることを確認する必要があります（ビジネスの説明を含む）。

### Apple Payの本番環境でのテスト

実稼動モードでApple Payをテストするには、[実稼動ドメインを登録](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain)する必要があります。
