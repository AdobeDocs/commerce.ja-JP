---
title: オンボーディング
description: ' [!DNL Product Recommendations]の要件とサポートされているプラットフォームについて説明します。'
exl-id: 7b8a1117-b6d5-4e5d-bb97-09f76a024cbd
source-git-commit: 8f421bd4421b9599ad52aa68c5caaee6592ccb43
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# オンボーディング

>[!IMPORTANT]
>
>**製品レコメンデーションはHIPAA対応サービスではありません。** HIPAA対応の製品を使用するか、保護された健康情報（PHI）を処理するAdobe Commerceの実装では、製品レコメンデーションを有効にしたり、使用したりしないでください。 商品レコメンデーションは、現在HIPAA非対応として分類されているCommerce SaaS サービスの一部です。
>
>どのAdobe Commerce機能がHIPAAに対応しているか、どのサービスをPHIで使用してはならないかについて詳しくは、[Adobe CommerceでのHIPAA対応](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/overview)および[操作](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/operations#adobe-commerce-services)を参照してください。

[!DNL Product Recommendations]のオンボーディングプロセスでは、サーバーのコマンドラインへのアクセスが必要で、次の手順で構成されています。 コマンドラインでの作業に慣れていない場合は、開発者またはシステムインテグレータに助けを求めてください。

- [導入ワークフロー](implementation-workflow.md)
- [インストールと設定](install-configure.md)
- [設定](settings.md)
- [検証](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/)
- [ステージング環境](staging-environment.md)

## 要件定義

- Adobe Commerce 2.4.4以降
- PHP 8.1、8.2、8.3、または8.4
- コンポーザー2

### サポートされているプラットフォーム

- Adobe Commerce オンプレミス（EE） : 2.4.4以降
- Adobe Commerce クラウド版（ECE） : 2.4.4以降

## エンドポイント

[!DNL Product Recommendations]は`https://catalog-service.adobe.io/graphql`のエンドポイントを通じて通信します。

### ページビルダーのサポート

[!DNL Product Recommendations]は、ページビルダーのコンテンツタイプとしてページに追加できます。 ページビルダーのサポートを製品レコメンデーションに追加するには、[ インストールと設定](install-configure.md)を参照してください。

[[!DNL Page Builder] を](page-builder.md) コンテンツに追加する方法については、[!DNL Product Recommendations]統合[!DNL Page Builder]を参照してください。

### SaaS価格インデックス

商品レコメンデーションのお客様は[SaaS価格インデックス ](../price-index/price-indexing.md)を使用できます。これにより、価格の更新と同期時間を迅速に行うことができます。

### B2B サポート {#b2bsupport}

B2Bのストアフロントでは、買い物客や顧客グループごとに商品の可視性や価格を決定する複雑なロジックが必要になることがよくあります。 [!DNL Product Recommendations]様は、[ カテゴリの権限](release-notes.md)、[共有カタログ ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/category-permissions.html)、[顧客グループ固有の価格](https://experienceleague.adobe.com/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html)を尊重することで、この機能を[ サポート ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html)するようになりました。 たとえば、特定のカテゴリーを小売顧客セグメントから隠している場合、そのセグメントの買い物客には、それらのカテゴリーの商品に関するレコメンデーションは表示されません。 また、特定の顧客グループや企業向けに共有カタログを定義すると、それらの買い物客は、アクセス可能な商品に関してのみレコメンデーションを見ることができます。 あらゆる推奨商品には、各買い物客の顧客グループに基づいた、正しい顧客グループ固有の価格が反映されています。

>[!NOTE]
>
>販売者は、[ カタログサービス ](../catalog-service/overview.md) Storefront APIを使用して、ウィジェットまたはストアフロント要素をカスタマイズおよび拡張できますが、Adobe サポートチームでは、カスタマイズは対象外です。
