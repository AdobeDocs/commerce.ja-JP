---
title: ボイド
description: Void を使用すると、購入金額の承認によってブロックまたは保留されているクレジットまたはデビットカードのアカウントで資金を解放できます。
exl-id: 029a7038-2812-46ce-b188-929a7a758d89
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# ボイド

[!DNL Payment Services] は、トランザクションの無効化に関するCommerceの既存の機能をサポートしています。 無効は、購買金額の承認によって保有されているクレジット・カードまたはデビット・カード勘定科目の資金をリリースします。 トランザクションは、支払がまだキャプチャされていない場合にのみ無効にできます。

* 店舗が POS の資金のみを許可 [&#x200B; る &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} 設定）されている場合、店舗からの購入は、Commerce管理者のステータスが `Processing` い注文となります。

* 請求されていない [&#x200B; 注文をキャンセル &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order){target="_blank"} することもできます。 取得されていない認証も、そのキャンセルプロセスの一環として無効になります。

>[!NOTE]
>
>注文をキャンセルした場合も無効になりますが、注文を無効にしてもキャンセルはトリガーになりません。

注文の基本的な手順について詳しくは、『コアユーザーガイド』の [&#x200B; 注文ワークフロー &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/order-management/orders/order-processing){target="_blank"} に関するトピックを参照してください。

ボイド機能と注文トランザクションのボイド方法について詳しくは、『コアユーザガイド』の [&#x200B; 注文の処理 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/order-management/orders/order-processing#process-an-order){target="_blank"} を参照してください。
