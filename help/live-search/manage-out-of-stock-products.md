---
title: ' [!DNL Live Search]の在庫切れ商品の管理'
description: Adobe Commerceで [!DNL Live Search] 在庫切れ商品を管理する方法について説明します。 在庫表示、inStock フィルター、GraphQL API フィルタリングを設定します。
feature: Services, Search
role: Admin, Developer
level: Intermediate
source-git-commit: bc8f35434c9f01f1a920745fe42617df2003ca60
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# 在庫切れ商品の管理

在庫設定、クエリ時間フィルター、オプションのバックエンド機能フラグを使用して、在庫切れ商品を[!DNL Live Search]の検索およびカテゴリの結果でどのように表示するかを制御できます。 これらのオプションには重要な制限があり、このトピックで説明します。

## ストックステータスフィルター

Adobe Commerce stock属性`quantity_and_stock_status`はファセットとしてサポートされておらず、**[!UICONTROL Add Facet]** ダイアログには表示されません。 ただし、[!DNL Live Search]は、クエリ時にフィルターとして使用できる`inStock` フィールドを公開します。

## 在庫切れ商品の非表示

在庫切れ商品を非表示にするには、次のいずれかの方法を使用します。

### Commerce設定

&#x200B;1. *管理者*&#x200B;から、**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Catalog]**>**[!UICONTROL Inventory]**&#x200B;に移動します。

&#x200B;1. **[!UICONTROL Display Out of Stock Products]**&#x200B;を&#x200B;**[!UICONTROL No]**&#x200B;に設定します。

1. **[!UICONTROL Save Config]**&#x200B;をクリックします。

**[!UICONTROL Display Out of Stock Products]**&#x200B;が`No`に設定されている場合、[!DNL Live Search]は`inStock = 'no`をPLP ウィジェットを通じてストアフロントクエリに追加するため、在庫切れの製品は返されません。

### API フィルター

[!DNL Live Search] APIを直接呼び出す場合（GraphQLまたはREST）、在庫切れ商品を明示的にフィルタリングします。例：

```graphql
query productSearchInStockOnly {
  productSearch(
    phrase: ""
    filter: [
      { attribute: "inStock", eq: "true" }
    ]
  ) {
    total_count
    items {
      productView {
        sku
        name
        inStock
      }
    }
  }
}
```

この方法は、[Live Search PLP ウィジェット &#x200B;](plp-styling.md)を通じてリクエストをルーティングしない場合に使用します。

### 在庫切れ後の在庫切れを表示

関連度でソートする際に、結果セットで在庫切れの商品を常に在庫切れの商品の後に残しておくために、Adobeでは環境用の内部機能フラグを有効にすることができます。

- この機能フラグは[!DNL Live Search]管理UIでは公開されません。
- リクエストするには、[Adobe サポート &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide){target="_blank"}に連絡し、在庫切れの商品を検索結果の最後に移動する機能を参照してください。

>[!NOTE]
>
>フラグを有効にすると、*関連性*&#x200B;で並べ替えると、結果セット内の残りの在庫切れ商品が一番下に移動します。 その他のソート注文（例：*Price*&#x200B;または&#x200B;*Product Name*）は影響を受けません。

### マーチャンダイジングルールと在庫の検索

検索マーチャンダイジングルールは、クエリベースで、在庫の状態やファセット値によるグループ全体ではなく、個々の商品をターゲットにします。

- ルール条件は、買い物客の検索フレーズ（`Query is`、`Query contains`、`Query starts with`、`Query ends with`）にのみ依存します。
- ルールイベント（ブースト、埋め込み、ピン、非表示）は、イベントごとに1つのSKUに適用されます。

そうした制約により：

- 在庫状況だけで、すべての在庫切れ商品を埋め込む、または非表示にするルールを作成することはできません。
- ルールにイベントとして追加した特定のSKUを手動で非表示または埋め込むことができます（ルールごとに50 ルールと25 イベントの制限があります）。

カタログ全体で在庫切れの商品を非表示にしたり、優先順位付けを解除したりするには、検索マーチャンダイジングルールの代わりに、このトピックで説明されている在庫設定と`inStock` フィルター（およびオプションの機能フラグ）を使用します。

>[!MORELIKETHIS]
>
> - [&#x200B; マーチャンダイジングルールの検索](rules.md)
> - [Inventory managementのグローバルオプションの設定](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/configuration)
