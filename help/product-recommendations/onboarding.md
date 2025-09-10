---
title: オンボーディング
description: ' [!DNL Product Recommendations] の要件とサポートされるプラットフォームについて説明します。'
exl-id: 7b8a1117-b6d5-4e5d-bb97-09f76a024cbd
source-git-commit: 3821893c3df01e2e36ab0142616e52c1c92b4d51
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# オンボーディング

[!DNL Product Recommendations] のオンボーディングプロセスでは、サーバーのコマンドラインにアクセスする必要があります。このプロセスは次の手順で構成されます。 コマンドラインからの操作に詳しくない場合は、開発者またはシステムインテグレーターにお問い合わせください。

- [実装ワークフロー](implementation-workflow.md)
- [インストールと設定](install-configure.md)
- [設定](settings.md)
- [ 検証 ](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/)
- [ステージング環境](staging-environment.md)

## 要件

- Adobe Commerce 2.4.4 以降
- PHP 8.1, 8.2
- コンポーザー 2

### サポートされるプラットフォーム

- Adobe Commerce オンプレミス（EE） :2.4.4 以降
- クラウド上のAdobe Commerce（ECE） :2.4.4 以降

## エンドポイント

[!DNL Product Recommendations] は、`https://catalog-service.adobe.io/graphql` のエンドポイントを介して通信します。

### ページビルダーのサポート

ページビル [!DNL Product Recommendations] ーコンテンツタイプとしてページに追加できます。 Product Recommendations にページビルダーのサポートを追加するには、[ インストールと設定 ](install-configure.md) を参照してください。

コンテンツに [[!DNL Page Builder]  ータを追加する方法については、](page-builder.md) 統合 [!DNL Product Recommendations] を参照 [!DNL Page Builder] てください。

### SaaS 価格インデックス作成

製品レコメンデーションのお客様は、[SaaS 価格インデックス作成 ](../price-index/price-indexing.md) を使用できます。これにより、価格の変更の更新と同期化時間が短縮されます。

### B2B サポート {#b2bsupport}

B2B ストアフロントには、多くの場合、買い物客または顧客グループごとに製品の可視性と価格を指示する複雑なロジックが必要です。 [!DNL Product Recommendations] カテゴリ権限 [、](release-notes.md) 共有カタログ [、および ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/category-permissions.html) 顧客グループ固有の価格 [ を考慮して、この機能を ](https://experienceleague.adobe.com/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html) サポート [ するように設 ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) しました。 例えば、小売顧客セグメントから特定のカテゴリを非表示にした場合、そのセグメントの買い物客には、それらのカテゴリの製品のレコメンデーションは表示されません。 また、特定の顧客グループや会社用に共有カタログを定義すると、買い物客は、アクセスできる製品に関するレコメンデーションのみが表示されます。 すべての推奨製品は、各買い物客の顧客グループに基づいて、正しい顧客グループ固有の価格を反映しています。

>[!NOTE]
>
>マーチャントは、[Catalog Service](../catalog-service/overview.md) Storefront API を使用して、ウィジェットやストアフロント要素をカスタマイズおよび拡張できますが、カスタマイズはAdobe サポートチームの範囲外です。
