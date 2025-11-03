---
title: '[!DNL Product Recommendations] リリースノート'
description: Adobe Commerceからのの最新  [!DNL Product Recommendations]  リリース情報です。
feature: Services, Recommendations, Release Notes
exl-id: 37404605-5b62-4c71-90d1-4f09e6105c4b
source-git-commit: 65aedb6cb8888ddc4cb6278c83b38b733864e324
workflow-type: tm+mt
source-wordcount: '1857'
ht-degree: 0%

---

# [!DNL Product Recommendations] リリースノート

リリースノートには、次の [!DNL Product Recommendations] モジュールのアップデートが含まれています。

* [!DNL Product Recommendations] メタパッケージ：`magento/product-recommendations`
* [!DNL Product Recommendations] （オプション）モジュールでのページビルダーのサポート：`magento/module-page-builder-product-recommendations`
* [!DNL Product Recommendations] （オプション）モジュールの視覚的類似性推奨タイプのサポート：`magento/module-visual-product-recommendations`

最新のリリースバージョンに対するサポートが提供されます。 古いバージョンのリリースノートが参照用に提供されています。
リリースノートには次のものが含まれます。

![ 新機能 ](../assets/new.svg) 新機能
![ 修正 ](../assets/fix.svg) 修正点および改善点
![ バグ ](../assets/bug.svg) 既知の問題

詳しくは、開発者向けドキュメントの [ 製品サポートについて ](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability) を参照してください。

## ホステッド サービスの更新

これらのメモでは、バージョン管理されたリリースの外部で公開または検出された、更新プログラムや既知の問題、またはホストされるサービスの改善について説明します。

_2025 年 10 月 1 日_

![ 新規 ](../assets/new.svg) 顧客がログインデータ用に `ds-logged-in` という名前の新しいデータストレージキーを追加しました。

_2025 年 1 月 31 日_

![ 新規 ](../assets/new.svg) テスト環境には、クエリされていないカタログデータ用の新しいデータ保持ポリシーがあります。 [学習を増やす](overview.md#catalog-data-retention-policy)。

_2024 年 6 月 28 日_

![ バグ ](../assets/bug.svg) 買い物かごページで [!DNL Product Recommendations] ユニットから買い物かごに追加された製品が、買い物かごページの再読み込み時に、推奨製品のリストから削除されません。
![ バグ ](../assets/bug.svg) 買い物かごから削除された製品は、買い物かごのページがリロードされるまで、引き続き `cartSkus` 配列に保持されます。

_2023 年 7 月 18 日_

![ 新規 ](../assets/new.svg) [!DNL Product Recommendations] GraphQL [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) クエリが追加されました。

_2023 年 4 月 25 日_

![ 新規 ](../assets/new.svg) [!DNL Product Recommendations] お客様は、[SaaS 価格インデックス作成 ](../price-index/price-indexing.md) を活用できるようになりました。

## 現在のメジャーバージョン

### 6.5.0 magento/product-recommendations

_2025 年 11 月 3 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 修正 ](../assets/fix.svg) 様々な環境での製品のレコメンデーションユニットのやり取りを改善しました。

### 以前のバージョン

### 6.4.0 magento/product-recommendations

_2025 年 9 月 17 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 修正 ](../assets/fix.svg) ローカルストレージデータが使用できない場合に、JavaScript エラーが原因で製品のレコメンデーションユニットが表示されなくなる断続的な問題を修正しました。 この修正により、ローカルストレージに `ds-view-history-time-decay` がない場合に PREX がエラーをスローしなくなります。
![ 新規 ](../assets/new.svg) `recommendations-sdk` の CDN URL を `adobe.io` ドメインに更新しました。

### magento/product-recommendations の 6.3.0

_2025 年 9 月 5 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 新規 ](../assets/new.svg)[Product Recommendations ワークスペース ](page-builder.md) 内のデフォルト以外のストア表示で作成された [PageBuilder レコメンデーションユニット ](workspace.md) の指標を表示するサポートが追加されました。
![ 新規 ](../assets/new.svg) Product Recommendations は、制限が有効な場合に cookie/ローカルストレージでのデータ収集と保存を防ぐことで、[cookie 制限モード ](setting-cookie.md) を完全に尊重するようになりました。

### magento/product-recommendations の 6.2.1

_2025 年 7 月 14 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 修正 ](../assets/fix.svg) [ レコメンデーションをプレビュー ](./create.md#preview-recommendations) パネルを改善しました。

### magento/product-recommendations の 6.2.0

_2025 年 4 月 4 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 新規 ](../assets/new.svg) `recommendations-admin-ui` の CDN URL を `adobe.io` ドメインに更新しました。

### magento/product-recommendations の 6.1.0

_2025 年 3 月 11 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 新規 ](../assets/new.svg) PHP 8.4 のサポートを追加しました。

### magento/product-recommendations の 6.0.3

_2024 年 11 月 6 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 修正 ](../assets/fix.svg) 現在の storreview に属さないカテゴリが [ カテゴリフィルター ](filters.md#category) に含まれていた問題を修正しました。
![ 修正 ](../assets/fix.svg) `magento/product-recommendations` メタパッケージの依存関係の問題を修正しました。

### magento/product-recommendations の 6.0.2

_2024 年 5 月 9 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 修正 ](../assets/fix.svg)Product Recommendations ユニット内のシンプルな製品で「**[!DNL Add to Cart]**」ボタンをクリックすると、買い物客が現在のページに留まらず、ホームページにリダイレクトされる問題を修正しました。
![ バグ ](../assets/bug.svg) `referenceBlock` XML ファイルの `ProductRecommendations Layout` 要素が原因で検証エラーが発生しています。

### magento/product-recommendations の 6.0.1

_2024 年 3 月 19 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 新規 ](../assets/new.svg) PHP 8.3 のサポートを追加しました。

### magento/product-recommendations の 6.0.0

_2024 年 2 月 22 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 新規 ](../assets/new.svg)[!DNL Catalog Sync Dashboard] が [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard) になりました。 この刷新されたダッシュボードでは、[!DNL Product Recommendations]、[!DNL Live Search] および [!DNL Catalog Service] のデータストリームに関するインサイトが提供されます。
![ 修正 ](../assets/fix.svg) [!DNL Product Recommendations] のチェックアウトエラーが発生する問題を修正しました。

+++5.0.0 以前

### magento/product-recommendations の 5.0.1

_2023 年 9 月 15 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 新規 ](../assets/new.svg)[Saas 価格インデクサー ](../price-index/price-indexing.md) をサポートする新しいモジュールを追加しました。
![ 新規 ](../assets/new.svg) バンドル製品やギフトカードなど、より多くの種類の製品の書き出しをサポートする新しいデータエクスポートモジュールを追加しました。
![ 修正 ](../assets/fix.svg) 製品および価格フィードのテーブルサイズが大幅に縮小されました。 テーブル `catalog_data_exporter_products` および `catalog_data_exporter_product_prices` では、大幅なサイズ削減が必要です。

#### 既知の制限事項

* アンダースコア（_）が含まれている場合、`websiteCode` の値が誤って返されます。

### magento/product-recommendations の 5.0.0

_2023 年 3 月 20 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 新規 ](../assets/new.svg)Adobe Commerce 2.4.6 をサポートするように [!DNL Product Recommendations] を更新しました。
![ 新規 ](../assets/new.svg) これはメジャーバージョンリリースです。 [ 編集 ](install-configure.md#update) プロジェクトのルート `composer.json` ファイル。
![ 新機能 ](../assets/new.svg)[!DNL Product Recommendations]Commerceで完全な [Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction) 機能をサポートするようになりました（以前はマルチSourceインベントリ（MSI）と呼ばれていました）。 完全なサポートを有効にするには、依存関係モジュールをバージョン 102.2.0 以降に [ 更新 ](install-configure.md#update) する必要 `commerce-data-export` あります。

### magento/product-recommendations の 4.0.1

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 修正 ](../assets/fix.svg) 以前は、表示通貨 [!DNL Product Recommendations] デフォルト以外の通貨に切り替えるとエラーが表示されていました。 通貨の切り替えが正しく機能するようになりました。

### magento/product-recommendations の 4.0.0

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 新規 ](../assets/new.svg) 各推奨タイプのトレーニングの進行状況を視覚化するのに役立つ [ 準備状況インジケーター ](create.md) を追加しました。
![ 新規 ](../assets/new.svg) これはメジャーバージョンリリースです。 [ 編集 ](install-configure.md#update) プロジェクトのルート `composer.json` ファイル。 このリリースでは、[!DNL Product Recommendations] をインストールおよび設定する際に、[ 実稼動キーとサンドボックスキー ](../landing/saas.md) の 2 つの API キーを指定する必要もあります。

#### 既知の制限事項

* アンダースコア（_）が含まれている場合、`websiteCode` の値が誤って返されます。

### magento/product-recommendations の 3.3.7

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 新規 ](../assets/new.svg)PHP 8.1 のサポートを追加しました
![ 新規 ](../assets/new.svg) 画像のサイズ変更が改善され、参照表示テンプレートでの画像のサイズ変更がより一貫して処理されるようになりました

### magento/product-recommendations の 3.3.6

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 新規 ](../assets/new.svg) 依存関係を明示的にリスト化することで、[!DNL Product Recommendations] メタパッケージを最適化しました。

### magento/product-recommendations の 3.3.5

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 新規 ](../assets/new.svg)[B2B サポート ](onboarding.md#b2bsupport) を [!DNL Product Recommendations] に追加
![ 新規 ](../assets/new.svg) コマンドラインを使用してCommerce サービスに [sync catalog data](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) 新しいフィードを追加しました

### magento/product-recommendations の 3.3.3

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 新規 ](../assets/new.svg) 新しく追加された [ レコメンデーションタイプ ](type.md)：コンバージョン（買い物かごに表示）、コンバージョン（購入に表示）、最近表示された項目。 これらの新しいレコメンデーションタイプは、`magento/product-recommendations` モジュール 3.2.2 以降で使用できます。
![ 修正 ](../assets/fix.svg)Fastly の Web Application Firewall （WAF）が誤って Cookie をブロックしていた問題を修正しました
![ 修正 ](../assets/fix.svg) デフォルト以外のストア表示に割り当てられた製品が、その特定のストア表示のレコメンデーションを作成する際に、_Recommendations 製品プレビュー_ パネルに表示されない問題を修正しました
![ 修正 ](../assets/fix.svg) ページビルダーの特定のレコメンデーションユニット名でレコメンデーションユニットがストアフロントに表示されない問題を修正しました

### magento/product-recommendations の 3.3.2

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 修正 ](../assets/fix.svg) B2B サポートの依存関係が見つからない問題を修正しました

### magento/product-recommendations の 3.3.1

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 新規 ](../assets/new.svg)B2B 顧客グループの価格をサポートするようになりました。 レコメンデーションユニットで [ 価格フィルター ](filters.md) を設定すると、ログインしている B2B 顧客には、表示された製品の顧客グループ価格設定が表示されます。

### magento/product-recommendations の 3.3.0

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 新規 ](../assets/new.svg) Adobe Client Data Layer のサポートが追加され、Adobe Commerceの機能およびサービス全体で行動データの収集を標準化できるようになりました。 詳細については、[readme](https://github.com/adobe/commerce-events/blob/main/packages/storefront-events-collector/README.md) を参照してください。

### magento/product-recommendations の 3.2.6

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 修正 ](../assets/fix.svg)JavaScript モーダルエラーを修正しました
![ 修正 ](../assets/fix.svg)Fastly の Web Application Firewall （WAF）が誤って Cookie をブロックしていた問題を修正しました

### magento/product-recommendations の 3.2.5

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 新規 ](../assets/new.svg)Magento サービスの名前を [Commerce サービスに変更し ](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas) 管理者の操作性が向上しました

### magento/product-recommendations の 3.2.4

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 修正 ](../assets/fix.svg) 製品属性のインデックス作成時に「設定可能な製品オプションデータを取得できません」エラーが修正されました

### magento/product-recommendations の 3.2.3

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 修正 ](../assets/fix.svg) カタログ同期中の「設定可能な製品オプションデータを取得できません」エラーを修正しました
![ 修正 ](../assets/fix.svg) 「URL にストアコードを追加」設定を有効にすると、ストアコードが正しく設定されない問題を修正しました
![ 修正 ](../assets/fix.svg) 管理パネルの設定変更の検出が改善され、これらの変更がカタログ同期データに反映されるようになりました

### magento/product-recommendations の 3.2.2

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 新規 ](../assets/new.svg) 作成時に [ レコメンデーション結果をプレビュー ](create.md) する機能を追加しました。 モジュールを最新バージョンに更新する必要が生じる場合があります。
![ 新規 ](../assets/new.svg) 管理者からカタログ同期プロセスを [ 監視および管理 ](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) できる機能が追加されました。
![ 新規 ](../assets/new.svg) レコメンデーションに表示する製品を制御する [ フィルター ](filters.md) を追加しました。
![ 新規 ](../assets/new.svg) [ 視覚的類似性 ](type.md#visualsim) レコメンデーションタイプを追加しました。

### ページビルダー用 magento/module-page-builder-product-recommendations の 1.2.1

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 新規 ](../assets/new.svg) `magento/product-recommendations` モジュールの 3.2.0 以降のバージョンのサポートを追加しました

### magento/product-recommendations の 3.1.0

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 新規 ](../assets/new.svg) コマンドラインを使用してカタログを SaaS サービスに [ 再同期 ](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) する機能が追加されました。
![ 新規 ](../assets/new.svg) データベーステーブル接頭辞のサポートが追加されました
![ 修正 ](../assets/fix.svg) PHP 7.1 のサポートを削除しました

### magento/product-recommendations の 3.0.8

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 修正 ](../assets/fix.svg) モジュールを設定する前に、イベントがデータ収集のために送信され、無効なトラフィックが発生していた問題を修正しました

### magento/product-recommendations の 3.0.6

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 新規 ](../assets/new.svg) **（Beta）** 新しい [ 視覚的類似性 ](type.md#visualsim) レコメンデーションタイプのサポートが含まれます。

### magento/module-visual-product-recommendations 1.0.0

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 新規 ](../assets/new.svg) **（Beta）** [ 視覚的類似性 ](type.md#visualsim)。 _視覚的類似性_ レコメンデーションタイプを使用すると、表示している製品に視覚的に類似した製品を表示するレコメンデーションユニットを製品の詳細ページにデプロイできます。

### magento/product-recommendations の 3.0.5

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 修正 ](../assets/fix.svg) カタログの書き出し中に発生する可能性のある「製品オプションデータを取得できません」エラーを修正しました。
![ 修正 ](../assets/fix.svg)_ダッシュボードの_ 売上高 _[!DNL Product Recommendations]_列の通貨記号に、設定されたベース通貨が正しく反映されるようになりました。

### magento/product-recommendations の 3.0.4

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 修正 ](../assets/fix.svg)Adobe Commerce 2.4.0 がサポートされるようになりました

### magento/product-recommendations の 3.0.3

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 修正 ](../assets/fix.svg) ストアフロントテンプレートのシンボル実装を改善しました

### ページビルダー用 magento/module-page-builder-product-recommendations の 1.0.4

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 新規 ](../assets/new.svg) ページビルダーのコンテンツタイプの編集時に追加された製品レコメンデーション名

### 3.0.2 magento/product-recommendations

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 新規 ](../assets/new.svg) ページビルダーでレコメンデーション単位を選択する際のグリッドにステータス列が追加されました
![ 修正 ](../assets/fix.svg) 製品および画像 URL の http/https プロトコルが正しくない問題を修正しました

### magento/product-recommendations の 3.0.1

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

これはメジャーバージョンリリースです。 [ 編集 ](install-configure.md#update) プロジェクトのルートの composer.json ファイル。

![ 新規 ](../assets/new.svg) 代替 SaaS データ スペースから [!DNL Product Recommendations] を取得します。 これにより、製品環境で計算された [!DNL Product Recommendations] を実稼動以外の他の環境で使用できます。 [Switching SaaS Data Spaces](settings.md) では、この機能について詳しく説明します。

![ 修正 ](../assets/fix.svg) uBlock オリジンを使用する買い物客のチェックアウトが禁止される問題を修正しました
![ 修正 ](../assets/fix.svg) 不要な買い物かごへの追加イベントを送信する問題を修正しました

### ページビルダー用 magento/module-page-builder-product-recommendations の 1.0.3

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 新規 ](../assets/new.svg) ページビルダーのサポート。 ページビルダーの統合を使用すると、ページビルダーが作成したコンテンツの任意の場所にレコメンデーションユニットを正確かつ詳細に配置できます。 また、見出しとレコメンデーションユニット自体のスタイルを設定することもできます。 詳しくは [ ページビルダー ](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/add-content/recommendations) を参照してください。

### magento/product-recommendations の 2.0.0

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 新規 ](../assets/new.svg) 一般提供リリース

+++

## マニュアル

[!DNL Product Recommendations] と [!DNL Product Recommendations] の開発について詳しくは、以下を参照してください。

* [ユーザーガイド](overview.md)
* [ 開発者向けドキュメント ](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/developer/development-overview)
