---
title: 実装アーキテクチャオプション
description: Commerce Foundation、Adobe Commerce as a Cloud Service、Optimizer Connector、スタンドアロンのOptimizerなどのAdobe Commerceアーキテクチャを比較します。
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:39:51.406Z'
TQID: 'https://experienceleague.adobe.com/tYkxRAfJWOY7C0OEqYxEb4onwvnnL9wEofEG2e6qnKA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: ef0c45ae-6bee-4821-a65e-e1e118e8a01c
    internal-label: Commerce Optimizer
feature_v2:
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: 8dc0e58b-adf0-51bb-8db5-bb36e3e656fb
    internal-label: Inventory
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%
---

# 実装アーキテクチャオプション

Adobe Commerceの導入アーキテクチャは、コマースバックエンド（[!DNL Adobe Commerce]または[!DNL Adobe Commerce Optimizer]）、ストアフロント、接続されたサービスと統合のセットという3つのレイヤーを組み合わせています。 次のオプションを比較して、各アーキテクチャ内のどのシステムがカタログ、価格設定、カート、チェックアウト、注文、顧客取引を所有しているかを特定します。

## アーキテクチャオプションの概要

トランザクションの所有権とストアフロントのエクスペリエンスごとにオプションを比較します。

### Commerceのプラットフォームとトランザクション

| オプション | 記録システム | トランザクションパス | 最適なフィット |
| --- | --- | --- | --- |
| **[!DNL Adobe Commerce as a Cloud Service]（Commerce Foundation**） | AdobeのCommerce Foundation | Managed Commerce FoundationとコネクテッドCommerceサービス | Adobeを利用して、SaaS （Software as a Service）を実現し、インフラストラクチャの所有権を低減したいCommerce |
| [!DNL Adobe Commerce Optimizer Connector]**を持つクラウドまたはオンプレミスの**[!DNL Adobe Commerce] | 既存のCommerce Foundation, for Commerce データとトランザクション | 既存のCommerce Foundation APIと接続されたトランザクションサービス | 既存の[!DNL Adobe Commerce]展開にOptimizerの検出およびマーチャンダイジング機能を追加したいお客様 |
| **外部コマースバックエンドを持つスタンドアロン [!DNL Adobe Commerce Optimizer]** | 既存またはサードパーティのコマースプラットフォーム： 外部ソースからOptimizerにカタログと価格データが追加される | API Mesh、App Builder、ダイレクト統合を利用して、ストアフロントとサードパーティのカート、チェックアウト、顧客、注文、支払い、税務、配送、フルフィルメントサービスを連携できます | 既存またはサードパーティのトランザクションコマースプラットフォームを維持しながら、Optimizerの機能を必要とするお客様 |
| Commerce Foundation **を使用したクラウドまたはオンプレミスの**[!DNL Adobe Commerce] | Commerce財団 | Commerce Foundation APIと、支払い、税務、配送、在庫、フルフィルメントの統合機能を構成 | クラウドまたはオンプレミスのインフラストラクチャをデプロイメント制御できる完全な[!DNL Adobe Commerce] プラットフォームを必要とするお客様 |

### ストアフロント体験

ストアフロントは、Commerce Foundation API、ストアフロントサービス（[!DNL Catalog Service]、[!DNL Live Search]および[!DNL Product Recommendations]）、または[!DNL Adobe Commerce Optimizer] マーチャンダイジングサービスに接続します。

| オプション | ストアフロント体験 | ストアフロントのデータパス |
| --- | --- | --- |
| **[!DNL Adobe Commerce as a Cloud Service]（Commerce Foundation**） | Edge Delivery Servicesまたはその他のサポートされているヘッドレス体験を活用したCommerce Storefront | ストアフロントサービスに加えて、コアプラットフォームデータ用のCommerce Foundation API |
| [!DNL Adobe Commerce Optimizer Connector]**を持つクラウドまたはオンプレミスの**[!DNL Adobe Commerce] | Edge Delivery ServicesまたはOptimizer エクスペリエンスを使用したカスタムヘッドレスストアフロント | Commerce Optimizer Merchandising Services GraphQL API （Optimizerで管理されるカタログとマーチャンダイジングデータ用） |
| **外部コマースバックエンドを持つスタンドアロン [!DNL Adobe Commerce Optimizer]** | Edge Delivery Servicesまたはカスタムのヘッドレスストアフロントを活用したCommerce Storefront | Commerce Optimizer Merchandising Services カタログおよびマーチャンダイジングデータ用のGraphQL API |
| Commerce Foundation **を使用したクラウドまたはオンプレミスの**[!DNL Adobe Commerce] | Edge Delivery Services、Luma、PWA、またはカスタムヘッドレスストアフロント | Commerce Foundation APIと、設定済みのStorefront サービス |

## Adobe Commerce as a Cloud Service

![管理対象のCommerce FoundationおよびStorefront ServicesがCommerce StorefrontにフィードするAdobe Commerce as a Cloud Serviceのアーキテクチャ図](../assets/architecture/commerce-cloud-service-storefront-services-arch.drawio.png){width="600" zoomable="yes"}

**主な境界** - AdobeがCommerce Foundation プラットフォームを管理します。 アーキテクチャは、ストアフロント エクスペリエンスに[!DNL Catalog Service]、[!DNL Live Search]、[!DNL Product Recommendations]などのストアフロントサービスを使用します。 AEM Assetsによる[!DNL Product Visuals]は、オプションのSaaS統合です。 Commerce](../aem-assets/aem-assets-integration.md)の[AEM Assetsとの連携を参照してください。

**参照：**

- [[!DNL Adobe Commerce as a Cloud Service] の概要](/help/cloud-service/overview.md)
- [Commerce ストアフロント](https://experienceleague.adobe.com/en/tools/commerce-storefront/)
- [Storefront Services GraphQL スキーマ](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)

## Adobe CommerceとCommerce Foundation

![Adobe Commerce オンクラウドまたはオンプレミスと、Storefront ServicesおよびCommerce Foundation APIによるCommerce Storefrontのフィードのアーキテクチャ図](../assets/architecture/commerce-paas-storefront-services-arch.drawio.png){width="600" zoomable="yes"}

**主な境界**:Commerce FoundationがCommerce プラットフォームとトランザクションフローを所有します。 [!DNL Catalog Service]、[!DNL Live Search]および[!DNL Product Recommendations]は、設定時に、カタログ、検索、およびレコメンデーションに最適化されたストアフロント アクセスを提供します。 AEM Assetsとの連携はオプションです。 Commerce](../aem-assets/aem-assets-integration.md)の[AEM Assetsとの連携を参照してください。

**参照：**

- [Commerce ストアフロント](https://experienceleague.adobe.com/en/tools/commerce-storefront/)
- [COMMERCE GRAPHQL API](https://developer.adobe.com/commerce/webapi/graphql/)
- [Storefront Services GraphQL スキーマ](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)


## Adobe CommerceとOptimizer コネクタ

![Adobe Commerce Optimizer Connectorのアーキテクチャ図は、カタログと価格データをAdobe CommerceからAdobe Commerce Optimizerに同期し、Merchandising Services APIを介してCommerce Storefrontに送っています](../assets/architecture/adobe-commerce-optimizer-architecture.drawio.png){width="600" zoomable="yes"}

**キー境界** - コネクタは、[!DNL Adobe Commerce]から[!DNL Adobe Commerce Optimizer]までのカタログと価格データを同期します。 [!DNL Adobe Commerce]は引き続きトランザクションシステムであり、OptimizerはMerchandising Services APIを通じて検出およびマーチャンダイジング体験を提供します。

**参照：**

- [Commerce Optimizerとの連携](/help/optimizer/integrations/integrations-overview.md)
- [Commerce Optimizer Merchandising Services](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/)
- [COMMERCE GRAPHQL API](https://developer.adobe.com/commerce/webapi/graphql/)
- [Commerce ストアフロント](https://experienceleague.adobe.com/en/tools/commerce-storefront/)

## サードパーティバックエンドを備えたスタンドアロンのCommerce Optimizer

![お客様が所有するソースシステムのアーキテクチャ図。カタログと価格データをData Ingestionを介してスタンドアロンのAdobe Commerce Optimizerに送信し、サードパーティのコマースバックエンドに接続されたCommerce Storefrontに送り込む](../assets/architecture/adobe-commerce-optimizer-standalone-detailed.drawio.png){width="800" zoomable="yes"}

**主な境界** - スタンドアロン [!DNL Adobe Commerce Optimizer]は、カタログの検索とマーチャンダイジングのエクスペリエンスを所有していますが、トランザクション Commerce バックエンドは所有していません。 カタログと価格データは、Data Ingestion REST APIを使用して入力します。 Edge Delivery Servicesのストアフロントでは、商品エクスペリエンスにGraphQL APIを使用し、カートとチェックアウトの際にサードパーティバックエンドに接続します。

**参照：**

- [Adobe Commerce Optimizerとは？](/help/optimizer/overview.md)
- [Commerce Optimizer Data Ingestion](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)
- [Commerce Optimizer Merchandising Services](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/)
- [Commerce ストアフロント](https://experienceleague.adobe.com/en/tools/commerce-storefront/)

## 用語クイックリファレンス

| 優先語 | 意味 | 現在のアーキテクチャラベルとして使用することを避ける |
| --- | --- | --- |
| **Commerce Foundation** | ベースコマースとトランザクション機能 | Core Commerce、PHP基盤レイヤー |
| **ストアフロントサービス** | カタログサービス、ライブサーチ、商品レコメンデーション用のストアフロント向けAPI | Commerceの基盤がひとつ限定されているラベル |
| **Commerce Optimizer マーチャンダイジングサービス** | カタログの発見とマーチャンダイジング体験のためのOptimizer API | Commerce Foundation API |
| **Edge Delivery Servicesを活用したCommerce Storefront** | 顧客向けストアフロントの導入 | API ファミリ |

## 関連するガイダンス

- [参照アーキテクチャ](reference-architectures.md)
- [Commerce オプションの選択](../portfolio/choose-commerce-option.md)
- [ストアフロント](../storefronts/overview.md)
- [API](../apis/commerce-apis.md)
