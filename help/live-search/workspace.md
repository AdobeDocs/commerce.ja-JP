---
title: Live Search のセットアップ
description: ワークスペ  [!DNL Live Search]  スを使用して、検索パフォーマンスの設定、管理、監視を行います。
exl-id: 07c32b26-3fa4-4fae-afba-8a10866857c3
source-git-commit: bb212bf88ba7bad3deb2d2d699124413f4dd76ff
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 0%

---

# Live Search のセットアップ

ワークスペースでは、[!DNL Live Search] のパフォーマンスを設定、管理、監視できます。 上部のメニューから、各機能領域のツールにアクセスできます。 使用可能な機能は、現在のメニュー選択を反映します。

![Workspace](assets/workspace.png)

## データ収集

ワークスペースの各機能領域に正しいデータが含まれるようにするには、選択したストアフロント実装に基づいてデータ収集を設定する必要があります。

1. Luma - データ収集は標準で利用できます。
1. ヘッドレス – ストアフロントの実装に応じて、データ収集を手動で設定する必要があります。

ヘッドレスストアフロントを使用している場合、追加する必要のある必須イベントの詳細については、次のドキュメントを参照してください。

- ライブ検索ダッシュボードの [&#x200B; 必須イベント &#x200B;](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search)。
- 前提条件として追加する必要がある [&#x200B; ストアフロントイベントコレクター &#x200B;](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/)。
- イベント構造 [&#x200B; 例 &#x200B;](https://github.com/adobe/commerce-events/tree/main/examples)。

### ヘルスケア関連のお客様

医療関係のお客様が [&#x200B; データ接続 &#x200B;](../data-connection/hipaa-readiness.md#installation) 拡張機能の一部である [&#x200B; データサービス HIPAA 拡張機能 &#x200B;](../data-connection/overview.md) をインストールした場合、[!DNL Live Search] で使用されるストアフロントイベントデータは取得されなくなります。 これは、ストアフロントのイベントデータがクライアントサイドで生成されるからです。 ストアフロントのイベントデータのキャプチャと送信を続行するには、[!DNL Live Search] のイベント収集を再度有効にします。 詳しくは、[&#x200B; 一般設定 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/config/general/general#data-services) を参照してください。

## 範囲を設定

最初は、すべての [&#x200B; 設定の &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=ja#scope-settings) 範囲 [!DNL Live Search] が `Default Store View` に設定されます。 [!DNL Commerce] のインストールに複数のストア表示が含まれている場合は、**範囲** を [&#x200B; ストア表示 &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=ja) に設定します。この場合、ファセット設定が適用されます。

## メニューオプション

| オプション | 説明 |
|--- |--- |
| [&#x200B; パフォーマンス &#x200B;](performance.md) | Dashboard は、製品検索パフォーマンスに対するinsightを提供します。 |
| [&#x200B; 切り子面 &#x200B;](facets.md) | 複数のディメンションの属性値を使用して検索条件を絞り込む高性能フィルタリング。 |
| [&#x200B; シノニム &#x200B;](synonyms.md) | 検索範囲を拡張し、買い物客がカタログと異なる製品を検索するために使用する可能性のある単語を含めます。 |
| [&#x200B; マーチャンダイジングを検索 &#x200B;](rules.md) | スケジュールされたアクションをトリガーにする論理ルールを使用して、検索エクスペリエンスを形作ります。 製品をブースト、埋め込み、ピン留め、非表示にして、検索結果を調整してビジネス目標をサポートします。 |
| [&#x200B; カテゴリマーチャンダイジング &#x200B;](category-merch.md) | カテゴリレベルでルールとインテリジェントマーチャンダイジングを適用します。 |
| [GraphQL](graphql.md) | ストアの管理者にログインした開発者は、実際のカタログデータを使用してクエリを作成およびテストできます。 詳しくは、[&#x200B; 開発者向けドキュメントの &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/)GraphQLの概要 [!DNL Live Search] を参照してください。 |
| [&#x200B; 設定 &#x200B;](settings.md) | ストアフロントで価格ファセット値を価格範囲ごとにグループ化する方法を決定し、インデックス作成言語を設定します。 |

## 検索可能として属性を設定

ターゲットの絞られた結果を生成するには、[&#x200B; 検索可能 &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html?lang=ja) （`searchable=true`）製品属性のセットを確認します。 関連性を確保するために、明確で簡潔な意味を持つコンテンツが属性に含まれている場合にのみ、属性を検索可能にします。 `description` など、精度が低く長いテキストを含む属性の使用は避けてください。これらの属性はデフォルトで検索が有効になっていますが、検索結果の精度を下げる可能性があります。 例えば、人が「ショートパンツ」を検索し、「ショートスリーブ」という用語を含む説明を持つシャツがある場合、シャツは検索結果に含まれます。

属性を検索可能にするには、次の手順を実行します。

1. 管理者で、**ストア**/*属性*/**製品** に移動します。
1. 検索可能にする属性（`color` など）を選択します。
1. **ストアフロントのプロパティ** を選択し、**検索で使用** を `yes` に設定します。

   ![Workspace](assets/attribute-searchable.png)

[!DNL Live Search] た、Adobe Commerceで設定されている product 属性の [weight](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-results.html?lang=ja#weighted-search) も考慮されます。 重み付けが大きい属性は、検索結果内で高く表示されます。

次の属性は常に検索可能です。

- `sku`
- `name`
- `categories`

[&#x200B; ファセット &#x200B;](facets.md) は、フィルタリング可能にするために [!DNL Live Search] で定義される製品属性です。 [!DNL Live Search] では、任意のフィルタリング可能な属性をファセットとして設定できますが、一度に検索できるファセットの数には [&#x200B; 制限 &#x200B;](boundaries-limits.md) があります。

>[!NOTE]
>
>製品属性は、製品属性設定に必要なプロパティ *Use in Search = Yes*、*Use in Search Results Layered Navigation=yes*、および *Use in Layered Navigation=Filterable （with results）* がある場合にのみフィルタリングできます。 これらのプロパティが見つからない場合、ファセット設定に属性が表示されません。 設定手順については、[&#x200B; ファセットの追加 &#x200B;](facets-add.md#add-a-facet) を参照してください。

[&#x200B; シノニム &#x200B;](synonyms.md) とは、ユーザーが正しい製品に導くために定義できる用語です。 ズボンを探しているユーザーは「ズボン」や「スラックス」と入力する場合があります。 これらの検索用語で「パンツ」の結果にユーザーがアクセスできるように、同義語を設定できます。

## Commerceの設定

次の節では、[!DNL Live Search] でサポートされるCommerce設定とサポートされない Web サイト設定について説明します。

### サポートされる設定値

>[!IMPORTANT]
>
>Live Search 4.0.0 でデフォルトで有効になっている製品リストウィジェットを使用することを強くお勧めします。このウィジェットは、今後のリリースでアダプタの実装を完全に置き換えることを目的としています。 詳しくは、[&#x200B; 製品リストウィジェットを有効にする &#x200B;](install.md#enable-product-listing-widgets) を参照してください。

| Commerceの設定 | 説明 | ポップオーバーでサポート | アダプタでサポート |
|---|---|---|---|
| ストア/設定/カタログ/カタログ/カタログ検索/ページごとにすべての製品を許可 | `Yes` に設定した場合は、「ページごとに表示」コントロールに `ALL` オプションが含まれます。 | はい。 最大 500 製品 | はい。 最大 500 製品 |
| ストア/設定/カタログ/カタログ/カタログ検索/クエリの最短長 | カタログ検索で許可される最小文字数。 | はい | はい |
| ストア/設定/カタログ/カタログ/カタログ検索/グリッド許可値のページごとの製品 | グリッド表示に表示される製品の数を指定します。 | はい | はい |
| ストア /設定/ カタログ / カタログ / カタログ / カタログ検索/ グリッドのデフォルト値のページごとの製品 | グリッド表示でデフォルトでページごとに表示される製品の数を決定します。 | はい。 最大 500 製品 | はい。 最大 500 製品 |
| 「ストア」 > 「構成」 > 「カタログ」 > 「在庫」 > 「在庫切れ製品の表示」 | 在庫切れの商品を表示します。 | はい | はい |
| ストア /設定/通貨/ デフォルトの表示通貨 | 価格の表示に使用される主要通貨。 | はい | はい |
| 「ストア」 > 「構成」 > 「一般」 > 「通貨設定」 > 「通貨オプション」 > 「基準通貨」 | すべてのオンライン支払トランザクションに使用される主要通貨。 | はい | はい |

ウィジェット商品一覧ページとポップオーバーの価格は、設定された通貨レートを使用して、デフォルトの表示通貨に変換されます。

### サポートされていない設定値

| Commerceの設定 | 説明 | 備考 |
|---|---|---|
| ストア/設定/カタログ/ストアフロント/リストモード | 検索結果リストの形式を決定します。 | 正しくレンダリングされるが、一部のページインタラクションではイベントが送信されない |
| ストア/設定/カタログ/カタログ/カタログ検索/クエリの最大長 | カタログ検索で許可される最大文字数。 | 実装されていません。検索サービスは最大 255 文字まで受け入れます |
| 「構成」 > 「売上」 > 「税金」 > 「価格表示設定」 > 「カタログに製品価格を表示」 | カタログに公開された製品価格に税を含めるか除外するか、または価格の 2 つのバージョン（1 つは税あり、もう 1 つは税なし）を表示するかを決定します |  |
| ストア/設定/カタログ/ストアフロント/製品リスト並べ替え基準 | 検索結果リストの並べ替え順を決定します。 | [!DNL Live Search] 製品一覧ページウィジェット [&#x200B; には適用されません &#x200B;](plp-styling.md) |

### 検索語句

[!DNL Live Search] では、Luma やその他の php ベースのテーマなど、Adobe Commerceがルーティングを処理する実装で [&#x200B; 検索用語リダイレクト &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-terms.html?lang=ja) をサポートしています。
