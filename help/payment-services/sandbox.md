---
title: テストサンドボックスの設定
description: テストモードで使用するには、PayPal サンドボック  [!DNL Payment Services]  アカウントを使用します。
exl-id: 99c14b4e-e6cf-48f9-9546-5c0d5c71464d
feature: Payments, Checkout, Configuration, Install, Paas, Saas
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# テストサンドボックスの設定

サンドボックスオンボーディングを開始する前に、無料の PayPal 開発者アカウントに新規登録し、（オンボーディングに使用する）マーチャントアカウントと（チェックアウトのテストに使用する）買い物客アカウントの両方を作成する必要があります。 必要に応じて、複数の開発者アカウントを作成できます。

PayPal サンドボックスアカウントを使用すると、テストモードで [!DNL Payment Services] を使用できます。 PayPal では、サンドボックスのオンボーディングに、PayPal Developer Portal で生成されたビジネスサンドボックスのテストアカウント、メール、パスワードを使用する必要があります。 *サンドボックスのオンボーディングプロセス中に別のアカウントを作成しないでください。*

## サンドボックスのオンボード

サンドボックスのオンボーディングを完了するには：

1. [PayPal 開発者アカウントページ ](https://developer.paypal.com/developer/accounts/) に移動します。
1. 「**[!UICONTROL Log in to Dashboard]**」をクリックして、PayPal 開発者ポータルで生成された既存のビジネスサンドボックステストアカウントでログインするか、「**新規登録**」をクリックしてアカウントを作成します。
1. PayPal サンドボックスアカウントの作成：
   1. _[!UICONTROL Testing Tools]_/**[!UICONTROL Sandbox Accounts]**&#x200B;に移動します。
   1. 「**[!UICONTROL Create account]**」をクリックします。

      サンドボックス PayPal のオンボーディングプロセス中に PayPal サンドボックスアカウントを作成した場合は、[ オンボーディングサンドボックスをリセット ](#reset-your-sandbox-account) する必要があります。そうしないと、メールを検証できません。

   1. 「アカウントタイプ」として「**[!UICONTROL Business]**」を選択し、「**[!UICONTROL Create]**」をクリックします。
   1. 「_[!UICONTROL Sandbox Accounts]_」セクションで、作成したサンドボックスアカウントの「_[!UICONTROL Manage accounts]_」列の 3 つのドットをクリックします。
   1. 「**[!UICONTROL View/edit account]**」をクリックします。

      ![PayPal - サンドボックスアカウントの表示/編集 ](assets/onboarding-viewedit-sandbox.png){width="300" zoomable="yes"}

   1. メール ID とシステムで生成されたパスワードをコピーして、後で使用するために保存します。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL Payment Services]** に移動します。
1. 「**[!UICONTROL Sandbox onboarding]**」をクリックします。

   このオプションは、[!DNL Payment Services] のサンドボックスのオンボーディングをまだ完了していない場合に表示されます。

   サンドボックスのマーチャント ID が自動生成され、[ 設定 ](configure-admin.md) に入力されます。 この ID は変更しないでください。

   PayPal アカウントを接続して支払いの受け入れを開始するための PayPal ウィンドウが表示されます。

1. 手順 3 （PayPal ビジネスアカウント情報ではなく）で生成した PayPal サンドボックスアカウントのメールとパスワード、および国または地域を入力します。
1. 「**[!UICONTROL Next]**」をクリックします。

   ![PayPal – 支払いのために PayPal アカウントを接続します ](assets/paypal-connectacct.png){width="300" zoomable="yes"}

1. 以前に保存したサンドボックスアカウントの資格情報を使用して、PayPal フローに従い続けます。
1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL Payment Services]** に移動します。

   「**[!UICONTROL Sandbox onboarding]**」ボタンが表示されなくなり、「サンドボックスの支払いが保留中」というテキストが表示されます。

PayPal サンドボックスオンボーディングが承認されると、支払いシステムが現在サンドボックスモードにあり、ライブ支払いを処理していないことを示す通知が表示されます。

>[!IMPORTANT]
>
>（PayPal アカウントの設定で）支払い処理の [!DNL Payment Services] と [!DNL Adobe Commerce] の [!DNL Magento Open Source] に対する同意を取り消した場合、ストア内の注文は [!DNL Payment Services] で処理できません。 支払いサービス ホームに、失効した同意に関するアラートが表示されます。 アラートを解除するには、「**[!UICONTROL Do not show again]**」をクリックします。

### サンドボックスアカウントをリセット

サンドボックス PayPal のオンボーディングプロセス中に PayPal サンドボックスアカウントを作成した場合は、メールを検証できないので、オンボーディングサンドボックスをリセットする必要があります。

サンドボックスアカウントをリセットするには：

1. 「**[!UICONTROL Reset sandbox]**」をクリックします。 [PayPal ビジネスサンドボックスアカウントの作成 ](https://developer.paypal.com/docs/api-basics/sandbox/accounts/#create-a-business-sandbox-account)。
1. 「**[!UICONTROL Sandbox onboarding]**」をクリックして、次の一連の手順を完了します。

## 連絡先電話番号を有効にする

連絡先電話番号 PayPal がお客様から収集する連絡先電話番号を取得できます。 PayPal は常に PayPal アカウント所有者から連絡先の電話番号を収集して、ID を確認したり、アカウントの問題を解決したり、フルフィルメントプロセスを完了したりするために連絡を取ったりします。 ただし、PayPal は販売に悪影響を与える可能性があるため、マーチャントから直接電話番号を使用することはお勧めしません。 詳しくは、[PayPal 連絡先の電話番号を取得 ](https://www.sandbox.paypal.com/businessmanage/preferences/website) ドキュメントを参照してください。

この機能はデフォルトで `off` です。 有効にすると、顧客がチェックアウトページ外でブランド化チェックアウトフローを完了した際に、店舗管理者が電話番号を表示できます。

>[!IMPORTANT]
>
>この設定は、他のチェックアウトフローには適用されません。

## サンドボックス環境でのテスト

この機能を買い物客に公開する前に、統合およびステージング環境でテスト用データセットを使用し、実際のクレジットカードや銀行で実稼動環境で支払いをテストすることを強くお勧めします。

詳しくは [ テストと検証 ](test-validate.md) を参照してください。
