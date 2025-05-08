---
title: 配送状況の追跡  [!DNL Payment Services]
description: Paypal [!DNL Payment Services]  マーチャントダッシュボードに表示される出荷およびトラッキング情報をカスタマイズします。
feature: Payments, Paas, Saas
exl-id: 17aede1f-56ae-441a-b723-3193e865e469
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# [!DNL Payment Services] での配送の追跡

[!DNL Payment Services] を使用すると、マーチャントは PayPal マーチャントダッシュボードで出荷のトラッキング情報を確認できます。

Adobe Commerceの出荷グリッドについて詳しくは、[ 出荷 ](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/order-management/shipments){target=_blank} に関するトピックを参照してください。

## 出荷のトラッキングの仕組み

この機能は、PayPal がトラッキング情報を処理するために `capture_id` ールを受け取る必要があるため、注文が請求されているかどうかに依存します。 マーチャントがキャプチャ前に商品を出荷した場合、トラッキング情報は PayPal に送信されません。

>[!NOTE]
>
> 追跡番号ごとに 1 つの出荷を作成し、正しい品目を出荷に関連付けることをお勧めします。

## トラッキング番号の追加

以下の手順に従って、Adobe Commerceで [!DNL Payment Services] を使用して商品を作成します。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL Orders]** に移動します。

1. 選択した注文の [**[!UICONTROL Action]**] 列で、[**[!UICONTROL View]**] をクリックします。

1. 「**[!UICONTROL Ship]**」をクリックします。

1. **[!UICONTROL Payment & Shipping Method]** ブロックまで下にスクロールし、**[!UICONTROL Shipping Information]** で **[!UICONTROL Add Tracking Number]** をクリックします。

1. **[!UICONTROL Carrier]** を設定します。

1. 出荷を追跡するには、**[!UICONTROL Title]** と **[!UICONTROL Number]** を入力します。

1. 「**[!UICONTROL Submit Shipment]**」をクリックします。

>[!NOTE]
>
> または、配送モジュールを使用して追跡番号情報を入力することもできます。 発送モジュールが、トラッキングナンバー情報を `tracking_number` フィールドに保存していることを確認します。

### サードパーティとの互換性

サードパーティの拡張機能は、[Commerce API](https://developer.adobe.com/commerce/webapi/rest/attributes/#ShipmentRepositoryInterface){target=_blank} を通じて出荷エンティティが作成された場合の機能と互換性があります。
