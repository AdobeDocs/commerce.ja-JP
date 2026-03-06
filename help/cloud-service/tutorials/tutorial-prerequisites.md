---
title: チュートリアルの前提条件
description: 拡張機能やストアフロント開発ツールなど、Adobe Commerce as a Cloud Service チュートリアルの前提条件と設定手順について説明します。
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
source-git-commit: 1848c9dda4a1976e1bccb4d1f9d5a2e21540fc0b
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 0%

---

# チュートリアルの前提条件

このページでは、[!DNL Adobe Commerce as a Cloud Service] 評価の拡張チュートリアル [&#x200B; および &#x200B;](./ratings-extension.md) 発送方法の拡張チュートリアル [&#x200B; など、](./shipping-method-extension.md) のチュートリアルの前提条件と設定手順を示します。

## 一般的な前提条件

このチュートリアルでは、拡張機能とストアフロントの両方の開発に次のツールが必要です。

* [!DNL Node.js] （バージョン `22.x.x`）および npm （`9.0.0` 以降）：次のコマンドを使用して、インストールを確認します。

  ```bash
  node --version
  npm --version
  ```

* [Git](https://git-scm.com) のインストール – インストールの確認：

  ```bash
  git --version
  ```

* バッシュシェル
   * macOS/Linux：インストールは不要
   * Windows: [Git Bash](https://git-scm.com/install) または [Windows Subsystem for Linux （WSL）を使用してください &#x200B;](https://learn.microsoft.com/en-us/windows/wsl/install)

* [Cursor](https://cursor.com/download) （推奨）などの AI 支援 IDE をダウンロードします。 Cloud Code、Gemini CLI、Copilot などの他の IDE もサポートされていますが、プロンプトやチュートリアルのその他の手順を変更する必要がある場合があります。

## [!DNL Adobe Commerce as a Cloud Service] 前提条件

* [!DNL Adobe I/O CLI] のインストール

  ```bash
  npm install -g @adobe/aio-cli
  ```

* [Adobe I/O CLI Commerce](https://github.com/adobe-commerce/aio-cli-plugin-commerce)、[Adobe I/O CLI ランタイム &#x200B;](https://github.com/adobe/aio-cli-plugin-runtime)、[App Builder CLI](https://github.com/adobe/aio-cli-plugin-app-dev) プラグインをインストールします。

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime
  ```

### Adobe Developer Consoleの前提条件

必要な API と資格情報を使用して、Adobe Developer Consoleでプロジェクトを設定します。

1. [Adobe Developer Console](https://developer.adobe.com/console){target="_blank"} に移動します。
1. メールとパスワードを使用してログインします。

#### 新規プロジェクトの作成

Adobe Developer ConsoleでApp Builder プロジェクトを作成し、拡張機能をホストします。

1. [Adobe Developer Console](https://developer.adobe.com/) に移動します。
1. 「**[!UICONTROL Create project from a template]**」をクリックします。
1. **[!UICONTROL App Builder]** テンプレートを選択します。
1. **[!UICONTROL Project Title]** と **[!UICONTROL App Name]** を入力します。
1. 「**[!UICONTROL Include Runtime]**」チェックボックスがオンになっていることを確認します。

   ![App Builder テンプレートを選択したAdobe Developer Console プロジェクトの作成 &#x200B;](../assets/app-builder-template.png){width="600" zoomable="yes"}

1. 「**[!UICONTROL Save]**」をクリックします。

#### ワークスペースへの API の追加

イベント管理とCommerce統合のために、必要な API をステージワークスペースに追加します。

1. **[!UICONTROL Stage]** ワークスペースをクリックし、各 API に対して次の手順を繰り返します。

   ![API の「サービスを追加」オプションを使用したステージワークスペース &#x200B;](../assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. 「**[!UICONTROL Add Service]**」をクリックし、「**[!UICONTROL API]**」を選択します。

1. 次のいずれかの API を選択します。 以下に示す各 API に対して、このプロセスを繰り返します。

   * **[!UICONTROL Adobe Services]** フィルター：
      * **[!UICONTROL I/O Management API]**
      * **[!UICONTROL I/O Events]** API
   * **[!UICONTROL Experience Cloud]** フィルター：
      * **[!UICONTROL Adobe I/O Events for Adobe Commerce]** API

1. 「**[!UICONTROL Next]**」をクリックします。

1. 「**[!UICONTROL Save configured API]**」をクリックします。

1. すべての API をワークスペースに追加するまで、前の手順を繰り返します。

   ![&#x200B; 必要なすべての API が正常に追加されたことを示すWorkspace](../assets/apis-added.png){width="600" zoomable="yes"}

### Adobe I/O CLI の設定

[!DNL Adobe I/O CLI] を組織、プロジェクト、ワークスペースに接続します。

1. 既存の設定を消去します。

   ```bash
   aio config clear
   ```

1. [!DNL Adobe I/O CLI] を使用してログイン：

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

   ![Adobe I/O CLI の組織プロジェクトとワークスペースの選択を示すターミナル &#x200B;](../assets/cli-configuration.png){width="600" zoomable="yes"}

### スターターキットのクローンを作成

構築している拡張機能に対して、次のCommerce スターターキットリポジトリーの 1 つを複製し、プロジェクトを準備します。

統合スターターキット：

```bash
git clone https://github.com/adobe/commerce-integration-starter-kit.git extension
cd extension
```

スターターキットのチェックアウト：

```bash
git clone https://github.com/adobe/commerce-checkout-starter-kit.git extension
cd extension
```

>[!BEGINTABS]

>[!TAB  統合スターターキット ]

### .env ファイルの作成

環境設定ファイルを作成します。

```bash
cp env.dist .env
```

`.env` ファイルをテキストエディターで開き、次の OAuth 資格情報を追加します。

```bash
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

これらの値を **[!UICONTROL Credential details]** Developer Console[&#x200B; の &#x200B;](https://developer.adobe.com/) ページからコピーするには、ワークスペースの「**[!UICONTROL OAuth Server-to-Server]**」タブをクリックします。

![Adobe Developer Consoleの OAuth サーバー間資格情報ページ &#x200B;](../assets/oauth-credentials.png){width="600" zoomable="yes"}

#### Commerce設定を追加

`.env` ファイルに次のCommerce インスタンスの詳細を追加します。

```bash
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

これらの値を検索するには：

1. [Commerce Cloud サービスインスタンス &#x200B;](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances) に移動します。
1. インスタンスの横にある「情報」アイコンをクリックします。
1. REST エンドポイントを `COMMERCE_BASE_URL` としてコピーします。
1. GraphQL エンドポイントを `COMMERCE_GRAPHQL_ENDPOINT` としてコピーします。

#### イベントのプレフィックスの設定

イベントプレフィックスに一時的な値を設定します。

```bash
EVENT_PREFIX=test
```

### Workspace 設定のダウンロード

次のコマンドを実行して、ワークスペース設定ファイルをダウンロードします。

```bash
aio console workspace download workspace.json
```

ワークスペース設定ファイルを `scripts` ディレクトリにコピーします。

```bash
cp workspace.json scripts/
```

### ローカルワークスペースをリモートワークスペースに接続する

ローカルプロジェクトをリモートワークスペースにリンクします。

```bash
aio app use workspace.json -m
```

![aio app use コマンドでワークスペース接続が成功したことを示すターミナル &#x200B;](../assets/connect-workspace.png){width="600" zoomable="yes"}

>[!TAB  スターターキットをチェックアウト ]

### ローカルワークスペースのリモートワークスペースへの接続

ローカルプロジェクトをリモートワークスペースにリンクします。 プロジェクトルート（`extension` フォルダー）から、次を実行します。

```bash
aio app use --merge
```

プロンプトが表示されたら、Adobe I/O CLI の設定時に選択した組織、プロジェクト、ワークスペースを使用するオプションを選択します。 これにより、ワークスペース設定がアプリに書き込まれ、デプロイとローカル開発でそのワークスペースが使用されるようになります。

![aio app use コマンドでワークスペース接続が成功したことを示すターミナル &#x200B;](../assets/connect-workspace.png){width="600" zoomable="yes"}

>[!ENDTABS]

### 拡張 AI ツールのインストール

このプロセスにより、MCP 設定（`.<agent>/mcp.json`）、スキル ディレクトリ（`.<agent>/skills/`）が作成され、`AGENTS.md` がプロジェクト ルートに追加されます。 スターターキット、コーディングエージェント、パッケージマネージャーを選択するように求められます。


1. 次のコマンドを使用して、`extension` フォルダー内に AI 支援開発ツールを設定します。

   ```bash
   cd extension
   ```

   ```bash
   aio commerce extensibility tools-setup
   ```

   ![AI 拡張ツール設定コマンド出力を示すターミナル &#x200B;](../assets/install-ai-tools.png){width="600" zoomable="yes"}

1. セットアップが完了したら、コーディング エージェントを再起動して、新しい MCP ツールとスキルをロードできるようにします。 これで、お使いの環境でCommerce App Builder ツールを使用できるようになりました。

   >[!NOTE]
   >
   >スターターキットのスキルが見つからないという警告が表示された場合は、問題が発生しました。多くの場合、セットアップがスターターキットのクローンを作成したフォルダー以外で実行されていることが原因です。 `aio commerce extensibility tools-setup` フォルダー（スターターキットプロジェクトルート）から `extension` を実行し、プロンプトが表示されたら適切なスターターキットを選択します。

   ![&#x200B; チェックアウトスターターキットが選択された状態で AI 拡張ツールが設定されていることを示すターミナル &#x200B;](../assets/tools-setup-checkout.png){width="600" zoomable="yes"}

## ストアフロントの前提条件

[&#x200B; 評価拡張チュートリアル &#x200B;](./ratings-extension.md#connect-to-the-storefront) ストアフロント [&#x200B; セクションを完了し、ストアに製品の評価を表示するには &#x200B;](./ratings-extension.md) 次の項目が必要です。

* [Google Chrome](https://www.google.com/chrome/) - ストアフロントのテストに必要

* [!DNL Commerce] インスタンスに接続されたストアフロントプロジェクト。 ストアフロントプロジェクトがない場合は、[&#x200B; リポジトリをコマースデータにリンク &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/){target="_blank"} セクションを含む [&#x200B; ストアフロントの作成 &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#link-repo-to-commerce-data){target="_blank"} の手順に従います。

### ストアフロントリポジトリのクローンを作成します

ターミナルを開き、リポジトリのクローンを作成します。

```bash
git clone --branch agentic-dev https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

### 依存関係のインストール

プロジェクトの依存関係をインストールします。

```bash
npm install
```

### ストアフロントの AI ツールのインストール

`storefront` フォルダー内で AI 支援開発ツールを設定します。 ボイラープレートプロジェクトのルートから次のコマンドを実行します。

```bash
aio commerce extensibility tools-setup
```

コマンドでは、次の 2 つのプロンプトを順を追って説明します。

1. **スターターキットを選択** — **AEM ボイラープレート Commerce** を選択します。

1. **コーディングエージェントの選択** — サポートされているエージェントのリストからエージェントを選択します。

このコマンドは、`@adobe-commerce/commerce-extensibility-tools` パッケージを開発用の依存性としてインストールし、スキルファイルをエージェントのスキルディレクトリにコピーし、MCP （Model Context Protocol）を設定します。これにより、エージェントがCommerce ドキュメントの検索ツールにアクセスできるようになります。