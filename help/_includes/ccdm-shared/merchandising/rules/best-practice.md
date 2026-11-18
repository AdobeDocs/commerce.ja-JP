---
source-git-commit: e3be9274ca8db80d3559b24a5c8be36f5d61b2ba
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%
---
<!--
SOURCE OF TRUTH: Edit this file in the commerce.en repo:
https://github.com/Adobe-Enterprise-Docs/commerce.ja-JP/blob/main/help/_includes/ccdm-shared/merchandising/rules/best-practice.md

This content is shared by the Adobe Commerce Optimizer Guide (commerce.en) and the
Merchandising Services with CCDM Guide (commerce-admin.en). Changes made in commerce.en
are synced automatically to commerce-admin.en, so do not edit the copy in that repo.
This includes related images in help/assets/ccdm-shared/.
-->

# マーチャンダイジングルールのベストプラクティス

コンバージョンと収益を最適化するには、効果的な&#x200B;**検索ルール**、強力な&#x200B;**デフォルトリスト** ルール、および&#x200B;**[カテゴリルール &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/merchandising/rules/add#rule-types)**&#x200B;を実装します。 販売データ、在庫、プロモーション、[&#x200B; インテリジェントランキング &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking)を使用してランキングを調整します。

買い物客のクエリに一致する場合にのみ[検索抑制ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/merchandising/rules/overview#search-suppression-rules)を使用します。商品が異なるランキングを必要とする場合ではなく、商品を0個返す必要があります。

よく考えられた&#x200B;**デフォルトのルール**&#x200B;を確立することが重要です。 [既定のルール &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/merchandising/rules/overview#default-rule)は、より具体的な検索ルールが適用されないときに検索結果を最初に並べ替える方法を決定します。これにより、見つけやすさと購入の可能性が向上します。 定期的に見直して、買い物客のニーズや施策に対応できるようにしましょう。

## 検索ルールを最適化するためのヒント

- 販売量の多い商品や最近の販売活動をピン留めしたり強化したりできます。
- 高い評価と好意的なレビューを得た商品に優先順位を付ける。
- 在庫商品が上位に表示されていることを確認する。
- 関連性を損なうことなく、利益率の高い商品をわずかに優先する。
- セール中の商品や特別プロモーションの一部をハイライト表示します。
- プロモーション期間中の日付範囲を使用して、プロモーション期間中または販売期間中に検索ルールを自動的に設定できます。
- 「おすすめ」や「最も閲覧されたもの」など、[&#x200B; インテリジェントなランキング &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking)を使用して、個々の買い物客の行動に基づいて検索結果をカスタマイズします。
- **None**&#x200B;以外のインテリジェントな戦略が選択されている場合は、ルールごとに&#x200B;**[インテリジェントランキングの向上](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking-boost)**&#x200B;を調整し、公開前に&#x200B;**ルールをテスト**&#x200B;します。
- インテリジェントランキング戦略が異なるクエリの実際の検索結果にどのような影響を与えるかをプレビューするには、常に「ルールをテスト」パネルを使用します。

## カテゴリルールのヒント

- 季節的なコレクションやおすすめの部門など、厳選された注文が検索と同じくらい重要な高トラフィックまたはマージンの&#x200B;**カテゴリページ**&#x200B;で[&#x200B; カテゴリルール &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/merchandising/rules/add#rule-types)を使用します。
- **インテリジェントランキング** （例：トレンド、最も閲覧されたカテゴリ）を、買い物客がそのカテゴリを閲覧する方法に合わせます。カテゴリーページでは、検索ルールと同じように検索クエリテキストが使用されません。 [&#x200B; インテリジェントランキング &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking)を参照してください。 **None**&#x200B;以外のインテリジェントメソッドの場合、**[インテリジェントランキングの向上](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking-boost)**&#x200B;とカテゴリプレビューを使用して、そのカテゴリルールの行動強度を調整します。
- **ピン**、**ブースト**、**ベリー**&#x200B;をキャンペーンプランと一貫して適用します。通常、手動配置は、買い物客がリストに&#x200B;**デフォルトの並べ替え**&#x200B;を使用している場合にのみ適用されます。 [手動ランキング &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/merchandising/rules/add#manual-ranking)を参照してください。
- エディターの&#x200B;**カテゴリ** ルールフローでプレビューし、公開後にストアフロントで検証します。これは、検索時の「ルールをテスト」パネルで使用するのと同じ規律です。

## 検索抑制のベストプラクティスとユースケース {#search-suppression-best-practices}

検索抑制ルールは、条件に一致するクエリの結果をブロックするため、ストアフロントには商品がゼロの検索結果ページが表示されます。 ルールエディターには、抑制ルールのプレビューは表示されません。 制限を満たす最も狭い条件を使用してから、[検索抑制ルールの作成と管理](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/merchandising/rules/add#search-suppression-rules)に従います。 ルールがアクティブになったら、ストアフロントで一致する検索と一致しない検索を検証します。 ストアフロントの実際の結果なしプレゼンテーションを確認します。

| ユースケース | 推奨される設定 | 確認すべきこと |
| --- | --- | --- |
| 検索のための規制コンプライアンス | 影響を受けるカタログビューにルールをスコープ設定し、制限付き検索語と一致させます。 | コンプライアンスチームで条件を確認してください。 検索抑制だけでは、カテゴリーナビゲーション、マーチャンダイジングページ、レコメンデーション、ダイレクト製品URLによるアクセスを妨げることはできません。 |
| ブランド制限 | 長いクエリ内で制限されたブランド名をブロックする必要がある場合は、**クエリ contains**&#x200B;を使用します。 | ルールがアクティブになったら、類似テキストを含む無関係なストアフロントクエリを確認して、正当な検索を抑制しないようにします。 |
| 特定の検索語句が結果を返さないようにする | 商品を返さない正確なフレーズには、**Query is**&#x200B;を使用します。 | 関連するフレーズを個別に確認してください。 完全一致条件を指定しても、そのフレーズを含むすべてのクエリがブロックされるわけではありません。 |
| クエリプレフィックスまたはサフィックスに関する制限 | **クエリーは**&#x200B;で始まり、**クエリーは**&#x200B;で終わります。制限されたテキストの場所が重要です。 | ルールがアクティブになったら、ストアフロントクエリの先頭、中央、末尾のテキストを確認して、目的の範囲を確認します。 |
| 一時的な検索制限 | 時間制限付き制限の開始日と終了日を設定します。 | スケジュールと有効ステータスを確認し、制限の終了後もルールが必要かどうかを確認します。 |

- 各ルールにわかりやすい名前を付け、その説明に制限の理由を記録します。
- 変更を公開する前にクエリ条件を確認します。 ルールがアクティブになったら、ブロックする必要があるストアフロントクエリと、引き続き商品を返す必要があるクエリを確認します。 キャッシュされたクエリの結果は、更新に最大15分かかる場合があります。
- ストアフロントの「結果なし」状態を確認し、クエリの修正やストアフロントでサポートされているカテゴリーへの移動など、買い物客が閲覧を続けるための便利な方法があることを確認します。
- 製品レベルの除外の代わりにクエリの抑制を使用しないでください。 検索結果、検索候補、オートコンプリートをまたいで商品を除外するには、手動除外または&#x200B;**属性ベースのマーチャンダイジングイベント**&#x200B;を使用し、**デフォルトの検索ルール**&#x200B;で&#x200B;**非表示** アクションを実行します。
- アクティブな抑制ルールを定期的に確認します。 不要になったルールは無効にするか、制限が変更されたときに編集して公開します。
