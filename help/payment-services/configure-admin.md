---
title: '[!DNL Payment Services]設定'
description: インストール後、ストア設定の管理者で [!DNL Payment Services] を設定できます。
role: Admin, User
level: Intermediate
exl-id: e1a3269d-bdf9-4b0f-972f-e8a0ef469503
feature: Payments, Checkout, Configuration
source-git-commit: 14c4178338859d55a7391139033d51d1aa6f7678
workflow-type: tm+mt
source-wordcount: '3209'
ht-degree: 0%

---

# [!DNL Payment Services]設定

管理者の便利な設定オプションを使用して、[!DNL Payment Services]をニーズに合わせてカスタマイズできます。

管理者で[!DNL Payment Services]および[!DNL Adobe Commerce]の[!DNL Magento Open Source]を設定する場合、これらの設定は&#x200B;_[!UICONTROL Method]_&#x200B;の_[!UICONTROL General Configuration]_ フィールドで設定されている環境にのみ適用されます。 設定フィールドで行った変更は、_[!UICONTROL Method]_&#x200B;の選択を切り替えることとは関係ありません。メソッドを切り替えた場合、選択はリセットされません。

## 一般設定

ストアと[!DNL Payment Services]に対して&#x200B;_[!UICONTROL Merchant Location]_&#x200B;を有効にし、_[!UICONTROL General Configuration]_ セクションでサンドボックステストまたはライブ支払いを有効にすることができます。

1. _管理者_ サイドバーで、**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**&#x200B;に移動します。
1. 左側のパネルで、**[!UICONTROL Sales]**&#x200B;を展開し、**[!UICONTROL Payment Methods]**&#x200B;を選択します。
1. _[!UICONTROL Merchant Country]_&#x200B;に_[!UICONTROL Merchant Location]_ フィールドを設定します。 _[!UICONTROL Merchant Country]_&#x200B;が指定されていない場合は、一般設定の&#x200B;_[!UICONTROL Default Country]_&#x200B;が使用されます。
1. _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;セクションを展開して、_[!UICONTROL [!DNL Payment Services]]_ セクションにアクセスします。
1. _[!UICONTROL [!DNL Payment Services]]_&#x200B;セクションで、_[!UICONTROL General Configuration]_ セクションを展開します。
1. **Enable**&#x200B;の場合は、ストアで`Yes`を有効にするために[!DNL Payment Services]に設定します。
1. **メソッド**&#x200B;の場合、ストアの`Sandbox`をまだテストしている場合は[!DNL Payment Services]に、ライブ支払いを有効にする準備ができている場合は`Production`に設定します。
1. **[!UICONTROL Payment Services Sandbox ID]**&#x200B;および&#x200B;**[!UICONTROL Payment Services Production ID]**&#x200B;の値は、[Commerce Services Connector](https://experienceleague.adobe.com/ja/docs/commerce-merchant-services/user-guides/integration-services/saas){target=_blank}を設定し、初めて[!DNL Payment Services] ダッシュボードにアクセスすると、自動的に入力されます。 これは、サンドボックスや実稼動環境のオンボーディングを完了するために実行します。 これらの値は、SaaS IDを[!DNL Payment Services]に関連付けます。

   >[!WARNING]
   >
   > Commerce Services Connectorでデータスペース IDを変更する必要がある場合は、[!DNL Payment Services] IDをリセットする必要があります。 「**決済サービス IDのリセット**」をクリックして、サンドボックス IDをリセットします。 [!DNL Payment Services] サンドボックス IDをリセットした場合は、再度オンボーディングする必要があります。

1. **[!UICONTROL PayPal Merchant ID]**&#x200B;と&#x200B;**[!UICONTROL PayPal Merchant Status]**&#x200B;の値は、初めて[!DNL Payment Services] ダッシュボードにアクセスすると、PayPalによって自動的に提供されます。
1. **ソフト記述子** （ストア/ブランド/カタログ間で区切る顧客トランザクション銀行取引明細書に表示されるカスタム値）の場合、`Soft descriptor`または既存の値を置き換えて、テキストフィールドにカスタムテキスト（最大22文字）を追加します。
1. **[!UICONTROL Save Config]**&#x200B;をクリックして変更を保存します。
1. **[!UICONTROL System]** > **[!UICONTROL Cache Management]**&#x200B;に移動し、**[!UICONTROL Flush Cache]**&#x200B;をクリックして、無効なすべてのキャッシュを更新します。

### 設定オプション

| フィールド | 範囲 | 説明 |
|---|---|---|
| [!UICONTROL Enable] | web サイト | Web サイトの[!DNL Payment Services]を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Method] | ストアビュー | ストアのメソッドまたは環境を設定します。 オプション：[!UICONTROL Sandbox] / [!UICONTROL Production] |
| [!UICONTROL Payment Services Sandbox ID] | ストアビュー | サンドボックスのオンボーディング中に自動生成されるサンドボックスマーチャント ID。 |
| [!UICONTROL Payment Services Production ID] | ストアビュー | 本番環境でのオンボーディング中に自動生成される、本番環境のマーチャント ID。 |
| [!UICONTROL PayPal Merchant ID] | ストアビュー | PayPal アカウントの作成時に生成された、一意のPayPal加盟店アカウント ID。 |
| [!UICONTROL PayPal Merchant Status] | ストアビュー | PayPal加盟店IDのステータス。 |
| [!UICONTROL Soft Descriptor] | web サイトまたはストアビュー | Web サイトとストアビューにソフト記述子を追加して、ブランド、ストア、または製品ラインを描く顧客トランザクションに情報を追加します。 |

## [!UICONTROL Credit Card Fields]

[!UICONTROL Credit Card Fields]の支払いオプションは、クレジットカードまたはデビットカードの支払い方法にシンプルで安全なチェックアウトを提供します。

詳しくは、[支払いオプション &#x200B;](payments-options.md#paypal-payment-buttons)を参照してください。

1. _管理者_ サイドバーで、**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**&#x200B;に移動します。
1. 左側のパネルで、**[!UICONTROL Sales]**&#x200B;を展開し、**[!UICONTROL Payment Methods]**&#x200B;を選択します。
1. _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;セクションを展開します。
1. _[!UICONTROL Payment Services]_&#x200B;セクションで、_[!UICONTROL Credit Card Fields]_ セクションを展開します。
1. 「**[!UICONTROL Title]**」に、チェックアウト時に表示される支払い方法の名前を変更するテキスト（必要に応じて）を入力します。
1. 支払いアクション [を](production.md#set-payment-services-as-payment-method)設定するには、**[!UICONTROL Authorize]**&#x200B;または&#x200B;**承認とキャプチャ**&#x200B;を選択します。
1. チェックアウトページで支払い方法を優先するには、`Numeric Only` フィールドに&#x200B;**[!UICONTROL Sort order]**&#x200B;値を入力します。
1. **[!UICONTROL Show on checkout page]**&#x200B;の場合、`Yes`を選択して、チェックアウトページでクレジットカードのフィールドを有効にします。
1. **[!UICONTROL Vault Enabled]**&#x200B;の場合、`Yes`を選択して、チェックアウト用のクレジットカードの保管を有効にします。
1. **[!UICONTROL Vault Enabled in Admin]**&#x200B;で、`Yes`を選択して、保管されているクレジットカードを使用して顧客の注文を作成できるようにします。
1. **[!UICONTROL 3D Secure authentication]**&#x200B;を有効にするには（`Off`をデフォルトで有効にする）、`Always`または`When required`を選択します。
1. **[!UICONTROL Debug Mode]**&#x200B;の場合、「`Yes`」を選択してデバッグモードを有効にするか、「`No`」を選択して無効にします。
1. **[!UICONTROL Save Config]**&#x200B;をクリックして変更を保存します。
1. **[!UICONTROL System]** > **[!UICONTROL Cache Management]**&#x200B;に移動し、**[!UICONTROL Flush Cache]**&#x200B;をクリックして、無効なすべてのキャッシュを更新します。

### 設定オプション

| フィールド | 範囲 | 説明 |
|---|---|---|
| [!UICONTROL Title] | ストアビュー | チェックアウト時に支払い方法ビューでこの支払いオプションのタイトルとして表示するテキストを追加します。 オプション：[!UICONTROL text field] |
| [!UICONTROL Payment Action] | web サイト | 指定された支払い方法の[支払いアクション &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=ja)。 オプション：[!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | ストアビュー | チェックアウトページで指定した支払い方法の並べ替え順序。 `Numeric Only`値 |
| [!UICONTROL Show on checkout page] | web サイト | チェックアウトページでクレジットカード情報フィールドを有効または無効にします。 オプション：[!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled] | ストアビュー | [&#x200B; クレジットカードの資格情報の保管](vaulting.md)を有効または無効にします。 オプション：[!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled in Admin] | ストアビュー | 管理者[の顧客に対する注文を](vaulting.md) マーチャントが優先支払い方法を使用して完了する機能を有効または無効にします。 オプション：[!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL 3D Secure authentication] | web サイト | [3DS セキュア認証](security.md#3ds)を有効または無効にします。 オプション：[!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Debug Mode] | web サイト | デバッグモードを有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Fastlane]

[[!DNL Fastlane by PayPal]](https://www.paypal.com/us/cshelp/article/what-is-fastlane-by-paypal-help1096)は、オンラインで安全に支払うための高速で簡単な方法です。 **ゲストチェックアウト**&#x200B;中に、今後さらに迅速に購入できるように、カードと配送情報を安全に保存できます。

詳しくは、[支払いオプション &#x200B;](payments-options.md#fastlane-button)を参照してください。

1. _管理者_ サイドバーで、**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**&#x200B;に移動します。
1. 左側のパネルで、**[!UICONTROL Sales]**&#x200B;を展開し、**[!UICONTROL Payment Methods]**&#x200B;を選択します。
1. _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;セクションを展開します。
1. _[!UICONTROL Payment Services]_&#x200B;セクションで、_[!UICONTROL Fastlane]_ セクションを展開します。
1. 有効にするには、`Yes`の&#x200B;**[!UICONTROL Enable Fastlane]**&#x200B;を選択します（`No`は無効にします）。

   >[!NOTE]
   >
   > [!UICONTROL Fastlane]が有効になっている場合、[!UICONTROL Credit Card Fields]支払いオプションは無効になります。

1. 「**[!UICONTROL Title]**」に、チェックアウト時に表示される支払い方法の名前を変更するテキスト（必要に応じて）を入力します。 既定のタイトルは`Credit Card (via Fastlane)`です
1. 支払いアクション [を](production.md#set-payment-services-as-payment-method)設定するには、**[!UICONTROL Authorize]**&#x200B;または&#x200B;**承認とキャプチャ**&#x200B;を選択します。
1. **[!UICONTROL 3D Secure Authentication for Fastlane]**&#x200B;を有効にするには（デフォルトでは`Off`）、EUの規制に準拠する`When required`を選択するか、追加の不正利用防止レイヤーを追加する`Always`を選択します。

   >[!NOTE]
   >
   > カード発行者が3D セキュア認証を必要とする場合、[!UICONTROL Payment Services]設定に関係なく、この手順を回避することはできません。

1. チェックアウトページで支払い方法を優先するには、`Numeric Only` フィールドに&#x200B;**[!UICONTROL Sort order]**&#x200B;値を入力します。
1. Adobe Commerceのチェックアウト中に[!UICONTROL Fastlane] ブランディングを有効にするかどうかを指定するには、**[!UICONTROL Enable messaging]** フィールドを`Yes`に設定します。
1. **[!UICONTROL Save Config]**&#x200B;をクリックして変更を保存します。
1. **[!UICONTROL System]** > **[!UICONTROL Cache Management]**&#x200B;に移動し、**[!UICONTROL Flush Cache]**&#x200B;をクリックして、無効なすべてのキャッシュを更新します。

| フィールド | 範囲 | 説明 |
|---|---|---|
| [!UICONTROL Enable Fastlane] | ストアビュー | チェックアウトページで[!DNL Fastlane]を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Title] | ストアビュー | チェックアウト時に支払い方法ビューでこの支払いオプションのタイトルとして表示するテキストを追加します。 デフォルト値は`Credit Card (via Fastlane)`です。 オプション：[!UICONTROL text field] |
| [!UICONTROL Payment Action] | web サイト | 指定された支払い方法の[支払いアクション &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=ja)。 オプション：[!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL 3D Secure authentication] | ストアビュー | Fastlane[の](security.md#3ds)3D セキュア認証を有効または無効にします。 オプション：[!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Sort order] | ストアビュー | チェックアウトページで指定した支払い方法の並べ替え順序。 `Numeric Only`値 |
| [!UICONTROL Enable messaging] | ストアビュー | Adobe Commerceのチェックアウト時に[!UICONTROL Fastlane] ブランディングを有効にするかどうかを指定します。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |

### オプション。 スタイルの詳細設定

これらのオプション設定は、web サイトでの[!UICONTROL Fastlane]の表示方法をカスタマイズできます。

>[!TIP]
>
>アクセシビリティガイドラインを満たさないスタイルは、デフォルト設定に戻ります。

1. _[!UICONTROL Payment Services]_&#x200B;セクションで、_[!UICONTROL Fastlane]_ セクションに移動します。
1. _[!UICONTROL Advanced Style Settings (optional)]_&#x200B;セクションを展開します。
1. 必要に応じて設定を変更します。
1. **[!UICONTROL Save Config]**&#x200B;をクリックして変更を保存します。

カスタマイズについて詳しくは、[PayPal Developer Docs](https://developer.paypal.com/limited-release/accelerated-checkout-bt/)を参照してください。

#### ルート設定

これらのオプション設定は、全体的な[!UICONTROL Fastlane] チェックアウトコンポーネントを変更します。

| フィールド | 範囲 | 説明 |
|---|---|---|
| [!UICONTROL Background Color] | ストアビュー | コンポーネントの背景色を定義します。 `RGB`値のみ |
| [!UICONTROL Border Color] | ストアビュー | コンポーネントの境界線カラーを定義します。 `RGB`値のみ |
| [!UICONTROL Font Family] | ストアビュー | コンポーネントのフォントを設定します。 テーマで使用できるフォントのみが表示されます |
| [!UICONTROL Font Size Base] | ストアビュー | フォントのサイズを定義します。 `px` （ピクセル）値のみ |
| [!UICONTROL Padding] | ストアビュー | コンポーネントのパディングを設定します。 `px` （ピクセル）値のみ |
| [!UICONTROL Primary Color] | ストアビュー | コンポーネントのメインカラーを定義します。 `RGB`値のみ |
| [!UICONTROL Text Color] | ストアビュー | コンポーネントのテキストのメインカラーを定義します。 `RGB`値のみ |

#### 入力設定

これらのオプション設定は、[!UICONTROL Fastlane] コンポーネントの顧客入力フィールドに適用されます。

| フィールド | 範囲 | 説明 |
|---|---|---|
| [!UICONTROL Background Color] | ストアビュー | コンポーネントの背景色を定義します。 `RGB`値のみ |
| [!UICONTROL Border Color] | ストアビュー | コンポーネントの境界線カラーを定義します。 `RGB`値のみ |
| [!UICONTROL Border Radius] | ストアビュー | 境界線の半径を定義します。 `px` （ピクセル）値のみ |
| [!UICONTROL Border Width] | ストアビュー | 境界線の幅を定義します。 `px` （ピクセル）値のみ |
| [!UICONTROL Focus Border Color] | ストアビュー | コンポーネントのフォーカスの境界線カラーを定義します。 `RGB`値のみ |
| [!UICONTROL Text Color Base] | ストアビュー | コンポーネントのテキストのメインカラーを定義します。 `RGB`値のみ |

## [!UICONTROL Apple Pay]

[!DNL Apple Pay]を使用すると、加盟店はSafariで安全で高速かつシームレスなチェックアウト体験を提供できます。加盟店アカウントごとに最大99 ドメインをサポートできます。 [!DNL Apple Pay] ボタンを押すと、お客様のiOSまたはmacOS デバイスから支払い、連絡先、配送情報が自動的に入力されるので、ワンタップですばやく購入できるので、コンバージョン率を高めることができます。

>[!IMPORTANT]
>
> Appleは、未確認のドメインからの支払いを拒否します。 加盟店は、Appleの「支払い」ボタンが使用されているドメインを確認する必要があります。 国の制限が適用されます。 ドメイン認証要件について詳しくは、[Apple Pay ドキュメント &#x200B;](https://developer.apple.com/documentation/apple_pay_on_the_web)を参照してください。

詳しくは、[支払いオプション &#x200B;](payments-options.md#apple-pay-button)を参照してください。

1. _管理者_ サイドバーで、**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**&#x200B;に移動します。
1. 左側のパネルで、**[!UICONTROL Sales]**&#x200B;を展開し、**[!UICONTROL Payment Methods]**&#x200B;を選択します。
1. _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;セクションを展開します。
1. _[!UICONTROL Payment Services]_&#x200B;セクションで、_[!UICONTROL Apple Pay]_ セクションを展開します。
1. 「**[!UICONTROL Title]**」に、チェックアウト時に表示される支払い方法の名前を変更するテキスト（必要に応じて）を入力します。
1. 支払いアクション [を](production.md#set-payment-services-as-payment-method)設定するには、**[!UICONTROL Authorize]**&#x200B;または&#x200B;**[!UICONTROL Authorize and Capture]**&#x200B;を選択します。
1. Adobe Commerceで[!DNL Apple Pay] オプションを有効にする場所を指定するには、必要に応じて次のオプションで`Yes`を選択します。
   * **[!UICONTROL Show Apple Pay on checkout page]**
   * **[!UICONTROL Show Apple Pay at start of checkout]**
   * **[!UICONTROL Show Apple Pay on product detail page]**
   * **[!UICONTROL Show Apple Pay in mini cart preview]**
   * **[!UICONTROL Show Apple Pay on cart page]**
1. デバッグモードを有効にするには、`Yes`の&#x200B;**[!UICONTROL Debug Mode]**&#x200B;を選択します（`No`は無効にします）。
1. 変更を保存するには、「**[!UICONTROL Save Config]**」をクリックします。
1. **[!UICONTROL System]** > **[!UICONTROL Cache Management]**&#x200B;に移動し、**[!UICONTROL Flush Cache]**&#x200B;をクリックして、無効なすべてのキャッシュを更新します。

### 設定オプション

| フィールド | 範囲 | 説明 |
|---|---|---|
| [!UICONTROL Title] | ストアビュー | チェックアウト時に支払い方法ビューでこの支払いオプションのタイトルとして表示するテキストを追加します。 オプション：[!UICONTROL text field] |
| [!UICONTROL Payment Action] | web サイト | 指定された支払い方法の[支払いアクション &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=ja)。 オプション：[!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Show Apple Pay on checkout page] | web サイト | チェックアウトページで[!DNL Apple Pay]を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Apple Pay at start of checkout] | ストアビュー | チェックアウトフローの開始時に[!DNL Apple Pay]を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | ストアビュー | チェックアウトページで指定した支払い方法の並べ替え順序。 `Numeric Only`値 |
| [!UICONTROL Show Apple Pay on product detail page] | ストアビュー | 製品詳細ページで[!DNL Apple Pay]を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Apple Pay in mini cart preview] | ストアビュー | ミニカートのプレビューで[!DNL Apple Pay]を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Apple Pay on cart page] | ストアビュー | カートページで[!DNL Apple Pay]を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | web サイト | デバッグモードを有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Google Pay]

[!UICONTROL Google Pay]支払いオプションを使用すると、販売者は買い物客にGoogle Payを提供でき、買い物客はデバイスでGoogle Walletを使用して購入できます。

詳しくは、[支払いオプション &#x200B;](payments-options.md#google-pay-button)を参照してください。

1. _管理者_ サイドバーで、**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**&#x200B;に移動します。
1. 左側のパネルで、**[!UICONTROL Sales]**&#x200B;を展開し、**[!UICONTROL Payment Methods]**&#x200B;を選択します。
1. _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;セクションを展開します。
1. _[!UICONTROL Payment Services]_&#x200B;セクションで、_[!UICONTROL Google Pay]_ セクションを展開します。
1. （オプション） **[!UICONTROL Title]** フィールドに新しい名前を入力して、チェックアウト時に表示される支払い方法の名前を変更します。
1. [&#128279;](production.md#set-payment-services-as-payment-method)または&#x200B;**[!UICONTROL Authorize]**&#x200B;を選択して、支払いアクション **[!UICONTROL Authorize and Capture]**&#x200B;を設定します。
1. Adobe Commerceで[!DNL Google Pay] オプションを有効にする場所を指定するには、必要に応じて次のオプションで`Yes`を選択します。
   * **[!UICONTROL Show Google Pay on checkout page]**
   * **[!UICONTROL Show Google Pay at start of checkout]**
   * **[!UICONTROL Show Google Pay on product detail page]**
   * **[!UICONTROL Show Google Pay in mini cart preview]**
   * **[!UICONTROL Show Google Pay on cart page]**
1. **[!UICONTROL 3D Secure authentication]**&#x200B;を有効にするには（`Off`をデフォルトで有効にする）、`Always`または`When required`を選択します。
1. デバッグモードを有効にするには、`Yes`の&#x200B;**[!UICONTROL Debug Mode]**&#x200B;を選択します（`No`は無効にします）。
1. 必要に応じて&#x200B;_[!UICONTROL Google Pay]_、**[!UICONTROL Button Color]**&#x200B;および&#x200B;**[!UICONTROL Button Type]**&#x200B;を選択して、**[!UICONTROL Button Style]**&#x200B;ボタンの外観を設定します。
1. 高さを設定するには、**[!UICONTROL Button Style]**&#x200B;で定義された高さのデフォルト値を使用します。
1. 変更を保存するには、「**[!UICONTROL Save Config]**」をクリックします。
1. **[!UICONTROL System]** > **[!UICONTROL Cache Management]**&#x200B;に移動し、**[!UICONTROL Flush Cache]**&#x200B;をクリックして、無効なすべてのキャッシュを更新します。

### 設定オプション

| フィールド | 範囲 | 説明 |
|---|---|---|
| [!UICONTROL Title] | ストアビュー | チェックアウト時に支払い方法ビューにこの支払いオプションに表示されるテキストラベルを指定します。 オプション：`[!UICONTROL text field]` |
| [!UICONTROL Payment Action] | web サイト | 指定された支払い方法の[支払いアクション &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=ja)。 オプション：`[!UICONTROL Authorize]` / `[!UICONTROL Authorize and Capture]` |
| [!UICONTROL Show Google Pay on checkout page] | web サイト | チェックアウトページで[!DNL Google Pay]を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Google Pay at start of checkout] | ストアビュー | チェックアウトフローの開始時に[!DNL Google Pay]を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | ストアビュー | チェックアウトページで指定した支払い方法の並べ替え順序。 `Numeric Only`値 |
| [!UICONTROL Show Google Pay on product detail page] | ストアビュー | 製品詳細ページで[!DNL Google Pay]を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Google Pay in mini cart preview] | ストアビュー | ミニカートのプレビューで[!DNL Google Pay]を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Google Pay on cart page] | ストアビュー | 買い物かごページの[!DNL Google Pay]を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL 3D Secure authentication] | ストアビュー | [3D セキュア認証](security.md#3ds)を有効または無効にします。 オプション：[!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Debug Mode] | web サイト | デバッグモードを有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Button Color] | ストアビュー | [!DNL Google Pay] ボタンの色を定義します。 オプション：`[!UICONTROL Default]` / `[!UICONTROL Black]` / `[!UICONTROL White]` |
| [!UICONTROL Button Type] | ストアビュー | [!DNL Google Pay] ボタンの種類を定義します。 オプション：`[!UICONTROL buy]` / `[!UICONTROL checkout]` / `[!UICONTROL order]` / `[!UICONTROL pay]` / `[!UICONTROL plain]` |

詳しくは、[Google Pay API リクエストオブジェクトオプション &#x200B;](https://developers.google.com/pay/api/web/reference/request-objects)のドキュメントを参照してください。

## [!DNL PayPal Payment Buttons]

[!DNL PayPal payment buttons]の支払いオプションは、顧客にシンプルで迅速かつ安全なチェックアウトプロセスを提供します。

詳しくは、[支払いオプション &#x200B;](payments-options.md#paypal-payment-buttons)を参照してください。

[!DNL PayPal payment buttons]の設定

管理画面でPayPal支払いボタン支払いオプションを有効にして設定できます。

1. _管理者_ サイドバーで、**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**&#x200B;に移動します。
1. 左側のパネルで、**[!UICONTROL Sales]**&#x200B;を展開し、**[!UICONTROL Payment Methods]**&#x200B;を選択します。
1. _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;セクションを展開します。
1. _[!UICONTROL Payment Services]_&#x200B;セクションで、_[!UICONTROL PayPal payment buttons]_ セクションを展開します。
1. チェックアウト時に表示される支払い方法の名前を変更するには、_[!UICONTROL Title]_&#x200B;フィールドを編集します。
1. 支払いアクション [を](production.md#set-payment-services-as-payment-method)設定するには、**[!UICONTROL Authorize]**&#x200B;または&#x200B;**[!UICONTROL Authorize and Capture]**&#x200B;を選択します。
1. チェックアウトページで支払い方法を優先するには、`Numeric Only` フィールドに&#x200B;**[!UICONTROL Sort order]**&#x200B;値を入力します。
1. [後払いメッセージ &#x200B;](payments-options.md#pay-later-button)を有効または無効にするには、`Yes`の`No`/**[!UICONTROL Display Pay Later Message]**&#x200B;を選択します。

   * [後払いメッセージ &#x200B;](payments-options.md#pay-later-button)を有効にすると、**[!UICONTROL Configure Messaging]** モーダルボタンが表示され、**[!UICONTROL PayPal Pay Later messaging]**&#x200B;のスタイルを設定できます。

1. Adobe CommerceでPayPal支払いボタンを有効にする場所を指定するには、必要に応じて次のオプションで`Yes`を選択します。
   * **[!UICONTROL Show buttons on checkout page]**
   * **[!UICONTROL Show buttons at start of checkout]**
   * **[!UICONTROL Show buttons on product detail page]**
   * **[!UICONTROL Show buttons in mini cart preview]**
   * **[!UICONTROL Show buttons on cart page]**
1. Venmoを支払いオプションとして有効にするには、`Yes`の&#x200B;**[!UICONTROL Venmo Enabled]**&#x200B;を選択します。
1. 支払いオプション （PayPal スマートボタン）としてクレジットカードとデビットカードを有効にするには、`Yes`の&#x200B;**[!UICONTROL Credit and Debit Card Enabled]**&#x200B;を選択します。
1. [PayPal Pay Later](payments-options.md#pay-later-button)支払いオプションを有効または無効にするには、`Yes`の`No`/**[!UICONTROL PayPal Pay Later Enabled]**&#x200B;を選択します。
1. デバッグモードを有効にするには、`Yes`の&#x200B;**[!UICONTROL Debug Mode]**&#x200B;を選択します（`No`は無効にします）。
1. 変更を保存するには、「**[!UICONTROL Save Config]**」をクリックします。
1. **[!UICONTROL System]** > **[!UICONTROL Cache Management]**&#x200B;に移動し、**[!UICONTROL Flush Cache]**&#x200B;をクリックして、無効なすべてのキャッシュを更新します。

### 設定オプション

| フィールド | 範囲 | 説明 |
|---|---|---|
| [!UICONTROL Title] | ストアビュー | チェックアウト時に支払い方法ビューでこの支払いオプションのタイトルとして表示するテキストを追加します。 オプション：テキストフィールド |
| [!UICONTROL Payment Action] | web サイト | 指定された支払い方法の[支払いアクション &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"}。 オプション：[!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Display Pay Later Message] | web サイト | ショッピングカート、商品ページ、ミニカート、チェックアウトフロー中に、PayPal Pay Later メッセージを有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Configure Messaging] | ストアビュー | PayPal Pay Later Messagingのスタイルを変更する。 オプション：`[!UICONTROL Product page]` / `[!UICONTROL Cart]` |
| [!UICONTROL Show buttons on checkout page] | ストアビュー | チェックアウトページで[!DNL PayPal payment buttons]を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons at start of checkout] | ストアビュー | チェックアウトフローの開始時に[!DNL PayPal payment buttons]を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | ストアビュー | チェックアウトページで指定した支払い方法の並べ替え順序。 `Numeric Only`値 |
| [!UICONTROL Show buttons on product detail page] | ストアビュー | 製品詳細ページで[!DNL PayPal payment buttons]を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini cart preview] | ストアビュー | ミニカートのプレビューで[!DNL PayPal payment buttons]を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | ストアビュー | カートページで[!DNL PayPal payment buttons]を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL App Switch] | ストアビュー | このオプションは、**US**&#x200B;のマーチャントと購入者にのみ適用されます。 有効にすると、すべてのExpress PayPal支払いが利用可能な場合、PayPal モバイルアプリ経由で行われます。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Contact Preference] | ストアビュー | このオプションは、**US**&#x200B;のマーチャントと購入者にのみ適用されます。 **yes**&#x200B;に設定すると、購入者の電子メールと電話番号がPayPal支払いモーダルに表示されます。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Venmo Enabled] | ストアビュー | 支払いボタンが表示されるVenmo支払いオプションを有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Credit and Debit Card Enabled] | ストアビュー | 支払いボタンが表示されるクレジットカードとデビットカードのオプションを有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL PayPal Pay Later Enabled] | ストアビュー | 支払いボタンが表示されるPayPal Pay Later支払いオプションの表示を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | web サイト | デバッグモードを有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |

## 現地での支払い方法

ローカル支払い方法（LPM）は、銀行振込やローカライズされた支払いソリューションなど、地域固有およびローカルの支払い方法と、既存のカードベースのオプションをサポートします。 マーチャントは、Commerce設定内で利用可能なLPMを直接有効または無効にできます。 利用可能な支払い方法について詳しくは、[支払いオプション &#x200B;](payments-options.md#local-payment-methods)を参照してください。

1. _管理者_ サイドバーで、**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**&#x200B;に移動します。
1. 左側のパネルで、**[!UICONTROL Sales]**&#x200B;を展開し、**[!UICONTROL Payment Methods]**&#x200B;を選択します。
1. _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;セクションを展開します。
1. _[!UICONTROL Payment Services]_&#x200B;セクションで、_[!UICONTROL Local Payment Methods]_ セクションを展開します。
1. **[!UICONTROL Active]**&#x200B;の場合、`Yes`を選択してLPMを有効にするか、`No`を選択して無効にします。
1. **[!UICONTROL Title]**&#x200B;の場合、チェックアウト時に支払い方法の名前として表示するテキストを入力します。 このタイトルは、受注グリッドにも表示されます。
1. **[!UICONTROL Allowed Payment Methods]**&#x200B;で、提供する支払い方法を選択します。 利用可能な支払い方法は、購入者の請求先住所とweb サイトの基本通貨によって異なります。
1. **[!UICONTROL Sort Order]**&#x200B;に数値を入力して、使用可能な支払い方法のリスト内のLPMの表示位置を決定します。
1. 変更を保存するには、**[!UICONTROL Save Config]**&#x200B;をクリックします。
1. **[!UICONTROL System]** > **[!UICONTROL Cache Management]**&#x200B;に移動し、**[!UICONTROL Flush Cache]**&#x200B;をクリックして、無効なすべてのキャッシュを更新します。

### 設定オプション

| フィールド | 範囲 | 説明 |
|---|---|---|
| [!UICONTROL Active] | web サイト | ローカル支払い方法を有効または無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Title] | ストアビュー | チェックアウト時および受注グリッドに表示される支払方法名。 オプション：[!UICONTROL text field] |
| [!UICONTROL Allowed Payment Methods] | web サイト | 提供するLPMを選択します。 メソッドは、請求先住所とweb サイトの通貨がメソッドの要件に一致する顧客にのみ表示されます。 オプション：`Bancontact` / `BLIK` / `eps` / `iDEAL` / `MyBank` / `Przelewy24` |
| [!UICONTROL Sort Order] | ストアビュー | 使用可能な支払い方法のリスト内のLPM グループの表示位置。 この設定は、すべてのLPMにグループとして適用されます。個々のLPMは個別に並べ替えることはできません。 `Numeric Only`値 |

>[!NOTE]
>
>各現地決済方法（LPM）には、特定の国と通貨の要件があります。 支払い方法は、顧客の請求先国とweb サイトの基本通貨が要件に一致する場合にのみ表示されます。 例えば、ベース通貨がEURの場合、ベルギーの請求先住所を持つ顧客に対してのみBancontactが表示されます。

## 行項目

ライン項目は、商品の詳細、数量、価格などの詳細な注文情報をPayPalに送信します。 この機能はデフォルトで有効になっています。 詳しくは、[行項目](line-items.md)を参照してください。

### 設定オプション

| フィールド | 範囲 | 説明 |
|---|---|---|
| [!UICONTROL Line Items Enabled] | web サイト | PayPalへの行項目と金額の内訳の送信を有効または無効にします。 [!DNL Payment Services]でサポートされていないカスタム料金を追加するサードパーティの拡張機能を使用する場合は、この設定を無効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |

## ボタンのスタイル

支払いボタンの&#x200B;_[!UICONTROL Button style]_&#x200B;オプションを設定することもできます。

1. _管理者_ サイドバーで、**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**&#x200B;に移動します。
1. 左側のパネルで、**[!UICONTROL Sales]**&#x200B;を展開し、**[!UICONTROL Payment Methods]**&#x200B;を選択します。
1. _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;セクションを展開します。
1. _[!UICONTROL [!DNL Payment Services]]_&#x200B;セクションで、_[!UICONTROL PayPal Smart Button Styling]_ セクションを展開します。
1. レイアウトを設定するには、`Vertical`の`Horizontal`または&#x200B;**[!UICONTROL Layout]**&#x200B;を選択します
1. 色を設定するには、**[!UICONTROL Color]**&#x200B;の使用可能な色から選択します。
1. シェイプを設定するには、`Rectangular`の`Pill`または&#x200B;**[!UICONTROL Shape]**&#x200B;を選択します。
1. デフォルトの高さを使用するには、`Yes`の`No`または&#x200B;**[!UICONTROL Use Default Height]**&#x200B;を選択します。
1. カスタムの高さを設定するには、**[!UICONTROL Height]**&#x200B;に必要なピクセル高さを追加します。
1. キャッチフレーズを設定するには、`Yes`の`No`または&#x200B;**[!UICONTROL Tagline]**&#x200B;を選択します。
1. 変更を保存するには、「**[!UICONTROL Save Config]**」をクリックします。
1. **[!UICONTROL System]** > **[!UICONTROL Cache Management]**&#x200B;に移動し、**[!UICONTROL Flush Cache]**&#x200B;をクリックして、無効なすべてのキャッシュを更新します。

### 設定オプション

| フィールド | 範囲 | 説明 |
|--- |--- |--- |
| [!UICONTROL Layout] | ストアビュー | Paypal支払いボタンのレイアウトのスタイルを定義します。 オプション：`[!UICONTROL Vertical]` / `[!UICONTROL Horizontal]` |
| [!UICONTROL Color] | ストアビュー | Paypal支払いボタンの色を定義します。 オプション：[!UICONTROL Blue] / `[!UICONTROL Gold]` / `[!UICONTROL Silver]` / `[!UICONTROL White]` / `[!UICONTROL Black]` |
| [!UICONTROL Shape] | ストアビュー | Paypal支払いボタンの形状を定義します。 オプション：`[!UICONTROL Rectangular]` / `[!UICONTROL Pill]` |
| [!UICONTROL Use Default Height] | ストアビュー | PayPal支払いボタンでデフォルトの高さを使用するかどうかを定義します。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Height] | ストアビュー | PayPal支払いボタンの高さを定義します。 デフォルト値：なし |
| [!UICONTROL Label] | ストアビュー | PayPalの支払いボタンに表示されるラベルを定義します。 オプション：`[!UICONTROL PayPal]` / `[!UICONTROL Checkout]` / `[!UICONTROL Buynow]` / `[!UICONTROL Pay]` / `[!UICONTROL Installment]` |
| [!UICONTROL Tagline] | ストアビュー | taglineを有効にします。 オプション：`[!UICONTROL Yes]` / `[!UICONTROL No]` |

## キャッシュをフラッシュする

Apple Pay、Venmo、PayPal PayLater ボタンの切り替えなど、_Settings_&#x200B;で設定を変更する場合は、ストアに最新の設定が表示されるように、キャッシュを手動でフラッシュします。

1. _管理者_ サイドバーで、**[!UICONTROL System]** > **[!UICONTROL Cache Management]**&#x200B;に移動します。
1. **[!UICONTROL Flush Cache]**&#x200B;をクリックして、無効なすべてのキャッシュを更新します。

キャッシュ管理テーブルのキャッシュタイプのステータスが`INVALIDATED`の場合、ストアにその項目の最新の設定が表示されない可能性があります。 キャッシュをフラッシュしてストアを更新し、最新の設定を表示します。

ストアに正しい設定が表示されていることを確認するには、定期的に[&#x200B; キャッシュをフラッシュします](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/tools/cache-management)。

## 役割の設定

管理者ユーザーがCommerce Adminで注文を作成および管理できるようにするには、[!DNL Payment Services]固有のリソースをユーザーロールに対して有効にします。

役割の管理方法については、[&#x200B; ユーザーの役割](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions-user-roles.html?lang=ja)を参照してください。

役割にリソースを割り当てる場合は、次を選択する必要があります。

* **[!DNL Payment Services]**&#x200B;でのお支払い – このリソースを使用すると、管理画面で注文を作成する際に、支払い方法として[!DNL Payment Services]のクレジットカードを利用できるようになります。 **アクション**&#x200B;親リソースを選択すると、このリソースも選択されます。

* **[!DNL Payment Services]** – このリソースには、**ダッシュボード**&#x200B;および&#x200B;**SaaS サービスプロキシ**&#x200B;のリソースが含まれています。これも選択する必要があります。 [!DNL Payment Services]が&#x200B;_Sales_ メニューに表示されていることを確認します。

  ![決済サービスリソース &#x200B;](assets/roles-payments.png){width="400" zoomable="yes"}


## カード保管

お客様が自分のアカウントのクレジットカード情報を保管（または「保存」）して今後の購入に使用できるようにする機能を有効にできます。

管理画面のカード保管を使用して、既存顧客に対する後続の注文を完了することもできます。

[&#x200B; クレジットカードのフィールド設定](#credit-card-fields)でカードの保管を有効または無効にします。

詳しくは、[&#x200B; クレジットカードの保管](vaulting.md)を参照してください。

## 3DS

3DSは、お客様や販売者を店舗での不正行為から守り、欧州連合（EU）基準への準拠を可能にします。

[&#x200B; クレジットカードのフィールド設定](#credit-card-fields)で3DSを有効または無効にします。

詳細については、「[3DS in Security](security.md#3ds)」を参照してください。

## 複数のPayPal アカウントを使用

[!UICONTROL Payment Services]では、web サイト レベルで&#x200B;**1**&#x200B;個の加盟店アカウント内で複数のPayPal アカウントを使用できます。 例えば、複数の国（異なる[通貨](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/site-store/currency/currency)を使用する）でストアを運営している場合、またはビジネスの一部にAdobe Commerceを使用するが&#x200B;_all_&#x200B;を使用しない場合は、複数のPayPal アカウントを使用するように加盟店アカウントを設定できます。

Web サイト、ストア、ストアビューの階層について詳しくは、[&#x200B; サイト、ストア、およびビューの範囲](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=ja)を参照してください。

CLIを使用した複数のPayPal アカウントのスコープの設定について詳しくは、[&#x200B; コマンドライン設定](configure-cli.md#configure-scope-via-cli)を参照してください。

営業担当者は、加盟店アカウント用に新しい[&#x200B; スコープ &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=ja#scope-settings)を作成し、PayPalで追加サイトをオンボーディングして、表示するように設定したPayPal ボタンがサイトに表示されるようにすることができます。 営業担当者に問い合わせる
web サイトで複数のPayPal アカウントを使用する場合のサポートを担当します。
