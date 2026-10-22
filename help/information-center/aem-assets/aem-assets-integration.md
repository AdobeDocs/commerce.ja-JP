---
title: Commerce向けAEM Assets統合
description: AEM AssetsをAdobe Commerce、Adobe Commerce as a Cloud Service、Adobe Commerce Optimizerと統合して、商品画像とメディアを一元管理する方法を説明します。
role: Admin, Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:34:13.564Z'
TQID: 'https://experienceleague.adobe.com/v15DE37DoqpstrsWqnwd6DYpa5moT-BhQ80zDq2KP6I'
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
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 4%
---

# Commerce向けAEM Assets統合

AEM Assetsとの統合により、Adobe Commerceの商品ビジュアル機能が有効になり、AEM Assetsで商品の画像や動画などのメディアを一元管理することができます。 これは、個別のCommerce プラットフォームではなく、任意のCommerce アーキテクチャオプションで動作するオプションのアドオンです。

## アーキテクチャ別の統合パス

2つの統合パスがあります。 選択するプロセスは、Commerceのアーキテクチャによって異なります。

| Commerce アーキテクチャ | AEM Assets統合パス | 詳細情報 |
| --- | --- | --- |
| クラウドまたはオンプレミスの[!DNL Adobe Commerce] | Commerceの[!DNL AEM Assets]統合。 Commerce統合パッケージを使用して、[!DNL Adobe Commerce]と[!DNL AEM Assets]の間で商品の画像、ビデオ、その他のメディアを同期および管理します。 | [Commerce用AEM Assets統合](/help/aem-assets-integration/overview.md) |
| [!DNL Adobe Commerce as a Cloud Service] | [!DNL Product Visuals] powered by [!DNL AEM Assets] | [AEM Assets統合の設定](/help/aem-assets-integration/overview.md#next-steps) |
| スタンドアロン [!DNL Adobe Commerce Optimizer] | [!DNL Product Visuals]は[!DNL AEM Assets]によって強化されています。 ベースカタログと価格データは、[Optimizer Data Ingestion API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)を通じて取得されます。 | [AEM Assetsを使用した商品ビジュアル &#x200B;](/help/optimizer/setup/product-visuals.md) |
| [!DNL Adobe Commerce]と[!DNL Adobe Commerce Optimizer Connector] | [!DNL Product Visuals]は[!DNL AEM Assets]によって強化されています。 カタログと価格データは、コネクタによって[!DNL Adobe Commerce]から同期されます。 | [Commerce Optimizerとの連携](/help/optimizer/integrations/integrations-overview.md) |

[!DNL Product Visuals]は、Adobe Commerce as a Cloud ServiceとAdobe Commerce Optimizerの統合パスです。 Adobe AEMで管理している商品画像をCommerceのカタログレイヤーに同期し、ストアフロント APIを通じてストアフロント体験に提供します。

## 選択する前

- Commerce オンクラウドまたはオンプレミス パスとCommerce as a Cloud ServiceまたはAdobe Optimizer [!DNL Product Visuals] パスの間で、設定とライセンス要件が異なります。 まず、デプロイメント固有の要件を確認します。
- [!DNL AEM Assets]はデジタルアセットを管理します。 Commerceのカタログ、価格設定、カート、チェックアウト、注文システムは、置き換わりません。
- 商品アセットは、SKUまたはその他の文書化されたマッチングメタデータを使用して、Commerce商品と照合されます。
- マーケティング部門とマーチャンダイジング部門が一元化された商品画像とアセットワークフローを必要とする場合は、Adobe Commerceのアーキテクチャに合ったパスを選択しましょう。

## 関連情報

- [Adobe Experience Manager Assets ドキュメント](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/overview)
- [アーキテクチャの概要](../architecture-options/overview.md)
- [API](../apis/commerce-apis.md)
