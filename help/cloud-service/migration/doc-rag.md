---
title: Documentation RAG サービス
description: Adobe Commerce開発にAIを活用したドキュメント検索サービスを使用する方法について説明します。
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
role: Developer
hide: true
hidefromtoc: true
source-git-commit: ba445bf33ec9334c853245fce125af12cd244367
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 0%

---

# Documentation RAG サービス（Beta）

>[!NOTE]
>
>ドキュメントのRAG サービスは現在Betaにあり、エクスペリエンスは変更される可能性があります。

ドキュメントのRAG （Retrieval-Augmented Generation）サービスは、関連するAdobe CommerceとApp Builderのドキュメントに対して、AIを活用したセマンティック検索機能を提供します。

このRAGは、Adobe Commerceに関する質問を行うためのIDE インターフェイスを提供し、アプリケーションの開発やその他の移行タスクに関するベストプラクティスについてアドバイスします。

RAG サービスは、[Commerce拡張ツール &#x200B;](https://developer.adobe.com/commerce/extensibility/developer-agent/){target="_blank"} MCP （Model Context Protocol） サーバーの一部であり、Cursorおよびその他のMCP互換AI アシスタントと統合されています。

## 使用可能なドキュメント

次の表は、現在RAG サービスによってインデックスが作成されているドキュメントと、関連するインデックスを検索する際にトリガーに使用できるキーワードを示しています。 RAG サービスの開発に伴い、含まれるドキュメントは引き続き拡大していきます。

| カテゴリ | Index | 含まれるコンテンツ | キーワード |
|-------|---------|---------|------------------------|
| [&#x200B; ストアフロント &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/) | commerce-storefront-docs | Edge Delivery Services、ドロップイン、ストアフロントコンポーネント | ストアフロント、ドロップイン、EDS、製品リスト、チェックアウト |
| [拡張性](https://developer.adobe.com/commerce/extensibility/) | commerce-extensibility-docs | Webhook、イベント、拡張機能、統合 | webhook, イベント，拡張機能，API メッシュ，GraphQL |
| [Commerce](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview) | commerce-core-docs | Core Commerce（カタログ、顧客、注文） | カタログ，製品，顧客，注文，在庫 |
| [App Builder](https://developer.adobe.com/app-builder/docs/intro_and_overview/) | app-builder-docs | App Builder, ランタイムアクション，UI拡張機能 | アプリビルダー、ランタイムアクション、React Spectrum |

インデックス選択について詳しくは、[自動インデックス選択](#automatic-index-selection-recommended)および[明示的インデックス選択](#explicit-index-selection)を参照してください。

各インデックスに含まれるドキュメントについて詳しくは、[取り込まれたソースリスト &#x200B;](https://github.com/adobe-commerce/azure-commerce-documentation-agent/blob/develop/docs/INGESTED_SOURCES.md)を参照してください。

## セキュリティとプライバシー

* **IMS authentication** – すべてのAPI呼び出しでAdobe IMS OAuth2 トークンが使用されます。
* **データストレージがありません** - MCP サーバーは資格情報またはデータを保存しません。
* **ローカル実行** – すべてのツールがコンピューター上でローカルに実行されます。
* **安全な通信** - ドキュメント検索では、トークン検証にHTTPSが使用されます。

実稼動エンドポイントは、[Azure フロントドア &#x200B;](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview)によって保護されます。これには、次の保護機能が含まれます。

* Microsoft Default RuleSet 2.1およびBot Manager RuleSet 1.0を使用したWeb Application Firewall （WAF）
* 米国の禁輸地域（キューバ、イラン、北朝鮮、シリア、クリミア、ルハンスク、ドネツク）のジオブロッキング
* エッジでのDDoS対策
* フロントドアからのトラフィックのみを受け入れるようにAPI管理バックエンドをロックダウン

セキュリティ要件が異なる場合は、カスタムエンドポイントを使用できます。 詳しくは、[&#x200B; カスタムフロントドアエンドポイント &#x200B;](#custom-front-door-endpoint)を参照してください。

## 前提条件

インストールする前に、次のことを確認してください。

* [Node.js](https://nodejs.org/en/download){target="_blank"} 18以上（LTSを推奨）
* [&#x200B; カーソル IDE](https://cursor.com/download){target="_blank"} （推奨）または他のMCP互換IDE

  >[!NOTE]
  >
  >他のMCP互換IDEはサポートされていますが、最良のエクスペリエンスを得るにはCursorが推奨されます。 別のIDEを使用している場合は、選択したIDEを操作するために、ドキュメントのプロンプトやその他の手順を変更する必要があります。

## インストール

1. [Adobe I/O CLI](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/)をグローバルにインストールします。

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Adobe IMSによる認証：

   ```bash
   aio auth login
   ```

1. Commerce拡張ツールリポジトリを複製し、次のディレクトリに移動します。

   ```bash
   git clone https://github.com/adobe-commerce/commerce-extensibility-tools.git
   cd commerce-extensibility-tools
   ```

1. 依存関係をインストールします。

   ```bash
   npm install
   ```

1. `commerce-extensibility-tools` MCP サーバーを含めるには、（グローバルではなく）Commerce プロジェクトディレクトリで`.cursor/mcp.json`を作成または更新します。

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

   `<your-project-directory>`を、リポジトリを複製した実際のパスに置き換えることを確認してください。

   >[!NOTE]
   >
   >Windowsで、プロジェクトディレクトリへのパスの提供に関する問題が発生した場合は、[&#x200B; パスの問題に関するトラブルシューティング &#x200B;](#path-issues-windows)を参照してください。

1. カーソル IDEを再起動して、MCP サーバーを読み込みます。

1. AI アシスタントに次の情報を求めて、インストールを確認します。

   ```shell-session
   Can you show me the available Adobe Commerce tools?
   ```

## 使用状況

インストールが完了したら、インデックス [自動的](#automatic-index-selection-recommended)または[明示的](#explicit-index-selection)を呼び出すことができます。 [`/search-commerce-docs` コマンド &#x200B;](#command-based-search)も使用できます。

>[!NOTE]
>
>RAG サービスは、上位5つの最も関連性の高い結果を返します。

### 自動インデックス選択（推奨）

Commerceプロジェクトについて自然言語で質問すると、適切なドキュメントインデックスが自動的に検索され、関連する情報が提供されます。

>[!BEGINSHADEBOX]

次のプロンプトは、`commerce-storefront-docs` インデックスを自動的に選択します。

```shell-session
"How do I use Edge Delivery Services drop-ins for product listing?"
```

次のプロンプトは、`commerce-extensibility-docs` インデックスを自動的に選択します。

```shell-session
"How do I create a webhook in Adobe Commerce?"
```

次のプロンプトは、`commerce-core-docs` インデックスを自動的に選択します。

```shell-session
"How to configure product catalog settings?"
```

次のプロンプトは、`app-builder-docs` インデックスを自動的に選択します。

```shell-session
"What are App Builder runtime action best practices?"
```

>[!ENDSHADEBOX]

### 明示的なインデックス選択

または、プロンプトで使用するインデックスを指定することもできます。

```shell-session
Search commerce-storefront-docs for authentication drop-in
```

```shell-session
Using app-builder-docs, how do I deploy runtime actions?
```

### コマンドベースの検索

RAG サービスが使用されていることを確認する場合は、`/search-commerce-docs` Cursor コマンドを手動で呼び出して、プロンプトでドキュメントを検索できます。

```shell-session
/search-commerce-docs "How do I subscribe to Commerce events?"
```

## カスタム正面玄関エンドポイント

デフォルトでは、ドキュメント検索では、WAF保護を備えた実稼動[Azure フロントドア &#x200B;](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview) エンドポイントが使用されます。 テストまたは開発の目的で、`FRONT_DOOR_URL`環境変数でこれを上書きできます。

カスタムエンドポイントを使用するには、それをCursor MCP設定に追加します。

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
>ほとんどの開発者は、デフォルトの実稼動エンドポイントを使用する必要があり、`FRONT_DOOR_URL`変数を設定する必要はありません。

## トラブルシューティング

次の節では、ドキュメント RAG サービスを使用する際に発生する可能性のある一般的な問題に関するトラブルシューティングのヒントを示します。

### 認証エラー

ドキュメント検索ツールはAdobe IMS認証を必要とします。 認証エラーが発生した場合は、次の手順に従って問題をトラブルシューティングし、解決してください。

1. ログインしていることを確認してください：

   ```bash
   aio where
   ```

1. IMS トークンが表示されていることを確認します。

   ```bash
   aio auth login --bare
   ```

1. 認証エラーが引き続き発生する場合は、ログアウトして再度ログインしてみてください。

   ```bash
   aio auth logout
   aio auth login
   ```

### MCP サーバーが読み込まれていません

MCP サーバーが接続していない場合、または担当者からRAGに接続できないと言われた場合は、次の手順を使用して問題をトラブルシューティングし、解決します。

1. **Cmd、** （macOS）または&#x200B;**Ctrl、** （WindowsおよびLinux）を使用してカーソル設定を開きます。

1. 「MCP」を検索し、`commerce-extensibility-tools`が表示され、有効になっていることを確認します。

1. MCP設定パネルでエラーメッセージを確認します。

1. プロジェクトに`mcp.json` ファイルが存在することを確認します。

   ```bash
   cat .cursor/mcp.json
   ```

1. パスが正しく、絶対であることを確認します。

   ```bash
   ls -la /<your-project-directory>/commerce-extensibility-tools/index.js
   ```

### ツールが見つかりません

1. カーソルを終了して再度開きます。

1. **Cmd+Shift+P** （macOS）または&#x200B;**Ctrl+Shift+P** （Windows/Linux）を使用して、Cursorの開発者コンソールでMCP サーバーのログを確認し、「Developer: Open Logs Folder」を検索します。

1. インストールを確認します。

   ```bash
   cd commerce-extensibility-tools
   npm install
   node index.js
   ```

   サーバーはエラーなしで起動する必要があります。

### パスの問題（Windows）

Windowsでは、フォワードスラッシュ `/`またはエスケープバックスラッシュ `\\`を使用します。

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

## 関連資料

* [Adobe Commerce開発者用マニュアル](https://developer.adobe.com/commerce/docs/){target="_blank"}
* [App Builder ドキュメント](https://developer.adobe.com/app-builder/docs/){target="_blank"}
* [モデルコンテキストプロトコル](https://modelcontextprotocol.io/){target="_blank"}
* [カーソル IDE](https://cursor.sh/docs){target="_blank"}
