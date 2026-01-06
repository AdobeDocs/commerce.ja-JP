---
title: 評価拡張機能チュートリアルの前提条件
description: 評価拡張機能のラボの前提条件について説明します。
feature: App Builder, Cloud
role: Developer
level: Intermediate
hide: true
hidefromtoc: true
source-git-commit: 4ca909c2f8f95fbc404ce6a745d769958b2c01f4
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# 評価の拡張チュートリアルの前提条件（Beta）

>[!NOTE]
>
>このチュートリアルで使用する AI ツールは、現在Betaにあり、バグやその他の問題が含まれている可能性があります。

このページでは、[!DNL Adobe Commerce as a Cloud Service] 評価拡張機能チュートリアル [ など、](./ratings-extension.md) のチュートリアルの前提条件と設定手順を示します。

## Adobe Commerce as a Cloud Serviceの前提条件

* [!DNL Adobe I/O CLI] のインストール

  ```bash
  npm install -g @adobe/aio-cli
  ```

* [Adobe I/O CLI Commerce](https://github.com/adobe-commerce/aio-cli-plugin-commerce)、[Adobe I/O CLI ランタイム ](https://github.com/adobe/aio-cli-plugin-runtime)、[App Builder CLI](https://github.com/adobe/aio-cli-plugin-app-dev) プラグインをインストールします。

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime
  ```

* [Cursor](https://cursor.com/download) （推奨）などの AI を利用した IDE のダウンロード、Claude Code、Gemini CLI、Copilot などの他の IDE もサポートされていますが、チュートリアルのプロンプトやその他の手順の変更が必要になる場合があります。

### Adobe Developer Consoleの前提条件

1. [Adobe Developer Console](https://developer.adobe.com/console){target="_blank"} に移動します。
1. メールとパスワードを使用してログインします。

#### 新規プロジェクトの作成

1. [Adobe Developer Console](https://developer.adobe.com/) に移動します。
1. [!UICONTROL **テンプレートからプロジェクトを作成**] をクリックします。
1. [!UICONTROL **App Builder**] テンプレートを選択します。
1. [!UICONTROL **プロジェクトタイトル**] および [!UICONTROL **アプリ名**] を入力します。
1. 「**[!UICONTROL Include Runtime]**」チェックボックスがオンになっていることを確認します。

   ![App Builder テンプレートを選択したAdobe Developer Console プロジェクトの作成 ](../assets/app-builder-template.png){width="600" zoomable="yes"}

1. [!UICONTROL **保存**] をクリックします。

#### ワークスペースへの API の追加

1. [!UICONTROL **ステージング**] ワークスペースをクリックし、各 API に対して次の手順を繰り返します。

   ![API の「サービスを追加」オプションを使用したステージワークスペース ](../assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. [!UICONTROL **サービスを追加**] をクリックし、「[!UICONTROL **API**]」を選択します。

1. 次のいずれかの API を選択します。 以下に示す各 API に対して、このプロセスを繰り返す必要があります。

   * [!UICONTROL **Adobe サービス**] フィルター：
      * [!UICONTROL **I/O Management API**]
      * [!UICONTROL **I/O イベント**] API
   * [!UICONTROL **Experience Cloud**] フィルター：
      * [!UICONTROL **Adobe Commerce用Adobe I/O Events**] API

1. [!UICONTROL **次へ**] をクリックします。

1. 「[!UICONTROL **設定済み API を保存**]」をクリックします。

1. すべての API がワークスペースに追加されるまで、前の手順を繰り返します。

   ![ 必要なすべての API が正常に追加されたことを示すWorkspace](../assets/apis-added.png){width="600" zoomable="yes"}

### Adobe I/O CLI の設定

1. 既存の設定を消去します。

   ```bash
   aio config clear
   ```

   [!DNL Adobe I/O CLI] を使用してログイン：

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

   ![Adobe I/O CLI の組織プロジェクトとワークスペースの選択を示すターミナル ](../assets/cli-configuration.png){width="600" zoomable="yes"}

### 統合スターターキットのクローン

Commerce統合スターターキットリポジトリーのクローンを作成し、プロジェクトを準備します。

```bash
git clone https://github.com/adobe/commerce-integration-starter-kit.git extension
cd extension
```

![Commerce統合スターターキットの Git clone コマンドを示すターミナル出力 ](../assets/clone-starter-kit.png){width="600" zoomable="yes"}

### .env ファイルの作成

環境設定ファイルを作成します。

```bash
cp env.dist .env
```

`.env` ファイルをテキストエディターで開き、次の OAuth 資格情報を追加します。

```shell-session
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

これらの値は、ワークスペースの「**[!UICONTROL Credential details]**」タブをクリックして、[Developer Console](https://developer.adobe.com/) の **[!UICONTROL OAuth Server-to-Server]** ページからコピーできます。

![Adobe Developer Consoleの OAuth サーバー間資格情報ページ ](../assets/oauth-credentials.png){width="600" zoomable="yes"}

#### Commerce設定を追加

`.env` ファイルに次のCommerce インスタンスの詳細を追加します。

```shell-session
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

これらの値を検索するには：

1. [Commerce Cloud サービスインスタンス ](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances) に移動します。
1. インスタンスの横にある「情報」アイコンをクリックします。
1. REST エンドポイントを `COMMERCE_BASE_URL` としてコピーします。
1. GraphQL エンドポイントを `COMMERCE_GRAPHQL_ENDPOINT` としてコピーします。

#### イベントのプレフィックスを設定

イベントプレフィックスに一時的な値を設定します。

```shell-session
EVENT_PREFIX=test
```

### ワークスペース設定のダウンロード

次のコマンドを実行して、ワークスペース設定ファイルをダウンロードします。

```bash
aio console workspace download workspace.json
```

ワークスペース設定ファイルを `scripts` ディレクトリにコピーします。

```bash
cp workspace.json scripts/
```

### ローカルワークスペースのリモートワークスペースへの接続

ローカルプロジェクトをリモートワークスペースにリンクします。

```bash
aio app use workspace.json -m
```

![aio app use コマンドでワークスペース接続が成功したことを示すターミナル ](../assets/connect-workspace.png){width="600" zoomable="yes"}

### 拡張 AI ツールのインストール

Cursor ルール ファイルと MCP 設定を更新して、`commerce-extensibility-tools` パッケージを含めます。

1. 次のコマンドを使用して、`extension` フォルダー内に AI 支援開発ツールを設定します。

   ```bash
   cd extension
   ```

   ```bash
   aio commerce extensibility tools-setup
   ```

   ![AI 拡張ツール設定コマンド出力を示すターミナル ](../assets/install-ai-tools.png){width="600" zoomable="yes"}
<!--
## Storefront prerequisites

The following items are required to complete the [storefront](./ratings-extension.md#connect-to-the-storefront) section of [this tutorial](./ratings-extension.md) and see the product ratings in your store.

* Install [!DNL Node.js] (version `22.x.x`) and npm (`9.0.0` or higher). Verify your installation:

   ```bash
   node --version
   npm --version
   ```

* Install [Git](https://git-scm.com) (Optional) - Required only if [cloning the repository directly](#option-a-clone-the-repository-recommended)(recommended), not needed if you [download the zip file](#option-b-download-the-zip-file). Verify your installation:

  ```bash
  git --version
  ```

* Bash shell
  * macOS/Linux: No installation required
  * Windows: Use [Git Bash](https://git-scm.com/install) or [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install)

* [Google Chrome](https://www.google.com/chrome/) - Required for testing the storefront

### Get the project files

You can obtain the project files using one of the following methods:

#### Option A: Clone the repository (recommended)

If you have [!DNL Git] installed, open your terminal and clone the repository:

```bash
git clone --branch agentic-dev https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

#### Option B: Download the zip file

If you do not have [!DNL Git] installed:

1. Download the project zip file from: [https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip](https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip)
1. Extract the zip file to a folder on your machine.
1. Open your terminal and navigate into the unzipped folder:

   ```bash
   cd path/to/aem-boilerplate-commerce-agentic-dev
   ```

### Install root dependencies

Install the main project dependencies:

```bash
npm install
```

This will install all the necessary packages for the storefront application.

### Install MCP server dependencies

Navigate to the MCP server directory and install its dependencies:

```bash
cd mcp-server
npm install
cd ..
```

### Configure environment variables

The MCP server requires certain environment variables to connect to the RAG service.

Create an `.env` file in the `mcp-server` directory:

```bash
cd mcp-server
cp env.example .env
```

Edit the `.env` file and add the following values:

```env
RAG_MODE=worker
WORKER_RAG_URL=
```

### Enable MCP in Cursor

The Model Context Protocol (MCP) server provides AI agents with access to [!DNL Adobe Commerce] Storefront documentation.

#### Open Cursor MCP settings

![Open Cursor MCP Settings](../assets/cursor-mcp-settings.png){width="600" zoomable="yes"}

1. Open [!DNL Cursor].
1. Navigate to **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**.

#### Enable and configure MCP features

The project includes an MCP configuration file at `.cursor/mcp.json`. This file should already be configured to use the local MCP server.

Verify the MCP configuration:

1. Ensure the "commerce-documentation-rag" server is listed and enabled

The configuration should look similar to this:

![MCP Configuration](../assets/mcp-configuration.png){width="600" zoomable="yes"}

>[!NOTE]
>
>The `start-mcp.sh` script will automatically load the environment variables from your `.env` file in the `mcp-server` directory.

#### Restart Cursor

After enabling MCP and configuring the server:

1. Quit [!DNL Cursor] completely.
1. Reopen [!DNL Cursor] and open the `aem-boilerplate-commerce` project.

#### Verify MCP connection

Check that the MCP server is running correctly:

1. Open a new chat in [!DNL Cursor].
1. Look for an indicator showing the MCP server is connected. This indicator is typically located in the chat interface.
1. Try entering a prompt like the following:

   ```shell-session
   Search the storefront docs for information about slots
   ```

If the MCP server is working, you should see relevant documentation results.

![MCP Connection Verified](../assets/mcp-connection-verified.png){width="600" zoomable="yes"}

If this works, you are ready to continue with the [tutorial](./ratings-extension.md).
 -->
