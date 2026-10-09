---
title: ボイド
description: ボイドを使用すると、購入金額の承認によってブロックまたは保持されているクレジットカードまたはデビットカードのアカウントの資金を解放できます。
exl-id: 029a7038-2812-46ce-b188-929a7a758d89
feature: Payments, Checkout, Paas, Saas
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
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
source-wordcount: '244'
ht-degree: 0%
---
# ボイド

[!DNL Payment Services]は、トランザクションを無効にするためのCommerceの既存の機能をサポートしています。 ボイドは、購入金額の承認によって保有されているクレジットカードまたはデビットカード口座の資金をリリースします。 トランザクションは、支払いがまだキャプチャされていない場合にのみ無効化できます。

* 販売時点付きの資金のみを承認するようにストアが[設定](https://experienceleague.adobe.com/ja/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"}されている場合、ストアからの購入は、Commerce管理画面で`Processing` ステータスの注文になります。

* 請求書を発行していない注文[&#128279;](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order){target="_blank"}を解約することもできます。 キャプチャされていない認証も、その解約プロセスの一部として無効になります。

>[!NOTE]
>
>注文をキャンセルしても無効になりますが、注文をキャンセルしてもキャンセルはトリガーされません。

注文の基本的な手順について詳しくは、コアユーザーガイドの[注文ワークフロー](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/order-management/orders/order-processing){target="_blank"}のトピックを参照してください。

無効な機能と注文トランザクションを無効にする方法について詳しくは、コアユーザーガイドの「[注文を処理する](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/order-management/orders/order-processing#process-an-order){target="_blank"}」を参照してください。
