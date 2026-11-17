---
source-git-commit: 4032a0871d0a9b129ad870c93f62a2a7596ea8b7
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%
---
<!--
SOURCE OF TRUTH: Edit this file in the commerce.en repo:
https://github.com/Adobe-Enterprise-Docs/commerce.en/blob/main/help/_includes/ccdm-shared/merchandising/facets/best-practice.md

This content is shared by the Adobe Commerce Optimizer Guide (commerce.en) and the
Merchandising Services with CCDM Guide (commerce-admin.en). Changes made in commerce.en
are synced automatically to commerce-admin.en, so do not edit the copy in that repo.
This includes related images in help/assets/ccdm-shared/.
-->

# ファセットのベストプラクティス

フィルター機能とファセット機能は、Commerceのエクスペリエンスの重要なコンポーネントであり、買い物客が検索結果を絞り込み、より効率的に商品を見つけられるようにすることで、買い物客の体験を向上させるように設計されています。 この機能により、特定の基準を適用することで、膨大な商品カタログを整理し、ショッピングプロセスをより早く、より簡単に、より満足度の高いものにすることができます。 効果的で買い物客にフレンドリーなフィルターとファセットを実装することで、顧客が必要なものをすばやく効率的に見つけられるようになり、満足度とコンバージョン率が向上します。

## ファセットを最適化するためのヒント

- タイトル、カテゴリ、ブランド、価格帯、色、サイズなど、関連する製品属性を決定し、[動的ファセット &#x200B;](type.md)として設定します。 
- カタログ全体で一貫性があり、製品に非常に関連性の高い製品属性を設定して並べ替え、買い物客の関連性とフィルタリング機能を向上させます。
- ファセットラベルはわかりやすく、サイト全体で一貫性のある名前が付けられていることを確認します。 例えば、`Cost`の代わりに`Price Range`を使用します。
- ファセットの数を最も重要なファセットに制限することで、買い物客に負担をかけないようにしましょう。 選択肢が多すぎると、意思決定の疲労を招く可能性があります。 ファセット設定では、ファセットとして設定された最大100個の属性と、ファセットごとに最大100個の値をサポートします。 [&#x200B; ファセットの制限](/help/optimizer/boundaries-limits.md#product-discovery)の詳細をご覧ください。
- 買い物客が複数のフィルター条件を同時に選択し、結果を絞り込めるようにします。 例えば、「赤」と「青」の両方の色を選択できるようにします。
- 各ファセットオプションの横に利用可能な商品数を表示して、買い物客が期待できる検索結果を把握できるようにします。
- 特にモバイルデバイスでは、インターフェイスをクリーンで管理しやすくするために、折りたたみ可能なファセットセクションを実装します。
- また、個々のファセットや選択したすべてのフィルターをリセットして、新しい検索を容易に開始できます。
- 多数の属性がある場合は、属性を単一のメタ属性に組み合わせることを検討してください。 例えば、靴のサイズは数値で、シャツのサイズは一般的に「S/M/L/XL」です。 これら2種類のサイズを組み合わせて、1つの検索可能な属性にすることができます。
