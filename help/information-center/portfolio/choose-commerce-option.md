---
title: Commerce オプションの選択
description: トランザクションの所有権、デプロイメントモデル、マーチャンダイジングニーズにもとづいて、Adobe Commerceのアーキテクチャを比較できます。
role: Admin, Developer, Leader, User
feature: Storefront, Integration, Configuration
recommendations: noCatalog
TQID: 'https://experienceleague.adobe.com/5y0IU5nji50eqfFNQHbVDV-R81Mx0I8v5Y0a6nccL-w'
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
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
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
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%
---

# Commerce オプションの選択

まず、カート、チェックアウト、注文などの取引を所有しているシステムを特定します。 次に、バックエンドに合ったマーチャンダイジングパスを選びます。

## 決定の指針となる質問

次の質問を使用して、評価するオプションを特定します。 既存のコマースのバックエンド、維持するインフラ責任、商品の発見とマーチャンダイジングの改善が必要かどうか検討します。 Adobe Commerce Optimizerは、発見とマーチャンダイジングの機能を提供します。 トランザクションを処理するバックエンドは置き換わりません。

1. **AdobeでCommerce Platform as a Software as a Service （SaaS）を管理しますか？**
   - はい：Adobe Commerce as a Cloud Serviceを評価します。
   - いいえ：Adobe Commerceが必要で、クラウドまたはオンプレミスのインフラストラクチャを引き続き制御する場合は、Adobe Commerce オンクラウドまたはオンプレミスを検討してください。
1. **買い物かご、チェックアウト、注文、その他の取引を処理するためにAdobe Commerceが必要ですか？**
   - はい：Adobe Commerce オンクラウドまたはオンプレミス、またはAdobe Commerce as a Cloud Serviceを評価します。 これらのオプションでは、Commerce Foundationをトランザクションバックエンドとして使用します。
   - いいえ：既存またはサードパーティのトランザクションバックエンドを維持します。 Adobeの検出およびマーチャンダイジング機能も必要な場合は、スタンドアロンのAdobe Commerce Optimizerを検討してください。
1. **Adobe Commerce Optimizerを使用して、既存のサードパーティ製コマースバックエンドでの商品検索とマーチャンダイジングを改善しますか？**
   - はい：取引のサードパーティバックエンドを維持しながら、スタンドアロンのAdobe Commerce Optimizerを評価します。
1. **既にAdobe Commerceをクラウドまたはオンプレミスで運用しており、より強力な検出とマーチャンダイジングが必要ですか？**
   - はい：Adobe Commerce Optimizer Connectorを評価して、Adobe Commerceが引き続きトランザクションを処理しながら、カタログと価格データを同期させます。

以下の比較表を使用して、回答を出発点と一致させます。 システム図の詳細については、[&#x200B; アーキテクチャオプション &#x200B;](../architecture-options/overview.md)を参照してください。

## Commerceのオプションを比較

| お客様の要件 | 出発点の推奨 | トランザクションを所有するシステム | マーチャンダイジングと発見 |
| --- | --- | --- | --- |
| Adobeは、CommerceプラットフォームをSaaSとして管理します。 | [Adobe Commerce as a Cloud Service](/help/cloud-service/overview.md) | as a Cloud Service財団 | Adobe Commerce as a Cloud Service用にプロビジョニングされたCommerce サービスを使用します。 Adobe Commerce Optimizerとの連携の可用性については、この表の下のメモを参照してください。 |
| クラウドやオンプレミスのインフラストラクチャを引き続き制御するには、Adobe Commerceが必要です。 | [Adobe Commerce オンクラウドまたはオンプレミス &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/start/guide-overview) | Adobe Commerce財団 | 必要に応じて、サポートされているCommerceサービスを使用します。 |
| オンプレミスでAdobe Commerceを使用しており、Adobe Commerce Optimizerを導入して発見とマーチャンダイジングを行いたい場合。 | Adobe Commerceと[Adobe Commerce Optimizer コネクタ &#x200B;](/help/aco-connector/overview.md) | Adobe Commerceは、引き続き取引の記録システムとして活用されています。 | このコネクタは、カタログと価格データをAdobe Commerce Optimizerに同期し、発見とマーチャンダイジングのエクスペリエンスを提供します。 |
| サードパーティのコマースバックエンドを持っており、そのバックエンドを置き換えることなく、Adobe Commerce Optimizerの発見とマーチャンダイジングが必要です。 | スタンドアロン [Adobe Commerce Optimizer](/help/optimizer/overview.md) | サードパーティコマースのバックエンド | カタログと価格データをAdobe Commerce Optimizerに送信します。 API Mesh、App Builder、または直接統合を利用して、カートやチェックアウトなどのトランザクションオペレーションをバックエンドと統合できます。 |

>[!NOTE]
>
>Adobe Commerce as a Cloud ServiceとAdobe Commerce Optimizerの連携は、Commerceのロードマップに記載されています。 両方の基盤が必要な場合は、現時点では個別のアーキテクチャオプションとして使用することを計画してください。 統合のタイムラインについて詳しくは、Adobeのアカウントマネージャーにお問い合わせください。

## 関連するガイダンス

- [プラットフォームとサービス](platform-and-services.md)
- [建築オプション](../architecture-options/overview.md)
- [基本を学ぶ](../get-started/get-started-by-role.md)
