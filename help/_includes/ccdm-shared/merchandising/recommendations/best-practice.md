---
source-git-commit: 4032a0871d0a9b129ad870c93f62a2a7596ea8b7
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%
---
<!--
SOURCE OF TRUTH: Edit this file in the commerce.en repo:
https://github.com/Adobe-Enterprise-Docs/commerce.en/blob/main/help/_includes/ccdm-shared/merchandising/recommendations/best-practice.md

This content is shared by the Adobe Commerce Optimizer Guide (commerce.en) and the
Merchandising Services with CCDM Guide (commerce-admin.en). Changes made in commerce.en
are synced automatically to commerce-admin.en, so do not edit the copy in that repo.
This includes related images in help/assets/ccdm-shared/.
-->

# 推奨事項のベストプラクティス

Adobeでは、推奨事項を使用する際に次のガイドラインを推奨しています。

- レコメンデーションタイプの多様化。 顧客は同じ商品を何度も提案するような場合、レコメンデーションを無視し始めます。

- 同じレコメンデーションをカートページと注文確認ページにデプロイしないでください。 買い物かごページには`Most Added to Cart`を、注文確認ページには`Bought This, Bought That`を使用することを検討してください。

- サイトの整理： 同じページに3つ以上のレコメンデーションユニットをデプロイしないでください。

- ストアで衣料品を販売している場合、`More like this`の推奨事項は、表示される製品の性別と一致しない性別に固有の製品を提案できます。 このレコメンデーションタイプは、衣料品以外のカテゴリでのみ使用することを検討してください。

## プレースメント

レコメンデーションタイプは多数ありますが、どのタイプを各ページで採用すべきですか？ どこから始めればよいかわからない場合は、次のことをお試しください。

| ページ | レコメンデーションタイプ |
|---|---|
| ホームページ | `Recommended for you` |
| 製品ページ | `Viewed this, viewed that` |
| 買い物かご | `Bought this, bought that` |

[指標](/help/optimizer/manage-results/recommendation-performance.md)を追跡し、必要に応じて調整できます。 ここで重要な点は、実験です。

## レコメンデーションラベル

ストアフロントのレコメンデーションに割り当てられたラベルは、買い物客がそれらのレコメンデーションをどのように解釈するかに影響します。 以下のラベルは、レコメンデーションのタイプごとに頻繁に使用されます。

| レコメンデーションタイプ | 推奨ラベル |
|---|---|
| 最も閲覧された<br>最もカートに追加された商品<br>最も購入された商品<br> コンバージョン （カートに表示） <br> コンバージョン （購入に表示） | 最も人気のあるアイテム <br>人気のあるアイテム <br> トレンド <br>現在人気のあるアイテム <br>最近人気のあるアイテム <br>このアイテム（PDP）から着想を得た人気アイテム <br>売れ筋<br>興味があるかもしれません |
| あなたにおすすめ | あなただけのために<br>あなたにおすすめ<br>お買い物のトレンドからインスピレーションを得て |
| Viewed This, Viewed That | このアイテムを閲覧したお客様も<br>お客様も<br>関連アイテムを閲覧しました |
| 「これを見て、買った」 | 最終的に購入したお客様<br>最終的に購入したお客様<br>この商品を閲覧した後、他のユーザーは何を購入しますか？ |
| 「これを買った、買った」 | 必要なものをすべて入手する<br>これらのことを忘れないでください<br>頻繁に一緒に購入 |
| さらに | この<br>のような項目が他にもあります |
| 汎用 | また、<br>買い物客も<br>同様のオプション <br>関連アイテムが気に入ったかもしれません |
| トレンド | トレンド <br> トレンド情報<br>最近トレンド情報<br>注目アイテム <br> トレンド関連商品（PDP） |
| 最近表示した項目 | 最近閲覧した<br>別のページを見る |
