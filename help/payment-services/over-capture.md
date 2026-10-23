---
title: Overcapture
description: Payment Services拡張機能のオーバーキャプチャ要件と設定について説明します。
role: Admin, User
level: Intermediate
feature: Payments, Paas
source-git-commit: d2bcc58f34af50f26d4a4f082e5b3fc30089ab58
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%
---
# Overcapture

オーバーキャプチャを使用すると、PayPalのオーバーキャプチャ契約を持つ資格のある加盟店は、注文の請求時に最初に承認された金額を超える金額をキャプチャできます。 例えば、最終金額は、重量にもとづく調整や、承認からフルフィルメントまでの材料費の変更によって増加します。

PayPalは、各加盟店アカウントの超過取得制限を決定します。 [!DNL Payment Services]でオーバーキャプチャを有効にしても、契約書が確立されないか、PayPalで承認されている上限が増えません。

>[!NOTE]
>
>このトピックでは、[!DNL Payment Services]拡張機能のオーバーキャプチャについて説明します。 [!DNL Adobe Commerce as a Cloud Service]については、個別の可用性とイネーブルメントの要件については、[&#x200B; カスタムキャプチャ量](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/order-management/invoices#custom-capture-amounts)を参照してください。

## 前提条件

オーバーキャプチャを有効にする前に：

* オーバーキャプチャは、[!DNL Payment Services] 2.17.0以降でのみ使用できます。
* Overcaptureは、米国を拠点とする企業のみが利用できます。 PayPalの[&#x200B; オーバーキャプチャ要件（PSD2） &#x200B;](https://www.paypal.com/us/cshelp/article/overcapture-requirements-psd2-help954)は、欧州経済地域（EEA）のPayPal バイヤーに販売する米国を拠点とするマーチャントにも適用されます。
* Overcaptureは、代替支払い方法（APM）では利用できません。
* PayPalでオーバーキャプチャ契約を取得し、PayPal アカウントマネージャーで加盟店アカウントに承認された制限を確認します。
* 支払い方法の&#x200B;**[!UICONTROL Payment Action]**&#x200B;を`Authorize`に設定します。 オーバーキャプチャは、請求時に後でキャプチャされた承認済み注文に適用されます。自動的に`Authorize and Capture`でキャプチャされた注文には適用されません。 [Set [!DNL Payment Services] を支払い方法](production.md#set-payment-services-as-payment-method)として参照してください。

## オーバーキャプチャを有効にする

1. _管理者_ サイドバーで、**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**&#x200B;に移動します。
1. 左側のパネルで、**[!UICONTROL Sales]**&#x200B;を展開し、**[!UICONTROL Payment Methods]**&#x200B;を選択します。
1. ストアスコープセレクターを使用して設定するweb サイトを選択します。
1. _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;セクションを展開します。
1. _[!UICONTROL Payment Services]_&#x200B;セクションで、_[!UICONTROL General Configuration]_ セクションを展開します。
1. **[!UICONTROL Over Capture Enabled]**&#x200B;を`Yes`に設定します。
1. **[!UICONTROL Save Config]**&#x200B;をクリックして変更を保存します。
1. **[!UICONTROL System]** > **[!UICONTROL Cache Management]**&#x200B;に移動し、**[!UICONTROL Flush Cache]**&#x200B;をクリックして、無効なすべてのキャッシュを更新します。

## 承認済みの支払いのキャプチャ

オーバーキャプチャは、Adminでの請求中に行われます。 要求されたキャプチャ金額は、加盟店アカウントに対してPayPalが承認した制限内である必要があります。 標準の請求ワークフローについては、[請求書の作成](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice)を参照してください。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]** > **[!UICONTROL Orders]**&#x200B;に移動します。
1. まだキャプチャされていない承認された支払いで注文を開きます。
1. **[!UICONTROL Invoice]**&#x200B;をクリックします。
1. 「カスタム取得金額」フィールドに、取得する合計金額を入力します。 例えば、許可された金額がUSD 100で、合意された最終請求がUSD 110の場合は、`10`ではなく`110`と入力します。 リクエストされた金額は、PayPalが承認した限度内である必要があります。
1. 請求書のオンラインキャプチャを選択して、支払いプロバイダーを通じて支払いをリクエストします。
1. 請求書を確認し、**[!UICONTROL Submit Invoice]**&#x200B;をクリックします。

### Invoice APIを使用したキャプチャ

標準の[請求書の作成](https://developer.adobe.com/commerce/webapi/rest/tutorials/orders/order-create-invoice) エンドポイントを使用します。

```http
POST /rest/<store_code>/V1/order/<orderId>/invoice
```

注文のストアコードと注文の内部IDを使用します。 承認済みの管理者または統合トークンで認証し、`Content-Type: application/json`を設定します。

次のペイロードの例では、加盟店のPayPal契約でその金額が許可されている場合、USD 100で許可された注文について、USD 110のオンラインキャプチャを含む請求書を全額請求します。

```json
{
  "capture": true,
  "notify": false,
  "arguments": {
    "extension_attributes": {
      "custom_capture_amount": 110
    }
  }
}
```

この例では、

1. `capture`件がオンライン キャプチャを要求しています。
1. `notify`は、Commerceが請求書の通知メールを送信するかどうかを制御します。
1. `custom_capture_amount`はキャプチャする最終的な金額であり、許可された金額を超えた増加ではありません。

## 拒否されたキャプチャのトラブルシューティング

PayPalがオーバーキャプチャリクエストを拒否した場合：

* 支払に使用するPayPal加盟店アカウントに対して、超過取得契約が有効であることを確認します。
* 要求された金額が承認済みの限度内にあることを確認してください。 上限を超えた場合は、より低い金額をリクエストするか、PayPalのアカウントマネージャーに連絡して増加について相談してください。
