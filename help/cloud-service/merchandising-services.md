---
title: コンポーザブルカタログデータモデルとマーチャンダイジングサービス
description: コンポーザブルカタログデータモデルが[!DNL Adobe Commerce as a Cloud Service]でのカタログ配信をどのように変更するか、およびマーチャントとストアフロントチームが知っておく必要があることについて説明します。
feature: Catalog Management, Personalization, Saas
role: Leader
level: Beginner
autotag-review: '2026-11-09T05:07:21.124Z'
TQID: 'https://experienceleague.adobe.com/5Aaumfx9-lOBMDOg59rr-MMl-0sgFLSVUzngkdzfyR0'
product_v2:
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 76cfaac4-e563-56dd-8938-708bf8b84956
    internal-label: Attributes
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: a8ae7a5a-6cdc-5922-bd0d-6feb44b04984
    internal-label: Upgrade
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
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
  - id: e9004f3c-09ae-5d24-acd2-fa0987fdb66e
    internal-label: Companies
  - id: f37757d8-3174-5335-b977-1161792f965d
    internal-label: Personalization
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
    internal-label: Reporting
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: 0bda134570bb3bf2f43da545917dedc95394df5e
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%
---

# Merchandising Services

Adobe Commerce as a Cloud Serviceは、マーチャンダイジングサービスを通じて、コンポーザブルカタログデータモデル（CCDM）をサポートするようになりました。 Adobe Commerce Optimizerはこのデータモデルを導入し、CCDMは両方の製品に、ストアフロントカタログの閲覧とマーチャンダイジングの機能を提供するための共通の基盤を提供します。一方、Commerce財団は、製品、価格、取引を継続的に管理しています。

このトピックでは、CCDMでの変更、機能の継続、およびマーチャント、パートナー、ストアフロント開発者にとっての変更の意味について説明します。

## CCDMはどのような変化をもたらしますか？

元のカタログモデルでは、カタログサービスを使用してストアフロントに商品データを配信し、ライブサーチと商品レコメンデーションでは検索、マーチャンダイジング、レコメンデーション機能を提供します。 このモデルでは、Commerceは[SaaS データ書き出し](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/overview)を使用して同期します。

CCDMでは、これらの機能は、Adobe Commerce Optimizerと同じカタログ基盤で動作します。 [&#x200B; カタログビュー](https://experienceleague.adobe.com/en/docs/commerce-admin/merchandising-with-ccdm/setup/catalog-view)と[&#x200B; ポリシー](https://experienceleague.adobe.com/en/docs/commerce-admin/merchandising-with-ccdm/setup/policies)は、ストアフロントで使用可能なカタログコンテキストを定義します。 ポリシーによって商品の品揃えが決まります。マーチャンダイジングルールは、あらゆるカタログビューに適用することも、特定のビューに合わせてカスタマイズすることもできます。

これにより、カタログの設定、アクセス、マーチャンダイジング方法が変更されます。 CCDMは、オリジナルのCommerceカタログの検索、レコメンデーション、マーチャンダイジング機能を基盤としており、カタログビューレベルでの制御を可能にします。 その他の管理機能とレポート機能については、以下で説明します。

Commerce財団は、商品と価格の正規の情報源であり続けています。 Adobe Commerceとas a Cloud Serviceのネイティブな連携により、単一の基盤からCCDMにデータを同期できます。 web サイト、実店舗、ストアビューの設定は、既存のカート、チェックアウト、注文管理ワークフローとともにCommerceに残ります。

## ライセンスとプロビジョニング

マーチャンダイジングサービスは、既存のAdobe Commerce as a Cloud Service SKUに含まれています。 これは2つ目の製品やサブスクリプションではなく、Adobe Commerce Optimizerの別途購入、使用権限、テナントは必要ありません。

## アーキテクチャの概要

[!DNL Commerce Foundation]は引き続き商品と価格の主要レコードであり、引き続きトランザクションを管理します。 ネイティブ統合により、製品データと価格データが[!DNL Commerce]からCCDMに一方向で同期されます。 この同期のために別のコネクタまたは[!DNL App Builder] アプリをインストールしていません。

ストアフロントは、CCDMが支援するマーチャンダイジングサービスを使用して、ブラウジング、検索、レコメンデーション、マーチャンダイジングのためのカタログデータとコンテキストを取得します。 リクエストでは、カタログコンテキストを使用して、目的のオーディエンスの商品と価格を取得します。 Web サイト、ストア、ストアビューの設定を[!DNL Commerce]で引き続き管理します。

次の図は、より広範なAdobe Commerce as a Cloud Service アーキテクチャにおけるマーチャンダイジングサービスの位置を示しています。

![&#x200B; マーチャンダイジングサービスへのカタログデータフローを示すCommerce アーキテクチャ &#x200B;](./assets/data-flow-ccdm.png){zoomable="yes"}

## マーチャントにとっての新機能は何ですか？

新しいモデルでは、既存のマーチャンダイジングルールをすべてのカタログビューまたは特定のビューにスコープできます。 これにより、各ストアフロントのオーディエンスにマーチャンダイジングを適用することができます。 カタログ ビュー[&#128279;](https://experienceleague.adobe.com/en/docs/commerce-admin/merchandising-with-ccdm/merchandising/rules/add)にマーチャンダイジング ルールを スコープ設定する方法について説明します。

管理画面で、[!UICONTROL Catalog Views]と[!UICONTROL Policies]を使用してカタログコンテキストを設定できます。 [!UICONTROL Success Metrics]を使用して、収益、コンバージョン、エンゲージメント、獲得、直帰率を確認することもできます。 詳しくは、[成功指標](https://experienceleague.adobe.com/en/docs/commerce-admin/merchandising-with-ccdm/manage-results/success-metrics)を参照してください。

## 導入する前の検討事項

マーチャンダイジングサービスを導入する前に、CCDM モデルがライセンス、カタログ統合、ストアフロント、管理者ワークフローにどのような影響を与えるかを確認しましょう。

### カタログ管理と統合

[!DNL Commerce Foundation]の商品と価格の管理を続行します。 ネイティブ統合により、CCDMに同期されます。 マーチャンダイジングサービス用の2番目の製品カタログを作成しないでください。

### Storefrontの実装

ストアフロントでカタログデータを取得する方法は、実装によって異なります。

- **[!DNL Adobe Commerce Storefront]** ドロップイン – ドロップインが移行を処理します。 コードの変更は必要ありません。 [&#x200B; ストアフロント設定ドキュメント &#x200B;](https://experienceleague.adobe.com/en/tools/commerce-storefront/)を参照してください。
- **カスタムまたはその他のストアフロント** - [&#x200B; ヘッダー設定リファレンス &#x200B;](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/configuration/commerce-configuration/#headers)の説明に従って、カタログリクエストヘッダーを更新します。

カタログクエリを確認し、CCDM ベースモデルのリクエストヘッダーを確認します。 既存のクエリやヘッダーが変更されないと仮定しないでください。 マーチャンダイジング GraphQLのクエリは、元のカタログサービスモデルで使用されるクエリとは異なります。 その他のクエリはCCDMをサポートしています。 [&#x200B; マーチャンダイジング GraphQL API リファレンス &#x200B;](https://developer.adobe.com/commerce/services/reference/graphql/)を使用し、[&#x200B; ストアフロントヘッダーリファレンス &#x200B;](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/configuration/commerce-configuration/#headers)に対して必要なカタログコンテキストを検証します。

### サードパーティ製アプリと拡張機能

カタログデータの読み取りやカタログイベントのプロバイダーとの利用を可能にする、サードパーティ製のアプリや拡張機能を確認します。 互換性は、各アプリまたは拡張機能でのインターフェイスの使用方法によって異なります。

### 管理者エクスペリエンス

CCDMを使用するAdobe Commerce as a Cloud Serviceでは、[[!DNL Adobe Unified Experience]](https://experienceleague.adobe.com/en/docs/commerce-admin/start/admin/admin-unified-experience) （統合シェル）が使用されます。 Adobeは、CCDMとは別にUnified Shellをリリースしました。 元のカタログサービスモデル上の既存のインスタンスは、クラシックシェルと統合シェルの両方にアクセスできます。

### 制限

CCDM モデルでは、Adobe Commerce as a Cloud Serviceの制限は変更されません。 カタログ基盤をOptimizerと共有しても、CommerceがOptimizerのキャパシティまたは制限を継承するわけではありません。

## 可用性と移行

このリリースの後にAdobe Commerce as a Cloud Serviceで開始する組織には、デフォルトでマーチャンダイジングサービスが提供されます。 自社で使用しているカタログデータモデルが必要な場合は、Adobeのアカウントチームに連絡し、例外の有無について問い合わせます。

このリリース以前にAdobe Commerce as a Cloud Serviceを使用していた組織は、[新しいインスタンスのプロビジョニング &#x200B;](./getting-started.md#create-an-instance)時に、どちらかのカタログモデルを選択できます。 デフォルトでは、[!UICONTROL Enable CCDM] スイッチャーは無効になっています。 CCDMを有効にすると、それを無効にすることはできません。

既存のインスタンスは自動的に変更されません。 一般提供（GA）では、既存の元のカタログサービスインスタンスをマーチャンダイジングサービスに移行することはできません。
