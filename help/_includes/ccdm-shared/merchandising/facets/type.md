---
source-git-commit: 4032a0871d0a9b129ad870c93f62a2a7596ea8b7
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%
---
<!--
SOURCE OF TRUTH: Edit this file in the commerce.en repo:
https://github.com/Adobe-Enterprise-Docs/commerce.ja-JP/blob/main/help/_includes/ccdm-shared/merchandising/facets/type.md

This content is shared by the Adobe Commerce Optimizer Guide (commerce.en) and the
Merchandising Services with CCDM Guide (commerce-admin.en). Changes made in commerce.en
are synced automatically to commerce-admin.en, so do not edit the copy in that repo.
This includes related images in help/assets/ccdm-shared/.
-->

# ファセットの種類

ファセットにはさまざまな種類があり、関連する場合にのみ&#x200B;*フィルター* リストに表示されます。 使用可能なファセットのリストは、返された製品に応じて変更されます。 以下の特徴がプレゼンテーションと行動に影響します。

- ピン留めされたファセット – 最も一般的に使用されるファセットは、リストの上部にピン留めできます。 残りのファセットは、ピン留めされたファセットの後に&#x200B;*ソートタイプ*&#x200B;の順序で一覧表示されます。
- 動的ファセット - [Adobe AI](https://business.adobe.com/jp/ai.html)が商品セットとクエリに最も関連性が高いと見つける商品属性。 計算では、カタログ全体の属性メタデータを考慮し、クエリ時にクエリに最も関連するファセットを決定します。
- 価格ファセット – 価格帯ごとに商品を返品します。 [*設定*](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/settings) ワークスペースで、選択数と価格帯の間隔を指定できます。

## ファセットラベル

ファセットラベルは、[&#x200B; ファセットワークスペース &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/merchandising/facets/workspace)から編集できます。

## 並べ替えタイプ

ストアフロント用にレンダリングされたすべてのファセットは、アルファベット順またはカウント順に並べ替えられます。

| 並べ替えタイプ | 説明 |
|--- |--- |
| アルファベット | ストアフロント *フィルター* リストでは、ファセットはアルファベット順に並べ替えられます。 |
| カウント | ファセットは、現在の返品商品セットのファセットごとに見つかった値の数で並べ替えることもできます。 |
