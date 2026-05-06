---
title: ' [!DNL Adobe Commerce] と [!DNL Adobe LLM Optimizer]の統合'
description: ' [!DNL Adobe Commerce] から [!DNL Adobe LLM Optimizer] に接続して、LLMのカタログシグナルを監視し、承認済みのカタログ最適化をデプロイします。'
role: Admin, User, Leader
recommendations: noCatalog
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# [!DNL Adobe Commerce]と[!DNL Adobe LLM Optimizer]の統合

>[!IMPORTANT]
>
>この統合へのアクセスは制限されています。 詳しくは、テクニカルアカウントマネージャーにお問い合わせください。

[!DNL Adobe LLM Optimizer]は、大規模言語モデル （LLM）とAI アシスタントからの回答で、コンテンツがどのように表示されるかを監視、分析、最適化するのに役立つエンタープライズ ソリューションです。 LLM Optimizerを利用すれば、調査や商品の発見のために、AI ツールを利用する顧客が増えるにつれて、ブランドとカタログが正確に引用され、コンテクストに沿って表示されるようになります。

このガイドでは、商品カタログがCommerceに保存されている場合に、**[!DNL Adobe Commerce]**&#x200B;がそのワークフローにどのように適合するかを説明します。 利用可能になる機能、必要な設定、管理者および取り込みチャネル間でのデプロイされた最適化の動作について説明します。

>[!NOTE]
>
>[!DNL Adobe LLM Optimizer]はスタンドアロン Adobe ソリューションです。 コア監視および商談ワークフローには、[!DNL Adobe Experience Manager] （AEM）またはその他のAdobe アプリケーションは必要ありません。 Commerce固有のデプロイアクションは、カタログがLLM Optimizerに接続され、承認済みの変更を[!DNL Adobe Commerce]にプッシュする場合にのみ適用されます。

## 統合によって可能になること {#what-integration-enables}

LLM Optimizerを[!DNL Adobe Commerce] カタログに接続すると、広範なコンテンツインサイトから&#x200B;**カタログ対応**&#x200B;のレコメンデーションに移行できます。

- **タイトル、説明、構造化シグナルなど、LLMによる製品の解釈方法に影響するカタログデータのギャップと不整合を**&#x200B;特定します。
- **レビュー**&#x200B;は、ジャスティフィケーションと前後の比較を含む、サポートコンテキストによる改善を提案しました。
- 製品名や説明の更新など、**選択した最適化を** Commerce カタログに直接デプロイすると、管理者のワークフロー、グリッド、ストアフロントに対応するデータが常に整合します。

カタログソースが[!DNL Adobe Commerce]の場合、Adobeは完全なエンドツーエンドのワークフローをサポートできます。自動的に商談を特定し、変更を提案し、承認済みの修正を適用します。 Commerce以外で作成されたカタログの場合、LLM Optimizerは引き続き改善を分析して提案できますが、変更の適用は統合モデル（例えば、カタログのミラーリングや手動アップデート）によって異なります。 [統合制限と境界](boundaries-limits.md)を参照してください。

## 対象 {#who-this-is-for}

- **デジタルマーケターおよびマーチャンダイザー**&#x200B;は、LLM主導の回答で製品データが正確かつ一貫性を持つようにしたいと考えています。また、カタログコピーを大規模に改善するための管理された方法を必要としている人です。
- カタログの整合性、管理プロセス、および製品属性をフィードする統合（API、CSV、PIM）を所有する&#x200B;**Commerce管理者**。

## 前提条件 {#prerequisites}

Adobe LLM OptimizerとのAdobe Commerce統合に&#x200B;**アクセス**&#x200B;がある場合は、次の前提条件が適用されます。 詳しくは、テクニカルアカウントマネージャーにお問い合わせください。

- ストアフロントはLLM向けおよびエージェント型ボットでクロールできます。このクロール機能は、LLM Optimizer測定および最適化戦略の一部です（カタログ対応インサイトの一般的な前提条件）。
- Commerceに基づくデプロイワークフローの場合、必要なCommerce サービスとカタログ接続が有効になり、正常に動作します。 タスクレベルの設定については、[Adobe CommerceとLLM Optimizerの接続](get-started/connect-to-llmo.md)を参照してください。

また、システム間でデータがどのように移動するのかも理解する必要があります。

### 高レベルのデータフロー {#high-level-data-flow}

概念的には、カタログの最適化は2つのパターンに従います（機能に応じて、プロジェクトでは1つまたは両方を使用します）。

| 方向 | 目的 |
| --- | --- |
| **Commerce カタログ -> LLM Optimizer** | カタログとURL シグナルが、LLM Optimizer UIでの商談と提案に反映されます。 |
| **LLM Optimizer -> Commerce** | デプロイアクションを承認すると、製品名と説明の更新がメインのCommerce カタログに書き込まれ、管理者とストアフロントの両方に最適化された値が反映されます。 |

### [!DNL Adobe Commerce]とサードパーティのカタログの比較 {#commerce-vs-third-party}

| カタログソース | LLM Optimizerの一般的なカバレッジ |
| --- | --- |
| **[!DNL Adobe Commerce]** | IDと提案の強力なサポートに加えて、設定した承認済みカタログフィールド更新のデプロイが可能です。 |
| **サードパーティのコマース** | 識別と提案がサポートされます。加盟店システムへの自動デプロイは、加盟店のソースカタログへの直接書き込みではなく、エクスポート、ミラーリング、またはパートナーのワークフローによって異なります。 |

## Catalog Agent、Storefront MCP、およびLLM Optimizer {#catalog-agent-and-mcp}

お客様の[!DNL Adobe Commerce] **製品カタログ**&#x200B;は、製品データの記録システム（名前、説明、属性、価格設定、在庫）です。 AIを活用した発見と最適化を強化するために、**Adobe Commerce Storefront MCP** （モデルコンテキストプロトコル）は、ライブのCommerce カタログデータとAdobe AI エクスペリエンスの間の構造化インターフェイスです。

**カタログエージェント**&#x200B;は、ストアフロント MCPの上に配置されています。 カタログエージェントを使用すると、[!DNL Adobe LLM Optimizer]は、ギャップを特定し、改善を提案し、承認時に変更をデプロイすることで、カタログおよびPDP コンテキストのクエリ、エンリッチ、アクションを実行できます。 これらの機能は、[LLM OptimizerとAdobe Commerceの併用](get-started/use-llmo-with-commerce.md)に記載されているLLM Optimizer ワークフローに表示されます。

## Catalog AgentによるLLM向けCommerceの改善 {#catalog-agent-optimizations}

カタログエージェントは、製品詳細ページの充実と製品カタログの充実という2つの補完的な最適化を通じて、見つけやすさに対処します。

### 製品詳細ページの強化 {#pdp-enrichment-overview}

**商品詳細ページ （PDP） エンリッチメント**&#x200B;では、商品ページのコンテンツの改善を提案しています。これにより、買い物客がAI アシスタントや類似ツールを通じて商品を見つけたときに、商品がより明確に読み取れるようになります。 目標は、既にマーチャンダイジングしているストアフロントのレイアウトを変更することなく、明瞭性と一貫性を高めることです。 LLM Optimizerで提案を確認し、準備ができたらデプロイします。

デプロイ後、ライブの製品ページを抜き取って、ショッピング体験が期待どおりに表示されることを確認します。

### 製品カタログの強化 {#catalog-enrichment-overview}

**製品カタログの強化**&#x200B;は、コピーが薄い、曖昧な、または一貫性のない、より明確な&#x200B;**製品名**&#x200B;と&#x200B;**製品説明**&#x200B;を提案します。 提案にはそれぞれコンテキストが含まれているため、何を変更するのかをチームが決定することができます。 更新を承認すると、更新を[!DNL Adobe Commerce] カタログに適用できるので、これらのフィールドを使用する管理者、ストアフロント、およびその他のエクスペリエンスに同じ文言が反映されます。

これらのフィールドはCommerceに保存されているため、一度だけ名前または説明を変更すると、その商品データを読み込むあらゆるチャネルにメリットをもたらします（システムの更新方法とタイミングによって異なります）。

## 関連トピック {#related-topics}

- [Adobe CommerceとLLM Optimizerの連携](get-started/connect-to-llmo.md)
- [Adobe CommerceでのLLM Optimizerの使用](get-started/use-llmo-with-commerce.md)
- [統合の制限と境界](boundaries-limits.md)
