---
title: 移行と導入
description: Adobe Commerce Optimizerの導入、既存のストアフロントの近代化、Adobe Commerce as a Cloud Serviceへの完全移行について説明します。
role: Admin, Developer, Leader
feature: Storefront, Integration, Configuration
recommendations: noCatalog
TQID: 'https://experienceleague.adobe.com/2iEJ6fA-wLr18bi9C8l-w3srx1AWlAtiGt1cG9RPv0Q'
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
  - id: 1783ae9f-7157-5aeb-a915-91e260301e46
    internal-label: Routes
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%
---

# 移行と導入

アセットの導入を、単一の基盤で一括して行う必要はありません。 目先の目標が、ストアフロントの近代化、マーチャンダイジングの改善、バックエンドの近代化、マネージドソフトウェア as a Service （SaaS）への完全な移行のいずれであるかにもとづいて、ルートを選択します。

## 導入ルート

### 既存のAdobe Commerceの導入を最新化する

- 既存のCommerce Foundationをトランザクションバックエンドのままにします。
- [!DNL Edge Delivery Services]を活用したCommerce Storefrontを導入します。
- Storefront Services、App Builder、API Mesh、オプションのAEM Assets統合を使用できます。

### Commerce Optimizerをブリッジとして使用

- [!DNL Adobe Commerce] クラウドまたはオンプレミスを[!DNL Adobe Commerce Optimizer Connector]を使用して接続します。
- マーチャンダイジングサービス、発見、レコメンデーション、Edge Delivery Servicesストアフロントを導入する。
- 商品、価格、カタログ構造、カート、チェックアウト、顧客、注文の主要な記録システムとして[!DNL Adobe Commerce]を維持します。
- このアーキテクチャを[!DNL Adobe Commerce as a Cloud Service]への移行として使用します。

### Adobe Commerce as a Cloud Serviceへの完全な移行

- 現在のアプリケーション、カスタマイズ、統合、ストアフロント、データを評価します。
- SaaS対応の拡張性パターンを使用してカスタマイズを最新化。
- ストアフロントと統合を再構築または調整する。
- カタログ、顧客、注文、設定、サポートされているカスタムデータを移行して検証します。
- 新しいSaaS環境をテスト、カットオーバー、運用します。

### スタンドアロンのAdobe Commerce Optimizerを導入する

- サードパーティのCommerceプラットフォーム、PIM、ERPなどからカタログや価格データを取り込むことができます。
- カタログの取得、検索、レコメンデーション、マーチャンダイジングに[!DNL Adobe Commerce Optimizer] マーチャンダイジングサービスを使用します。
- [!DNL Edge Delivery Services]を活用したCommerce Storefrontを使用します。
- 連続性のあるサードパーティシステムを利用して、カート、チェックアウト、顧客、注文、支払い、税務、配送、フルフィルメントを維持できます。

## 推奨シーケンス

1. 現在の状況を評価し、システムの所有権を定義する。
1. API ファーストの統合境界の確立。
1. ストアフロントとエクスペリエンスのレイヤーを近代化。
1. マーチャンダイジングサービスとAEM Assetsを並行して導入する。
1. 必要に応じて、Commerce Foundationを移行します。
1. 検証、カットオーバー、監視、最適化。

## 関連するガイダンス

- [Commerce オプションの選択](../portfolio/choose-commerce-option.md)
- [建築オプション](../architecture-options/overview.md)
- [既存のストアフロントを近代化](../implementation-guides/modernize-storefront.md)
- [Adobe Commerce Optimizerを有効にする](../implementation-guides/enable-aco.md)
