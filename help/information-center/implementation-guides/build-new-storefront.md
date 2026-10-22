---
title: 新しいストアフロントの構築
description: Edge Delivery Services、Commerceのドロップインコンポーネント、コンテンツブロックおよびテンプレートを使用して、新しいAdobe Commerce ストアフロントを計画および構築する方法について説明します。
role: Developer, Leader
feature: Storefront
recommendations: noCatalog
autotag-review: '2026-10-20T10:58:53.700Z'
TQID: 'https://experienceleague.adobe.com/z-PCoaJzaOyd7SlxjyWs-0tEVo3hpdHucdgq4cZSeQw'
product_v2:
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%
---

# 新しいストアフロントの構築

次のデプロイメントタイプを持つAdobe Commerceのお客様は、Edge Delivery Services、Commerce ドロップインコンポーネント、コンテンツブロックを使用して、新しいストアフロントを構築できます。

- Adobe Commerce as a Cloud Service
- Adobe Commerce Optimizer
- Adobe Commerce Optimizerを使用しないストアフロントサービスを使用するクラウドまたはオンプレミスのAdobe Commerce
- Adobe Commerce Optimizer Connectorを使用したクラウドまたはオンプレミスでのAdobe Commerce

Adobe Commerce ボイラープレートを使用すると、独自のAdobe Commerceまたは[!DNL Adobe Commerce Optimizer] インスタンスをカスタマイズして接続できるストアフロントを利用できます。

>[!NOTE]
>
>Adobe Commerce on cloud infrastructureまたはオンプレミスの場合、コネクタを介したAdobe Commerce Optimizerの導入は、ストアフロントの近代化オプションの1つであり、必須ではありません。 このパスを選択した場合は、[Luma Bridge](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/discovery/luma-bridge/)を使用して、Luma ストアフロントとEdge Delivery Services ストアフロントを接続します。

## Adobe Experience Managerの導入方法

1. アーキテクチャと使用可能なドロップインコンポーネントについては、[Adobe Commerce Storefrontの概要](https://experienceleague.adobe.com/en/tools/commerce-storefront/merchants/quick-start/create-content/)および[Storefront アーキテクチャ &#x200B;](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/architecture/)のドキュメントを参照してください。

1. ストアフロントを設定するには、ストアフロントのドキュメントに従います。

   - [ストアフロントの構築](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/create-storefront/)
   - [Storefront開発者ガイド &#x200B;](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/)でプロジェクトのスコープ、設定、起動を行います。

1. ストアフロントとCommerceバックエンドを連携。

   デプロイメントモデルに応じて指示に従います。 詳しくは、_Storefront開発者ガイド_&#x200B;の[&#x200B; バックエンドオプション &#x200B;](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/backends/){target="_blank"}を参照してください。

## 関連するガイダンス

- [Adobe Commerce Storefrontの概要](https://experienceleague.adobe.com/en/tools/commerce-storefront/merchants/quick-start/create-content/)
- [Adobe Commerce Optimizerを有効にする](enable-aco.md)
- [Adobe Commerce Optimizer Connector](../../aco-connector/overview.md)
- [AEM Assetsとの連携](connect-aem-assets.md)
- [ストアフロントのバックエンドオプション](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/backends/){target="_blank"}
