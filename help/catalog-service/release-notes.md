---
title: '[!DNL Commerce Storefront Catalog Service Release Notes]'
description: Adobe Commerceの最新  [!DNL Catalog Service]  リリース情報です。
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
source-git-commit: 9ba7a964243c616cc7e40fb180a855b839cd4597
workflow-type: tm+mt
source-wordcount: '2252'
ht-degree: 0%

---

# [!DNL Commerce Storefront Catalog Service] リリースノート

これらのリリースノートでは、次のような最新のCommerce カタログサービスのアップデートについて説明しています。

- **ストアフロントカタログサービスリリース**

   - データ取得を改善するための Catalog Service API スキーマの機能強化。
   - Catalog Service API とその基盤となるインフラストラクチャのセキュリティ、パフォーマンス、信頼性の向上。

- **Catalog Service metapackage リリース**

   - パフォーマンス、安定性、他のAdobe Commerce コンポーネントとの互換性を向上させるための依存関係を更新しました。

アップデートはタイプ別に分類されます。

![&#x200B; 新機能 &#x200B;](../assets/new.svg) 新機能
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 修正点および改善点
![&#x200B; バグ &#x200B;](../assets/bug.svg) 既知の問題

最新バージョンのサポートが提供されています。 古いバージョンのリリースノートは参照用に含まれています。

## Storefront カタログサービス

### v1.48 リリース

_2025 年 2 月 19 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg) GraphQL API の `categoryTree` クエリで、カテゴリの説明、画像および SEO メタタグを返すようになりました。 この更新により、ストアフロントの開発者がカテゴリ画像を表示し、適切なメタタイトル、説明およびキーワードで検索エンジンの最適化を向上させるために必要なデータが提供されます。 ヘッドレスストアフロントの場合、[&#x200B; コンポーザブルカタログデータモデル &#x200B;](https://developer.adobe.com/commerce/services/optimizer/) を使用したCommerce実装でのみサポートされます &lt;<!--DATA-6933-->

### v1.47 リリース

_2025 年 2 月 12 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg)API サービスで `CategoryProductView` タイプがサポートされ、カテゴリ別の製品の拡張ビューとクエリが有効になりました。 この更新により、開発者はカテゴリに基づいて製品データを効率的に取得およびフィルタリングでき、カテゴリ駆動型のユースケースの柔軟性とパフォーマンスが向上します。 詳しくは、[&#x200B; ストアフロントでのカテゴリの実装 &#x200B;](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/categories-storefront-implementation/) を参照してください。 ヘッドレスストアフロントの場合、[&#x200B; 構成可能なカタログデータモデル &#x200B;](https://developer.adobe.com/commerce/services/optimizer/) を使用したCommerce実装でのみサポートされま <!--DATA-6949-->。

### v1.46 リリース

_2025 年 12 月 11 日_

![&#x200B; 修正 &#x200B;](../assets/fix.svg) システムレベルおよびインフラストラクチャの改善により、パフォーマンスと安定性を向上させます。<!--DATA-6852, DATA-6864-->

### v1.45 リリース

_2025 年 11 月 17 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg)**名前による属性フィルタリング** - `productSearch` GraphQL クエリで、`names` フィールドを使用した製品属性のフィルタリングがサポートされるようになりました。 <!--DATA-6831--> このフィルターを使用すると、次のことができます。

- 特定の属性のみをリクエストすることで、応答のペイロードサイズを削減
- 既存の `roles` フィルターと組み合わせて、表示ロールと属性名で絞り込みます
- 例：

  **属性名のみでフィルタリング**

  ```graphql
  query {
    products(skus: ["SKU-001"]) {
      attributes(names: ["color", "size", "material"]) {
        name
        label
        value
      }
    }
  }
  ```

  **役割と名前の両方でフィルタリング：**

  ```graphql
  query {
    products(skus: ["SKU-001"]) {
      attributes(roles: ["visible in PDP"], names: ["eco_collection", "new"]) {
        name
        label
        value
        roles
      }
    }
  }
  ```

>[!NOTE]
>
>フィルターを適用せずにすべての属性を取得するには、`names` 引数を省略するか、空の配列を指定します。

### v1.44 リリース

_2025 年 11 月 6 日_

![&#x200B; 修正 &#x200B;](../assets/fix.svg) システムレベルおよびインフラストラクチャの改善により、パフォーマンスと安定性を向上させます。<!--DATA-6852, DATA-6864-->

### v1.43 リリース

_2025 年 11 月 3 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg)**多次元製品カスタマイズ用の製品レイヤー** - Adobe Commerce Optimizer実装で、チャネル固有のロケール対応コンテンツ配信がサポートされるようになりました。<!--DATA-6632-->

- 様々な製品コンテンツを様々な顧客セグメントに提供する
- ベースデータを複製せずにロケール固有のカスタマイズを適用する
- レイヤーマスクを使用したフィールドレベルのオーバーライドの制御
- プレミアム、季節ごとのコンテンツ、モバイルに最適化されたコンテンツレイヤーのサポート

  レイヤーは、既存の `products` クエリを使用して取得され、リクエストヘッダーからサーバーサイドで適用され、スキーマの変更は必要ありません。 詳しくは、[Adobe Commerce Optimizerガイドの &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/setup/catalog-layer) カタログレイヤー _を参照してください_

![&#x200B; 修正 &#x200B;](../assets/fix.svg) 親に価格がない場合、グループ化された製品をクエリできるようになりました。子製品は、独自の表示役割を返します。<!--DATA-6779-->

![&#x200B; 修正 &#x200B;](../assets/fix.svg) システムレベルおよびインフラストラクチャの改善により、パフォーマンスと安定性を向上させます。<!--DATA-6721, DATA-6864-->

### v1.42 リリース

_2025 年 9 月 8 日_

![&#x200B; 新 &#x200B;](../assets/new.svg)**追加された階層別価格サポート** によるボリューム価格の照会：<!--DATA-6643-->

階層レベルの価格を取得するには：

1. 目的の SKU で `products` クエリを使用します
2. **SimpleProductView** の場合、`price.tiers` にアクセスします
3. **ComplexProductView** については、`priceRange.minimum.tiers` および `priceRange.maximum.tiers` にアクセスします
4. 各階層には、割引された `tier` 価格と `quantity` 条件が含まれます
5. `gte` （以上）および `lt` （以下）の数量しきい値を定義します

**例：**

```graphql
query {
  products(skus: ["SKU-001"]) {
    ... on SimpleProductView {
      price {
        regular { amount { value currency } }
        tiers {
          tier { amount { value currency } }
          quantity {
            ... on ProductViewTierRangeCondition { gte lt }
          }
        }
      }
    }
  }
}
```

![&#x200B; 最終価格の最小値でフィルタリングした固定 &#x200B;](../assets/fix.svg) **階層価格** <!--DATA-6643-->

API は、割引価格が製品の最終価格の最低価格 **下** の層のみを返すようになりました。 ストアフロントには最終価格の最小値が適用されるので、より高い階層は省略されます。

適用先：

- **シンプル製品**:`price.tiers` には、`tier.amount.value` &lt; `price.final.amount.value` （最小最終）の階層のみが含まれます。
- **複雑な製品**:`priceRange.minimum.tiers` と `priceRange.maximum.tiers` は、価格範囲を作成する際に同じルールを使用します。

### v1.41 リリース

_2025 年 9 月 2 日_

![&#x200B; 修正 &#x200B;](../assets/fix.svg)**価格情報が見つからない場合のエラー処理の改善** – 価格データがまだ受信されていない場合、API はエラーをスローする代わりに価格フィールドの `null` を返し、クライアントが欠落しているデータを適切に処理できるようにします。<!--DATA-6612-->

![&#x200B; 修正 &#x200B;](../assets/fix.svg) システムレベルおよびインフラストラクチャの改善により、パフォーマンスと安定性を向上。<!--DATA-6671-->

### v1.40 リリース

_2025 年 7 月 30 日_

![&#x200B; 修正 &#x200B;](../assets/fix.svg) セキュリティ、パフォーマンス、安定性を強化するためのシステムレベルおよびインフラストラクチャの改善 <!--DATA-6619-->

### v1.39 リリース

_2025 年 7 月 24 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg)**ユニット ID でレコメンデーションユニットを取得** – 新しいGraphQL エンドポイント `recommendationsByUnitIds` より柔軟でターゲットを絞ったアクセスのために、一意の ID でレコメンデーションユニットを取得します。

- `unitIds` は必須です（取得する recId のリスト）。
- コンテキストパラメーター（`currentSku`、`cartSkus`、`userViewHistory`、`userPurchaseHistory`、`category`）は、既存のレコメンデーションクエリと同じように動作します。

- **例**

  ```graphql
  query {
    recommendationsByUnitIds(
      unitIds: ["11ee89d1-bfae-4582-a921-2ced44ff6bf7"]
      currentSku: "24-MB01"
      cartSkus: ["24-MB01"]
    ) {
      totalResults
      results {
        unitId
        unitName
        totalProducts
        productsView {
          sku
        }
        pageType
        typeId
        storefrontLabel
        displayOrder
      }
    }
  }
  ```

![&#x200B; 修正 &#x200B;](../assets/fix.svg) セキュリティ、パフォーマンス、安定性を強化するためのシステムレベルおよびインフラストラクチャの改善 <!--DATA-6316-->

### v1.38 リリース

_2025 年 7 月 15 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg)**ギフトカードの製品タイプ**-Catalog Storefront サービスで、JSON オブジェクトや配列などの製品属性がサポートされるようになり、ギフトカードなどの複雑なタイプを柔軟に管理できるようになりました。<!--DATA-6573-->


### v1.37 リリース

_2025 年 6 月 20 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg)**階層的な価格台帳構成** – 親子価格台帳の正確な価格範囲。 計算では、階層と継承されたルールが考慮されます。複数の価格台帳がリンクされている場合は、価格設定エラーが減少します。 Adobe Commerce Optimizerのみ。 [&#x200B; 本の価格 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/setup/pricebooks) を参照してください。

![&#x200B; 新規 &#x200B;](../assets/new.svg)**大文字と小文字を区別しないキー** - クエリ内のキー検索で大文字と小文字を区別しなくなり、キーの大文字と小文字からエラーを減らしました。<!--DATA-6494, DCAT-2495-->

### v1.36 リリース

_2025 年 6 月 20 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg)**Catalog Storefront 用のパブリック IO イベント** - リアルタイム統合および可観測性（CSS および EDS）を実現するパブリック IO イベントを追加しました。<!--DATA-6329-->

![&#x200B; 新規 &#x200B;](../assets/new.svg)**サーバーサイドレンダリング（SSR）** – 大規模なカタログでのパフォーマンス、SEO、UX の向上を実現する SSR をサポートするアーキテクチャが改善されました。<!--DATA-6278, DATA-6280-->

![&#x200B; 新規 &#x200B;](../assets/new.svg)**インフラストラクチャとセキュリティ** – 新しいAWSの役割、ServiceNow の統合、イベントサービスの CI/CD パイプラインが追加されました。

![&#x200B; 新規 &#x200B;](../assets/new.svg)**イベント形式と可観測性** - ペイロードの効率化、モニタリングの強化、バリアントイベントデータの改善 <!--DATA-6332, DATA-6402, -->

![&#x200B; 修正 &#x200B;](../assets/fix.svg) セキュリティ、パフォーマンス、安定性を強化するためのシステムレベルおよびインフラストラクチャの改善 <!--DATA-6404, DATA-6410, -->

+++ 以前のバージョン

## v1.35 リリース

_2025 年 6 月 13 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg) **キャッシュされていないデータを取得** - `Magento-Is-Preview` ヘッダーを有効にして、キャッシュされていないデータをカタログエンドポイントから検索サービスに渡します。<!--DATA-6345-->

![&#x200B; 新規 &#x200B;](../assets/new.svg)**複数選択の商品オプション**-GraphQL API で、商品オプションで複数の選択が許可されているかどうかを表示するようになりました（例えば、バンドルで「複数の項目を選択」を選択するなど）。<!--DATA-6487-->

![&#x200B; 新規 &#x200B;](../assets/new.svg) 価格のない製品をサポートするために、データ取り込みに関する価格検証を更新しました。<!--DATA-6098-->

![&#x200B; 修正 &#x200B;](../assets/fix.svg)Adobe Commerce Optimizerでシンプルなバンドル価格を実現するため、エラー処理を改善しました。<!--DATA-6541-->

![&#x200B; 修正 &#x200B;](../assets/fix.svg) セキュリティ、パフォーマンス、安定性を強化するためのシステムレベルおよびインフラストラクチャの改善 <!--DATA-6273, DATA-6485, -->

## v1.34 リリース

_2025 年 3 月 23 日_

![&#x200B; 修正 &#x200B;](../assets/fix.svg) セキュリティ、パフォーマンス、安定性を強化するためのシステムレベルおよびインフラストラクチャの改善 <!--DATA-5732-->

## v1.33 リリース

_2025 年 4 月 29 日_

![&#x200B; 修正 &#x200B;](../assets/fix.svg) システムレベルとインフラストラクチャの改善。 インフラストラクチャは、既存のワークロードに影響を与えることなく、非常に大きなカタログ（最大 4 億 4,000 万 SKU）をサポートするようになりました。

### v1.32 リリース

_2025 年 3 月 28 日_

![&#x200B; 修正 &#x200B;](../assets/fix.svg) 構成可能なカタログに対して、役割を持たない属性のインデックスがデフォルトで作成されなくなり、インデックス作成時間が短縮され、ストレージが削減されました。 機能フラグを使用して、レガシー動作を再度有効にすることができます。

![&#x200B; 修正 &#x200B;](../assets/fix.svg) システムレベルおよびインフラストラクチャの改善により、セキュリティ、パフォーマンス、安定性を向上させます。<!--DATA-6348, DATA-6440, DATA-6446, DATA-6641-->

### v1.31 リリース

_2025 年 2 月 18 日_

![&#x200B; 修正 &#x200B;](../assets/fix.svg) セキュリティ、パフォーマンス、安定性を強化するためのシステムレベルおよびインフラストラクチャの改善 <!--DATA-6389, DATA-6367, DATA-6373-->

### v1.30 リリース

_2024 年 12 月 9 日_

メジャーリリース：ヘッドレスストアフロント、ヘッダー管理、製品データ処理のための [&#x200B; 構成可能なカタログデータモデル &#x200B;](https://developer.adobe.com/commerce/services/optimizer/)。

![&#x200B; 新規 &#x200B;](../assets/new.svg) **構成可能なカタログ・データ・モデル（CCDM）**：構成可能なカタログを使用してヘッドレス・ストアフロントをサポートします。 新しいエンドポイントは、カタログビューとポリシー ID を受け入れます（下位互換性があります）。 組み込みのページネーションを使用した、設定可能な製品の詳細と価格。<!--DATA-6018, DATA-6288-->

![New](../assets/new.svg)**Header Management**-`AC-Locale` を、構成可能なカタログ API 操作のために `AC-Scope-Locale` に名前を変更しました。ヘッダーマッピングとデフォルト値を指定しました。<!--DATA-6303, DATA-6078-->

![&#x200B; 新 &#x200B;](../assets/new.svg)**製品データと価格設定** 構成可能なカタログデータモデルのサポートと、構成可能な製品の価格処理の向上。<!--DATA-6279-->

`CurrencyEnum` は、フェデレーション ロジックに合わせて、製品検索クエリの `NONE` をサポートするように更新されました。<!--DATA-6285-->

![&#x200B; 修正 &#x200B;](../assets/fix.svg)**インフラストラクチャとアップグレード**：セキュリティ、パフォーマンス、安定性に関するシステム・レベルの向上

![&#x200B; 修正 &#x200B;](../assets/fix.svg) バンドルの製品オプションに有効な製品のみが表示されるようになりました。<!--DATA-6347-->

### v1.29 リリース

_2024 年 12 月 9 日_

![&#x200B; 新機能 &#x200B;](../assets/new.svg)**商品クエリでの画像順序** – 「GraphQL `images`」フィールドの商品画像がカタログの書き出し `sortOrder` に従って、ストアフロントと API の動作が一貫するようになりました。<!--DATA-6258-->

![&#x200B; 修正 &#x200B;](../assets/fix.svg) セキュリティ、パフォーマンス、安定性を強化するためのシステムレベルおよびインフラストラクチャの改善 <!--DATA-6619-->

### v1.28 リリース

![&#x200B; 修正 &#x200B;](../assets/fix.svg) セキュリティ、パフォーマンス、安定性を強化するためのシステムレベルおよびインフラストラクチャの改善 <!--DATA-6180, DATA-6230, DATA-6254, DATA-6257-->

### v1.27 リリース

_2024 年 9 月 26 日_

![&#x200B; 修正 &#x200B;](../assets/fix.svg) セキュリティ、パフォーマンス、安定性を強化するためのシステムレベルおよびインフラストラクチャの改善 <!--DATA-6243-->

### v1.26 リリース

_2024 年 10 月 22 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) GraphQL スキーマに、正確なサイトマップと検索エンジンのインデックス再作成（Googleなど）のための製品情報の `lastModifiedAt` が含まれるようになりました。<!--DATA-6209-->

### v1.23 リリース

_2024 年 8 月 22 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 修正 &#x200B;](../assets/fix.svg) 製品の上書き（価格）データなしで製品情報を取得できるようになりました。 以前は、次のクエリが返されていました：`The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.` <!--DATA-6121-->

### v1.22 リリース

_2024 年 8 月 13 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) 製品 SKU ごとにすべてのバリアントを取得するサポートが追加されました。 詳しくは、[Catalog Service API リファレンス &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/) を参照してください。<!--DATA-6067-->

### v1.19 リリース

_2024 年 5 月 23 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降


![&#x200B; 修正 &#x200B;](../assets/fix.svg)<!--DATA-5033--> オプション値の `InStock` フラグは、製品バリアントのスコーピングされた `enabled` ステータスを尊重するようになりました。

![&#x200B; 修正 &#x200B;](../assets/fix.svg)<!--DATA-5888--> 最大 16 桁、小数点以下 4 桁の製品価格のサポートが追加されました。 [&#x200B; データ管理ダッシュボード &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) または [CLI](../landing/catalog-sync.md#command-line-interface) から再同期して、更新を適用します。

#### 既知の制限事項

次の機能は、まだサポートされていません。

- 動的属性ペイロードの最大サイズは 9 MB です。
- グループ商品価格はシンプルな商品価格で算出できます。
- 画像配列では、最初の画像にのみ役割が含まれます。

次の場合は、API メッシュとコア GraphQL API を使用します。

- 広告の最低価格
- 階層の価格
- 固定価格で製品をバンドル

詳細と例については、[&#x200B; カタログサービスと API メッシュ &#x200B;](mesh.md) を参照してください。

### v1.18 リリース

_2024 年 4 月 11 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg)PHP 8.3 のサポートを追加しました。

![&#x200B; 新規 &#x200B;](../assets/new.svg) [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) クエリと [`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) クエリは、シンプルな製品と複雑な製品の両方でカスタマイズ可能なオプションデータを返すようになりました。<!--DATA-5538-->

### v1.17 リリース

_2024 年 2 月 22 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) データストリーム（製品レコメンデーション、ライブ検索、カタログサービス）で [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html?lang=ja) を使用できるようになりました。 `catalog-service` metapackage v3.1.0 以降が必要です。

### v1.16 リリース

_2024 年 2 月 13 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg)Catalog Service API で製品ビデオがサポートされるようになりました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) 在庫切れのオプションが PDP ウィジェットに表示されるようになりました。

#### 既知の制限事項

これらの機能は、まだサポートされていません。

- 動的属性ペイロードの最大サイズは 9 MB です。
- グループ製品価格。 この値は、単純な製品価格で計算できます。
- 画像配列では、最初の画像にのみ役割が含まれます。

次の場合は、API メッシュとコア GraphQL API を使用します。

- 広告の最低価格
- [階層の価格](mesh.md)

### v1.13 リリース

_2023 年 10 月 12 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) カタログサービスでは、製品バリアントの `inStock` フラグをサポートしています。
![&#x200B; 新規 &#x200B;](../assets/new.svg)`urlKey` フィールドと `externalId` フィールドがGraphQL スキーマに追加されました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) ダウンロード可能な製品とギフトカードがサポートされるようになりました。

### v1.12 リリース

_2023 年 9 月 19 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) カタログサービスで [SaaS 価格インデックス作成 &#x200B;](../price-index/price-indexing.md) が使用されるようになりました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) このリリースには、サービス側のバグ修正と改善が含まれています。

### v1.11 リリース

_2023 年 7 月 18 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) カタログサービスで、商品レコメンデーション用の [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) GraphQL クエリがサポートされるようになりました。

### v1.10 リリース

_2023 年 6 月 27 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg)Catalog Service API で `related products` がサポートされるようになりました。

### v1.7 リリース

_2023 年 4 月 12 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) 削除された製品のバリエーションがカタログサービスでクリーンアップされるようになりました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) インフラストラクチャの拡張性とパフォーマンスの向上。

### v1.6 リリース

_2023 年 3 月 28 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) クエリにスウォッチを追加しました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) `entityId`API メッシュ [&#x200B; を使用して &#x200B;](mesh.md) を取得する機能が追加されました。

### v1.5 リリース

_2023 年 3 月 6 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) GraphQL機能 [`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) 追加しました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) パフォーマンスと API のスケーラビリティが向上しました。

### v1.4 リリース

_2023 年 2 月 7 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) 公開されたカタログサービスメタパッケージで、インストール手順を簡素化します。
![&#x200B; 修正 &#x200B;](../assets/fix.svg)API のスケーラビリティとパフォーマンスの改善。

### v1.3 リリース

_2023 年 1 月 17 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![&#x200B; 新機能 &#x200B;](../assets/new.svg) オンボーディングエクスペリエンスを簡素化および改善しました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) 新しい顧客サンドボックスエンドポイントは、実稼動前のテストで使用できます。
![&#x200B; 新規 &#x200B;](../assets/new.svg) 仮想製品のサポートが追加されました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg)API のスケーラビリティとパフォーマンスの改善。

### v1.1 リリース

_2022 年 11 月 18 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) カタログサービスでAdobe [API メッシュ &#x200B;](https://developer.adobe.com/graphql-mesh-gateway/) がサポートされるようになりました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) API のスケーラビリティと全体的なパフォーマンスが向上しました。

### v1.0 リリース

_2022 年 10 月 4 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) バンドルされた製品とグループ化された製品のサポート。
![&#x200B; 新規 &#x200B;](../assets/new.svg) B2B 表示オーバーライドを追加しました。 製品が検索できるようになり、特定の顧客グループのために買い物かごに追加できるようになりました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) サービスがより安定し、パフォーマンスが向上しました。

### 0.3 リリース - Beta+

_2022 年 9 月 12 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) バリアント画像：選択したオプションに基づいて返される製品画像。
![&#x200B; 新規 &#x200B;](../assets/new.svg) 価格の役割：特定の顧客グループのメンバーのみが製品価格を表示できます。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) サービスの安定性とパフォーマンスが向上しました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) 製品がカタログから削除されると、更新が受信されます。

### Beta リリース

_2022 年 8 月 9 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.x 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) `products` クエリと `refineProduct` クエリは、次のデータを返します。

- 事前定義済み（システム）製品属性。
- 製品の動的属性および役割別のフィルター（製品の表示ページ/製品のリストページ）。
- 製品オプション。
- 製品画像を役割（PDP/PLP）別にフィルタリングする方法を説明します。
- シンプルな製品の特定の価格と設定可能な製品の価格範囲。
- 顧客グループの価格と価格範囲。 顧客グループを持たない買い物客に対しては、フォールバックのデフォルト価格が返されます。
- B2B 顧客固有の価格を使用する製品タイプ。

+++

## Catalog Service メタパッケージ

カタログサービスの PHP メタパッケージ （`magento/catalog-service`）を更新しました。

- Adobe Commerce as a Cloud Serviceをご利用のお客様の場合、お使いの環境に最新バージョンがインストールされています。

- オンプレミスのクラウド上のAdobe Commerceの場合、Adobeでは Composer を使用して、クラウド環境のカタログサービスメタパッケージを最新リリースにアップグレードすることをお勧めします。

### v3.3.0 リリース

_2025 年 10 月 14 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) **データ サービスのアップグレード**—`magento/data-services` 依存関係が^8.0.0 に更新されました。アップグレードする前に、8.x の互換性に関する環境およびカスタム Data Services API の使用状況を確認してください。
ea
![&#x200B; 新規 &#x200B;](../assets/new.svg) 3.3.0 リリースのバージョンとメタデータを更新しました。

### v3.2.0 リリース

_2024 年 4 月 12 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg)3.2.0 のバージョンとメタデータが更新されました。その他の依存関係は変更されません。

### v3.1.0 リリース

_2024 年 1 月 26 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) 新しいパッケージ依存関係を追加しました。

- カタログサービスで使用されるカテゴリ権限データを書き出すための **カテゴリ権限データエクスポーター** （`magento/module-category-permission-data-exporter`）。
- カタログ同期に関連する管理 UI および設定の **カタログ同期管理者**`magento/module-catalog-sync-admin`。

![&#x200B; 新規 &#x200B;](../assets/new.svg) 3.1.0 リリースのバージョンとメタデータを更新しました。

## 関連ドキュメント

- Adobe Commerce on cloud、オンプレミスまたはAdobe Commerce as a Cloud Serviceにデプロイされたプロジェクトの場合は、次のドキュメントを参照してください。

   - [カタログサービスガイド](overview.md)
   - [Catalog Service GraphQL API リファレンス &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)
   - [Adobe Commerce管理ガイド &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/)
   - [Adobe Commerce as a Cloud Service ガイド &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/)
   - [Adobe Commerce on Cloud ガイド &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud/)

- **Adobe Commerce Optimizer** または **Adobe Commerce Optimizer Connector** を使用するプロジェクトの場合は、次のドキュメントを参照してください。

   - [&#x200B; マーチャンダイジングサービス開発者ガイド &#x200B;](https://developer.adobe.com/commerce/services/optimizer/)
   - [&#x200B; マーチャンダイジング GraphQL API リファレンス &#x200B;](https://developer.adobe.com/commerce/services/reference/graphql/)
   - [Adobe Commerce Optimizer ガイド](../optimizer/overview.md)
