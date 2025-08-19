---
title: 実稼動  [!DNL Payment Services]  有効にする
description: 実稼動に対して  [!DNL Payment Services]  を有効にして、オンボーディングプロセスを完了します。
exl-id: 3b1269e8-127b-47f8-9738-9722a5737c63
feature: Payments, Checkout, Configuration, Install, Paas, Saas
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# 実稼動で [!DNL Payment Services] を有効にする

このトピックの手順に従って、サービスを実稼動環境に移行し [ オンボーディングプロセス ](onboard.md) を完了するには、次の操作を行います。

* [!BADGE PaaS のみ &#x200B;]{type=Informative tooltip="クラウドプロジェクト上のAdobe Commerceにのみ適用されます（Adobeが管理する PaaS インフラストラクチャ）。"}[ インストール ](install.md) 支払いサービス拡張機能
* [!BADGE PaaS のみ &#x200B;]{type=Informative tooltip="クラウドプロジェクト上のAdobe Commerceにのみ適用されます（Adobeが管理する PaaS インフラストラクチャ）。"} インスタンスの [ 設定と接続 ](connect.md)
* サンドボックスの [ 設定 ](sandbox.md) および [ テスト ](test-validate.md)

## 支払方法として [!DNL Payment Services] を設定

[Commerce サービスを設定 ](connect.md#configure-commerce-services) し、[ サンドボックステスト ](sandbox.md#enable-sandbox-testing) または [ ライブ支払い ](#enable-live-payments) を有効にした後、支払い方法として [!DNL Payment Services] を設定する必要があります。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL Payment Services]** に移動します。
1. 「**[!UICONTROL Enable Payment Services]**」をクリックします。

   このオプションは、1 つ以上の web サイトの支払い方法として [!DNL Payment Services] を設定していない場合に表示されます。

   関連するオプションが展開された状態で（**[!UICONTROL Sales]**/**[!UICONTROL Payment Services]**/_[!UICONTROL Settings]_） ホームビューの設定エリアに移動します。ここで、[!DNL Payment Services] のオプションを [ 支払い方法 ](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods){target="_blank"} として有効にできます。

1. _[!UICONTROL General Configuration]_&#x200B;で、**[!UICONTROL Enable]**&#x200B;を `Yes` に設定します。
1. **[!UICONTROL Payment Action]** と _[!UICONTROL Credit Card Fields]_&#x200B;の両方について、_[!UICONTROL PayPal payment buttons]_ を次のいずれかに設定します。

   | 設定 | 説明 |
   |---|---|
   | `Authorize` | 購入を承認し、資金を保留します。 この金額は、マーチャントによって「キャプチャ」されるまで引き出されません。 |
   | `Authorize and Capture` | 購入を承認すると、マーチャントは資金を「キャプチャ」します。 |

   >[!IMPORTANT]
   >
   >[!DNL Payment Services] は部分取り込みをサポートしています。 マーチャントは、注文の一部を部分的にキャプチャ（請求）できます。 例えば、各項目を個別にキャプチャしたり、1 つの項目を今すぐキャプチャして、残りの項目を後でキャプチャしたりできます。

1. 「**[!UICONTROL Save]**」をクリックします。
1. 「**[!UICONTROL Go to Payment Services]**」をクリックすると、[!DNL Payment Services] ホームに戻ります。
1. [ キャッシュをクリアします ](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cache-management.html)。

   設定を変更するたびにクリアを行う必要があります。

クレジットカードフィールドと PayPal 支払いボタンの設定について詳しくは、[ 設定  [!DNL Payment Services]](configure-admin.md) を参照してください。

## マーチャントのオンボーディングの完了

ストアが支払いサービスを有効にする次のステップは、ライブオンボーディングを完了することです。

支払いサービスでは、お客様の国や希望する支払い方法に応じて、[**高度** （完全にサポートされている）および **標準** （エクスプレスチェックアウト）の支払いオプション ](../payment-services/payments-options.md#standard-vs-advanced-payments-experience) およびオンボーディングフローを提供します。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL Payment Services]** に移動します。
1. 「**[!UICONTROL Live onboarding]**」をクリックします。

   このオプションは、[!DNL Payment Services] のライブオンボーディングをまだ完了していない場合に表示されます。

1. _国を選択_ モーダルで、操作する国を選択します。

   Payment Services は、現在 [5 か国 ](../payment-services/introduction.md#availability) のすべての支払いオプションを完全にサポートしています。 支払いサービスは、国リストに表示されるその他すべての国に対して、高速チェックアウト機能（支払いオプションのサブセット）を提供します。

   リストから選択した国によって、支払いオプションとオンボーディングフロー（[ 詳細 ](#advanced-onboarding) （完全にサポート）または [ 標準 ](#standard-onboarding) （エクスプレスチェックアウト））が決まります。

>[!TIP]
>
> オンボーディングオプション（標準または詳細）を選択して続行したら、オンボーディングを再度完了して、最初の選択からアップグレードまたはダウングレードする必要があります。

### 詳細オンボーディング

このオンボーディングフローは、[ 完全にサポートされている国 ](../payment-services/introduction.md#availability) のマーチャントが使用できます。

国を選択すると、次のようになります。

1. 表示されるモーダルで、「**詳細**」を選択します。

   **標準** オプションについては、[ 標準のオンボーディングフロー ](#standard-onboarding) に進みます。

1. **続行** をクリックします。
1. PayPal アカウントの資格情報（サンドボックスアカウントの資格情報ではありません）を使用して、完全にサポートされている高度なオンボーディングで PayPal フローを続行します _または_ 新しい PayPal アカウントに新規登録します。

>[!IMPORTANT]
>
>**高度なオンボーディング** では、ライブオンボーディングを有効にするために、マーチャントに [ 支払い権限のリクエスト ](#request-payments-entitlement-from-adobe) を行う必要があります。

### 標準オンボーディング

この標準のオンボーディングフローは、[ 高速チェックアウトのサポートのみ ](../payment-services/introduction.md#availability) が提供されている、利用可能な国のマーチャントで利用できます。

国を選択すると、次のようになります。

1. 表示された _支払いサービス契約_ モーダルで、「**支払いサービス契約**」リンクをクリックして、Adobe Commerce支払いサービス契約を表示します。
1. _支払いサービス契約_ モーダルで、「**同意します**」をクリックします。
1. PayPal アカウントの資格情報（サンドボックスアカウントの資格情報ではありません）を使用して、PayPal エクスプレスチェックアウトオンボーディングの PayPal フローを続行するか、新しい PayPal アカウントに新規登録します。

>[!IMPORTANT]
>
>[Appleの Pay フィールドと Credit Card フィールド ](../payment-services/payments-options.md)、**Standard オンボーディング** では使用できません。

## メールアドレスを確認

1. 管理者サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL Payment Services]** に移動します。

   「_[!UICONTROL Live onboarding]_」ボタンが表示されなくなり、「[!UICONTROL Live payments pending]」テキストボックスが表示されます。

   そのテキストボックスでは、オンボーディングを完了するために PayPal でメールアドレスを確認するように求められる場合もあります。

1. メールアドレスを確認するメッセージが表示されたら、PayPal から送信された確認メッセージをメールで確認し、クリックしてメールアドレスを確認します。
1. 管理者サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL Payment Services]** に移動します。
1. ブラウザーウィンドウを更新します。

   PayPal マーチャントオンボーディングが承認されると、支払いシステムがサンドボックスモードであり、ライブ支払いを処理していないことを示す通知が表示されます。

   >[!IMPORTANT]
   >
   >（PayPal アカウントの設定で）支払い処理の [!DNL Payment Services] と [!DNL Adobe Commerce] の [!DNL Magento Open Source] に対する同意を取り消した場合、ストア内の注文は [!DNL Payment Services] で処理できません。 支払サービスのホームに、失効した同意に関するアラートが表示されます。

## Adobeからの支払い権限のリクエスト

ストアを有効にするには、Adobeから支払い権限をリクエストします（[ 詳細なオンボーディングのみ ](#advanced-onboarding)）。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL Payment Services]** に移動します。
1. **[!UICONTROL Get Live Payments]** ホームで「[!DNL Payment Services]」をクリックします。

   ![ リクエストの使用権限 ](assets/request-entitlements.png){width="500" zoomable="yes"}

1. フォームに入力します。
1. 営業チームのメンバーから連絡があります。

または、Adobeの [business.adobe.com](https://business.adobe.com/resources/payment-services.html) で支払い権限をリクエストすることもできます。

>[!IMPORTANT]
>
>支払い権限が承認されるまで、**ライブオンボーディング** にはアクセスできません。

## 価格レベルの構成

[!DNL Payment Services] を入手 _Merchant ID_:

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL Payment Services]** に移動します。
1. ホームビューで、「**[!UICONTROL Settings]**」をクリックします。 詳しくは、[ ホーム ](payments-home.md) を参照してください。
1. 必要な _マーチャント ID_ を選択し、営業担当者に送信します。営業担当者が正しい価格レベルを設定します。

支払取引の詳細は、[ レベル 2 およびレベル 3 の処理 ](levels-card-payment-transactions.md) を参照してください。

## ライブ支払いを有効にする

_実稼動マーチャント ID_ が自動生成され、[configuration](configure-admin.md) に入力されます。 この ID は変更しないでください。

ライブ支払を有効にする：

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL Payment Services]** に移動します。
1. 「ホーム」で、ページの右上にある「**[!UICONTROL Settings]**」をクリックします。 詳しくは、[ ホーム ](payments-home.md) を参照してください。
1. _[!UICONTROL General Configuration]_&#x200B;のセクションで、**[!UICONTROL Payment mode]**&#x200B;を `Production` に設定します。
1. 「**[!UICONTROL Save]**」をクリックします。
1. [ キャッシュをクリアします ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management){target="_blank"}。

   >[!IMPORTANT]
   >
   >キャッシュをクリアしないと、チェックアウト時に PayPal の支払いオプションが表示されません。

[!DNL Payment Services] ホームに戻ると、ライブ支払を処理中のため、サンドボックス支払モード メッセージが表示されなくなります。

従来の設定オプションについては、[ 管理者での設定 ](configure-admin.md) を参照してください。

>[!IMPORTANT]
>
>（PayPal アカウントの設定で）支払い処理に対する [!DNL Payment Services] の同意を取り消した場合、ストア内の注文は [!DNL Payment Services] で処理できません。 支払い処理を再度有効にする場合は、オンボーディングを再度完了する必要があります。 支払サービスのホームに、失効した同意に関するアラートが表示されます。

## 実稼動環境でテスト

この機能を買い物客に公開する前に、実際のクレジットカードや銀行を使用して、実稼動環境で支払いをテストすることを強くお勧めします。

詳しくは [ テストと検証 ](test-validate.md) を参照してください。
