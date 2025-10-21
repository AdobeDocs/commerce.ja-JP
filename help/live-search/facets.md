---
title: ファセット
description: ファセット [!DNL Live Search]、複数のディメンションの属性値を検索条件として使用します。
exl-id: d036265e-1868-461d-ab4c-7f469b1c6f5b
source-git-commit: 86484d49aa4b79bfe64455dba18b84bcd9073736
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# ファセット

ファセットは、複数のディメンションの属性値を検索条件として使用する、高パフォーマンスのフィルタリング方法です。 ファセット検索も似ていますが、標準の [&#x200B; レイヤー化されたナビゲーション &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-layered.html?lang=ja) よりも大幅に「スマート」です。 使用可能なフィルターのリストは、検索結果で返される製品の [&#x200B; フィルタリング可能な属性 &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-layered.html?lang=ja#filterable-attributes) によって決まります。

[!DNL Live Search] は `productSearch` クエリを使用して、[!DNL Live Search] に固有のファセットやその他のデータを返します。 コード例については [`productSearch` 開発者向けドキュメントの &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) クエリを参照してください。

![&#x200B; フィルタリングされた検索結果 &#x200B;](assets/storefront-search-results-run.png)

ファセット内で、買い物客は「スタイル」の「基本」や「スナッグ」など、複数のオプションを選択でき、検索結果はこれらのスタイルのみを表示するように更新されます。 同様に、買い物客がファセットをまたいだオプション（「スタイル」の「基本」や「気候」の「屋内」など）を選択すると、検索結果が更新され、選択したスタイルと選択した気候が表示されます。

定義済みのファセットを URL パラメーターとして使用でき、結果はパラメーター値 `http://yourstore.com?brand=acme&color=red` に基づいてフィルターされます。

## ファセットの要件

ファセットのカテゴリと製品属性の要件は、レイヤーナビゲーションで使用するフィルタリング可能な属性に似ています。 属性の各ストアフロントのプロパティでは、「検索結果の階層型ナビゲーションで使用」の値を「はい」に設定する必要があります。 属性設定の確認と更新は、管理者の [!DNL Stores]/[!DNL Attribute] メニューから行えます。

>[!NOTE]
>
>製品カテゴリをファセットとして定義した場合、ファセットにはカテゴリとサブカテゴリの `url_path` が表示されます。
>
>![&#x200B; カテゴリファセット &#x200B;](assets/facet-category.png)

[&#x200B; のファセット要件について詳しくは、](./boundaries-limits.md#facets) 境界と制限 [!DNL Live Search] を参照してください。

競合する属性が多数ある場合は、属性を 1 つの「meta-attribute」に組み合わせることを検討してください。 例えば、靴は一般的に数値サイズ、シャツは一般的に「S/M/L/XL」サイズです。 これら 2 種類のサイズを 1 つの検索可能な属性に組み合わせることができます。

| 設定 | 説明 |
|--- |--- |
| [&#x200B; カテゴリの表示設定 &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/create/categories-display-settings.html?lang=ja) | アンカー – `Yes` |
| [&#x200B; 属性プロパティ &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create.html?lang=ja) | [&#x200B; カタログ入力タイプ &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/attributes-input-types.html?lang=ja) - `Yes/No`、`Dropdown`、`Multiple Select`、`Price`、`Visual swatch` （ウィジェットのみ）、`Text swatch` （ウィジェットのみ） |
| 属性ストアフロント プロパティ | 検索結果での使用階層ナビゲーション - `Yes` |

## ファセットの集約

ファセットの集計は、ストアフロントに 3 つのファセット（カテゴリ、カラー、価格）があり、3 つすべてに対して買い物客がフィルターを適用する場合（カラー= ブルー、価格は$10.00～50.00、カテゴリ = `promotions`）に実行されます。

* `categories` aggregation - `categories` を集計して、`color` フィルターと `price` フィルターを適用しますが、`categories` フィルターは適用しません。
* `color` aggregation - `color` を集計して、`price` フィルターと `categories` フィルターを適用しますが、`color` フィルターは適用しません。
* `price` aggregation - `price` を集計して、`color` フィルターと `categories` フィルターを適用しますが、`price` フィルターは適用しません。
