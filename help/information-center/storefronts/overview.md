---
title: ストアフロント
description: Edge Delivery Servicesを活用したCommerce ストアフロントや、ヘッドレス実装のカスタマイズなど、Adobe Commerce ストアフロントのオプションについて説明します。
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:12:22.967Z'
TQID: 'https://experienceleague.adobe.com/1mQm2s3UGzr7S4j9RMZAaRoUVtzu93N1IFbOypR8vkA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%
---

# ストアフロント

ストアフロントは、Commerceのバックエンド層とAPI層から分離されています。 選択したアーキテクチャに応じて、ストアフロントは、Commerce Foundation API、Storefront Services API、[!DNL Adobe Commerce Optimizer] マーチャンダイジングサービス API、またはAPI Mesh、App Builder、その他の統合メカニズムを介して接続されたシステムからデータを取得できます。 各ストアフロントとCommerce バックエンドの組み合わせについては、[ アーキテクチャオプション ](../architecture-options/overview.md)を参照してください。

## Edge Delivery Servicesを活用したCommerce Storefront

[!DNL Edge Delivery Services]を活用したCommerce ストアフロントは、Adobe Commerce ボイラープレート上に、ドロップインコンポーネントとコンテンツブロックを使用して構築された、顧客向けのストアフロントオプションです。 バックエンドに応じて、Commerce Foundation、Storefront Services、または[!DNL Adobe Commerce Optimizer] マーチャンダイジングサービスに接続する[ アーキテクチャの概要](../architecture-options/overview.md)のいずれかと互換性があります。 [Adobe Commerce Storefrontの概要](https://experienceleague.adobe.com/en/tools/commerce-storefront/)を参照してください。

## Storefront Services

[!DNL Storefront Services]は、[!DNL Adobe Commerce]で使用されるストアフロント指向のサービスです。 サービス APIは、次のような機能に対する最適化されたアクセスを提供します。

- [!DNL Catalog Service]
- [!DNL Live Search]
- [!DNL Product Recommendations]

クラウドまたはオンプレミス（設定時）の[!DNL Adobe Commerce]と[!DNL Adobe Commerce as a Cloud Service]の両方でStorefront サービスを使用します。 これらは[!DNL Adobe Commerce as a Cloud Service]に限定されるものではなく、2つの[!DNL Adobe Commerce] プラットフォームオプションを区別するラベルとして使用しないでください。 [Storefront Services GraphQL スキーマ ](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)を参照してください。

## カスタムヘッドレスストアフロント

[!DNL Edge Delivery Services]が提供するCommerce ストアフロント以外のストアフロントオプションには、[!DNL Luma]、[!DNL PWA Studio]、またはプラットフォームのサポートと実装要件に応じたカスタムヘッドレスストアフロントが含まれます。 カスタムヘッドレスストアフロントは、選択した[ アーキテクチャオプション ](../architecture-options/overview.md)に基づいて、他のストアフロントオプション（Commerce Foundation、Storefront Services、Commerce Optimizer Merchandising Services）と同じAPI ファミリーに接続されます。

## カートとチェックアウトの統合

カートやチェックアウトのトランザクションを処理する場所は、ストアフロントテクノロジーではなく、Commerceバックエンドによって異なります。

- [!DNL Adobe Commerce]のCommerce Foundationがバックエンドの場合、ストアフロントでは、Commerce Foundation APIをカート、チェックアウト、お客様、注文処理、設定された支払い、税務、配送、フルフィルメントの統合に使用します。
- スタンドアロン [!DNL Adobe Commerce Optimizer]と同様に、サードパーティのコマースプラットフォームがバックエンドである場合、ストアフロントは、API Mesh、App Builder、または直接統合を介して、そのプラットフォームのカート、チェックアウト、顧客、注文、支払い、税務、配送、フルフィルメントサービスに接続されます。

## 関連するガイダンス

- [アーキテクチャの概要](../architecture-options/overview.md)
- [API](../apis/commerce-apis.md)
