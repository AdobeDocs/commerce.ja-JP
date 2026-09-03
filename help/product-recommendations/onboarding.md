---
title: オンボーディング
description: ' [!DNL Product Recommendations]の要件とサポートされているプラットフォームについて説明します。'
exl-id: 7b8a1117-b6d5-4e5d-bb97-09f76a024cbd
TQID: https://experienceleague.adobe.com/FLrOFe-Lwe7i3dOwCISflVGEv2MIkXmmE-NqTvpaY-0
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 0802d0e53a1ed6701318647b7bf78435082ad5f3
workflow-type: tm+mt
source-wordcount: 477
ht-degree: 0%

---

# オンボーディング

>[!IMPORTANT]
>
>**製品レコメンデーションはHIPAA対応サービスではありません。** HIPAA対応の製品を使用するAdobe Commerceの実装や、保護された医療情報（PHI）を処理する製品レコメンデーションを有効にしたり、使用したりしないでください。 商品レコメンデーションは、現在HIPAA非対応として分類されているCommerce SaaS サービスの一部です。
>
>どのAdobe Commerce機能がHIPAAに対応しているか、どのサービスをPHIで使用してはならないかについて詳しくは、[Adobe CommerceでのHIPAA対応](https://experienceleague.adobe.com/ja/docs/commerce-admin/start/compliance/hipaa-ready-service/overview)および[操作](https://experienceleague.adobe.com/ja/docs/commerce-admin/start/compliance/hipaa-ready-service/operations#adobe-commerce-services)を参照してください。

[!DNL Product Recommendations]のオンボーディングプロセスでは、サーバーのコマンドラインへのアクセスが必要で、次の手順で構成されています。 コマンドラインでの作業に慣れていない場合は、開発者またはシステムインテグレーターにヘルプを依頼してください。

- [導入ワークフロー](implementation-workflow.md)
- [インストールと設定](install-configure.md)
- [設定](settings.md)
- [検証](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify)
- [ステージング環境](staging-environment.md)

## 要件定義

[Adobe Commerce](https://business.adobe.com/jp/products/magento/magento-commerce.html) 2.4.4以降。 詳しくは、[必要システム構成](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/system-requirements){target="_blank"}を参照してください。

### サポートされているプラットフォーム

- Adobe Commerce オンプレミス（EE） : 2.4.4以降
- Adobe Commerce クラウド版（ECE） : 2.4.4以降

要件の詳細については、[必要システム構成](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/system-requirements)を参照してください。

## エンドポイント

[!DNL Product Recommendations]は`https://catalog-service.adobe.io/graphql`のエンドポイントを通じて通信します。

### ページビルダーのサポート

[!DNL Product Recommendations]は、ページビルダーのコンテンツタイプとしてページに追加できます。 ページビルダーのサポートを製品レコメンデーションに追加するには、[&#x200B; インストールと設定](install-configure.md)を参照してください。

[!DNL Product Recommendations]を[!DNL Page Builder] コンテンツに追加する方法については、[[!DNL Page Builder] 統合](page-builder.md)を参照してください。

### Fastlyの画像の最適化

[!DNL Product Recommendations]は、Fastly画像最適化パラメーターを[!DNL Product Recommendations]画像URLに適用するオプションの[Fastly画像最適化](install-configure.md#fastlysupport) モジュールをサポートしています。 このサポートを追加するには、[&#x200B; インストールと設定](install-configure.md#fastlysupport)を参照してください。

### SaaS価格インデックス

商品レコメンデーションのお客様は[SaaS価格インデックス &#x200B;](../price-index/price-indexing.md)を使用できます。これにより、価格の更新と同期時間を迅速に行うことができます。

### B2B サポート {#b2bsupport}

B2Bのストアフロントでは、買い物客や顧客グループごとに商品の可視性や価格を決定する複雑なロジックが必要になることがよくあります。 [!DNL Product Recommendations]様は、[&#x200B; カテゴリの権限](https://experienceleague.adobe.com/ja/docs/commerce-admin/catalog/categories/category-permissions)、[共有カタログ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/b2b/shared-catalogs/catalog-shared)、[顧客グループ固有の価格](https://experienceleague.adobe.com/ja/docs/commerce-admin/catalog/products/pricing/pricing-advanced)を尊重することで、この機能を[&#x200B; サポート &#x200B;](release-notes.md)するようになりました。 たとえば、特定のカテゴリーを小売顧客セグメントから隠している場合、そのセグメントの買い物客には、そのカテゴリーの商品のレコメンデーションは表示されません。 また、特定の顧客グループや企業向けに共有カタログを定義すると、それらの買い物客は、アクセス可能な商品に関してのみレコメンデーションを見ることができます。 あらゆる推奨商品には、各買い物客の顧客グループに基づいた、適切な顧客グループ固有の価格が反映されています。

>[!NOTE]
>
>販売者は、[&#x200B; カタログサービス &#x200B;](../catalog-service/overview.md) Storefront APIを使用して、ウィジェットまたはストアフロント要素をカスタマイズおよび拡張できますが、Adobe サポートチームでは、カスタマイズは対象外です。
