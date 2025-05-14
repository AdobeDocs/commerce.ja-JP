---
title: 何  [!DNL Live Search]?
description: Adobe Commerceの [!DNL Live Search] は、迅速で関連性の高い直感的な検索エクスペリエンスを提供します。
recommendations: noCatalog
exl-id: 15399216-6a96-4d0b-bbc1-293190cb9e14
source-git-commit: 29374c45f57e923666e255bfefadd9a1e736cfef
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 0%

---

# [!DNL Live Search] とは

[!DNL Live Search] は、Adobe Commerceの標準の検索機能に代わる機能です。 [!DNL Live Search] 機能は Composer と共にインストールされ、[!DNL Commerce] ストアを [Commerce Services Connector](../landing/saas.md) に接続します。 これを設定すると、デフォルトの検索テキストフィールドが [!DNL Live Search] のテキストフィールドに置き換えられます。 [!DNL Live Search] は、検索結果を参照する際に堅牢なフィルタリング機能を提供する製品一覧表示ページ（PLP）ウィジェットもインストールします。

[!DNL Live Search] を使用すると、次のことができます。

- 有意義な検索エクスペリエンスを作成すると、買い物客や買い物客ができるだけ少ない労力で欲しいものを見つけるのに役立ちます。
- セッション内の買い物客の行動に応じて、AI を活用した動的なファセット化と検索結果の再ランキングを利用できます。
- 簡単に更新でき、ライセンスに含まれる軽量の SaaS ベースのサービスを使用して、総所有コストを削減します。
- GraphQL API、ヘッドレスの柔軟性、API サンドボックス環境、超高速 SaaS を有効にして、技術を習得します。

>[!IMPORTANT]
>
>サイト検索に関しては、Adobe Commerceのオプションが用意されています。 実装する前に、[ 境界と制限 ](boundaries-limits.md) 情報を確認し、ビジネスニーズに適し [!DNL Live Search] いることを確認します。

## アーキテクチャ

アーキテクチャのAdobe Commerce側では、検索 *管理者* のホスティング、カタログデータの同期、クエリサービスの実行が含まれます。 [!DNL Live Search] をインストールして設定すると、Adobe Commerceで検索とカタログデータの SaaS サービスとの共有が開始されます。 この時点で、管理者ユーザーは、検索 [ ファセット ](facets.md)、[ 同義語 ](synonyms.md) および [ マーチャンダイジングルール ](category-merch.md) を設定、カスタマイズおよび管理できます。

![ ライブ検索のデータフロー ](assets/ls-cs-data-flow.png)

## クイックツアー

スピード、関連性、使いやすさを重視し、買い物客とマーチャントの両方に [!DNL Live Search] ってゲームの変化をもたらします。 次のビデオをご覧になり、ストアフロントから [!DNL Live Search] の簡単なツアーをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3418797?learn=on)

Live Search の使用と設定に関する詳細なビデオについては、[ 完全なデモ  [!DNL Live Search]](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/getting-started/capabilities/live-search-full-demonstration) のトピックを参照してください。

### 入力中に検索

買 [!DNL Live Search] 物客が [ 検索 ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) ボックスにクエリを入力すると、検索結果の候補と、上位のサムネール画像が [ ポップオーバー ](storefront-popover.md) で応答されます。 [ 製品詳細 ](https://experienceleague.adobe.com/en/docs/commerce-admin/start/storefront/storefront) ページは、買い物客が推奨製品またはおすすめ製品をクリックすると表示されます。 ポップオーバーのフッターにある _すべて表示_ リンクには、検索結果のページが表示されます。

[!DNL Live Search] は、2 文字以上のクエリに対して、「入力中に検索」を行った結果を返します。 部分一致の場合、1 単語あたりの最大文字数は 20 文字です。 クエリの文字数は変更できません。 ポップオーバーには、「`name`」、「`sku`」および「`category_ids`」フィールドが含まれます。

![ 例 storefront – 入力中に検索 ](assets/storefront-search-as-you-type.png)

### すべての検索結果を表示

「入力中の検索」クエリで返されたすべての製品をリストするには、ポップオーバーのフッターにある _すべて表示_ をクリックします。

![ ストアフロントの例 – 価格ファセット ](assets/storefront-view-all-search-results.png)

### [!DNL Live Search] での入力ミスの処理方法

検索が行われると、[!DNL Live Search] は入力ミスを考慮しないファジーなしの検索を実行します。 結果が見つからない場合、[!DNL Live Search] は、マイナーな入力ミスを考慮した 2 番目のあいまい検索を実行します。 ファジー検索は、編集距離の最大値が 1 の場合に実行されます。 この編集距離は、[ レベンシュタイン距離 ](https://en.wikipedia.org/wiki/Levenshtein_distance) の概念を使用し、次の 3 種類の操作が可能です。

| 操作 | 説明 | 例 |
|---|---|---|
| 挿入 | 文字を追加します。 | &quot;cat&quot; -> &quot;cart&quot; |
| 削除 | 文字を削除しています。 | 「cart」 – > 「cat」 |
| 置換 | ある文字を別の文字に置き換えます。 | &quot;cart&quot; -> &quot;cast&quot; |

あいまい検索ロジックに加えて、転置も考慮されます。つまり、単語内の隣接する 2 つの文字が入れ替わります（例えば、「the」ではなく「teh」）。 これらの編集制限は、フレーズ全体ではなく、単語ごとであることに注意してください。

### ファセットを使用したフィルター検索

フィルタリングされた検索では、複数のディメンションの属性値、つまり [ ファセット ](facets.md) が検索条件として使用されます。 フィルターの選択はマーチャントによって定義され、返された製品に従って変更されます。最も一般的に使用されるファセットはリストの上部にピン留めされます。

ファセットを URL パラメーターとして使用：`http://yourwebsite.com?color=red`、ライブ検索では、これらの属性値に基づいて結果がフィルタリングされます。

### 同義語

[ シノニム ](synonyms.md) リーチを拡大し、カタログ内の用語とは異なる、買い物客が使用する可能性のある用語を含めることで、クエリの焦点を絞ります。 同義語辞書を微調整して、買い物客がエンゲージし、購入するパスを維持することができます。

### マーチャンダイジングルール

マーチャンダイジング [ ルール ](rules.md) は、検索するロジックとイベントを追加する if-then ステートメントを使用してショッピングエクスペリエンスを形成します。 プロモーションやシーズン、その他の期間に合わせて、商品を簡単にブーストまたは埋め込むことができます。

### 検索用語のサポート

[!DNL Live Search] は、Commerce[ 検索語句のリダイレクト ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-terms) をサポートしています。 例えば、「配送料」などの語句を検索すると、配送料ページに直接移動できます。

## Live Search コンポーネント

- [ ポップオーバーウィジェット ](storefront-popover.md)[!DNL Live Search]、検索結果を含む検索フィールドの下に開くボックスです。
- [ 製品一覧表示ページウィジェット ](plp-styling.md) （PLP）は、ファセットと同義語をサポートする、検索可能な製品一覧表示ページを提供します。 このウィジェットは Live Search 4.0.0 以降にインストールされ、有効になっており、検索アダプターを置き換えます。
- （**非推奨**）検索アダプターは PLP ウィジェットの前身であり、Live Search &lt; 4.0.0 でインストールされました。4.0.0 より前のバージョンの Live Search を使用している場合、Commerceはアップグレードして、PLP ウィジェットの機能のメリットを享受し、今後の改善を受けることをお勧めします。 今後、検索アダプタは、セキュリティ上の問題に対処するためにのみ更新されます。

## [!DNL Live Search] workspace

[!DNL Live Search][ ワークスペース ](workspace.md) は、管理者でシノニム、ファセット、カテゴリマーチャンダイジングなどの [!DNL Live Search] 機能を設定する領域です。

## イベント

[!DNL Live Search] は [ イベント ](events.md) を使用して [ インテリジェントマーチャンダイジング ](category-merch.md) および [ パフォーマンス ](performance.md) ダッシュボードを計算します。 イベントはデフォルトの実装で提供されています。 ヘッドレスストアフロントのイベントは、手動で有効にする必要があります。

## カタログデータ保持ポリシー

テスト環境で、カタログデータの検索クエリを 90 日連続で送信しない場合、カタログデータは休止モードに設定され、検索クエリではデータが返されません。 実稼動環境のカタログデータは、このポリシーの影響を受けません。

テスト環境でカタログデータを再アクティブ化するには、「[!DNL Live Search] を再アクティブ化 [ というタイトルで ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page) サポートリクエストを送信」し、環境 ID を含めます。 テスト環境のカタログデータは、数時間以内に復元する必要があります。
