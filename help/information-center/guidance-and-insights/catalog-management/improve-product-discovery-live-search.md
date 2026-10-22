---
title: Adobe Commerceライブサーチで商品の見つけやすさを向上
description: 検索パフォーマンスのインサイトとセマンティック検索を使用して、買い物客が関連性の高い商品を見つけやすくする方法を説明します。
audience: Merchandisers, commerce administrators, and store owners
autotag-review: '2026-10-21T12:57:39.807Z'
TQID: 'https://experienceleague.adobe.com/vUbbKdcd7RFb3YUNNjlW4u7AgtiXJKeZeRs9uJwxYyY'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 76cfaac4-e563-56dd-8938-708bf8b84956
    internal-label: Attributes
  - id: cdfd3bc1-dc23-5cf0-b965-d3c0c55cde67
    internal-label: Best Practices
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: 125c1f49-aefd-5f34-a252-288937f95f6b
    internal-label: Marketing Tools
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
source-git-commit: f54c816fd23786ec519d5c890bc2664c3dcf8c6f
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%
---

# Adobe Commerceライブサーチで商品の見つけやすさを向上

<table style="table-layout:auto">
<tr style="border: 0;">
   <td valign="middle" style="vertical-align: middle;"><img alt="サンドラ・ゴンザレス・マンガナの肖像" src="../../assets/guidance-and-insights/live-search-author-avatar-sgonzalezmangana.png" width="96"><br><strong>Sandra Gonzalez Mangana</strong><br><em> シニアプロダクトマネージャー</em></td>
</tr>
</table>

*検索パフォーマンスインサイトとセマンティック検索により、買い物客が必要な商品を見つけられるよう支援します。*

カタログで適切な商品を掲載することは、ショッピング体験の一部にすぎません。 また、買い物客が自然に使う言葉、フレーズ、質問を使って、商品を見つけられる必要もあります。

Adobe Commerceのライブサーチは、発見した問題を発見し、エクスペリエンスを絞り込むのに役立つ検索パフォーマンスのインサイトを提供します。 これらのインサイトは、検索結果だけでなく、買い物客が困っている箇所を調査するために活用できます。

## 検索パフォーマンスのシグナルを探す

ライブサーチのパフォーマンスワークスペースで、ユニーク検索、ゼロ結果検索、人気の高い検索結果、クリックスルー率、コンバージョン率、平均クリック位置などの指標を確認します。 トレンドを特定し、注意が必要なクエリや製品を決定するために使用します。 [&#x200B; パフォーマンス &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/live-search/live-search-admin/performance)

![&#x200B; ユニーク検索、平均クリック数、クリック率、コンバージョン率、検索結果ゼロ率を表示するライブサーチのパフォーマンスワークスペース。ユニーク検索、検索結果ゼロ、人気の検索結果のタブが表示される](../../assets/guidance-and-insights/live-search-performance-dashboard.png){width="800" zoomable="yes"}

*ライブ検索パフォーマンス ワークスペースに、レビューする指標が表示されます。 表示される値はサンプル データです。*

次のようなシグナルを考慮します。

- **検索結果がゼロの検索：**&#x200B;検索結果のないクエリは、カタログ、製品情報、検索設定のギャップを示している可能性があります。 検索結果ゼロの検索を5%未満に抑えることを目指しましょう。 このしきい値を超えるレートは、調査する価値のあるシグナルです。
- **クリック数が少ない、またはクリック数が少ない：**&#x200B;買い物客のニーズと一致しない結果が表示される、関連する商品が目立たない可能性があります。 エンゲージメントを確保するには、検索の50%以上が商品のクリックにつながるようにしましょう。
- **検索のコンバージョン率が低い：**&#x200B;検索が買い物客の質問から購入への移動を支援しているかどうかを確認します。 コンバージョン率が3%以上を目指しましょう。

これらを、普遍的な合否ではなく、ベンチマークおよび診断シグナルとして扱いましょう。 パフォーマンスは、業界、カタログの複雑さ、顧客行動、各指標の測定方法によって異なります。 ストアのベースラインを設定し、長期的なパフォーマンスを比較します。 結果は、カタログ、買い物客、結果の測定方法によって異なる場合があります。

## 正確な言葉だけでなく、顧客の意図にも対応

買い物客は、必ずしもカタログ内の用語を使用して商品を説明するわけではありません。 例えば、「一日中立っていられる快適な靴」を探している人は、「クッション付きウォーキングスニーカー」と呼ばれる商品に興味を持つかもしれません。

セマンティック検索では、意味とコンテキストをキーワードマッチングと併用することで、カタログの文言と一致しないクエリであっても、自然言語のクエリを関連商品に結び付けることができます。 ライブサーチは、キーワードとセマンティックマッチングを1つの検索エクスペリエンスに統合したものです。 [&#x200B; セマンティック検索](https://experienceleague.adobe.com/ja/docs/commerce/live-search/live-search-admin/semantic-search)

セマンティックマッチングは、探索的検索に役立ちますが、関連性は、依然としてカタログで利用可能な商品や情報に依存します。 正確なモデル、仕様、または互換性の要件を含む検索の場合、結果が正確なままであることを確認します。

## デプロイメントのセマンティック検索の確認

設定は、使用するAdobe Commerce製品によって異なります。

- **Adobe Commerce on cloud infrastructureまたはオンプレミス：** Live Search セマンティック検索は、Adobe Commerce 2.4.4以降で使用できます。 管理画面で、マーケティング/SEOと検索/ライブ検索に移動し、設定を開き、セマンティック検索を有効にして保存します。 英語のカタログをサポートしています。 [設定 – セマンティック検索](https://experienceleague.adobe.com/ja/docs/commerce/live-search/live-search-admin/settings)
- **Adobe Commerce as a Cloud Service:**&#x200B;このシステムでは、セマンティック検索がデフォルトで有効になります。 英語のカタログをサポートしています。 [&#x200B; セマンティック検索](https://experienceleague.adobe.com/ja/docs/commerce/live-search/live-search-admin/semantic-search)
- **Adobe Commerce Optimizer:** セマンティック検索がデフォルトで有効になります。 オプションで、セマンティックブーストや類似度しきい値などのコントロールを調整できます。 設定には、ファジー検索オプションも含まれます。 [&#x200B; セマンティック検索](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/setup/semantic-search) ・ [設定 – オプションの調整](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/settings)

## 検索インサイトをアクションにつなげる

継続的なレビューサイクルを活用して、製品の見つけやすさを向上させます。

1. **調査するクエリを検索します。** 検索結果ゼロの検索、人気のクエリ、エンゲージメントの低い検索を確認できます。
2. **買い物客が何を求めているかを確認します。** クエリが欠落している製品、文言の不一致、不明確な製品データを指しているかどうかを判断します。
3. **製品情報を改善します。** 商品の属性と説明を、買い物客が使用する用語に合わせて正確かつ有益にします。 ライブサーチの場合、Adobeでは、検索可能な適切な属性と重みを設定し、属性データが適切であることを確認することをお勧めします。 [&#x200B; ライブ検索のベストプラクティス &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/live-search/best-practice)
4. **検索エクスペリエンスを調整します。** 必要に応じて、検索ルール、類義語、ファセットを使用して、買い物客が検索結果を見つけて絞り込めるようにします。 [&#x200B; ライブ検索のベストプラクティス &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/live-search/best-practice)
5. **結果を確認して、繰り返します。** 変更後も同じクエリとパフォーマンスシグナルを監視し、買い物客の行動に応じて調整できます。

## あらゆる検索を大切にする

検索クエリは、買い物客が何を求めているかを示すシグナルです。 検索パフォーマンスのインサイトを関連商品情報や適切な検索機能と組み合わせることで、買い物客のニーズを満たす商品を容易に見つけることができます。

### 詳細情報

- [ライブサーチとは？](../../../live-search/overview.md)
- [ライブサーチのベストプラクティス](../../../live-search/best-practice.md)
- [&#x200B; クラウド インフラストラクチャ上のAdobe Commerceのセマンティック検索](../../../live-search/semantic-search.md)
- Adobe Commerce Optimizerの[&#x200B; セマンティック検索](../../../optimizer/setup/semantic-search.md)
