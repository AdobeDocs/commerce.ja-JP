---
title: '[!DNL Payment Services]での発送を追跡しています'
description: Paypal Merchant ダッシュボードに表示される[!DNL Payment Services]件の配送と追跡情報をカスタマイズします。
feature: Payments, Paas, Saas
exl-id: 17aede1f-56ae-441a-b723-3193e865e469
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%
---
# [!DNL Payment Services]での発送を追跡しています

[!DNL Payment Services]を使用すると、加盟店はPayPal加盟店ダッシュボードで配送の追跡情報を確認できます。

Adobe Commerceの出荷グリッドについて詳しくは、[出荷](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/shipments){target=_blank}のトピックを参照してください。

## 配送の追跡の仕組み

この機能は、PayPalが追跡情報を処理するために`capture_id`を受け取る必要があるため、注文が請求されたかどうかによって異なります。 販売店がキャプチャ前に商品を出荷した場合、追跡情報はPayPalに送信されません。

>[!NOTE]
>
> 追跡番号ごとに1つの出荷を作成し、正しい品目を出荷に関連付けることをお勧めします。

## 追跡番号の追加

次の手順では、[!DNL Payment Services]を使用してAdobe Commerceで荷物を作成するプロセスについて説明します。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]** > **[!UICONTROL Orders]**&#x200B;に移動します。

1. 選択した注文の&#x200B;**[!UICONTROL Action]**&#x200B;列で、**[!UICONTROL View]**&#x200B;をクリックします。

1. **[!UICONTROL Ship]**&#x200B;をクリックします。

1. **[!UICONTROL Payment & Shipping Method]** ブロックまで下にスクロールし、**[!UICONTROL Shipping Information]**&#x200B;の&#x200B;**[!UICONTROL Add Tracking Number]**&#x200B;をクリックします。

1. **[!UICONTROL Carrier]**&#x200B;を設定します。

1. 配送を追跡するには、**[!UICONTROL Title]**&#x200B;と&#x200B;**[!UICONTROL Number]**&#x200B;を入力します。

1. **[!UICONTROL Submit Shipment]**&#x200B;をクリックします。

>[!NOTE]
>
> または、配送モジュールを使用して追跡番号情報を入力する場合もあります。 配送モジュールがトラッキング番号情報を`tracking_number` フィールドに保存していることを確認してください。

### サードパーティとの互換性

サードパーティの拡張機能は、[Commerce API](https://developer.adobe.com/commerce/webapi/rest/attributes/#ShipmentRepositoryInterface){target=_blank}を通じて出荷エンティティを作成する際の機能と互換性があります。
