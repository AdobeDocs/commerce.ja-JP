---
title: 返金
description: クレジットメモ処理の一環として、管理画面で[!DNL Payment Services]件の注文の返金を作成します。
exl-id: 2b3721a1-9c9d-4e3f-ab7d-5bd61573dcb4
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
source-wordcount: '305'
ht-degree: 0%
---
# 返金

[!DNL Payment Services]件の注文の返金は、クレジットメモ処理の一環として管理画面で作成されます。 クレジットメモは、全額または一部払い戻しのために、お客様に起因する金額を示す文書です。これは、購入に適用されるか、お客様に直接払い戻されます。 クレジットメモは、[請求済み](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"}の注文に対してのみ発行できます。

詳しくは、コアユーザーガイドの[&#x200B; クレジットメモ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos){target="_blank"}を参照し、クレジットメモの発行および印刷の方法を確認してください。

PayPalまたはクレジットカードで処理された注文の場合、次のことができます。

* 注文の全額を返金します
* 注文の一部（または複数の一部）の返金
* 特定の注文項目の値より少ない金額を返金します

詳しくは、コアユーザーガイドの「[&#x200B; クレジットメモの発行](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create){target="_blank"}」を参照してください。

>[!NOTE]
>
>PayPalまたはクレジットカードで処理された注文で、残りの注文金額（元の金額から既存の返金の合計を差し引いた金額）を超える注文を部分的に返金しようとした場合、または全注文金額を超える金額の返金を行った場合にエラーが発生します。

[!UICONTROL Payment Settings]設定の[!UICONTROL Payment Action]設定（`Authorize`または`Authorize and Capture`）により、注文の[基本払い戻しワークフロー](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos#refund-workflow){target="_blank"}が決定されます。

詳しくは、_クレジットメモの発行_&#x200B;の[支払いアクション設定セクション &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create#payment-action-setting){target="_blank"}を参照してください。
