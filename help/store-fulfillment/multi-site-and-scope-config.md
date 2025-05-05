---
title: 複数の Web サイトとスコープの設定
description: 複数の web サイトおよびストア範囲の在庫および配信方法を設定します。
role: Admin
level: Experienced
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# 複数の Web サイトとスコープの設定

複数の web サイト、ストア、ストアビューに対応するために、いくつかの要素に対して [ 範囲 ](https://experienceleague.adobe.com/ja/docs/commerce-admin/start/setup/websites-stores-views#scope-settings) を設定できます。

- 範囲ごとの [ 在庫の管理 ](https://experienceleague.adobe.com/ja/docs/commerce-admin/inventory/stocks/stocks-manage)

- 範囲ごとに [!DNL Delivery Methods] を管理

Web サイトまたはストア範囲に在庫を割り当てることができます。 次に、店舗のソースを更新して、使用可能な配信方法（宅配、店舗の受け取り）を設定します。

コンフィギュレーションを正常に更新した後、Adobe Commerce ストアフロントの商品詳細ページ（PDP）の店舗受取オプションは、店舗受取を許可する在庫ソースから入手できる商品に対してのみ選択できます。

## 店舗ピックアップ設定の管理

管理の [ 配信方法の設定 ](enable-general.md#delivery-methods) で、各 web サイトまたはストア範囲の [!UICONTROL In-Store Pickup] のオプションを有効または無効にします。

1. **[!UICONTROL Stores > Configuration]** に移動します。

1. 設定する範囲（格納する web サイト）を選択します。

1. 範囲を選択した状態で、**[!UICONTROL Sales > Delivery Methods]** に移動します。

1. **[!UICONTROL In-Store Pickup]** 配信メソッドを無効または有効にします。

また、このセクションでは、カーブサイドまたは店舗での受け取りをグローバルに利用できるかどうかを管理できます。

在庫ソースごとに [!UICONTROL In-Store Pickup] と [!UICONTROL Delivery Method] の設定を管理します。 実装に対する完全な柔軟性を実現するために、その他の設定は数多く存在します。
