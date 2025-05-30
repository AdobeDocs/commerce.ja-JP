---
title: '[!DNL Live Search] ベストプラクティス'
description: ストアに実装する際のベストプラクティス  [!DNL Live Search]  説明します。
role: Admin, Developer
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '2426'
ht-degree: 0%

---

# ベストプラクティス

この記事は、マーチャンダイザーがサイト検索機能を強化し、コンバージョン率を最大化するシームレスで効率的な買い物客のエクスペリエンスを確保するのに役立ちます。 概要に示した方法に従って、高度な検索機能を実装し、Adobe Commerce [!DNL Live Search] で最適なパフォーマンスを得るために検索ツールを継続的に絞り込む方法を学びます。

検索結果の関連性と有効性を決定する重要な要因はいくつかあります。

- 適切に構造化された製品データにより、検索アルゴリズムで製品をクエリに効果的に一致させることができます。 品質の低い製品データは、関連性の低い検索結果につながります。 マーチャンダイジング戦略の成功に直接影響を与える手順は次のとおりです。
   - 適切な属性を、対応する重みで検索可能として設定します。
   - これらの属性内のデータが関連していることを確認します。
- 適切に設計された検索エクスペリエンスは、顧客との信頼を構築し、顧客が必要なものを見つけることができるという自信を植え付けます。
- 検索ルールは、人気度、新着、プロモーション条件、その他のマーチャンダイジング戦略に基づいて特定の製品の可視性を高め、ビジネス要件を満たすため、重要です。
- ファセットナビゲーションを使用すると、買い物客は検索を絞り込んで、関連性の高い結果をすばやく得ることができます。

[!DNL Live Search] を管理するには、Adobe [!DNL Commerce] Admin で **マーケティング**/*SEO と検索*/**[!DNL Live Search]** に移動します。 

## 検索機能の最適化

このセクションでは、オートコンプリートなどの機能を使用して、買い物客のタイプに応じたリアルタイムの提案、同義語およびスペルを提供し、買い物客が異なる単語を使用している場合でも商品を見つけられるようにする方法、買い物客が検索結果を絞り込むことができるファセット、検索リダイレクトによって検索クエリから特定のページに買い物客を自動的にリダイレクトする方法について説明します。

### Autocomplete

オートコンプリートは、先行入力または自動候補とも呼ばれ、検索語句を入力すると買い物客に候補を動的に表示するインタラクティブな検索機能です。 これにより、買い物客は入力に基づいてリアルタイムの提案を提供することで、商品を迅速かつ簡単に見つけることができます。

[!DNL Live Search] [[!DNL popover]](storefront-popover.md) ウィジェットを使用すると、オートコンプリート検索オプションで人気のある製品を候補として表示できます。 買い物客が文字を入力するたびに、ポップオーバーが更新され、提案された製品や上位の検索結果のサムネール画像が表示されます。

ユーザー [!DNL Live Search]2 文字で入力すると、結果が返されます。 部分一致の場合、1 単語あたりの最大文字数は 20 文字です。 「入力中の検索」クエリの文字数は設定できません。

[ ポップオーバー ](storefront-popover.md) ウィジェットの詳細情報。

### 同義語とスペルミス

Live Search は、デフォルトでスペルミスを管理します。 同義語を設定すると、買い物客がカタログで指定した単語とは異なる単語を使用する可能性があります。 あなたの製品が「ソファ」としてリストされている間、誰かが「ソファ」を探しているので、あなたは販売を失いたくありません。 顧客が商品の検索に使用する可能性のあるすべての単語を入力することで、様々な検索語句を取り込むことができます。 結果を向上させるには [ 同義語を一方向または双方向として設定 ](synonyms-add.md#step-2-define-the-synonym-by-type) できます。

#### 同義語を最適化するためのヒント

- ブランド名および略称をフルネームにマッピングします（「HP」から「Hewlett-Packard」など）。一般的な商品のニックネーム（「iPhone」から「Apple iPhone」など）。
- 業界特有の専門用語や、買い物客が同じ意味で使用する用語（例えば、「スニーカー」や「ランニングシューズ」）を含めます。
- 新しい検索トレンド、製品の追加、買い物客の行動に基づいて、同義語リストを定期的に更新します。
- 検索結果と買い物客のフィードバックを分析して、シノニムマッピングの有効性をテストします。 マッピングを調整して、精度と関連性を向上させます。

同義語の詳細：

- [シノニムのタイプ](synonyms-type.md)
- [シノニムの作成](synonyms-add.md)
- [シノニムの管理](synonyms-manage.md)
- [言語サポート](settings.md#language)

### ファセット

フィルターとファセットの機能は、[!DNL Commerce] サイトの重要なコンポーネントであり、買い物客が検索結果を絞り込んで製品をより効率的に見つけることができるようにすることで、買い物客のエクスペリエンスを向上させるように設計されています。 この機能は、特定の条件を適用することで、買い物客が膨大な品目のカタログを並べ替えるのに役立ち、ショッピングプロセスをより速く、より簡単に、より満足させることができます。 効果的で買い物客に優しいフィルターとファセットを実装することで、顧客が必要とするものを迅速かつ効率的に見つけ、最終的に満足度とコンバージョン率を高めることができます。

製品属性をファセットとして設定するには、次の [ プロパティを設定する必要があります ](facets-add.md#step-1-add-a-facet)。

- **[!UICONTROL Use in Search]** -  `Yes`
- **[!UICONTROL Use in Layered Navigation]** -  `Filterable (with results)`
- **[!UICONTROL Use in Search Results Layered Navigation]** -  `Yes`

#### ファセットを最適化するヒント

- タイトル、カテゴリ、ブランド、価格範囲、色、サイズなど、製品に最も関連性が高く便利な属性を決定し、[ 動的ファセット ](facets-type.md) として設定します。 
- カタログ全体で一貫性があり、製品との関連性が高い製品属性を設定および並べ替えて、買い物客に対する関連性とフィルタリング機能を向上させます。
- ファセットラベルが理解しやすく、サイト全体で一貫して名前が付けられていることを確認します。 例えば、「コスト」ではなく「価格範囲」を使用します。
- ファセットの数を最も重要なファセットに制限することで、圧倒的な買い物客を避けます。 オプションが多すぎると、決定疲労が生じる可能性があります。 デフォルトでは、[!DNL Live Search] はファセットとして設定される属性が最大 100 個に制限され、各ファセット内で返されるバケットは 30 個に制限されます。 詳しくは、[ ファセットの制限 ](boundaries-limits.md#facets) を参照してください。 
- 買い物客が複数のフィルター条件を同時に選択して、結果を絞り込めるようにします。 例えば、買い物客が「赤」と「青」の両方の色を選択できるようにします。
- 各ファセットオプションの横に使用可能な製品の数を表示して、買い物客が期待できる検索結果を把握できるようにします。
- 折りたたみ可能なファセットセクションを実装して、特にモバイルデバイスで、インターフェイスをクリーンで管理しやすくします。
- 買い物客が個々のファセットまたは選択したすべてのフィルターを簡単にリセットして、新しい検索を開始できるようにします。

ファセットの詳細：

- [ファセットのタイプ](facets-type.md)
- [ファセットを追加](facets-add.md)
- [ ファセットの管理 ](facets-manage.md) （ファセットの編集、ピン留め、削除、公開）
- [価格ファセット](settings.md#price-faceting)

### リダイレクトを検索

検索リダイレクトを使用すると、検索クエリから特定のページに買い物客を自動的にリダイレクトできます。 検索リダイレクトを使用すると、買い物客のエクスペリエンスを向上させ、製品ページ、カテゴリ、ランディングページ、カスタマイズされた一連の検索結果など、最も関連性の高いコンテンツをお客様に案内できます。 検索リダイレクトはショッピングエクスペリエンスを合理化し、買い物客が探しているものを迅速かつ効率的に見つけられるようにします。

検索リダイレクトの設定で推奨される使用例：

- **人気のある製品またはカテゴリ** – 一般的な用語や人気のある用語を検索したときに、特定の製品ページまたはカテゴリに買い物客をリダイレクトします。 例えば、「iPhone」を検索すると、iPhoneのカテゴリページや特定のモデルページに直接リダイレクトされる場合があります。

- **プロモーションキャンペーン** - プロモーションイベントやセールスの際に、関連する検索用語を、特別オファーやおすすめ製品をハイライト表示するランディングページにリダイレクトします。

- **ブランド検索** – 買い物客がブランド名を検索すると、そのブランドのすべての製品が一覧表示されるブランドの専用ページにリダイレクトされます。

- **製品の廃止** – 製品の廃止が決定した場合、その製品の検索を類似の製品または新しいバージョンの製品にリダイレクトできます。

検索リダイレクトは常にテストして、正しく機能し、最も関連性の高いページに導かれていることを確認してください。 継続的にパフォーマンスを監視し、必要に応じて調整を行います。

[ 検索リダイレクトの管理 ](https://experienceleague.adobe.com/ja/docs/commerce-admin/catalog/catalog/search/search-terms) 方法を説明します。

## 検索結果の関連性の向上

この節では、有効な検索ルールを実装し、製品メタデータを使用して正確で詳細な属性を確実に検索できるようにすることで、検索結果の関連性を向上させる方法について説明します。

### 画像

設定可能な製品の子製品に、正しい役割を持つ画像があることを確認します。 親製品または子製品があると、検索結果に画像が表示されない場合があります。

>[!NOTE]
>
>検索語によって、検索結果の画像が異なる場合があります。 検索語句によって子製品の方が関連性が高いと判断された場合は、親製品の画像ではなく子製品の画像が使用されます。

### ルールを検索

コンバージョン率と売上高を最適化するには、効果的な検索ルールを実装する必要があります。 [ マーチャンダイジングを検索 ](rules.md) を使用して、販売データ、在庫レベル、プロモーションに基づく製品ランキングを調整します。

よく考えられたデフォルトの検索ルールを確立することが重要です。 [ デフォルトルール ](rules.md#default-rule) は、検索結果が最初にどのように並べ替えられ、買い物客にどのように表示されるかを決定し、全体的なエクスペリエンスを向上させ、購入の可能性を高めます。 このルールを定期的に監視および調整することで、買い物客のニーズとビジネス目標を引き続き効果的に満たすことができます。

#### 検索ルールを最適化するためのヒント

- 販売量が多い製品や最近の販売活動をピン留めまたはブーストします。
- 高い評価と肯定的なレビューで製品の優先順位を付けます。
- 在庫品目が上位にランクされていることを確認します。
- 関連性を損なうことなく、利益率の高い製品を少し優先します。
- 販売されている製品や特別なプロモーションの一部を強調します。
- プロモーション期間中に日付範囲を使用して、プロモーション期間中または販売期間中に検索ルールを自動的に設定します。
- 「あなたにお勧め」、「最も多く閲覧された [&#128279;](rules-add.md#intelligent-ranking) など、「インテリジェントランキング  を使用して、個々の買い物客の行動に基づいて検索結果をカスタマイズします。 買い物客の行動を調整するには、イベンティングが正しく実装されていることを確認する必要があります。 Luma マーチャントの場合、イベントは標準で利用できます。 ヘッドレス実装またはカスタム実装の場合は、特定のニーズに基づいて [ イベントを実装 ](events.md) する必要があります。

検索ルールの詳細：

- [マーチャンダイジングワークスペース](rules-workspace.md#set-the-scope)
- [要件](rules.md#requirements)
- [デフォルトの検索ルール](rules.md#default-rule)
- 検索ルールの管理
   - [作成](rules-add.md)
   - [編集、表示、削除](rules-manage.md)
- データ収集
   - [[!DNL Live Search] イベント](events.md)
   - [Adobe Commerce イベント コレクター ](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/)
   - [GitHub Commerce イベント ](https://github.com/adobe/commerce-events/tree/main/examples) 

### 製品メタデータの活用

正確で詳細な製品属性が [ 検索可能として設定 ](workspace.md#set-attributes-as-searchable) されていることを確認します。 SKU、名前、カテゴリの属性は、デフォルトで検索でき、検索から除外することはできません。 最適な結果を得るには、SKU にスペースを使用しないでください。

検索関連性を高めるには、検索可能な各属性に重みを割り当てます。 重み付けが大きい属性は、検索結果内で高く表示されます。 関連度による並べ替えは、検索の重みなど、複数の条件の影響を受けます。 つまり、検索の重み付けが小さい属性は、検索の重み付けが大きい属性よりも関連性が高い場合があります。 その他の条件には、特定の属性の一致数、見つかった検索語句の位置、検索語句の前後の全体的なテキスト構造などがあります。

各製品の検索可能な各属性内に関連するコンテンツが含まれていることを確認します。 大量のコンテンツがある属性は、検索結果の関連性を低下させる可能性があるので、検索可能として設定しないことをお勧めします。

検索の製品属性の詳細を説明します。

- [検索可能として属性を設定](workspace.md#set-attributes-as-searchable)
- [ 属性へのウェイトの割り当て ](https://experienceleague.adobe.com/ja/docs/commerce-admin/catalog/catalog/search/search-results#weighted-search)

## 検索結果の監視

[!DNL Live Search] を使用して検索結果を最適化するには、関連する主要業績評価指標（KPI）を監視します（ユニーククエリ、平均クリック位置、クリックスルー率、コンバージョン率、ゼロ結果率など）。これにより、買い物客が検索機能とどのように関わっているかを把握できます。 このデータに従って、検索ルールを定期的に更新および調整できます。

これらの KPI は、[!DNL Live Search] [ パフォーマンス ワークスペース ](performance.md) 内で監視できます。このワークスペースには、次の指標があります。 

- **ユニーク検索** - [!DNL Commerce] サイトで実行されたユニーク検索クエリの数。 同じ買い物客または異なる買い物客が複数回繰り返した場合でも、各ユニーク検索は 1 回だけカウントされます。 この指標は、顧客が使用する検索用語の多様性を理解するのに役立ち、買い物客が探している製品や情報に関するインサイトを提供します。 一意の検索を追跡すると、次のことが可能です。

   - 一般的な検索トレンドと、頻繁に検索する項目を特定します。
   - 製品カタログまたはコンテンツの潜在的なギャップを検出します。
   - [ 同義語 ](synonyms.md) を追加したり、検索ルールを作成または更新したりして、検索機能を最適化します。

- **平均クリック位置** - サイトで検索クエリを実行した後に、買い物客がクリックした検索結果の平均位置を示します。 この指標は、検索結果の関連性と有効性に関するインサイトを提供します。

  平均クリック数が少ない（1 に近い）場合は、買い物客が関連性の高い結果をすぐに見つけ、検索戦略が効果的であることを示します。 これにより、買い物客の行動と、スクロールして目的の製品を見つけようとする意欲がどの程度あるかを理解できます。 平均クリック数が多い場合は、最も関連性の高い結果が上部に表示されないことを示している可能性があるので、検索戦略のレビューと最適化が必要になります。

- **クリックスルー率（CTR）** – 検索クエリの実行後に検索結果をクリックした買い物客の割合を測定します。 CTR が高い場合、検索結果をクリックする際に、買い物客にとって関連性が高く、アピールできることを示します。 CTR の監視は、改善点を特定するのに役立ちます。 CTR が低い場合、検索結果が買い物客の意図に一致せず、検索ルールの絞り込み、製品データの強化、結果の表示の改善の必要性を促す可能性があります。

- **コンバージョン率** – 検索機能が売上高を増やし、ビジネス目標を達成する上での有効性を示します。 これは、買い物客のニーズに応え、スムーズなショッピングエクスペリエンスを促進するうえで、検索機能が全体的に効果的であることを反映しています。 コンバージョン率が高い場合は、検索結果の関連性が高く、説得力があり、買い物客が購入を完了するきっかけになることを示します。 コンバージョン率が低い場合は、検索の関連性、製品の可用性、検索から購入までの買い物客のジャーニー全体に関する問題が示唆される場合があります。

- **結果ゼロ** – 結果を返さない [!DNL Commerce] サイトの検索クエリの割合を測定します。 この指標は、買い物客の検索が失敗した頻度を理解するために重要であり、製品カタログや検索設定の潜在的なギャップに関するインサイトを提供できます。 結果がゼロの割合が高いと、買い物客が不満を感じ、買い物のエクスペリエンスが低下し、顧客が失われる可能性があります。 カタログ内で買い物客が検索している製品やカテゴリが見つからないことを示し、在庫や製品リストの決定に役立つ場合があります。

  結果がゼロになる割合を減らすには、次の操作を行います。

   - 完全に一致する語句が見つからない場合は、代替の検索語句や関連する検索語句（[ シノニム ](synonyms.md) など）を提供します。
   - 検索リダイレクトを設定して検索で結果が得られない場合に、買い物客に関連する提案や代替提案を提供します。
   - 結果がゼロのクエリを定期的に確認してパターンを特定し、製品カタログと検索設定に対して必要な調整を行います。

- **人気の結果** – 買い物客の好みや行動に合わせて検索結果を大幅に強化できます。

この指標データを使用して、次の方法で検索機能を最適化できます。

- 検索結果の人気製品を上位に自動的にランク付けするルールを実装します。 頻繁にクリックした製品や購入した製品は、上部に表示されるように優先させることができます。 特定の検索クエリに対して、人気のある製品のリストを手動でキュレーションし、これらの項目が目立つように表示されるようにします。
- 現在トレンドとなっている製品や、最近人気が急上昇した製品をハイライトします。 これは、季節的なイベント、休日、プロモーション期間中に特に効果的です。 これを達成するには、検索ルールを設定する際に、ユースケースやビジネスニーズに合ったインテリジェントなランキングを使用します。
- 人気のあるフィルターやファセットをハイライト表示します。買い物客が特定のブランドや価格範囲で頻繁にフィルターを適用する場合は、それらのファセットをピン留めし、それに応じて並べ替えることで、それらのオプションをより目立たせます。
- 検索で結果がゼロの場合は、人気結果データを使用して、買い物客のエンゲージメントが高い代替製品や関連カテゴリを提案します。
- 一般的な検索用語と製品データを分析して、重要なキーワードを特定します。 これらのキーワードを使用して製品の検索可能な属性を最適化し、検索関連性を向上させます。
- 結果データを定期的に分析して、変化するトレンド、買い物客の好みや行動を把握し、上位の検索用語を特定して、問題を検出します。 このフィードバックループを使用して、検索ルールと製品オファーを継続的に調整および改善します

[!DNL Live Search] レポート内の正しいデータを取得するには、イベンティングが正しく実装されていることを確認する必要があります。 Luma マーチャントの場合、イベントは標準で利用できます。 ヘッドレス実装またはカスタム実装の場合は、特定のニーズに基づいて [ イベントを実装 ](events.md) する必要があります。
