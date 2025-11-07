---
title: ADL Commerce ラボの前提条件
description: 評価拡張機能のラボの前提条件について説明します。
role: Developer
hide: true
hidefromtoc: true
source-git-commit: ba4d096bcb99420c029d0b0674fc00f1f1445cea
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Adobe Developers Live - Adobe Commerce ラボの前提条件

このページでは、[ 評価拡張機能のラボ ](./workbook.md) の前提条件と、その他の手動による設定手順を示します。 このラボには、これらの手順のほとんどを自動化するスクリプトも含まれています。

## 拡張機能の前提条件

開始する前に、次の前提条件を満たしてください。

* [!DNL Adobe I/O CLI] のインストール

  ```bash
  npm install -g @adobe/aio-cli
  ```

* Commerce プラグインのインストール

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
  ```

* [Cursor](https://cursor.com/download) （推奨）などの AI を利用した IDE のダウンロード、Claude Code、Gemini CLI、Copilot などの他の IDE もサポートされていますが、このチュートリアルのプロンプトやその他の手順の変更が必要になる場合があります。
<!-- 
### Create a new project on Adobe Developer Console

1. Navigate to [Adobe Developer Console](https://developer.adobe.com/).
1. Click [!UICONTROL **Create project from a template**].
1. Select the [!UICONTROL **App Builder**] template.
1. Enter a [!UICONTROL **Project Title**] and [!UICONTROL **App Name**].
1. Ensure the **[!UICONTROL Include Runtime]** checkbox is marked.

   ![Create project with App Builder template](./assets/app-builder-template.png){width="600" zoomable="yes"}

1. Click **Save**.

### Add APIs to the workspace

1. Click the [!UICONTROL **Stage**] workspace and then repeat the following steps for each API.

   ![APIs added to workspace](./assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. Click [!UICONTROL **Add Service**] and select [!UICONTROL **API**].

1. Select the [!UICONTROL **Adobe Services**] filter and select one of the following APIs:

   * [!UICONTROL **I/O Management API**]
   * [!UICONTROL **I/O Events**]

1. Select the [!UICONTROL **Experience Cloud**] filter and select one of the following APIs:

   * [!UICONTROL **Adobe I/O Events for Adobe Commerce**]

1. Click [!UICONTROL **Next**].

1. Click[!UICONTROL **Save configured API**].

1. Repeat the previous steps until all APIs are added to the workspace.

   ![APIs added to workspace](./assets/apis-added.png){width="600" zoomable="yes"} -->

### AIO CLI の設定

1. 既存の設定を消去します。

   ```bash
   aio config clear
   ```

   AIO CLI を使用してログインします。

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

   ![CLI 設定 ](./assets/cli-configuration.png){width="600" zoomable="yes"}

### クローン統合スターターキット

Commerce統合スターターキットリポジトリーのクローンを作成し、プロジェクトを準備します。

```bash
git clone --branch adl https://github.com/adobe/commerce-integration-starter-kit.git extension
cd extension
```

![ スターターキットの複製 ](./assets/clone-starter-kit.png){width="600" zoomable="yes"}

### .env ファイルを作成します

環境設定ファイルを作成します。

```bash
cp env.dist .env
```

<!-- Open the `.env` file in a text editor and add the following OAuth credentials:

```text
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

You can copy these values from the **[!UICONTROL Credential details]** page in [Developer Console](https://developer.adobe.com/) by clicking the **[!UICONTROL OAuth Server-to-Server]** tab on your workspace.

![OAuth credentials](./assets/oauth-credentials.png){width="600" zoomable="yes"}

#### Add the Commerce configuration

Add the following Commerce instance details to your `.env` file:

```text
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

To find these values:

1. Go to [Commerce Cloud Service instances](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances).
1. Click the information icon next to your assigned seat.
1. Copy the REST endpoint as `COMMERCE_BASE_URL`.
1. Copy the GraphQL Endpoint as `COMMERCE_GRAPHQL_ENDPOINT`.

#### Set event prefix

Set a temporary value for the event prefix:

```text
EVENT_PREFIX=test
```
 -->

### ワークスペース設定のダウンロード

次のコマンドを実行して、ワークスペース設定ファイルをダウンロードします。

```bash
aio console workspace download workspace.json
```

### ローカルワークスペースのリモートワークスペースへの接続

ローカルプロジェクトをリモートワークスペースにリンクします。

```bash
aio app use workspace.json -m
```

![ ワークスペースに接続 ](./assets/connect-workspace.png){width="600" zoomable="yes"}

## ストアフロントの前提条件

このチュートリアルの [ ストアフロント ](#connect-to-the-storefront) セクションを完了し、ストアの製品の評価を確認するには、次の項目が必要です。
<!-- 
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
  * Windows: Use [Git Bash](https://git-scm.com/install) or [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install).

* [Google Chrome](https://www.google.com/chrome/) - Required for testing the storefront -->

### プロジェクトファイルの取得

プロジェクト ファイルは、次の 2 つの方法のいずれかで取得できます。

<!-- 
#### Option A: Clone the repository (recommended) -->

[!DNL Git] がインストールされている場合は、ターミナルを開いてリポジトリのクローンを作成します。

```bash
git clone --branch agentic-dev https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

<!-- #### Option B: Download the zip file

If you don't have [!DNL Git] installed:

1. Download the project zip file from: [https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip](https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip)
1. Extract the zip file to a folder on your machine.
1. Open your terminal and navigate into the unzipped folder:

   ```bash
   cd path/to/aem-boilerplate-commerce-agentic-dev
   ``` -->

### ルート依存関係のインストール

主なプロジェクトの依存関係をインストールします。

```bash
npm install
```

これにより、ストアフロントアプリケーションに必要なすべてのパッケージがインストールされます。

### MCP サーバーの依存関係のインストール

MCP サーバーディレクトリに移動し、依存関係をインストールします。

```bash
cd mcp-server
npm install
cd ..
```

<!-- ### Configure environment variables

The MCP server requires certain environment variables to connect to the RAG service.

Create a `.env` file in the `mcp-server` directory:

```bash
cd mcp-server
cp env.example .env
```

Edit the `.env` file and add the following values (we'll provide the actual URL during the lab):

```env
RAG_MODE=worker
WORKER_RAG_URL=<provided-during-lab>
```

>[!NOTE]
>
>The actual value for `WORKER_RAG_URL` will be provided by the lab facilitator at the start of the session. -->

### カーソルでの MCP の有効化

モデルコンテキストプロトコル（MCP）サーバーを使用すると、AI エージェントはストアフロントのドキュメント [!DNL Adobe Commerce] アクセスできます。

#### Open Cursor MCP の設定

![Open Cursor MCP Settings](./assets/cursor-mcp-settings.png){width="600" zoomable="yes"}

1. Open [!DNL Cursor]
1. **[!UICONTROL Cursor]**/**[!UICONTROL Settings]**/**[!UICONTROL Cursor Settings]**/**[!UICONTROL Tools & MCP]** に移動します。

#### MCP 機能の有効化と設定

プロジェクトには、`.cursor/mcp.json` に MCP 設定ファイルが含まれています。 このファイルは、ローカルの MCP サーバを使用するように設定されている必要があります。

MCP の設定を確認します。

1. 「commerce-documentation-rag」サーバーが表示され、有効になっていることを確認します

設定は次のようになります。

![MCP 設定 ](./assets/mcp-configuration.png){width="600" zoomable="yes"}

>[!NOTE]
>
>`start-mcp.sh` スクリプトは、`.env` ディレクトリの `mcp-server` ファイルから環境変数を自動的に読み込みます。

#### カーソルを再起動

MCP を有効にしてサーバーを設定したら、次の手順を実行します。

1. [!DNL Cursor] を完全にやめる
1. [!DNL Cursor] を再度開き、`aem-boilerplate-commerce` プロジェクトを開きます

#### MCP 接続の確認

MCP サーバが正常に動作していることを確認します。

1. [!DNL Cursor] で新しいチャットを開く
1. MCP サーバが接続されていることを示すインジケータを探します（通常はチャット インターフェイス）。
1. 「スロットに関する情報については、ストアフロントドキュメントを検索します」のような質問をしてみてください

MCP サーバが動作している場合は、関連するドキュメントの結果が表示されます。

![MCP 接続が確認されました ](./assets/mcp-connection-verified.png){width="600" zoomable="yes"}

### 開発サーバーの起動

ローカル開発サーバーを起動します。

```bash
npm run start
```

開発サーバーは `http://localhost:3000` に起動します。

アパレルページ（`http://localhost:3000/apparel`）に移動します。

![ 開発サーバーを実行中 ](./assets/development-server-running.png){width="600" zoomable="yes"}
