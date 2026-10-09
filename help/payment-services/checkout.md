---
title: '[!DNL Payment Services]でのチェックアウト'
description: 顧客のニーズに合わせて[!DNL Payment Services] チェックアウトをカスタマイズします。
feature: Payments, Checkout, Paas, Saas
exl-id: 47df165f-2145-4e0e-b272-54b8e768cf19
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
source-wordcount: '343'
ht-degree: 0%
---

# [!DNL Payment Services]でのチェックアウト

買い物客に最適なAdobe Commerce [!DNL Payment Services]のチェックアウトを設定できます。 [注文自動無効化](#order-auto-voided-if-error)や[&#x200B; クレジットカードの保管](#credit-card-vaulting)などの機能により、買い物客にスムーズなユーザーエクスペリエンスを提供できます。

## エラーが発生した場合は自動的に無効化される注文

チェックアウト中にエラーが発生した場合、[!DNL Payment Services]は注文を自動的に無効/キャンセルします。

買い物客のチェックアウトページにエラーメッセージが表示されます。 メッセージは異なる場合があります。

チェックアウト中に![&#x200B; エラー](assets/user-checkout-error.png " チェックアウト中にエラー"){width="600" zoomable="yes"}が発生しました

キャンセルされた注文に関するコメントは、特定の[注文](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/order-management/orders/orders?lang=en)の管理画面にも表示されます。

![注文の管理者の注文コメントをキャンセルしました](assets/admin-checkout-error.png "注文の管理者の注文コメントをキャンセルしました"){width="600" zoomable="yes"}

買い物客が注文の認証を受けたが、注文が作成されず`Capture`に変換された場合、注文は自動的に無効化されます。 このプロセスにより、買い物客のクレジットカードにクレジットが予約されないようにし、標準の29日間の期間の終了時に承認が失効したときに発生する支払いプロバイダーの手数料を回避することができます。

>[!NOTE]
>
>注文の自動無効化は、お客様が`Authorize and Capture` モードではなく`Authorize` モードに設定された支払い方法を使用している場合にのみ発生します。

## 製品ページからのチェックアウト

顧客がPayPalまたは[!DNL Pay Later] ボタンを使用して商品ページから直接チェックアウトすると、現在の商品ページに表示されている商品のみが購入されます。 顧客のカートに既に入っている商品は、チェックアウトフローに追加されないため、購入されません。

この機能により、顧客は現在表示している商品をすばやく購入し、カートに追加した商品を保持できます。
顧客が注文をキャンセルすると、現在の商品ページの商品が顧客のカートに追加されます。

顧客が商品ページからチェックアウトフローに入ると、チェックアウトページが簡素化され、注文関連のデータとオプションのみが表示されます。

## クレジットカードの保管

買い物客は、web サイトレベル（同じ加盟店アカウント内の任意の店舗）で今後の購入のためにクレジットカード情報を保管（または「保存」）できます。

詳しくは、[&#x200B; クレジットカードの保管](vaulting.md)を参照してください
