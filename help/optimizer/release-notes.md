---
title: Adobe Commerce Optimizer リリースノート
description: データ取り込みREST APIおよびストアフロントカタログデータ取得用のGraphQL APIの更新など、 [!DNL Adobe Commerce Optimizer]の月次リリース情報。
feature: Release Notes
role: Admin, Developer, User, Leader
recommendations: noCatalog
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよび [!DNL Adobe Commerce Optimizer]  プロジェクトにのみ適用されます（Adobeで管理されるSaaS インフラストラクチャ）。"
exl-id: e420d461-9ea2-4e32-aa37-230b14a297d7
TQID: https://experienceleague.adobe.com/apcpxN0AOniRcHDCa5MMAVWysxRO5mTcudXXXjET-Lo
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: bd4c59c451d7b08de7dc6ef00da2556fb9a6696f
workflow-type: tm+mt
source-wordcount: 1319
ht-degree: 0%

---

# リリースノート

次のリリースノートには、[!DNL Adobe Commerce Optimizer]の更新内容が記載されています。次の内容を含みます。

* [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour)の新機能と機能強化。
* ストアフロントカタログデータ取得[&#128279;](https://developer.adobe.com/commerce/services/reference/graphql/)用の[&#x200B; データ取り込みREST API](https://developer.adobe.com/commerce/services/reference/rest/)およびGraphQL APIを更新しました。

  {{aco-api-updates-and-dropins}}

## 2026年6月

>[!BEGINSHADEBOX]

### セマンティック検索

[!DNL Adobe Commerce Optimizer]は、**[!UICONTROL Settings]**&#x200B;の&#x200B;[**詳細検索**](./settings.md#advanced-search) タブで&#x200B;**[セマンティック検索]**&#x200B;をサポートするようになりました。 セマンティック検索では、AIを利用して意味やコンテキストをまたいで商品をキーワード検索と一致させ、自然言語のクエリに対して空の検索ページを減らします。 適格な英語カタログの場合は、デフォルトで有効になっています。 オプションで、**[!UICONTROL Semantic boost]**、**[!UICONTROL Similarity threshold]**&#x200B;および&#x200B;**[!UICONTROL Fuzzy search]**&#x200B;を同じタブで調整できます。 属性の設定やストアフロントの変更は必要ありません。 [学習を増やす](./setup/semantic-search.md)。

### 推奨価格フィルター（ベータ版）

商品レコメンデーションユニットは、**[!UICONTROL Filter products]**&#x200B;段階で&#x200B;[**価格フィルター**](./merchandising/recommendations/filters.md#price)&#x200B;をサポートするようになりました。 商品の詳細ページで&#x200B;**static**&#x200B;の最小範囲と最大範囲または&#x200B;**dynamic** ルールを使用して、ストアフロントのアクティブな価格表から推奨商品を現在表示されている商品の&#x200B;**最終計算価格**&#x200B;と比較する候補を含めるか、除外します。 価格ルールでは、候補セットがフィルタリングされます。 商品を再分類しません。 [学習を増やす](./merchandising/recommendations/filters.md#price)。

{{aco-release}}

>[!ENDSHADEBOX]

## 2026年5月

>[!BEGINSHADEBOX]

### インテリジェントなランキング向上

検索の[&#x200B; マーチャンダイジングルール &#x200B;](./merchandising/rules/add.md#intelligent-ranking-boost)、デフォルトの製品リスト、および[&#x200B; カテゴリーページ &#x200B;](./merchandising/rules/add.md#rule-types) （ベータ版）に&#x200B;**[!UICONTROL Intelligent Ranking Boost]**&#x200B;が含まれるようになりました。 **最も閲覧された**&#x200B;や&#x200B;**トレンド**&#x200B;などの戦略が、カテゴリーリストの検索や行動シグナルに対するテキストの関連性に関連して、商品の順序にどの程度影響を与えているかを調整できます。 ルールのプレビューに設定が反映されます。 ブーストはクエリ時に適用されるため、変更するときにカタログの再同期は必要ありません。

### APIの更新

_2026年5月28日_

<!-- v1.2 -->

![修正](../assets/fix.svg) **完全なナビゲーションツリー** - タグ付けされていない中間ノードがパスに存在する場合、タグ付けされた下位カテゴリが、ファミリーフィルター処理された`navigation` ツリーに正しく含まれるようになりました。この修正により、買い物客はナビゲーション内のすべての関連カテゴリーを表示できるようになり、商品の閲覧と発見が簡単になりました。
<!--DATA-7183-->

![修正](../assets/fix.svg) **空のスラグ処理を`categoryTree`要求**&#x200B;で修正 – `slugs`引数に空の文字列が含まれていると、[`categoryTree`](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) クエリが内部サーバーエラーを返す問題を修正しました。空のスラグ値は無視されるようになったため、ストアフロントと統合では、リクエストに失敗することなくカテゴリーデータを引き続き解決できます。
<!--DATA-7184-->

![修正](../assets/fix.svg) **`searchCategory`要求は、大文字と小文字を区別しないアルファベット順の結果を返します** - `searchCategory` クエリは、大文字と小文字を区別せずに検索結果をアルファベット順に並べ替えるようになり、一貫性のある予測可能な順序を確保します。接頭辞が短いカテゴリは、名前が同じ場合に最初に表示されます。
<!--COMOPT-2142-->

_2026年5月4日_

<!--v1.53-->

**正しい通貨表示** – すべての製品タイプに対して、ストアフロントの製品価格に正しい通貨コード（USDなど）が表示されるようになりました。 以前は、一部の製品で予想される通貨の代わりに`NONE`が表示され、価格が欠落していました。

<!--DATA-7115-->

{{aco-release}}

>[!ENDSHADEBOX]

## 2026年4月

**リリース日**: 2026年4月7日

>[!BEGINSHADEBOX]

### カタログルール（ベータ版）

[&#x200B; カテゴリルール &#x200B;](./merchandising/rules/add.md)は、マーチャンダイジングルールを拡張して、検索と同じランキングとアクション（ピン、ブースト、埋め込み）を持つカテゴリページで、カテゴリをターゲットにして商品の順序を制御できるようにします。

### 価格フィルター（ベータ版）

レコメンデーションフィルターに、[価格帯フィルター](./merchandising/recommendations/filters.md#price) （最小および最大）が含まれるようになりました。

### APIの更新

_2026年4月29日_

<!--v1.52 release-->

**リクエストのバッチ処理が必要** — カタログデータを取得する場合、GraphQL APIは、リクエストごとに最大100個のSKUを適用するようになりました。 [文書化された制限と境界](https://experienceleague.adobe.com/en/docs/commerce/optimizer/boundaries-limits#product-discovery)を参照してください。

<!--DATA-7156-->

_2026年4月17日_

<!--v1.51 release-->

**GraphQL**&#x200B;を使用して名前でカテゴリを検索 – [`searchCategory`](https://developer.adobe.com/commerce/services/reference/graphql/)の新しいクエリでは、ストアフロントと統合のページネーションと一致するカテゴリが返されます。 パラメーターと応答フィールドについては、API リファレンスを参照してください。<!--COMOPT-1819-->

_2026年4月7日_

<!--v1.50 release-->

**より簡単なカテゴリ検索** — [categoryTree](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) クエリは`family`をオプションとして扱うため、ファミリーを指定せずにスラグでカテゴリを解決できます。

{{aco-release}}

>[!ENDSHADEBOX]

## 2026年3月

今月の[[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) リリースはありませんでした。 以下のAPI アップデートを参照してください。

>[!BEGINSHADEBOX]

### APIの更新

_2026年3月24日_

ダイナミックバンドルが、計算された価格帯を返すようになりました。<!--DATA-7014-->

{{aco-release}}

>[!ENDSHADEBOX]

## 2026年2月

**リリース日**: 2026年2月19日

>[!BEGINSHADEBOX]

### マーチャンダイジングルールとレコメンデーションのカタログビュー（ベータ版）

レコメンデーションユニットを[作成](./merchandising/recommendations/create.md)または[&#x200B; マーチャンダイジングルール &#x200B;](./merchandising/rules/add.md)するときに、カタログビューを指定できるようになりました。

### APIの更新

_2026年2月19日_

<!--v1.48-->

**ストアフロント用のカテゴリ コンテンツが充実** — [categoryTree](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) クエリで、ストアフロントがより充実したカテゴリ ページをレンダリングできるように、説明、画像、SEO メタタグが返されるようになりました。<!--DATA-6933-->

_2026年2月12日_

<!--v1.49-->

**カテゴリー別に商品データを強化** — GraphQL APIは[`CategoryProductView`](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#definition-CategoryProductView){target="blank"} タイプを追加し、ラウンドトリップが少ないカテゴリー別に商品をクエリおよびフィルタリングできるようにします。

{{aco-release}}

>[!ENDSHADEBOX]

## 「Generative AI tool deployment - internal study

今月の[[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) リリースはありませんでした。 以下のAPI アップデートを参照してください。

>[!BEGINSHADEBOX]

### APIの更新

_2026年1月19日_

* **より豊富なカテゴリがREST API**&#x200B;でサポートされるようになりました – [&#x200B; カテゴリ API](https://developer.adobe.com/commerce/services/reference/rest/#operation/createCategories)操作では、`families`に加えて`metaTags`、`images`、`description`のオプション値を受け入れることができるようになりました。これにより、カテゴリに対してより豊富なマーチャンダイジングとSEOの詳細を提供できます。

{{aco-release}}

>[!ENDSHADEBOX]

## 2025年12月

**リリース日**: 2025年12月10日

>[!BEGINSHADEBOX]

### 機会

マーチャンダイザーは、[Adobe Sites Optimizer](./manage-results/opportunities.md)を通じてAIを活用したレコメンデーションを取得して、サイトの問題を検出し、パフォーマンスの修正を提案できるようになりました。

### カタログレイヤー

マーチャンダイザーは、[&#x200B; カタログレイヤー](./setup/catalog-layer.md)を使用して、ソースカタログを編集せずに商品データをオーバーレイし、レイヤーの優先度を管理し、Adobe Sites Optimizerの自動修正を使用できるようになりました。

{{aco-release}}

>[!ENDSHADEBOX]

## 2025年11月

今月の[[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) リリースはありませんでした。 以下のAPI アップデートを参照してください。

>[!BEGINSHADEBOX]

### APIの更新

_2025年11月21日_

**データ取り込みREST APIの認証手順を更新しました** – この手順で、OAuth アクセストークンと、データ取り込みサービスの正しいDeveloper Console資格情報範囲が参照されるようになりました。 資格情報範囲が古い場合は、再生成してアクセスを維持します。

_2025年11月3日_

<!-- v1.43 -->

**GraphQLの階層化されたローカライズされた商品コンテンツ** — チャネル固有の、ロケールに応じた商品コンテンツを[!DNL Adobe Commerce Optimizer]から配信できるようになりました。

* 顧客セグメント別に商品コンテンツをカスタマイズ
* ベースカタログデータを複製することなく、ロケール固有の上書きを適用します
* レイヤーマスクを使用したフィールドレベルのオーバーライドの制御
* プレミアムなコンテンツレイヤー、季節ごとのコンテンツレイヤー、モバイルに最適化されたコンテンツレイヤーの使用

GraphQL API スキーマが変更されていません。レイヤーは、既存の`products` クエリおよびリクエストヘッダーを通じて適用されます。 [&#x200B; カタログレイヤー](./setup/catalog-layer.md)を参照してください。

{{aco-release}}

>[!ENDSHADEBOX]

## 2025年10月

**リリース日**: 2025年10月14日

>[!BEGINSHADEBOX]

### Commerce Optimizer Salesforce Commerce Connector

[!DNL Commerce Optimizer Salesforce Commerce Connector]は、Salesforce B2C Commerce カタログ データを[!DNL Commerce Optimizer]に同期する新しいApp Builder スターターキットです。<!--COMOPT-536-->

**管理者向け：**

* Salesforce カタログの変更（商品、価格、メタデータ、価格表）が自動的に[!DNL Commerce Optimizer]に同期されます。
* [!DNL Adobe Commerce]外で実行して、統合タッチポイントを減らします。
* スケジュールされた更新により、マーチャンダイジングとレコメンデーションに関する[!DNL Commerce Optimizer] データを最新の状態に保つことができます。

**開発者向け：**

* SalesforceカタログをSaaS マーチャンダイジングサービスに取り込むための拡張可能なフレームワーク。
* 実装、デザインドキュメント、コードサンプルを参照し、ビルドとトラブルシューティングを高速化できます。

### 階層検索

* **階層検索（GA）** – 商品検索で`startsWith`と`contains`の一致がサポートされるようになりました。 [階層検索と拡張検索タイプ &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#layered-search-and-expansion-of-search-types)を参照してください。

### APIの更新

* _2025年10月17日_

  **製品レイヤーの取り込みにREST API サポートを追加** — [&#x200B; カタログレイヤーAPI](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers)を使用して、特定のコンテキスト、ロケール、またはビジネス要件に対するベース製品データをカスタマイズおよび上書きします。 レイヤーを作成したら、[Adobe Commerce Optimizer Studio](./setup/catalog-layer.md).<!--DATA-6632-->から適用して管理できます

* _2025年10月14日_

  **プログラマティック カテゴリ ツリー** — REST （グローバルまたはチャネル固有）を介したナビゲーションとグループ化のためのカテゴリ ツリーを大規模に作成、更新、管理します。1つのツリーにつき最大10,000本のツリーと500個のカテゴリを含みます。 _カタログデータ取り込みREST API リファレンス_&#x200B;の[&#x200B; カテゴリ &#x200B;](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="blank"}を参照してください。<!--DCAT-2649-->

* _2025年10月8日_

  **データ取り込みのためのより明確なカテゴリーマッピング** – 新しいガイドラインでは、カテゴリースラグの形式と階層ルールについて説明し、製品`routes.path`の値が既存のカテゴリースラグと一致する必要があることを明確にします（例：`men/clothing`）。

{{aco-release}}

>[!ENDSHADEBOX]

## 2025年9月

今月の[[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) リリースはありませんでした。 以下のAPI アップデートを参照してください。

>[!BEGINSHADEBOX]

### APIの更新

_2025年9月23日_

* **REST API**&#x200B;を使用してカテゴリを管理 – [&#x200B; カテゴリ API](https://developer.adobe.com/commerce/services/reference/rest/#operation/createCategories)を使用してカテゴリを作成および管理します。 カテゴリー製品を論理グループに整理し、スラグベースのパスを通じてネストされた階層をサポートします。 商品にカテゴリを割り当てたら、GraphQL `[navigation](https://developer.adobe.com/commerce/services/reference/graphql/#navigation)`および`[categoryTree](https://developer.adobe.com/commerce/services/reference/graphql/#categorytree)` クエリを使用して商品を取得し、ストアフロントメニューとカテゴリーツリーをレンダリングします。<!--DCAT-2626-->

{{aco-release}}

>[!ENDSHADEBOX]

## 2025年8月

**リリース日**: 2025年8月28日

>[!BEGINSHADEBOX]

### EU地域が利用可能になりました

EU実稼動地域（**eu1**）は、IMS組織で使用できます。 Cloud Managerで[a [!DNL Commerce Optimizer]  インスタンス &#x200B;](./get-started.md#step-1-create-an-instance)を追加する場合、**[!UICONTROL Region]**&#x200B;として&#x200B;**[!UICONTROL European Union]**&#x200B;を選択します（実稼動環境のみ）。

欧州連合リージョンのベースの本番URLは次のとおりです。

* 管理者：`https://eu1.admin.commerce.adobe.com`
* RESTとGraphQL: `https://eu1.api.commerce.adobe.com`

![地域フィールドを持つCloud Managerのインスタンス作成ダイアログ &#x200B;](./assets/create-instance.png){width="600" align="center" zoomable="yes"}

{{aco-release}}

>[!ENDSHADEBOX]
