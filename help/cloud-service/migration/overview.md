---
title: ' [!DNL Adobe Commerce as a Cloud Service]に移行'
description: ' [!DNL Adobe Commerce as a Cloud Service]への移行方法について説明します。'
feature: Cloud
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
role: Developer
level: Intermediate
autotag-review: '2026-06-18T16:12:28.840Z'
TQID: 'https://experienceleague.adobe.com/GmxaQdGKvAIDpZ2jvmlLFSYw0IFQysIMOT0lUnsJBsI'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2:
  - id: e91a50b1-0b31-436e-9033-00e4776e94cb
  - id: f56d26ed-050b-4fb7-b29b-8e6e994e80a2
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: addc3a3a-2b1c-4fdf-aea4-4b1eb2931ba6
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: bef6657cdf6703b6a0a1109bd6582ecbe4e19930
workflow-type: tm+mt
source-wordcount: 3302
ht-degree: 0%

---

# [!DNL Adobe Commerce as a Cloud Service]に移行

このガイドは、開発者が[!DNL Adobe Commerce on Cloud]またはオンプレミスから[!DNL Adobe Commerce as a Cloud Service] （SaaS）に移行するのに役立ちます。 このSaaS モデルは、パフォーマンスの向上、拡張性、および[!DNL Adobe Experience Cloud]との統合を提供します。

>[!NOTE]
>
>移行ツールについて詳しくは、[一括データ移行ツール &#x200B;](./bulk-data/migration-tool.md)を参照してください。

## 概要

確立された[!DNL Adobe Commerce] ストアを[!DNL Adobe Commerce as a Cloud Service]に移行することは、データを移行するだけではありません。 実際の移行は、次の領域にまたがっています。

- アプリケーション - [!DNL Adobe Commerce on Cloud]またはオンプレミスのインストール用に構築されたカスタマイズと拡張機能
- データ – カタログ、注文、顧客、設定
- ストアフロント
- 外部システムとの統合

[!DNL Adobe Commerce as a Cloud Service]はバージョンのないSaaS プラットフォームです。つまり、これらの領域を適応させずに移行することはできません。 カスタマイズは[!DNL App Builder] アプリケーションに近代化され、ストアフロントはEdge Delivery Services （EDS）で再構築され、データは新しい[!DNL Adobe Commerce as a Cloud Service] テナントに移行され、統合はSaaS パターンを使用して再確立されます。

移行を1つのモノリシックプロジェクトとして検討する代わりに、Adobeでは、[3つの移行ツール &#x200B;](#migration-tools-workflow)を中心に構築された統合された移行ワークフローを提供します。

この共有ワークフローは、発見を統合し、エンジニアリングと配信チームを調整し、一貫した移行計画を提供します。

![移行フロー図](../assets/migration-flow.png)

### PaaSとSaaSの比較

[!DNL Adobe Commerce on Cloud]またはオンプレミス（PaaS）と[!DNL Adobe Commerce as a Cloud Service] （SaaS）では、それらの管理方法とマーチャントがプラットフォームとどのように関わっているかが異なります。

**主な違い**

- [!BADGE PaaSのみ]{type=Informative url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"}
- **[!DNL Adobe Commerce on Cloud Infrastructure]**：マーチャントは、アプリケーションコード、アップグレード、パッチ適用、インフラストラクチャ設定を管理します。
- **[!DNL Adobe Commerce]オンプレミス**：マーチャントは、Adobeのホスト環境で、アプリケーションコード、アップグレード、パッチ適用、インフラストラクチャ設定を管理します。

  >[!NOTE]
  >
  >サービス（MySQL、Elasticsearchなど）の[共有責任モデル &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/security-and-compliance/shared-responsibility)。

- [!BADGE SaaSのみ]{type=Positive url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"} **SaaS （新規 – [!DNL Adobe Commerce as a Cloud Service]）**: Adobeは、コアアプリケーション、インフラストラクチャ、およびアップデートを完全に管理します。 開発者は、拡張性ポイント（API、App Builder、UI SDK）によるカスタマイズに重点を置きます。 コアアプリケーションコードはロックされています。

**アーキテクチャへの影響**

- **バージョンのないプラットフォーム**：継続的な更新は、コアのメジャーバージョンのアップグレードが不要であることを意味します。
- **マイクロサービスとAPI ファースト**：拡張性と統合に対するAPIへの依存度を高めます。
- **デフォルトのヘッドレス（オプション）**：分離型ストアフロントの強力なサポート（Edge Delivery Servicesを搭載したCommerce ストアフロントなど）。
- **Edge Delivery Services**: フロントエンドのパフォーマンスとデプロイメントに影響します。

**新しいツールと概念**

- Adobe Developer App Builder[&#128279;](https://developer.adobe.com/graphql-mesh-gateway/)の[Adobe Developer App Builder](https://developer.adobe.com/app-builder/)およびAPI メッシュ
- [Commerce Optimizer](../../optimizer/overview.md)
- [Edge 配信サービス](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=ja)
- [Commerce Cloud Manager](../getting-started.md#create-an-instance)を使用したセルフサービス プロビジョニング

### 移行のジャーニー

移行は、次のフェーズを経て移行します。

- **評価** – 既存の実装を分析し、インベントリのカスタマイズ、統合、ストアフロントの特性、データ構造について検討します。 分析後、移行に関する推奨事項、複雑さスコアリング、労力の見積もりを含むロードマップを作成します。
- **アプリケーションを最新化し、データを移行する** - カスタマイズを[!DNL App Builder] アプリケーションとして再構築しながら、ビジネス データを[!DNL Adobe Commerce as a Cloud Service]に移行します。
- **ストアフロントを最新化** - Commerce用Edge Delivery Services（EDS）でストアフロントを再構築します。
- **カットオーバーして操作** - トラフィックを[!DNL Adobe Commerce as a Cloud Service]に切り替え、レガシーシステムを廃止し、継続的な操作に移行します。

移行は通常、直線的ではなく、反復的なものです。 企業は、最終的な本番稼動のカットオーバーの前に、複数の環境を評価し、推奨事項を検証し、段階的に近代化し、実装計画を改善することができます。

### 移行ツール ワークフロー

次のワークフローにはそれぞれ独自のツールがあります。 移行時に使用する一般的なブループリントとして機能する移行評価を使用して、移行を完了するために一緒に使用します。

| ワークフロー | ツール | 説明 |
| --- | --- | --- |
| [評価](#migration-assessment-tool) | **移行評価ツール** | カスタムモジュール、サードパーティの拡張機能、統合、ストアフロントの観察、データベーススキーマ、カスタムテーブル、移行の推奨事項、複雑さのスコアリング、近代化の労力の見積もりをインベントリする、AIを活用した既存の実装の評価。 |
| [&#x200B; アプリケーションとストアフロントの近代化](#code-and-storefront-migration-commerce-developer-mcp) | **Commerce Developer MCP** | COMMERCEアプリケーションのAIを活用した近代化、カスタマイズの[!DNL App Builder]への移行の高速化、Edge Delivery Services（EDS）へのストアフロント変換のサポート、実装のレビューと検証による広範なアプリケーション近代化ジャーニーのガイドをエンジニアリングチームが提供します。 |
| [&#x200B; データ移行](#data-migration-commerce-data-migration-service) | **Commerce Data Migration Service** | カタログ、顧客、注文データの抽出、読み込み、完全性の検証を[!DNL Adobe Commerce as a Cloud Service]に行います。 |

これらのトラックはスタンドアロンではありません。 適切な順序でまとめて使用することで、手戻りを最小限に抑えることができます。

- **最初に評価を実行** – 評価を実行すると、最初にサポートされていないカスタマイズを特定し、移行労力を推定し、データ移行の考慮事項を公開し、実装を開始する前に統合依存関係を強調表示します。 評価は、アプリケーションの近代化ワークフローとデータ移行ワークフローの両方で使用される移行の設計図になります。
- **アプリケーションの近代化** - Commerce Developer MCPは、移行評価を使用して、近代化するカスタマイズとその方法を決定します。 次に、MCPは、対応する[!DNL App Builder]個のアプリケーションとストアフロントコンポーネントを生成します。
- **データ移行** - データ移行スコープに関するアンケートでは、評価で表示されたスコープ、ボリューム、カスタムテーブルをキャプチャします。
- **カスタムおよびサードパーティのデータ** - サードパーティの拡張機能によってカスタムテーブルに保持されているデータは、評価中に識別されますが、標準データ移行では処理されず、[!DNL App Builder]のカスタマイズが必要です。

ストアフロントの近代化は、単なるUIの移行ではありません。 ビジネス機能の移行に加えて、エクスペリエンスアーキテクチャ、再利用可能なコンポーネントの近代化、パフォーマンスの最適化、Edge Delivery Servicesパターンの採用を検討する必要があります。

統合は移行評価の一部として評価されますが、その実装はシナリオによって異なります。 統合では、[!DNL App Builder]、[!DNL API Mesh]、Adobe I/O Events、[!DNL Adobe Commerce as a Cloud Service]のAPIを活用できます。

これらの移行ツールは、移行評価を中心とした統合された移行ワークフローを拡張および維持し続けます。

### 次のステップ

移行の準備ができたら、まず評価を作成します。 移行評価は、残りの移行が従う計画を確立します。

Migration Assessment ToolとCommerce Developer MCPは、AIを利用して、検出、計画、導入を支援します。 他のエンジニアリングワークフローと同様に、AI生成のレコメンデーションと実装は、標準アーキテクチャ、テスト、品質保証プロセスの一環として、チームで慎重にレビューし、検証する必要があります。

## 移行評価ツール

開発または移行を開始する前に、移行のサイズを考慮し、開発が必要な項目を決定する必要があります。 [!DNL Adobe Commerce on Cloud]またはオンプレミスの[!DNL Adobe Commerce] ストアには、カスタムモジュール、統合、ストアフロントのカスタマイズ、データ構造が含まれている可能性が高く、誰かが実装を分析するまで明らかにならない可能性があります。 移行評価ツールは、コードベースを自動的にスキャンして、開発用にこれらの項目を識別します。

### 評価の概要

移行評価ツールは、既存の実装のAI評価を実行し、構造化された近代化評価と[!DNL Adobe Commerce as a Cloud Service]移行ロードマップを生成します。 また、アプリケーションのカスタマイズ、統合、データ構造、ストアフロントの特性など、近代化に影響を与える実装の詳細を評価することで、移行の包括的な全体像を構築できます。 これにより、発見を迅速かつ反復可能なプロセスに変換し、取り組む前に労力、リスク、順序を評価できます。

移行評価ツールが生成する評価は、単なるレポートではありません。 評価は、移行ライフサイクル全体を通じて計画、実装、検証に情報を提供する共有された移行アーティファクトになります。 移行ジャーニーの第一段階として、その調査結果には、アプリケーションの近代化とそれに続くデータ移行の取り組みの両方が含まれます。

移行評価レポートに含まれる内容とその使用方法について詳しくは、[移行評価](./assessment.md)を参照してください。

### 評価ステージ

評価は、既存の実装に対して実行され、一連の自動化されたステージを通じて進行します。

- **Inventory** – 実装をカタログ化します。 含まれるもの：カスタムモジュール、Composerの依存関係、サードパーティの拡張機能、設定、ストアフロントコンポーネント（該当する場合）、ファイル、拡張ポイント、イベント、プラグイン、API、cron ジョブ、キュー、データベーススキーマ、カスタムデータベーステーブル。
- **Analyze** – 静的分析を実行して、ストアのカスタマイズ、標準の[!DNL Adobe Commerce] インストールからの相違、およびそれらのカスタマイズがアプリケーション全体でどのように相互作用するかを特定します。
- **Classify** — AIを使用して各カスタマイズを解釈し、カスタマイズの内容を要約し、関連する機能をグループ化し、実装パターンを特定し、コンテキストに沿った移行の推奨事項を提供します。
- **Map and recommend** – 各Adobe サービスを、デフォルトの機能、[!DNL App Builder]個のアプリケーション、または機能を含む[!DNL Adobe Commerce as a Cloud Service]個の同等の機能にマッピングします。 そして、近代化への道を提案し、複雑さ、依存関係、実装の取り組みを評価します。
- **レポート** – 移行実行を計画するためのエクスポート可能なロードマップを作成します。これにより、関係者にリスクを伝えることができます。 また、優先事項、依存関係、技術的負債、導入リスクを特定します。

### 評価価値

評価の価値とは、開発の詳細を確定する前に得られる信頼性の量のことです。 定期的なスコープ設定を伴う移行を推定する代わりに、評価は実装に関するエビデンスに基づいた理解を提供します。 これには、移行が簡単なカスタマイズ、再設計が必要なカスタマイズ、完全に廃止できるカスタマイズなどが含まれます。 日常的に評価をおこなうことで、時代遅れの機能や未使用の機能を洗い出し、技術的負債を低減できます。

各レコメンデーションには、設計者とエンジニアが計画中に検証できる基礎となる実装に関する引用とともに、裏付けの証拠が含まれています。 あらゆる評価は同じ手法に従うため、一貫したスコアリングとプランニングのフレームワークにより、複数の開発ニーズを比較できます。

評価は単なる出発点ではありません。 下流移行ツールは、評価の結果を使用して、実装を加速し、承認された移行計画との一貫性を維持します。 カスタマイズ分析はアプリケーションの近代化のための設計図となり、データ評価では、データベースサイズ、エンティティインベントリ、カスタムテーブルを分析することで、データ移行の作業範囲を決定します。

### 評価範囲

移行評価ツールは、移行の全体像を把握することに重点を置いています。 カスタムモジュール、プラグイン、イベント、API、cron ジョブ、キュー、外部システムとの統合、ストアフロントの特性、およびそれらのカスタマイズが依存するデータベーススキーマを分析します。 この評価では、検出した内容を使用可能な[!DNL Adobe Commerce as a Cloud Service]機能にマッピングし、[!DNL App Builder]を使用してSaaS アーキテクチャの再設計や機能の近代化を行う場所を特定します。

評価は、実行ツールというよりも計画ツールです。 近代化する必要があるものを特定し、実装の複雑さを推定し、推奨事項を提供します。 導入に関する意思決定とアーキテクチャの検証は、引き続きAdobe、パートナー、カスタマーエンジニアリング部門の間で共同で行われます。

サードパーティの拡張機能によってカスタムテーブルに保存されたデータは、移行の検討として表示されます。 標準データ移行では、このデータは自動的に移行されません。 これらのシナリオをサポートするには、カスタム [!DNL App Builder] アプリケーションが必要になる場合があります。 詳しくは、[&#x200B; データ移行ガイド &#x200B;](#data-migration-commerce-data-migration-service)を参照してください。

この評価では、ストアフロントのカスタマイズとデータ移行ワークフローに対して次の分析を行います。

- コードとストアフロントの移行：評価のアプリケーション分析は、Commerce Developer MCPの設計図となります
- データ移行 – 評価のエンティティインベントリ、データベース特性分析、およびカスタムテーブル分析により、Commerce Data Migration Serviceの範囲が確立されます。

アプリケーションの変更に応じて評価を再実行することもできます。 これにより、チームは改善作業を検証し、近代化の進捗状況を測定し、エンゲージメント全体を通じて移行計画を継続的に改善できます。

### 次のステップ

すべての[!DNL Adobe Commerce as a Cloud Service]移行は評価から始まります。 これは、スコープを設定し、不確実性を減らし、実装を開始する前に共有された移行ブループリントを作成するための費用対効果の高い方法です。

評価ツールとダウンストリーム開発者ワークフローについて詳しくは、[Adobe Commerce Developer MCP](https://developer.adobe.com/commerce/extensibility/developer-agent/)を参照してください。

## コードとストアフロントの移行（Commerce Developer MCP）

[!DNL Adobe Commerce on Cloud]またはオンプレミスのカスタマイズでは、アプリケーション内で実行されるインプロセス PHP （モジュール、プラグイン、イベントオブザーバー）を使用できます。 [!DNL Adobe Commerce as a Cloud Service]はバージョンのないSaaS プラットフォームであり、そのモデルは適用されなくなります。 カスタマイズは、イベントとAPIを通じてCommerceと統合される、プロセス外の[!DNL Adobe Developer App Builder] アプリケーションとして実行されます。 このアーキテクチャのストアのカスタマイズを最新化することは、通常、[!DNL Adobe Commerce as a Cloud Service]移行で最も重要なエンジニアリング作業です。

### コード移行の概要

Commerce Developer MCPは、移行評価から始まり、従来のPHP カスタマイズを[!DNL App Builder]個のアプリケーションに近代化するための会話型IDE エクスペリエンスを提供します。 また、Edge Delivery Services（EDS）上のストアフロントの再構築についても支援します。 Commerce開発者MCPは、Migration Assessment Toolの調査結果を直接利用することで、手作業による解釈を減らし、トレーサビリティを維持し、プロセス全体の一貫性を確保することで、承認された移行ロードマップに沿った実装を維持します。

移行が主なユースケースですが、Commerce Developer MCPは、[!DNL Adobe Commerce]の包括的なAI開発エージェントとして設計されています。 MCPは、近代化、新しい開発、運用ワークフロー、およびすべての[!DNL Adobe Commerce as a Cloud Service]の更新をサポートしています。 このレベルの柔軟性により、移行後もCommerce アプリケーションの構築と拡張を継続することができます。

### Commerce Developer MCP

Commerce Developer MCPは、[移行評価](#migration-assessment-tool)の結果を使用して、識別されたカスタマイズを、反復的な開発ワークフローを通じて[!DNL App Builder]個のアプリケーションに変換します。 これらのツールを使用して開発する場合は、次のガイドラインを考慮してください。

- **設計図から始める** - Commerce Developer MCPは、特定されたカスタマイズ、レコメンデーション、移行優先度を実装計画の基盤として使用して、移行評価を利用します。

- **各カスタマイズを計画** – 各カスタマイズについて、Commerce Developer MCPは、推奨される[!DNL Adobe Commerce as a Cloud Service] アーキテクチャ、必要な統合パターン、およびプロセス外アプリケーションへの移行に必要な再設計を説明する仕様を作成します。

- **共同で構築** - Commerce Developer MCPは、最初にコードを生成するのではなく、実装の計画、アーキテクチャの議論、コードの生成と改良、推奨パターンの検証、デプロイメントガイダンスの提供を通じて、開発ライフサイクル全体を支援します。 開発者は、自然言語を通じて、生成された実装を反復的に改良できます。これにより、近代化の取り組み全体を通じて、プロジェクトの詳細を共同で改善できます。

  - 生成された実装は、エンジニアリングチームによる完全なレビュー可能、テスト可能、拡張可能な状態を維持しながら、配信を加速するように設計されています。

- **統合とデプロイ** - Commerce開発者MCPは、適切な統合パターンを通じてCommerceにアプリケーションを接続し、デプロイメントワークフローを支援し、デプロイメント前に推奨されるアーキテクチャパターンに照らし合わせて実装を検証します。これにより、一貫性が向上し、重複作業が削減されます。

  - Commerce Developer MCPには、[!DNL Adobe Commerce App Builder] MCPが含まれています。このMCPは、ドメインの知識、実装パターン、アーキテクチャのガイダンス、コンテクストに即した製品の専門知識、および検証されたコーディング手法を、開発ワークフローで直接提供します。 これにより、開発者がCommerce Developer MCPと直接作業する場合でも、Claude、Cursor、Copilotなどの他のエージェントと組み合わせて作業する場合でも、MCPの推奨事項がAdobeのベストプラクティスに沿ったものとなるようにします。

### ストアフロントの近代化

フロントエンドでは、Commerce Developer MCPが、Adobe Commerce ボイラープレート、ドロップインコンポーネント、EDS ブロックを使用して、Commerce用Edge Delivery Services（EDS）の[&#x200B; ストアフロント &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=ja)を最新化します。

Commerce Developer MCPは、Commerceのボイラープレートに基づいて、既存のストアフロントプロジェクトを読み込みます。 次のような方法でストアフロントを近代化できます。

- レスポンシブ EDS ブロックの生成
- Commerce対応ページデータの生成（ホーム、PLP、PDP、カート、チェックアウト、アカウント）
- ドロップインコンポーネントの作成と拡張
- デザインをEDS実装に変換する
- 従来のモノリシックなストアフロントをコンポーザブルなEDS ブロックアーキテクチャに変換する

MCPは、次のような機能も支援します。

- コンポーネントの近代化
- 再利用可能なブロック構成
- 顧客体験の最適化
- Edge Delivery Servicesの現在のベストプラクティスとの整合性

### 開発者のMCP値

処理中のPHPのカスタマイズから構成可能な[!DNL App Builder] アプリケーションに移行することは、大幅なアーキテクチャシフトを表します。 Commerce Developer MCPは、[!DNL Adobe Commerce]の知識、[!DNL App Builder]の実装パターン、および製品のベストプラクティスを開発ワークフローに直接埋め込むことで、そのギャップを埋めます。

このコンテキストを含めることで、配信速度とエンジニアリング品質の両方の一貫性が向上します。 チームは、一貫したアーキテクチャのガイダンスに従った実装を作成しながら、アプリケーションをより迅速に近代化できます。

Commerceの開発者MCPは、推奨される実装パターンを組み込むことで、個々の専門知識に対する依存度を減らし、プロジェクトをまたいで一貫性のある方法で近代化の取り組みを拡大するのに役立ちます。

移行プロセスは、既存の実装を改善する機会でもあります。 これにより、従来の技術的負債を回避して、従来のカスタマイズを簡素化し、古い機能を廃止し、SaaS機能を導入して、アプリケーションアーキテクチャを最新化できます。

Commerce開発者MCPは、移行評価を直接利用するため、あらゆる近代化の取り組みは、トレーサビリティを元の評価に戻し、実装が承認済みの移行ロードマップに沿ったものとなるようにします。

また、Commerce Developer MCPでは、ビジネス要件の変更に応じて個別に進化できるモジュール [!DNL App Builder] アプリケーションを奨励することで、コンポーザブルアプリケーションの設計を促進しています。

### 開発者MCP スコープ

バックエンドでは、Commerce Developer MCPが、PHP モジュール、プラグイン、イベントオブザーバーを[!DNL App Builder]個のアプリケーションに変換し、それらをAdobe Commerceに接続するための統合パターンを確立することで、カスタマイズと統合レイヤーを最新化します。 また、チェックアウト、決済、管理UIをまたいで、開発を迅速化できます。

フロントエンドでは、Commerce Developer MCP [がEdge Delivery Services上のCommerce ストアフロント &#x200B;](#storefront-modernization)を最新化します。

MCPはデータ移行を処理しません。 ビジネス データは、[Commerce Data Migration Service](#data-migration-commerce-data-migration-service)を通じて移行されます。 MCPは、ビジネスロジックまたはカスタムテーブルがアプリケーションの近代化を必要とする場合に必要な[!DNL App Builder] アプリケーションをサポートします。

### 次のステップ

コードとストアフロントの近代化は、移行評価ツールのロードマップで移行範囲と優先順位が確立された後に開始されます。

MCPのインストールと使用方法について詳しくは、[Commerce Developer MCP](https://developer.adobe.com/commerce/extensibility/developer-agent/)のドキュメントを参照してください。

## データ移行（Commerce Data Migration Service）

[!DNL Adobe Commerce as a Cloud Service]に移行するには、カタログ、注文、顧客、設定など、長年のデータを移行する必要があります。

Commerce Data Migration Serviceは、手作業による移行を、繰り返し可能な自動化された単一のプロセスに置き換えます。 複雑なデータベースの移行を、より予測可能かつ効率的におこなうことができます。

### Commerce Data Migration Service

移行では、Docker コマンドラインツール （`./bin/console migration`）によって実行されるガイド付きワークフローを使用します。 システム インテグレータまたはオペレーターは、ソースストアに対してこのワークフローを実行します。

コアデータの移行は自動化されますが、ほとんどの移行には非標準のスキーマ、拡張機能、エッジケースが含まれているため、すべての移行はソースストアの[評価](#migration-assessment-tool)から始まります。 資格情報と接続性の検証、移行の登録、検証ベースラインの確立を完了すると、データ移行を進めることができます。

移行サービスツールは、次のデータ管理手順を実行します。

1. **抽出して変換** — ソースからすべての関連データを並行して抽出し、[!DNL Adobe Commerce as a Cloud Service]用に再形成します。 互換性のないデータが除外され、カスタム属性やその他の構造が再マッピングされます。
1. **Load** – 抽出されたデータをCommerce Data Migration Serviceに転送します。 サービスはデータを[!DNL Adobe Commerce as a Cloud Service]に読み込み、インデックスを再構築し、カタログを取り込みます。
1. **Verify** — ソースデータとターゲットデータをデータベースレベルで比較します。 次に、サービスはストアフロントのGraphQLと管理者REST APIを通じてライブレコードのサンプルを検証し、データを検証します。
1. **レポート** – 各ステップの結果を最終的な移行レポートに統合します。

これらのデータを移動する段階にはメンテナンス期間が必要ですが、準備段階ではダウンタイムを最小限に抑えて稼働を維持します。

### 移行サービスの値

Commerce Data Migration Serviceは、証拠を使用することでデータの整合性を保持します。 あらゆる移行は、ソースとターゲットのデータを比較し、APIを通じてライブレコードのサンプルを検証することによって検証されます。 カスタム属性など、[!DNL Adobe Commerce as a Cloud Service]に完全にマッピングされないデータは、抽出中に自動的にフィルタリングされ、再マッピングされます。

移行サービスは、エンタープライズ規模のデータベース向けに設計されています。 データの移行は非同期でパーティション化および処理されるため、大規模なカタログや広範な注文履歴を確実に移行できます。 パイプラインの成長に合わせて、複数の移行を並行して実行できます。 移行が中断された場合、移行は最後に完了したステージから再開され、停止したジョブが検出され、自動的に再試行されます。

ダウンタイムは、次の方法で最小化されます。

- 作業の大部分は、実店舗が稼働している間に実行されます。つまり、最後のカットオーバーのみがメンテナンスウィンドウを必要とします。
- データ移行では、移行する必要のないテーブルとレコードを非常に効率的な直接SQLの読み取りおよび書き込みおよびスキップします。

移行では、Adobe インフラストラクチャを通じて本番データを移動するので、パス全体が保護されます。

- すべてのアップロードは、ターゲットに到達する前にマルウェアをスキャンします
- 取り込み層は、ファイルタイプを検証し、安全でないデータベース操作をブロックします
- あらゆるリクエストは、Adobe IMSとゲートウェイの署名の検証を使用して認証されます

Commerce Data Migration Serviceは世界中の本番環境で稼働しており、既に複数のエンタープライズレベルの移行を提供しています。

### カスタムデータとサードパーティデータ

移行サービスでは、ファーストパーティのコアコマースデータのみがサポートされます。 移行サービスは、カスタムのサードパーティエンティティを処理しません。

サードパーティデータはケースごとに移行できるため、Docker抽出ツールに対応するカスタマイズが必要です。 カスタムツールを作成した後、データをソースから抽出し、[!DNL App Builder]またはサードパーティのデータベースに書き込むことができます。

各拡張機能はデータを異なる方法でモデル化するため、サードパーティデータの移行パスは、ソースストレージとターゲットストレージのスキーマと場所を決定した後でのみ設計できます。 サードパーティデータの移行は、スコーピングの時間を確保するために、早期に特定する必要があります。

### 次のステップ

移行の準備ができたら、[&#x200B; データ移行スコープに関するアンケート &#x200B;](../assets/data-migration-scoping-questionnaire.xlsx)を完了します。このアンケートには、ソーストポロジ、エンティティの範囲、ボリューム、コンプライアンスの制約、カットオーバーの仕組み、移行の計画に必要な[&#x200B; カスタムテーブル &#x200B;](#custom-and-third-party-data)が必要です。 このアンケートを完了すると、Adobeで環境を評価し、移行ウィンドウを計画できるようになります。

ワークフロー、サポートされているデータ、検証について詳しくは、[一括データ移行ツール ガイド &#x200B;](bulk-data/migration-tool.md)のドキュメントを参照してください。

ソース環境を準備するシステムインテグレーターは、標準の[Adobe Commerce Cloud CLI](https://experienceleague.adobe.com/ja/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-overview)と[Adobe Developer Console](https://developer.adobe.com)をIMS資格情報に使用することもできます。
