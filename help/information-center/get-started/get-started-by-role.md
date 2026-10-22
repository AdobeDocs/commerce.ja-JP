---
title: 役割別に始める
description: プロジェクトで現在使用しているCommerce プラットフォームと役割に基づいて、Adobe Commerce ドキュメントで適切な開始点を見つける方法について説明します。
role: Admin, Developer, Leader, User
feature: Storefront, Configuration
recommendations: noCatalog
autotag-review: '2026-10-20T11:43:29.080Z'
TQID: 'https://experienceleague.adobe.com/P-GWpL9blAHwmSyN-eFzjUlsOVqyDTxiuLavocyeEdQ'
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
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
subfeature_v2:
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%
---

# 役割ごとに始める

Adobe Commerceのドキュメントは、複数のリポジトリやサイトをまたいで整理されています。 適切な出発点は、役割と、管理者やマーチャンダイザーがプロジェクトで使用するプラットフォームやマーチャンダイジングパスによって異なります。 どのプラットフォームが自分に適用されるかわからない場合は、[&#x200B; プラットフォームとサービス &#x200B;](../portfolio/platform-and-services.md)を参照してください。

## ビジネスユーザーにとっても

Adobe Commerceの概要と、管理者とストアフロントの連携の仕組みについて説明します。

- [[!DNL Adobe Commerce as a Cloud Service] の概要](/help/cloud-service/overview.md)

- [[!DNL Adobe Commerce Optimizer role-based workflows]](/help/optimizer/get-started.md#role-based-workflows)

- [Adobe Commerce入門ガイド](https://experienceleague.adobe.com/en/docs/commerce-admin/start/guide-overview)


## マーチャンダイジング担当者には

Adobe Commerceには、2つのマーチャンダイジングパスがあります。 適用され、利用できるものは、バックエンドによって異なります。役割によって異なります。

- **[!DNL Live Search]、[!DNL Product Recommendations]、および[!DNL Catalog Service]の拡張機能** - [!DNL Adobe Commerce as a Cloud Service]およびAdobe Commerce（クラウドまたはオンプレミス）で使用されます。 次のガイドを参照してください。

- [ライブサーチとは？](/help/live-search/overview.md)
- [商品レコメンデーションとは？](/help/product-recommendations/overview.md)
- Adobe Commerce[&#128279;](/help/catalog-service/overview.md)の カタログサービス。

- **ネイティブマーチャンダイジング （[!DNL Adobe Commerce Optimizer]**） - Adobe Commerce on Cloudまたはオンプレミスが[!DNL Adobe Commerce Optimizer Connector]を使用して[!DNL Adobe Commerce Optimizer]に接続する場合に使用します。 [&#x200B; マーチャンダイジングの概要](/help/optimizer/merchandising/overview.md)を参照してください。

## 管理者向け

セットアップは、プラットフォームと、プロジェクトで[!DNL Adobe Commerce Optimizer]を使用するかどうかで異なります。

- **[!DNL Adobe Commerce as a Cloud Service]** - Commerce サービスが自動的にインストールおよび設定されます。 [Adobe Commerce as a Cloud Serviceの概要](/help/cloud-service/getting-started.md)を参照してください。

- **[!DNL Adobe Commerce Optimizer]** - Commerce バックエンドとは別に設定したSaaS （Software as a Service）製品。 [Adobe Commerce Optimizerの基本を学ぶ](/help/optimizer/get-started.md)を参照してください。

- **[!DNL Adobe Commerce Optimizer Connector]および[!DNL Adobe Commerce Optimizer Connector for B2B]** - Adobe Commerce（クラウド上またはオンプレミス）をAdobe Commerce Optimizerに接続します。 [Adobe Commerce Optimizer Connectorの基本を学ぶ](/help/aco-connector/get-started.md)を参照してください。

- **Adobe Commerce on Cloudまたはオンプレミス（PaaS）**：各Commerce サービス拡張機能をインストールしてから設定します。 詳しい手順については、各拡張機能のガイドを参照してください。

- [ライブサーチを始める](/help/live-search/install.md)
- [製品レコメンデーションのインストールと設定](/help/product-recommendations/install-configure.md)
- [&#x200B; カタログサービスのインストール &#x200B;](/help/catalog-service/installation.md)。

- Adobe Commerce on Cloudまたはオンプレミスのプラットフォーム管理については、以下を参照してください。

- [Commerce on Cloud Infrastructure ガイド](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/overview)
- オンプレミス用[Adobe Commerce Operational Guides](https://experienceleague.adobe.com/en/docs/commerce-operations/operational-guides/home)。

## 開発者向け

Adobe Commerceの拡張、カスタマイズ、統合、ストアフロントの構築。

- [Adobe Commerce開発者向けドキュメント](https://developer.adobe.com/commerce/docs/)
- [Adobe Commerce Storefront開発者ガイド](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/)
- [[!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/overview.md) （クラウド上の既存のCommerceまたはオンプレミスのバックエンドに[!DNL Adobe Commerce Optimizer]に接続する場合に使用）。

## ソリューションアーキテクト向け

複数のCommerce製品にまたがるアーキテクチャのレコメンデーションと参照パターンを確認できます。

- [建築オプション](../architecture-options/overview.md)

## パートナー向け

イネーブルメントガイド、認定パス、パートナープログラムのリソースを検索できます。

- [Adobe パートナープログラム](https://partners.adobe.com/digitalexperience/about)
- [Adobe イネーブルメントノード](https://partners.adobe.com/digitalexperience/learn/enablement-node)
