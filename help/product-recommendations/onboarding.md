---
title: 使用開始
description: 要件とサポートされているプラットフォームについては、以下を参照してください [!DNL Product Recommendations]。
exl-id: 7b8a1117-b6d5-4e5d-bb97-09f76a024cbd
badgePaas: label="PaaS のみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeが管理する PaaS インフラストラクチャ）およびオンプレミスプロジェクトにのみ適用されます。"
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# オンボーディング

[!DNL Product Recommendations] のオンボーディングプロセスでは、サーバーのコマンドラインにアクセスする必要があります。このプロセスは次の手順で構成されます。 コマンドラインからの操作に詳しくない場合は、開発者またはシステムインテグレーターにお問い合わせください。

- [実装ワークフロー](implementation-workflow.md)
- [インストールと設定](install-configure.md)
- [設定](settings.md)
- [確かめる](verify.md)
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

[!DNL Product Recommendations] は、ページ Builder コンテンツタイプとしてページに追加できます。 製品Recommendationsにページビルダーのサポートを追加するには、 [インストールと設定](install-configure.md)を参照してください。

コンテンツに [!DNL Product Recommendations] ータを追加する方法については、[[!DNL Page Builder]  統合 ](page-builder.md) を参照 [!DNL Page Builder] てください。

### SaaS 価格インデックス作成

製品レコメンデーションのお客様は、[SaaS 価格インデックス作成 ](../price-index/price-indexing.md) を使用できます。これにより、価格の変更の更新と同期化時間が短縮されます。

### B2B サポート {#b2bsupport}

B2B ストアフロントには、多くの場合、買い物客または顧客グループごとに製品の可視性と価格を指示する複雑なロジックが必要です。 [ カテゴリ権限 ](release-notes.md)、[ 共有カタログ ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/category-permissions.html)、および [ 顧客グループ固有の価格 ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) を考慮して、この機能を [ サポート ](https://experienceleague.adobe.com/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html) するように設 [!DNL Product Recommendations] しました。 例えば、小売顧客セグメントから特定のカテゴリを非表示にした場合、そのセグメントの買い物客には、それらのカテゴリの製品のレコメンデーションは表示されません。 また、特定の顧客グループや会社用に共有カタログを定義すると、買い物客は、アクセスできる製品に関するレコメンデーションのみが表示されます。 すべての推奨製品は、各買い物客の顧客グループに基づいて、正しい顧客グループ固有の価格を反映しています。

>[!NOTE]
>
>マーチャントは、 [カタログサービス](../catalog-service/overview.md) ストアフロントAPIを使用してウィジェットまたはストアフロント要素をカスタマイズおよび拡張できますが、カスタマイズはAdobe Systemsのサポートチーム範囲対象外です。
