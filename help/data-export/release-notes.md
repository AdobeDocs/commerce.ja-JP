---
title: '[!DNL SaaS Data Export Extension] リリースノート'
description: Adobe Commerceの最新  [!DNL Data Export Extension]  リリース情報です。
feature: Services, Release Notes
recommendations: noCatalog
exl-id: 8ae51d3d-8c12-4607-b7e5-985033143a84
source-git-commit: 7e19d42f4e064cfc4efd7c275546725795b60310
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 0%

---

# [!DNL SaaS Data Export] Extension リリースノート

これらのリリースノートでは、[!DNL SaaS data export] 拡張機能の最新バージョンについて説明します。 現在のメジャーリリースバージョンに対するサポートが提供されます。 古いバージョンのリリースノートが参照用に提供されています。

次のような更新があります。

![ 新機能 ](../assets/new.svg) 新機能
![ 修正 ](../assets/fix.svg) 修正点および改善点
![ バグ ](../assets/bug.svg) 既知の問題


>[!NOTE]
>
>SaaS データ書き出し拡張機能は、Live Search、Product Recommendations、Catalog Service と共に自動的にインストールされるモジュールのコレクションです。 Composer を使用すると、システムにインストールされているバージョンを確認できます。 場合によっては、Commerce サービスのバージョンを更新せずに修正点または新機能を取得するように、システムのデータエクスポート拡張機能をアップグレードする必要があります。

## 現在のメジャーバージョン

## 103.3.20 リリース

![ 修正 ](../assets/fix.svg) カタログデータの書き出し cron ジョブの失敗に関連するエラーのメッセージ `cron.log` ージを改善することで、トラッキングできない `BulkException` エラーが修正されました。<!--MDEE-966-->
![ 修正 ](../assets/fix.svg) ストアの表示数が多いインスタンスでの製品の再同期処理のパフォーマンスが向上しました。<!--MDEE-974-->

## 103.3.19 リリース

![ 修正 ](../assets/fix.svg) フィード拡張機能を改善するために、データの書き出し拡張機能を更新しました。 <!--MDEE-936-->
![ 修正 ](../assets/fix.svg) フィードテーブルで誤ってデータが失われるのを防ぐために、データエクスポートプロセッサーは、完全に再同期する前にインデクサーのステータスを検証するようになりました。

## 103.3.18 リリース

![ 修正 ](../assets/fix.svg) 製品およびカテゴリエンティティのステージングの更新が、データの書き出しのデータの更新時に正しくトリガーされるようになりました。<!--MDEE-963-->

## 103.3.17 リリース

![ 修正 ](../assets/fix.svg)PHP 8.4 の互換性を追加しました。<!--MDEE-941-->

## 103.3.16 リリース

![ 修正 ](../assets/fix.svg) 複数のストアビューの設定可能な製品では、オプションの値を空にすることができます。<!--MDEE-926-->

## 103.3.15 リリース

![ 修正 ](../assets/fix.svg) 古い設定での統合テストが安定して動作するようにしました。 <!--MDEE-869-->
![ 修正 ](../assets/fix.svg) 不要な属性オプションの伝播を停止します。 <!--MDEE-882-->
![ 修正 ](../assets/fix.svg) データのシリアル化が失敗した場合に、データのエクスポートログに送信されるエラーメッセージを修正しました。 <!--MDEE-913-->
![ 修正 ](../assets/fix.svg) テストカバレッジを追加し、シンプルな製品アップデートの信頼性を向上しました。<!--MDEE-886-->

## 103.3.14 リリース

![ 修正 ](../assets/fix.svg) エクスポーターインデクサーが、依存インデクサーの正しいステータスを維持するようになりました。 以前は、これらのインデックスは誤って無効化されていたので、追加のチェックと検証が必要で、インデックス作成のパフォーマンスが低下していました。<!--MDEE-866-->

## 103.3.13 リリース

![ 修正 ](../assets/fix.svg) 属性オプションデータのローカルキャッシュを追加することで、データ同期プロセスのパフォーマンスが向上しました。<!--MDEE-864-->

## 103.3.12 リリース

![ 修正 ](../assets/fix.svg) シンプルな製品と仮想製品の同期時間が長くなる問題を解決しました。<!--MDEE-861-->

## 103.3.11 リリース

![ 修正 ](../assets/fix.svg) データ書き出しサービスで、バンドル製品の特別価格データをパーセンテージで送信するようになりました。これにより、最終価格として送信された以前の問題が修正されます。 <!--MDEE-854-->
![ 修正 ](../assets/fix.svg) Monolog 3 との互換性を確保するため、Monolog の実装を更新しました。<!--MDEE-858-->

## 103.3.10 リリース

![ 修正 ](../assets/fix.svg) 製品のカスタムオプションフィードに対する複数のレビューのフィルターが修正されました。 <!--MDEE-842-->
![ 修正 ](../assets/fix.svg) フィードのハッシュ値が変更されるまで、無効なフィードは再送信されません。<!--MDEE-848-->

## 103.3.9 リリース

![ 修正 ](../assets/fix.svg) エンティティを削除すると、web サイト（`scopesWebsite`）および顧客グループ（`scopesCustomerGroup`）のスコーピングサービスフィードに `deleted` フラグが生成されるようになりました。<!--MDEE-839-->

## 103.3.8 リリース

![ 修正 ](../assets/fix.svg) 無効な設定オプションは、アクティブなオプションとして書き出されなくなりました。<!--MDEE-812-->
![ 修正 ](../assets/fix.svg) 子製品に変更が加えられた場合に、設定可能な製品のオプションと値が更新されるようになりました。 <!--MDEE-835-->
![ 新規 ](../assets/new.svg) 製品属性フィードに追加のシステム属性データを含める機能が追加されました。

## 103.3.7 リリース

![ 修正 ](../assets/fix.svg) InventoryDataExporter モジュールから不要な依存関係を削除しました。
![ 修正 ](../assets/fix.svg)CatalogInventoryDataExporter モジュールに含まれる在庫モジュールの必須バージョンを、Adobe Commerce バージョン 2.4.4 をサポートするように変更しました。

## 103.3.6 リリース

![ 修正 ](../assets/fix.svg) マルチスレッドモードでのフィードのインデックス再作成中に発生したデッドロックを修正しました。 クエリは、挿入操作と更新操作に分けられるようになりました。
![ 修正 ](../assets/fix.svg) 多くの web サイトを含む大規模なカタログの価格クエリを最適化しました。
![ 新規 ](../assets/new.svg) デッドロックが発生した場合に失敗したトランザクションを再実行する再試行ロジックが追加されました。

## 103.3.5 リリース

![ 修正 ](../assets/fix.svg)SaaS 共通モジュールの最新の互換性のあるデータ書き出しバージョンの依存関係を設定します。

![ 修正 ](../assets/fix.svg) 別のサービス設定 `ScopeConfig` サポートするために、インスタンスを `ServiceConfigInterface` に置き換えました。

## 103.3.4 リリース

![ 修正 ](../assets/fix.svg) Commerce インスタンスからCommerce サービス <!--MDEE-785--> ーバーにデータが送信されるたびに `data_sent_outside` イベントをディスパッチするメカニズムを追加することで、データ転送監査ログがサポートされるようになりました

## 103.3.3 リリース

![ 新規 ](../assets/new.svg)SaaS データ エクスポートで、属性メタデータ クエリの Entity-Attribute-Value （EAV）属性がキャッシュされるようになりました。

![ 修正 ](../assets/fix.svg) 製品が削除された場合に、再試行時に `InventoryStockStatus` フィードが保存されない問題を修正しました。

## 103.3.2 リリース

![ 修正 ](../assets/fix.svg) 削除されたエンティティフィードに `modifiedAt` フィールドが表示されない問題を修正しました。

## 103.3.1 リリース

![ 修正 ](../assets/fix.svg) ページビルダーのインストール時に、製品フィードのインデックス再作成中に `Invalid Template File` メッセージが表示される問題を修正しました。

## 103.3.0 リリース

![ 新規 ](../assets/new.svg) 統合構造に即時エクスポートフィードテーブルを移行しました。
`id`, `source_entity_id`, `feed_id`, `modified_at`, `is_deleted`, `status`, `feed_data`, `feed_hash`, `errors`

![ 新規 ](../assets/new.svg) 移行されたカタログおよび在庫は、即時エクスポートソリューションにフィードされます。

![ 新規 ](../assets/new.svg) 即時エクスポートフィード cron-jobs の名前を `*_feed_resend_failed_items` に変更しました。

![ 新規 ](../assets/new.svg) 即時エクスポートフィード、インデクサービュー ID および変更ログテーブルの名前を変更しました。
- フィードテーブル（およびインデクサー表示 ID）:
   - `catalog_data_exporter_products` -> `cde_products_feed`
   - `catalog_data_exporter_product_attributes` -> `cde_product_attributes_feed`
   - `catalog_data_exporter_categories` -> `cde_categories_feed`
   - `catalog_data_exporter_product_prices` -> `cde_product_prices_feed`
   - `catalog_data_exporter_product_variants` -> `cde_product_variants_feed`
   - `inventory_data_exporter_stock_status` -> `inventory_data_exporter_stock_status_feed`
- 変更ログテーブル名 – フィードテーブルと同じ命名パターンに従いますが、変更ログテーブル名には `_cl` サフィックスが追加されます。  例：`catalog_data_exporter_products_cl`-> `cde-products_feed_cl`
これらのエンティティのいずれかを参照するカスタムコードがある場合、コードが引き続き正しく機能するように、新しい名前で参照を更新します。

![ 修正 ](../assets/fix.svg) フィードデータのフィールド `modified_at`、必要なフィードに対してのみ設定します。

![ 修正 ](../assets/fix.svg) 製品属性のみを取得するように `productAttributes` クエリを変更します。

## 103.2.6 リリース

![ 修正 ](../assets/fix.svg) テーブルにプレフィックスが付いている場合にフィードのインデックスを再作成できない問題を修正しました。

## 103.2.5 リリース

![ 修正 ](../assets/fix.svg) 価格クエリを最適化しました。

## 103.2.4 リリース

![ 修正 ](../assets/fix.svg)Commerce Inventory managementが有効な場合に、商品に対して表示される間違った在庫ステータスを修正しました。

## 103.2.3 リリース

![ 修正 ](../assets/fix.svg) 固定 Web サイトレベルの特別価格。
![ 修正 ](../assets/fix.svg) 処理されるすべてのフィードに mutex が追加されました。


## 103.2.2 リリース

![ 修正 ](../assets/fix.svg) 大規模なカタログのフィードのバッチ化戦略を改善しました。 メモリの使用量を減らすために、バッチ表に入力される ID の数が制限されるようになりました。

![ 修正 ](../assets/fix.svg) MSI モジュールへの CommerceInventoryDataExporter のハード依存関係を解消しました。

![ 修正 ](../assets/fix.svg) より多くの情報を収集し、様々な書き出しステージで整理するように、`commerce-data-exporter` ログが改善されました。

## 103.2.1 リリース

- リリースされている更新バージョン。

## 103.2.0 リリース

- 製品と価格のマルチスレッドデータ同期を追加しました。
