---
title: '[!DNL Adobe Commerce Optimizer Connector]'
description: ' [!DNL Adobe Commerce] から [!DNL Adobe Commerce Optimizer]までのカタログ同期、検索、およびストアフロント配信の [!DNL Adobe Commerce Optimizer Connector] について説明します。'
feature: Integration, Storefront, Configuration
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
autotag-review: '2026-06-09T19:00:00.000Z'
TQID: 'https://experienceleague.adobe.com/-C-XP5YYxwyGrkvVR6CDd-FpDybqnlaKMmFPKOKUbFA'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75id: c32adafa-ed01-4b31-997e-2413013911b0id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2: id: ae62cf09-5996-4921-bda8-fbe67b62e470id: f8ddfd3b-6194-46e8-a176-0e918039be56id: dad884f1-e840-49a1-970e-2f965bdbc410
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7id: e0eb8757-182f-49f3-94a4-1587d16f5094id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 23e4f419628a7838357752ecef0c242f1dcdd4c4
workflow-type: tm+mt
source-wordcount: 990
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
| **SaaSに向けた将来への道筋** | PaaSから[!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer]までの低リスクの近代化パスを、再プラットフォームなしで提供します。 |

## コネクタアーキテクチャ {#connector-architecture}

次の図は、[!DNL Adobe Commerce]から[!DNL Adobe Commerce Optimizer]まで、およびストアフロントとチェックアウトシステムへのコネクタのエンドツーエンドのアーキテクチャを示しています。

![Adobe Commerce Optimizer Connectorのエンドツーエンドのアーキテクチャ図](./assets/aco-connector-end2end-architecture.png){width="700" zoomable="yes"}

このアーキテクチャでは：

- [!DNL Adobe Commerce] （クラウドまたはオンプレミス）は、記録システムとフィード プロデューサーです
- コネクタは、カタログ、価格、カテゴリフィードを書き出します
- [!DNL Adobe Commerce Optimizer]は、フィード データを取り込み、カタログ ソース、価格表、カタログ ビューに正規化します
- ストアフロント（[!DNL Edge Delivery Services]またはカスタムヘッドレスビルドのCommerce ストアフロント）は、検出とレコメンデーションのために[!DNL Adobe Commerce Optimizer]のGraphQL APIを呼び出し、カートとチェックアウトの操作のために[!DNL Adobe Commerce]または他の接続されたサードパーティプラットフォームを呼び出します

## コネクタの[!DNL Adobe Commerce]の仕組み {#how-the-connector-works-with-adobe-commerce}

[!DNL Adobe Commerce Optimizer Connector]は、既存のCommerce スコープ（web サイトとストアビュー）と顧客セグメンテーションを使用して、[!DNL Adobe Commerce Optimizer] カタログモデルに入力することで機能します。

![Commerce データのAdobe Commerce Optimizerへのマッピング ](./assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}

- **カタログソース→ストアビュー** – 各ストアビューは、[!DNL Adobe Commerce Optimizer]で個別のカタログSourceになります。 そのソースには、ローカライズされた製品属性とストアビュー固有のデータが含まれています
- **Web サイト →価格表** – 各[!DNL Adobe Commerce] Web サイトは[!DNL Adobe Commerce Optimizer]の1つ以上の価格表にマップされます。 価格表および価格入力としてのweb サイトの価格と顧客グループの価格のエクスポート
- **顧客グループ →価格バリエーション** — [!DNL Adobe Commerce]顧客グループの価格が、関連する価格表に追加エントリとして表示されます

[!DNL Adobe Commerce Optimizer]がデータを取り込んだ後、次の設定を行うことができます。

- [!DNL Adobe Commerce Optimizer] Studioの&#x200B;**カタログビューとポリシー** （地域、ブランド、または顧客固有のサブセットを構築する場合）
- **製品発見** （検索、ファセット、マーチャンダイジングルール）
- **[!DNL Product Recommendations]**

コネクタを有効にすると、[!DNL Adobe Commerce] インスタンスはカタログと価格データの記録システムのままになります。 [!DNL Adobe Commerce]でデータを更新すると、コネクタはその更新を[!DNL Adobe Commerce Optimizer] インスタンスに同期します。

>[!NOTE]
>
>[!DNL Adobe Commerce Optimizer]の設定について詳しくは、[[!DNL Adobe Commerce Optimizer]  マーチャンダイジングツール ](/help/optimizer/overview.md#quick-tour)を参照してください。

## 一般的なワークフロー {#typical-workflows}

これらのワークフローは、チームが[!DNL Adobe Commerce Optimizer Connector]を設定および使用する方法を説明します。 統合を設定し、これらのワークフローを有効にする方法について詳しくは、[開始](/help/aco-connector/get-started.md)を参照してください。

### 初期設定と設定 {#initial-setup}

_はじめに_ ガイドの[設定手順](/help/aco-connector/get-started.md#configuration-steps)を参照してください。

### 継続的なデータ同期 {#ongoing-sync}

初期設定の後、コネクタは次の機能をサポートします。

- 初回移行または大規模な構造変更の&#x200B;**完全カタログ同期**
- 製品または価格が変更されたときに継続的に更新する場合は、**Deltaが同期**&#x200B;します
- ターゲット フィードの&#x200B;**コマンドの再同期**

[!DNL Adobe Commerce Optimizer Connector]では、次のフィードを利用できます。

- `products` – 製品データ
- `productAttributes` – 製品属性のメタデータ
- `priceBooks` – 価格表
- `prices` – 製品価格
- `categories` - カテゴリ データ

詳細については、次のトピックを参照してください。

- [!DNL Adobe Commerce] CLI再同期操作については、[CLI再同期コマンド ](/help/data-export/data-export-cli-commands.md#sync-using-cli-commands){target="_blank"}を参照してください
- [[!DNL Adobe Commerce Optimizer Connector]個のモジュールとフィード エンドポイント](/help/aco-connector/reference/connector-reference.md)
- [コネクタフィードのフィールドマッピング](/help/aco-connector/reference/field-mapping.md)

### マーチャンダイジングとストアフロントの設定 {#merchandising-storefronts}

[!DNL Adobe Commerce]個のデータを[!DNL Adobe Commerce Optimizer]で利用できるようになったら、[[!DNL Adobe Commerce Optimizer] Studio](/help/optimizer/overview.md#quick-tour)を使用して、マーチャンダイジングとストアフロントのエクスペリエンスを同期カタログに接続します。 一般的な次のステップは次のとおりです。

- **カタログビューとポリシー** – 地域、ブランド、または顧客固有のサブセットを定義し、[!UICONTROL Store setup] メニューからルールにアクセスします
- **製品の発見とレコメンデーション** — [!UICONTROL Merchandising] メニューで検索、ファセット、マーチャンダイジングルール、類義語、レコメンデーションユニットを設定します。 検索とレコメンデーションの動作は[!DNL Adobe Commerce Optimizer]で管理されています。管理者権限[!DNL Adobe Commerce]の[!DNL Live Search]および[!DNL Product Recommendations]の設定は、これらのフローには適用されなくなりました
- **ストアフロント接続** – 正しい[!DNL Adobe Commerce Optimizer] テナント、カタログビュー、マーチャンダイジング API エンドポイントで、[!DNL Edge Delivery Services]またはサードパーティのヘッドレスビルドにCommerce ストアフロントをポイントします。 サードパーティ統合の例については、 [!DNL Adobe Commerce Optimizer]](/help/optimizer/developer/salesforce-connector.md)の[Salesforce Commerce コネクタを参照してください
- **チェックアウト** — カート、チェックアウト、注文管理、顧客アカウントを[!DNL Adobe Commerce]または接続されたサードパーティのプラットフォームに保存します。 必要に応じて、[!DNL App Builder]と[!DNL API Mesh]をカートのハンドオフに使用します

ステップバイステップの設定ガイダンスについては、[基本を学ぶ](/help/aco-connector/get-started.md)と[[!DNL Adobe Commerce Optimizer]  マーチャンダイジングツール ](/help/optimizer/overview.md#quick-tour)を参照してください。

## サポートされるシナリオ {#supported-scenarios}

このコネクタは、バックエンドを再構築せずに[!DNL Adobe Commerce Optimizer]を導入したいクラウドおよびオンプレミスのデプロイメントで[!DNL Adobe Commerce]を使用するB2C マーチャント向けに設計されています。

**一般的な使用例：**

- **ストアフロントのみの最新化**
既存の[!DNL Adobe Commerce] バックエンドを維持し、PLP/Search/PDPを[!DNL Adobe Commerce Optimizer]を利用した[!DNL Edge Delivery Services] ストアフロントに移動します

- **カタログと検索パフォーマンスの拡張**
[!DNL Adobe Commerce]の製品と価格の所有権を維持しながら、大量のカタログ インデックス作成と検索を[!DNL Adobe Commerce Optimizer]のSaaS サービスにオフロードします

- **SaaSの段階的な導入**
互換性のあるコンポーザブル [!DNL Adobe Commerce] カタログを使用して、[!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer]に向かう足がかりとしてコネクタを使用します

## 責任と実装の前提条件 {#responsibilities-prerequisites}

[!DNL Adobe Commerce]は、製品、価格設定、顧客グループに関する信頼できる唯一の情報源です。 [!DNL Adobe Commerce]で変更を行います。コネクタは変更を[!DNL Adobe Commerce Optimizer]に同期します。

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

## このトピックの詳細ヘルプ {#more-help-on-this-topic}

- 統合を設定し、主要なワークフローを有効にする：[ [!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/get-started.md)を使い始める
- [!DNL Adobe Commerce Optimizer]の概念とアーキテクチャについて説明します：[何ですか [!DNL Adobe Commerce Optimizer]?](/help/optimizer/overview.md)
- 同期メカニズム、初期化、およびエラー処理について説明します。[ コネクタ同期パイプライン ](/help/aco-connector/connector-sync-pipeline.md)
- すべてのフィードのフィールドレベルのデータマッピング：[ コネクタフィードのフィールドマッピング ](/help/aco-connector/reference/field-mapping.md)
- GraphQLとバンドルエンコーディングを使用したヘッドレスストアフロントの統合：[ ヘッドレスストアフロントの統合](/help/aco-connector/headless-storefront.md)
- 同期と設定の問題の診断：[ トラブルシューティング ](/help/aco-connector/troubleshooting.md)
