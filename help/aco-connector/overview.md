---
title: Adobe Commerce Optimizer Connector
description: '[!DNL Adobe Commerce]から[!DNL Adobe Commerce Optimizer]までのカタログ同期、検索、およびストアフロント配信の[!DNL Adobe Commerce Optimizer Connector]について説明します。'
feature: Integration, Storefront, Configuration
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
autotag-review: '2026-06-09T19:00:00.000Z'
nudge: true
TQID: 'https://experienceleague.adobe.com/v769V06jl-9YfovpL3HOB-FxovIMZyHxOlHXHvkQmbc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
    internal-label: Commerce ecosystem
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 76cfaac4-e563-56dd-8938-708bf8b84956
    internal-label: Attributes
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: adedf70c-c1e1-5734-acdc-c5c43b114964
    internal-label: Release Notes
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e9004f3c-09ae-5d24-acd2-fa0987fdb66e
    internal-label: Companies
  - id: f37757d8-3174-5335-b977-1161792f965d
    internal-label: Personalization
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
    internal-label: Storefront configuration
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
    internal-label: Cloud architecture
  - id: dad884f1-e840-49a1-970e-2f965bdbc410
    internal-label: Extensions
  - id: 3c398179-d35a-51ba-b317-6c5b95feef5e
    internal-label: Logs
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
  - id: f56d26ed-050b-4fb7-b29b-8e6e994e80a2
    internal-label: B2B
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 0%
---
# [!DNL Adobe Commerce Optimizer Connector]

[!DNL Adobe Commerce Optimizer Connector]は、[!DNL Adobe Commerce] （クラウドまたはオンプレミス）と[!DNL Adobe Commerce Optimizer]の間のネイティブのファーストパーティ統合です。 [!DNL Adobe Commerce] ストアのカタログと価格データを[!DNL Adobe Commerce Optimizer]に同期することで、次のことが可能になります。

- **AIを活用した商品の発見とレコメンデーション**
- **高性能なヘッドレスストアフロント**&#x200B;を実行します（[!DNL Edge Delivery Services]によるCommerce ストアフロントを含む）
- **の前後**&#x200B;のKPIとデータ同期の正常性を1か所で分析します

[!DNL Adobe Commerce]は、商品、価格、カタログ構造に関する記録システムのままです。 [!DNL Adobe Commerce Optimizer]がエクスペリエンスとマーチャンダイジングのレイヤーとなり、接続されているあらゆるストアフロントやチャネルに迅速かつ適切な結果を提供します。

## 主な特長 {#key-benefits}

| 利点 | アドビにとっての意味 |
| --- | --- |
| **ビルドするカスタムコネクタがありません** | オーダーメイドのフィードやスクリプトを作成、管理するのではなく、サポートされているファーストパーティ統合を利用できます。 |
| **[!DNL Adobe Commerce Optimizer]**&#x200B;で価値実現までの時間を短縮 | 既存の[!DNL Adobe Commerce]展開に加えて、AI 検索、レコメンデーション、ヘッドレスストアフロントを有効にします。 |
| **Commerce スコープと整列** | Web サイト、ストアビュー、顧客グループを[!DNL Adobe Commerce Optimizer]個のカタログ構成（カタログソースと価格表）に自動的にマッピングします。 |
| **運用上の可視性** | 専用の[!UICONTROL Data Feed Sync Status] ビューから、フィードの正常性、最終同期時間、SKUごとのステータスを監視します。 |
| **SaaSに向けた将来への道筋** | クラウドまたはオンプレミスのCommerceから、再プラットフォームなしで[!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer]への段階的な移行パスを提供します。 |

## コネクタアーキテクチャ {#connector-architecture}

次の図は、[!DNL Adobe Commerce]から[!DNL Adobe Commerce Optimizer]まで、およびストアフロントとチェックアウトシステムへのコネクタのエンドツーエンドのアーキテクチャを示しています。

![Adobe Commerce Optimizer Connectorのエンドツーエンドのアーキテクチャ図](./assets/aco-connector-end2end-architecture.png){width="700" zoomable="yes"}

このアーキテクチャでは：

- [!DNL Adobe Commerce] （クラウドまたはオンプレミス）は、記録システムとフィード プロデューサーです
- コネクタは、カタログ、価格、カテゴリフィードを書き出します
- [!DNL Adobe Commerce Optimizer]は、フィード データを取り込み、カタログ ソース、価格表、カタログ ビューに正規化します
- ストアフロント（[!DNL Edge Delivery Services]またはカスタムヘッドレスビルドのCommerce ストアフロント）は、検出とレコメンデーションのために[!DNL Adobe Commerce Optimizer]のGraphQL APIを呼び出し、カートとチェックアウトの操作のために[!DNL Adobe Commerce]または他の接続されたサードパーティプラットフォームを呼び出します

[[!DNL SaaS Data Export]](/help/data-export/overview.md)上に構築されたコネクタは、収集したフィードを[!DNL Catalog Data Ingestion API]形式にマッピングし、認証と送信を処理します。 同期動作、スコープ制御、エラー処理については、[&#x200B; コネクタ同期パイプライン &#x200B;](/help/aco-connector/connector-sync-pipeline.md)を参照してください。

## コネクタの[!DNL Adobe Commerce]の仕組み {#how-the-connector-works-with-adobe-commerce}

[!DNL Adobe Commerce Optimizer Connector]はB2C カタログの同期をサポートしています。 [!DNL Adobe Commerce] インスタンスのカタログと価格設定フィードを同期し、ストア ビュー、web サイト、顧客グループを[!DNL Adobe Commerce Optimizer]のカタログ ソースと価格表にマッピングします。 B2B共有カタログや会社割り当て設定は同期されません。 同期後、[!DNL Adobe Commerce Optimizer] Studioでカタログビューとポリシーを設定します。

![[!DNL Adobe Commerce] データを[!DNL Adobe Commerce Optimizer]](./assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}にマッピングしています

### ベースカタログマッピング

コネクタは、[!DNL Adobe Commerce] カタログデータを[!DNL Adobe Commerce Optimizer] カタログモデルにマッピングします。

- **カタログソース→ストアビュー** – 各ストアビューは[!DNL Adobe Commerce Optimizer]で個別のカタログソースになります。 そのソースには、ローカライズされた製品属性とストアビュー固有のデータが含まれています。
- **Web サイト →価格表** – 各[!DNL Adobe Commerce] Web サイトは[!DNL Adobe Commerce Optimizer]の1つ以上の価格表にマップされます。 web サイトの価格設定と顧客グループの価格設定は、価格表や価格入力として書き出されます。
- **顧客グループ →価格表エントリ** — [!DNL Adobe Commerce]顧客グループの価格は、関連する価格表に追加エントリとして表示されます。

コネクタがカタログデータを同期したら、[!DNL Adobe Commerce Optimizer] Studioでマーチャンダイジングモデルを設定します。 例えば、次のように設定します。

- 地域、ブランド、または顧客固有のサブセットの&#x200B;**カタログビューとポリシー**
- 検索、ファセット、マーチャンダイジングルールの&#x200B;**製品発見**
- **[!DNL Product Recommendations]**

### B2B コネクタの動作 {#b2b-shared-catalog-projection-specification}

[!DNL Adobe Commerce Optimizer Connector for B2B]は、B2B共有カタログと会社の割り当て設定を一方向に投影して、ベースコネクタを保護されたカタログエクスペリエンスに拡張します。 [!DNL Adobe Commerce]は、カタログと価格設定データの信頼できる唯一の情報源です。B2B コネクタは、ベースカタログと価格設定の同期に基づいて構築され、コネクタで生成された予測を管理します。

プロジェクションマッピング、ランタイム認証フロー、保護境界については、[B2B共有カタログ投影](b2b-shared-catalog-projection.md)を参照してください。 セットアップ手順については、[B2B コネクタの基本を学ぶ](/help/aco-connector/get-started-b2b-shared-catalogs.md)を参照してください。

>[!NOTE]
>
>[!DNL Adobe Commerce Optimizer]の設定について詳しくは、[[!DNL Adobe Commerce Optimizer]  マーチャンダイジングツール &#x200B;](/help/optimizer/overview.md#quick-tour)を参照してください。

## 一般的なワークフロー {#typical-workflows}

これらのワークフローは、チームが[!DNL Adobe Commerce Optimizer Connector]を設定および使用する方法を説明します。 統合を設定し、これらのワークフローを有効にする方法について詳しくは、[開始](/help/aco-connector/get-started.md)を参照してください。

### 初期設定と設定 {#initial-setup}

_はじめに_ ガイドの[設定手順](/help/aco-connector/get-started.md#configuration-steps)を参照してください。

### 継続的なデータ同期 {#ongoing-sync}

初期設定の後、コネクタは次の機能をサポートします。

- 初回移行または大規模な構造変更の&#x200B;**完全カタログ同期**
- 製品または価格が変更されたときに継続的に更新する場合は、**Deltaが同期**&#x200B;します
- ターゲット フィードを同期するための&#x200B;**再同期コマンド**

自動化された同期動作、cron スケジュール、エラー処理については、[&#x200B; コネクタ同期パイプライン &#x200B;](/help/aco-connector/connector-sync-pipeline.md)を参照してください。 カタログの完全な同期または大規模な更新の前に、[&#x200B; データ量と同期時間の見積もり](/help/aco-connector/reference/estimate-data-volume-sync-time.md)を使用して、タイミングを計画し、サイトの中断を回避します。

[!DNL Adobe Commerce Optimizer Connector]では、次のフィードを利用できます。

- `products` – 製品データ
- `productAttributes` – 製品属性のメタデータ
- `priceBooks` – 価格表
- `prices` – 製品価格
- `categories` - カテゴリ データ

詳細については、次のトピックを参照してください。

- カタログデータの同期を確認し、コネクタフィードを手動で再同期します：[同期を管理](/help/aco-connector/data-sync-status.md)
- [!DNL Adobe Commerce]件のCLI再同期操作については、[Commerce CLIを使用したフィードの同期](/help/data-export/data-export-cli-commands.md)を参照してください
- [[!DNL Adobe Commerce Optimizer Connector]個のモジュールとフィード エンドポイント](/help/aco-connector/reference/connector-reference.md)
- [コネクタフィードのフィールドマッピング](/help/aco-connector/reference/field-mapping.md)

### マーチャンダイジングとストアフロントの設定 {#merchandising-storefronts}

[!DNL Adobe Commerce]個のデータを[!DNL Adobe Commerce Optimizer]で利用できるようになったら、[[!DNL Adobe Commerce Optimizer] Studio](/help/optimizer/overview.md#quick-tour)を使用して、マーチャンダイジングとストアフロントのエクスペリエンスを同期カタログに接続します。 一般的な次のステップは次のとおりです。

- **カタログ ビューとポリシー** – 基本コネクタの場合は、[!UICONTROL Store setup] メニューから、地域、ブランド、または顧客固有のサブセットとアクセス ルールを定義します。 カタログビューのクエリを制限するには、[&#x200B; プライベートカタログビュー](/help/optimizer/setup/private-catalog-view.md)を参照してください
- **製品の発見とレコメンデーション** — [!UICONTROL Merchandising] メニューで検索、ファセット、マーチャンダイジングルール、類義語、レコメンデーションユニットを設定します。 検索とレコメンデーションの動作は[!DNL Adobe Commerce Optimizer]で管理されています。管理者権限[!DNL Adobe Commerce]の[!DNL Live Search]および[!DNL Product Recommendations]の設定は、これらのフローには適用されなくなりました
- **ストアフロント接続** – 正しい[!DNL Adobe Commerce Optimizer] テナント、カタログビュー、マーチャンダイジング API エンドポイントで、[!DNL Edge Delivery Services]またはサードパーティのヘッドレスビルドにCommerce ストアフロントをポイントします。 カスタムヘッドレス統合については、[&#x200B; ヘッドレスストアフロント統合](/help/aco-connector/headless-storefront.md)を参照してください。 サードパーティ統合の例については、 [!DNL Adobe Commerce Optimizer]&#x200B;[&#128279;](/help/optimizer/developer/salesforce-connector.md)のSalesforce Commerce コネクタを参照してください
- **チェックアウト** — カート、チェックアウト、注文管理、顧客アカウントを[!DNL Adobe Commerce]または接続されたサードパーティのプラットフォームに保存します。 必要に応じて、[!DNL App Builder]と[!DNL API Mesh]をカートのハンドオフに使用します

ステップバイステップの設定ガイダンスについては、[基本を学ぶ](/help/aco-connector/get-started.md)と[[!DNL Adobe Commerce Optimizer]  マーチャンダイジングツール &#x200B;](/help/optimizer/overview.md#quick-tour)を参照してください。

## サポートされるシナリオ {#supported-scenarios}

ベース [!DNL Adobe Commerce Optimizer Connector]は、バックエンドを再構築せずに[!DNL Adobe Commerce Optimizer]を導入したいクラウドおよびオンプレミスのデプロイメントで[!DNL Adobe Commerce]を持つB2C マーチャントをサポートしています。

個別の[!DNL Adobe Commerce Optimizer Connector for B2B]は、ベースコネクタを拡張して共有カタログ設定を同期し、カスタム共有カタログをプライベートカタログビューとして自動的にプロジェクトします。 詳しくは、[B2B カタログの投影](b2b-shared-catalog-projection.md)を参照してください。

**一般的な使用例：**

- **ストアフロントのEdge Deliveryへの移行**
既存の[!DNL Adobe Commerce] バックエンドを維持し、PLP/Search/PDPを[!DNL Adobe Commerce Optimizer]を活用した[!DNL Edge Delivery Services]のストアフロントに移動します。

- **カタログと検索パフォーマンスの拡張**
[!DNL Adobe Commerce]の製品と価格の所有権を維持しながら、大量のカタログのインデックス作成と検索を[!DNL Adobe Commerce Optimizer]のSaaS （Software as a Service）サービスにオフロードします。

## 責任と実装の前提条件 {#responsibilities-prerequisites}

[!DNL Adobe Commerce]は、製品、価格設定、顧客グループの記録システムです。 [!DNL Adobe Commerce]で変更を行うと、コネクタによって[!DNL Adobe Commerce Optimizer]に同期されます。

**[!DNL Adobe Commerce Optimizer]は次の責任を負います：**

- カタログモデリング（カタログソース、価格表、カタログビュー、ポリシー）
- 製品の発見とレコメンデーション
- ストアフロント指標、データ同期ダッシュボード、成功指標レポート

**コネクタが次のものではありません：**

- [!DNL Adobe Commerce]個の買い物かご、チェックアウト、または注文フローを変更
- ストアフロントプロジェクトを自動的にプロビジョニングします（Commerce Storefront / [!DNL Edge Delivery Services]個のツールが処理します）

**開始する前：**

- [!DNL Adobe Commerce]が最小バージョンと[!DNL Adobe Commerce Optimizer Connector]要件を満たしていることを確認してください。 詳しくは、[基本を学ぶ](/help/aco-connector/get-started.md#requirements-to-use-the-integration)を参照してください。
- IMS組織アクセス、インスタンス [!DNL Adobe Commerce Optimizer]、必要な資格情報および地域の詳細があることを確認します。

>[!MORELIKETHIS]
>
> - [の基本を学ぶ [!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/get-started.md) – 統合を設定し、主要なワークフローを有効にします。
> - [&#x200B; コネクタ同期パイプライン &#x200B;](/help/aco-connector/connector-sync-pipeline.md) – 同期メカニズム、初期化、エラー処理について説明します。
> - [同期の管理](/help/aco-connector/data-sync-status.md) — カタログデータの同期を確認し、フィードを手動で再同期します。
> - コネクタフィードの[&#x200B; フィールドマッピング &#x200B;](/help/aco-connector/reference/field-mapping.md) – すべてのフィードのフィールドレベルのデータマッピングを確認します。
> - [&#x200B; トラブルシューティング シナリオ &#x200B;](/help/aco-connector/troubleshooting/troubleshooting-scenarios.md) – 設定ミスまたは予期しない同期結果を解決します。
> - [&#x200B; リリースノート &#x200B;](/help/aco-connector/release-notes.md) — コネクタの更新と既知の問題を確認します。
