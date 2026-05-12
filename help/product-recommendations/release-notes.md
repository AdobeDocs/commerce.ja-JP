---
title: '[!DNL Product Recommendations] リリースノート'
description: Adobe Commerceからの [!DNL Product Recommendations] の最新のリリース情報。
feature: Services, Recommendations, Release Notes
exl-id: 37404605-5b62-4c71-90d1-4f09e6105c4b
TQID: https://experienceleague.adobe.com/cr5tBPTFRNlSTqtFNfUWS6p1LdhSrir28x3N1WC4Zw8
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 2233
ht-degree: 0%

---

# [!DNL Product Recommendations] リリースノート

リリースノートには、次の[!DNL Product Recommendations] モジュールの更新が記載されています。

* [!DNL Product Recommendations] メタパッケージ：`magento/product-recommendations`
* [!DNL Product Recommendations] （オプション）モジュールでのページビルダーのサポート：`magento/module-page-builder-product-recommendations`
* [!DNL Product Recommendations] （オプション）モジュールの視覚的類似性のレコメンデーションタイプのサポート：`magento/module-visual-product-recommendations`

Adobeは、最新リリースの商品レコメンデーションバージョンをサポートしています。 古いバージョンのリリースノートは、参照用に提供されています。

アップデートには以下が含まれます。

![新機能](../assets/new.svg)
![修正](../assets/fix.svg)修正と機能強化
![&#x200B; バグ &#x200B;](../assets/bug.svg)既知の問題

製品サポートについて詳しくは、[開発者向けドキュメント &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability)を参照してください。

## ホスト型サービスの更新

これらのメモでは、バージョン管理されたリリース以外で公開または検出された更新または既知の問題、またはホストされたサービスの改善について説明します。

_2026年4月28日_

![修正](../assets/fix.svg) （**[!DNL Adobe Commerce as a Cloud Service]**&#x200B;のみ） [製品プレビューパネル &#x200B;](create.md#preview-recommendations)を更新しました。プレビューにSKUが必要なレコメンデーションタイプ（クロスセル、アップセル、類似性ベースのレコメンデーションなど）に対してのみ表示されるようになりました。 その他のタイプの場合、プレビューは非表示になります。 **最近表示した**&#x200B;や&#x200B;**あなたにおすすめ**&#x200B;などのパーソナライズされたタイプは、プレビューがサポートされていない場合にメッセージを表示します。

_2026年2月19日_

![修正](../assets/fix.svg) レコメンデーション単位の製品制限に達した場合、_最近閲覧した_ レコメンデーションタイプに表示された製品が予期しない順序で削除される問題を修正しました。 製品は、製品が閲覧された順に先入れ先出し（FIFO）で削除されるようになりました。

_2025年11月19日_

![新規](../assets/new.svg) ページの種類ごとに、アクティブなレコメンデーションユニットを最大50個作成できるようになりました。 以前は、制限は5でした。

_2025年10月1日_

![新規](../assets/new.svg)顧客がログインしたデータの`ds-logged-in`という名前の新しいデータストレージキーを追加しました。

_2025年1月31日_

![新規](../assets/new.svg) テスト環境に、クエリされていないカタログデータに対する新しいデータ保持ポリシーがあります。 [学習を増やす](overview.md#catalog-data-retention-policy)。

_2024年6月28日_

![&#x200B; バグ &#x200B;](../assets/bug.svg)買い物かごページの[!DNL Product Recommendations] ユニットから買い物かごに追加された商品は、買い物かごページが再読み込みされたときに、おすすめ商品のリストから削除されません。
![&#x200B; バグ &#x200B;](../assets/bug.svg)買い物かごから削除された製品は、買い物かごページが再読み込みされるまで、`cartSkus`配列に残り続けます。

_2023年7月18日_

![新規](../assets/new.svg) [!DNL Product Recommendations]には、GraphQL [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) クエリが含まれています。

_2023年4月25日_

![新規](../assets/new.svg) [!DNL Product Recommendations]のお客様は、[SaaS価格インデックス &#x200B;](../price-index/price-indexing.md)を利用できるようになりました。

## 現在のメジャーバージョン

### 6.7.0 magento/product-recommendations

_2026年3月17日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) PHP 8.5のサポートを追加しました。

### 以前のバージョン

### 6.6.0 magento/product-recommendations

_2026年1月28日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) [&#x200B; データフィード同期ステータス監視ダッシュボード &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)に依存関係を追加しました。 このダッシュボードでは、Commerceから商品レコメンデーションなどの外部サービスに商品およびカテゴリーデータを転送するデータエクスポートフィードの健全性とパフォーマンスに関するリアルタイムのインサイトを表示できます。

### 6.5.0 magento/product-recommendations

_2025年11月3日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg)製品レコメンデーションユニットが異なる環境で操作する方法を改善しました。

### 6.4.0 magento/product-recommendations

_2025年9月17日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg) ローカルストレージデータが利用できない場合にJavaScript エラーが発生すると、商品レコメンデーションユニットが消える断続的な問題を解決しました。 この修正により、`ds-view-history-time-decay`がローカルストレージに見つからない場合に、PREXがエラーをスローしなくなります。
![新規](../assets/new.svg) `recommendations-sdk`のCDN URLを`adobe.io` ドメインに更新しました。

### magento/product-recommendationsの6.3.0

_2025年9月5日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) [商品レコメンデーションワークスペース &#x200B;](workspace.md)内のデフォルト以外のストアビューで作成された[PageBuilder レコメンデーションユニット &#x200B;](page-builder.md)の指標を表示するためのサポートを追加しました。
![新規](../assets/new.svg)製品の推奨事項は、制限が有効になっている場合に、Cookie/ローカルストレージでのデータの収集と保存を防ぐことにより、[Cookie制限モード &#x200B;](setting-cookie.md)を完全に尊重するようになりました。

### 6.2.1 of magento/product-recommendations

_2025年7月14日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg) [&#x200B; プレビューのレコメンデーション &#x200B;](./create.md#preview-recommendations) パネルを改善しました。

### magento/product-recommendationsの6.2.0

_2025年4月4日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) `recommendations-admin-ui`のCDN URLを`adobe.io` ドメインに更新しました。

### magento/product-recommendationsの6.1.0

_2025年3月11日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) PHP 8.4のサポートを追加しました。

### 6.0.3 of magento/product-recommendations

_2024年11月6日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg)現在のストアビューに属していないカテゴリが[&#x200B; カテゴリフィルター](filters.md#category)に含まれている問題を修正しました。
![修正](../assets/fix.svg) `magento/product-recommendations` メタパッケージの依存関係の問題を修正しました。

### 6.0.2 of magento/product-recommendations

_2024年5月9日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg)商品レコメンデーションユニット内のシンプルな商品の&#x200B;**[!DNL Add to Cart]** ボタンをクリックすると、現在のページに留まるのではなく、買い物客がホームページにリダイレクトされる問題を修正しました。
![&#x200B; バグ &#x200B;](../assets/bug.svg) `ProductRecommendations Layout` XML ファイルの`referenceBlock`要素によって検証エラーが発生しました。

### magento/product-recommendationsの6.0.1

_2024年3月19日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) PHP 8.3のサポートを追加しました。

### magento/product-recommendationsの6.0.0

_2024年2月22日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) [!DNL Catalog Sync Dashboard]は[[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)になりました。 この刷新されたダッシュボードは、[!DNL Product Recommendations]、[!DNL Live Search]および[!DNL Catalog Service]のデータストリームに関するインサイトを提供します。
![修正](../assets/fix.svg) [!DNL Product Recommendations]のチェックアウトエラーの原因となる問題を修正しました。

+++5.0.0以前

### 5.0.1 of magento/product-recommendations

_2023年9月15日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) [Saas価格インデクサー](../price-index/price-indexing.md)をサポートする新しいモジュールを追加しました。
![新規](../assets/new.svg)新しいデータ書き出しモジュールを追加し、バンドル商品やギフトカードなど、より多くの商品タイプの書き出しをサポートするようになりました。
![修正](../assets/fix.svg)製品と価格フィードのテーブルサイズが大幅に削減されました。 テーブル `catalog_data_exporter_products`と`catalog_data_exporter_product_prices`のサイズを大幅に縮小する必要があります。

#### 既知の制限事項

* アンダースコア （_）が含まれている場合、`websiteCode`値が誤って返されます。

### magento/product-recommendationsの5.0.0

_2023年3月20日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) Adobe Commerce 2.4.6をサポートするために[!DNL Product Recommendations]を更新しました。
![新規](../assets/new.svg)これはメジャーバージョンのリリースです。 プロジェクトのルート `composer.json` ファイルを[編集](install-configure.md#update)します。
![新規](../assets/new.svg) [!DNL Product Recommendations]は、Commerceで[Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction)の機能をすべてサポートするようになりました（以前はマルチSource インベントリ（MSI）と呼ばれていました）。 完全なサポートを有効にするには、依存関係モジュール `commerce-data-export`をバージョン 102.2.0以降に[更新](install-configure.md#update)する必要があります。

### 4.0.1 of magento/product-recommendations

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg)以前は、[!DNL Product Recommendations]は、表示通貨がデフォルト以外の通貨に切り替えられたときにエラーを表示していました。 通貨の切り替えが正常に機能するようになりました。

### magento/product-recommendationsの4.0.0

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)各レコメンデーションタイプのトレーニングの進捗状況を視覚化するために、[準備状況インジケーター](create.md)を追加しました。
![新規](../assets/new.svg)これはメジャーバージョンのリリースです。 プロジェクトのルート `composer.json` ファイルを[編集](install-configure.md#update)します。 このリリースでは、[!DNL Product Recommendations]をインストールおよび設定する際に、実稼動キー[とサンドボックスキー](../landing/saas.md)の2つのAPI キーを指定する必要もあります。

#### 既知の制限事項

* アンダースコア （_）が含まれている場合、`websiteCode`値が誤って返されます。

### 3.3.7 of magento/product-recommendations

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg) PHP 8.1のサポートを追加
![新規](../assets/new.svg)画像のサイズ変更を改善し、画像のサイズ変更が参照表示テンプレートでより一貫して処理されるようになりました

### 3.3.6 of magento/product-recommendations

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg)依存関係を明示的に一覧表示して、[!DNL Product Recommendations] メタパッケージを最適化しました

### 3.3.5 of magento/product-recommendations

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg)さんが[B2B サポート &#x200B;](onboarding.md#b2bsupport)を追加しました [!DNL Product Recommendations]
![新規](../assets/new.svg) コマンドラインを使用して、[&#x200B; カタログ データを](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync)Commerce サービスに同期する新しいフィードを追加

### 3.3.3 of magento/product-recommendations

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg)新しい[&#x200B; レコメンデーションタイプ &#x200B;](type.md)を追加しました：コンバージョン（カートに表示）、コンバージョン（購入に表示）、最近表示。 これらの新しいレコメンデーションタイプは、`magento/product-recommendations` モジュール 3.2.2以降で使用できます。
![修正](../assets/fix.svg) FastlyのWeb Application Firewall （WAF）が誤ってCookieをブロックしていた問題を修正しました
![修正](../assets/fix.svg)特定のストアビューのレコメンデーションを作成する際に、デフォルト以外のストアビューに割り当てられた製品が&#x200B;_レコメンデーション製品プレビュー_ パネルに表示されない問題を修正しました
![修正](../assets/fix.svg) ページビルダーの特定のレコメンデーションユニット名によって、ストアフロントにレコメンデーションユニットを表示できない問題を修正しました

### 3.3.2 of magento/product-recommendations

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![修正](../assets/fix.svg) B2B サポートの依存関係が見つからない問題を修正しました

### 3.3.1 of magento/product-recommendations

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg) B2B カスタマーグループの価格のサポートを追加しました。 レコメンデーションユニットに[価格フィルター](filters.md)を設定すると、ログインしているB2Bのお客様には、表示される製品の顧客グループの価格セットが表示されます。

### 3.3.0 of magento/product-recommendations

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg) Adobe Commerceの機能とサービス全体で行動データの収集を標準化するために、Adobe Client Data Layerのサポートが追加されました。 詳しくは、[readme](https://github.com/adobe/commerce-events/blob/main/packages/storefront-events-collector/README.md)を参照してください。

### 3.2.6 of magento/product-recommendations

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![修正](../assets/fix.svg) JavaScript モーダルエラーを修正しました
![修正](../assets/fix.svg) FastlyのWeb Application Firewall （WAF）が誤ってCookieをブロックしていた問題を修正しました

### 3.2.5 of magento/product-recommendations

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg)がMagento サービスを[Commerce サービス &#x200B;](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas)に名前変更し、管理者の操作性が向上しました

### 3.2.4 of magento/product-recommendations

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![修正](../assets/fix.svg)製品属性のインデックス作成時の「設定可能な製品オプションデータを取得できません」エラーを修正しました

### 3.2.3 of magento/product-recommendations

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![修正](../assets/fix.svg) カタログ同期中に「設定可能な製品オプションデータを取得できません」エラーが発生する問題を修正しました
![修正](../assets/fix.svg) 「URLにストアコードを追加」設定を有効にしたときに、ストアコードが正しく設定されない問題を修正しました
![修正](../assets/fix.svg)管理者パネル設定の変更の検出を改善して、これらの変更がカタログ同期データに反映されるようにしました

### 3.2.2 of magento/product-recommendations

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg)作成時に[推奨結果をプレビュー](create.md)する機能を追加しました。 これには、モジュールを最新バージョンに更新する必要がある場合があります。
![新規](../assets/new.svg)管理者からカタログ同期プロセスを[監視および管理](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync)する機能を追加しました。
![新規](../assets/new.svg) [&#x200B; フィルター](filters.md)を追加して、どの製品をレコメンデーションに表示するかを制御しました。
![新規](../assets/new.svg)さんが[視覚的な類似性](type.md#visualsim)のレコメンデーションタイプを追加しました。

### ページビルダーのmagento/module-page-builder-product-recommendationsの1.2.1

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg) `magento/product-recommendations` モジュールの3.2.0以降のバージョンのサポートを追加しました

### 3.1.0 of magento/product-recommendations

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg) カタログを[再同期](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync)する機能をコマンドライン経由でSaaS サービスに追加しました。
![新規](../assets/new.svg) データベース テーブルのプレフィックスのサポートを追加しました
![修正](../assets/fix.svg) PHP 7.1 サポートを削除しました

### 3.0.8 of magento/product-recommendations

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![修正](../assets/fix.svg) モジュールが構成される前にデータ収集のためにイベントが送信され、無効なトラフィックが発生する問題を修正しました

### 3.0.6 of magento/product-recommendations

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg) **（Beta）**&#x200B;新しい[視覚的な類似性](type.md#visualsim)のレコメンデーションタイプのサポートが含まれています。

### magento/module-visual-product-recommendationsの1.0.0

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg) **（Beta）** [視覚的類似性](type.md#visualsim)。 _視覚的な類似性_&#x200B;のレコメンデーションタイプを使用すると、表示中の製品と視覚的に類似する製品を表示するレコメンデーションユニットを製品詳細ページにデプロイできます。

### 3.0.5 of magento/product-recommendations

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![修正](../assets/fix.svg) カタログの書き出し中に発生する可能性のある「製品オプションデータを取得できません」エラーを修正しました。
![修正](../assets/fix.svg) _[!DNL Product Recommendations]_&#x200B;ダッシュボードの_&#x200B;収益&#x200B;_列の通貨記号に、設定された基本通貨が正しく反映されるようになりました。

### 3.0.4 of magento/product-recommendations

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![修正](../assets/fix.svg) Adobe Commerce 2.4.0のサポートを追加しました

### 3.0.3 of magento/product-recommendations

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![修正](../assets/fix.svg) ストアフロントテンプレートでのシンボル実装の改善

### ページビルダーのmagento/module-page-builder-product-recommendationsの1.0.4

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg) ページビルダーのコンテンツタイプを編集する際に、商品レコメンデーション名を追加しました

### 3.0.2 magento/product-recommendations

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg) ページビルダーでレコメンデーションユニットを選択する際に、グリッドにステータス列を追加しました
![修正](../assets/fix.svg)製品URLと画像URLの誤ったhttp/https プロトコルの問題を修正しました

### 3.0.1 of magento/product-recommendations

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

これはメジャーバージョンのリリースです。 プロジェクトのルート composer.json ファイルを[編集](install-configure.md#update)します。

![新規](../assets/new.svg)代替SaaS データスペースから[!DNL Product Recommendations]を取得します。 これにより、製品環境で計算された[!DNL Product Recommendations]を、実稼動以外の他の環境で使用できます。 [SaaS データスペースの切り替え](settings.md)では、この機能について詳しく説明しています。

![修正](../assets/fix.svg) uBlock Originを使用している買い物客に対してチェックアウトが禁止される問題を修正しました
![修正](../assets/fix.svg)不要な追加イベントを送信する問題を修正しました

### ページビルダーのmagento/module-page-builder-product-recommendationsの1.0.3

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg) ページビルダーのサポート。 ページビルダーとの統合により、ページビルダーで作成されたコンテンツ上の任意の場所に、レコメンデーション単位を正確かつ詳細に配置することができます。 見出しやレコメンデーションユニット自体にスタイルを適用することもできます。 詳しくは、[&#x200B; ページビルダー](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/add-content/recommendations)にアクセスしてください。

### magento/product-recommendationsの2.0.0

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg)一般公開リリース！

+++

## 関連文書

[!DNL Product Recommendations]および[!DNL Product Recommendations]開発について詳しくは、次を参照してください。

* [ユーザーガイド](overview.md)
* [開発者用マニュアル](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/developer/development-overview)
