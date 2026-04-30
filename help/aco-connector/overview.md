---
title: Adobe Commerce Optimizer Connector
description: Commerce クラウドまたはオンプレミス プロジェクトのデータをAdobe Commerce Optimizerに接続する方法について説明します
feature: Personalization, Integration, Configuration
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
source-git-commit: c9cce4766ef3f30390d50f53237328be1cfeefdf
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 0%

---


# Adobe Commerce Optimizer Connector

Adobe Commerce Optimizer Connectorは、Adobe Commerce（クラウドまたはオンプレミス）とAdobe Commerce Optimizer間のネイティブなファーストパーティ統合です。 Adobe Adobe Commerceストアのカタログと価格データをCommerce Optimizerに同期することで、次のことが可能になります。

- **AIを活用した商品の発見とレコメンデーション**
- **高性能なヘッドレスストアフロント**&#x200B;を実行します（Edge DeliveryによるCommerce ストアフロントを含む）
- **の前後**&#x200B;のKPIとデータ同期の正常性を1か所で分析します

Commerceは、商品、価格、カタログ構造に関する記録システムです。 Commerce Optimizerを利用すれば、エクスペリエンスとマーチャンダイジングのレイヤーを構築し、接続されているあらゆるストアフロントやチャネルに迅速かつ適切な検索結果を提供できます。

## 主な特長 {#key-benefits}

| 利点 | アドビにとっての意味 |
| --- | --- |
| **ビルドするカスタムコネクタがありません** | オーダーメイドのフィードやスクリプトを作成、管理するのではなく、サポートされているファーストパーティ統合を利用できます。 |
| **Commerce Optimizerで価値創出までの時間を短縮** | 既存のAdobe Commerce展開に加えて、AI 検索、レコメンデーション、ヘッドレスストアフロントを有効にできます。 |
| **Commerce スコープと整列** | Web サイト、ストアビュー、お客様グループをCommerce Optimizer カタログ構成図（カタログソースと価格表）に自動的にマッピングします。 |
| **運用上の可視性** | 専用のデータフィード同期ステータスビューで、フィードの正常性、最終同期時間、SKUごとのステータスを監視できます。 |
| **SaaSに向けた将来への道筋** | PaaSからAdobe Commerce as a Cloud Service + Optimizerに向けた低リスクの近代化パスを提供します。 |

## コネクタアーキテクチャ {#connector-architecture}

次の図は、Adobe CommerceからCommerce Optimizer、そしてストアフロントやチェックアウトシステムに至るまで、コネクタのエンドツーエンドのアーキテクチャを示しています。

![Commerce Optimizer コネクタのエンドツーエンドのアーキテクチャ図Commerce](./assets/aco-connector-end2end-architecture.png){width="700" zoomable="yes"}

このアーキテクチャでは：

- Adobe Commerce（クラウドまたはオンプレミス）は、記録システムとフィードプロデューサーです
- コネクタは、カタログ、価格、カテゴリフィードを書き出します
- Commerce Optimizerは、フィード データを取り込み、カタログ ソース、価格表、カタログ ビューに正規化します
- ストアフロント（Edge DeliveryまたはカスタムヘッドレスビルドのCommerce ストアフロント）は、Commerce Optimizer GraphQL APIを呼び出して発見とレコメンデーションを行い、Commerceまたはカートとチェックアウトの処理を行う別の接続されたサードパーティプラットフォームに呼び出します

## Adobe Commerceでのコネクタの仕組み {#how-it-works}

- Commerce Optimizerは、フィードデータを取り込み、正規化して、カタログソース、価格表、カタログビューに取り込みます。

- ストアフロント（Edge DeliveryまたはカスタムヘッドレスビルドのCommerce ストアフロント）では、Commerce Optimizer GraphQL APIを呼び出して発見とレコメンデーションを行い、Commerceや、カートとチェックアウトの処理に使用する他の接続されたサードパーティプラットフォームに呼び出します。

## Adobe Commerceでのコネクタの仕組み

Adobe Commerce Optimizer コネクタは、既存のCommerce スコープ（web サイトとストアビュー）と顧客セグメンテーションを使用して、Commerce Optimizer カタログモデルに入力することで動作します。

![Commerce データのAdobe Commerce Optimizerへのマッピング &#x200B;](/help/aco-connector/assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}

- **ストアビュー→カタログソース** – 各ストアビューは、Commerce Optimizerの個別のカタログSourceになります。 そのソースには、ローカライズされた製品属性とストアビュー固有のデータが含まれています
- **Web サイト→価格表** – 各Commerce Web サイトは、Commerce Optimizerの1つ以上の価格表にマッピングされます。 価格表および価格入力としてのweb サイトの価格と顧客グループの価格のエクスポート
- **お客様グループ →価格バリエーション** — Commerceのお客様グループの価格が、関連する価格表に追加エントリとして表示されます

Commerce Optimizerがデータを取り込んだ後、次の設定を行うことができます。

- Commerce Optimizerの&#x200B;**カタログビューとポリシー** （地域、ブランド、または顧客固有のサブセットを構築する場合）
- **製品発見** （検索、ファセット、マーチャンダイジングルール）
- **商品レコメンデーション**

コネクタを有効にすると、Adobe Commerce インスタンスはカタログと価格データの記録システムのままになります。 Commerceでデータを更新すると、コネクタはその更新を[!DNL Adobe Commerce Optimizer] インスタンスに同期します。

>[!NOTE]
>
>Commerce Optimizerの設定について詳しくは、[[!DNL Adobe Commerce Optimizer]  マーチャンダイジングツール &#x200B;](../optimizer/overview.md#quick-tour)を参照してください。

## 一般的なワークフロー {#typical-workflows}

これらのワークフローでは、Adobe Commerce Optimizer Connectorの設定と使用方法について説明します。 統合を設定し、これらのワークフローを有効にする方法について詳しくは、[開始](get-started.md)を参照してください。

### 初期設定と設定 {#initial-setup}

1. **Composerを使用して、Adobe Commerce**&#x200B;にコネクタパッケージをインストールします。

   `composer require adobe-commerce/commerce-data-export-aco-adapter`

1. Commerce AdminまたはCLI経由で&#x200B;**認証と環境の詳細**&#x200B;を設定します。

   ```terminal
   bin/magento aco:config:init \
     --org_id=<your-org> \
     --tenant_id=<your-tenant> \
     --client_id=<your-client-id> \
     --client_secret=<your-secret> \
     --region=na1 \
     --type=production
   ```

1. **Commerce スコープをCommerce Optimizerにマッピング：**

   - スコープに含める必要があるweb サイトとストアビューを確認する
   - 顧客グループと価格ルールが期待通りにモデル化されていることを確認する

1. **接続性を確認：**

   - テスト同期を実行し、カタログソース、価格表、および初期商品がCommerce Optimizerに表示されることを確認します
   - Commerceのデータフィード同期ステータスページとCommerce Optimizerのデータシンクダッシュボードを使用して検証します

### 継続的なデータ同期 {#ongoing-sync}

初期設定の後、コネクタは次の機能をサポートします。

- 初回移行または大規模な構造変更の&#x200B;**完全カタログ同期**
- 製品または価格が変更されたときに継続的に更新する場合は、**Deltaが同期**&#x200B;します
- ターゲット フィードの&#x200B;**再同期コマンド** （v1.0.12の時点でのカテゴリを含む）:

   - `bin/magento saas:resync --feed=products`
   - `bin/magento saas:resync --feed=prices`
   - `bin/magento saas:resync --feed=categories`

### マーチャンダイジングとストアフロントの設定 {#merchandising-storefronts}

CommerceのデータがCommerce Optimizerで利用可能になったら、Commerce Optimizer Studioを使用して、マーチャンダイジングとストアフロントのエクスペリエンスを同期カタログに接続します。

**マーチャンダイジングとストアフロントを設定するには：**

1. Commerce Optimizer Studioで&#x200B;**カタログビューとポリシー**&#x200B;を作成：

   - ブランド、地域、顧客セグメント、チャネルごとにカタログをフィルタリングします
   - ストアフロントやパートナーごとにデータアクセスルールを適用できます

1. Optimizer UIで&#x200B;**製品検出と推奨事項**&#x200B;を設定します。

   - マーチャンダイジングルール、ファセット、類義語、レコメンデーションユニットの作成
   - コネクターは、すべての検索とレコメンデーション設定をCommerce Optimizerにオフロードします（Commerce管理者のライブ検索ルールと商品レコメンデーションは、これらのフローには適用されなくなりました）

1. **ストアフロント**&#x200B;をCommerce Optimizerに接続：

   - Edge Delivery Servicesを搭載したCommerce ストアフロントの場合、適切なOptimizer テナントビューとカタログビューを使用し、マーチャンダイジング APIを介して検索とレコメンデーションエンドポイントを呼び出すようにストアフロントを設定します
   - サードパーティのストアフロントの場合は、検索とレコメンデーションの呼び出しにOptimizerのパブリック APIまたはSDKを使用します

   >[!NOTE]
   >
   >サードパーティ統合の例については、[Salesforce Commerce Connector for Commerce Optimizer](../optimizer/developer/salesforce-connector.md)を参照してください。

1. **既存のプラットフォームでチェックアウトを維持**:

   - Adobe Commerceやサードパーティプラットフォームで、カート、チェックアウト、注文管理、顧客アカウントを維持します
   - 外部のチェックアウトシステムと統合する場合は、App BuilderとAPI Meshを使用してカートのハンドオフを行います

## サポートされるシナリオ {#supported-scenarios}

このコネクタは、バックエンドを再構築することなくCommerce Optimizerを導入したい、Adobe Commerce クラウド版およびオンプレミスのデプロイメントを使用するB2C マーチャント向けに設計されています。

**一般的な使用例：**

- **ストアフロントのみの最新化**
既存のCommerce バックエンドを維持し、PLP/Search/PDPをCommerce Optimizerを活用したEdge Delivery ストアフロントに移行します

- **カタログと検索パフォーマンスの拡張**
Commerceでは、商品と価格の所有権を維持しながら、Commerce OptimizerのSaaS サービスに多額のカタログインデックスと検索をオフロードします

- **SaaSの段階的な導入**
互換性のあるコンポーザブルなCommerce カタログを備えたAdobe Commerce as a Cloud Service + Optimizerへの足がかりとして、コネクタを使用します

## 責任と実装の前提条件 {#responsibilities-prerequisites}

Commerceは、商品、価格設定、顧客グループのための信頼できる唯一の情報源です。 Commerceで変更を行います。コネクタによってCommerce Optimizerに同期されます。

**Commerce Optimizerは次の責任を負います：**

- カタログモデリング（カタログソース、価格表、カタログビュー、ポリシー）
- 製品の発見とレコメンデーション
- ストアフロント指標、データ同期ダッシュボード、成功指標レポート

**コネクタが次のものではありません：**

- Commerceのカート、チェックアウト、注文フローを変更する
- ストアフロントプロジェクトを自動的にプロビジョニングする（Commerce Storefront / Edge Delivery ツールで処理）

**開始する前：**

- Commerceが最小バージョンおよびサービスコネクタ要件を満たしていることを確認します。 詳しくは、[基本を学ぶ](get-started.md#prerequisites)を参照してください。
- IMS組織アクセス、インスタンス [!DNL Adobe Commerce Optimizer]、必要な資格情報および地域の詳細があることを確認します。

## 関連ドキュメント {#related-documentation}

- 統合を設定し、主要なワークフローを有効にする：[Adobe Commerce Optimizer コネクタの基本を学ぶ](get-started.md)
- Commerce Optimizerのコンセプトとアーキテクチャについて説明します。[Adobe Commerce Optimizerとは何ですか？](../optimizer/overview.md)
