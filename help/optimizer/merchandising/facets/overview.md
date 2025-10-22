---
title: ファセットの概要
description: のファセットと、検索結果  [!DNL Adobe Commerce Optimizer]  改善方法について説明します。
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
exl-id: cf16626e-8f85-47ca-b973-891b16c31fe3
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# ファセット

ファセットは、複数のディメンションの属性値を検索条件として使用する、パフォーマンスの高いフィルタリング方法です。

![&#x200B; フィルタリングされた検索結果 &#x200B;](../../assets/storefront-search-results-run.png)

ファセット内で、買い物客は「スタイル」の「基本」や「スナッグ」など、複数のオプションを選択でき、検索結果はこれらのスタイルのみを表示するように更新されます。 同様に、買い物客がファセットをまたいだオプション（「スタイル」の「基本」や「気候」の「屋内」など）を選択すると、検索結果が更新され、選択したスタイルと選択した気候が表示されます。

定義済みのファセットを URL パラメーターとして使用でき、結果はパラメーター値 `http://yourstore.com?brand=acme&color=red` に基づいてフィルターされます。

## ファセットの集約

ファセットの集計は、ストアフロントに 3 つのファセット（カテゴリ、カラー、価格）があり、3 つすべてに対して買い物客がフィルターを適用する場合（カラー= ブルー、価格は$10.00～50.00、カテゴリ = `promotions`）に実行されます。

- `categories` aggregation - `categories` を集計して、`color` フィルターと `price` フィルターを適用しますが、`categories` フィルターは適用しません。
- `color` aggregation - `color` を集計して、`price` フィルターと `categories` フィルターを適用しますが、`color` フィルターは適用しません。
- `price` aggregation - `price` を集計して、`color` フィルターと `categories` フィルターを適用しますが、`price` フィルターは適用しません。

## デフォルトの属性値

次の製品属性は [!DNL Adobe Commerce Optimizer] で使用され、デフォルトで有効になっています。

| プロパティ | 説明 | 属性 |
|---|---|---|
| 並べ替え | 製品リストでの並べ替えに使用 | `price` |
| 検索可能 | 検索で使用 | `price` <br />`sku`<br />`name` |

製品属性とそのプロパティについて詳しくは、[&#x200B; データ取得メタデータ API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#metadata) を参照してください。

## システム以外のデフォルトの属性プロパティ

次の表に、システム以外の属性のデフォルトの検索プロパティとフィルタリング可能プロパティを示します。 *検索時に使用* 属性プロパティを `Yes` に設定すると、[!DNL Adobe Commerce Optimizer] で属性を検索できるようになります。

| 属性コード | 検索可能 |
|--- |--- |
| activity | はい |
| attributes_brand | はい |
| ブランド | はい |
| 気候 | はい |
| カラー | はい |
| 色 | はい |
| 費用 | はい |
| eco_collection |  |
| 性別 | はい |
| 製造元 | はい |
| 素材 | はい |
| 目的 | はい |
| strap_bags | はい |
| style_general | はい |

## デフォルトのシステム属性プロパティ

次の表に、システム属性のデフォルトの検索およびフィルタリング可能プロパティを示します。

| 属性コード | 検索可能 |
|--- |--- |
| allow_open_amount | はい |
| 説明 | はい |
| name | はい |
| 価格 | はい |
| short_description | はい |
| sku | はい |
| ステータス | はい |
| tax_class_id | はい |
| url_key | はい |
| 重み | はい |
