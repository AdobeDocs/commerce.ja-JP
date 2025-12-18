---
title: ドキュメント RAG サービス
description: Adobe Commerce開発用の AI を利用したドキュメント検索サービスの使用方法を説明します。
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 28396828516645abec3b42a2c6874afe9134dfb8
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# ドキュメント RAG サービス（Beta）

>[!NOTE]
>
>ドキュメント RAG サービスは現在Betaにあり、エクスペリエンスは変更される可能性があります。

ドキュメント RAG （Retrieval-Augmented Generation）サービスは、関連するAdobe CommerceおよびApp Builder ドキュメントで、AI を利用したセマンティック検索機能を提供します。

この RAG は、Adobe Commerceに関する質問を行うための IDE インターフェイスを提供し、アプリケーション開発やその他の移行作業のベストプラクティスについてアドバイスします。

RAG サービスは、Cursor および他の MCP 互換 AI アシスタントと統合される [Commerce拡張ツール ](./coding-tools.md)MCP （Model Context Protocol）サーバーの一部です。

## 使用可能なドキュメント

次の表に、RAG サービスで現在インデックスが作成されているドキュメントと、関連インデックスの検索をトリガーにするために使用できるキーワードを示します。 含まれるドキュメントは、RAG サービスの開発に合わせて、さらに拡張される予定です。

| カテゴリ | 索引 | 含まれるコンテンツ | キーワード |
|-------|---------|---------|------------------------|
| [ ストアフロント ](https://experienceleague.adobe.com/developer/commerce/storefront/) | commerce-storefront-docs | Edge Delivery Services、ドロップダウン、ストアフロントコンポーネント | ストアフロント，ドロップダウン，EDS，製品一覧，チェックアウト |
| [ 拡張性 ](https://developer.adobe.com/commerce/extensibility/) | commerce-extensibility-docs | Webhook、イベント、拡張機能、統合 | webhook, イベント，拡張機能，API メッシュ，GraphQL |
| [Commerce](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview) | commerce-core-docs | Core Commerce（カタログ、顧客、注文） | カタログ，製品，顧客，注文，在庫 |
| [App Builder](https://developer.adobe.com/app-builder/docs/intro_and_overview/) | app-builder-docs | App Builder、実行時のアクション、UI 拡張機能 | app builder, ランタイムアクション，React Spectrum |

インデックスの選択の詳細については、「[ インデックスの自動選択 ](#automatic-index-selection-recommended)」および「[ インデックスの明示的な選択 ](#explicit-index-selection)」を参照してください。

各インデックスに含まれているドキュメントについて詳しくは、[ 取り込まれたソースリスト ](https://github.com/adobe-commerce/azure-commerce-documentation-agent/blob/develop/docs/INGESTED_SOURCES.md) を参照してください。

## セキュリティとプライバシー

* **IMS 認証** – すべての API 呼び出しは、Adobe IMSOAuth2 トークンを使用します。
* **データストレージなし** - MCP サーバーには資格情報やデータは保存されません。
* **ローカル実行** – すべてのツールがコンピューター上でローカルに実行されます。
* **セキュア通信** - ドキュメント検索では、トークン検証で HTTPS を使用します。

実稼動エンドポイントは、次の保護を含む [Azure Front Door](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview) によって保護されています。

* Microsoftのデフォルトルールセット 2.1 および Bot Manager ルールセット 1.0 を使用した web アプリケーションファイアウォール（WAF）
* 米国の禁輸対象地域（キューバ、イラン、北朝鮮、シリア、クリミア、ルハンスク、ドネツク）のジオブロック
* エッジでの DDoS 保護
* フロントドアからのトラフィックのみを受け入れるために API 管理バックエンドがロックダウンされる

様々なセキュリティ要件に対して、カスタムエンドポイントを使用できます。 詳しくは、[ カスタム正面ドアの端点 ](#custom-front-door-endpoint) を参照してください。

## 前提条件

インストールする前に、次のことを確認します。

* [Node.js](https://nodejs.org/en/download){target="_blank"} 18 以降（LTS 推奨）
* [ カーソル IDE](https://cursor.com/download){target="_blank"} （推奨）または別の MCP 互換 IDE

  >[!NOTE]
  >
  >他の MCP 互換 IDE もサポートされていますが、最適なエクスペリエンスを得るには Cursor を使用することをお勧めします。 別の IDE を使用している場合は、選択した IDE で動作するように、プロンプトとその他の手順をドキュメントで変更する必要があります。

## インストール

1. [Adobe I/O CLI](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/) をグローバルにインストールします。

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Adobe IMSによる認証：

   ```bash
   aio auth login
   ```

1. Commerce拡張ツールリポジトリをクローンし、次のディレクトリに移動します。

   ```bash
   git clone https://github.com/adobe-commerce/commerce-extensibility-tools.git
   cd commerce-extensibility-tools
   ```

1. 依存関係をインストールします。

   ```bash
   npm install
   ```

1. Commerce プロジェクトディレクトリ（グローバルではない）で `.cursor/mcp.json` を作成または更新して、`commerce-extensibility-tools` の MCP サーバーを組み込みます。

   ```json
   {
     "mcpServers": {
       "commerce-extensibility-tools": {
         "command": "node",
         "args": [
           "/<your-project-directory>/commerce-extensibility-tools/index.js"
         ],
         "env": {
           "NODE_ENV": "production"
         }
       }
     }
   }
   ```

   `<your-project-directory>` を、リポジトリのクローンを作成した実際のパスに置き換えてください。

   >[!NOTE]
   >
   >Windows では、プロジェクトディレクトリへのパスを指定する際に問題が発生した場合は、[ パスの問題のトラブルシューティング ](#path-issues-windows) を参照してください。

1. Cursor IDE を再起動して、MCP サーバーを読み込みます。

1. AI アシスタントに確認して、インストールを検証します。

   ```shell-session
   Can you show me the available Adobe Commerce tools?
   ```

## 使用状況

インストールが完了すると、インデックスを [ 自動的に ](#automatic-index-selection-recommended) または [ 明示的に ](#explicit-index-selection) 呼び出すことができます。 [`/search-commerce-docs` コマンドを使用することもでき ](#command-based-search) す。

>[!NOTE]
>
>RAG サービスは、最も関連性の高い上位 5 つの結果を返します。

### 自動インデックス選択（推奨）

Commerce プロジェクトに関する自然言語での質問を行うと、適切なドキュメントインデックスが自動的に検索され、関連する情報が提供されます。

>[!BEGINSHADEBOX]

次のプロンプトでは、`commerce-storefront-docs` インデックスが自動的に選択されます。

```shell-session
"How do I use Edge Delivery Services drop-ins for product listing?"
```

次のプロンプトでは、`commerce-extensibility-docs` インデックスが自動的に選択されます。

```shell-session
"How do I create a webhook in Adobe Commerce?"
```

次のプロンプトでは、`commerce-core-docs` インデックスが自動的に選択されます。

```shell-session
"How to configure product catalog settings?"
```

次のプロンプトでは、`app-builder-docs` インデックスが自動的に選択されます。

```shell-session
"What are App Builder runtime action best practices?"
```

>[!ENDSHADEBOX]

### 明示的なインデックス選択

または、使用するインデックスをプロンプトで指定できます。

```shell-session
Search commerce-storefront-docs for authentication drop-in
```

```shell-session
Using app-builder-docs, how do I deploy runtime actions?
```

### コマンドベースの検索

RAG サービスが使用されていることを確認するには、`/search-commerce-docs` Cursor コマンドを手動で呼び出し、プロンプトでドキュメントを検索します。

```shell-session
/search-commerce-docs "How do I subscribe to Commerce events?"
```

## カスタム正面ドアの端点

デフォルトでは、ドキュメント検索では、WAF Protection を備えた実稼動 [Azure Front Door](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview) エンドポイントを使用します。 テストや開発の目的で、`FRONT_DOOR_URL` 環境変数を使用してこれを上書きできます。

カスタムエンドポイントを使用するには、Cursor MCP 設定に追加します。

```json
{
  "mcpServers": {
    "commerce-extensibility-tools": {
      "command": "node",
      "args": ["/<your-project-directory>/commerce-extensibility-tools/index.js"],
      "env": {
        "NODE_ENV": "production",
        "FRONT_DOOR_URL": "https://<custom-endpoint>.azurefd.net"
      }
    }
  }
}
```

>[!NOTE]
>
>ほとんどの開発者は、デフォルトの実稼動エンドポイントを使用する必要があり、`FRONT_DOOR_URL` 変数を設定する必要はありません。

## トラブルシューティング

次の節では、ドキュメント RAG サービスの使用時に発生する可能性のある一般的な問題のトラブルシューティングに関するヒントを示します。

### 認証エラー

ドキュメント検索ツールには、Adobe IMS認証が必要です。 認証エラーが発生した場合は、次の手順を使用して問題のトラブルシューティングと解決を行ってください。

1. ログインしていることを確認します。

   ```bash
   aio where
   ```

1. IMS トークンが表示されていることを確認します。

   ```bash
   aio auth login --bare
   ```

1. 認証エラーが解決しない場合は、ログアウトしてからログインし直します。

   ```bash
   aio auth logout
   aio auth login
   ```

### MCP サーバーが読み込まれない

MCP サーバーが接続されていない場合、またはエージェントが RAG に接続できないと表示している場合は、次の手順に従って問題のトラブルシューティングと解決を行います。

1. **Cmd」、「**」（macOS）または **Ctrl」、「**」（Windows および Linux）を使用して「Cursor Settings」を開きます。

1. 「MCP」を検索し、`commerce-extensibility-tools` がリストされ、有効になっていることを確認します。

1. MCP 設定パネルでエラーメッセージを確認します。

1. `mcp.json` ファイルがプロジェクトに存在することを確認します。

   ```bash
   cat .cursor/mcp.json
   ```

1. パスが正しく、絶対パスであることを確認します。

   ```bash
   ls -la /<your-project-directory>/commerce-extensibility-tools/index.js
   ```

### ツールが見つかりません

1. カーソルを終了し、再度開きます。

1. **Cmd+Shift+P** （macOS）または **Ctrl+Shift+P** （Windows/Linux）を使用し、「Developer: Open Logs Folder」を検索して、Cursor の Developer Console で MCP サーバーのログを確認します。

1. インストールを確認します。

   ```bash
   cd commerce-extensibility-tools
   npm install
   node index.js
   ```

   サーバーはエラーなしで起動する必要があります。

### パスの問題（Windows）

Windows の場合、次のようにスラッシュ `/` またはエスケープされたバックスラッシュ `\\` 使用します。

```json
{
  "args": ["C:/Users/yourname/projects/commerce-extensibility-tools/index.js"]
}
```

```json
{
  "args": ["C:\\Users\\yourname\\projects\\commerce-extensibility-tools\\index.js"]
}
```

## その他のリソース

* [Adobe Commerce開発者向けドキュメント ](https://developer.adobe.com/commerce/docs/){target="_blank"}
* [App Builder ドキュメント ](https://developer.adobe.com/app-builder/docs/){target="_blank"}
* [ モデル コンテキスト プロトコル ](https://modelcontextprotocol.io/){target="_blank"}
* [ カーソル IDE](https://cursor.sh/docs){target="_blank"}
