---
title: チュートリアルの前提条件
description: 拡張機能やストアフロント開発ツールなど、Adobe Commerce as a Cloud Service チュートリアルの前提条件と設定手順について説明します。
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
source-git-commit: 0ece7b58bdafd664297cbdee809c53ef2389fb12
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 0%

---

# チュートリアルの前提条件

このページでは、[!DNL Adobe Commerce as a Cloud Service]評価の拡張機能チュートリアル [や](./ratings-extension.md)配送方法の拡張機能チュートリアル [など、](./shipping-method-extension.md) チュートリアルの前提条件と設定手順について説明します。

## 一般的な前提条件

このチュートリアルでは、拡張機能とストアフロントの両方の開発に次のツールが必要です。

* [!DNL Node.js] （バージョン `22.x.x`）およびnpm （`9.0.0`以降）：次のコマンドを使用してインストールを確認します。

  ```bash
  node --version
  npm --version
  ```

* [Git](https://git-scm.com)をインストールします – インストールを確認します：

  ```bash
  git --version
  ```

* バッシュシェル
   * macOS/Linux：インストールは不要
   * Windows: [Git Bash](https://git-scm.com/install)または[Windows Subsystem for Linux （WSL） &#x200B;](https://learn.microsoft.com/en-us/windows/wsl/install)を使用

* [&#x200B; カーソル &#x200B;](https://cursor.com/download)などのAI支援IDEのダウンロード（推奨）。 Claude Code、Gemini CLI、Copilotなどの他のIDEもサポートされていますが、チュートリアルのプロンプトやその他の手順の変更が必要になる場合があります。

## [!DNL Adobe Commerce as a Cloud Service]の前提条件

* [!DNL Adobe I/O CLI]をインストール

  ```bash
  npm install -g @adobe/aio-cli
  ```

* [Adobe I/O CLI Commerce](https://github.com/adobe-commerce/aio-cli-plugin-commerce)、[Adobe I/O CLI Runtime](https://github.com/adobe/aio-cli-plugin-runtime)および[App Builder CLI](https://github.com/adobe/aio-cli-plugin-app-dev) プラグインをインストールします。

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime
  ```

[!DNL Adobe I/O CLI]と必要なプラグインをインストールしたら、拡張性ワークスペースを設定します。 Adobeでは、最速のエクスペリエンスを得るために自動セットアップを使用することをお勧めします。

* **[自動セットアップ &#x200B;](#automated-setup) （推奨）** – 単一のコマンドを実行して、ワークスペースを自動的に設定します。
* **[手動設定](#manual-setup)** – 各コンポーネントを個別に設定するには、手順に従います。

### 自動設定（推奨） {#automated-setup}

>[!TIP]
>
>自動設定で問題が発生した場合は、以下の[手動設定](#manual-setup)手順に従ってください。

`app-setup` コマンドは、[!DNL Adobe Developer Console] プロジェクトの作成、必要なAPIの追加、[!DNL Adobe I/O CLI]の設定、スターターキットの複製、ローカルワークスペースの接続、拡張性AI ツールのインストールなど、ワークスペースの設定プロセスを自動化します。

`app-setup` コマンドを使用すると、次の手順を実行できます。

* 必要なAPIを使用した[!DNL Adobe Developer Console] プロジェクトの選択または作成
* 組織、プロジェクト、ワークスペースを使用した[!DNL Adobe I/O CLI]の設定
* 適切なスターターキットを複製し、プロジェクトを設定する
* 環境を設定し、ローカルワークスペースをリモートワークスペースに接続する
* Commerce拡張ツールとコーディングエージェントのスキルのインストール

次のコマンドを実行し、インタラクティブなプロンプトに従います。

```bash
aio commerce extensibility app-setup
```

コマンドが完了したら、プロジェクトディレクトリに移動し、コーディングエージェントを再起動して、新しいMCP ツールとスキルを読み込みます。 チュートリアルでストアフロントが必要な場合は、コマンドを再実行し、[!DNL AEM Boilerplate Commerce] スターターキットを選択します。

次のインストール例は、チェックアウトスターターキットのインタラクティブなプロンプトと出力を示しています。

+++インストール例（チェックアウトスターターキット）

```shell-session
aio commerce extensibility app-setup

🚀 Adobe Commerce Extensibility App Setup

✔ Logged in
📁 Working directory: /Users/username/projects/my-commerce-project

✔ Which starter kit would you like to use? Checkout Starter Kit
✔ Enter a name for your project directory: my-extension
✔ Which coding agent would you like to install the skills for? Cursor

📦 Cloning Checkout Starter Kit...
   ✔ Repository cloned
   Using npm (package-lock.json found)
   ✔ Dependencies installed

📋 Current Adobe I/O Console configuration:
   Org: My Organization (1234567)
   Project: My Commerce Project (1234567890123456789)
   Workspace: Stage (9876543210987654321)
✔ Do you want to continue with this configuration? (Answer "No" to select a different org/project/workspace)
No

🔧 Selecting Adobe I/O Console org, project, and workspace...

? Select Org: My Organization
Org selected My Organization
You are currently in:
1. Org: My Organization
2. Project: <no project selected>
3. Workspace: <no workspace selected>

? Select Project: My Commerce Project
Project selected : My Commerce Project
You are currently in:
1. Org: My Organization
2. Project: My Commerce Project
3. Workspace: <no workspace selected>

? Select Workspace: Stage
Workspace selected Stage
You are currently in:
1. Org: My Organization
2. Project: My Commerce Project
3. Workspace: Stage

✅ Console configured:
   Org: My Organization
   Project: My Commerce Project
   Workspace: Stage

🔐 Configuring workspace credentials and services...
   ✔ Workspace configuration loaded
   ✔ OAuth server-to-server credentials already configured
   ✔ All required services available in organization
   ✔ Subscribed to: Adobe Commerce as a Cloud Service

📋 Configuring Checkout Starter Kit...
   Creating .env from env.dist...
✔ Select tenant (type to search) My Commerce Instance:
https://<region>.api.commerce.adobe.com/<tenant-id>/graphql
   ✔ Commerce instance configured
✔ Enter the event prefix for your workspace: my-prefix
   ✔ Workspace IDs configured
   ✔ OAuth credentials configured
   ✔ Checkout Starter Kit configured

🔧 Installing Commerce Extensibility tools and agent skills...
   ✔ Commerce Extensibility tools installed

🎉 App setup complete!

📁 Project directory: /Users/username/projects/my-commerce-project/my-extension

Next steps:
   1. cd into your project directory
   2. Restart your coding agent to load the Commerce Extensibility tools and skills
```

+++

### 手動設定 {#manual-setup}

次の節では、拡張性ワークスペースの各コンポーネントを手動で設定する方法について説明します。 手動設定を希望する場合、または[自動設定](#automated-setup)で問題が発生した場合は、次の手順に従います。

### Adobe Developer Consoleの前提条件

必要なAPIと資格情報を使用して、Adobe Developer Consoleでプロジェクトを設定します。

1. [Adobe Developer Console](https://developer.adobe.com/console){target="_blank"}に移動します。
1. メールアドレスとパスワードを使用してログインします。

#### 新しいプロジェクトの作成

Adobe Developer ConsoleでApp Builder プロジェクトを作成し、拡張機能をホストします。

1. [Adobe Developer Console](https://developer.adobe.com/)に移動します。
1. **[!UICONTROL Create project from a template]**&#x200B;をクリックします。
1. **[!UICONTROL App Builder]** テンプレートを選択します。
1. **[!UICONTROL Project Title]**&#x200B;と&#x200B;**[!UICONTROL App Name]**&#x200B;を入力します。
1. 「**[!UICONTROL Include Runtime]**」チェックボックスがマークされていることを確認します。

   ![App Builder テンプレートを選択したAdobe Developer Console プロジェクトの作成](../assets/app-builder-template.png){width="600" zoomable="yes"}

1. **[!UICONTROL Save]**&#x200B;をクリックします。

#### ワークスペースへのAPIの追加

イベント管理とCommerceの統合のために、必要なAPIをステージワークスペースに追加します。

1. **[!UICONTROL Stage]** ワークスペースをクリックし、各APIについて次の手順を繰り返します。

   ![APIの「サービスを追加」オプションを使用したステージングワークスペース &#x200B;](../assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. **[!UICONTROL Add Service]**&#x200B;をクリックし、**[!UICONTROL API]**&#x200B;を選択します。

1. 次のいずれかのAPIを選択します。 以下に示す各APIについて、このプロセスを繰り返します。

   * **[!UICONTROL Adobe Services]** フィルター：
      * **[!UICONTROL I/O Management API]**
      * **[!UICONTROL I/O Events]** API
   * **[!UICONTROL Experience Cloud]** フィルター：
      * **[!UICONTROL Adobe I/O Events for Adobe Commerce]** API

1. **[!UICONTROL Next]**&#x200B;をクリックします。

1. **[!UICONTROL Save configured API]**&#x200B;をクリックします。

1. すべてのAPIをワークスペースに追加するまで、前の手順を繰り返します。

   ![必要なすべてのAPIが正常に追加されたことを示すWorkspace](../assets/apis-added.png){width="600" zoomable="yes"}

### Adobe I/O CLIの設定

組織、プロジェクト、ワークスペースに[!DNL Adobe I/O CLI]を接続します。

1. 既存の設定をすべて消去します。

   ```bash
   aio config clear
   ```

1. [!DNL Adobe I/O CLI]を使用してログインします。

   ```bash
   aio auth login -f
   ```

1. 次の各コマンドを使用して、組織、プロジェクト、ワークスペースを選択します。

   ```bash
   aio console org select
   ```

   ```bash
   aio console project select
   ```

   ```bash
   aio console workspace select
   ```

   ![Adobe I/O CLI組織プロジェクトとワークスペースの選択を示すターミナル &#x200B;](../assets/cli-configuration.png){width="600" zoomable="yes"}

### スターターキットの複製

次のいずれかのCommerce スターターキットリポジトリを、構築およびプロジェクトの準備に使用する拡張機能に複製します。

統合スターターキット：

```bash
git clone https://github.com/adobe/commerce-integration-starter-kit.git extension
cd extension
```

チェックアウトスターターキット：

```bash
git clone https://github.com/adobe/commerce-checkout-starter-kit.git extension
cd extension
```

>[!BEGINTABS]

>[!TAB 統合スターターキット ]

### .env ファイルの作成

環境設定ファイルを作成します。

```bash
cp env.dist .env
```

テキストエディターで`.env` ファイルを開き、次のOAuth資格情報を追加します。

```bash
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

ワークスペースの「**[!UICONTROL Credential details]**」タブをクリックして、[Developer Console](https://developer.adobe.com/)の&#x200B;**[!UICONTROL OAuth Server-to-Server]** ページからこれらの値をコピーします。

Adobe Developer Console![の](../assets/oauth-credentials.png){width="600" zoomable="yes"}OAuth サーバー間の資格情報ページ

#### Commerce設定の追加

次のCommerce インスタンスの詳細を`.env` ファイルに追加します。

```bash
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

これらの値を検索するには：

1. [Commerce Cloud サービスインスタンス &#x200B;](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances)に移動します。
1. インスタンスの横にある情報アイコンをクリックします。
1. REST エンドポイントを`COMMERCE_BASE_URL`としてコピーします。
1. GraphQL エンドポイントを`COMMERCE_GRAPHQL_ENDPOINT`としてコピーします。

#### イベント接頭辞の設定

イベント接頭辞に一時的な値を設定します。

```bash
EVENT_PREFIX=test
```

### ワークスペース設定のダウンロード

次のコマンドを実行して、ワークスペース設定ファイルをダウンロードします。

```bash
aio console workspace download workspace.json
```

ワークスペース設定ファイルを`scripts` ディレクトリにコピーします。

```bash
cp workspace.json scripts/
```

### ローカルワークスペースをリモートワークスペースに接続する

ローカルプロジェクトをリモートワークスペースにリンクします。

```bash
aio app use workspace.json -m
```

![aio アプリ使用コマンドでワークスペース接続が成功したことを示すターミナル &#x200B;](../assets/connect-workspace.png){width="600" zoomable="yes"}

>[!TAB  チェックアウトスターターキット ]

### ローカルワークスペースをリモートワークスペースに接続する

ローカルプロジェクトをリモートワークスペースにリンクします。 プロジェクトのルート（`extension` フォルダー）から、次を実行します。

```bash
aio app use --merge
```

プロンプトが表示されたら、Adobe I/O CLIの設定時に選択した組織、プロジェクト、ワークスペースを使用するオプションを選択します。 これにより、デプロイとローカル開発がそのワークスペースを使用するように、ワークスペース設定がアプリに書き込まれます。

![aio アプリ使用コマンドでワークスペース接続が成功したことを示すターミナル &#x200B;](../assets/connect-workspace.png){width="600" zoomable="yes"}

>[!ENDTABS]

### 拡張可能なAI ツールの導入

このプロセスにより、MCP設定（`.<agent>/mcp.json`）、スキルディレクトリ（`.<agent>/skills/`）が作成され、プロジェクトのルートに`AGENTS.md`が追加されます。 スターターキット、コーディングエージェント、パッケージマネージャーを選択するよう求められます。


1. 次のコマンドを使用して、`extension` フォルダーにAI支援の開発ツールを設定します。

   ```bash
   cd extension
   ```

   ```bash
   aio commerce extensibility tools-setup
   ```

   ![AI拡張ツールのセットアップ コマンド出力を表示している端末](../assets/install-ai-tools.png){width="600" zoomable="yes"}

1. 設定が完了したら、コーディングエージェントを再起動して、新しいMCP ツールとスキルを読み込めるようにします。 Commerce App Builder ツールが、お客様の環境で使用できるようになりました。

   >[!NOTE]
   >
   >スターターキットにスキルが見つからないという警告が表示された場合、何らかの問題が発生しました。多くの場合、セットアップはスターターキットがクローンされた場所以外のフォルダーで実行されたためです。 `aio commerce extensibility tools-setup` フォルダー（スターターキットプロジェクトのルート）から`extension`を実行し、プロンプトが表示されたら適切なスターターキットを選択します。

   ![&#x200B; チェックアウトスターターキットを選択した状態でAI拡張性ツールのセットアップを表示している端末](../assets/tools-setup-checkout.png){width="600" zoomable="yes"}

## Storefrontの手動設定

この節では、[評価の拡張機能チュートリアル &#x200B;](./ratings-extension.md)およびその他のストアフロントチュートリアル用にストアフロントを手動で設定する方法について説明します。

ストアフロントを自動的に設定するには、`app-setup`Automated setup[&#x200B; セクションで説明されている](#automated-setup) コマンドを実行し、[!DNL AEM Boilerplate Commerce] スターターキットを選択します。

### 前提条件

[評価の拡張機能チュートリアル &#x200B;](./ratings-extension.md#connect-to-the-storefront)の[&#x200B; ストアフロント &#x200B;](./ratings-extension.md) セクションを完了し、ストアで製品の評価を表示するには、次の項目が必要です。

* [Google Chrome](https://www.google.com/chrome/) - ストアフロントのテストに必要

* [!DNL Commerce] インスタンスに接続されたストアフロントプロジェクト。 ストアフロントプロジェクトがない場合は、[&#x200B; ストアフロントを作成](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/){target="_blank"}の手順に従います。これには、[&#x200B; コマースデータへのリポジトリのリンク &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#link-repo-to-commerce-data){target="_blank"}の節が含まれます。

### ストアフロントリポジトリの複製

ターミナルを開き、リポジトリを複製します。

```bash
git clone https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

### 依存関係のインストール

プロジェクトの依存関係をインストールします。

```bash
npm install
```

### ストアフロント AI ツールのインストール

`storefront` フォルダーでAI支援の開発ツールを設定します。

ボイラープレートプロジェクトのルートから次のコマンドを実行します。 このコマンドは、`@adobe-commerce/commerce-extensibility-tools` パッケージを開発依存関係としてインストールし、スキルファイルを担当者のスキルディレクトリにコピーし、担当者がCommerce ドキュメント検索ツールにアクセスできるようにMCP （Model Context Protocol）を設定します。

```bash
aio commerce extensibility tools-setup
```

このコマンドは、次の2つのプロンプトを示します。

1. **スターターキットを選択** — **AEM定型Commerce**&#x200B;を選択します。

1. **コーディングエージェントを選択** – サポートされているエージェントのリストからエージェントを選択します。
