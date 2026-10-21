---
title: Commerce アーキテクチャの概要
description: Adobe Commerceの製品モデルについて学び、詳細なアーキテクチャオプション、ストアフロント、API ガイダンスを確認する場所を確認します。
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T10:11:03.706Z'
TQID: 'https://experienceleague.adobe.com/V9Zp0eS8b45xYEay4EK91tPVnKhRdkWGDj4Vv7hB79U'
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
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%
---

# Commerce アーキテクチャの概要

Adobe Commerceのアーキテクチャは、一般的に、コマースバックエンド（[!DNL Adobe Commerce]または[!DNL Adobe Commerce Optimizer]）、ストアフロント、一連の接続されたサービスおよび統合の3つのレイヤーを組み合わせています。 このセクションでは、製品モデルについて説明し、各専用ページで維持される詳細な比較、図、API参照を示します。

## Adobe Experience Managerの導入方法

| セクション | 次の目的で使用します |
| ------- | --------- |
| [&#x200B; プラットフォームとサービス &#x200B;](../portfolio/platform-and-services.md) | Adobe Commerce、Commerce Foundation、Adobe Commerce Optimizer、Adobe Commerce as a Cloud Serviceの各Commerce製品について説明します。 |
| [Commerce オプションを選択](../portfolio/choose-commerce-option.md) | トランザクションの所有権、デプロイメントモデル、マーチャンダイジングニーズにもとづいて、Commerceのオプションを比較できます。 |
| [&#x200B; アーキテクチャオプション &#x200B;](../architecture-options/implementation-architectures.md) | システム図や参照リンクなど、サポートされている4つのアーキテクチャをすべて詳細に比較できます。 |
| [&#x200B; ストアフロント &#x200B;](../storefronts/overview.md) | ストアフロントのオプションと、それらが各アーキテクチャとどのように連携しているかを把握します。 |
| [API](../apis/commerce-apis.md) | Commerce Foundation、Storefront Services、Commerce Optimizerで使用されるAPI ファミリーを比較します。 |
| [CommerceのAEM Assets統合](../aem-assets/aem-assets-integration.md) | あらゆるCommerceまたはOptimizerのアーキテクチャに、一元化されたデジタルアセット管理システムを追加できます。 |
| [移行と導入](../migration-adoption/overview.md) | Adobe Commerce Optimizerを段階的に導入しながら、アーキテクチャ間の移行を計画する。 |

## 用語クイックリファレンス

| 優先語 | 意味 | 現在のアーキテクチャラベルとして使用することを避ける |
| --- | --- | --- |
| **Commerce Foundation** | ベースコマースとトランザクション機能 | Core CommerceとPHPの基盤レイヤー |
| **ストアフロントサービス** | カタログサービス、ライブサーチ、商品レコメンデーション用のストアフロント向けAPI | Commerceの基盤がひとつ限定されているラベル |
| **Commerce Optimizer マーチャンダイジングサービス** | カタログの発見とマーチャンダイジング体験のためのOptimizer API | Commerce Foundation API |
| **Edge Delivery Servicesを活用したCommerce Storefront** | 顧客向けストアフロントの導入 | API ファミリ |

## 関連するガイダンス

- [実装アーキテクチャ](implementation-architectures.md)
- [参照アーキテクチャ](reference-architectures.md)
- [新しいストアフロントの構築](../implementation-guides/build-new-storefront.md)
