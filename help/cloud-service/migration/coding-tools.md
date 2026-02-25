---
title: Adobe Commerce App Builderの AI コーディング開発者ツール
description: AI ツールを使用してCommerce App Builder アプリケーションを作成する方法を説明します。
feature: App Builder, Cloud
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
role: Developer
level: Intermediate
source-git-commit: 4e3f593ead4b0e32bdf474498421b20475dcbe52
workflow-type: tm+mt
source-wordcount: '2470'
ht-degree: 0%

---

# Adobe Commerce App Builderの AI コーディング開発者ツール

[!DNL Adobe Commerce as a Cloud Service] に移行する際には、AI コーディングツールを使用して、既存の [!DNL Adobe Commerce] PHP 拡張機能を [!DNL Adobe Developer App Builder] アプリケーションに変換できます。 また、これらのツールを使用して、新しい [!DNL App Builder] アプリケーションを作成することもできます。

AI コーディングツールには次の利点があります。

* **開発ワークフローの強化**：統合されたAdobe Commerce開発ツールです。
* **AI を利用した支援**：コンテキスト認識コードの生成とデバッグ。
* **Commerce固有の機能**: Adobe Commerce App Builder開発用の専用ツールです。
* **自動ワークフロー**：開発およびデプロイメントプロセスを合理化します。

AI コーディングツールをインストールすると、以下にアクセスできます。

* スキル – アプリケーションの開発をガイドし、情報を提供するために設計された、Adobe CommerceおよびApp Builder固有のスキルセット。
* 開発者 MCP サーバー
* App Builder MCP サーバー

## 最新バージョンへの更新

[AI コーディング開発者ツールをインストール &#x200B;](#installation) した後、次のコマンドを実行して、最新バージョンに更新できます。

```bash
aio commerce extensibility tools-setup
```

ツールが最新バージョンに更新されます。

## 前提条件

* 次のような [&#x200B; エージェントスキル &#x200B;](https://agentskills.io/home#adoption) をサポートするコーディングエージェント。

   * [&#x200B; カーソル &#x200B;](https://cursor.com/download)
   * [&#x200B; コードをクロード &#x200B;](https://www.claude.com/product/claude-code)
   * [GitHub コパイロット &#x200B;](https://github.com/features/copilot)
   * [&#x200B; ウィンドサーフ &#x200B;](https://windsurf.com)
   * [Gemini CLI](https://github.com/google-gemini/gemini-cli)
   * [OpenAI Codex](https://openai.com/index/introducing-codex/)
   * [&#x200B; クライン &#x200B;](https://cline.bot)

* [Node.js](https://nodejs.org/en/download):LTS バージョン
* パッケージマネージャー：[npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) または [yarn](https://classic.yarnpkg.com/lang/en/docs/install/#mac-stable)
* [Git](https://github.com/git-guides/install-git)：リポジトリのクローン作成とバージョン管理の場合

## インストール

>[!NOTE]
>
>AI コーディングツールパッケージ全体ではなく、ドキュメント RAG サービスのみをインストールする場合は、[&#x200B; ドキュメント RAG サービス &#x200B;](./doc-rag.md) を参照してください。

1. 最新の [Adobe I/O CLI](https://github.com/adobe/aio-cli) をグローバルにインストールします。

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. 次のプラグインをインストールします。

   * [Adobe I/O CLI Commerce](https://github.com/adobe-commerce/aio-cli-plugin-commerce)
   * [Adobe I/O CLI ランタイム &#x200B;](https://github.com/adobe/aio-cli-plugin-runtime)
   * [App Builder CLI](https://github.com/adobe/aio-cli-plugin-app-dev)

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime
   ```

1. 次のいずれかのクローンを作成します。

   * Commerce[&#x200B; 統合スターターキット &#x200B;](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration) - バックオフィス統合を構築するためのキット。

     ```bash
     git clone git@github.com:adobe/commerce-integration-starter-kit.git
     ```

   * Commerce[&#x200B; チェックアウトスターターキット &#x200B;](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/) で、支払い、送料、税金などのチェックアウトエクスペリエンスを構築または拡張します。

     ```bash
     git clone git@github.com:adobe/commerce-checkout-starter-kit.git
     ```

1. スターターキット ディレクトリに移動します。

   ```bash
   cd commerce-integration-starter-kit
   ```

1. インタラクティブなセットアップコマンドを実行して、Commerce AI 拡張ツールをインストールします。

   ```bash
   aio commerce extensibility tools-setup
   ```

   セットアッププロセスにより、設定オプションが求められます。 画面の指示に従って、インストールを完了します。 ツールは選択したディレクトリにインストールされます。

   * プロジェクトに使用するスターターキットを選択します。

     ```shell-session
     ? Which starter kit would you like to use?
     ❯ Integration starter kit
        Checkout starter kit
     ```

   * 好みのコーディングエージェントを選択します。 40 を超えるコーディングエージェントがサポートされていますが、好みのエージェントが表示されない場合は、`Other` のオプションを使用して、任意のコーディングエージェントのスキルをインストールできます。 スキルを設定する手順については、コーディングエージェントのドキュメントを参照してください。

     ```shell-session
     ? Which coding agent would you like to install skills for?
     ❯ Cursor
        Claude Code
        GithubCopilot
        Windsurf
        Gemini CLI
        OpenAI Codex
        Cline
        ...
     ```

   * NPM または Yarn がインストールされているかどうかをインストーラが検出し、自動的に適切な選択を行います。 ただし、どちらもインストールされていない場合は、パッケージマネージャーを選択するように求められます。Adobeでは、一貫性を保つため `npm` を使用することをお勧めします。

     ```shell-session
     ? Which package manager would you like to use?
     ❯ npm
        yarn
     ```

1. コーディングツールを正常にインストールした後、インストールプロセスによって以下が設定されます。

   * Adobe Commerce開発用の MCP サーバーの統合
   * 開発経験の向上に役立つ [&#x200B; エージェントスキル &#x200B;](#skills)
   * Commerce固有の開発ツールとワークフロー

   これで、スキルと MCP ツールがインストールされました。 スキルと MCP ツールが表示されない場合は、コーディングエージェントを再起動します。

>[!NOTE]
>
>プロジェクトをデプロイする前に、次の設定タスクを完了する必要があります。
>
>* Adobe I/O CLI を使用して [0&rbrace;Adobe Developer Console&rbrace; にログインします。](https://developer.adobe.com/console)
>* App Builder プロジェクトを作成します（「[&#x200B; プロジェクト設定 &#x200B;](https://developer.adobe.com/commerce/extensibility/events/project-setup) を参照）。
>* `.env` ファイルで環境変数を設定します。
>
>これらの設定手順を手動で完了することも、AI コーディングツールを利用してプロセスをガイドすることもできます。 設定手順について詳しくは、[&#x200B; 統合の作成 &#x200B;](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration/) を参照してください。

## インストール後の設定

### Adobe I/O CLI にログインします。

[!DNL Adobe I/O CLI] をインストールした後、MCP サーバを使用する場合は常にログインする必要があります。

```bash
aio auth login
```

ログインしていることを確認するには、次のコマンドを実行します。

```bash
aio where
```

問題が発生した場合は、ログアウトしてからログインし直してください。

```bash
aio auth logout
aio auth login
```

>[!NOTE]
>
>MCP サーバの一部の機能はログインしなくても動作しますが、RAG （Retrieval-Augmented Generation）サービスは動作しません。 RAG サービスは、Adobe Commerceの完全なドキュメントセットにリアルタイムでアクセスできる AI コーディングエージェントを提供し、現在のCommerceの開発手法、API、アーキテクチャパターンに基づいて質問に答え、コードを生成できるようにします。
>
>RAG サービスを個別にインストールするには、[&#x200B; ドキュメント RAG サービス &#x200B;](./doc-rag.md) を参照してください。

### カーソル

1. カーソル IDE を再起動して、新しい MCP ツールと設定をロードします。

1. `.cursor/skills/` フォルダーにスキルが存在することを確認して、インストールを検証します。

1. MCP サーバを有効にします。

   * **Cmd+Shift+P** （macOS）または **Ctrl+Shift+P** （Windows および Linux）を使用して、Cursor MCP Settings を開きます。
   * **表示：MCP 設定を開く** と入力します
   * リストで **commerce-extensibility MCP Server** を見つけます
   * サーバー **オン** を切り替えて、コーディングツールを有効にします

1. サーバーステータスの確認 – Commerce拡張機能 MCP サーバーは次のように表示されます。

   ```shell-session
   Status: Connected/Active
   Server: commerce-extensibility
   Configuration: Automatically configured via .cursor/mcp.json
   ```

1. 次のプロンプトを使用して、エージェントが MCP サーバを使用しているかどうかを確認します。 表示されない場合は、エージェントに対して、使用可能な MCP ツールを使用するように明示的に依頼します。

   ```shell-session
   What are the differences between Adobe Commerce PaaS and Adobe Commerce as a Cloud Service when configuring a webhook that activates an App Builder runtime action?
   ```

### コパイロット

1. Visual Studio Code を再起動して、新しい MCP ツールと設定を読み込みます。

1. `copilot-instructions.md` ファイルが `.github` フォルダーに存在することを確認して、インストールを検証します。

1. MCP サーバを有効にします。

   * 左側のサイドバーのアクティビティバーにある **拡張機能** アイコンをクリックするか、**Cmd+Shift+X** （macOs）または **Ctrl+Shift+X** （Windows および Linux）を使用して、拡張機能パネルを開きます。
   * [[!UICONTROL **MCP SERVERS - INSTALLED**]] をクリックします。
   * [!UICONTROL **commerce-extensibility MCP Server**] の横にある歯車アイコンをクリックし、サーバーが停止している場合は [!UICONTROL **サーバーを起動**] を選択します。
   * 歯車アイコンをもう一度クリックし、「[!UICONTROL **出力を表示**]」を選択します。

1. サーバーステータスを確認します。 `MCP:commerce-extensibility` の出力は、次のようになります。

   ```shell-session
   2025-11-13 12:58:50.652 [info] Starting server commerce-extensibility
   2025-11-13 12:58:50.652 [info] Connection state: Starting
   2025-11-13 12:58:50.652 [info] Starting server from LocalProcess extension host
   2025-11-13 12:58:50.657 [info] Connection state: Starting
   2025-11-13 12:58:50.657 [info] Connection state: Running
   
   (...)
   
   2025-11-13 12:58:50.753 [info] Discovered 10 tools
   ```

1. 次のプロンプトを使用して、エージェントが MCP サーバを使用しているかどうかを確認します。 表示されない場合は、エージェントに対して、使用可能な MCP ツールを使用するように明示的に依頼します。

   ```shell-session
   What are the differences between Adobe Commerce PaaS and SaaS when configuring a webhook that activates an App Builder runtime action?
   ```

## サンプルプロンプト

次のプロンプト例では、統合スターターキットを使用して、注文時に通知を送信するアプリケーションを作成しています。

```shell-session
Implement an Adobe Commerce SaaS application that will send an ERP notification when a customer places an order. The ERP notification must be sent as a POST HTTP call to <ERP URL> with the following details in the request JSON body:

Order ID -> orderID
Order Total -> total
Customer Email ID -> emailID
Payment Type -> pType
```

次のプロンプト例では、チェックアウトスターターキットを使用して、カスタムの発送方法を提供するアプリケーションを作成します。

```shell-session
Implement an Adobe Commerce SaaS application that provides custom shipping methods.
The extension should:
1. Return shipping options based on the destination postal code
2. If postal code is in California, add an "Express California" option for $15
3. If postal code is outside US, add an "International Standard" option for $25
4. The carrier code should be "MYSHIP"
```



## プロンプトコマンド

プロンプトに加えて、`/search-commerce-docs` コマンドを使用して、エージェントとの会話でドキュメントを検索できます。 例：

```shell-session
/search-commerce-docs "How do I subscribe to Commerce events?"
```

## スキル

コーディングエージェントとチャットすると、スキルが自動的に呼び出されますが、次のコマンドを使用して手動で呼び出すこともできます。

* `/architect` - [!DNL App Builder] と選択したスターターキットを使用して、Adobe Commerce Extensions のアーキテクチャを設計します。 統合の計画、イベントの選択、データフローの設計またはアーキテクチャの決定を行う際に使用します。
* `/developer` - パターンとファイル構造に従って、Adobe Commerce[!DNL App Builder] 拡張子を実装します。 コードの生成、設定ファイルの更新または実行時アクションの実装の際に使用します。
* `/devops-engineer` – 拡張機能をデプロイして操作 [!DNL App Builder] ます。 アプリケーションのデプロイ、環境の設定、デプロイメントの問題のトラブルシューティング、CI/CD の設定またはオンボーディングエラーの解決の際に使用します。
* `/product-manager` - Adobe Commerce Extensions の要件を収集および文書化します。 新しいプロジェクトを開始する際、受け入れ基準を定義する際、ビジネス目標を明確にする際、ドキュメントを作成する際 `REQUIREMENTS.md` 使用します。
* `/technical-writer` - [!DNL App Builder] アプリケーションに関する包括的なドキュメントを作成します。 `README.md`、ユーザーガイド、API ドキュメント、changelogs を記述する際や、ドキュメントの完全性を確保する際に使用します。
* `/tester` - [!DNL App Builder] アプリケーションの包括的なテストを作成します。 単体テストの記述、統合テスト、セキュリティの検証、コード品質とカバレッジの保証の際に使用します。
* `/tutor` （試験的） – 明確な説明と例 [!DNL Adobe Commerce] 使用して、アプリケーション開発の概念を教えます。 [!DNL App Builder] を学習する際、イベントを理解する際、開発パターンに関するガイダンスが必要な際に使用します。

## ベストプラクティス

Adobeでは、AI コーディングツールを使用する際に、次のベストプラクティスに従うことをお勧めします。

### プランモード

コーディングエージェントとチャットする場合は、**プラン** モードを選択して、プロジェクトの詳細な実装計画を作成する必要があります。

**プラン** モードを選択する方法は、使用しているエージェントによって異なります。 手順については、エージェントのマニュアルを参照してください。 例：

* [&#x200B; カーソル &#x200B;](https://cursor.com/docs/agent/modes)
* [&#x200B; コードをクロード &#x200B;](https://code.claude.com/docs/en/common-workflows#when-to-use-plan-mode)
* [Gemini CLI](https://geminicli.com/docs/cli/plan-mode/)

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
* [&#x200B; スターターキットをチェックアウト &#x200B;](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/)
* [Adobe Commerce スターターキット テンプレート &#x200B;](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit)
* [Adobe I/O Events スターターテンプレート &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/io-events/getting-started-io-events)
* [App Builder サンプルアプリケーション &#x200B;](https://developer.adobe.com/app-builder/docs/resources/sample_apps)

#### これらのリソースを使用する理由

* **実証済みのパターン**：スターターキットは、Adobeのベストプラクティスとアーキテクチャに関する意思決定を具体化しています
* **迅速な開発**：ボイラープレートと設定に費やす時間を短縮します
* **一貫性**：確立された規則に従ってアプリケーションが実行されるようにします
* **メンテナンス性**：標準パターンに従うと、メンテナンスと更新が容易になります
* **ドキュメント**：スターターキットには、例とドキュメントが付属しています
* **コミュニティサポート**：標準的なアプローチを使用すると、支援を受けやすくなります
* **AI コンテキストの効率性**：使い慣れたパターンや構造を使用して操作することで、広範な説明の必要性を減らし、コード生成の精度を向上させます
* **トークンの使用量の削減**：すべてをゼロから生成するのではなく、既存のパターンを参照することで、会話の効率が向上し、コンテキストの要約が少なくなります

### プロトコル

次の 4 段階のプロトコルは、インストールされたスキルによって自動的に適用されます。 ツールは、アプリケーションを開発する際に、次のプロトコルに自動的に従う必要があります。

* フェーズ 1：要件の分析と説明
   * 質問を明確にしたら、完全な回答を提供します。
* フェーズ 2：アーキテクチャ計画とユーザー承認
   * プランを提示する際は、承認する前に慎重にレビューします。
* フェーズ 3：コードの生成と実装
* フェーズ 4：ドキュメント化と検証

### 複雑な開発のための実装計画の要求

複数の実行時アクション、タッチポイントまたは統合が関与する複雑な開発の場合、AI ツールに詳細な実装計画の作成を明示的にリクエストします。 複数のコンポーネントを含む [&#x200B; フェーズ 2](#protocol) の全体的な計画を確認したら、詳細な実装計画を求めて、管理可能なタスクに分類します。

```shell-session
Create a detailed implementation plan for this complex development.
```

複雑なAdobe Commerce アプリケーションには、多くの場合、次のものが含まれます。

* 複数の実行時アクション
* 複数のタッチポイントをまたいだイベント設定
* 外部システムとの統合
* 州の管理要件
* 複数のコンポーネントでのテスト

### MCP ツールの使用

>[!NOTE]
>
>MCP ツールを使用する前に、[Adobe I/O CLI にログイン &#x200B;](#log-in-to-the-adobe-io-cli) していることを確認します。

このツールはデフォルトで MCP ツールに設定されていますが、状況によっては CLI コマンドを使用できます。 MCP ツールを確実に使用するには、プロンプトで明示的にリクエストします。

CLI コマンドが使用されていて、代わりに MCP ツールを使用する場合は、次のプロンプトを使用します。

```shell-session
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

AI ツールによって作成される不必要な複雑さに疑問を投げかけます。

単純な読み取り専用エンドポイントに不要なファイル（`validator.js`、`transformer.js`、`sender.js`）を追加する場合は、次のプロンプトを使用します。

```shell-session
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

```shell-session
Help me test the customer-created runtime action running locally
```

**デバッグの失敗**:

```shell-session
Why did the subscription-updated runtime action activation fail?
```

**ログを確認**:

```shell-session
Help me check the logs for the last stock-monitoring runtime action invocation
```

**テストペイロードの作成**:

```shell-session
Generate test data for this Commerce event
```

```shell-session
Create a test payload for the customer_save_after event
```

**ランタイム エンドポイントの検索**:

```shell-session
What's the URL for this deployed action?
```

**認証の処理**:

```shell-session
How do I authenticate with this external API?
```

**トラブルシューティング**:

```shell-session
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

変更したアクションのみをデプロイして、開発を高速化します。 このアプローチは、既存の機能が中断されるリスクを軽減し、変更に関するフィードバックを迅速に提供します。

* MCP ツールを使用した特定のアクションのデプロイ

  ```bash
  aio-app-deploy --actions action-name
  ```

* ローカルテスト後に個々のアクションをデプロイ
* 段階的に導入し、開発時にアプリケーションの完全な導入を回避

#### 実行時のクリーンアップ

大きな変更を加えた後、ツールを活用して、孤立したアクションをクリーンアップします。 AI ツールでクリーンアッププロセスを体系的に処理できます。 孤立したアクションを効率的に特定し、そのステータスを確認し、手動の介入なしで安全に削除できます。

```shell-session
Help me identify and clean up orphaned runtime actions
```

AI ツールをリクエストして、デプロイ済みのアクションをリストし、未使用のアクションを特定する

```shell-session
List all deployed actions and identify which ones are no longer needed
```

適切なコマンドを使用して、AI ツールに孤立したアクションを削除させる

```shell-session
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

AI コーディングツールを使用する場合は、次のアンチパターンを使用しないでください。

* **説明フェーズをスキップしない** – 必ず、実装の前にフェーズ 1 が完了するようにします。
* **各機能の後はテストをスキップしないでください** – 増分的にテストし、すべてが完了するまで待たないでください。
* **根本原因分析なしに複雑さを追加しない** – 不要なファイル追加に疑問を呈し、適切な調査を依頼します。
* **実際のデータテストを行わずに成功を宣言しないでください** - エッジケースだけでなく、常に実際のデータを使用してテストします。
* **実行時のクリーンアップを忘れないでください** – 大きな変更の後で、孤立したアクションを常にクリーンアップします。

## フィードバックの提供

AI コーディングツールに関するフィードバックを提供することに関心がある開発者は、`/feedback` コマンドを使用できます。

このコマンドを使用すると、テキストのフィードバックを提供したり、ログをAdobeに送信したりできます。 送信したログは、個人情報や個人情報を削除するためにサニタイズされます。

>[!TIP]
>
>ユーザーエクスペリエンスは、使用している IDE によって若干異なります。 次のプロセスでは、Cursor でのエクスペリエンスについて説明します。

1. エージェントに `/feedback` と入力し、`commerce-extensibility/feedback` コマンドを選択します。

1. IDE の上部に表示される「**フィードバック**」フィールドにツールのフィードバックを入力し、**Enter** キーを押します。

   ![&#x200B; カーソルフィードバックコマンド入力フィールド &#x200B;](../assets/feedback-response.png){width="600" zoomable="yes"}

1. **ローカルに保存** フィールドで、`yes` または `no` と入力し、**Enter** キーを押して、ログのローカルコピーを保存するかどうかを指定します。

   ![&#x200B; カーソルフィードバックコマンドの「ローカルに保存」フィールド &#x200B;](../assets/feedback-save.png){width="600" zoomable="yes"}

   **はい** を選択した場合、フィードバックを送信した後に `chats` フォルダーのログを確認できます。

1. `commerce-extensibility/feedback` コマンドがエージェントのチャット入力フィールドに表示されます。 **Enter** キーを押すか **送信** をクリックして、フィードバックをAdobeに送信します。

>[!NOTE]
>
>`/feedback` コマンドが表示されない場合は、[&#x200B; 最新バージョンにアップデート &#x200B;](#updating-to-the-latest-version) する必要があります。
