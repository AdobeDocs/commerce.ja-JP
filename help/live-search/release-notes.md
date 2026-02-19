---
title: '[!DNL Live Search] リリースノート'
description: Adobe Commerceからのの最新  [!DNL Live Search]  リリース情報です。
feature: Services, Search, Release Notes
exl-id: 099cf79c-968c-4381-b66d-7f6141ad2db3
source-git-commit: 85753091e3f7708c65cc8465050d03f44add04ae
workflow-type: tm+mt
source-wordcount: '2688'
ht-degree: 0%

---

# [!DNL Live Search] リリースノート

これらのリリースノートでは、[!DNL Live Search] の最新バージョンについて説明しています。

最新のリリースバージョンに対するサポートが提供されます。 古いバージョンのリリースノートが参照用に提供されています。
次のような更新があります。

![&#x200B; 新機能 &#x200B;](../assets/new.svg) 新機能
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 修正点および改善点
![&#x200B; バグ &#x200B;](../assets/bug.svg) 既知の問題

## ホステッド サービスの更新

これらのメモでは、バージョン管理されたリリースの外部で公開された更新や、ホストされるサービスの改善について説明します。

_2025 年 10 月 1 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg) 顧客がログインデータ用に `ds-logged-in` という名前の新しいデータストレージキーを追加しました。

_2025 年 4 月 29 日_

![&#x200B; 修正 &#x200B;](../assets/fix.svg) 「**パフォーマンス**」タブの [**CSV に書き出し**](./performance.md) レポートに、日付範囲で指定されたすべてのデータが含まれていない問題を修正しました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 検索クエリフィルターを使用した場合に、[&#x200B; マーチャンダイジングルール &#x200B;](./rules.md) を保存できなかった問題を修正しました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 結果ページの上部に [&#x200B; ピン留めされた製品 &#x200B;](./facets-manage.md#pinunpin-facet) が表示されない問題を修正しました。

_2025 年 4 月 21 日_

![&#x200B; 修正 &#x200B;](../assets/fix.svg) 価格の範囲フィルターの問題を修正して、上限範囲に等しい製品が結果に含まれないようにしました。 この変更は、ファセットの価格範囲の定義方法に合っています。

_2025 年 4 月 3 日_

![&#x200B; 修正 &#x200B;](../assets/fix.svg)SaaS データ書き出し拡張機能を更新し、B2B マーチャントの「製品をルートカテゴリに割り当てる必要がある」 [&#x200B; 制限 &#x200B;](boundaries-limits.md#b2b-and-category-permissions) を削除しました。 SaaS データ書き出し拡張機能をバージョン 103.4.0 以降に更新する方法については、[&#x200B; データ書き出し拡張機能の管理 &#x200B;](../data-export/manage-extension.md) を参照してください。

_2025 年 2 月 20 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg)Commerceでは、複数の単語の同義語をサポートしています。 [&#x200B; 詳細情報 &#x200B;](synonyms-type.md#multi-word-synonym-behavior)。 複数語の同義語のサポートは、この 2 月 20 日のリリース日以降にのみ使用できます。 既存の複数ワードの同義語を使用する場合は、完全な再インデックスが必要になります。これは、[&#x200B; サポートチケットを作成 &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) してリクエストできます。

_2025 年 1 月 31 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg) テスト環境には、クエリされていないカタログデータ用の新しいデータ保持ポリシーがあります。 [学習を増やす](overview.md#catalog-data-retention-policy)。

_2024 年 9 月 19 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg)Beta リリースで導入された高度な検索機能：`startsWith` と `contains` を使用したレイヤー検索。 [学習を増やす](workspace.md#layered-search-and-expansion-of-search-types)。

_2024 年 9 月 4 日_

![&#x200B; 修正 &#x200B;](../assets/fix.svg) 返すことができるバケットの最大数 [&#x200B; ファセット内 &#x200B;](boundaries-limits.md#facets) が 100 に増えました。

_2024 年 8 月 7 日_

![&#x200B; 修正 &#x200B;](../assets/fix.svg) 10,000 から 40,000,000 に [&#x200B; 価格ファセット &#x200B;](settings.md#price-faceting) の最大間隔値または価格範囲を増やしました。

_2024 年 2 月 13 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg) [!DNL Live Search] [&#x200B; 検索マーチャンダイジング &#x200B;](rules.md) のデフォルトルールの設定がサポートされるようになりました。

_2023 年 10 月 12 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg)Commerce管理者が、[!DNL Live Search] ーザーに対するインデックスの言語を指定できるようになりました。 [&#x200B; 設定 &#x200B;](settings.md) を参照してください。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 「検索ルール」タブの名前が「検索マーチャンダイジング」に変更されました。

_2023 年 6 月 13 日_

![&#x200B; 修正 &#x200B;](../assets/fix.svg) 引用符やアポストロフィなどの一部の文字がランキングの問題の原因となっていた問題を修正しました。 インデックス再作成を行うと、これらの問題は解決します。

_2023 年 4 月 25 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg) [!DNL Live Search] お客様は、新しい [SaaS 価格インデクサー &#x200B;](../price-index/price-indexing.md) を活用できるようになりました。

### PLP ウィジェット

_2026 年 2 月 2 日_

![&#x200B; 修正 &#x200B;](../assets/fix.svg)PLP バージョン 2.3.0 で、ブラウザーの「戻る」ボタンで PLP ウィジェットのページネーション状態が正しく更新されなかった問題を修正しました。

_2025 年 5 月 22 日_

![&#x200B; 修正 &#x200B;](../assets/fix.svg) ロケールがフランス語、ドイツ語、イタリア語、スペイン語に変更された際に、「買い物かごに追加」ボタンが英語のままになる問題を修正しました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 在庫切れの製品に対して「買い物かごに追加」ボタンが表示される問題を修正しました。

_2024 年 5 月 31 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg)PLP ウィジェットのバージョン 2.0.0 がリリースされました。このバージョンでは、次の機能がサポートされています。

- 「買い物かごに追加」ボタン – シンプルな製品でのみ使用できます。
- 製品ごとに複数の画像 – 設定可能な製品に対して別の色を選択すると、画像が変化する場合があります。

_2023 年 10 月 27 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg) [!DNL Live Search] PLP ウィジェットがカラースウォッチをサポートするようになりました。

## [!DNL Live Search] 4.6.1

_2026 年 2 月 19 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 修正 &#x200B;](../assets/fix.svg) ビジュアルマーチャンダイザー拡張機能の機能に関連する特定の条件下で発生する可能性があるエラーを修正しました。

## [!DNL Live Search] 4.6.0

_2025 年 10 月 9 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg)`startsWith` と `contains` を使用したレイヤー検索の次の詳細検索機能の GA リリースです。 [&#x200B; 詳細情報 &#x200B;](workspace.md#layered-search-and-expansion-of-search-types)。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) `ProductInterface` ライブサーチ [&#x200B; サービスの &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) オブジェクトは非推奨（廃止予定）になりました。 代わりに、カタログサービスの `ProductView` オブジェクトを使用します。

## [!DNL Live Search] 4.5.0

_2025 年 9 月 5 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) Live Search は、制限が有効な場合に Cookie/ローカルストレージでのデータ収集と保存を防ぐことで、[Cookie 制限モード &#x200B;](install.md#cookies) を完全に尊重するようになりました。

## [!DNL Live Search] 4.4.1

_2025 年 8 月 11 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 修正 &#x200B;](../assets/fix.svg) サンドボックス環境用の固定カタログサービスエンドポイント。

## [!DNL Live Search] 4.4.0

_2025 年 7 月 14 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) [&#x200B; 価格グループ化 &#x200B;](./settings.md#price-faceting) の上限を 50 から 100 に増加しました。

## [!DNL Live Search] 4.3.0

_2025 年 3 月 11 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 修正 &#x200B;](../assets/fix.svg) [!DNL Live Search] Adobe Commerce 2.4.8-beta2 を実行するインストールで、PHP 8.4 がサポートされるようになりました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 検索アダプターが `psr/http-message:2.0` と互換性がなかった問題を修正しました。

## [!DNL Live Search] 4.2.3

_2025 年 2 月 13 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 修正 &#x200B;](../assets/fix.svg) 注文詳細ページに注文番号、日付、**[!UICONTROL Reorder]** ボタンが表示されない問題を修正しました。

## [!DNL Live Search] 4.2.2

_2025 年 1 月 6 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 修正 &#x200B;](../assets/fix.svg) Adobe Commerce バージョン 2.4.5 以前の `categoryList` GraphqL クエリでエラーが発生していた問題を修正しました。

## [!DNL Live Search] 4.2.1

_2024 年 7 月 31 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 修正 &#x200B;](../assets/fix.svg) 特定のスクリプトがチェックアウトページに読み込まれない問題を修正しました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) `composer.json` ファイルの依存関係バージョンを修正しました。

## [!DNL Live Search] 4.2.0

_2024 年 5 月 31 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) PLP ウィジェットバージョン 2.0.0 を使用するように Live Search 拡張機能を更新しました。

## [!DNL Live Search] 4.1.2

_2024 年 5 月 16 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

### 更新

![&#x200B; 修正 &#x200B;](../assets/fix.svg) カテゴリの [`productSearch` と &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-by-categories) に基づいて正しくフィルタリングするように、`categoryPath` `categoryList` GraphQL クエリを修正しました。

## [!DNL Live Search] 4.1.1

_2024 年 3 月 19 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

### 新機能

![&#x200B; 新規 &#x200B;](../assets/new.svg) ポーランド語の言語サポートを追加しました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) [!DNL Live Search] Adobe Commerce 2.4.4 を実行するインストールで、PHP 8.3 がサポートされるようになりました。

## [!DNL Live Search] 4.1.0

_2024 年 2 月 22 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

### 新機能

![&#x200B; 新規 &#x200B;](../assets/new.svg) [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) が利用可能になりました。 この刷新されたダッシュボードでは、[!DNL Product Recommendations]、[!DNL Live Search] および [!DNL Catalog Service] のデータストリームに関するインサイトが提供されます。

### 更新

![&#x200B; 修正 &#x200B;](../assets/fix.svg) ゲストユーザーがデフォルト以外のストア表示で買い物かごに製品を追加した際にエラーが発生する問題を修正しました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) ロケールの設定に関係なく、検索ポップオーバーに通貨記号が常に価格値の前に表示される問題を修正しました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) インストール時の互換性の問題を修正するために、無効なコアプラグインの不要なタイプ定義を削除しました。

## [!DNL Live Search] 4.0.0

_2023 年 11 月 13 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

### 新機能

![&#x200B; 新規 &#x200B;](../assets/new.svg) [!DNL Live Search]PLP ウィジェットでカラースウォッチがサポートされるようになりました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) [!DNL Live Search] カテゴリ ID ではなくカテゴリ名が表示されるようになりました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) [!DNL Live Search]PLP ウィジェットで取り消し線による価格をサポートするようになりました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) フィルターパネルを非表示にする「フィルターを非表示」ボタンが導入されました。


### 更新

![&#x200B; 修正 &#x200B;](../assets/fix.svg) 新規インストールの場合、[!DNL Live Search] PLP ウィジェットがデフォルトで有効になりました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 検索アダプターは非推奨（廃止予定）になりました。 今後、検索アダプタは、セキュリティ上の問題に対処するためにのみ更新されます。
![&#x200B; 修正 &#x200B;](../assets/fix.svg)CSS スタイルを再設定し、ウィジェットクラスを適切に分離しました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 軽微なバグ修正

バージョン 3.1.1 以降をインストールしたら、新しいインデクサーを有効にします。

- 製品価格フィード
- スコープ web サイト データ フィード
- 範囲顧客グループデータフィード

アップグレード後、変更を実稼動環境にプッシュする前に、QA またはステージング環境で、更新された設定をテストします。

+++3.1.1 以前

### [!DNL Live Search] 3.1.1

_2023 年 9 月 15 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) 新しい「カテゴリマーチャンダイジング」タブが追加されました。 ユーザーは、カテゴリごとにインテリジェントランキングと手動ランキング（ピン、ブースト、埋め込み、非表示）を追加できるようになりました
![&#x200B; 新規 &#x200B;](../assets/new.svg) ユーザーは、インテリジェントまたは手動のランキングにより、単一のカテゴリルールを追加できます
![&#x200B; 新規 &#x200B;](../assets/new.svg) ユーザーは、サブカテゴリにインテリジェントなランキングルールを追加できるようになりました
![&#x200B; 新規 &#x200B;](../assets/new.svg) インテリジェントランキング付きのサブカテゴリを削除する際に、詳細な情報が提供されます
![&#x200B; 新規 &#x200B;](../assets/new.svg) 継承されたランキング戦略のルールを削除する機能が追加されました
![&#x200B; 新規 &#x200B;](../assets/new.svg) 単一カテゴリのルールを削除する機能が追加されました
![&#x200B; 新規 &#x200B;](../assets/new.svg) ルールを追加する際に、カテゴリ名で検索できるようになりました
![&#x200B; 新規 &#x200B;](../assets/new.svg) カテゴリツリー表示では、ルールが適用されているカテゴリを表示できるようになりました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) カテゴリプレビューには、選択したカテゴリのみが表示されます。
![&#x200B; 新規 &#x200B;](../assets/new.svg)AEM CIF[&#x200B; ポップオーバーウィジェット &#x200B;](https://github.com/adobe/aem-cif-guides-venia/pull/319) および [PLP ウィジェット &#x200B;](https://github.com/adobe/aem-cif-guides-venia/pull/320) コンポーネントを使用すると、AEM サイトで [!DNL Live Search] を活用できます。

#### 更新

![&#x200B; 修正 &#x200B;](../assets/fix.svg) 製品および価格フィードのテーブルサイズが大幅に縮小されました。 テーブル `catalog_data_exporter_products` および `catalog_data_exporter_product_prices` では、大幅なサイズ削減が必要です。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 「ルール」タブの名前が「検索ルール」に変更されました
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 「トレンド」でランキングする場合、次の中から選択できるようになりました。
- 3 日（デフォルト）
- 14 日間
- 30 日間
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 「イベント」（ブースト/ピン/ベリー/非表示）の名前は「手動ランキング」に変更されました
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 「ランキングタイプ」は「インテリジェントランキング」に名前が変更されました
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 軽微なバグ修正

### [!DNL Live Search] 3.1.0

_2023 年 9 月 1 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type="Informative" tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

#### 更新

![&#x200B; 修正 &#x200B;](../assets/fix.svg) 製品一覧表示ウィジェットが更新され、[Catalog Service API](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) を使用するようになりました。

### [!DNL Live Search] 3.0.2

_2023 年 8 月 7 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type="Informative" tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

#### 新機能

![&#x200B; 新規 &#x200B;](../assets/new.svg) 次の値が `storeDetails` オブジェクトに追加されました。

- 「1 ページにすべての製品を許可」
- 通貨レート
- 「グリッド許容値の 1 ページあたりの製品数」
- 「グリッドのデフォルト値の 1 ページあたりの製品数」
- ストアの言語

#### 更新

![&#x200B; 修正 &#x200B;](../assets/fix.svg) 高度なデータ取得をサポートするために、カタログサービスモジュールがメタパッケージに追加されました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 製品一覧表示ページウィジェットを使用したときに、「**マイアカウント**」ページナビゲーションが表示されなくなりました。

マーチャントがこれらの機能にアクセスするには、[!DNL Live Search] 拡張機能のバージョン >= 3.0.2 をアップグレードする必要があります。

実稼動環境にプッシュする前に、アップグレードとテストを行うことをお勧めします。 テスト環境の結果を確認した後、ピーク外の時間に実稼動環境をアップグレードすることを検討します。

#### 制限事項

Live Search Product Listing Page Widget を使用すると、Google Tag Manager が失敗する。 Google Tag Manager が必要な場合は、デフォルトの検索アダプタを使用します。

### [!DNL Live Search] 3.0.1

_2023 年 3 月 14 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type="Informative" tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

#### 新機能

![&#x200B; 新規 &#x200B;](../assets/new.svg) ルールプレビューの製品項目カード
![&#x200B; 新規 &#x200B;](../assets/new.svg) 製品一覧ペ [&#x200B; ジウィジェット &#x200B;](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-storefront/plp-styling)
![&#x200B; 新規 &#x200B;](../assets/new.svg) カテゴリ [&#x200B; フィルタリングオプション &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#facets)
![&#x200B; 新規 &#x200B;](../assets/new.svg) ドラッグ&amp;ドロップでピンイベントを作成する機能が追加されました
![&#x200B; 新規 &#x200B;](../assets/new.svg) 新しいピン留めアクション：
- スポットにピン留め – ボタンをピン留めして、ワンクリックでピンイベントを作成
 – 先頭にピン留め – 製品を先頭に配置します
 – 下部にピン留め – 結果の下部に製品を配置します
- ワンクリックでイベントのピン留めを解除
![&#x200B; ルール &#x200B;](../assets/new.svg) 新しい [&#x200B; インテリジェントランキング &#x200B;](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/rules/rules-add)
![&#x200B; 新規 &#x200B;](../assets/new.svg) [!DNL Live Search] は、Commerce（旧称：マルチSourceインベントリ、MSI）で完全な [Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction) 機能をサポートするようになりました。 完全なサポートを有効にするには、依存関係モジュールをバージョン 102.2.0 以降に [&#x200B; 更新 &#x200B;](install.md#update) する必要 `commerce-data-export` あります。

#### 更新

![&#x200B; 修正 &#x200B;](../assets/fix.svg) 「Configure Rules」で職階が自動的にソートされるようになりました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 既存のイベントを削除すると、プレビューが更新されるようになりました
![&#x200B; 修正 &#x200B;](../assets/fix.svg) イベントのないルールは保存できません
![&#x200B; 修正 &#x200B;](../assets/fix.svg) ファセットを削除する「タイプを選択」セレクター
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 未保存のルールに新しい「編集中」ステータスを追加しました

#### 修正点

![&#x200B; 修正 &#x200B;](../assets/fix.svg) 保存中に未完了のイベントがある場合のサーバーエラーを修正しました
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 複数のイベントが存在する場合の、特定のイベントの正しい削除を修正しました
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 新しいイベントが追加された際に、既存のルールイベントが更新されない修正
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 詳細からの 2 回目の「編集」クリックで修正されました。ページ [!DNL Live Search] リロードが必要です
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 同義語：ユーザーが入力をクリックアウトしても、フォーカスをフィールドに戻すことができない問題を修正しました
![&#x200B; 修正 &#x200B;](../assets/fix.svg) その他のマイナーなバグ修正とパフォーマンスの更新
![&#x200B; バグ &#x200B;](../assets/bug.svg) – 「あなたにお勧め」によるランキングは、ライブ検索ウィジェット内でのみサポートされています。 デフォルトの Luma およびPWAの検索機能ではサポートされません。
![&#x200B; バグ &#x200B;](../assets/bug.svg) - カスタムの価格属性ファセットが Luma で正しくレンダリングされませんが、API が適切にフィルタリングします。

マーチャントがこれらの機能にアクセスするには、[!DNL Live Search] 拡張機能のバージョン 3.0.1 をアップグレードする必要があります。

実稼動環境にプッシュする前に、アップグレードとテストを行うことをお勧めします。 テスト環境の結果を確認した後、ピーク外の時間に実稼動環境をアップグレードすることを検討します。

### [!DNL Live Search] 2.0.5

[!BADGE &#x200B; サポート対象 &#x200B;]{type="Informative" tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 修正 &#x200B;](../assets/fix.svg) - ネットワークの問題が原因でSDK リソースが使用できない場合、Live Search がエラーをスローします。 このバグは修正されました。

マーチャントがこれらの機能にアクセスするには、Live Search 拡張機能のバージョン >= 2.0.5 をアップグレードする必要があります。

実稼動環境にプッシュする前に、アップグレードとテストを行うことをお勧めします。 テスト環境の結果を確認した後、ピーク外の時間に実稼動環境をアップグレードすることを検討します。

### [!DNL Live Search] 2.0.4

[!BADGE &#x200B; サポート対象 &#x200B;]{type="Informative" tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) ライブサーチでは、管理者の「在庫切れの製品を表示」設定によるフィルタリングをサポートするようになりました。 「在庫切れの製品を表示」を false に設定すると、`inStock = true` がフィルターに追加されます。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) パフォーマンスを向上させるために、ライブ検索のポップアップから「候補」ブロックが削除されました。 機能を置き換える場合に備えて、データはGraphQLを通じて渡されます。
カテゴリフィルタリングのため、![&#x200B; 修正 &#x200B;](../assets/fix.svg) `categories` と `categoryPath` は `categoryIds` に取って代わりました。 詳しくは、「[productSearch](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/)」トピックを参照してください。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 以前は、B2B 会社に関連付けられているユーザーが検索を行うと、誤った顧客グループコードが表示されていました。 ライブサーチが正しい値を返すようになりました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 以前は、存在しない用語を検索すると、Live Search がエラーを返していました。 そのバグが修正されました。

マーチャントがこれらの機能にアクセスするには、[!DNL Live Search] 拡張機能のバージョン >= 2.0.4 をアップグレードする必要があります。

実稼動環境にプッシュする前に、アップグレードとテストを行うことをお勧めします。 テスト環境の結果を確認した後、ピーク外の時間に実稼動環境をアップグレードすることを検討します。

### [!DNL Live Search] 2.0.3

[!BADGE &#x200B; サポート対象 &#x200B;]{type="Informative" tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新機能 &#x200B;](../assets/new.svg) ライブサーチでは、カテゴリ権限、共有カタログ、顧客グループ固有の価格を考慮することで、B2B 機能をサポートするようになりました。

マーチャントがこれらの機能にアクセスするには、[!DNL Live Search] 拡張機能のバージョン 2.0.3 をアップグレードする必要があります。

実稼動環境にプッシュする前に、アップグレードとテストを行うことをお勧めします。 テスト環境の結果を確認した後、ピーク外の時間に実稼動環境をアップグレードすることを検討します。

### [!DNL Live Search] 2.0

[!BADGE &#x200B; サポート対象 &#x200B;]{type="Informative" tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

以下の新機能、修正点および改善点を利用するには、既存の [!DNL Live Search] インストールを [!DNL Live Search] 2.0.0 にアップグレードする必要があります。

![&#x200B; 新規 &#x200B;](../assets/new.svg) [!DNL Live Search]Adobe Commerce 2.4.4 を実行するインストールで、PHP 8.1 がサポートされるようになりました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) インストール中に無効になるモジュールのリストに `Magento_ElasticsearchCatalogPermissionsGraphQl` モジュールが追加されます。
![&#x200B; 新規 &#x200B;](../assets/new.svg) [[!DNL storefront popover]](overview.md) で使用可能な行数は、*Admin* から設定できます。
![&#x200B; 新規 &#x200B;](../assets/new.svg) Beta [PWA](https://developer.adobe.com/commerce/pwa-studio/) が [!DNL Live Search] でサポートされました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) [!DNL Live Search] インストールプロセスが、詳細なプロセス変更によって更新されました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) [&#x200B; 詳細検索 &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) リンクがストアフロントのフッターから削除されました。
![&#x200B; バグ &#x200B;](../assets/bug.svg) 次の製品属性は、PWAのベータ版リリースに関連して使用される場合、[Commerce GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/) でサポートされていません：`description`、`name`、`short_description`
![&#x200B; バグ &#x200B;](../assets/bug.svg) PWA for [!DNL Live Search] のベータ版リリースでは、[&#x200B; イベント処理 &#x200B;](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/) がサポートされていません。

### [!DNL Live Search] 1.3.1

[!BADGE &#x200B; サポート対象 &#x200B;]{type="Informative" tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![Fix](../assets/fix.svg) [Custom price 属性 &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types) が [facet](facets-add.md) として設定された場合にエラーが返されなくなりました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) [&#x200B; 通貨記号 &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration#step-5-customize-currency-symbols-optional) （`data-currency-symbol`）が使用できない場合にエラーが発生する問題を修正しました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) [[!DNL Storefront popover]](storefront-popover.md) 利用可能な場合、[&#x200B; 特別価格 &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-special) （最終価格の最小値）が表示されるようになりました。

### [!DNL Live Search] 1.3.0

[!BADGE &#x200B; サポート対象 &#x200B;]{type="Informative" tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) [&#x200B; パフォーマンス &#x200B;](performance.md) レポートダッシュボードは、買い物客が使用する検索用語にinsightを提供します。
![&#x200B; 新規 &#x200B;](../assets/new.svg) [!DNL Live Search] [&#x200B; ストアフロントイベントSDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/) を使用すると、イベントの公開サービス、サブスクリプションサービス、指標を含む共通のデータレイヤーにアクセスできます。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) [[!DNL Storefront popover]](storefront-popover.md) には、表示を制御する `active` コンテナ用の新しい `.search-autocomplete` クラスがあります。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) ストアフロントで、[&#x200B; 検索語句 &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-terms) フッターリンクが削除され、[!DNL Live Search] のインストールではキャッシュが無効になります。
![&#x200B; バグ &#x200B;](../assets/bug.svg) 検索アダプタのパッチが重複した製品を処理します。
![&#x200B; バグ &#x200B;](../assets/bug.svg) [!DNL Live Search] は、複数の [&#x200B; 仮想） &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/sources/sources-manage) 在庫 [&#x200B; を持つ（単一ソース &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/stocks/stocks-manage) （物理）在庫の場所をサポートしています。 複数のインベントリソースは現在サポートされていません。

### [!DNL Live Search] 1.2.0

[!BADGE &#x200B; サポート対象 &#x200B;]{type="Informative" tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) [[!DNL Storefront popover]](storefront-popover.md) 買い物客が検索ボックスにクエリを入力すると、候補となる製品と上位の検索結果のサムネール画像が表示されます。
![&#x200B; 新規 &#x200B;](../assets/new.svg) Commerce *管理者* セッションは、キーボードが無操作状態が長時間続いている間も開いたままになります
![&#x200B; 新規 &#x200B;](../assets/new.svg) [!DNL Live Search] は、オンボーディング後に自動的に有効になります
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 最初のインデックス作成時間が 1 時間未満である
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 製品の増分更新をほぼリアルタイム（インストールとセットアップ後）
![&#x200B; 修正 &#x200B;](../assets/fix.svg) シノニム・エディタのソート可能な列
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 検索条件 [!DNL Live Search] 空の並べ替え順の値が含まれる場合に、エラーがスローされなくなりました
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 属性コードに「to」または「from」の文字列が含まれている場合に、範囲フィルタリングが機能しなくなった

### [!DNL Live Search] 1.1.0

[!BADGE &#x200B; サポート対象 &#x200B;]{type="Informative" tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![&#x200B; バグ &#x200B;](../assets/bug.svg) [!DNL Live Search] サービスでは、Adobe Commerce インストールの [&#x200B; 基本通貨 &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration) のみをサポートしています。
![&#x200B; バグ &#x200B;](../assets/bug.svg) ファセットを追加するときに、「`Update on Save`」に設定すると、製品属性フィードが正しく更新されない。 この問題を回避するには、[&#x200B; インデックス管理 &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) に移動し、製品属性フィードを `Update by Schedule` に設定します。
![&#x200B; バグ &#x200B;](../assets/bug.svg) [!DNL Live Search] 同義語はストアビューごとに定義されていますが、現在は web サイトごとに保存され、`environmentId` と `storeViewCode` の組み合わせで識別されています。 その結果、Adobe Commerce インストール内のすべての web サイトとストアビューで同義語が共有されます。 ストア表示の最近作成された同義語セットが優先されます。
![&#x200B; バグ &#x200B;](../assets/bug.svg) 同義語の用語に複数の単語が含まれている場合、各単語は個別の同義語として扱われます。 例えば、「time piece」を「watch」の同義語として定義した場合、「time」と「piece」の両方が watch の同義語として扱われます。

+++

## マニュアル

詳細情報：

- [Adobe Commerce開発者向けドキュメント &#x200B;](https://developer.adobe.com/commerce/docs)
- [Adobe Commerce ユーザーガイド &#x200B;](https://experienceleague.adobe.com/en/docs/commerce)
- [[!DNL Live Search] on Marketplace](https://commercemarketplace.adobe.com/magento-live-search.html)
