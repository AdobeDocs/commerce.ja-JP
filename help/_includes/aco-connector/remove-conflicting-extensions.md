---
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 27%
---

# 競合する拡張機能の削除

次のいずれかの拡張機能がインストールされている場合は、[!DNL Adobe Commerce Optimizer Connector for B2B]をインストールする前にアンインストールしてください。

* [!DNL Adobe Commerce Live Search] (`magento/live-search`)
* [!DNL Adobe Commerce Product Recommendations] (`magento/product-recommendations`)
* [!DNL Adobe Commerce Catalog Service] (`magento/catalog-service`, `magento/catalog-service-installer`)
* **[!UICONTROL Data Management Dashboard]** (`magento-catalog-sync-admin`)

これらの拡張機能に関連付けられたデータは、引き続きCommerce データベースで使用できます。 ただし、コネクタが有効になっている場合は、[!DNL Commerce Optimizer]に書き出されません。 コネクタを有効にした後、これらの拡張機能によって提供されるAdobe Commerce検索およびマーチャンダイジング機能を実装するには、[[!DNL Commerce Optimizer] 管理UI](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/overview#quick-tour)から設定します。

>[!IMPORTANT]
>
>コネクタを有効にする前にこれらの拡張機能を削除しないと、設定画面が壊れ、[!DNL Commerce Optimizer]のデータが重複し、401または403の認証エラーが発生します。