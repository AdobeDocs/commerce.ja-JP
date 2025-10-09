---
title: 拡張機能のコーディングツール
description: AI ツールを使用してCommerce App Builder拡張機能を作成する方法を説明します。
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
role: Architect
hide: true
hidefromtoc: true
source-git-commit: 6d2debaeefd65d273c1e0e92f9a7b03740b11520
workflow-type: tm+mt
source-wordcount: '1422'
ht-degree: 0%

---

# 拡張機能のコーディングツール

[!DNL Adobe Commerce as a Cloud Service] に移行する際には、AI コーディングツールを使用して、既存の [!DNL Adobe Commerce] PHP 拡張機能を [!DNL Adobe Developer App Builder] 拡張機能に変換できます。 また、新しい [!DNL App Builder] 拡張機能の作成にも使用できます。

AI コーディングツールを使用すると、次のような利点があります。

* **開発ワークフローの強化**：統合されたAdobe Commerce開発ツールです。
* **AI を利用した支援**：コンテキスト認識コードの生成とデバッグ。
* **Commerce固有の機能**: Adobe Commerce App Builder開発用の専用ツールです。
* **自動ワークフロー**：開発およびデプロイメントプロセスを合理化します。

## 前提条件

* [&#x200B; カーソル &#x200B;](https://cursor.com/download)
* [Node.js](https://nodejs.org/en/download):LTS バージョン
* パッケージマネージャー：[npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) または [yarn](https://classic.yarnpkg.com/lang/en/docs/install/#mac-stable)
* [Git](https://github.com/git-guides/install-git)：リポジトリのクローン作成とバージョン管理の場合

## インストール

1. 最新の [Adobe I/O CLI](https://github.com/adobe/aio-cli) をグローバルにインストールします。

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. [Adobe I/O CLI Commerce プラグイン &#x200B;](https://github.com/adobe-commerce/aio-cli-plugin-commerce) をインストールします。

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
   ```

1. Commerceのクローン [&#x200B; 統合スターターキット &#x200B;](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration):

   ```bash
   git clone git@github.com:adobe/commerce-integration-starter-kit.git
   ```

1. スターターキット ディレクトリに移動します。

   ```bash
   cd commerce-integration-starter-kit
   ```

1. インタラクティブなセットアップコマンドを実行して、Commerce AI 拡張ツールをインストールします。

   ```bash
   aio commerce extensibility tools-setup
   ```

セットアッププロセスにより、設定オプションが表示されます。 設定場所として「現在のディレクトリ」を選択し、現在のワークスペースにツールをインストールします。

```terminal
? Where would you like to setup the tools?
❯ Current directory
  New directory
```

Adobeでは、パッケージマネージャーを選択する場合、一貫性を確保するために `npm` を使用することをお勧めします。

```terminal
? Which package manager would you like to use?
❯ npm
  yarn
```

1. コーディングツールを正常にインストールした後、インストールプロセスによって以下が設定されます。

   * Adobe Commerce開発用の MCP サーバーの統合
   * 開発エクスペリエンスを向上させるためのカーソル IDE ルール
   * Commerce固有の開発ツールとワークフロー

   以下のファイルがワークスペースに追加されます。

   * MCP 構成：`.cursor/mcp.json`
   * 規則ディレクトリ：`.cursor/rules/`

## インストール後の設定

1. カーソル IDE を再起動して、新しい MCP ツールと設定をロードします。

1. `.cursor/rules/` フォルダーの下にルールが存在することを確認して、インストールを検証します。

1. MCP サーバを有効にします。

   * **Cmd+Shift+P** （macOS）または **Ctrl+Shift+P** （Windows および Linux）を使用して、Cursor MCP Settings を開きます。
   * **表示：MCP 設定を開く** と入力します
   * リストで **commerce-extensibility MCP Server** を見つけます
   * サーバー **オン** を切り替えて、コーディングツールを有効にします

1. サーバーステータスの確認 – Commerce拡張機能 MCP サーバーは次のように表示されます。

   ```terminal
   Status: Connected/Active
   Server: commerce-extensibility
   Configuration: Automatically configured via .cursor/mcp.json
   ```

## サンプルプロンプト

次のサンプルプロンプトでは、注文時に通知を送信する拡張機能を作成します。

```terminal
Implement an Adobe Commerce SaaS extension that will send an ERP notification when a customer places an order. The ERP notification must be sent as a POST HTTP call to <ERP URL> with the following details in the request JSON body:

Order ID -> orderID
Order Total -> total
Customer Email ID -> emailID
Payment Type -> pType
```

## ベストプラクティス

Adobeでは、AI コーディングツールを使用する際に、次のベストプラクティスに従うことをお勧めします。

### Checklist

開発セッションを開始する前に、以下を行います。

* `REQUIREMENTS.md` をチェック
* MCP ツールが動作していることを確認
* 現在のフェーズと目標のレビュー
* サンプルコードまたは基礎モードのプロジェクトから開始

開発中：

* 4 段階の [&#x200B; プロトコル &#x200B;](#protocol) を信頼する
* 複雑な開発のための実装計画の要求
* 利用可能な場合は MCP ツールを使用
* 実装後の各機能のテスト
* 最初にローカルでテストしてから、デプロイして再度テストします
* サポートをテストするためのコーディングツールの活用
* 不必要な複雑さに疑問を呈する
* 増分デプロイして開発を迅速化

新しいチャットを開始する場合：

* 適切なセッションハンドオフの提供
* `@` を使用したキーファイルの参照
* セッションの明確な目標の設定
* フェーズ ベースの境界を使用する

### ワークフロー

AI コーディングツールを使用して開発する場合は、まずサンプルコードまたは基礎モードのプロジェクトを使用します。 このアプローチにより、AI 開発ワークフローを最適化しながら、何もから始めるのではなく、強固な基盤の上に構築できるようになります。

また、これにより、Adobeのテンプレートを活用し、確立されたディレクトリ構造と規則を維持しながら、実証済みのパターンとアーキテクチャに基づいて構築できます。

使用を開始するには、次のリソースを参照してください。

* [&#x200B; 統合スターターキット &#x200B;](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration)
* [Adobe Commerce スターターキット テンプレート &#x200B;](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit)
* [Adobe I/O Events スターターテンプレート &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-learn/tutorials/adobe-developer-app-builder/io-events/getting-started-io-events)
* [App Builder サンプルアプリケーション &#x200B;](https://developer.adobe.com/app-builder/docs/resources/sample_apps)

#### これらのリソースを使用する理由

* **実証済みのパターン**：スターターキットは、Adobeのベストプラクティスとアーキテクチャに関する意思決定を具体化しています
* **迅速な開発**：ボイラープレートと設定に費やす時間を短縮します
* **一貫性**：確立された規則に従って拡張機能が動作することを確認します
* **メンテナンス性**：標準パターンに従うと、メンテナンスと更新が容易になります
* **ドキュメント**：スターターキットには、例とドキュメントが付属しています
* **コミュニティサポート**：標準的なアプローチを使用すると、支援を受けやすくなります
* **AI コンテキストの効率性**：使い慣れたパターンや構造を使用して操作することで、広範な説明の必要性を減らし、コード生成の精度を向上させます
* **トークンの使用量の削減**：すべてをゼロから生成するのではなく、既存のパターンを参照することで、会話の効率が向上し、コンテキストの要約が少なくなります

### プロトコル

次の 4 段階のプロトコルが、規則システムによって自動的に適用されます。 ツールは、拡張機能を開発する際に、次のプロトコルに自動的に従う必要があります。

* フェーズ 1：要件の分析と説明
   * 質問を明確にしたら、完全な回答を提供します。
* フェーズ 2：アーキテクチャ計画とユーザー承認
   * プランを提示する際は、承認する前に慎重にレビューします。
* フェーズ 3：コードの生成と実装
* フェーズ 4：ドキュメント化と検証

### 複雑な開発のための実装計画の要求

複数の実行時アクション、タッチポイントまたは統合が関与する複雑な開発の場合、AI ツールに詳細な実装計画の作成を明示的にリクエストします。 複数のコンポーネントを含む [&#x200B; フェーズ 2](#protocol) の全体的な計画を確認したら、詳細な実装計画を求めて、管理可能なタスクに分類します。

```terminal
Create a detailed implementation plan for this complex development.
```

複雑なAdobe Commerce拡張機能には、多くの場合、次のものが含まれます。

* 複数の実行時アクション
* 複数のタッチポイントをまたいだイベント設定
* 外部システムとの統合
* 州の管理要件
* 複数のコンポーネントでのテスト

### MCP ツールの使用

このツールはデフォルトで MCP ツールに設定されていますが、状況によっては CLI コマンドを使用することもできます。 MCP ツールを確実に使用するには、プロンプトで明示的にリクエストします。

CLI コマンドが使用されていて、代わりに MCP ツールを使用する場合は、次のプロンプトを使用します。

```terminal
Use only MCP tools and not CLI commands
```

* MCP ツール：aio-app-deploy、aio-app-dev、aio-dev-invoke
* CLI コマンド：aio アプリのデプロイ、aio アプリの開発

CLI コマンドは、次のシナリオで使用できます。

* 複雑なデプロイメントシナリオ
* デバッグの具体的な問題
* MCP ツールに制限がある場合
* MCP 統合のメリットを受けない 1 回限りの操作

### 開発

AI ツールによって作成される不必要な複雑さに疑問を投げかけることが重要です。

単純な読み取り専用エンドポイントに不要なファイル（`validator.js`、`transformer.js`、`sender.js`）を追加する場合は、次のプロンプトを使用します。

```terminal
Why do we need these files for a simple read-only endpoint?
Perform a root cause analysis before adding complexity
Verify if simpler solutions exist
```

### テスト

テスト時には次のベストプラクティスを使用します。

#### 実装後の各機能のテスト

実装計画での機能の開発が完了したら、直ちにテストします。 早期テストを行うことで、複合的な問題を防ぎ、デバッグを容易にすることができます。

* すべての機能が完了するまで待たない
* 増分的にテストして、問題を早期に検出します
* 次の機能に移行する前に機能を検証

#### 最初にローカルテスト

必ず、最初に `aio-app-dev` ツールを使用してローカルでテストしてください。 これにより、すぐにフィードバックが得られ、イテレーションサイクルの短縮、デバッグの容易化、デプロイメントのオーバーヘッドの発生がありません。

1. ローカル開発 サーバの起動：

   ```bash
   aio-app-dev
   ```

1. アクションをローカルでテスト：

   ```bash
   aio-dev-invoke action-name --parameters '{"test": "data"}'
   ```

#### デプロイして再度テストします

ローカルテストが正常に完了したら、ランタイム環境にデプロイしてテストします。 ランタイム環境は、ローカル開発とは動作が異なる場合があります。

1. ランタイムにデプロイ：

   ```bash
   aio-app-deploy
   ```

1. デプロイ済みアクションのテスト

1. Web ブラウザーまたはダイレクト HTTP リクエストの使用

1. デバッグ用にアクティブ化ログを確認する

#### サポートをテストするためのコーディングツールの活用

テストに関するヘルプを求めます。 ツールは、デバッグ、ログ分析および特定の実行時アクションに適したテストデータの作成に役立ちます。

**実行時アクションをテスト**:

```terminal
Help me test the customer-created runtime action running locally
```

**デバッグの失敗**:

```terminal
Why did the subscription-updated runtime action activation fail?
```

**ログを確認**:

```terminal
Help me check the logs for the last stock-monitoring runtime action invocation
```

**テストペイロードの作成**:

```terminal
Generate test data for this Commerce event
```

```terminal
Create a test payload for the customer_save_after event
```

**ランタイム エンドポイントの検索**:

```terminal
What's the URL for this deployed action?
```

**認証の処理**:

```terminal
How do I authenticate with this external API?
```

**トラブルシューティング**:

```terminal
Help me debug why this action is returning 500 errors
```

### デバッグ

何か問題が起こったら立ち止まって評価しなさい。 問題が発生した場合：

* 停止して評価 – 壊れた状態で続行しないでください
* ログを確認 – 有効化ログを使用して問題を特定します
* シンプル：複雑さを排除して問題を切り分ける
* 増分テスト – 一度に 1 つの問題を修正
* 検証 – 続行する前に各修正をテストします

### デプロイメント

をデプロイする際は、次のベストプラクティスを使用します。

#### 増分的にデプロイ

変更したアクションのみをデプロイして、開発を高速化します。 これにより、既存の機能が中断されるリスクが軽減され、変更に関するフィードバックが迅速になります。 また、既存の機能を中断するリスクも軽減します。

* MCP ツールを使用した特定のアクションのデプロイ

  ```bash
  aio-app-deploy --actions action-name
  ```

* ローカルテスト後に個々のアクションをデプロイ
* 段階的に導入し、開発時にアプリケーションの完全な導入を回避

#### 実行時のクリーンアップ

大きな変更を加えた後、ツールを活用して、孤立したアクションをクリーンアップします。 AI ツールでクリーンアッププロセスを体系的に処理できるので、孤立したアクションを効率的に特定し、ステータスを確認し、手動の介入なしで安全に削除できます。

```terminal
Help me identify and clean up orphaned runtime actions
```

AI ツールをリクエストして、デプロイ済みのアクションをリストし、未使用のアクションを特定する

```terminal
List all deployed actions and identify which ones are no longer needed
```

適切なコマンドを使用して、AI ツールに孤立したアクションを削除させる

```terminal
Remove the orphaned actions that are no longer part of the current implementation
```

### 監視

アプリケーションを監視する際は、次のベストプラクティスを使用します。

#### コンテキスト品質指標を監視

* **良好なコンテキスト**:AI は最近の決定を記憶し、正しいファイルを参照します
* **悪いコンテキスト**:AI が、以前に提供した情報を要求し、解決された問題を繰り返す

#### 開発速度の追跡

* **高速**：明確な進捗、必要な明確な説明は最小限
* **低速**：説明の繰り返し、AI の混乱、緩慢な進行

#### コスト効率の監視

トークン使用パターンの追跡：

* **効率的**：トークンの使用率が低く、コンテキストの要約がほとんどない
* **非効率的**：トークンの使用率が高い、複数の要約、繰り返し作業

## 回避すべき内容

AI コーディングツールを使用する場合は、次のアンチパターンを避ける必要があります。

* **説明フェーズをスキップしない** – 必ず、実装の前にフェーズ 1 が完了するようにします。
* **各機能の後はテストをスキップしないでください** – 増分的にテストし、すべてが完了するまで待たないでください。
* **根本原因分析なしに複雑さを追加しない** – 不要なファイル追加に疑問を呈し、適切な調査を依頼します。
* **実際のデータテストを行わずに成功を宣言しないでください** - エッジケースだけでなく、常に実際のデータを使用してテストします。
* **実行時のクリーンアップを忘れないでください** – 大きな変更の後で、孤立したアクションを常にクリーンアップします。
