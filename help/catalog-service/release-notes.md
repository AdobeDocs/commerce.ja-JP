---
title: '[!DNL Commerce Storefront Catalog Service Release Notes]'
description: Adobe Commerceの [!DNL Catalog Service] の最新リリース情報。
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
TQID: https://experienceleague.adobe.com/-yxW4sTuk7LPjGy5YsQ65phtkBLiByg8SmBaQPHMevM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 616ad9e9b45a66f127a55ef87dd6c6b9c0b470c8
workflow-type: tm+mt
source-wordcount: 3024
ht-degree: 0%

---

# [!DNL Commerce Storefront Catalog Service] リリースノート

このリリースノートでは、次のような最新のCommerce カタログサービスのアップデートについて説明します。

- **[ストアフロントカタログサービスのリリース](#storefront-catalog-service)**

   - カタログサービス API スキーマの機能強化によるデータ取得の改善
   - カタログサービス APIとその基盤となるインフラストラクチャのセキュリティ、パフォーマンス、信頼性を向上させます。

  これらのAPIについて詳しくは、Commerce Developer ドキュメントの[Storefront Services スキーマ &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)を参照してください。

- **[カタログサービス メタパッケージリリース](#catalog-service-metapackage)**

   - パフォーマンス、安定性、他のAdobe Commerce コンポーネントとの互換性を向上させるために、依存関係を更新しました。

- **[カタログ サービス インストーラーのリリース](#catalog-service-installer)**

   - カタログサービスとCommerce スタックの互換性を維持するために、依存関係を更新しました。

>[!NOTE]
>
>Commerce プロジェクトでAdobe Commerce Optimizerを使用してカタログデータをCommerce Edge Delivery サービスまたはヘッドレスストアフロントに配信する場合は、最新のAPI アップデートについて[Adobe Commerce Optimizer リリースノート &#x200B;](../optimizer/release-notes.md)を参照してください。

更新はタイプ別に分類されます。

![新機能](../assets/new.svg)
![修正](../assets/fix.svg)修正と機能強化
![&#x200B; バグ &#x200B;](../assets/bug.svg)既知の問題

最新バージョンのサポートが提供されます。 古いバージョンのリリースノートは、参照用に含まれています。

## Storefront Catalog Service

## 2026年6月

**リリース日**: 2026年7月1日

![新規](../assets/new.svg) **新規`canEditQuantity` フィールド** - カタログサービス GraphQLで`canEditQuantity`を`ProductViewOptionValueProduct`に追加しました。 Commerce管理者からバンドル選択のオプションの&#x200B;**User Defined**&#x200B;数量設定を公開するので、ストアフロントコンシューマーはバンドル選択の数量が編集可能かどうかを判断できます。

### 2026年5月

**リリース日**: 2026年5月20日
<!-- v1.55 -->

![新規](../assets/new.svg)文書化された制限と境界[に従って、Adobe CommerceとAdobe Commerce as a Cloud Serviceの両方のクライアントに対して、リクエストごとに最大100 SKUの制限を適用しました](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/boundaries-limits)。


**リリース日**: 2026年5月13日


![新規](../assets/new.svg) **GraphQLでのカテゴリの並べ替え順序** - `CategoryView` GraphQL タイプにポジションフィールドが含まれるようになりました。そのため、ストアフロントでは、カタログ階層で加盟店が設定した順序でカテゴリを表示できます。


**リリース日**: 2026年5月4日
<!-- v1.53 -->

![修正](../assets/fix.svg) ストアフロントの製品価格には、すべての製品タイプに対して正しい通貨コード（USDなど）が表示されるようになりました。 以前は、一部の製品で予想される通貨の代わりに`NONE`が表示され、価格が欠落していました。 この更新により、ストアフロント全体で一貫性のある正確な価格レンダリングが保証されます。<!--DATA-7115-->

### 2026年4月

**リリース日**: 2026年4月29日


![新規](../assets/new.svg) Adobe Commerce OptimizerおよびAdobe Commerce as a Cloud Serviceのリクエストごとに、最大100 SKUの制限が適用されました
[文書化された制限と境界](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/boundaries-limits)に従うクライアント。<!--DATA-7156-->

**リリース日**: 2026年4月17日


![新規](../assets/new.svg) クライアントがページ区切りの結果を含むカテゴリを名前で検索できる新しい`searchCategory` GraphQL クエリを追加しました。 クエリは、必須の`searchTerm` （最低3文字）およびオプションの`family`、`pageSize`、および`currentPage`個のパラメーターを受け入れます。 結果には、完全なカテゴリ メタデータを持つ`CategoryTreeView` オブジェクト、ページネーション用の`totalCount`および`pageInfo`が含まれます。<!--COMOPT-1819-->

このクエリは、Adobe Commerce Optimizer マーチャンダイジングサービスを使用しているお客様のみが使用できます。 [searchCategory](https://developer.adobe.com/commerce/services/reference/graphql/)を参照してください。

### 2026年3月

**リリース日**: 2026年3月24日


![新規](../assets/new.svg)動的バンドルの価格帯を計算および返すためのサポートを追加しました。


### 2025年12月

**リリース日**: 2025年12月11日
<!-- v1.46 -->

![&#x200B; パフォーマンスと安定性を向上させるために、システム レベルとインフラストラクチャの改善を](../assets/fix.svg)修正します。


### 2025年11月

**リリース日**: 2025年11月17日
<!-- v1.45 -->

![新規](../assets/new.svg) **名前による属性のフィルタリング**- `productSearch` GraphQL クエリで、`names` フィールドでの商品属性のフィルタリングがサポートされるようになりました。<!--DATA-6831--> このフィルターを使用すると、次のことが可能になります。

- 特定の属性のみを要求することで、応答ペイロードのサイズを削減します
- 既存の`roles` フィルターと組み合わせて、表示役割と属性名で絞り込みます
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
>フィルターを適用せずにすべての属性を取得するには、`names`引数を省略するか、空の配列を指定します。

**リリース日**: 2025年11月6日
<!-- v1.44 -->

![&#x200B; パフォーマンスと安定性を向上させるために、システム レベルとインフラストラクチャの改善を](../assets/fix.svg)修正します。<!--DATA-6852, DATA-6864-->

![修正](../assets/fix.svg) グループ化された製品は、親に価格が設定されていない場合にクエリできるようになりました。子製品は、独自の表示役割を返します。<!--DATA-6779-->

![&#x200B; パフォーマンスと安定性を向上させるために、システム レベルとインフラストラクチャの改善を](../assets/fix.svg)修正します。<!--DATA-6721, DATA-6864-->

### 2025年9月

**リリース日**: 2025年9月8日
<!-- v1.42 -->

![新規](../assets/new.svg) **階層価格設定サポート**&#x200B;を追加して、クエリのボリューム価格を確認しました：<!--DATA-6643-->

階層の価格を取得するには：

1. `products` クエリを目的のSKUで使用します
2. **SimpleProductView**&#x200B;の場合、`price.tiers`にアクセスします
3. **ComplexProductView**&#x200B;の場合、`priceRange.minimum.tiers`および`priceRange.maximum.tiers`にアクセスします
4. 各層には、割引された`tier`価格と`quantity`条件が含まれています
5. 数量しきい値を`gte` （以上）および`lt` （以下）で定義します

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

![修正](../assets/fix.svg) **最終価格が最低価格** <!--DATA-6643-->でフィルタリングされました

APIは、割引価格が製品の最終価格の最低価格の&#x200B;**より**&#x200B;低い階層のみを返すようになりました。 最低最終価格がストアフロントに適用されるため、より高い階層は省略されます。

適用対象：

- **シンプルな製品**: `price.tiers`には、`tier.amount.value` &lt; `price.final.amount.value`の階層のみが含まれます（最終版の最小値）。
- **複雑な商品**: `priceRange.minimum.tiers`と`priceRange.maximum.tiers`は、価格帯を作成する際に同じルールを使用します。

**リリース日**: 2025年9月2日
<!-- v1.41 -->

![修正](../assets/fix.svg) **価格データの欠落に対するエラー処理の改善** – 価格データがまだ受信されていない場合、APIはエラーをスローする代わりに価格フィールドに`null`を返します。クライアントは欠落データを適切に処理できます。<!--DATA-6612-->

![&#x200B; パフォーマンスと安定性を向上させるために、システム レベルとインフラストラクチャの改善を](../assets/fix.svg)修正します。<!--DATA-6671-->

### 2025年7月

**リリース日**: 2025年7月30日
<!-- v1.40 -->

![&#x200B; セキュリティ、パフォーマンス、安定性を強化するために、システム レベルとインフラストラクチャの改善を](../assets/fix.svg)修正します。<!--DATA-6619-->

**リリース日**: 2025年7月24日
<!-- v1.39 -->

![新規](../assets/new.svg) **単位IDでレコメンデーションユニットを取得** – 新しいGraphQL エンドポイント `recommendationsByUnitIds`は、より柔軟でターゲットを絞ったアクセスを実現するために、一意のIDでレコメンデーションユニットを取得します。

- `unitIds`が必要です（取得するrecIdのリスト）。
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

![&#x200B; セキュリティ、パフォーマンス、安定性を強化するために、システム レベルとインフラストラクチャの改善を](../assets/fix.svg)修正します。<!--DATA-6316-->

**リリース日**: 2025年7月15日
<!-- v1.38 -->

![新規](../assets/new.svg) **ギフトカード製品タイプ** – カタログのストアフロントサービスで、商品属性をJSON オブジェクトまたは配列としてサポートするようになり、ギフトカードなどの複雑なタイプの柔軟な管理が可能になりました。<!--DATA-6573-->

+++以前のバージョン

### 2025年6月

**リリース日**: 2025年6月20日
<!-- v1.37 -->

![新規](../assets/new.svg) **階層価格表設定** – 親子価格表の正確な価格範囲。 計算では、階層と継承されたルールが尊重され、複数の価格表がリンクされている場合の価格エラーが軽減されます。 Adobe Commerce Optimizerのみ。 [価格表](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/setup/pricebooks)を参照してください。

![新規](../assets/new.svg) **大文字と小文字を区別しないキー** - クエリ内のキー検索では、大文字と小文字が区別されなくなりました。キーの大文字と小文字が区別されなくなりました。<!--DATA-6494, DCAT-2495-->

**リリース日**: 2025年6月20日
<!-- v1.36 -->

![新規](../assets/new.svg) **Catalog Storefront**&#x200B;のパブリック IO イベント – リアルタイム統合と識別可能性（CSSおよびEDS）用のパブリック IO イベントを追加しました。<!--DATA-6329-->

![新規](../assets/new.svg) **サーバーサイドレンダリング （SSR）** – 大規模なカタログでのパフォーマンス、SEO、UXの向上を目的とした、SSRをサポートするアーキテクチャの改善<!--DATA-6278, DATA-6280-->

![新規](../assets/new.svg) **インフラストラクチャとセキュリティ**：新しいAWS ロール、ServiceNow統合、およびイベントサービスのCI/CD パイプライン。

![新規](../assets/new.svg) **イベント形式と識別可能性** – 合理化されたペイロード、監視の強化、バリアントイベントデータの改善<!--DATA-6332, DATA-6402, -->

![&#x200B; セキュリティ、パフォーマンス、安定性を強化するために、システム レベルとインフラストラクチャの改善を](../assets/fix.svg)修正します。<!--DATA-6404, DATA-6410, -->

**リリース日**: 2025年6月13日
<!-- v1.35 -->

![新規](../assets/new.svg) **キャッシュされていないデータを取得** – キャッシュされていないデータをカタログ エンドポイントから検索サービスに渡すために`Magento-Is-Preview` ヘッダーを有効にします。<!--DATA-6345-->

![新規](../assets/new.svg) **複数選択の商品オプション**-GraphQL APIで、商品オプションで複数の選択が許可されているかどうかが表示されるようになりました（例：バンドルの「複数選択」など）。<!--DATA-6487-->

![新規](../assets/new.svg) データ取り込みの価格検証を更新して、価格なしで製品をサポートしました。<!--DATA-6098-->

![修正](../assets/fix.svg) Adobe Commerce Optimizerのシンプルなバンドル価格のエラー処理を改善しました。<!--DATA-6541-->

![&#x200B; セキュリティ、パフォーマンス、安定性を強化するために、システム レベルとインフラストラクチャの改善を](../assets/fix.svg)修正します。<!--DATA-6273, DATA-6485, -->

### 2025年4月

**リリース日**: 2025年4月8日
<!-- v1.34 -->

![&#x200B; セキュリティ、パフォーマンス、安定性を強化するために、システム レベルとインフラストラクチャの改善を](../assets/fix.svg)修正します。<!--DATA-5732-->

<!-- v1.33 -->
![Fix](../assets/fix.svg) インフラストラクチャは、既存のワークロードに影響を与えることなく、非常に大きなカタログ（最大4億4,000万SKU）をサポートするようになりました。

### 2025年3月

**リリース日**: 2025年3月28日
<!-- v1.32 -->

役割のない![修正](../assets/fix.svg)属性は、コンポーザブルカタログのデフォルトでインデックス作成されなくなり、インデックス作成時間が短縮され、ストレージが削減されました。 従来の動作は、機能フラグを使用して再度有効にできます。

![&#x200B; セキュリティ、パフォーマンス、安定性を強化するために、システム レベルとインフラストラクチャの改善を](../assets/fix.svg)修正します。


### 2025年2月

**リリース日**: 2025年2月18日
<!-- v1.31 -->

![&#x200B; セキュリティ、パフォーマンス、安定性を強化するために、システム レベルとインフラストラクチャの改善を](../assets/fix.svg)修正します。<!--DATA-6389, DATA-6367, DATA-6373-->

### 2024年12月

**リリース日**: 2024年12月9日
<!-- v1.30 -->

メジャーリリース：ヘッドレスストアフロント、ヘッダー管理、製品データ処理用の[構成可能なカタログデータモデル &#x200B;](https://developer.adobe.com/commerce/services/optimizer/)。

![新規](../assets/new.svg) **コンポーザブルカタログデータモデル（CCDM）**：ヘッドレスストアフロントにコンポーザブルカタログを使用する顧客をサポートします。 新しいエンドポイントでは、カタログビューとポリシーID （後方互換性）を使用できます。 組み込みのページネーションを使用した設定可能な製品の詳細と価格。<!--DATA-6018, DATA-6288-->

![新規](../assets/new.svg) **ヘッダー管理**-`AC-Locale`の名前が、コンポーザブルカタログ API操作の`AC-Scope-Locale`に変更されました。ヘッダーマッピングとデフォルト値が指定されました。<!--DATA-6303, DATA-6078-->

![新規](../assets/new.svg) **製品データと価格設定** – 構成可能なカタログデータモデルのサポートと、構成可能な製品の価格処理の改善<!--DATA-6279-->

`CurrencyEnum`が更新され、製品検索クエリの`NONE`をサポートするようになり、フェデレーションロジックと一致しました。<!--DATA-6285-->

![修正](../assets/fix.svg) **インフラストラクチャとアップグレード** - セキュリティ、パフォーマンス、安定性を向上させるシステムレベルの改善。

![修正](../assets/fix.svg) バンドル製品オプションに、有効な製品のみが表示されるようになりました。<!--DATA-6347-->

**リリース日**: 2024年12月9日
<!-- v1.29 -->

![新規](../assets/new.svg) **商品クエリでの画像順序** - GraphQL `images` フィールドの商品画像が、一貫したストアフロントとAPI動作のためにカタログの書き出し`sortOrder`に従うようになりました。<!--DATA-6258-->

![&#x200B; セキュリティ、パフォーマンス、安定性を強化するために、システム レベルとインフラストラクチャの改善を](../assets/fix.svg)修正します。<!--DATA-6619-->

**リリース日**: 2024年12月
<!-- v1.28 -->

![&#x200B; セキュリティ、パフォーマンス、安定性を強化するために、システム レベルとインフラストラクチャの改善を](../assets/fix.svg)修正します。


### 2024年10月

**リリース日**: 2024年10月22日
<!-- v1.26 -->

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) GraphQL スキーマには、正確なサイトマップと検索エンジンのインデックス再作成（Googleなど）のために、商品情報に`lastModifiedAt`が含まれるようになりました。


### 2024年9月

**リリース日**: 2024年9月26日
<!-- v1.27 -->

![&#x200B; セキュリティ、パフォーマンス、安定性を強化するために、システム レベルとインフラストラクチャの改善を](../assets/fix.svg)修正します。


### 2024年8月

**リリース日**: 2024年8月22日
<!-- v1.23 -->

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg)製品情報は、製品の上書き（価格）データなしで取得できるようになりました。 以前は、次のクエリが返されていました。 

**リリース日**: 2024年8月13日
<!-- v1.22 -->

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)製品SKUですべてのバリエーションを取得するためのサポートを追加しました。 [&#x200B; カタログサービス API リファレンス &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)を参照してください。

### 2024年5月

**リリース日**: 2024年5月23日
<!-- v1.19 -->

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降


![修正](../assets/fix.svg) オプション値の`InStock` フラグが、製品バリアントのスコープ `enabled` ステータスを尊重するようになりました。

<!--DATA-5033-->

![修正](../assets/fix.svg)最大16桁と小数点以下桁の製品価格のサポートを追加しました。 [&#x200B; データ管理ダッシュボード &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)または[CLI](../data-export/data-export-cli-commands.md)から再同期して、更新を適用します。

#### 既知の制限事項

次の機能はまだサポートされていません。

- 動的属性ペイロードの最大サイズは9 MBです。
- グループ製品価格は、シンプルな製品価格で計算できます。
- 画像配列内では、最初の画像にのみ役割が含まれます。

API MeshとCore GraphQL APIを使用して、次のことを行います。

- 最低広告価格
- 階層の価格
- 固定価格のバンドル商品

詳細と例については、[&#x200B; カタログサービスとAPI メッシュ &#x200B;](mesh.md)を参照してください。

### 2024年4月

**リリース日**: 2024年4月11日
<!-- v1.18 -->

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) PHP 8.3のサポートを追加しました。

![新規](../assets/new.svg) [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/)および[`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) クエリでは、シンプルな製品と複雑な製品の両方に対して、カスタマイズ可能なオプション データが返されるようになりました。<!--DATA-5538-->

### 2024年2月

**リリース日**: 2024年2月22日
<!-- v1.17 -->

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html?lang=ja)は、データストリーム（商品レコメンデーション、ライブサーチ、カタログサービス）で利用できるようになりました。 `catalog-service` メタパッケージ v3.1.0以降が必要です。

**リリース日**: 2024年2月13日
<!-- v1.16 -->

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)製品ビデオがカタログサービス APIでサポートされるようになりました。![修正](../assets/fix.svg)在庫切れオプションがPDP ウィジェットに表示されるようになりました。

#### 既知の制限事項

これらの機能はまだサポートされていません。

- 動的属性ペイロードの最大サイズは9 MBです。
- グループ商品価格。 この値はシンプルな商品価格で計算できます。
- 画像配列内では、最初の画像にのみ役割が含まれます。

API MeshとCore GraphQL APIを使用して、次のことを行います。

- 最低広告価格
- [階層の価格](mesh.md)

### 2023年10月

**リリース日**: 2023年10月12日
<!-- v1.13 -->

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) カタログサービスは、製品バリエーションの`inStock` フラグをサポートしています。![新規](../assets/new.svg) `urlKey`および`externalId` フィールドがGraphQL スキーマに追加されました。![新規](../assets/new.svg) ダウンロード可能な製品とギフトカードがサポートされるようになりました。

### 2023年9月

**リリース日**: 2023年9月19日
<!-- v1.12 -->

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![New](../assets/new.svg) Catalog Serviceで[SaaS価格インデックス &#x200B;](../price-index/price-indexing.md)が使用されるようになりました。![修正](../assets/fix.svg)このリリースには、サービス側のバグ修正と機能強化が含まれています。

### 2023年7月

**リリース日**: 2023年7月18日
<!-- v1.11 -->

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![New](../assets/new.svg) Catalog Serviceで、商品レコメンデーション用の[`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) GraphQL クエリがサポートされるようになりました。

### 2023年6月

**リリース日**: 2023年6月27日（PT）
<!-- v1.10 -->

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) カタログサービス APIで`related products`がサポートされるようになりました。

### 2023年4月

**リリース日**: 2023年4月12日
<!-- v1.7 -->

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) カタログサービスで、削除された製品バリエーションをクリーンアップできるようになりました。![修正](../assets/fix.svg) インフラストラクチャのスケーラビリティとパフォーマンスの改善。

### 2023年3月

**リリース日**: 2023年3月28日（PT）
<!-- v1.6 -->

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) クエリにスウォッチを追加しました。![新規](../assets/new.svg) [API Mesh](mesh.md)を使用して`entityId`を取得する機能を追加しました。

**リリース日**: 2023年3月6日（PT）
<!-- v1.5 -->

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)さんが[`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/)個のGraphQL機能を追加しました。![修正](../assets/fix.svg) パフォーマンスとAPIのスケーラビリティが向上しました。

### 2023年2月

**リリース日**: 2023年2月7日
<!-- v1.4 -->

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg)公開されたカタログサービスメタパッケージは、インストール手順を簡素化します。![APIのスケーラビリティとパフォーマンスの改善を修正](../assets/fix.svg)。

### 「Generative AI tool deployment - internal study

**リリース日**: 2023年1月17日（PT）
<!-- v1.3 -->

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg) オンボーディング体験を簡略化および改善しました。![新規](../assets/new.svg)新しい顧客サンドボックスエンドポイントを実稼動前テストで使用できます。![新しい](../assets/new.svg)仮想プロダクトのサポートが追加されました。![APIのスケーラビリティとパフォーマンスの改善を修正](../assets/fix.svg)。

### 2022年11月

**リリース日**: 2022年11月18日
<!-- v1.1 -->

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg) カタログサービスで、Adobeの[API メッシュ &#x200B;](https://developer.adobe.com/graphql-mesh-gateway/)がサポートされるようになりました。![修正](../assets/fix.svg) APIのスケーラビリティと全体的なパフォーマンスが向上しました。

### 2022年10月

**リリース日**: 2022年10月4日
<!-- v1.0 -->

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新しい](../assets/new.svg) バンドルおよびグループ化された製品のサポート。![新規](../assets/new.svg)さんがB2B表示の上書きを追加しました。 製品は検索可能になり、特定の顧客グループのカートに追加できます。![修正](../assets/fix.svg) サービスは安定し、パフォーマンスが向上しました。

### 2022年9月

**リリース日**: 2022年9月12日
<!-- v0.3 -->

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg) バリアント画像：選択したオプションに基づいて返される製品画像。![新規](../assets/new.svg)価格役割：特定の顧客グループのメンバーのみが製品価格を表示できます。![修正](../assets/fix.svg) サービスの安定性とパフォーマンスが向上しました。![新規](../assets/new.svg)製品がカタログから削除されると、更新が受信されます。

### 2022年8月

**リリース日**: 2022年8月9日
<!-- Beta -->

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.x以降

![新規](../assets/new.svg) `products`および`refineProduct` クエリでは、次のデータが返されます。

- 定義済み（システム）製品属性。
- 動的な製品属性を作成し、役割（製品表示ページ/製品リストページ）ごとにフィルタリングできます。
- 商品オプション：
- 製品画像を役割（PDP/PLP）別にフィルタリングできます。
- シンプルな商品の具体的な価格と、設定可能な商品の価格帯。
- 顧客グループの価格と価格帯。 顧客グループを持たない買い物客には、デフォルトのフォールバックプライスが返されます。
- B2B顧客向けの価格設定を使用する製品タイプ。

+++

## カタログサービスメタパッケージ

カタログサービス PHP メタパッケージ （`magento/catalog-service`）を更新しました。

- Adobe Commerce as a Cloud Serviceのお客様の場合、最新バージョンが環境にインストールされます。

- クラウド上またはオンプレミスのAdobe Commerceの場合、Adobeでは、最新リリースのカタログサービスメタパッケージをクラウド環境でアップグレードするためにComposerを使用することをお勧めします。

### v3.5.0 リリース

**リリース日**: 2026年7月10日

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) **ステージング済みカテゴリ URL キー同期** - カタログサービス メタパッケージの依存関係を更新して、カタログステージング データ エクスポーターモジュール （`magento/module-catalog-staging-data-exporter`）を含めました。 このモジュールは、ステージングされたカテゴリ `url_key`の変更が適用されたときに製品フィードを再書き出しするので、ステージングされたカタログの変更はSaaS カタログ （カタログサービス、ライブサーチ、製品レコメンデーション）に正しく反映されます。

![新規](../assets/new.svg) カタログサービスとCommerce スタックの互換性を維持するために、依存関係を更新しました。

### v3.4.0 リリース

**リリース日**: 2026年6月8日

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) **データフィード同期ステータスの監視のサポート** - データエクスポーターステータス拡張機能（`magento/module-data-exporter-status`）を含めるようにカタログサービス メタパッケージ依存関係を更新しました。 これにより、追加のインストールや設定手順を必要とせずに、Commerce管理者から[&#x200B; データフィード同期ステータスのモニタリング &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)が有効になります

![新規](../assets/new.svg) カタログサービスとCommerce スタックの互換性を維持するために、依存関係を更新しました。

### v3.3.0 リリース

**リリース日**: 2025年10月14日

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) **データサービスのアップグレード**—`magento/data-services`依存関係が^8.0.0に更新されました。 アップグレードする前に、環境とカスタム Data Services APIの使用状況を8.x互換性で確認してください。

![新規](../assets/new.svg) 3.3.0 リリースのバージョンとメタデータが更新されました。

### v3.2.0 リリース

**リリース日**: 2024年4月12日

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) バージョンとメタデータが3.2.0に更新されました。 その他の依存関係は変更されません。

### v3.1.0 リリース

**リリース日**: 2024年1月26日

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)新しいパッケージの依存関係を追加しました：

- カタログ サービスで使用されるカテゴリ権限データを書き出すための&#x200B;**カテゴリ権限データ エクスポーター** （`magento/module-category-permission-data-exporter`）。
- 管理者UIとカタログ同期に関連する設定の&#x200B;**カタログ同期管理者** `magento/module-catalog-sync-admin`です。

![新規](../assets/new.svg) 3.1.0 リリースのバージョンとメタデータが更新されました。

## カタログサービスインストーラー

インストーラーはカタログサービス拡張機能で配信され、カタログサービスがCommerce スタックと一致するように、インストールと環境チェックを処理します。

- **Adobe Commerce as a Cloud Service**&#x200B;のお客様の場合、最新のインストーラーのバージョンが環境にインストールされます。

- **クラウド インフラストラクチャ上のAdobe Commerce**&#x200B;または&#x200B;**オンプレミス**&#x200B;の場合、インストーラーを[Catalog Service メタパッケージ &#x200B;](#catalog-service-metapackage)に合わせます。

Composerを使用して`magento/catalog-service`をアップグレードすると、インストーラーパッケージが自動的に最新バージョンに更新されます。 これらのリリースノートで必要な変更（新しいPHP バージョンのサポートなど）が記述されている場合は、Composerを使用して`magento/catalog-service-installer`を個別にアップグレードすることもできます。 これにより、インストールツールは、実行するカタログサービスバージョンとの互換性を維持できます。

### v1.0.6 リリース

**リリース日**: 2026年3月25日

![新規](../assets/new.svg) **PHP 8.5** - カタログサービスがPHP 8.5で動作する場合に互換性を確保します。

## 関連ドキュメント

- クラウド、オンプレミス、またはAdobe Commerce as a Cloud Service上の**Adobe Commerceにデプロイされたプロジェクトについては、次のドキュメントを参照してください。

   - [カタログサービスガイド](overview.md)
   - [カタログサービス GraphQL API リファレンス](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)
   - [Adobe Commerce管理ガイド](https://experienceleague.adobe.com/en/docs/commerce-admin/)
   - [Adobe Commerce as a Cloud Service ガイド](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/)
   - [Adobe Commerce Cloud版ガイド](https://experienceleague.adobe.com/en/docs/commerce-cloud/)

- **Adobe Commerce Optimizer**&#x200B;または&#x200B;**Adobe Commerce Optimizer Connector**&#x200B;を使用しているプロジェクトについては、次のドキュメントを参照してください。

   - [マーチャンダイジングサービス開発者ガイド](https://developer.adobe.com/commerce/services/optimizer/)
   - [マーチャンダイジング GraphQL API リファレンス](https://developer.adobe.com/commerce/services/reference/graphql/)
   - [Adobe Commerce Optimizer ガイド](../optimizer/overview.md)
