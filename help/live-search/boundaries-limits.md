---
title: 限界と限界
description: ビジネスのニーズを満たすために [!DNL Live Search] の境界と制限について説明します。
role: Admin, Developer
exl-id: 28b8d98f-0784-4c4d-b382-81c01838e0de
source-git-commit: 79d5df6c52598312bf8833bb6baa37d2138e530d
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 0%

---

# 限界と限界

Adobe Commerceのサイト検索機能なら、複数のオプションが用意されています。 次の制限と制限を確認して、[!DNL Live Search]と[!DNL Catalog Service]がビジネスのニーズを満たしていることを確認します。 コンテンツ検索、BYOA （bring-your-own-algorithm）、属性ベースのマーチャンダイジングなどの高度な検索機能が必要な場合は、サードパーティの検索ソリューションを検討してください。

## 一般

- 検索アダプターは、[&#x200B; 4.0.0時点で](release-notes.md#live-search-400)非推奨[!DNL Live Search]となっています。製品リストページ （PLP） ウィジェットは、今後[!DNL Live Search]のすべての実装でサポートされるソリューションです。 検索アダプタは、セキュリティ関連の更新のみを受け取ります。 PLP ウィジェットへの移行について詳しくは、[移行ガイド &#x200B;](migrate-to-plp.md)を参照してください。
- [がインストールされている場合、](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search)詳細検索[!DNL Live Search] モジュールは無効になり、ストアフロントフッターの詳細検索リンクは削除されます。
- [階層の価格設定](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier)は、[!DNL Live Search] フィールドおよび製品リストページ ウィジェットではサポートされていません。
- 製品価格には付加価値税（VAT）が含まれていますが、[!DNL Live Search]はVATを別の値として表示することはできません。
- コンテンツ検索（CMS ページおよびブロック）はサポートされていません。
- ページ分割できる結果の最大数は10,000です。 カテゴリーや検索結果に多数の商品が含まれる場合に、ディープページネーションを使用する必要がないように、商品を絞り込む有意義な方法を提供します。
- 説明とカスタム属性を含め、属性ごとに1 MBのハードリミットがあります。
- 検索アダプタは、カスタムソースモデルで作成され、ファセットとして使用される製品属性をサポートしていません。 この機能をサポートするには、[製品リストページ ウィジェット &#x200B;](plp-styling.md)を使用する必要があります。
- カスタム製品タイプはサポートされていません。
- プログラムで`"is_user_defined": false`を使用して作成されたカスタム属性はサポートされていません。
- [開発者ドキュメント &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#limitations)で説明されているように、「次から始まる」条件または「次を含む」条件を使用して、結果をフィルタリングできます。
- 過去1年以内のパフォーマンス指標のみを追跡できます。
- 検索クエリに複数の単語が含まれている場合、単語の間の空白を使用すると、それらの単語は別々の検索語として扱われます。 複数単語の検索クエリを考慮する場合は、[類義語](./synonyms.md)を使用します。
- [!DNL Live Search]は、[検索語リダイレクト &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-terms)をネイティブにサポートしていません。 Fastlyまたはその他のカスタム設定を使用して、リダイレクトを実装する。

## インデックス作成

- [!DNL Live Search] [&#x200B; インデックス &#x200B;](indexing.md)は、ストアビューごとに最大450個の製品属性を提供します。 これらは次のように配布されます。
   - 50個の並べ替え可能な属性
   - 200のフィルター可能な属性
   - 200の検索可能な属性
- [!DNL Live Search]は、Adobe Commerce データベースの商品のみをインデックス作成します。
- CMS ページにはインデックスが付いていません。
- SKU、名前、カテゴリ属性はデフォルトで検索可能であり、検索から除外することはできません。 製品がカテゴリに含まれない場合は、必ずカテゴリから製品の割り当てを解除してください。

## ファセット

- 定義されたフィルター可能な属性のセットから、最大100個の属性をファセットとして設定できます。
- ファセット内では、最大100個のバケットを返すことができます。 100個を超えるバケットを返す必要がある場合は、[&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)を作成して、Adobeがパフォーマンスへの影響を分析し、お客様の環境でこの制限を増やすことができるかどうかを判断できるようにします。
- 動的なファセットは、大きなインデックスや高序数のインデックスでパフォーマンスの問題を引き起こす可能性があります。 ダイナミックファセットを作成し、パフォーマンスの低下やタイムアウトエラーを伴うページの読み込みがないことに気づいた場合は、ファセットをピン留めに変更して、パフォーマンスの問題が解決するかどうかを判断してください。
- ストックステータス（`quantity_and_stock_status`）はファセットとしてサポートされていません。 `inStock: 'true'`を使用して、在庫切れの商品をフィルタリングできます。 `LiveSearchAdapter`管理者で「在庫切れ商品を表示」が「True」に設定されている場合、これは[!DNL Commerce] モジュールで標準でサポートされます。
- 日付タイプの属性は、ファセットとしてサポートされていません。
- 属性メタデータに対して、その属性がファセットとして追加された後に行われた変更は、ファセットには反映されません。
- 最大50個の並べ替え可能な属性と200個の検索可能な属性を含めることができます。

## クエリ

- [!DNL Live Search]は、動的ファセットや入力時の検索などの機能をサポートするために、クエリに一意の[GraphQL エンドポイント &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/)を使用します。 [GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/)と似ていますが、いくつかの違いがあり、一部のフィールドが完全に互換性がない場合があります。
- 検索クエリで返すことができる結果の最大数は10,000です。
- ページあたりの結果の最大数は100です。
- 日付タイプ属性を使用して結果をフィルタリングすることはできません。

>[!NOTE]
>
>位置で並べ替えるには、有効な`categoryPath`または`categoryIds` フィルターがアクティブである必要があります。 [学習を増やす](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#error-handling-for-categorypath-and-categoryids)。

## マーチャンダイジングの検索

- ストアビューあたりの検索マーチャンダイジング [&#x200B; ルール &#x200B;](rules.md)の最大数は50です。
- ルールごとの条件の最大数は10です。
- ルールごとのイベントの最大数は25です。
- ルールと手動でランク付けされた商品は、デフォルトの並べ替え順序「並べ替え順：最も関連性の高い」が選択されている場合に、検索結果に適用されます。 買い物客がソート順序を名前や価格によるソートなどに変更した場合、ルールと手動ランキングは有効ではなくなります。
- ページ分割された応答で予期しない結果が発生するのを防ぐには、ピン留めされた製品数が要求されたページサイズを超えないようにする必要があります。

## 同義語

- [!DNL Live Search]は、ストアビューごとに最大200個の[類義語](synonyms.md)を管理できます。

## カテゴリーマーチャンダイジング

- ストアビューごとにカテゴリごとに1つのルールを作成できます。
- ルールごとの条件の最大数は10です。
- ルールごとのイベントの最大数は25です。
- ルールは、ストアフロントで特定のカテゴリが開かれ、そのカテゴリにルールが存在する場合に適用されます。 カテゴリ マーチャンダイジングルールの場合、デフォルトの並べ替え順序は「並べ替え：位置」です。 買い物客が並べ替え順序を変更すると、非表示、ピン留め、埋め込まれた商品はすべて並べ替えられなくなります。

## B2Bおよびカテゴリ権限

- デフォルトの共有カタログに製品が追加されていない場合、製品は表示されません。
- [&#x200B; カテゴリ権限](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/category-permissions)を使用して顧客グループを制限するには：
   - 製品はルートカテゴリに割り当てる必要があります。 （**注：** SaaS データ書き出し拡張機能をバージョン 103.4.0以降に更新することで、この制限を削除できます。 [&#x200B; データ書き出し拡張機能の管理](../data-export/manage-extension.md)を参照してください。
   - 「ログインしていない」顧客グループには「許可」の閲覧権限を与える必要があります。
   - 製品を「ログインしていない」顧客グループに制限するには、各カテゴリに移動し、各[顧客グループ &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage)に対して権限を設定します。
- 現時点では、PWA Studio上のPLP ウィジェットを使用したB2Bのすぐに使用できるサポートはサポートされていません。 ただし、この機能を実装するには、[API](install.md#pwa-support)を使用できます。
- [!DNL Live Search]のカテゴリ ファセットには、特定の[顧客グループ &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage)に表示できないカテゴリが表示される場合があります。
- [!DNL Live Search]は、最大1,000の顧客グループをサポートできます。

## [!DNL Storefront popover]

- [[!DNL popover]](storefront-popover.md)は、*Luma* テーマを使用するストア、または&#x200B;*Luma*&#x200B;に基づくカスタマイズされたテーマでのみ使用できます。 検索結果ページのパンくずリストには、*Luma*&#x200B;のスタイル設定はありません。
- [!DNL popover]は&#x200B;*空白* テーマをサポートしていません。
- [!DNL popover]は、クイック注文フォームではサポートされていません。
- ウィッシュリストと製品の比較はサポートされていません。
- ペルーのSOL （PEN）の通貨記号はサポートされていません。

## トラブルシューティング

[!DNL Live Search]の一般的な問題のトラブルシューティングについては、次のナレッジベース記事を参照してください。

- [[!DNL Live Search]  カタログが同期されていません](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync) – 商品カタログデータがAdobe Commerce ストアとライブサーチサービス間で正しく同期されない場合の解決策を提供します。 この記事では、同期ステータスの確認、同期エラーの特定、データ同期の問題の解決方法について説明します。
- [[!DNL Live Search]  ダッシュボードと検索結果のランキングが正しくありません](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-dashboard-ranking-incorrect) - ライブ検索ダッシュボードに表示される検索結果またはパフォーマンス指標が期待どおりに表示されない問題を解決します。 この記事では、ランキングの不整合とダッシュボードデータの不整合をトラブルシューティングする方法について説明します。
- [[!DNL Live Search]  ファセットがアルファベット順に並べ替えられない](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-facets-not-sorted) - ファセット値がアルファベット順ではなく予期しない順序で表示される問題を解決します。 この記事では、ストアフロントでファセットの並べ替え動作を設定および修正する手順を説明します。

追加サポートが必要な場合は、[&#x200B; サポート &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)にお問い合わせください。
