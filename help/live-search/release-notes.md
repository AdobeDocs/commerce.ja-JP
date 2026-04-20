---
title: '[!DNL Live Search] リリースノート'
description: Adobe Commerceからの [!DNL Live Search] の最新のリリース情報。
feature: Services, Search, Release Notes
exl-id: 099cf79c-968c-4381-b66d-7f6141ad2db3
source-git-commit: 14c4178338859d55a7391139033d51d1aa6f7678
workflow-type: tm+mt
source-wordcount: '2708'
ht-degree: 0%

---

# [!DNL Live Search] リリースノート

これらのリリースノートには、[!DNL Live Search]の最新バージョンが記載されています。

最新リリースのライブサーチ版のサポートが提供されます。 古いバージョンのリリースノートは、参照用に提供されています。
アップデートには以下が含まれます。

![新機能](../assets/new.svg)
![修正](../assets/fix.svg)修正と機能強化
![&#x200B; バグ &#x200B;](../assets/bug.svg)既知の問題

## ホスト型サービスの更新

これらのメモでは、バージョン管理されたリリース以外で公開されたアップデートや、ホストされたサービスの改善について説明します。

_2025年10月1日_

![新規](../assets/new.svg)顧客がログインしたデータの`ds-logged-in`という名前の新しいデータストレージキーを追加しました。

_2025年4月29日_

![修正](../assets/fix.svg) 「**パフォーマンス**」タブの&#x200B;[**CSV**](./performance.md)への書き出しレポートに、日付範囲で指定されたすべてのデータが含まれていない問題を修正しました。
![修正](../assets/fix.svg)検索クエリフィルターを使用した場合、[&#x200B; マーチャンダイジングルール &#x200B;](./rules.md)を保存できない問題を修正しました。
![修正](../assets/fix.svg)結果ページの上部に[&#x200B; ピン留めされた製品](./facets-manage.md#pinunpin-facet)が表示されない問題を修正しました。

_2025年4月21日_

![修正](../assets/fix.svg)価格の範囲フィルターの問題を修正して、上限値と等しい商品が結果に含まれないようにしました。 この変更は、ファセットの価格帯の定義方法と一致しています。

_2025年4月3日_

![修正](../assets/fix.svg) SaaS データ書き出し拡張機能を更新して、B2B マーチャントの「製品をルートカテゴリに割り当てる必要があります」を削除しました[制限](boundaries-limits.md#b2b-and-category-permissions)。 SaaS データ書き出し拡張機能をバージョン 103.4.0以降に更新する方法については、[&#x200B; データ書き出し拡張機能の管理](../data-export/manage-extension.md)を参照してください。

_2025年2月20日_

![新規](../assets/new.svg) Commerceは、複数の単語の類義語をサポートしています。 [詳細情報](synonyms-type.md#multi-word-synonym-behavior)。 マルチワードの類義語のサポートは、この2月20日のリリース日以降のみ利用可能です。 既存のマルチワードの類義語を使用する場合は、完全なインデックス再作成が必要です。このインデックスを作成するには、[&#x200B; サポートチケットの作成](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)を依頼してください。

_2025年1月31日_

![新規](../assets/new.svg) テスト環境に、クエリされていないカタログデータに対する新しいデータ保持ポリシーがあります。 [学習を増やす](overview.md#catalog-data-retention-policy)。

_2024年9月19日_

次の高度な検索機能の![New](../assets/new.svg) Beta リリース：`startsWith`と`contains`を使用した階層検索。 [学習を増やす](workspace.md#layered-search-and-expansion-of-search-types)。

_2024年9月4日_

![修正](../assets/fix.svg) ファセット内で[返すことができるバケットの最大数を100に増やしました](boundaries-limits.md#facets)。

_2024年8月7日_

![修正](../assets/fix.svg) [価格ファセット &#x200B;](settings.md#price-faceting)の最大区間値または価格範囲を10,000から40,000,000に増加しました。

_2024年2月13日_

![新規](../assets/new.svg) [!DNL Live Search]では、[検索マーチャンダイジング &#x200B;](rules.md)のデフォルトルールの設定がサポートされるようになりました。

_2023年10月12日_

![新規](../assets/new.svg) Commerce管理者は、[!DNL Live Search]のインデックスの言語を指定できるようになりました。 [設定](settings.md)を参照してください。
![修正](../assets/fix.svg) 「検索ルール」タブの名前が「マーチャンダイジングを検索」に変更されました。

_2023年6月13日_

![修正](../assets/fix.svg)引用符やアポストロフィなどの一部の文字がランキングの問題を引き起こす問題を修正しました。 インデックスを再作成すると、これらの問題を解決できます。

_2023年4月25日_

![新規](../assets/new.svg) [!DNL Live Search]のお客様は、新しい[SaaS価格インデックス &#x200B;](../price-index/price-indexing.md)を利用できるようになりました。

### PLP ウィジェット

_2026年2月2日_

![修正](../assets/fix.svg) ブラウザーの戻るボタンがPLP ウィジェットのページネーション状態を正しく更新しなかったPLP バージョン 2.3.0の問題を修正しました。

_2025年5月22日_

![修正](../assets/fix.svg) ロケールがフランス語、ドイツ語、イタリア語またはスペイン語に変更された場合に「買い物かごに追加」ボタンが英語のままになる問題を修正しました。
![修正](../assets/fix.svg)在庫切れ商品の「カートに追加」ボタンが表示される問題を修正しました。

_2024年5月31日_

![新規](../assets/new.svg) PLP ウィジェットのバージョン 2.0.0がリリースされ、次の機能がサポートされるようになりました。

- 「カートに追加」ボタン – シンプルな商品でのみ利用可能。
- 製品ごとに複数の画像 – 設定可能な製品に異なる色を選択すると、画像が変更される場合があります。

_2023年10月27日_

![新規](../assets/new.svg) [!DNL Live Search] PLP ウィジェットでカラースウォッチがサポートされるようになりました。

## [!DNL Live Search] 4.7.0

_2026年3月17日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) PHP 8.5のサポートを追加しました。

## [!DNL Live Search] 4.6.1

_2026年2月19日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg) Visual Merchandiser拡張機能の機能に関連する特定の条件で発生する可能性のあるエラーを修正しました。

## [!DNL Live Search] 4.6.0

_2025年10月9日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

次の高度な検索機能に関する![新規](../assets/new.svg)のGA リリース：`startsWith`と`contains`を使用した階層検索。 [詳細情報](workspace.md#layered-search-and-expansion-of-search-types)。
![修正](../assets/fix.svg) `ProductInterface` ライブサーチ [&#x200B; サービスの](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) オブジェクトは非推奨（廃止予定）になりました。 代わりに、カタログサービスで`ProductView` オブジェクトを使用してください。

## [!DNL Live Search] 4.5.0

_2025年9月5日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) ライブサーチでは、制限が有効になっている場合、Cookie/ローカルストレージでのデータ収集と保存を防ぐことにより、[Cookie制限モード &#x200B;](install.md#cookies)を完全に尊重するようになりました。

## [!DNL Live Search] 4.4.1

_2025年8月11日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg) サンドボックス環境の固定カタログサービスエンドポイント。

## [!DNL Live Search] 4.4.0

_2025年7月14日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) [価格グループ化](./settings.md#price-faceting)の上限を50から100に増加しました。

## [!DNL Live Search] 4.3.0

_2025年3月11日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg) [!DNL Live Search]は、Adobe Commerce 2.4.8-beta2を実行するインストールでPHP 8.4をサポートするようになりました。
![修正](../assets/fix.svg)検索アダプタが`psr/http-message:2.0`と互換性がない問題を修正しました。

## [!DNL Live Search] 4.2.3

_2025年2月13日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg)注文詳細ページに注文番号、日付、**[!UICONTROL Reorder]** ボタンが表示されない問題を修正しました。

## [!DNL Live Search] 4.2.2

_2025年1月6日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg) Adobe Commerce バージョン 2.4.5以前の`categoryList` GraphqL クエリでエラーが発生していた問題を修正しました。

## [!DNL Live Search] 4.2.1

_2024年7月31日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg)特定のスクリプトがチェックアウトページに読み込まれない問題を修正しました。
![修正](../assets/fix.svg) `composer.json` ファイルの依存関係のバージョンを修正しました。

## [!DNL Live Search] 4.2.0

_2024年5月31日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) PLP ウィジェット バージョン 2.0.0を使用するようにライブ検索拡張機能を更新しました。

## [!DNL Live Search] 4.1.2

_2024年5月16日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

### 更新

![修正](../assets/fix.svg) [`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-by-categories) GraphQL クエリが、カテゴリの`categoryPath`と`categoryList`に基づいて正しくフィルタリングされるように修正しました。

## [!DNL Live Search] 4.1.1

_2024年3月19日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

### 新機能

![新規](../assets/new.svg) ポーランド語の言語サポートを追加しました。
![新規](../assets/new.svg) [!DNL Live Search]は、Adobe Commerce 2.4.4を実行するインストールでPHP 8.3をサポートするようになりました。

## [!DNL Live Search] 4.1.0

_2024年2月22日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

### 新機能

![新規](../assets/new.svg) [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)が利用可能になりました。 この刷新されたダッシュボードは、[!DNL Product Recommendations]、[!DNL Live Search]および[!DNL Catalog Service]のデータストリームに関するインサイトを提供します。

### 更新

![修正](../assets/fix.svg) ゲストユーザーがデフォルト以外のストアビューで商品をカートに追加したときにエラーが発生する問題を修正しました。
![修正](../assets/fix.svg)検索ポップオーバーで、ロケール設定に関係なく、価格の値の前に通貨記号が常に表示される問題を修正しました。
![修正](../assets/fix.svg)無効なコアプラグインの不要な型定義を削除して、インストール時の互換性の問題を修正しました。

## [!DNL Live Search] 4.0.0

_2023年11月13日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

### 新機能

![新規](../assets/new.svg) [!DNL Live Search]は、PLP ウィジェットでカラースウォッチをサポートするようになりました。
![新規](../assets/new.svg) [!DNL Live Search]には、カテゴリ IDではなくカテゴリ名が表示されるようになりました。
![新規](../assets/new.svg) [!DNL Live Search]は、PLP ウィジェットで取り消し価格をサポートするようになりました。
![新規](../assets/new.svg) フィルターパネルを非表示にする「フィルターを非表示」ボタンが導入されました。


### 更新

![修正](../assets/fix.svg) [!DNL Live Search] PLP ウィジェットが、新規インストールに対してデフォルトで有効になりました。
![修正](../assets/fix.svg)検索アダプタは非推奨（廃止予定）です。 今後、検索アダプタは、セキュリティの問題に対処するためにのみ更新されます。
![修正](../assets/fix.svg)CSS スタイルを再構成して、ウィジェットクラスをより適切に分離しました。
![軽微なバグ修正](../assets/fix.svg)件

バージョン 3.1.1以降をインストールした後、新しいインデクサーを有効にします。

- 製品価格フィード
- Web サイトのデータフィードの範囲
- 顧客グループのデータフィードの範囲

アップグレード後、変更を実稼動環境にプッシュする前に、更新された設定をQAまたはステージングでテストします。

+++3.1.1以前

### [!DNL Live Search] 3.1.1

_2023年9月15日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)新しいカテゴリ マーチャンダイジングタブが追加されました。 ユーザーは、カテゴリごとにインテリジェントなランキングと手動ランキング（ピン、ブースト、埋め込み、非表示）を追加できるようになりました
![新規](../assets/new.svg) ユーザーは、インテリジェントまたは手動のランキングで1つのカテゴリ ルールを追加できます
![新規](../assets/new.svg) ユーザーがインテリジェントなランキングルールをサブカテゴリに追加できるようになりました
![新](../assets/new.svg) インテリジェントなランキングを使用してサブカテゴリを削除すると、詳細な情報が提供されます
![新規](../assets/new.svg)継承されたランキング戦略のルールを削除する機能を追加しました
![新規](../assets/new.svg)単一カテゴリのルールを削除する機能を追加しました
![新規](../assets/new.svg) ユーザーがルールを追加するときに、カテゴリ名で検索できるようになりました
![新規](../assets/new.svg) カテゴリツリー表示で、ユーザーはルールが適用されているカテゴリを表示できるようになりました。
![新規](../assets/new.svg) カテゴリのプレビューには、選択したカテゴリのみが表示されます。
![新規](../assets/new.svg) AEM CIF [&#x200B; ポップオーバーウィジェット &#x200B;](https://github.com/adobe/aem-cif-guides-venia/pull/319)および[PLP ウィジェット &#x200B;](https://github.com/adobe/aem-cif-guides-venia/pull/320) コンポーネントを使用すると、AEM サイトで[!DNL Live Search]を利用できます。

#### 更新

![修正](../assets/fix.svg)製品と価格フィードのテーブルサイズが大幅に削減されました。 テーブル `catalog_data_exporter_products`と`catalog_data_exporter_product_prices`のサイズを大幅に縮小する必要があります。
![修正](../assets/fix.svg) 「ルール」タブの名前が「ルールを検索」に変更されました
![修正](../assets/fix.svg) 「トレンド」でランキングする際に、次のいずれかを選択できるようになりました。
- 3日間（デフォルト）
- 14日間
- 30日間
![修正](../assets/fix.svg) 「イベント」（ブースト/ピン/埋め込み/非表示）の名前が「手動ランキング」に変更されました
![修正](../assets/fix.svg) 「ランキングタイプ」の名前が「インテリジェントランキング」に変更されました
![軽微なバグの修正](../assets/fix.svg)

### [!DNL Live Search] 3.1.0

_2023年9月1日_

[!BADGE &#x200B; サポートされている]{type="Informative" tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

#### 更新

![修正](../assets/fix.svg)製品リストウィジェットが更新され、[&#x200B; カタログサービス API](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/)が使用されるようになりました。

### [!DNL Live Search] 3.0.2

_2023年8月7日_

[!BADGE &#x200B; サポートされている]{type="Informative" tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

#### 新機能

![新規](../assets/new.svg) `storeDetails` オブジェクトに次の値が追加されました：

- 「ページごとのすべての製品を許可」
- 通貨レート
- 「グリッドで許可される値の1 ページあたりの製品」
- 「グリッドのページあたりの製品のデフォルト値」
- ストア言語

#### 更新

高度なデータ取得をサポートするために、![修正](../assets/fix.svg) カタログ サービス モジュールがメタパッケージに追加されました。
![修正](../assets/fix.svg)製品リストページ ウィジェットを使用すると、**マイアカウント** ページナビゲーションが消えなくなりました。

これらの機能にアクセスするには、[!DNL Live Search]拡張機能バージョン >= 3.0.2をアップグレードする必要があります。

実稼動にプッシュする前に、アップグレードしてテストすることをお勧めします。 テスト環境の結果を検証した後、オフピーク時間中に本番環境をアップグレードすることを検討してください。

#### 制限

ライブサーチの商品リストページ ウィジェットを使用すると、Google Tag Managerが失敗します。 Google Tag Managerが必要な場合は、デフォルトの検索アダプタを使用します。

### [!DNL Live Search] 3.0.1

_2023年3月14日_

[!BADGE &#x200B; サポートされている]{type="Informative" tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

#### 新機能

ルールプレビューの![新規](../assets/new.svg)製品項目カード
![新規](../assets/new.svg) [製品リストページ ウィジェット &#x200B;](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-storefront/plp-styling)
![新規](../assets/new.svg) [&#x200B; カテゴリフィルターオプション &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#facets)
![新規](../assets/new.svg) ピンイベントを作成するためのドラッグ&amp;ドロップ機能を追加しました
![新規](../assets/new.svg)新しいピン操作：
- Pin to spot - Pin ボタンをクリックするだけでPin イベントを作成
- Pin to top – 製品を最初の位置に配置します
- Pin to bottom – 結果の一番下に製品を配置します
- ワンクリックでイベントのピン留めを解除
![新規](../assets/new.svg) [&#x200B; ルールのインテリジェントなランキング &#x200B;](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/rules/rules-add)
![新規](../assets/new.svg) [!DNL Live Search]では、Commerceの[Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction)機能が完全にサポートされるようになりました（以前はマルチSource インベントリ（MSI）と呼ばれていました）。 完全なサポートを有効にするには、依存関係モジュール [をバージョン 102.2.0以降に](install.md#updating-live-search)更新`commerce-data-export`する必要があります。

#### 更新

![修正](../assets/fix.svg) ルールの設定で、位置が一意に自動的に並べ替えられるようになりました
![修正](../assets/fix.svg)既存のイベントを削除すると、プレビューが更新されます
イベントのない![修正](../assets/fix.svg) ルールは保存できません
![修正](../assets/fix.svg) ファセットの削除「タイプを選択」セレクター
![修正](../assets/fix.svg)未保存のルールの新しい「編集」ステータスを追加しました

#### 修正

![修正](../assets/fix.svg)保存中に未完成のイベントがある場合の固定サーバーエラー
![修正](../assets/fix.svg)複数のイベントがある場合に特定のイベントを正しく削除する問題を修正しました
![修正](../assets/fix.svg)新しいイベントが追加されたときに、既存のルールイベントが更新されない問題を修正しました
![修正](../assets/fix.svg) 2回目の「編集」クリックで修正されました。詳細、[!DNL Live Search] ページで再読み込みが必要です
![修正](../assets/fix.svg)類義語：ユーザーが入力からクリックアウトした際に、フィールドにフォーカスを返すことができなかった問題を修正しました
![修正](../assets/fix.svg)その他のマイナーなバグ修正とパフォーマンスの更新
![&#x200B; バグ &#x200B;](../assets/bug.svg) - 「おすすめ」によるランキングは、ライブサーチウィジェット内でのみサポートされています。 デフォルトのLumaおよびPWA検索機能ではサポートされていません。
![&#x200B; バグ &#x200B;](../assets/bug.svg) - カスタム価格属性ファセットがLumaで正しくレンダリングされませんが、APIは正しくフィルタリングします。

これらの機能にアクセスするには、[!DNL Live Search]拡張機能バージョン >= 3.0.1をアップグレードする必要があります。

実稼動にプッシュする前に、アップグレードしてテストすることをお勧めします。 テスト環境の結果を検証した後、オフピーク時間中に本番環境をアップグレードすることを検討してください。

### [!DNL Live Search] 2.0.5

[!BADGE &#x200B; サポートされている]{type="Informative" tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg) - ネットワークの問題によりSDK リソースが使用できない場合、ライブ検索でエラーがスローされます。 このバグは修正されています。

これらの機能にアクセスするには、Live Search拡張機能のバージョン >= 2.0.5をアップグレードする必要があります。

実稼動にプッシュする前に、アップグレードしてテストすることをお勧めします。 テスト環境の結果を検証した後、オフピーク時間中に本番環境をアップグレードすることを検討してください。

### [!DNL Live Search] 2.0.4

[!BADGE &#x200B; サポートされている]{type="Informative" tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) ライブ検索で、管理者の「在庫切れ商品を表示」設定によるフィルタリングがサポートされるようになりました。 「在庫切れ商品を表示」がfalseに設定されている場合、`inStock = true`がフィルターに追加されます。
![修正](../assets/fix.svg) パフォーマンスを向上させるために、ライブ検索ポップアップから「提案」ブロックが削除されました。 この機能を置き換えたい場合でも、データはGraphQLを通じて渡されます。
![修正](../assets/fix.svg) `categories`と`categoryPath`が、カテゴリーフィルタリング用に`categoryIds`を置き換えました。 詳しくは、[productSearch](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) トピックを参照してください。
![修正](../assets/fix.svg)以前は、B2B企業に関連付けられたユーザーが検索を行うと、誤った顧客グループコードを受け取っていました。 ライブサーチが正しい値を返すようになりました。
![修正](../assets/fix.svg)以前は、存在しない用語を検索すると、ライブサーチでエラーが返されていました。 そのバグは現在修正されています。

これらの機能にアクセスするには、[!DNL Live Search]拡張機能バージョン >= 2.0.4をアップグレードする必要があります。

実稼動にプッシュする前に、アップグレードとテストを行うことをお勧めします。 テスト環境の結果を検証した後、オフピーク時間中に本番環境をアップグレードすることを検討してください。

### [!DNL Live Search] 2.0.3

[!BADGE &#x200B; サポートされている]{type="Informative" tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) ライブサーチでは、カテゴリ権限、共有カタログ、顧客グループ固有の価格設定を尊重することで、B2B機能をサポートするようになりました。

これらの機能にアクセスするには、[!DNL Live Search]拡張機能バージョン >= 2.0.3をアップグレードする必要があります。

実稼動にプッシュする前に、アップグレードとテストを行うことをお勧めします。 テスト環境の結果を検証した後、オフピーク時間中に本番環境をアップグレードすることを検討してください。

### [!DNL Live Search] 2.0

[!BADGE &#x200B; サポートされている]{type="Informative" tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

次の新機能、修正、および機能強化を活用するには、既存の[!DNL Live Search] インストールを[!DNL Live Search] 2.0.0にアップグレードする必要があります。

![新規](../assets/new.svg) [!DNL Live Search]は、Adobe Commerce 2.4.4を実行するインストールでPHP 8.1をサポートするようになりました。
![新規](../assets/new.svg) `Magento_ElasticsearchCatalogPermissionsGraphQl` モジュールが、インストール中に無効化されたモジュールのリストに追加されます。
![新規](../assets/new.svg) [[!DNL storefront popover]](overview.md)の使用可能な行数は、*管理者*から設定できます。
![新規](../assets/new.svg) Beta [PWA](https://developer.adobe.com/commerce/pwa-studio/)は[!DNL Live Search]でサポートされています。
![新規](../assets/new.svg) [!DNL Live Search]のインストールプロセスが更新され、高度なプロセスが変更されます。
![修正](../assets/fix.svg) [詳細検索](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) リンクがストアフロント フッターから削除されました。
![&#x200B; バグ &#x200B;](../assets/bug.svg)次の製品属性は、[Commerce GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/)で、PWAのベータ版リリースに関連して使用されている場合はサポートされていません：`description`、`name`、`short_description`
![&#x200B; バグ &#x200B;](../assets/bug.svg) [!DNL Live Search]のPWAのベータ版リリースは、[&#x200B; イベント処理](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/)をサポートしていません。

### [!DNL Live Search] 1.3.1

[!BADGE &#x200B; サポートされている]{type="Informative" tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![修正](../assets/fix.svg) [&#x200B; カスタム価格属性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types)は、[&#x200B; ファセット &#x200B;](facets-add.md)として設定した際にエラーを返さなくなりました。
![修正](../assets/fix.svg)使用可能な[通貨シンボル &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration#step-5-customize-currency-symbols-optional) （`data-currency-symbol`）がない場合にエラーが発生する問題を修正しました。
![修正](../assets/fix.svg) [[!DNL Storefront popover]](storefront-popover.md)には、利用可能な場合に[特別価格](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-special) （最低最終価格）が表示されるようになりました。

### [!DNL Live Search] 1.3.0

[!BADGE &#x200B; サポートされている]{type="Informative" tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg) [&#x200B; パフォーマンス &#x200B;](performance.md) レポート ダッシュボードでは、買い物客が使用する検索語にinsightが使用されます。
![新規](../assets/new.svg) [!DNL Live Search] [Storefront Events SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/)では、イベントの公開とサブスクリプションサービス、および指標を使用して、共通のデータレイヤーにアクセスできます。
![修正](../assets/fix.svg) [[!DNL Storefront popover]](storefront-popover.md)には、表示を制御する`active` コンテナ用の新しい`.search-autocomplete` クラスがあります。
![修正](../assets/fix.svg) ストアフロントでは、[検索語](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-terms) フッターリンクが削除され、[!DNL Live Search]回のインストールでキャッシュが無効になります。
検索アダプタの![&#x200B; バグ &#x200B;](../assets/bug.svg) パッチは、重複する製品を処理します。
![&#x200B; バグ &#x200B;](../assets/bug.svg) [!DNL Live Search]は、複数の（仮想） [在庫](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/sources/sources-manage)を持つ[&#x200B; シングルソース &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/stocks/stocks-manage) （物理）在庫場所をサポートしています。 現在、複数の在庫ソースはサポートされていません。

### [!DNL Live Search] 1.2.0

[!BADGE &#x200B; サポートされている]{type="Informative" tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg) [[!DNL Storefront popover]](storefront-popover.md)は、買い物客が検索ボックスにクエリを入力すると、上位の検索結果の推奨商品とサムネール画像を表示します。
キーボードが非アクティブな状態が長期間続くと、![新規](../assets/new.svg) Commerce *管理者* セッションが開いたままになる
![新規](../assets/new.svg) [!DNL Live Search]は、オンボーディング後に自動的に有効になります
![修正](../assets/fix.svg)最初のインデックス作成時間が1時間未満です
![修正](../assets/fix.svg)製品の増分更新をほぼリアルタイムで（インストールおよびセットアップ後）
![類義語エディターの](../assets/fix.svg)並べ替え可能な列の修正
検索条件に空のソート順序値が含まれている場合、![修正](../assets/fix.svg) [!DNL Live Search]でエラーがスローされなくなりました
![属性コードに「から」または「から」の文字列が含まれている場合、範囲フィルタリングが壊れなくなりました](../assets/fix.svg)

### [!DNL Live Search] 1.1.0

[!BADGE &#x200B; サポートされている]{type="Informative" tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![&#x200B; バグ &#x200B;](../assets/bug.svg) [!DNL Live Search] サービスは、Adobe Commerce インストールの[基本通貨](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration)のみをサポートしています。
![&#x200B; バグ &#x200B;](../assets/bug.svg) ファセットを追加する際、`Update on Save`に設定すると、製品属性フィードが正しく更新されません。 この問題を回避するには、[&#x200B; インデックス管理](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)に移動し、製品属性フィードを`Update by Schedule`に設定します。
![&#x200B; バグ &#x200B;](../assets/bug.svg) [!DNL Live Search]の類義語はストアビューごとに定義されますが、現在はweb サイトごとに保存され、`environmentId`と`storeViewCode`の組み合わせで識別されます。 その結果、Adobe Commerceのインストール内のすべてのweb サイトとストアビューで同義語が共有されます。 ストアビュー用に最近作成された同義語のセットが優先されます。
![&#x200B; バグ &#x200B;](../assets/bug.svg)同義語の用語に複数の単語が含まれる場合、各単語は個別の同義語として扱われます。 例えば、「タイムピース」を「ウォッチ」の同義語として定義すると、「タイム」と「ピース」の両方がウォッチの同義語として扱われます。

+++

## 関連文書

詳細については、こちらをご覧ください：

- [Adobe Commerce開発者向けドキュメント &#x200B;](https://developer.adobe.com/commerce/docs)
- [Adobe Commerce ユーザーガイド &#x200B;](https://experienceleague.adobe.com/en/docs/commerce)
- [[!DNL Live Search]  マーケットプレイス &#x200B;](https://commercemarketplace.adobe.com/magento-live-search.html)
