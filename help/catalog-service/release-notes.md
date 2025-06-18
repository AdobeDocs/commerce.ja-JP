---
title: '[!DNL Catalog Service] リリースノート'
description: Adobe Commerceの最新  [!DNL Catalog Service]  リリース情報です。
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
source-git-commit: fe5f864262478d1f9e205f2cd275452594cf4675
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 0%

---

# [!DNL Catalog Service] リリースノート

これらのリリースノートでは、[!DNL Catalog Service] の最新バージョンについて説明しています。
現在のメジャーリリースバージョンに対するサポートが提供されます。 古いバージョンのリリースノートが参照用に提供されています。
次のような更新があります。

![ 新機能 ](../assets/new.svg) 新機能
![ 修正 ](../assets/fix.svg) 修正点および改善点
![ バグ ](../assets/bug.svg) 既知の問題

## 現在のメジャーバージョン

### V1.26 リリース

_2024 年 10 月 22 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 新規 ](../assets/new.svg) GraphQL スキーマに、商品情報の `lastModifiedAt` 属性が含まれるようになりました。 この正確なタイムスタンプは、顧客がサイトマップで製品の最新の更新を正確に反映するのに役立ちます。 また、Googleなどの検索エンジンでインデックス再作成が必要なタイミングを判断し、クローリングプロセスを最適化し、正確な情報が利用できない場合に使用される積極的な最終変更日に関連する問題を防ぐのに役立ちます。<!--DATA-6209-->

## 以前のバージョン

+++ 以前のバージョン

### V1.23 リリース

_2024 年 8 月 22 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 修正 ](../assets/fix.svg) 製品の上書き（価格）データを使用せずに製品情報を取得できるようになりました。 以前のリリースでは、これらのクエリで次のエラーが返されていました。
`The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.` <!--DATA-6121-->

### V1.22 リリース

_2024 年 8 月 13 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 新規 ](../assets/new.svg) 製品 SKU ごとにすべてのバリアントを取得するサポートが追加されました。 詳しくは、[Catalog Service API リファレンス ](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/) を参照してください。<!--DATA-6067-->

### V1.22 リリース

_2024 年 8 月 13 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 新規 ](../assets/new.svg) 製品 SKU ごとにすべてのバリアントを取得するサポートが追加されました。 詳しくは、[Catalog Service API リファレンス ](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/) を参照してください。<!--DATA-6067-->

### V1.19 リリース

_2024 年 5 月 23 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降


![ 修正 ](../assets/fix.svg)<!--DATA-5033--> オプション値の `InStock` フラグで、製品バリアントのスコーピングされた `enabled` ステータスが考慮されるようになりました。

![ 修正 ](../assets/fix.svg)<!--DATA-5888--> 大きな数値（最大 16 桁）とより大きな小数点精度（最大 4 桁）を必要とする製品価格のサポートを追加しました。 既存のカタログに価格構成の更新を適用するには、[Data Management ダッシュボード ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard) から、または [Adobe Commerce コマンドラインインターフェイス ](../landing/catalog-sync.md#command-line-interface) を使用して、カタログデータを再同期します。

#### 既知の制限事項

次の機能は、まだサポートされていません。

* 動的属性ペイロードの最大サイズは 9 MB です。
* グループ商品価格はシンプルな商品価格で算出できます。
* 画像配列では、最初の画像にのみ役割が含まれます。

API メッシュとコア GraphQL API を使用して、次の制限を解決します。

* 広告の最低価格
* 階層の価格
* 固定価格で製品をバンドル

詳細と例については、[ カタログサービスと API メッシュ ](mesh.md) を参照してください。

### V1.18 リリース

_2024 年 4 月 11 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 新規 ](../assets/new.svg)PHP 8.3 のサポートを追加しました。

![ 新規 ](../assets/new.svg)[`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) クエリと [`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) クエリは、シンプルな製品と複雑な製品の両方でカスタマイズ可能なオプションデータを返すようになりました。<!--DATA-5538-->

### V1.17 リリース

_2024 年 2 月 22 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 新規 ](../assets/new.svg)[[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-dashboard.html) が利用可能になりました。 この刷新されたダッシュボードでは、[!DNL Product Recommendations]、[!DNL Live Search] および [!DNL Catalog Service] のデータストリームに関するインサイトが提供されます。 この機能のサポートは、`catalog-service` メタパッケージの v3.1.0 で導入されました。

### V1.16 リリース

_2024 年 2 月 13 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 新規 ](../assets/new.svg)Catalog Service API で製品ビデオがサポートされるようになりました。
![ 修正 ](../assets/fix.svg) 在庫切れのオプションが PDP ウィジェットに表示されるようになりました。

#### 既知の制限事項

これらの機能は、まだサポートされていません。

* 動的属性ペイロードの最大サイズは 9 MB です。
* グループ製品価格。 この値は、単純な製品価格で計算できます。
* 画像配列では、最初の画像にのみ役割が含まれます。

API メッシュとコア GraphQL API を使用すると、次の制限を解決できます。

* 広告の最低価格
* [階層の価格](mesh.md)

### V1.13 リリース

_2023 年 10 月 12 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 新規 ](../assets/new.svg) カタログサービスでは、製品バリアントの `inStock` フラグをサポートしています。
![ 新規 ](../assets/new.svg)`urlKey` フィールドと `externalId` フィールドがGraphQL スキーマに追加されました。
![ 新規 ](../assets/new.svg) ダウンロード可能な製品とギフトカードがサポートされるようになりました。

### V1.12 リリース

_2023 年 9 月 19 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 新規 ](../assets/new.svg) カタログサービスで [SaaS 価格インデックス作成 ](../price-index/price-indexing.md) が使用されるようになりました。
![ 修正 ](../assets/fix.svg) このリリースには、サービス側のバグ修正と改善が含まれています。

### V1.11 リリース

_2023 年 7 月 18 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 新規 ](../assets/new.svg) カタログサービスで、商品レコメンデーション用の [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/recommendations/) GraphQL クエリがサポートされるようになりました。

### V1.10 リリース

_2023 年 6 月 27 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 新規 ](../assets/new.svg)Catalog Service API で `related products` がサポートされるようになりました。

### V1.7 リリース

_2023 年 4 月 12 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 新規 ](../assets/new.svg) 削除された製品のバリエーションがカタログサービスでクリーンアップされるようになりました。
![ 修正 ](../assets/fix.svg) インフラストラクチャの拡張性とパフォーマンスの向上。

### V1.6 リリース

_2023 年 3 月 28 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 新規 ](../assets/new.svg)[`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) クエリにスウォッチを追加しました。
![ 新規 ](../assets/new.svg) [API メッシュ ](mesh.md) を使用して `entityId` を取得する機能が追加されました。

### V1.5 リリース

_2023 年 3 月 6 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![ 新規 ](../assets/new.svg) GraphQL機能 [`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) 追加しました。
![ 修正 ](../assets/fix.svg) パフォーマンスと API のスケーラビリティが向上しました。

### V1.4 リリース

_2023 年 2 月 7 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 新規 ](../assets/new.svg) 公開されたカタログサービスメタパッケージで、インストール手順を簡素化します。
![ 修正 ](../assets/fix.svg)API のスケーラビリティとパフォーマンスの改善。

### V1.3 リリース

_2023 年 1 月 17 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 新機能 ](../assets/new.svg) オンボーディングエクスペリエンスを簡素化および改善しました。
![ 新規 ](../assets/new.svg) 新しい顧客サンドボックスエンドポイントは、実稼動前のテストで使用できます。
![ 新規 ](../assets/new.svg) 仮想製品のサポートが追加されました。
![ 修正 ](../assets/fix.svg)API のスケーラビリティとパフォーマンスの改善。

### V1.1 リリース

_2022 年 11 月 18 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 新規 ](../assets/new.svg) カタログサービスでAdobe [API メッシュ ](https://developer.adobe.com/graphql-mesh-gateway/) がサポートされるようになりました。
![ 修正 ](../assets/fix.svg) API のスケーラビリティと全体的なパフォーマンスが向上しました。

### V1.0 リリース

_2022 年 10 月 4 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 新規 ](../assets/new.svg) バンドルされた製品とグループ化された製品をサポートするようになりました。
![ 新規 ](../assets/new.svg) B2B 表示オーバーライドを追加しました。 製品が検索できるようになり、特定の顧客グループのために買い物かごに追加できるようになりました。
![ 修正 ](../assets/fix.svg) サービスがより安定し、パフォーマンスが向上しました。

### 0.3 リリース - Beta+

_2022 年 9 月 12 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 新規 ](../assets/new.svg) バリアント用の画像はサポートされます。製品画像は、選択したオプションに基づいて返されます
![ 新規 ](../assets/new.svg) 価格サポートの役割：特定の顧客グループのメンバーのみが製品の価格を表示できるようにします
![ 修正 ](../assets/fix.svg) サービスの安定性とパフォーマンスの向上
![ 新規 ](../assets/new.svg) 製品がカタログから削除されると、更新が受信されます

### Beta リリース

_2022 年 8 月 9 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![ 新規 ](../assets/new.svg) `products` クエリと `refineProduct` クエリは、次のデータを返します。

* 事前定義済み（システム）製品属性。
* 製品の動的属性および役割別のフィルター（製品の表示ページ/製品のリストページ）。
* 製品オプション。
* 製品画像を役割（PDP/PLP）別にフィルタリングする方法を説明します。
* シンプルな製品の特定の価格と設定可能な製品の価格範囲。
* 顧客グループの価格と価格範囲。 顧客グループを持たない買い物客に対しては、フォールバックのデフォルト価格が返されます。
* B2B 顧客固有の価格を使用する製品タイプ。
