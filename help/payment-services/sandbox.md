---
title: テストサンドボックスの設定
description: PayPal サンドボックスアカウントと管理者オンボーディングを使用して、ライブ支払い前に [!DNL Payment Services]  テストモードで実行します（Adobe Commerce オンプレミス、オンプレミス、SaaS）。
role: Admin, User
level: Intermediate
exl-id: 99c14b4e-e6cf-48f9-9546-5c0d5c71464d
feature: Payments, Checkout, Configuration, Install, Paas, Saas
source-git-commit: 2c6c812fd25feecfe5133d6623a1c814003d579c
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# テストサンドボックスの設定

サンドボックスオンボーディングを開始する前に、無料のPayPal開発者アカウントにサインアップし、（オンボーディングに使用する）マーチャントと（チェックアウトのテストに使用する）買い物客アカウントの両方を作成する必要があります。 必要に応じて、複数の開発者アカウントを作成できます。

PayPal サンドボックスアカウントでは、テストモードで[!DNL Payment Services]を使用できます。 PayPalでは、PayPal Developer Portalが生成したBusiness サンドボックスのテストアカウント、メール、パスワードをサンドボックスのオンボーディングに使用する必要があります。 *サンドボックスのオンボーディングプロセス中に別のアカウントを作成しないでください。*

## サンドボックスオンボーディング

サンドボックスのオンボーディングを完了するには：

1. [PayPal開発者アカウントページ ](https://developer.paypal.com/developer/accounts/)に移動します。
1. **[!UICONTROL Log in to Dashboard]**&#x200B;をクリックし、既存のPayPal Developer Portalが生成したBusiness サンドボックステストアカウントでログインするか、**新規登録**&#x200B;をクリックしてアカウントを作成します。
1. PayPal サンドボックスアカウントを作成します。
   1. _[!UICONTROL Testing Tools]_>**[!UICONTROL Sandbox Accounts]**に移動します。
   1. **[!UICONTROL Create account]**&#x200B;をクリックします。

      サンドボックス PayPal オンボーディングプロセス中にPayPal サンドボックスアカウントを作成した場合、メールを確認できないため、[ オンボーディングサンドボックスをリセット ](#reset-your-sandbox-account)する必要があります。

   1. アカウントタイプとして「**[!UICONTROL Business]**」を選択し、**[!UICONTROL Create]**&#x200B;をクリックします。
   1. _[!UICONTROL Sandbox Accounts]_セクションで、作成したサンドボックスアカウントの_[!UICONTROL Manage accounts]_&#x200B;列にある3つのドットをクリックします。
   1. **[!UICONTROL View/edit account]**&#x200B;をクリックします。

      ![PayPal - サンドボックスアカウントの表示/編集](assets/onboarding-viewedit-sandbox.png){width="300" zoomable="yes"}

   1. 電子メール IDとシステム生成パスワードをコピーして保存し、後で使用できるようにします。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**&#x200B;に移動します。
1. **[!UICONTROL Sandbox onboarding]**&#x200B;をクリックします。

   このオプションは、[!DNL Payment Services]のサンドボックスオンボーディングをまだ完了していない場合に表示されます。

   サンドボックスマーチャント IDが自動生成され、[設定](configure-admin.md)に入力されます。 このIDを変更または変更しないでください。

   PayPal アカウントを接続して支払いの受け入れを開始するためのPayPal ウィンドウが表示されます。

1. 手順3で生成したPayPal サンドボックスアカウントのメールアドレスとパスワード（PayPalの法人向けアカウント情報ではなく）と、お住まいの国または地域を入力します。
1. **[!UICONTROL Next]**&#x200B;をクリックします。

   ![PayPal – 支払いのためにPayPal アカウントに接続](assets/paypal-connectacct.png){width="300" zoomable="yes"}

1. 以前に保存したサンドボックスアカウントの資格情報を使用して、引き続きPayPal フローを実行します。
1. _管理者_ サイドバーで、**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**&#x200B;に移動します。

   **[!UICONTROL Sandbox onboarding]** ボタンが表示されなくなり、「サンドボックス支払い保留中」というテキストが表示されます。

PayPal サンドボックスオンボーディングが承認されると、お支払いシステムが現在サンドボックスモードであり、ライブ決済を処理していないことを示す通知が表示されます。

>[!IMPORTANT]
>
>支払いを処理するための[!DNL Payment Services]および[!DNL Adobe Commerce]の[!DNL Magento Open Source]への同意を（PayPal アカウント設定で）取り消した場合、ストア内の注文は[!DNL Payment Services]によって処理できません。 支払いサービスのホームに、失効した同意に関するアラートが表示されます。 アラートを閉じるには、**[!UICONTROL Do not show again]**&#x200B;をクリックします。

### サンドボックスアカウントをリセット

サンドボックス PayPal オンボーディングプロセス中にPayPal サンドボックスアカウントを作成した場合、メールを確認できないため、オンボーディングサンドボックスをリセットする必要があります。

サンドボックスアカウントをリセットするには：

1. **[!UICONTROL Reset sandbox]**&#x200B;をクリックします。 [PayPal ビジネス サンドボックス アカウントを作成](https://developer.paypal.com/docs/api-basics/sandbox/accounts/#create-a-business-sandbox-account)。
1. **[!UICONTROL Sandbox onboarding]**&#x200B;をクリックし、次の手順を完了します。

## 連絡先電話番号を有効にする

連絡先電話番号を使用すると、PayPalがお客様から収集する連絡先電話番号を取得できます。 PayPalは常にPayPal アカウント所有者から連絡先電話番号を収集し、IDの確認を支援し、アカウントの問題の解決やフルフィルメントプロセスの完了のために連絡を取ります。 しかし、PayPalは、売上に悪影響を与える可能性があるため、販売店から直接問い合わせ先電話番号を使用することを推奨しません。 詳しくは、[PayPalの問い合わせ先電話番号](https://www.sandbox.paypal.com/businessmanage/preferences/website)のドキュメントを参照してください。

この機能は既定では`off`です。 有効にすると、顧客がチェックアウトページ外でブランドのチェックアウトフローを完了したときに、ストア管理者は電話番号を確認できます。

>[!IMPORTANT]
>
>この設定は、他のチェックアウトフローには適用されません。

## バイヤーズ国

本番環境では、PayPalはバイヤーの位置情報を利用して、チェックアウトフローとエクスプレスフローで利用できる支払い方法を決定します。 サンドボックスモードでは位置情報はサポートされていないため、**購入者の国**&#x200B;設定を使用して購入者の場所をシミュレートし、どの支払い方法をレンダリングするかを制御します。

この設定は、Venmo （米国のみ）、Pay Later （米国および英国）、[Local Payment Methods](payments-options.md#local-payment-methods) （ヨーロッパ）などの地域固有の支払い方法をVPNなしでテストする場合に便利です。

購入者の国を設定するには：

1. _管理者_ サイドバーで、**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**に移動します。

1. 左側のパネルで、**[!UICONTROL Sales]**&#x200B;を展開し、**[!UICONTROL Payment Methods]**&#x200B;を選択します。

1. _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_セクションを展開します。

1. _[!UICONTROL Payment Services]_セクションで、_[!UICONTROL General Configuration]_ セクションを展開します。

1. **[!UICONTROL Method]**&#x200B;を`Sandbox`に設定します。

1. **[!UICONTROL Buyer's country]** ドロップダウンから目的の国を選択します。

1. **[!UICONTROL Save Config]**&#x200B;をクリックして変更を保存します。

>[!NOTE]
>
>**[!UICONTROL Buyer's country]**&#x200B;設定は、メソッドが`Sandbox`に設定されている場合にのみ表示されます。 これは実稼動環境には影響しません。

## サンドボックス環境でのテスト

この機能を買い物客に公開する前に、統合およびステージング環境にデータスペースをテストし、実稼動環境で支払いをテストすることを強くお勧めします。

詳しくは、[ テストと検証](test-validate.md)を参照してください。
