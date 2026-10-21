---
title: COMMERCE API
description: Commerce Foundation、Storefront Services、Commerce Optimizer Merchandising Services、Data IngestionなどのAdobe Commerce API ファミリーを比較できます。
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:36:11.529Z'
TQID: 'https://experienceleague.adobe.com/JBpnpCy9QITdcYtKnL2btd9grmgIk1prYaCNasgWkok'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
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
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: c4f010fa-1478-4300-a88d-706fbc036a7a
    internal-label: APIs and SDKs
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%
---

# API

| API ファミリー | プライマリ目的 | 使用者 |
| --- | --- | --- |
| **Commerce Foundation GraphQL API** | コアコマースおよびトランザクション機能：カタログ運用、カート、チェックアウト、顧客、注文など | クラウド上の[!DNL Adobe Commerce]、オンプレミス上の[!DNL Adobe Commerce]、および[!DNL Adobe Commerce as a Cloud Service] |
| **Storefront Services GraphQL API** | [!DNL Catalog Service]、[!DNL Live Search]、[!DNL Product Recommendations]を通じて、ストアフロント向けのカタログ、検索、レコメンデーションエクスペリエンスを提供 | クラウドまたはオンプレミス上の[!DNL Adobe Commerce]と、設定済みのサービスおよび[!DNL Adobe Commerce as a Cloud Service] |
| **Commerce Optimizer マーチャンダイジングサービス GraphQL API** | Optimizerで管理されているカタログ、カタログビュー、価格コンテキスト、検索、レコメンデーション、マーチャンダイジング結果の取得 | Optimizer コネクタを使用したクラウドまたはオンプレミスの[!DNL Adobe Commerce]、およびスタンドアロン [!DNL Adobe Commerce Optimizer] |
| **Commerce Optimizer Data Ingestion REST API** | スタンドアロン [!DNL Adobe Commerce Optimizer]実装へのカタログと価格データの追加 | 外部データソースに接続されたスタンドアロン [!DNL Adobe Commerce Optimizer] |

## Commerce Foundation GraphQL API

カタログ、カート、チェックアウト、顧客、注文など、主要なコマース機能。 クラウドの[!DNL Adobe Commerce]、オンプレミスの[!DNL Adobe Commerce]、および[!DNL Adobe Commerce as a Cloud Service]によって使用されます。 [Commerce GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/)を参照してください。

## Storefront Services GraphQL API

[!DNL Catalog Service]、[!DNL Live Search]、[!DNL Product Recommendations]を通じて、ストアフロント向けのカタログ、検索、レコメンデーションエクスペリエンスを提供します。 クラウド、オンプレミス、[!DNL Adobe Commerce as a Cloud Service]上の[!DNL Adobe Commerce]によって使用されます。 [Storefront Services GraphQL スキーマ &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)を参照してください。

## Commerce Optimizer Merchandising Services GraphQL API

Optimizerで管理されているカタログ、カタログビュー、価格コンテキスト、検索、レコメンデーション、マーチャンダイジングの結果を取得します。 [!DNL Adobe Commerce]様がクラウド上で、[!DNL Adobe Commerce Optimizer Connector]様とスタンドアロン [!DNL Adobe Commerce Optimizer]様とオンプレミスで使用しています。 [Commerce Optimizer マーチャンダイジングサービス &#x200B;](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/)を参照してください。

## Commerce Optimizer Data Ingestion REST API

外部データソースからスタンドアロン [!DNL Adobe Commerce Optimizer]実装にカタログと価格データを追加します。 [Commerce Optimizer Data Ingestion](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)を参照してください。

## Commerce Optimizerとの連携

[!DNL Adobe Commerce Optimizer]は、[!DNL Adobe Commerce]またはサードパーティのバックエンドのいずれと組み合わせているかに応じて、複数の統合パスを介して他のシステムに接続します。

### Adobe Commerce Optimizer Connector

クラウドまたはオンプレミスの[!DNL Adobe Commerce]のカタログと価格データを[!DNL Adobe Commerce Optimizer]に同期し、Optimizerが検出とマーチャンダイジングを提供する間、[!DNL Adobe Commerce]をトランザクションシステムとして保持します。 [Commerce Optimizerとの連携](/help/optimizer/integrations/integrations-overview.md)を参照してください。

### サードパーティ製コマース統合

サードパーティのコマースプラットフォーム、PIM、ERP、またはその他のソースからカタログと価格データを取り込み、Data Ingestion REST APIを介してスタンドアロンの[!DNL Adobe Commerce Optimizer]に取り込みます。一方、サードパーティのプラットフォームは引き続きトランザクション記録システムです。

### API MeshとApp Builder

API Meshを使用して、プライベート APIまたはサードパーティ APIでAdobe Commerce APIをオーケストレーションします。 Adobe Developer App Builderを使用して、カスタムアプリケーションや統合機能を構築できます。 関連するCommerceの拡張性ガイダンスについては、[API Mesh](https://developer.adobe.com/graphql-mesh-gateway/)および[Adobe Commerceの拡張性](https://developer.adobe.com/commerce/extensibility/)を参照してください。

イベント駆動型の統合については、[Adobe Commerce用Adobe I/O Events](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/io-events/getting-started-io-events)を参照してください。


### カートとチェックアウトの引き継ぎ

外部バックエンドを持つスタンドアロン [!DNL Adobe Commerce Optimizer]の場合、ストアフロントはマーチャンダイジングサービス GraphQL APIを使用して商品体験を行い、その後、API Mesh、App Builder、またはダイレクト統合を介して、カート、チェックアウト、顧客、注文、支払い、税務、配送、フルフィルメントをバックエンドに引き継ぎます。

### AEM Assets

AEM Assetsは、個別の統合パスではなく、任意のCommerceまたはOptimizer アーキテクチャに追加できる、オプションのクロスカットのDAM統合です。 Commerce[&#128279;](../aem-assets/aem-assets-integration.md)のAEM Assetsとの連携を参照してください。

## 関連するガイダンス

- [アーキテクチャの概要](../architecture-options/overview.md)
- [ストアフロント](../storefronts/overview.md)
- [Commerce向けAEM Assets統合](../aem-assets/aem-assets-integration.md)
