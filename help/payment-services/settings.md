---
title: 支払いサービスの設定
description: インストール後、ホームで  [!DNL Payment Services]  を設定できます。
role: Admin, User
level: Intermediate
exl-id: 108f2b24-39c1-4c87-8deb-d82ee1c24d55
feature: Payments, Checkout, Configuration, Paas, Saas
source-git-commit: 9e7eb509aa19f3382d36221ac0c7dcf2130e8d8d
workflow-type: tm+mt
source-wordcount: '2420'
ht-degree: 0%

---

# 設定

[!DNL Payment Services] ホームの便利な設定を使用して、ニーズに合わせて [!DNL Payment Services] をカスタマイズできます。

[!DNL Adobe Commerce] に対して [!DNL Payment Services] を設定するには、[!DNL Magento Open Source] をクリック **[!UICONTROL Settings]** ます。 これらの設定オプションは、[_一般_ 設定オプション ](#configure-general-settings) の _[!UICONTROL Payment mode]_&#x200B;フィールドで設定された環境にのみ適用されます。

マルチストア設定またはレガシー設定については、[ 管理者のの設定 ](configure-admin.md) を参照してください。

## 一般設定の指定

[!UICONTROL General] の設定により、支払い方法として支払いサービスを有効または無効にしたり、顧客トランザクションに情報を追加して、web サイトまたはストア表示にカスタム情報をマークまたはプレフィックス付けしたりできます。

### 支払いサービスの有効化

Web サイトに対して [!DNL Payment Services] を有効にし、サンドボックステストまたはライブ支払いを有効にできます。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL Payment Services]** に移動します。

1. 「**[!UICONTROL Settings]**」をクリックします。 詳しくは、[ 概要  [!DNL Payment Services]  ホーム ](payments-home.md) を参照してください。

   ![React 設定ビュー ](assets/react-settings-view.png){width="500" zoomable="yes"}

   _[!UICONTROL General]_&#x200B;のセクションには、支払い方法として [!DNL Payment Services] を有効にするために使用する設定が含まれています。

1. ストアの支払い方法として [!DNL Payment Services] を有効にするには、「_[!UICONTROL General]_」セクションで&#x200B;**[!UICONTROL Enable Payment Services as payment method]**&#x200B;を `Yes` に切り替えます。

1. ストアで [!DNL Payment Services] をテストしている場合は、**支払いモード** を `Sandbox` に設定します。 ライブ支払いを有効にする準備が整ったら、`Production` に設定します。

1. **[!UICONTROL Payment Services Sandbox ID]** と **[!UICONTROL Payment Services Production ID]** の値は、[Commerce サービスコネクタを設定し ](https://experienceleague.adobe.com/ja/docs/commerce-merchant-services/user-guides/integration-services/saas){target=_blank} 初めて [!DNL Payment Services] ダッシュボードにアクセスすると自動入力されます。 サンドボックス環境や実稼動環境のオンボーディングを完了するには、これを行います。 これらの値は、SaaS ID を [!DNL Payment Services] に関連付けます。

   >[!WARNING]
   >
   > [!DNL Payment Services] ID をリセットした場合は、再度オンボーディングする必要があります。

1. 「**[!UICONTROL Save]**」をクリックします。

   変更を保存せずにこのビューから移動しようとすると、変更の破棄、編集の継続、または変更の保存を求めるモーダルが表示されます。

1. **[!UICONTROL System]**/**[!UICONTROL Cache Management]** に移動し、「**[!UICONTROL Flush Cache]**」をクリックして、無効なキャッシュをすべて更新します。

これで、[ 支払いオプション ](#configure-payment-options) 機能およびストアフロント表示のデフォルト設定の変更に進むことができます。

### ソフト記述子を追加

Web サイトまたは個々のストア表示の設定に [!UICONTROL Soft Descriptor] を追加できます。 ソフト記述子は、顧客トランザクションの銀行取引明細書に表示されます。 例えば、複数のストア/ブランド/カタログがある場合、[!UICONTROL Soft Descriptor] のフィールドにカスタムテキストを追加することで、それらの間を簡単に区別できます。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL Payment Services]** に移動します。
1. 「**[!UICONTROL Settings]**」をクリックします。 詳しくは、[ 概要  [!DNL Payment Services]  ホーム ](payments-home.md) を参照してください。
1. ソフト記述子を作成する web サイト表示またはストア表示を **[!UICONTROL Scope]** ドロップダウンメニューで選択します。 初期設定の場合、このオプションを **[!UICONTROL Default]** のままにしてデフォルト値を設定します。
1. `Soft descriptor` を置き換えて、テキストフィールドにカスタムテキスト（最大 22 文字）を追加します。
1. 「**[!UICONTROL Save]**」をクリックします。
1. Web サイトまたはストアビュー用に設定されたデフォルト以外のソフト記述子を作成するには：
   1. ソフト記述子を作成する web サイト表示またはストア表示を **[!UICONTROL Scope]** ドロップダウンメニューで選択します。
   1. _オフ_&#x200B;**[!UICONTROL Use website]** （選択した範囲に応じて **[!UICONTROL Use default]**）を切り替えます。
   1. テキストフィールドにカスタムテキストを追加します。
   1. 「**[!UICONTROL Save]**」をクリックします。
1. Web サイトまたはストアビューでを有効にするには、親 Web サイトに使用するデフォルトのソフト記述子 _または_ を表示します。
   1. 既存のソフト記述子を有効にする web サイト表示またはストア表示を **[!UICONTROL Scope]** ドロップダウンメニューで選択します。
   1. _オン_&#x200B;**[!UICONTROL Use website]** （選択した範囲に応じて **[!UICONTROL Use default]**）を切り替えます。
   1. 「**[!UICONTROL Save]**」をクリックします。

   変更を保存せずにこのビューから移動しようとすると、変更の破棄、編集の継続、または変更の保存を求めるモーダルが表示されます。

### 設定オプション

| フィールド | 対象範囲 | 説明 |
|---|---|---|
| [!UICONTROL Enable] | web サイト | Web サイトの [!DNL Payment Services] を有効または無効にします。 オプション：[!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Payment mode] | ストア表示 | ストアのメソッド（環境）を設定します。 オプション：[!UICONTROL Sandbox] / [!UICONTROL Production] |
| [!UICONTROL Payment Services Sandbox ID] | ストア表示 | サンドボックスオンボーディング中に自動生成されるサンドボックスマーチャント ID。 |
| [!UICONTROL Payment Services Production ID] | ストア表示 | 実稼動（ライブ）オンボーディング中に自動生成される実稼動マーチャント ID。 |
| [!UICONTROL Soft Descriptor] | web サイトまたはストア表示 | Web サイトおよびストアビューにソフト記述子を追加して、ブランド、ストアまたは製品ラインを区別する顧客トランザクションに情報を追加します。 [!UICONTROL Use website] の切り替えにより、web サイトレベルで追加されたソフト記述子が適用されます。 [!UICONTROL Use default] 切替スイッチは、デフォルトとして追加された任意のソフト記述子を適用します。 |

## 支払オプションの設定

これで Web サイトの [!UICONTROL Payment Services] を有効にしたので、支払い機能とストアフロント表示のデフォルト設定を変更できます。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL Payment Services]** に移動します。
1. 「**[!UICONTROL Settings]**」をクリックします。 詳しくは、[ 概要  [!DNL Payment Services]  ホーム ](payments-home.md) を参照してください。
1. 以下の節に従って、[ クレジットカード ](#credit-card-fields)、[ 支払いボタン ](#payment-buttons) および [ ボタンスタイル ](#button-style) の支払いオプションを設定します。

### クレジットカードのフィールド

_[!UICONTROL Credit Card Fields]_&#x200B;の設定は、クレジットカードまたはデビットカードの支払い方法に対してシンプルで安全なチェックアウトオプションを提供します。

詳しくは、[ 支払いオプション ](payments-options.md#credit-card-fields) を参照してください。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL Payment Services]** に移動します。
1. 支払方法を有効にするストア表示を **[!UICONTROL Scope]** ドロップダウンメニューで選択します。
1. 「**[!UICONTROL Credit card fields]**」セクションで、「**[!UICONTROL Checkout title]**」フィールドの値を編集して、チェックアウト時に表示される支払い方法の名前を変更します。
1. [ 支払いアクションを設定 ](production.md#set-payment-services-as-payment-method) するには、**[!UICONTROL Payment action]** を `Authorize` または `Authorize and Capture` に切り替えます。
1. チェックアウトページで支払い方法に優先順位を付けるには、「**[!UICONTROL Sort order]**」フィールドに `Numeric Only` 値を入力します。
1. [3DS セキュア認証を有効にするには ](security.md#3ds) （デフォルトでは `Off`） **[!UICONTROL 3DS Secure authentication]** セレクターを `Always` または `When required` に切り替えます。
1. チェックアウトページでクレジットカードフィールドを有効または無効にするには、クレジッ **[!UICONTROL Show on checkout page]** セレクターを切り替えます。
1. [ カードのボルト ](#card-vaulting) を有効または無効にするには、**[!UICONTROL Vault enabled]** セレクターを切り替えます。
1. （マーチャントが [ 管理者の顧客に対してヴォールト支払方法を使用して注文を完了するために ](#card-vaulting) 管理者のヴォールト支払方法を有効または無効にするには、**[!UICONTROL Show vaulted methods in Admin]** のセレクターを切り替えます。
1. デバッグモードを有効または無効にするには、デバッ **[!UICONTROL Debug Mode]** セレクターを切り替えます。
1. 「**[!UICONTROL Save]**」をクリックします。

   変更を保存せずにこのビューから移動しようとすると、変更の破棄、編集の継続、または変更の保存を求めるモーダルが表示されます。

1. [ キャッシュをフラッシュします ](#flush-the-cache)。

#### 設定オプション

| フィールド | 対象範囲 | 説明 |
|---|---|---|
| [!UICONTROL Title] | ストア表示 | チェックアウト時に支払い方法ビューでこの支払いオプションのタイトルとして表示するテキストを追加します。 オプション：[!UICONTROL text field] |
| [!UICONTROL Payment Action] | web サイト | 指定した支払方法の [ 支払アクション ](https://experienceleague.adobe.com/ja/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"}。 オプション：[!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | ストア表示 | チェックアウトページでの指定した支払い方法の並べ替え順。 `Numeric Only` 値 |
| [!UICONTROL 3DS Secure authentication] | web サイト | [3DS セキュア認証 ](security.md#3ds) を有効または無効にします。 オプション：[!UICONTROL Always]/[!UICONTROL When Required]/[!UICONTROL Off] |
| [!UICONTROL Show on checkout page] | web サイト | チェックアウトページに表示するクレジットカードフィールドを有効または無効にします。 オプション：[!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Vault enabled] | ストア表示 | [ クレジット カードの保管 ](vaulting.md) を有効または無効にします。 オプション：[!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show vaulted payment methods in Admin] | ストア表示 | マーチャントが管理者で顧客の注文を完了する機能を有効または無効にします [ ボールト形式の支払い方法を使用 ](vaulting.md)。 オプション：[!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Debug Mode] | web サイト | デバッグモードを有効または無効にします。 オプション：[!UICONTROL Off] / [!UICONTROL On] |

### Apple ペイ

[!UICONTROL Apple Pay] ボタン支払いオプションを使用すると、Safari ブラウザーからストアのチェックアウトで [!UICONTROL Apple Pay] 支払いボタンを提供できます（マーチャントアカウントあたり最大 99 のドメイン）。

Apple Pay は、Paypal で [Apple Pay のセルフ登録を完了し ](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain) 店舗で [Apple Pay の設定 ](settings.md/#payment-buttons) を行った場合にのみ使用できます。

詳しくは、[ 支払いオプション ](payments-options.md#apple-pay-button) を参照してください。

[!UICONTROL Apple Pay] ボタンの支払いオプションを有効にして設定できます。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL Payment Services]** に移動します。
1. 支払方法を有効にするストア表示を **[!UICONTROL Scope]** ドロップダウンメニューで選択します。
1. 「**[!UICONTROL Apple Pay]**」セクションで、「_[!UICONTROL Checkout title]_」フィールドの値を編集して、チェックアウト時に表示される支払い方法の名前を変更します。
1. [ 支払いアクションを設定 ](production.md#set-payment-services-as-payment-method) するには、**[!UICONTROL Payment action]** を `Authorize` または `Authorize and Capture` に切り替えます。
1. チェックアウトページでApple Pay を有効または無効にするには、**[!UICONTROL Show Apple Pay on checkout page]** セレクターを切り替えます。
1. 商品の詳細ページでApple Pay を有効または無効にするには、**[!UICONTROL Show Apple Pay on product detail page]** セレクターを切り替えます。
1. ミニ買い物かごのプレビューでApple Pay を有効または無効にするには、**[!UICONTROL Show Apple Pay on the mini cart preview]** セレクターを切り替えます。
1. 買い物かごページでApple Pay を有効または無効にするには、**[!UICONTROL Show Apple Pay on cart page]** セレクターを切り替えます。
1. デバッグモードを有効または無効にするには、デバッ **[!UICONTROL Debug Mode]** セレクターを切り替えます。
1. 「**[!UICONTROL Save]**」をクリックします。

   変更を保存せずにこのビューから移動しようとすると、変更の破棄、編集の継続、または変更の保存を求めるモーダルが表示されます。

1. [ キャッシュをフラッシュします ](#flush-the-cache)。

#### 設定オプション

| フィールド | 対象範囲 | 説明 |
|---|---|---|
| [!UICONTROL Checkout title] | ストア表示 | チェックアウト時に支払い方法ビューでこの支払いオプションのタイトルとして表示するテキストを追加します。 オプション：[!UICONTROL text field] |
| [!UICONTROL Payment Action] | web サイト | 指定した支払方法の [ 支払アクション ](https://experienceleague.adobe.com/ja/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions)。 オプション：[!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Show on checkout page] | web サイト | チェックアウトページに表示する「Apple支払い」ボタンを有効または無効にします。 オプション：[!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show on checkout page] | web サイト | Appleの「支払い」ボタンを有効または無効にして、商品の詳細ページに表示します。 オプション：[!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show on mini cart preview] | web サイト | Appleの「支払い」ボタンを有効または無効にして、ミニ買い物かごのプレビューに表示します。 オプション：[!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show on cart page] | web サイト | Appleの「支払い」ボタンを有効または無効にして、買い物かごページに表示します。 オプション：[!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Debug Mode] | web サイト | デバッグモードを有効または無効にします。 オプション：[!UICONTROL Off] / [!UICONTROL On] |

### 支払いボタン

[!DNL PayPal payment buttons] の支払いオプションは、顧客にシンプルで迅速かつ安全なチェックアウトプロセスを提供します。 詳しくは、[ 支払いオプション ](payments-options.md#paypal-smart-buttons) を参照してください。

PayPal 支払いボタンの支払いオプションを有効にして設定できます。

1. 支払方法を有効にするストア表示を **[!UICONTROL Scope]** ドロップダウンメニューで選択します。
1. チェックアウト時に表示される支払い方法の名前を変更するには、「**[!UICONTROL Checkout Title]**」フィールドの値を編集します。
1. [ 支払いアクションを設定 ](production.md#set-payment-services-as-payment-method) するには、**[!UICONTROL Payment action]** を `Authorize` または `Authorize and Capture` に切り替えます。
1. チェックアウトページで支払い方法に優先順位を付けるには、「**[!UICONTROL Sort order]**」フィールドに `Numeric Only` 値を入力します。
1. 切り替えセレクターを使用して、ディスプレイ機能を有効または無効 [!DNL PayPal smart button] します。

   - **[!UICONTROL Show PayPal buttons on product checkout page]**
   - **[!UICONTROL Show PayPal buttons on product detail page]**
   - **[!UICONTROL Show PayPal buttons in mini-cart preview]**
   - **[!UICONTROL Show PayPal buttons on cart page]**
   - **[!UICONTROL Show PayPal Pay Later button]**
   - **[!UICONTROL Show PayPal Pay Later message]**
   - **[!UICONTROL Show Venmo button]**
   - **[!UICONTROL Show Apple Pay button]**
   - **[!UICONTROL Show PayPal Credit and Debit Card button]**

     >[!NOTE]
     >
     > Apple Pay を使用するには、テストのために [Apple サンドボックステスターアカウントが必要です ](https://developer.apple.com/apple-pay/sandbox-testing/#create-a-sandbox-tester-account) （偽のクレジットカードおよび請求情報を含む）。 Apple Pay をサンドボックス _または_ 実稼動モードで使用する準備が整ったら、[ テストと検証 ](test-validate.md#test-in-sandbox-environment) を完了した後、[ [!DNL Apple Pay]](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain)_ライブドメインの登録_ の節のみ）を完了し、[ のストア用に設定  [!DNL Payment Services]](settings.md#payment-buttons) を行います。

     支払いボタンまたは PayPal Pay Later メッセージの表示のオン/オフを切り替えると、設定の視覚的なプレビューが設定ページの下部に表示されます。

1. デバッグモードを有効にするには、デバッ **[!UICONTROL Debug Mode]** セレクターを切り替えます。
1. 「**[!UICONTROL Save]**」をクリックします。

   変更を保存せずにこのビューから移動しようとすると、変更の破棄、編集の継続、または変更の保存を求めるモーダルが表示されます。

1. [ キャッシュをフラッシュします ](#flush-the-cache)。

#### 設定オプション

| フィールド | 対象範囲 | 説明 |
|---|---|---|
| [!UICONTROL Title] | ストア表示 | チェックアウト時に支払い方法ビューでこの支払いオプションのタイトルとして表示するテキストを追加します。 オプション：テキストフィールド |
| [!UICONTROL Payment Action] | web サイト | 指定した支払方法の [ 支払アクション ](https://experienceleague.adobe.com/ja/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"}。 オプション：[!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | ストア表示 | チェックアウトページでの指定した支払い方法の並べ替え順。 `Numeric Only` 値 |
| [!UICONTROL Show PayPal buttons on checkout page] | ストア表示 | チェックアウトページで [!DNL PayPal payment buttons] を有効または無効にします。 オプション：[!UICONTROL &#x200B; Yes] / [!UICONTROL No] |
| [!UICONTROL Show PayPal buttons on product detail page] | ストア表示 | 製品の詳細ページで [!DNL PayPal payment buttons] を有効または無効にします。 オプション：[!UICONTROL &#x200B; Yes] / [!UICONTROL No] |
| [!UICONTROL Show PayPal buttons in mini-cart preview] | ストア表示 | ミニ買い物かごのプレビューで [!DNL PayPal payment buttons] を有効または無効にします。 オプション：[!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal buttons on cart page] | ストア表示 | 買い物かごページの [!DNL PayPal payment buttons] を有効または無効にします。 オプション：[!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal Pay Later button] | ストア表示 | 支払ボタンが表示される後で支払う支払いオプションの外観を有効または無効にします。 オプション：[!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal Pay Later Message] | web サイト | 買い物かご、製品ページ、ミニカート、およびチェックアウトフロー中の「後で支払う」メッセージを有効または無効にします。 オプション：[!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show Venmo button] | ストア表示 | 支払ボタンが表示される Venmo 支払オプションを有効または無効にします。 オプション：[!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show Apple Pay button] | ストア表示 | 支払いボタンが表示される「Apple Pay」支払いオプションを有効または無効にします。 オプション：[!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal Credit and Debit card button] | ストア表示 | 支払いボタンが表示されるクレジット カードおよびデビット カードの支払いオプションを有効または無効にします。 オプション：[!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Debug Mode] | web サイト | デバッグモードを有効または無効にします。 オプション：[!UICONTROL Off] / [!UICONTROL On] |

### ボタンのスタイル

また、支払いボタンの _[!UICONTROL Button style]_&#x200B;のオプションを設定することもできます。

1. **[!UICONTROL Layout]** を変更するには、「`Vertical`」または「`Horizontal`」を選択します。

   >[!NOTE]
   >
   > ボタンスタイルが `Horizontal` として設定され、ストアが複数の支払いボタンを表示するように設定されている場合、製品ページ、チェックアウトページ、ミニカートに 2 つのボタンのみが表示され、カートに 1 つのボタンが表示されます。

1. 水平方向のレイアウトでタグラインを有効にするには、**[!UICONTROL Show tagline]** セレクターを切り替えます。
1. **[!UICONTROL Color]** を変更するには、目的のカラーオプションを選択します。
1. **[!UICONTROL Shape]** を変更するには、「`Pill`」または「`Rectangle`」を選択します。
1. ボタンの高さセレクターを有効にするには、ボタ **[!UICONTROL Responsive button height]** の高さセレクターを切り替えます。
1. **[!UICONTROL Label]** を変更するには、目的のラベル オプションを選択します。

   レイアウト、カラー、シェイプ、高さ、ラベルの設定オプションを変更すると、その設定の視覚的なプレビューが設定ページの下部に表示されます。 下の画像では、**[!UICONTROL Shape]** が _長方形_ に設定され、**[!UICONTROL Label]** が _PayPal （推奨）_ に設定されています。

   ![[!DNL PayPal payment buttons] のオプション ](assets/payment-buttons.png){width="400" zoomable="yes"}

1. 「**[!UICONTROL Save]**」をクリックします。

   変更を保存せずにこのビューから移動しようとすると、変更の破棄、編集の継続、または変更の保存を求めるモーダルが表示されます。

1. [ キャッシュをフラッシュします ](#flush-the-cache)。

支払いボタンのスタイル設定は [ 管理の従来の設定で ](configure-admin.md#configure-paypal-smart-buttons) 設定することも、ここ [!DNL Payment Services Home] 設定することもできます。 PayPal 支払いボタンのスタイル設定について詳しくは、[PayPal のボタンスタイルガイド ](https://developer.paypal.com/docs/checkout/standard/customize/buttons-style-guide/) を参照してください。

#### 設定オプション

| フィールド | 対象範囲 | 説明 |
|--- |--- |--- |
| [!UICONTROL Layout] | ストア表示 | 支払いボタンのレイアウトのスタイルを定義します。 オプション：[!UICONTROL Vertical] / [!UICONTROL Horizontal] |
| [!UICONTROL Tagline] | ストア表示 | タグラインを有効/無効にします。 オプション：[!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Color] | ストア表示 | 支払いボタンの色を定義します。 オプション：[!UICONTROL Blue] / [!UICONTROL Gold] / [!UICONTROL Silver] / [!UICONTROL White] / [!UICONTROL Black] |
| [!UICONTROL Shape] | ストア表示 | 支払いボタンの形状を定義します。 オプション：[!UICONTROL Rectangular] / [!UICONTROL Pill] |
| [!UICONTROL Responsive Button Height] | ストア表示 | 支払いボタンで既定の高さを使用するかどうかを定義します。 オプション：[!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Height] | ストア表示 | 支払いボタンの高さを定義します。 デフォルト値：なし |
| [!UICONTROL Label] | ストア表示 | 支払いボタンに表示されるラベルを定義します。 オプション：[!UICONTROL PayPal] / [!UICONTROL Checkout] / [!UICONTROL Buynow] / [!UICONTROL Pay] / [!UICONTROL Installment] |

## 役割の設定

管理者ユーザーがCommerce管理者で注文を作成および管理できるようにするには、[!DNL Payment Services] 固有のリソースをユーザーロールに対して有効にします。

役割の管理方法については、[ ユーザーの役割 ](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions-user-roles.html?lang=ja) を参照してください。

役割にリソースを割り当てる場合は、次を選択する必要があります。

- **[!DNL Payment Services]** を使用して支払う – このリソースにより、管理で注文を作成するときに、支払い方法として [!DNL Payment Services] のクレジットカードを使用できるようになります。 **アクション** 親リソースを選択すると、このリソースも選択されます。
- **[!DNL Payment Services]** – このリソースには、**Dashboard** リソースと **SaaS Services Proxy** リソースが含まれます。これらのリソースも選択する必要があります。 [!DNL Payment Services] が _Sales_ メニューに表示されます。

  ![ 資金決済サービス資源 ](assets/roles-payments.png){width="400" zoomable="yes"}

## キャッシュをフラッシュします

_設定_ で設定を変更した場合（例えば、Apple Pay、Venmo、または PayPal PayLater ボタンの切り替え）、キャッシュを手動でフラッシュして、ストアに最新の設定が表示されるようにします。

1. _管理者_ サイドバーで、**[!UICONTROL System]**/**[!UICONTROL Cache Management]** に移動します。
1. 「**[!UICONTROL Flush Cache]**」をクリックして、無効なキャッシュをすべて更新します。

キャッシュ管理テーブルのキャッシュ タイプのステータスが `INVALIDATED` の場合、ストアにはその項目の最新の構成が表示されないことがあります。 キャッシュをフラッシュしてストアを更新し、最新の設定を表示します。

ストアが正しい設定を表示していることを確認するには、定期的に [ キャッシュをフラッシュ ](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/tools/cache-management) します。

## カードボルト

顧客が今後の購入に使用できるように、マイアカウントにクレジットカード情報を保管（または「保存」）できる機能を有効にできます。

また、管理者でカードボルトを使用して、既存の顧客の後続の注文を完了することもできます。

[ クレジットカードのフィールド設定 ](#credit-card-fields) でカードボルトを有効または無効にします。

詳しくは、[ クレジットカードボルト ](vaulting.md) を参照してください。

## 3DS

3DS は、店舗での詐欺行為から顧客や商人を保護し、欧州連合（EU）規格への準拠を可能にします。

[ クレジットカードのフィールド設定 ](#credit-card-fields) で 3DS を有効または無効にします。

詳しくは、「セキュリティ」の [3DS](security.md#3ds) を参照してください。

## 複数の PayPal アカウントの使用

ま [!UICONTROL Payment Services]、web サイトレベルの **one** マーチャントアカウント内で複数の PayPal アカウントを使用できます。 例えば、複数の国（異なる [ 通貨 ](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/site-store/currency/currency) を使用している）で店舗を運営している場合や、ビジネスの一部で _すべて_ ではなくAdobe Commerceを使用したい場合は、複数の PayPal アカウントを使用するようにマーチャントアカウントを設定できます。

Web サイト、ストア、ストア表示の階層について詳しくは、[ サイト、ストア、表示範囲 ](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=ja) を参照してください。

CLI を使用した複数の PayPal アカウントのスコープの設定について詳しくは、[ コマンドライン設定 ](configure-cli.md#configure-scope-via-cli) を参照してください。

営業担当は、マーチャントアカウントに新しい [ 範囲 ](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=ja#scope-settings) を作成し、PayPal を使用して追加のサイトをオンボーディングできるので、表示するように設定した PayPal ボタンをサイトに表示できます。 Web サイトで複数の PayPal アカウントを使用する場合は、販売担当者にお問い合わせください。
