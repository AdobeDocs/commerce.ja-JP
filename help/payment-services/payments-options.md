---
title: 支払いオプション
description: 支払いオプションを設定して、ストアの顧客が使用できる方法をカスタマイズします。
exl-id: 95e648e6-6cb8-4226-b5ea-e1857212f20a
feature: Payments, Checkout, Configuration, Paas, Saas
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 0%

---

# 支払いオプション

[!DNL Adobe Commerce] と [!DNL Magento Open Source] [!DNL Payment Services] を使用すると、複数の支払いオプションを利用できます。

これらの支払いオプションは、[ ホーム設定 ](payments-home.md) または [ ストア設定 ](configure-admin.md) で設定できます（従来の支払いオプションまたはマルチストア設定の場合に推奨）。

チェックアウトプロセスの位置に応じて、支払い方法ごとに異なる動作があります。

* 製品ページ – 品目の製品ページ
* ミニ・カート – 製品がカートに追加されたときにカート・アイコンをクリックすると使用可能です。
* 買い物かご – ミニカートから _買い物かごを表示および編集_ をクリックすると使用できます。
* チェックアウト表示 – ミニカートまたは買い物かごから _チェックアウトに進む_ をクリックすると使用できます。

>[!IMPORTANT]
>
>支払 [!DNL Payment Services] 処理する前に、オンボーディングを完了する必要があります。

## 標準支払と高度な支払いの比較

[!DNL Payment Services] では、事業を行う国に応じて、**詳細** （完全にサポートされている）および **標準** （エクスプレスチェックアウト）の支払いオプションとオンボーディングフローを提供します。

* **詳細** – 利用可能なすべての [ 支払いオプション ](../payment-services/payments-options.md) は、現在の [ 完全にサポートされている国 ](../payment-services/introduction.md#availability) で利用できます。 ライブ支払いを有効にするオンボーディング中に、[ 詳細なオンボーディングオプション ](../payment-services/production.md#advanced-onboarding) を選択します。

* **Standard** – 他のサポート対象の国では、支払いオプション（エクスプレスチェックアウト）のサブセット（PayPal クレジットおよびデビットカード）を利用できます。 [ クレジットカードのフィールド ](#credit-card-fields) と [Apple Pay](#apple-pay-button) は、このオンボーディングオプションでは使用できません。 ライブ支払いを有効にするためのオンボーディング中に、[ 標準オンボーディングオプション ](../payment-services/production.md#standard-onboarding) を選択します。

高度なオンボーディングと標準オンボーディングの完了については、[ 実稼動用に  [!DNL Payment Services]  有効にする ](../payment-services/production.md#complete-merchant-onboarding) を参照してください。

## [!UICONTROL Credit Card Fields]

クレジットカードまたはデビットカードの支払い方法に対して、シンプルで安全なチェックアウトを提供で [!UICONTROL Credit Card Fields] ます。 買い物客がクレジットカードのフィールドを使用してチェックアウトする際は、名前、請求先住所、クレジットカードまたはデビットカードの情報を入力して注文を行います。 顧客の顧客情報は、購入セッション中に安全に使用され、チェックアウトフローをシームレスに導きます。

![ チェックアウト時のクレジットカードフィールド ](assets/credit-card-fields.png){width="500" zoomable="yes"}

## [!UICONTROL Digital Wallets]

### [!DNL Fastlane] ボタン

[!DNL Fastlane] は、すばやく、安全に、手間のかからないオンライン支払い方法を提供します。 **ゲストのチェックアウト** 中に、カードと配送の詳細を安全に保存して、今後はさらに迅速に購入できます。

* **検証済み買い物客への即時アクセス**：何百万人もの再訪問者を認識し、数秒でシームレスな支払いを可能にします。
* **収益の向上**：より多くの購入が完了し、コンバージョン率と承認率が向上します。
* **チェックアウトの高速化**：安全なパスワードレスのログインエクスペリエンスで摩擦を軽減します。

[!DNL Fastlane] が有効な場合、[!UICONTROL Credit Card Fields] オプションはデフォルトで無効になります。

>[!NOTE]
>
> 現在、Fastlane は米国のマーチャントに対してのみサポートされているため、[!UICONTROL 3D Secure authentication] は現在サポートされていません。

詳しくは、[Fastlane by PayPal](https://www.paypal.com/us/fastlane){target=_blank} を参照してください。

### [!DNL Apple Pay] ボタン

[!DNL Apple Pay] を使用すると、マーチャントは、Safari （マーチャントアカウントあたり最大 99 のドメイン）で安全で合理化されたチェックアウトエクスペリエンスを提供し、コンバージョンを増やすことができます。 [!DNL Apple Pay] ボタンを使用すると、顧客のiOSまたはmacOS デバイスから保存された支払い、連絡先および配送に関する詳細を自動入力し、ワンタップのチェックアウトエクスペリエンスをすばやく実現できます。

![ ミニ カートの [Apple支払い ] ボタン ](assets/applepay-button.png){width="500" zoomable="yes"}

有効にすると、製品ページ、ミニカート、買い物かご、チェックアウトの各ビューに「[!DNL Apple Pay]」ボタンが表示されます。 [!DNL Apple Pay] は、ストア設定または拡張機能のホームで設定できます。

>[!NOTE]
>
>  Apple Pay ドメイン認証証明書は、既に支払いサービスコードに含まれています。 パス `/.well-known/apple-developer-merchantid-domain-association` が 200 応答コードを返すことを確認します。 [2&rbrace;Apple Pay Domain verification](https://developer.paypal.com/docs/checkout/apm/apple-pay/#download-and-host-sandbox-domain-association-file) 証明書について詳しくは、&lbrace;PayPal 開発者向けのApple Pay との統合に関するドキュメント **を参照してください。**

詳しくは、[ 設定 ](configure-admin.md#apple-pay) を参照してください。

### [!DNL Google Pay] ボタン

[!DNL Google Pay] をチェックアウトエクスペリエンスに統合することで、マーチャントは、買い物客のGoogle アカウントから保存された支払い、連絡先、配送情報を収集し、サポートされているブラウザーやアプリ間で便利で効率的なチェックアウトを提供できます。

[!DNL Google Pay] は、特定の国または地域および特定のデバイスでのみ利用できます。 詳しくは、[[!DNL Google Pay]  ドキュメント ](https://developer.paypal.com/docs/checkout/apm/google-pay/#link-googlepayintegration) を参照してください。

![ チェックアウトの「Google支払い」ボタン ](assets/google-pay-button.png){width="500" zoomable="yes"}

有効にすると、製品ページ、ミニカート、買い物かご、チェックアウトの各ビューに「[!DNL Google Pay]」ボタンが表示されます。 詳しくは、[ 設定 ](configure-admin.md) を参照してください。

>[!NOTE]
>
> [!DNL Google Pay] API は、安全なコンテキストの web サイトでのみ使用できます。 詳しくは、[ トラブルシューティング ](https://developers.google.com/pay/api/web/support/troubleshooting) のドキュメントを参照してください。

### [!DNL PayPal Payment Buttons]

[!DNL PayPal payment buttons] は、PayPal を使用して購入を完了し、買い物客の配送先住所、請求先住所、支払い詳細を保存して後で使用します。 買い物客は、以前に保存または PayPal によって提供されたあらゆる支払い方法を使用できます。

![PayPal ボタン ](assets/paypal-button.png){width="350" zoomable="yes"}

[!UICONTROL PayPal payment buttons] は、ストア設定または [!DNL Payment Services] ホームで設定できます。

国ごとの支払い方法の利用可能性については、PayPal の [ 支払い方法ドキュメント ](https://developer.paypal.com/docs/checkout/payment-methods/) を参照してください。

#### [!DNL PayPal] ボタン

PayPal ボタンを使用すると、お客様は安心してチェックアウトできます。

「[!DNL PayPal]」ボタンは、製品ページ、ミニカート、買い物かご、チェックアウト表示に表示されます。

#### [!DNL Venmo] ボタン

ユーザーは「[Venmo](https://venmo.com/)」ボタンを使用してチェックアウトできます。

「[!DNL Venmo]」ボタンは、製品ページ、ミニカート、買い物かご、チェックアウト表示に表示されます。

#### PayPal の「デビット」ボタンまたは「クレジットカード」ボタン

お客様は PayPal のデビットカードまたはクレジットカードのボタンを使用してチェックアウトできます。

PayPal の「デビット」または「クレジットカード」ボタンがチェックアウトページに表示されます。

このオプションは、クレジットカード統合の代わりに、PayPal がホストするボタンを使用して、買い物客にデビットまたはクレジットカードの支払いオプションを提示するために使用できます。

#### [!DNL Pay Later] ボタン

顧客が今すぐ購入して後で [!DNL Pay Later] ボタンを使用して支払うことができるように、短期、無利子の支払い、およびその他の資金調達オプションを提供します。

「[!DNL Pay Later]」ボタンは、製品ページ、ミニカート、買い物かご、チェックアウト表示に表示されます。

PayPal Developer ドキュメントの [Pay Later オファー ](https://developer.paypal.com/docs/checkout/pay-later/us/) に関する情報を参照してください。 **国または地域** ドロップダウンを使用して、関心のある地域を選択します。

[!DNL Pay Later] 設定 [ 設定を更新して、](configure-admin.md#pay-later-button) メッセージを無効または有効にする方法を説明します。

##### オプション。 後で支払うメッセージの設定

**後で支払う** の [ メッセージングの設定 ](configure-admin.md#pay-later-button) を使用すると、マーチャントはこの支払いオプションのデフォルトスタイルを変更できます。 **[!UICONTROL Display Pay Later Message]** 設定 `Yes` 設定で [ を ](configure-admin.md#pay-later-button) に設定すると、**[!UICONTROL Configure Messaging]** モーダルボタンが表示され、**[!UICONTROL PayPal Pay Later messaging]** のスタイルを設定できます。

![Pay Later Messaging](assets/pay-later-messaging.png){width="500" zoomable="yes"}

### PayPal 支払いボタンのみを使用

ストアを実稼動モードにすばやく切り替えるには、PayPal 支払いボタン _Venmo_ PayPal など）を設定します。- PayPal クレジットカードの支払いオプションも使用する代わりに、

これにより、次のことが可能になります。

* Venmo や PayPal の支払いボタンなど、顧客に対して様々な支払いオプションを提供します。PayPal でホストされるカードフィールドをオフにしたり、既存のクレジットカードプロバイダーを使用したりするオプションもあります。
* クレジットカード決済には既存のクレジットカード会社を使用し、PayPal の他の支払いオプションも使用します。
* PayPal の支払いボタンは、PayPal が支払いオプションとしてクレジットカードをサポートしていない地域で使用してください。

**PayPal 支払いボタン _のみ_ を使用して支払いをキャプチャする（PayPal クレジットカード支払いオプションを使用しない __）**

1. ストアが [ 実稼動モード ](configure-admin.md#enable-payment-services) であることを確認します。
1. [ 設定で目的の PayPal 支払いボタンを設定 ](configure-admin.md#payment-buttons) します。
1. _のセクションの_ のオプションを **[[!UICONTROL Show PayPal Credit and Debit card button]](configure-admin.md#payment-buttons)** オフ _[!UICONTROL Payment buttons]_&#x200B;します。

**既存のクレジット・カード・プロバイダを使用して支払を取得する _および_PayPal 支払いボタン** 手順は、次のとおりです。

1. ストアが [ 実稼動モード ](configure-admin.md#enable-payment-services) であることを確認します。
1. [ 目的の PayPal 支払いボタンを設定します ](configure-admin.md#payment-buttons)。
1. _のセクションの_ のオプションを **[[!UICONTROL PayPal Show Credit and Debit card button]](configure-admin.md#payment-buttons)** オフ _[!UICONTROL Payment buttons]_&#x200B;します。
1. _のセクションの_ のオプションを **[[!UICONTROL Show on checkout page]](configure-admin.md#credit-card-fields)** オフ _[!UICONTROL Credit card fields]_&#x200B;にし、[ 既存のクレジットカードプロバイダーアカウント ](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/payments/payments.html#payments) を使用します。

## チェックアウトオプション

[!DNL Payment Services] を使用すると、買い物客の好みや行動に最適なAdobe Commerceのチェックアウトエクスペリエンスを設定できます。 クレジットカード [ ヴォールティング ](vaulting.md) や注文の自動無効化などの機能により、顧客はシームレスで手間のかからないトランザクションを確実に行うことができます。

Adobe CommerceとMagento Open Source [!DNL Payment Services] を使用すると、複数のチェックアウトエクスペリエンスを利用できます。 チェックアウトプロセスの位置に応じて、支払い方法ごとに異なる動作があります。

* 製品ページ – 品目の製品ページ

* ミニ買い物かご – カートに製品が追加されたときに、買い物かごアイコンをクリックすると使用できます

* 買い物かご – 「表示」をクリックしてミニカートから買い物かごを編集すると使用可能

* チェックアウト表示 – 「ミニ・カートまたはショッピング・カートからチェックアウトに進む」をクリックすると使用可能

### 注文の再計算

お客様がミニカート、買い物かご、または商品ページからチェックアウトフローに入ると、注文レビューページに移動し、PayPal ポップアップウィンドウで選択した配送先住所を確認できます。 顧客が配送方法を選択すると、注文金額が適切に再計算され、顧客は配送料と税金を確認できます。

顧客がチェックアウトページからチェックアウトフローに入ると、システムは既に配送先住所と最終的な計算金額を認識しており、合計が適切に表されます。

祝日、送料、消費税は場所によって大きく異なる場合があります。 配送先住所 [!DNL Payment Services] 料金を受け取ると、適用可能なすべてのコストをすばやく再計算し、チェックアウトの最後の段階でそれらを適切に表示します。

国別の支払い方法の可用性については、[PayPal の支払い方法 ](https://developer.paypal.com/docs/checkout/payment-methods/){target=_blank} ドキュメントを参照してください。
