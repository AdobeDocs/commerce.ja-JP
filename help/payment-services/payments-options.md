---
title: 支払い方法
description: 支払いオプションを設定して、ストアの顧客が利用できる方法をカスタマイズします。
role: Admin, User
level: Intermediate
exl-id: 95e648e6-6cb8-4226-b5ea-e1857212f20a
feature: Payments, Checkout, Configuration, Paas, Saas
source-git-commit: 379345261bebe5bee9cdbcb6fd3b0ce6275df6ea
workflow-type: tm+mt
source-wordcount: '2326'
ht-degree: 0%

---

# 支払い方法

[!DNL Adobe Commerce]と[!DNL Magento Open Source] [!DNL Payment Services]では、複数の支払いオプションを利用できます。

これらの支払いオプションは、[&#x200B; ホーム設定](payments-home.md)または[&#x200B; ストア設定](configure-admin.md)で設定できます（従来の支払いオプションまたはマルチストア設定に推奨）。

決済方法は、決済プロセスのどの段階にあるかによって異なります。

* 製品ページ – 品目の製品ページ
* ミニカート：商品がカートに追加された際に、カートアイコンをクリックすると利用できます
* 買い物かご – _ミニカートからカートを表示して編集_&#x200B;をクリックすると利用できます
* チェックアウトビュー – _ミニカートまたはショッピングカートからチェックアウト_&#x200B;に進むと、クリック時に表示されます

>[!IMPORTANT]
>
>支払いを処理するには、[!DNL Payment Services] オンボーディングを完了する必要があります。

## 標準と高度な支払い体験

[!DNL Payment Services]では、お客様が事業を展開している国に応じて、**Advanced** （完全サポート）および&#x200B;**Standard** （Express Checkout）の支払いオプションとオンボーディングフローを提供しています。

* **詳細** – 現在の[完全にサポートされている国](compatibility.md#standard-vs-advanced-payment-services-experience)では、利用可能なすべての[支払いオプション &#x200B;](../payment-services/payments-options.md)を利用できます。 ライブ決済を有効にするオンボーディング中に、[高度なオンボーディングオプション &#x200B;](../payment-services/production.md#advanced-onboarding)を選択します。

* **Standard** – 支払いオプションのサブセット（Express Checkout）（PayPal クレジットカードおよびデビットカード）は、サポートされている他の国で利用可能です。 [&#x200B; クレジットカードのフィールド &#x200B;](#credit-card-fields)と[Apple Pay](#apple-pay-button)は、このオンボーディングオプションでは使用できません。 ライブ決済を有効にするオンボーディング中に、[標準オンボーディングオプション &#x200B;](../payment-services/production.md#standard-onboarding)を選択します。

高度なオンボーディングと標準オンボーディングの完了については、実稼動環境[&#128279;](../payment-services/production.md#complete-merchant-onboarding)の有効 [!DNL Payment Services] を参照してください。

## [!UICONTROL Credit Card Fields]

[!UICONTROL Credit Card Fields]は、クレジットカードまたはデビットカードの支払い方法にシンプルで安全なチェックアウトを提供します。 買い物客がクレジットカードのフィールドを使用してチェックアウトする場合、名前、請求先住所、クレジットカードまたはデビットカードの情報を入力して注文します。 購入セッション中に顧客データを安全に使用し、チェックアウトフローをスムーズに誘導できます。

![&#x200B; チェックアウト時のクレジットカードのフィールド &#x200B;](assets/credit-card-fields.png){width="500" zoomable="yes"}

## [!UICONTROL Digital Wallets]

### [!DNL Fastlane] ボタン

[!DNL Fastlane]では、迅速、安全、手間のかからないオンライン支払い方法を提供しています。 **ゲストチェックアウト**&#x200B;中に、今後さらに迅速に購入できるように、カードと配送情報を安全に保存できます。

* **検証済みの買い物客にすばやくアクセス**：数百万人のリピーターを特定し、数秒でシームレスな支払いを実現します。
* **売上を増加**：より多くの購入が完了したので、コンバージョン率と承認率を向上させます。
* **チェックアウトを高速化**：安全でパスワードのないログイン体験で顧客の摩擦を減らします。

[!DNL Fastlane]が有効になっている場合、[!UICONTROL Credit Card Fields] オプションはデフォルトで無効になっています。

>[!NOTE]
>
> サンドボックスインスタンスでは、Fastlane トランザクションはトランザクションアクティビティビューに配送先住所を表示しません。

詳しくは、「[Fastlane by PayPal](https://www.paypal.com/us/fastlane){target=_blank}」のトピックを参照してください。

### [!DNL Apple Pay] ボタン

[!DNL Apple Pay]を使用すると、加盟店は安全で合理的なチェックアウト体験を提供でき（加盟店アカウントごとに最大99 ドメイン）、コンバージョンを向上させることができます。

* **Safari （macOSおよびiOS）** — [!DNL Apple Pay] ボタンを使用すると、お客様のApple デバイスから、チェックアウトの開始時（express）および最終チェックアウトページの両方に、保存された支払い、連絡先、および配送の詳細を直接自動入力できます。
* **Chrome、Firefox、Microsoft Edge** – 買い物客は、**express チェックアウト**&#x200B;および&#x200B;**最終チェックアウト手順**&#x200B;の両方で[!DNL Apple Pay]を使用できます。 デスクトップでは、**QR コード**&#x200B;が表示され、買い物客は&#x200B;**iPhone** （iOS 18以降）のApple支払いシートで支払いを完了してウォレットフローを開きます。

Appleのこのフローの概要については、[Walletの新機能および [!DNL Apple Pay]](https://developer.apple.com/videos/play/wwdc2024/10108/?time=35){target=_blank} （Apple Developer, WWDC24）を参照してください。

![&#x200B; ミニカートの「Apple支払い」ボタン &#x200B;](assets/applepay-button.png){width="500" zoomable="yes"}

有効にすると、商品ページ、ミニカート、ショッピングカート、チェックアウトビューから[!DNL Apple Pay] ボタンが表示されます。 ストア設定または拡張機能のホームで[!DNL Apple Pay]を設定できます。

お客様は、[!DNL Apple Pay]のエクスプレス チェックアウト中に、**1つのカート価格ルール （クーポン） コード**&#x200B;を適用または削除できます。

>[!NOTE]
>
> Apple Pay ドメイン検証証明書は、既に[!DNL Payment Services] コードに含まれています。 パス `/.well-known/apple-developer-merchantid-domain-association`が200の応答コードを返すことを確認します。 **Apple Pay Domain verification**&#x200B;証明書について詳しくは、[Apple Pay](https://developer.paypal.com/docs/checkout/apm/apple-pay/#download-and-host-sandbox-domain-association-file)との統合に関するPayPal開発者ドキュメントを参照してください。

詳しくは、[設定](configure-admin.md#apple-pay)を参照してください。

#### [!DNL Apple Pay] expressの制限事項

[!DNL Apple Pay]支払いシートの&#x200B;**プロモーションコード**

* [!DNL Apple Pay]支払いシートに入力されたプロモーション コードは、Express フローにのみ適用されます。 標準チェックアウトページで[!DNL Apple Pay]が選択されている場合、これらは適用されません。
* [!DNL Apple Pay]の支払いシートごとに適用できるのは&#x200B;**one** プロモーション コードのみです。
* [!DNL Apple Pay]件のレビューページがありません。買い物客は支払い用紙から直接購入を完了します。
* 買い物客が[!DNL Apple Pay]支払いシートを閉じて再度開いた場合、以前に入力したプロモーションコードは記憶されません。割引額のみが合計に反映されます。

**Safari以外のブラウザー**

* [!DNL Apple Pay]個のボタンは、expressまたは標準のチェックアウトフローでAndroid デバイス上にレンダリングされません。
* **バーチャル製品**&#x200B;の場合、[!DNL Apple Pay]の支払いシートには、引き続き配送先住所の入力が求められます。 Appleでは、お客様が支払いの承認を行うまで請求先住所を提供しないため、請求先住所を集計するためのベストエフォート見積もりとして使用されます。

### [!DNL Google Pay] ボタン

[!DNL Google Pay]をチェックアウト体験に組み込むことで、加盟店は買い物客のGoogle アカウントから保存された支払い、連絡先、配送情報を収集でき、サポートされているブラウザーとアプリをまたいで、便利で合理的なチェックアウトを提供します。

[!DNL Google Pay]は、特定の国または地域、および特定のデバイスでのみ利用できます。 詳しくは、[[!DNL Google Pay]  ドキュメント &#x200B;](https://developer.paypal.com/docs/checkout/apm/google-pay/#link-googlepayintegration)を参照してください。

![&#x200B; チェックアウト時の「Google支払い」ボタン &#x200B;](assets/google-pay-button.png){width="500" zoomable="yes"}

有効にすると、商品ページ、ミニカート、ショッピングカート、チェックアウトビューから[!DNL Google Pay] ボタンが表示されます。 詳しくは、[設定](configure-admin.md)を参照してください。

[!DNL Google Pay] **express**&#x200B;のチェックアウトでは、**配送方法をGoogle支払いシート**&#x200B;に表示し、オプションの&#x200B;**レビュー**&#x200B;手順（**[レビューをスキップ](configure-admin.md#google-pay)**&#x200B;設定）をサポートし、チェックアウト時に&#x200B;**プロモーションコード** フィールドを含めることができます。

>[!NOTE]
>
> [!DNL Google Pay] APIは、安全なコンテキスト内のWeb サイトでのみ使用できます。 詳しくは、[&#x200B; トラブルシューティング &#x200B;](https://developers.google.com/pay/api/web/support/troubleshooting)のドキュメントを参照してください。

#### [!DNL Google Pay] expressの制限事項

**支払い用紙の発送**

* **shipping-in-sheet** ビヘイビアー（クライアントサイドのシッピングコールバック）は、**[!UICONTROL Skip Review]**&#x200B;が[Google支払い設定](configure-admin.md#google-pay)で`Yes`に設定されている場合にのみ使用できます。

[!DNL Google Pay]支払いシートの&#x200B;**プロモーションコード**

* [!DNL Google Pay]支払いシートに入力されたプロモーション コードは、Express フローにのみ適用されます。 標準チェックアウトページで[!DNL Google Pay]が選択されている場合、これらは適用されません。
* ストアで注文ごとに複数のクーポンが許可されている場合でも、[!DNL Google Pay]支払いシートごとに&#x200B;**one**&#x200B;のプロモーション コードのみを適用できます。 （標準のカートとチェックアウトでは、複数のクーポンが引き続きサポートされています）。
* プロモーションコードは、ギフトカード商品には適用できません。
* プロモーションコードフィールドは&#x200B;**Android デバイスではサポートされていません**。
* [!DNL Google Pay]の支払い用紙に追加されたコードは、Commerceの買い物かごページからではなく、支払い用紙からのみ削除できます。
* Adobe Commerce 2.4.4-2.4.6では、プラットフォームの制限により、[!DNL Google Pay]支払いシートの割引明細に値が表示されない場合があります。
* Adobe Commerce 2.4.7では、GraphQLの応答のプラットフォームの制限により、一部の商品（主にダウンロード可能な商品）に対して[!DNL Google Pay]支払いシートに割引値が表示されない場合があります。
* 自動[買い物かご価格ルール &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart.html?lang=ja)が適用される場合（例：200 ドルを超える支出の場合は「$50 オフ」など）は、買い物客が支払いシートに適用するコードと組み合わされます。 [!DNL Google Pay]支払いシートに表示される合計は、結果として注文概要と異なる場合があります。

### [!DNL PayPal Payment Buttons]

PayPalを使用して購入を完了する[!DNL PayPal payment buttons]は、後で使用するために買い物客の配送先住所、請求先住所、支払い詳細を保存します。 買い物客は、PayPalが過去に保存または提供していた支払い方法を使用できます。

![PayPal ボタン &#x200B;](assets/paypal-button.png){width="350" zoomable="yes"}

ストア設定または[!DNL Payment Services] ホームで[!UICONTROL PayPal payment buttons]を設定できます。

PayPalの[支払い方法に関するドキュメント &#x200B;](https://developer.paypal.com/docs/checkout/payment-methods/)で、国別の支払い方法の利用可能性について説明しています。

#### [!DNL PayPal] ボタン

顧客は、「PayPal」ボタンを使用して、簡単かつ確実に決済できます。

[!DNL PayPal] ボタンは、製品ページ、ミニカート、ショッピングカート、チェックアウトビューから表示されます。

#### [!DNL Venmo] ボタン

お客様は、[Venmo](https://venmo.com/) ボタンを使用してチェックアウトできます。

[!DNL Venmo] ボタンは、製品ページ、ミニカート、ショッピングカート、チェックアウトビューから表示されます。

#### PayPal デビットカードまたはクレジットカードのボタン

顧客は、「PayPal デビットカード」または「クレジットカード」ボタンを使用してチェックアウトできます。

PayPal デビットカードまたはクレジットカードのボタンは、チェックアウトページから表示されます。

このオプションは、クレジットカード統合の代わりに、PayPal ホスティングのボタンを使用して、デビットカードまたはクレジットカードの支払いオプションを買い物客に提示するために使用できます。

#### [!DNL Pay Later] ボタン

顧客に短期、無利息、その他の支払いオプションを提供して、今すぐ購入し、[!DNL Pay Later] ボタンで後から支払えるようにします。

[!DNL Pay Later] ボタンは、製品ページ、ミニカート、ショッピングカート、チェックアウトビューから表示されます。

[後払いオファー](https://developer.paypal.com/docs/checkout/pay-later/us/)に関する情報については、PayPal デベロッパーのドキュメントを参照してください。 **国または地域** ドロップダウンを使用して、興味のある地域を選択します。

[設定](configure-admin.md#paypal-payment-buttons)を更新して、[!DNL Pay Later] メッセージを無効または有効にする方法について説明します。

##### オプション。 後払いメッセージの設定

[Pay Later](configure-admin.md#paypal-payment-buttons)の&#x200B;**メッセージ**&#x200B;を設定すると、販売者はこの支払いオプションのデフォルトスタイルを変更できます。 [設定](configure-admin.md#paypal-payment-buttons)で&#x200B;**[!UICONTROL Display Pay Later Message]**&#x200B;を`Yes`に設定すると、**[!UICONTROL Configure Messaging]** モーダルボタンが表示され、**[!UICONTROL PayPal Pay Later messaging]**&#x200B;のスタイルを設定できます。

![後払いメッセージ &#x200B;](assets/pay-later-messaging.png){width="500" zoomable="yes"}

### PayPal支払いボタン用のサーバーサイド配送コールバック

PayPal、Pay Later、Venmoの支払い方法では、[&#x200B; サーバーサイドの配送コールバック &#x200B;](https://developer.paypal.com/docs/multiparty/checkout/standard/customize/shipping-module/)を使用して、PayPalがCommerce インスタンスと直接通信して配送オプションを取得し、リアルタイムで合計を計算できるようにします。

このサーバーサイドのアプローチにより、[!DNL Payment Services]は注文確認ポップアップをスキップして、より迅速で合理的な購入体験を提供できます。 送料や税金はコールバックを通じて動的に計算されるため、バイヤーはPayPalまたはVenmoのレビューページで直接正確な合計を確認できます。

>[!NOTE]
>
>コールバックエンドポイントは公開され、5秒以内に応答する必要があります。 応答時間がこの制限を超える場合、PayPalはポップアップにエラーメッセージを表示します。 これらの支払い方法をローカルでテストする方法については、[ローカル開発環境でのテスト &#x200B;](test-validate.md#test-on-local-development-environments)を参照してください。

### PayPal支払いボタンのみを使用

ストアをすばやく実稼動モードにするには、PayPal クレジットカード支払いオプションを使用する代わりに、_only_&#x200B;のPayPal支払いボタン（Venmo、PayPalなど）を設定できます。

これにより、次のことが可能になります。

* VenmoやPayPalの支払いボタンなど、顧客のためのさまざまな支払いオプションを提供しましょう。さらに、PayPalのホスティングカードフィールドをオフにし、既存のクレジットカード会社を利用することもできます。
* 既存のクレジットカード決済プロバイダーをクレジットカード決済に使用すると同時に、PayPalの他の決済オプションも使用します。
* PayPalが支払いオプションとしてクレジットカードをサポートしていない地域では、PayPalの支払いボタンを使用します。

_のみ_&#x200B;のPayPal支払いボタン（_ではなく_ PayPal クレジットカード支払いオプション）で&#x200B;**支払いをキャプチャするには**:

1. ストアが実稼動モード [&#128279;](configure-admin.md#general-configuration)のであることを確認します。
1. [設定で必要なPayPal支払いボタン &#x200B;](configure-admin.md#paypal-payment-buttons)を設定します。
1. _[!UICONTROL Payment buttons]_&#x200B;セクションの&#x200B;**[[!UICONTROL Show PayPal Credit and Debit card button]](configure-admin.md#paypal-payment-buttons)**&#x200B;オプションを_ オフ _にします。

既存のクレジットカード プロバイダー&#x200B;_および_&#x200B;のPayPal支払いボタン **での支払いを** キャプチャするには：

1. ストアが実稼動モード [&#128279;](configure-admin.md#general-configuration)のであることを確認します。
1. [PayPal支払いボタンを設定します](configure-admin.md#paypal-payment-buttons)。
1. _[!UICONTROL Payment buttons]_&#x200B;セクションの&#x200B;**[[!UICONTROL PayPal Show Credit and Debit card button]](configure-admin.md#paypal-payment-buttons)**&#x200B;オプションを_ オフ _にします。
1. _[!UICONTROL Credit card fields]_&#x200B;セクションの&#x200B;**[[!UICONTROL Show on checkout page]](configure-admin.md#credit-card-fields)**&#x200B;オプションを_ オフ _にし、[既存のクレジットカード プロバイダーのアカウント &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/payments/payments.html?lang=ja#payments)を使用します。

## 現地での支払い方法

ローカル支払い方法（LPM）は、銀行振込やローカライズされた支払いソリューションなど、地域固有およびローカルの支払い方法と、既存のカードベースのオプションをサポートします。 マーチャントは、Commerce設定内で利用可能なLPMを直接有効または無効にできます。 LPMは、Adobeの決済機能を拡張し、欧州市場のニーズをサポートして、チェックアウトのローカライゼーションを向上させ、コンバージョン、マーチャントの導入、バイヤー満足度の向上を支援します。

次のLPMを使用できます。

| お支払い方法 | 国 | 通貨 |
|----------------|-----------|----------|
| Bancontact | ベルギー | EUR |
| BLIK | ポーランド | プラン |
| eps | オーストリア | EUR |
| iDEAL | オランダ | EUR |
| MyBank | イタリア | EUR |
| Przelewy24 | ポーランド | EUR、プラン |

LPMは、請求先住所とweb サイトの基本通貨にもとづいて顧客に表示されます。 支払い方法は、両方の条件が支払い方法の要件に一致する場合にのみ表示されます。

詳しくは、[&#x200B; ローカル支払い方法の設定](configure-admin.md#local-payment-methods)を参照してください。

## Express チェックアウトボタン

より迅速なチェックアウト体験を促進するために、チェックアウトフローの開始時に支払いオプションを明示することができます。 PayPal、PayPal Pay Later、Venmo、Apple Pay、Google Payを利用して、購入を完了することができます。

有効にすると、チェックアウトプロセスの開始時にエクスプレスチェックアウトボタンが表示され、デジタルウォレットの支払い方法を好む顧客にはより迅速に購入できるようになります。

エクスプレスチェックアウトボタンを有効にするには、各支払い方法を個別に設定します。

* **PayPalと後払い**: [PayPal支払いボタン &#x200B;](configure-admin.md#paypal-payment-buttons)設定で&#x200B;**[!UICONTROL Show buttons at start of checkout]**&#x200B;を有効にします。

* **Apple Pay**: [Apple Pay](configure-admin.md#apple-pay)設定で&#x200B;**[!UICONTROL Show Apple Pay at start of checkout]**&#x200B;を有効にします。

* **Google Pay**: [Google Pay](configure-admin.md#google-pay)設定で&#x200B;**[!UICONTROL Show Google Pay at start of checkout]**&#x200B;を有効にします。

>[!NOTE]
>
>支払い方法の可用性は、購入者の場所によって異なります。 サンドボックスのテストでは、[購入者の国](sandbox.md#buyers-country)の設定を使用して、様々な地域をシミュレートします。 例えば、Venmoは米国でのみ利用可能です。 Pay Laterは、米国および英国でご利用いただけます。

## チェックアウトオプション

[!DNL Payment Services]を使用すると、買い物客の好みや行動に最適なAdobe Commerceのチェックアウトエクスペリエンスを設定できます。 クレジットカード [&#x200B; ヴォールティング &#x200B;](vaulting.md)や注文の自動無効化などの機能により、顧客にシームレスで手間のかからない取引を提供できます。

Adobe CommerceとMagento Open Source [!DNL Payment Services]を使用すると、複数のチェックアウトエクスペリエンスを利用できます。 決済方法は、決済プロセスのどの段階にあるかによって異なります。

* 製品ページ – アイテムの製品ページ

* ミニカート – カートに商品が追加された際に、カートアイコンをクリックすると利用できます

* ショッピングカート – ミニカートからカートを表示および編集をクリックすると利用可能

* チェックアウトビュー – 「ミニカートまたはショッピングカートからチェックアウトに進む」をクリックすると利用可能

### 注文の再計算

顧客がミニカート、ショッピングカート、または製品ページからチェックアウトフローに入ると、注文レビューページに誘導され、PayPal ポップアップウィンドウで選択した配送先住所を確認できます。 顧客が配送方法を選択すると、注文金額が適切に再計算され、顧客は送料と税金を確認できます。

顧客がチェックアウトページからチェックアウトフローに入ると、システムはすでに配送先住所と最終的に計算された金額を認識しており、合計が適切に表示されます。

祝日、送料、消費税は、場所によって大きく異なります。 [!DNL Payment Services]様が配送先住所と配送料を受け取った後、適用されるすべてのコストを迅速に再計算し、チェックアウトの最終段階で適切に表示します。

国別の支払い方法の利用可能性については、[PayPalの支払い方法](https://developer.paypal.com/docs/checkout/payment-methods/){target=_blank}のドキュメントをご覧ください。
