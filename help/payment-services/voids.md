---
title: ボイド
description: Void を使用すると、購入金額の承認によってブロックまたは保留されているクレジットまたはデビットカードのアカウントで資金を解放できます。
feature: Payments, Checkout
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# ボイド

[!DNL Payment Services] では、既存のCommerce機能を使用して取引を無効にすることができます。 Void を使用すると、購入金額の承認によってブロックまたは保留されているクレジットまたはデビットカードのアカウントで資金を解放できます。

>[!NOTE]
>
>トランザクションを無効にできるのは、支払がまだキャプチャされていない場合のみです。

店舗が POS の資金のみを許可 [ る ](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} 設定）されている場合、店舗からの購入は、Commerce管理者のステータスが `Processing` い注文となります。

請求されていない [ 注文をキャンセル ](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order){target="_blank"} することもできます。 取得されていない認証も、そのキャンセルプロセスの一環として無効になります。

>[!NOTE]
>
>注文をキャンセルした場合も無効になりますが、注文を無効にしてもキャンセルはトリガーになりません。

注文の基本的な手順について詳しくは、『コアユーザーガイド』の [ 注文ワークフロー ](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing){target="_blank"} に関するトピックを参照してください。

ボイド機能と注文トランザクションのボイド方法について詳しくは、『コアユーザガイド』の [ 注文の処理 ](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#process-an-order){target="_blank"} を参照してください。
