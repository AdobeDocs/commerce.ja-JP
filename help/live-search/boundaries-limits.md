---
title: 境界と制限
description: ビジネスのニーズを確実に満たすための  [!DNL Live Search]  の境界と制限について説明します。
role: Admin, Developer
exl-id: 28b8d98f-0784-4c4d-b382-81c01838e0de
source-git-commit: 5d99078bfbe5f38ce36874d318e49274dd447fa4
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 0%

---

# 境界と制限

サイト検索に関しては、Adobe Commerceのオプションが用意されています。 次の境界と制限を確認して、[!DNL Live Search] と [!DNL Catalog Service] がビジネスのニーズを満たしていることを確認します。 コンテンツ検索、独自アルゴリズムの作成（BYOA）、属性ベースのマーチャンダイジングなどの高度な検索機能が必要な場合は、サードパーティの検索ソリューションを検討してください。

## 一般

- [ がインストールされている場合は ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) 詳細検索 [!DNL Live Search] モジュールが無効になり、ストアフロントフッターの詳細検索リンクが削除されます。
- [ 階層の価格 ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier) は、[!DNL Live Search] フィールドおよび製品一覧ページウィジェットではサポートされていません。
- 製品価格には付加価値税（VAT）が含まれていま [!DNL Live Search] が、VAT を別の値として表示することはできません。
- コンテンツ検索（CMSのページとブロック）はサポートされていません。
- ページ分割できる結果の最大数は 10,000 個です。 カテゴリや検索結果に多数の製品が含まれる場合に、買い物客がディープページネーションを使用する必要がないようにするには、製品をフィルタリングする意味のある方法を提供します。
- 属性には、説明やカスタム属性を含め、1MB のハード制限があります。
- 検索アダプターは、カスタム ソース モデルで作成され、ファセットとして使用される製品属性をサポートしていません。 この機能をサポートするには、[ 製品一覧ページウィジェット ](plp-styling.md) を使用する必要があります。
- 検索アダプターは Live Search 4.0.0 で廃止されました。
- カスタム製品タイプはサポートされていません。
- `"is_user_defined": false` を使用してプログラムで作成されたカスタム属性はサポートされていません。
- [ 開発者ドキュメント ](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#limitations) に記載されているように、「次で始まる」または「次を含む」条件を使用し、いくつかの制限を設けることで、結果をフィルタリングできます。
- 昨年内のパフォーマンス指標のみを追跡できます。
- 検索クエリに複数の単語が含まれている場合、単語間の空白は別の検索用語として扱われます。 複数語の検索クエリを考慮する場合は、[synonyms](./synonyms.md) を使用します。
- [!DNL Live Search] は、[ 検索語句のリダイレクト ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-terms) をネイティブにサポートしていません。 Fastly またはその他のカスタム設定を使用して、リダイレクトを実装します。

## インデックス作成

- 1 つのストア表示につき最大 450 個の製品属性を [!DNL Live Search] [ インデックス ](indexing.md) します。 これらは次のように配布されます。
   - 並べ替え可能な 50 個の属性
   - 200 フィルタリング可能な属性
   - 検索可能な属性 200
- [!DNL Live Search] は、Adobe Commerce データベースからの商品のみにインデックスを作成します。
- CMSページにはインデックスが作成されません。
- SKU、名前、カテゴリの属性は、デフォルトで検索でき、検索から除外することはできません。 これらのカテゴリに製品を入れない場合は、カテゴリから製品の割り当てを解除してください。

## ファセット

- 定義済みのフィルター可能な属性のセットから、最大 100 個の属性をファセットとして設定できます。
- ファセット内では、最大 100 個のバケットを返すことができます。 100 個を超えるバケットを返す必要がある場合は、[ サポートチケットを作成 ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) します。これにより、Adobeでパフォーマンスへの影響を分析し、お使いの環境でこの制限を増やすことが可能かどうかを判断できます。
- 動的ファセットは、大きなインデックスや通常のインデックスのパフォーマンスで問題を引き起こす可能性があります。 動的ファセットを作成し、パフォーマンスの低下や、タイムアウトエラーを伴うページの読み込みがない場合は、ファセットをピン留めに変更して、パフォーマンスの問題が解決するかどうかを判断してください。
- 在庫状態（`quantity_and_stock_status`）はファセットとしてサポートされていません。 `inStock: 'true'` を使用して、在庫製品を除外できます。 `LiveSearchAdapter` 管理者で「在庫切れの製品を表示」が「True」に設定されている場合、これは [!DNL Commerce] モジュールの初期設定でサポートされています。
- 日付タイプ属性はファセットとしてサポートされていません。
- 属性をファセットとして追加した後に属性メタデータに加えた変更は、ファセットには反映されません。
- 最大 50 個の並べ替え可能な属性と 200 個の検索可能な属性を持つことができます。

## クエリ

- [!DNL Live Search] では、クエリで一意の [GraphQL エンドポイント ](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/) を使用して、動的なファセットや入力に応じた検索などの機能をサポートしています。 [GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/) と似ていますが、いくつかの違いがあり、一部のフィールドは完全な互換性がない場合があります。
- 検索クエリで返される結果の最大数は 10,000 個です。
- ページあたりの結果の最大数は 500 です。
- 日付タイプの属性を使用して結果をフィルタリングすることはできません。

## マーチャンダイジングを検索

- ストア表示あたりの検索マーチャンダイジング [ ルール ](rules.md) の最大数は 50 です。
- ルールごとの条件の最大数は 10 です。
- ルールごとのイベントの最大数は 25 です。
- デフォルトの並べ替え順「並べ替え基準：最も関連性の高い」が選択されている場合、ルールと手動でランク付けされた製品が検索結果に適用されます。 買い物客が並べ替え順を「名前で並べ替え」や「価格で並べ替え」などに変更すると、ルールと手動のランキングは無効になります。
- 応答がページ分割される際に予期しない結果が生じるのを防ぐため、ピン留めされた製品の数がリクエストされたページサイズを超えないようにしてください。

## 同義語

- 1 つ [!DNL Live Search] ストア表示で最大 200 個の [ 同義語 ](synonyms.md) を管理できます。

## カテゴリマーチャンダイジング

- ストア表示ごとに、カテゴリごとに 1 つのルールを作成できます。
- ルールごとの条件の最大数は 10 です。
- ルールごとのイベントの最大数は 25 です。
- ルールが適用されるのは、特定のカテゴリがストアフロントで開かれたときに、そのカテゴリのルールが存在する場合です。 カテゴリマーチャンダイジングルールの場合、デフォルトの並べ替え順は「並べ替え：位置」です。 買い物客が並べ替え順を変更すると、非表示、ピン留め、埋め込みのすべての製品が並べ替えられなくなります。

## B2B およびカテゴリの権限

- 製品は、デフォルトの共有カタログに追加されていない場合は表示されません。
- [ カテゴリ権限 ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/category-permissions) を使用して顧客グループを制限するには：
   - 製品はルートカテゴリに割り当てる必要があります。 （**注意：** この制限を解除するには、SaaS Data Export 拡張機能をバージョン 103.4.0 以降に更新します。 [ データ書き出し拡張機能の管理 ](../data-export/manage-extension.md) を参照してください。
   - 「ログインしていない」顧客グループには、「許可」閲覧権限を付与する必要があります。
   - 製品を「ログインしていない」顧客グループに制限するには、各カテゴリに移動して、各 [ 顧客グループ ](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage) に権限を設定します。
- PWA Studioの PLP ウィジェットを使用した B2B の標準サポートは、現時点ではサポートされていません。 ただし、この機能を実装するには [API を使用 ](install.md#pwa-support) できます。
- [!DNL Live Search] のカテゴリファセットには、特定の [ 顧客グループ ](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage) に表示できないカテゴリが表示される場合があります。
- 最大 1,000 の顧客グループをサポートで [!DNL Live Search] ます。

## [!DNL Storefront popover]

- [[!DNL popover]](storefront-popover.md) は、*Luma* テーマを使用するストア、または *Luma* に基づいてカスタマイズされたテーマでのみ使用できます。 検索結果ページのパンくずリストには *Luma* スタイルが設定されません。
- [!DNL popover] は *Blank* テーマをサポートしていません。
- [!DNL popover] は、クイックオーダーフォームではサポートされていません。
- ウィッシュリストと製品の比較はサポートされていません。
- ペルーのソル （PEN）の通貨記号はサポートされていません。

## トラブルシューティング

[!DNL Live Search] でよくある問題のトラブルシューティングについては、次のナレッジベースの記事を参照してください。

- [[!DNL Live Search]  カタログが同期されていません ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync)
- [[!DNL Live Search]  ダッシュボードと検索結果のランキングが正しくありません ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-dashboard-ranking-incorrect)
- [[!DNL Live Search]  ファセットはアルファベット順に並べ替えられません ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-facets-not-sorted)

追加のサポートが必要な場合は、[ サポート ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) にお問い合わせください。
