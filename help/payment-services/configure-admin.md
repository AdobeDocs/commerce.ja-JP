---
title: '[!DNL Payment Services] 設定'
description: インストール後、ストア設定の管理  [!DNL Payment Services]  で設定を行うことができます。
role: Admin, User
level: Intermediate
exl-id: e1a3269d-bdf9-4b0f-972f-e8a0ef469503
feature: Payments, Checkout, Configuration
source-git-commit: 6727102c54e0ac81df289ecd66ec61156662b8b9
workflow-type: tm+mt
source-wordcount: '3209'
ht-degree: 0%

---

# [!DNL Payment Services] 設定

管理者の役に立つ設定オプションを使用して、ニーズに合わせて [!DNL Payment Services] をカスタマイズできます。

管理者で [!DNL Payment Services] と [!DNL Adobe Commerce] に対して [!DNL Magento Open Source] を設定する場合、これらの設定は、_[!UICONTROL Method]_&#x200B;の_[!UICONTROL General Configuration]_ フィールドに設定された環境にのみ適用されます。 設定フィールドで行う変更は、_[!UICONTROL Method]_&#x200B;の選択の切り替えとは無関係です。メソッドを切り替えても、選択はリセットされません。

## 一般設定

ストアと [!DNL Payment Services] ージに対して _[!UICONTROL Merchant Location]_&#x200B;を有効にし、「_[!UICONTROL General Configuration]_」セクションでサンドボックステストまたはライブ支払いを有効にできます。

1. _管理者_ サイドバーで、**[!UICONTROL Stores]**/_[!UICONTROL Settings]_/**[!UICONTROL Configuration]**&#x200B;に移動します。
1. 左側のパネルで「**[!UICONTROL Sales]**」を展開し、「**[!UICONTROL Payment Methods]**」を選択します。
1. _[!UICONTROL Merchant Country]_&#x200B;で「_[!UICONTROL Merchant Location]_」フィールドを設定します。 _[!UICONTROL Merchant Country]_&#x200B;を指定しない場合は、一般設定の&#x200B;_[!UICONTROL Default Country]_ が使用されます。
1. 「_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_」セクションを展開して、「_[!UICONTROL [!DNL Payment Services]]_」セクションにアクセスします。
1. 「_[!UICONTROL [!DNL Payment Services]]_」セクションで、「_[!UICONTROL General Configuration]_」セクションを展開します。
1. **有効** の場合は、`Yes` に設定して、ストアに対して [!DNL Payment Services] を有効にします。
1. **メソッド** については、ストアで `Sandbox` をテストしている場合は [!DNL Payment Services] に、ライブ支払いを有効にする準備ができている場合は `Production` に設定します。
1. **[!UICONTROL Payment Services Sandbox ID]** と **[!UICONTROL Payment Services Production ID]** の値は、[Commerce サービスコネクタを設定し &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-merchant-services/user-guides/integration-services/saas){target=_blank} 初めて [!DNL Payment Services] ダッシュボードにアクセスすると自動入力されます。 サンドボックス環境や実稼動環境のオンボーディングを完了するには、これを行います。 これらの値は、SaaS ID を [!DNL Payment Services] に関連付けます。

   >[!WARNING]
   >
   > Commerce サービスコネクタでデータスペース ID を変更する必要がある場合は、[!DNL Payment Services] ID をリセットする必要があります。 「**支払いサービス ID をリセット**」をクリックして、サンドボックス ID をリセットします。 [!DNL Payment Services] サンドボックス ID をリセットした場合は、もう一度オンボードする必要があります。

1. **[!UICONTROL PayPal Merchant ID]** と **[!UICONTROL PayPal Merchant Status]** の値は、[!DNL Payment Services] ダッシュボードに初めてアクセスすると、PayPal によって自動的に提供されます。
1. **ソフト記述子** （顧客トランザクションの銀行取引明細書に表示されてストア/ブランド/カタログ間を区別するカスタム値）の場合は、カスタムテキスト（最大 22 文字）をテキストフィールドに追加して、`Soft descriptor` または既存の値に置き換えます。
1. 「**[!UICONTROL Save Config]**」をクリックして変更を保存します。
1. **[!UICONTROL System]** / **[!UICONTROL Cache Management]** に移動し、**[!UICONTROL Flush Cache]** をクリックして、無効なキャッシュをすべて更新します。

### 設定オプション

| フィールド | 範囲 | 説明 |
|---|---|---|
| [!UICONTROL Enable] | web サイト | Web サイトの [!DNL Payment Services] を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Method] | ストア表示 | ストアのメソッド（環境）を設定します。 オプション：[!UICONTROL Sandbox] / [!UICONTROL Production] |
| [!UICONTROL Payment Services Sandbox ID] | ストア表示 | サンドボックスオンボーディング中に自動生成されるサンドボックスマーチャント ID。 |
| [!UICONTROL Payment Services Production ID] | ストア表示 | 実稼動（ライブ）オンボーディング中に自動生成される実稼動マーチャント ID。 |
| [!UICONTROL PayPal Merchant ID] | ストア表示 | PayPal アカウントの作成時に生成される、一意の PayPal マーチャントアカウント ID。 |
| [!UICONTROL PayPal Merchant Status] | ストア表示 | PayPal マーチャント ID のステータス。 |
| [!UICONTROL Soft Descriptor] | web サイトまたはストア表示 | Web サイトおよびストアビューにソフト記述子を追加して、ブランド、ストアまたは製品ラインを区別する顧客トランザクションに情報を追加します。 |

## [!UICONTROL Credit Card Fields]

[!UICONTROL Credit Card Fields] の支払いオプションは、クレジットカードまたはデビットカードの支払い方法のためのシンプルで安全なチェックアウトを提供します。

詳しくは、[&#x200B; 支払いオプション &#x200B;](payments-options.md#paypal-smart-buttons) を参照してください。

1. _管理者_ サイドバーで、**[!UICONTROL Stores]**/_[!UICONTROL Settings]_/**[!UICONTROL Configuration]**&#x200B;に移動します。
1. 左側のパネルで「**[!UICONTROL Sales]**」を展開し、「**[!UICONTROL Payment Methods]**」を選択します。
1. 「_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_」セクションを展開します。
1. 「_[!UICONTROL Payment Services]_」セクションで、「_[!UICONTROL Credit Card Fields]_」セクションを展開します。
1. **[!UICONTROL Title]**：必要に応じてテキストを入力し、チェックアウト時に表示される支払い方法の名前を変更します。
1. [&#x200B; 支払い処理の設定 &#x200B;](production.md#set-payment-services-as-payment-method) を行うには、「**[!UICONTROL Authorize]**」または **「承認して取得** を選択します。
1. チェックアウトページで支払い方法に優先順位を付けるには、「`Numeric Only`」フィールドに **[!UICONTROL Sort order]** 値を入力します。
1. **[!UICONTROL Show on checkout page]** しくは、「`Yes`」を選択して、チェックアウトページでクレジットカードフィールドを有効にします。
1. **[!UICONTROL Vault Enabled]**: チェックアウト時にクレジット・カードのヴォールティングを有効にする場合は、「`Yes`」を選択します。
1. **[!UICONTROL Vault Enabled in Admin]** に、加盟店がボールトに登録されたクレジット カードを使用して顧客の注文を作成できるようにする `Yes` を選択します。
1. **[!UICONTROL 3D Secure authentication]** を有効にするには（デフォルトでは `Off`）、「`Always`」または「`When required`」を選択します。
1. **[!UICONTROL Debug Mode]**: デバッグモードを有効にするには `Yes` を選択し、無効にするには `No` を選択します。
1. 「**[!UICONTROL Save Config]**」をクリックして変更を保存します。
1. **[!UICONTROL System]** / **[!UICONTROL Cache Management]** に移動し、**[!UICONTROL Flush Cache]** をクリックして、無効なキャッシュをすべて更新します。

### 設定オプション

| フィールド | 範囲 | 説明 |
|---|---|---|
| [!UICONTROL Title] | ストア表示 | チェックアウト時に支払い方法ビューでこの支払いオプションのタイトルとして表示するテキストを追加します。 オプション：[!UICONTROL text field] |
| [!UICONTROL Payment Action] | web サイト | 指定した支払方法の [&#x200B; 支払アクション &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=ja)。 オプション：[!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | ストア表示 | チェックアウトページでの指定した支払い方法の並べ替え順。 `Numeric Only` 値 |
| [!UICONTROL Show on checkout page] | web サイト | チェックアウトページのクレジットカードフィールドを有効または無効にします。 オプション：[!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled] | ストア表示 | [&#x200B; クレジット カードの保管 &#x200B;](vaulting.md) を有効または無効にします。 オプション：[!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled in Admin] | ストア表示 | [&#x200B; マーチャントが管理でボルト付き支払い方法を使用して顧客の注文を完了する &#x200B;](vaulting.md) 機能を有効または無効にします。 オプション：[!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL 3D Secure authentication] | web サイト | [3DS セキュア認証 &#x200B;](security.md#3ds) を有効または無効にします。 オプション：[!UICONTROL Always]/[!UICONTROL When Required]/[!UICONTROL Off] |
| [!UICONTROL Debug Mode] | web サイト | デバッグモードを有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Fastlane]

[[!DNL Fastlane by PayPal]](https://www.paypal.com/us/cshelp/article/what-is-fastlane-by-paypal-help1096) は、オンラインで安全に支払うための迅速かつ簡単な方法です。 **ゲストのチェックアウト** 中に、カードと配送の詳細を安全に保存して、今後はさらに迅速に購入できます。

詳しくは、[&#x200B; 支払いオプション &#x200B;](payments-options.md#fastlane-button) を参照してください。

1. _管理者_ サイドバーで、**[!UICONTROL Stores]**/_[!UICONTROL Settings]_/**[!UICONTROL Configuration]**&#x200B;に移動します。
1. 左側のパネルで「**[!UICONTROL Sales]**」を展開し、「**[!UICONTROL Payment Methods]**」を選択します。
1. 「_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_」セクションを展開します。
1. 「_[!UICONTROL Payment Services]_」セクションで、「_[!UICONTROL Fastlane]_」セクションを展開します。
1. 有効にするには、`Yes` の **[!UICONTROL Enable Fastlane]** を選択します（`No` は無効にします）。

   >[!NOTE]
   >
   > [!UICONTROL Fastlane] が有効になっている場合、[!UICONTROL Credit Card Fields] 支払いオプションは無効になります。

1. **[!UICONTROL Title]**：必要に応じてテキストを入力し、チェックアウト時に表示される支払い方法の名前を変更します。 デフォルトのタイトルは `Credit Card (via Fastlane)` です。
1. [&#x200B; 支払い処理の設定 &#x200B;](production.md#set-payment-services-as-payment-method) を行うには、「**[!UICONTROL Authorize]**」または **「承認して取得** を選択します。
1. **[!UICONTROL 3D Secure Authentication for Fastlane]** （デフォルトで `Off`）を有効にするには、EU 規制に準拠する `When required` を選択するか、不正防止レイヤーを追加する `Always` を選択します。

   >[!NOTE]
   >
   > カード発行者が 3D セキュア認証を必要とする場合、[!UICONTROL Payment Services] の設定に関係なく、この手順を回避することはできません。

1. チェックアウトページで支払い方法に優先順位を付けるには、「`Numeric Only`」フィールドに **[!UICONTROL Sort order]** 値を入力します。
1. [!UICONTROL Fastlane] フィールドを **[!UICONTROL Enable messaging]** に設定して、Adobe Commerceのチェックアウト時に `Yes` ブランディングを有効にするかどうかを指定します。
1. 「**[!UICONTROL Save Config]**」をクリックして変更を保存します。
1. **[!UICONTROL System]** / **[!UICONTROL Cache Management]** に移動し、**[!UICONTROL Flush Cache]** をクリックして、無効なキャッシュをすべて更新します。

| フィールド | 範囲 | 説明 |
|---|---|---|
| [!UICONTROL Enable Fastlane] | ストア表示 | チェックアウトページで [!DNL Fastlane] を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Title] | ストア表示 | チェックアウト時に支払い方法ビューでこの支払いオプションのタイトルとして表示するテキストを追加します。 デフォルト値は `Credit Card (via Fastlane)` です。 オプション：[!UICONTROL text field] |
| [!UICONTROL Payment Action] | web サイト | 指定した支払方法の [&#x200B; 支払アクション &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=ja)。 オプション：[!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL 3D Secure authentication] | ストア表示 | Fastlane[&#x200B; の &#x200B;](security.md#3ds)3D セキュア認証を有効または無効にします。 オプション：[!UICONTROL Always]/[!UICONTROL When Required]/[!UICONTROL Off] |
| [!UICONTROL Sort order] | ストア表示 | チェックアウトページでの指定した支払い方法の並べ替え順。 `Numeric Only` 値 |
| [!UICONTROL Enable messaging] | ストア表示 | Adobe Commerceでのチェックアウト時に [!UICONTROL Fastlane] ブランディングを有効にするかどうかを指定します。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |

### オプション。 スタイルの詳細設定

これらのオプション設定により、Web サイトでの [!UICONTROL Fastlane] の表示方法をカスタマイズできます。

>[!TIP]
>
>アクセシビリティガイドラインを満たさないスタイルは、デフォルト設定に戻ります。

1. 「_[!UICONTROL Payment Services]_」セクションで、「_[!UICONTROL Fastlane]_」セクションに移動します。
1. 「_[!UICONTROL Advanced Style Settings (optional)]_」セクションを展開します。
1. 必要に応じて設定を変更します。
1. 「**[!UICONTROL Save Config]**」をクリックして変更を保存します。

カスタマイズについて詳しくは、[PayPal 開発者向けドキュメント &#x200B;](https://developer.paypal.com/limited-release/accelerated-checkout-bt/) を参照してください。

#### ルート設定

これらのオプション設定により、[!UICONTROL Fastlane] チェックアウトコンポーネント全体が変更されます。

| フィールド | 範囲 | 説明 |
|---|---|---|
| [!UICONTROL Background Color] | ストア表示 | コンポーネントの背景色を定義します。 `RGB` 値のみ |
| [!UICONTROL Border Color] | ストア表示 | コンポーネントのボーダーの色を定義します。 `RGB` 値のみ |
| [!UICONTROL Font Family] | ストア表示 | コンポーネントのフォントを設定します。 テーマで使用可能なフォントのみが表示されます |
| [!UICONTROL Font Size Base] | ストア表示 | フォントのサイズを定義します。 `px` （ピクセル）値のみ |
| [!UICONTROL Padding] | ストア表示 | コンポーネントのパディングを設定します。 `px` （ピクセル）値のみ |
| [!UICONTROL Primary Color] | ストア表示 | コンポーネントのメインカラーを定義します。 `RGB` 値のみ |
| [!UICONTROL Text Color] | ストア表示 | コンポーネントのテキストのメインカラーを定義します。 `RGB` 値のみ |

#### 入力設定

これらのオプション設定は、[!UICONTROL Fastlane] コンポーネントの顧客入力フィールドに適用されます。

| フィールド | 範囲 | 説明 |
|---|---|---|
| [!UICONTROL Background Color] | ストア表示 | コンポーネントの背景色を定義します。 `RGB` 値のみ |
| [!UICONTROL Border Color] | ストア表示 | コンポーネントのボーダーの色を定義します。 `RGB` 値のみ |
| [!UICONTROL Border Radius] | ストア表示 | 境界線の半径を定義します。 `px` （ピクセル）値のみ |
| [!UICONTROL Border Width] | ストア表示 | 境界線の幅を定義します。 `px` （ピクセル）値のみ |
| [!UICONTROL Focus Border Color] | ストア表示 | コンポーネントのフォーカス境界線の色を定義します。 `RGB` 値のみ |
| [!UICONTROL Text Color Base] | ストア表示 | コンポーネントのテキストのメインカラーを定義します。 `RGB` 値のみ |

## [!UICONTROL Apple Pay]

[!DNL Apple Pay] を使用すると、マーチャントは、Safari で安全で迅速かつシームレスなチェックアウトエクスペリエンスを提供でき、マーチャントアカウントあたり最大 99 のドメインをサポートできます。 [!DNL Apple Pay] ボタンを押すと、顧客のiOSまたはmacOS デバイスから支払い、連絡先、配送情報が自動的に入力され、ワンタップで素早く購入できるので、コンバージョン率を高めることができます。

>[!IMPORTANT]
>
> Appleが未確認のドメインからの支払いを拒否します。 マーチャントは、Apple Pay ボタンが使用されているドメインを検証する必要があります。 国の制限が適用されます。 ドメインの検証要件について詳しくは、[Apple Pay のドキュメント &#x200B;](https://developer.apple.com/documentation/apple_pay_on_the_web) を参照してください。

詳しくは、[&#x200B; 支払いオプション &#x200B;](payments-options.md#apple-pay-button) を参照してください。

1. _管理者_ サイドバーで、**[!UICONTROL Stores]**/_[!UICONTROL Settings]_/**[!UICONTROL Configuration]**&#x200B;に移動します。
1. 左側のパネルで「**[!UICONTROL Sales]**」を展開し、「**[!UICONTROL Payment Methods]**」を選択します。
1. 「_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_」セクションを展開します。
1. 「_[!UICONTROL Payment Services]_」セクションで、「_[!UICONTROL Apple Pay]_」セクションを展開します。
1. **[!UICONTROL Title]**：必要に応じてテキストを入力し、チェックアウト時に表示される支払い方法の名前を変更します。
1. [&#x200B; 支払いアクションを設定 &#x200B;](production.md#set-payment-services-as-payment-method) するには、「**[!UICONTROL Authorize]**」または「**[!UICONTROL Authorize and Capture]**」を選択します。
1. 必要に応じて次のオプションの「[!DNL Apple Pay]」を選択して、Adobe Commerceで `Yes` オプションを有効にする場所を指定します。
   * **[!UICONTROL Show Apple Pay on checkout page]**
   * **[!UICONTROL Show Apple Pay at start of checkout]**
   * **[!UICONTROL Show Apple Pay on product detail page]**
   * **[!UICONTROL Show Apple Pay in mini cart preview]**
   * **[!UICONTROL Show Apple Pay on cart page]**
1. デバッグモードを有効にするには、`Yes` の **[!UICONTROL Debug Mode]** を選択します（`No` は無効にします）。
1. 変更を保存するには、「**[!UICONTROL Save Config]**」をクリックします。
1. **[!UICONTROL System]** / **[!UICONTROL Cache Management]** に移動し、**[!UICONTROL Flush Cache]** をクリックして、無効なキャッシュをすべて更新します。

### 設定オプション

| フィールド | 範囲 | 説明 |
|---|---|---|
| [!UICONTROL Title] | ストア表示 | チェックアウト時に支払い方法ビューでこの支払いオプションのタイトルとして表示するテキストを追加します。 オプション：[!UICONTROL text field] |
| [!UICONTROL Payment Action] | web サイト | 指定した支払方法の [&#x200B; 支払アクション &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=ja)。 オプション：[!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Show Apple Pay on checkout page] | web サイト | チェックアウトページで [!DNL Apple Pay] を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Apple Pay at start of checkout] | ストア表示 | チェックアウトフローの開始時に [!DNL Apple Pay] を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | ストア表示 | チェックアウトページでの指定した支払い方法の並べ替え順。 `Numeric Only` 値 |
| [!UICONTROL Show Apple Pay on product detail page] | ストア表示 | 製品の詳細ページで [!DNL Apple Pay] を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Apple Pay in mini cart preview] | ストア表示 | ミニ買い物かごのプレビューで [!DNL Apple Pay] を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Apple Pay on cart page] | ストア表示 | 買い物かごページの [!DNL Apple Pay] のチェックインを有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | web サイト | デバッグモードを有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Google Pay]

[!UICONTROL Google Pay] 支払いオプションを使用すると、マーチャントは買い物客にGoogle Pay を提供でき、買い物客はデバイスでGoogle Wallet を使用して購入できます。

詳しくは、[&#x200B; 支払いオプション &#x200B;](payments-options.md#google-pay-button) を参照してください。

1. _管理者_ サイドバーで、**[!UICONTROL Stores]**/_[!UICONTROL Settings]_/**[!UICONTROL Configuration]**&#x200B;に移動します。
1. 左側のパネルで「**[!UICONTROL Sales]**」を展開し、「**[!UICONTROL Payment Methods]**」を選択します。
1. 「_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_」セクションを展開します。
1. 「_[!UICONTROL Payment Services]_」セクションで、「_[!UICONTROL Google Pay]_」セクションを展開します。
1. （オプション） **[!UICONTROL Title]** フィールドに新しい名前を入力して、チェックアウト時に表示される支払い方法の名前を変更します。
1. [&#x200B; 支払いアクションを設定 &#x200B;](production.md#set-payment-services-as-payment-method) するには、**[!UICONTROL Authorize]** または **[!UICONTROL Authorize and Capture]** を選択します。
1. 必要に応じて次のオプションの「[!DNL Google Pay]」を選択して、Adobe Commerceで `Yes` オプションを有効にする場所を指定します。
   * **[!UICONTROL Show Google Pay on checkout page]**
   * **[!UICONTROL Show Google Pay at start of checkout]**
   * **[!UICONTROL Show Google Pay on product detail page]**
   * **[!UICONTROL Show Google Pay in mini cart preview]**
   * **[!UICONTROL Show Google Pay on cart page]**
1. **[!UICONTROL 3D Secure authentication]** を有効にするには（デフォルトでは `Off`）、「`Always`」または「`When required`」を選択します。
1. デバッグモードを有効にするには、`Yes` の **[!UICONTROL Debug Mode]** を選択します（`No` は無効にします）。
1. 必要に応じて _[!UICONTROL Google Pay]_、**[!UICONTROL Button Color]**、**[!UICONTROL Button Type]**&#x200B;を選択して、「**[!UICONTROL Button Style]**」ボタンの外観を設定します。
1. 高さを設定するには、**[!UICONTROL Button Style]** で定義された高さの既定値を使用します。
1. 変更を保存するには、「**[!UICONTROL Save Config]**」をクリックします。
1. **[!UICONTROL System]** / **[!UICONTROL Cache Management]** に移動し、**[!UICONTROL Flush Cache]** をクリックして、無効なキャッシュをすべて更新します。

### 設定オプション

| フィールド | 範囲 | 説明 |
|---|---|---|
| [!UICONTROL Title] | ストア表示 | チェックアウト時に支払い方法ビューでこの支払いオプションに表示されるテキスト ラベルを指定します。 オプション：`[!UICONTROL text field]` |
| [!UICONTROL Payment Action] | web サイト | 指定した支払方法の [&#x200B; 支払アクション &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=ja)。 オプション：`[!UICONTROL Authorize]` / `[!UICONTROL Authorize and Capture]` |
| [!UICONTROL Show Google Pay on checkout page] | web サイト | チェックアウトページで [!DNL Google Pay] を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Google Pay at start of checkout] | ストア表示 | チェックアウトフローの開始時に [!DNL Google Pay] を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | ストア表示 | チェックアウトページでの指定した支払い方法の並べ替え順。 `Numeric Only` 値 |
| [!UICONTROL Show Google Pay on product detail page] | ストア表示 | 製品の詳細ページで [!DNL Google Pay] を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Google Pay in mini cart preview] | ストア表示 | ミニ買い物かごのプレビューで [!DNL Google Pay] を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Google Pay on cart page] | ストア表示 | 買い物かごページの [!DNL Google Pay] を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL 3D Secure authentication] | ストア表示 | [3D セキュア認証 &#x200B;](security.md#3ds) を有効または無効にします。 オプション：[!UICONTROL Always]/[!UICONTROL When Required]/[!UICONTROL Off] |
| [!UICONTROL Debug Mode] | web サイト | デバッグモードを有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Button Color] | ストア表示 | 「[!DNL Google Pay]」ボタンの色を定義します。 オプション：`[!UICONTROL Default]`/`[!UICONTROL Black]`/`[!UICONTROL White]` |
| [!UICONTROL Button Type] | ストア表示 | 「[!DNL Google Pay]」ボタンのタイプを定義します。 オプション：`[!UICONTROL buy]` / `[!UICONTROL checkout]` / `[!UICONTROL order]` / `[!UICONTROL pay]` / `[!UICONTROL plain]` |

詳しくは、[Google Pay API リクエストオブジェクトオプション &#x200B;](https://developers.google.com/pay/api/web/reference/request-objects) ドキュメントを参照してください。

## [!DNL PayPal Payment Buttons]

[!DNL PayPal payment buttons] の支払いオプションは、顧客にシンプルで迅速かつ安全なチェックアウトプロセスを提供します。

詳しくは、[&#x200B; 支払いオプション &#x200B;](payments-options.md#paypal-smart-buttons) を参照してください。

[!DNL PayPal payment buttons] の設定

PayPal 支払いボタンの支払いオプションを管理内で有効にして設定できます。

1. _管理者_ サイドバーで、**[!UICONTROL Stores]**/_[!UICONTROL Settings]_/**[!UICONTROL Configuration]**&#x200B;に移動します。
1. 左側のパネルで「**[!UICONTROL Sales]**」を展開し、「**[!UICONTROL Payment Methods]**」を選択します。
1. 「_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_」セクションを展開します。
1. 「_[!UICONTROL Payment Services]_」セクションで、「_[!UICONTROL PayPal payment buttons]_」セクションを展開します。
1. チェックアウト時に表示される支払い方法の名前を変更するには、「_[!UICONTROL Title]_」フィールドを編集します。
1. [&#x200B; 支払いアクションを設定 &#x200B;](production.md#set-payment-services-as-payment-method) するには、「**[!UICONTROL Authorize]**」または「**[!UICONTROL Authorize and Capture]**」を選択します。
1. チェックアウトページで支払い方法に優先順位を付けるには、「`Numeric Only`」フィールドに **[!UICONTROL Sort order]** 値を入力します。
1. [&#x200B; 後で支払うメッセージ &#x200B;](payments-options.md#pay-later-button) を有効/無効にするには、`Yes` で `No`/**[!UICONTROL Display Pay Later Message]** を選択します。

   * [&#x200B; 後で支払うメッセージ &#x200B;](payments-options.md#pay-later-button) を有効にすると、**[!UICONTROL Configure Messaging]** モーダル ボタンが表示され、**[!UICONTROL PayPal Pay Later messaging]** のスタイルを設定できます。

1. 必要に応じて次のオプションの `Yes` を選択して、Adobe Commerceで PayPal 支払いボタンを有効にする場所を指定します。
   * **[!UICONTROL Show buttons on checkout page]**
   * **[!UICONTROL Show buttons at start of checkout]**
   * **[!UICONTROL Show buttons on product detail page]**
   * **[!UICONTROL Show buttons in mini cart preview]**
   * **[!UICONTROL Show buttons on cart page]**
1. Venmo を支払いオプションとして有効にするには、`Yes` に「**[!UICONTROL Venmo Enabled]**」を選択します。
1. クレジットカードとデビットカードを支払いオプションとして有効にするには（PayPal スマートボタン）、「`Yes`」で「**[!UICONTROL Credit and Debit Card Enabled]**」を選択します。
1. [PayPal Pay Later](payments-options.md#pay-later-button) 支払いオプションを有効/無効にするには、`Yes` の `No`/**[!UICONTROL PayPal Pay Later Enabled]** を選択します。
1. デバッグモードを有効にするには、`Yes` の **[!UICONTROL Debug Mode]** を選択します（`No` は無効にします）。
1. 変更を保存するには、「**[!UICONTROL Save Config]**」をクリックします。
1. **[!UICONTROL System]** / **[!UICONTROL Cache Management]** に移動し、**[!UICONTROL Flush Cache]** をクリックして、無効なキャッシュをすべて更新します。

### 設定オプション

| フィールド | 範囲 | 説明 |
|---|---|---|
| [!UICONTROL Title] | ストア表示 | チェックアウト時に支払い方法ビューでこの支払いオプションのタイトルとして表示するテキストを追加します。 オプション：テキストフィールド |
| [!UICONTROL Payment Action] | web サイト | 指定した支払方法の [&#x200B; 支払アクション &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"}。 オプション：[!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Display Pay Later Message] | web サイト | 買い物かご、製品ページ、ミニカート、およびチェックアウトフロー中の PayPal Pay Later メッセージを有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Configure Messaging] | ストア表示 | PayPal Pay Later メッセージスタイルを変更します。 オプション：`[!UICONTROL Product page]` / `[!UICONTROL Cart]` |
| [!UICONTROL Show buttons on checkout page] | ストア表示 | チェックアウトページで [!DNL PayPal payment buttons] を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons at start of checkout] | ストア表示 | チェックアウトフローの開始時に [!DNL PayPal payment buttons] を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | ストア表示 | チェックアウトページでの指定した支払い方法の並べ替え順。 `Numeric Only` 値 |
| [!UICONTROL Show buttons on product detail page] | ストア表示 | 製品の詳細ページで [!DNL PayPal payment buttons] を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini cart preview] | ストア表示 | ミニ買い物かごのプレビューで [!DNL PayPal payment buttons] を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | ストア表示 | 買い物かごページの [!DNL PayPal payment buttons] のチェックインを有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL App Switch] | ストア表示 | このオプションは、**米国** のマーチャントおよびバイヤーにのみ適用されます。 有効にすると、すべての Express PayPal 支払いは、利用可能な場合は PayPal モバイルアプリを通過しようとします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Contact Preference] | ストア表示 | このオプションは、**米国** のマーチャントおよびバイヤーにのみ適用されます。 **はい** に設定すると、購入者の電子メールと電話番号が PayPal 支払いモーダルに表示されます。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Venmo Enabled] | ストア表示 | 支払ボタンが表示される Venmo 支払オプションを有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Credit and Debit Card Enabled] | ストア表示 | 支払いボタンが表示されるクレジット カードおよびデビット カード オプションを有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL PayPal Pay Later Enabled] | ストア表示 | 支払いボタンが表示される PayPal Pay Later 支払いオプションの外観を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | web サイト | デバッグモードを有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |

## 現地の支払方法

地域決済方法（LPM）は、既存のカードベースのオプションと共に、銀行振込やローカライズされた支払いソリューションなど、地域固有および地域固有の支払い方法をサポートします。 マーチャントは、Commerce設定内で直接利用可能な LPM を有効または無効にできます。 使用可能な方法について詳しくは、[&#x200B; 支払いオプション &#x200B;](payments-options.md#local-payment-methods) を参照してください。

1. _管理者_ サイドバーで、**[!UICONTROL Stores]**/_[!UICONTROL Settings]_/**[!UICONTROL Configuration]**&#x200B;に移動します。
1. 左側のパネルで「**[!UICONTROL Sales]**」を展開し、「**[!UICONTROL Payment Methods]**」を選択します。
1. 「_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_」セクションを展開します。
1. 「_[!UICONTROL Payment Services]_」セクションで、「_[!UICONTROL Local Payment Methods]_」セクションを展開します。
1. **[!UICONTROL Active]**: LPM を有効にする場合は「`Yes`」、無効にする場合は「`No`」を選択します。
1. **[!UICONTROL Title]**：チェックアウト時に支払方法名として表示するテキストを入力します。 このタイトルは、販売注文グリッドにも表示されます。
1. **[!UICONTROL Allowed Payment Methods]**：提供する支払い方法を選択します。 使用できる方法は、購入者の請求先住所と web サイトのベース通貨によって異なります。
1. **[!UICONTROL Sort Order]**：使用可能な支払方法のリスト内の LPM の表示位置を決定する数値を入力します。
1. 変更を保存するには、「**[!UICONTROL Save Config]**」をクリックします。
1. **[!UICONTROL System]** / **[!UICONTROL Cache Management]** に移動し、**[!UICONTROL Flush Cache]** をクリックして、無効なキャッシュをすべて更新します。

### 設定オプション

| フィールド | 範囲 | 説明 |
|---|---|---|
| [!UICONTROL Active] | web サイト | ローカル支払方法を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Title] | ストア表示 | チェックアウト時および販売注文グリッドに表示される支払方法名。 オプション：[!UICONTROL text field] |
| [!UICONTROL Allowed Payment Methods] | web サイト | 提供する LPM を選択します。 メソッドは、請求先住所と web サイトの通貨がメソッドの要件に一致する顧客にのみ表示されます。 オプション：`Bancontact` / `BLIK` / `eps` / `iDEAL` / `MyBank` / `Przelewy24` |
| [!UICONTROL Sort Order] | ストア表示 | 使用可能な支払方法のリスト内の LPM グループの表示位置。 この設定は、すべての LPM をグループとして適用します。個々の LPM を個別に並べ替えることはできません。 `Numeric Only` 値 |

>[!NOTE]
>
>それぞれの現地支払い方法（LPM）には、特定の国と通貨の要件があります。 支払い方法は、顧客の請求先住所の国と web サイトの基本通貨がこれらの要件に一致する場合にのみ表示されます。 例えば、Bancontact は、基本通貨が EUR の場合、ベルギーの請求先住所を持つ顧客に対してのみ表示されます。

## ライン項目

明細品目は、製品の詳細、数量、価格などの詳細な注文情報を PayPal に送信します。 この機能はデフォルトで有効になっています。 詳しくは、[&#x200B; 行項目 &#x200B;](line-items.md) を参照してください。

### 設定オプション

| フィールド | 範囲 | 説明 |
|---|---|---|
| [!UICONTROL Line Items Enabled] | web サイト | PayPal への行項目および金額の分類の送信を有効または無効にします。 [!DNL Payment Services] でサポートされていないカスタム料金を追加するサードパーティの拡張機能を使用する場合は、この設定を無効にしてください。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |

## ボタンのスタイル

また、支払いボタンの _[!UICONTROL Button style]_&#x200B;のオプションを設定することもできます。

1. _管理者_ サイドバーで、**[!UICONTROL Stores]**/_[!UICONTROL Settings]_/**[!UICONTROL Configuration]**&#x200B;に移動します。
1. 左側のパネルで「**[!UICONTROL Sales]**」を展開し、「**[!UICONTROL Payment Methods]**」を選択します。
1. 「_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_」セクションを展開します。
1. 「_[!UICONTROL [!DNL Payment Services]]_」セクションで、「_[!UICONTROL PayPal Smart Button Styling]_」セクションを展開します。
1. レイアウトを設定するには、`Vertical` に `Horizontal` または **[!UICONTROL Layout]** を選択します
1. 色を設定するには、**[!UICONTROL Color]** で使用可能な色から選択します。
1. 形状を設定するには、`Rectangular` に `Pill` または **[!UICONTROL Shape]** を選択します。
1. デフォルトの高さを使用するには、`Yes` に `No` または **[!UICONTROL Use Default Height]** を選択します。
1. カスタムの高さを設定するには、**[!UICONTROL Height]** に希望のピクセル高さを追加します。
1. タグラインを設定するには、「`Yes`」で「`No`」または「**[!UICONTROL Tagline]**」を選択します。
1. 変更を保存するには、「**[!UICONTROL Save Config]**」をクリックします。
1. **[!UICONTROL System]** / **[!UICONTROL Cache Management]** に移動し、**[!UICONTROL Flush Cache]** をクリックして、無効なキャッシュをすべて更新します。

### 設定オプション

| フィールド | 範囲 | 説明 |
|--- |--- |--- |
| [!UICONTROL Layout] | ストア表示 | Paypal 支払いボタンのレイアウトのスタイルを定義します。 オプション：`[!UICONTROL Vertical]` / `[!UICONTROL Horizontal]` |
| [!UICONTROL Color] | ストア表示 | Paypal 支払いボタンの色を定義します。 オプション：[!UICONTROL Blue] / `[!UICONTROL Gold]` / `[!UICONTROL Silver]` / `[!UICONTROL White]` / `[!UICONTROL Black]` |
| [!UICONTROL Shape] | ストア表示 | Paypal 支払いボタンの形状を定義します。 オプション：`[!UICONTROL Rectangular]` / `[!UICONTROL Pill]` |
| [!UICONTROL Use Default Height] | ストア表示 | PayPal 支払いボタンでデフォルトの高さを使用するかどうかを定義します。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Height] | ストア表示 | PayPal 支払いボタンの高さを定義します。 デフォルト値：なし |
| [!UICONTROL Label] | ストア表示 | PayPal 支払いボタンに表示されるラベルを定義します。 オプション：`[!UICONTROL PayPal]` / `[!UICONTROL Checkout]` / `[!UICONTROL Buynow]` / `[!UICONTROL Pay]` / `[!UICONTROL Installment]` |
| [!UICONTROL Tagline] | ストア表示 | タグラインを有効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |

## キャッシュをフラッシュします

_設定_ で設定を変更した場合（例えば、Apple Pay、Venmo、または PayPal PayLater ボタンの切り替え）、キャッシュを手動でフラッシュして、ストアに最新の設定が表示されるようにします。

1. _管理者_ サイドバーで、**[!UICONTROL System]**/**[!UICONTROL Cache Management]** に移動します。
1. 「**[!UICONTROL Flush Cache]**」をクリックして、無効なキャッシュをすべて更新します。

キャッシュ管理テーブルのキャッシュ タイプのステータスが `INVALIDATED` の場合、ストアにはその項目の最新の構成が表示されないことがあります。 キャッシュをフラッシュしてストアを更新し、最新の設定を表示します。

ストアが正しい設定を表示していることを確認するには、定期的に [&#x200B; キャッシュをフラッシュ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/tools/cache-management) します。

## 役割の設定

管理者ユーザーがCommerce管理者で注文を作成および管理できるようにするには、[!DNL Payment Services] 固有のリソースをユーザーロールに対して有効にします。

役割の管理方法については、[&#x200B; ユーザーの役割 &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions-user-roles.html?lang=ja) を参照してください。

役割にリソースを割り当てる場合は、次を選択する必要があります。

* **[!DNL Payment Services]** を使用して支払う – このリソースにより、管理で注文を作成するときに、支払い方法として [!DNL Payment Services] のクレジットカードを使用できるようになります。 **アクション** 親リソースを選択すると、このリソースも選択されます。

* **[!DNL Payment Services]** – このリソースには、**Dashboard** リソースと **SaaS Services Proxy** リソースが含まれます。これらのリソースも選択する必要があります。 [!DNL Payment Services] が _Sales_ メニューに表示されます。

  ![&#x200B; 資金決済サービス資源 &#x200B;](assets/roles-payments.png){width="400" zoomable="yes"}


## カードボルト

顧客が今後の購入に使用できるように、マイアカウントにクレジットカード情報を保管（または「保存」）できる機能を有効にできます。

また、管理者でカードボルトを使用して、既存の顧客の後続の注文を完了することもできます。

[&#x200B; クレジットカードのフィールド設定 &#x200B;](#credit-card-fields) でカードボルトを有効または無効にします。

詳しくは、[&#x200B; クレジットカードボルト &#x200B;](vaulting.md) を参照してください。

## 3DS

3DS は、店舗での詐欺行為から顧客や商人を保護し、欧州連合（EU）規格への準拠を可能にします。

[&#x200B; クレジットカードのフィールド設定 &#x200B;](#credit-card-fields) で 3DS を有効または無効にします。

詳しくは、「セキュリティ」の [3DS](security.md#3ds) を参照してください。

## 複数の PayPal アカウントの使用

ま [!UICONTROL Payment Services]、web サイトレベルの **one** マーチャントアカウント内で複数の PayPal アカウントを使用できます。 例えば、複数の国（異なる [&#x200B; 通貨 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/site-store/currency/currency) を使用している）で店舗を運営している場合や、ビジネスの一部で _すべて_ ではなくAdobe Commerceを使用したい場合は、複数の PayPal アカウントを使用するようにマーチャントアカウントを設定できます。

Web サイト、ストア、ストア表示の階層について詳しくは、[&#x200B; サイト、ストア、表示範囲 &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=ja) を参照してください。

CLI を使用した複数の PayPal アカウントのスコープの設定について詳しくは、[&#x200B; コマンドライン設定 &#x200B;](configure-cli.md#configure-scope-via-cli) を参照してください。

営業担当は、マーチャントアカウントに新しい [&#x200B; 範囲 &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=ja#scope-settings) を作成し、PayPal を使用して追加のサイトをオンボーディングできるので、表示するように設定した PayPal ボタンをサイトに表示できます。 セールス部門に連絡
web サイトで複数の PayPal アカウントを使用する際のサポートのための担当者です。
