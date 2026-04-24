---
title: 製品レビュー拡張機能チュートリアル
description: App Builder、Edge Delivery Services、AIを活用した開発ツールを使用して、Adobe Commerce as a Cloud Serviceの商品レビューおよびQ&A拡張機能を構築する方法について説明します。
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: ba445bf33ec9334c853245fce125af12cd244367
workflow-type: tm+mt
source-wordcount: '2533'
ht-degree: 0%

---

# 製品レビュー拡張機能チュートリアル

このチュートリアルでは、[!DNL Adobe App Builder]とAI支援の開発ツールを使用して、[!DNL Adobe Commerce as a Cloud Service] バックエンドを持つストアフロントに対して、製品レビューと質問と回答（Q&amp;A）のコンテンツを送信できる拡張機能の構築を説明します。 この拡張機能は、買い物客が商品のレビューおよび質問と回答（Q&amp;A）のコンテンツを表示および送信し、商品詳細ページ（PDP）に表示するためのREST API エンドポイントを提供します。

次の2つの部分を作成します。

- **App Builder拡張機能** — GETおよびPOST操作を使用したREST APIにより、`aio-lib-state`で検証、ページネーション、永続性を持つ製品レビューおよびQ&amp;A コンテンツを作成および表示します。
- **ストアフロント統合** – 買い物客がレビュー、質問、回答を送信するためのフォームを含む、レビューとQ&amp;Aを表示するPDP上の製品レビューブロック。

>[!NOTE]
>
>AI エージェントは非決定論的です。 このチュートリアルのプロンプト、質問、および出力は例です。 担当者がさまざまな質問、要件、アーキテクチャの提案を作成する場合もあります。 このチュートリアルの例を使用して、類似の結果に向けてエージェントを誘導します。

開始する前に、[前提条件](./tutorial-prerequisites.md)を完了してください。 このチュートリアルでは、**統合スターターキット**&#x200B;を使用します。 既にクローンを作成し、前提条件ページで説明されている設定手順を完了していることを確認します。

## 前提条件を確認

次の前提条件がインストールされていることを確認します。

```bash
# Check Node.js version (should be 22.x.x)
node --version

# Check npm version (should be 9.0.0 or higher)
npm --version

# Check Git installation
git --version

# Check Bash shell installation
bash --version
```

上記のコマンドのいずれかが予想される結果を返さない場合は、ガイダンスについて[前提条件](./tutorial-prerequisites.md)を参照してください。

さらに、次の点を確認します。

- 製品データを含む[!DNL Adobe Commerce as a Cloud Service] インスタンスがあります。 [Commerce Cloud サービスインスタンス &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/cloud-service/overview){target="_blank"}を参照してください。
- [!DNL Commerce] インスタンスに接続されたストアフロントプロジェクトがあります。 ストアフロントがない場合は、[&#x200B; ストアフロントの作成](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=ja){target="_blank"}の手順に従います。
- `aem` CLIがインストールされています：

  ```bash
  npm install -g @adobe/aem-cli
  ```

## 拡張機能の開発

このセクションでは、AIを活用した開発ツールを使用して、[!DNL Adobe Commerce as a Cloud Service] バックエンドを持つストアフロント向けに、製品レビューおよびQ&amp;A コンテンツを送信して表示するための拡張機能の開発を説明します。 この拡張機能は、製品レビューとQ&amp;A コンテンツを送信および表示し、PDPに表示するためのREST APIを提供します。

1. コーディングエージェントのMCP設定に移動します。 例えば、カーソルで、**[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**&#x200B;に移動します。 エラーなしで`commerce-extensibility` ツールセットが有効になっていることを確認します。 エラーが表示された場合は、ツールセットのオンとオフを切り替えます。

   >[!NOTE]
   >
   >AI支援の開発ツールを使用する場合、エージェントによって生成されたコードと応答に自然なバリエーションが存在することを期待します。
   >コードで問題が発生した場合は、担当者にデバッグのサポートを依頼してください。

1. Cursorのコンテキストにドキュメントが追加されている場合は、そのドキュメントを無効にします。

   **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Indexing & Docs]**&#x200B;に移動し、一覧されているドキュメントをすべて削除します。

### 手順1：最初のプロンプトを入力する

AI エージェントに実装を開始するよう促します。 エージェントに停止して質問するように伝えることで、実装を早い段階で導くことができます。

担当者のチャットウィンドウに次のプロンプトを入力します。

```shell-session
I want to build an Adobe Commerce as a Cloud Service extension that allows shoppers to submit and view product review and question and answer (Q&A) content that displays on product detail pages (PDP).

## Product Reviews
The application has REST API endpoints that can be called by a storefront to retrieve and submit product reviews for a given SKU.

The GET endpoint accepts the following query parameters:
- sku (string, required): The SKU of the product to fetch reviews for
- limit (integer, optional): The maximum number of reviews to return (default: 10)
- offset (integer, optional): The number of reviews to skip for pagination (default: 0)

The POST endpoint accepts the following JSON body parameters:
- sku (string, required): The SKU of the product to submit a review for
- rating (integer, required): The rating for the product (1-5)
- review (string, optional): The text of the review
- user (string, optional): The name of the user submitting the review

The POST endpoint validates the input and returns appropriate error responses for invalid data. The reviews are stored and associated with the corresponding product SKU.

## Questions and Answers
The application has REST API endpoints that can be called by a storefront to retrieve and submit questions and answers for a given SKU.

The GET endpoint accepts the following query parameters:
- sku (string, required): The SKU of the product to fetch questions and answers for
- limit (integer, optional): The maximum number of questions and answers to return (default: 10)
- offset (integer, optional): The number of questions and answers to skip for pagination (default: 0)

The POST endpoint accepts the following JSON body parameters:
- sku (string, required): The SKU of the product to submit a question or answer for
- type (string, required): The type of submission ("question" or "answer")
- questionId (string, required if type is "answer"): The ID of the question being answered
- content (string, required): The text of the question or answer
- user (string, optional): The name of the user submitting the question or answer

The POST endpoint validates the input and returns appropriate error responses for invalid data. The questions and answers are stored and associated with the corresponding product SKU. Answers are also associated with the corresponding question.

Do not require Adobe IMS authentication for these endpoints. They will be called directly from the storefront.

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>処理を進める前にエージェントに停止して質問するように伝えることで、プロセスの初期段階で実装を誘導できます。 これにより、主要な仮定と不足している要件が早期に特定され、このチュートリアルでガイド付きワークフローを開始するために必要になります。

### ステップ 2：担当者の質問に答える

担当者は、解決策の策定を開始する前に、回答する必要がある一連の質問を返します。 次の例は、典型的な質問と回答を示しています。 担当者は異なる質問をすることもありますが、トピックは一般的に同じです。

**エージェントの質問の例：**

1. **REST API — ホストとコンシューマー** — CRUD REST APIは、ストアフロントが呼び出すこのApp Builder アプリ（Adobe I/O Runtime上のweb アクション）に含める必要がありますか？ 誰が呼ぶのか（EDS Storefront、カスタム/ヘッドレスストアフロント、またはその両方）? CORS、パブリック（未認証）アクセスが必要ですか、それとも呼び出し元はAPI キーまたはOAuthを使用しますか？
1. **データモデル** — 「レビュー」または「質問」は何を表すべきですか？ 顧客識別子（メールのみ、または顧客ID）? 商品識別子（SKUのみ、またはSKU + ストアビュー）? 同じ顧客が同じSKUに対して複数のレビューを送信できますか？
1. **永続性** — `aio-lib-state`はレビューやQ&amp;Aを永続化するのに適した場所ですか、それとも外部ストアを持っていますか？ デザインはマルチテナントまたはシングルテナントを前提とすべきですか？
1. **ページネーションのセマンティクス** — Q&amp;A GETの場合、`limit`は質問のみ（ネストされた回答を含む）に適用されますか、質問の合計数と回答に適用されますか？

**回答の例：**

```shell-session
1. The REST API should be part of this App Builder app. It will be called by the EDS Storefront. No authentication — public access for both GET and POST.
2. For reviews: sku, rating (1-5), optional review text, optional user name. For Q&A: sku, type (question or answer), content, optional user. Answers linked to questions via questionId. Allow multiple reviews per SKU from the same user.
3. Use aio-lib-state. Single tenant for now.
4. Pagination by question — limit and offset apply to questions; each question includes its nested answers.
```

>[!NOTE]
>
>担当者がさまざまな質問をする場合があります。 これらの回答を、エージェントを同じ機能的な結果に導くためのガイダンスとして使用します。レビューとQ&amp;A付きのパブリック REST API、永続性`aio-lib-state`で認証なし。

### ステップ 3：要件とアーキテクチャの見直し

担当者は、レビューする要件とアーキテクチャドキュメントを生成します。 要件が指定した回答と一致し、アーキテクチャがカバーしていることを確認します。

- 4つのweb アクション：`reviews-get`、`reviews-post`、`qa-get`、`qa-post`
- 許可されたパターン （`[a-zA-Z0-9-_.]` — コロンなし）に準拠するキーで`aio-lib-state`を使用して永続化します
- JSON文字列として保存された状態の値（生のオブジェクトや配列ではない）
- 自己完結型パッケージ – バンドルをエスケープする`../../` パスを介してではなく、`product-reviews` パッケージ内の共有コード（utils、定数）

>[!NOTE]
>
>AI エージェントは非決定論的で、モデルとIDEによって動作が異なります。 異なる要件とアーキテクチャのセットを生成する、異なる質問のセットが表示される場合があります。 その場合は、実装がこのチュートリアルに記載されている内容と密接に一致するように、エージェントを方向に誘導してから先に進んでください。

### 手順4：実行計画の選択

担当者は、詳細な実装計画を作成するか、直接実装を完了するかを選択できます。

- より詳細に制御して段階的に実行できるレビュー可能なプランが必要な場合は、最初のオプションを選択します。
- エージェントに最小限の介入で完全な実装を行わせたい場合は、2番目のオプションを選択します。

### 手順5：拡張機能のデプロイ

エージェントが実装を完了したら、拡張機能をデプロイします。

```bash
aio app deploy
```

エージェントがアクションに`require-adobe-auth: true`を追加した場合は、エンドポイントをストアフロントから直接呼び出せるように、認証を削除するようにエージェントに依頼します。

```shell-session
Remove the requirement to provide a valid Adobe IMS access token from all product-reviews actions.
```

次に、次の手順を実行します。

```bash
aio app deploy
```

### 手順6：モックデータを作成し、テスト用に事前入力

モックデータファイルを作成し、curlを使用してAPIを事前入力することで、CLIとストアフロントでテスト用のサンプルレビューとQ&amp;A コンテンツを取得できます。

1. サンプルデータを含むファイル `docs/mock-product-reviews-data.json` （または類似）を作成します。 例：

   ```json
   {
     "reviews": [
       { "sku": "ADB153", "rating": 5, "review": "Great product, highly recommend!", "user": "shopper@example.com" },
       { "sku": "ADB153", "rating": 4, "review": "Good value for money.", "user": "buyer@example.com" }
     ],
     "questions": [
       { "sku": "ADB153", "type": "question", "content": "Does this come in other colors?", "user": "curious@example.com" }
     ]
   }
   ```

1. curlを使用して、デプロイしたAPIにデータをPOSTします。

   `<your-runtime-url>`を実際のApp Builder ランタイム URLに置き換えます（例：`https://1172492-prodreviewqa135-stage.adobeioruntime.net`）。

   ```bash
   API_URL="https://<your-runtime-url>/api/v1/web/product-reviews"
   
   # Submit reviews
   curl -s -X POST "$API_URL/reviews-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","rating":5,"review":"Great product, highly recommend!","user":"shopper@example.com"}'
   
   curl -s -X POST "$API_URL/reviews-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","rating":4,"review":"Good value for money.","user":"buyer@example.com"}'
   
   # Submit a question (save the returned id for the answer)
   curl -s -X POST "$API_URL/qa-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","type":"question","content":"Does this come in other colors?","user":"curious@example.com"}'
   
   # Submit an answer (replace <QUESTION-UUID> with the id from the question response)
   curl -s -X POST "$API_URL/qa-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","type":"answer","questionId":"<QUESTION-UUID>","content":"Yes, it comes in blue and red.","user":"seller@example.com"}'
   ```

1. GET リクエストを使用してデータを確認します。

   ```bash
   curl -s "$API_URL/reviews-get?sku=ADB153"
   curl -s "$API_URL/qa-get?sku=ADB153"
   ```

>[!TIP]
>
>レビューとQ&amp;A コンテンツの両方を含む製品にはSKU `ADB153`を使用し、レビューのない製品には`ADB152`を使用します。 このデータ設定を使用すると、ストアフロントで入力された状態と空の状態の両方をテストできます。

### 手順7：拡張機能のテスト

担当者にテスト手順を提示してもらうか、前の手順のcurlの例を使用します。 次に、一般的なテストコマンドの例を示します。

**レビューを送信：**

```bash
API_URL="https://<your-runtime-url>/api/v1/web/product-reviews"
curl -s -X POST "$API_URL/reviews-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","rating":5,"review":"Excellent!","user":"test@example.com"}'
```

**レビューを表示：**

```bash
curl -s "$API_URL/reviews-get?sku=ADB153"
```

**質問を送信：**

```bash
curl -s -X POST "$API_URL/qa-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","type":"question","content":"Is this dishwasher safe?","user":"test@example.com"}'
```

**回答**&#x200B;を送信します（質問の回答の`id`を`questionId`として使用します）。

```bash
curl -s -X POST "$API_URL/qa-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","type":"answer","questionId":"<QUESTION-UUID>","content":"Yes, it is.","user":"support@example.com"}'
```

### サービス契約の作成

サービスの実装が完了したら、担当者にストアフロント作業のサービス契約の作成を依頼します。

```shell-session
Create a service contract for the Product Review and Q&A application that defines the API endpoints, request and response formats, and any necessary data models. Ensure that the service contract is clear and detailed enough for a frontend developer to implement the storefront integration without needing to ask additional questions about the API. Name this file PRODUCT_REVIEW_QA_CONTRACT.md
```

このファイルをストアフロントプロジェクトにコピーし、ストアフロントエージェントが参照できるようにします。

## ストアフロントへの接続

このセクションでは、[!DNL Edge Delivery Services]とAI支援の開発ツールを使用して、製品レビューとQ&amp;A拡張機能のストアフロント部分を実装する方法について説明します。 PDPに商品レビューブロックを追加すると、レビューとQ&amp;Aの両方のコンテンツが表示され、買い物客が新しいコンテンツを送信できるようになります。

>[!NOTE]
>
>提供されるプロンプトは出発点です。 変更せずに使用することはできますが、エージェントと自然な会話をすることを検討してください。
>
>AI支援の開発ツールを使用する場合、エージェントによって生成されたコードと応答には常に自然なバリエーションがあります。
>
>コードで問題が発生した場合は、担当者にデバッグのサポートを依頼してください。

### ストアフロントの前提条件

ストアフロント統合を開始する前に、次の点を確認してください。

- [!DNL Commerce] インスタンスに接続されたストアフロントプロジェクト
- Commerce ストアフロント AI ツール [CLIを使用してインストール &#x200B;](./tutorial-prerequisites.md#install-the-storefront-ai-tools)
- `PRODUCT_REVIEW_QA_CONTRACT.md` ファイルがストアフロントプロジェクトにコピーされました

### 手順1：環境の検証

`config.json` ファイルを開き、`commerce-core-endpoint`と`commerce-endpoint`の値が[!DNL Adobe Commerce as a Cloud Service] GraphQL エンドポイントを指していることを確認します。

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### 手順2：最初のプロンプトを入力する

サービス契約が既にプロジェクト内にある場合は、担当者に製品レビューブロックの実装を依頼します。 エージェントで利用可能な場合は、**プラン** モードを使用して、プランなしでエージェントが続行できないようにします。

```shell-session
Analyze @PRODUCT_REVIEW_QA_CONTRACT.md and build a product review block using the API specified in the contract. The block displays both reviews and Q&A content on the product detail page, with forms for shoppers to submit reviews, questions, and answers. Use the project manager skill to plan this implementation.
```

>[!TIP]
>
>段階的なワークフローをトリガーし、導入をスムーズに進めることができます。 これにより、重要な仮定と欠けている要件をプロセスの初期段階で特定できます。

### ステップ 3：明確な質問に答える

担当者は、解決策の策定を開始する前に、回答する必要がある一連の質問を返します。 次の例は、典型的な質問と回答を示しています。 担当者は異なる質問をすることもありますが、トピックは一般的に同じです。

**エージェントの質問の例：**

1. **API ベース URL** — ストアフロントでproduct-reviews API ベース URLを取得するにはどうすればよいですか？ オプションには、設定ブロック（`apiBaseUrl`を含むテーブルなど）、グローバルプレースホルダー、または別のアプローチを含めることができます。
1. **SKU ソース** — ブロックは、PDP コンテキスト（現在の製品）またはブロック設定からSKUを読み取る必要がありますか？
1. **フォームの動作** – 送信が成功した後、フォームを非表示にするか、成功メッセージを表示するか、表示されたままにしますが、無効にしますか？

**回答の例：**

```shell-session
1. Block table config with apiBaseUrl (required). Each block instance can point to its own deployment.
2. From block table if set; otherwise use getProductSku() so it works on PDP without authoring a SKU.
3. Show a success message above the form; keep the form visible but disabled.
```

>[!NOTE]
>
>ブロック設定のプレースホルダーを、実際のApp Builder ランタイム URL （`https://1172492-prodreviewqa135-stage.adobeioruntime.net`など）に置き換えます。
>
>担当者がさまざまな質問をする場合があります。 回答をガイダンスとして使用します。
>
>- コードを変更することなく変更できるように、API ベース URLはブロックテーブルから取得する必要があります。
>- 設定されている場合は、ブロックテーブルのSKU、設定されていない場合はPDPの現在の製品のSKU。
>- 送信が成功した後、成功メッセージを表示し、フォームを無効にします。

### ステップ 4：要件とアーキテクチャの見直し

担当者は、ユーザーが確認する必要のある要件ドキュメントを更新します。 次のことを確認します。

- このブロックは、レビュー（評価、ユーザー、日付、テキスト）およびQ&amp;A （ネストされた回答を含む質問）をレンダリングします。
- Formsは、レビュー、質問、回答を提出するためのものです。
- ページネーションは、レビューとQ&amp;Aの両方のコンテンツでサポートされています。
- API統合では、ブロックテーブルのベース URLを使用します。
- 成功およびエラー状態は、契約に従って処理されます。

>[!NOTE]
>
>AI エージェントは非決定論的で、モデルとIDEによって動作が異なります。 異なる要件とアーキテクチャのセットを生成する、異なる質問のセットが表示される場合があります。 その場合は、実装がこのチュートリアルに記載されている内容と密接に一致するように、エージェントを方向に誘導してから先に進んでください。

### 手順5：実行計画の選択

担当者は、詳細な実装計画を作成するか、直接実装を完了するかを選択できます。

- より詳細に制御して段階的に実行できるレビュー可能なプランが必要な場合は、最初のオプションを選択します。
- エージェントに最小限の介入で完全な実装を行わせたい場合は、2番目のオプションを選択します。

実装時に、エージェントはブロックファイルを作成および変更します。 生成されるコードを確認し、必要に応じて質問したり、担当者に連絡したりできます。 If the block does not render, ask the agent to analyze the section decoration and block discovery pattern — the block element must be a direct child of the section so the framework can find it.

### Step 6: Add the block to the product page in Document Authoring

Add the product review block to the product page template so it appears on all PDPs. Use the Document Authoring service (da.live) to add and configure the block.

1. Open your document authoring service, for example [da.live](https://da.live/)

1. Click on your project space, open the **products** folder and select **default** (`products/default`).

1. Add a new block section.

   In the block table, add a row with the block name **product-review** (or the block name your agent created).

1. Configure the block with the required settings:
   - **apiBaseUrl** — Your App Builder runtime URL (for example, `https://<namespace>-<app-name>-stage.adobeioruntime.net`).
   - **sku** — Leave empty to use the current product&#39;s SKU on the PDP, or enter a specific SKU to display reviews for that product only.

1. Click **[!UICONTROL Publish]** to publish your changes.

### Step 7: Start the server and test

After you add the block to the product page in Document Authoring, start the development server and test the block.

1. ローカル開発サーバーを起動します。

   ```bash
   npm run start
   ```

1. In a browser, navigate to a product page that has pre-populated reviews and Q&amp;A content. 例：

   ```shell-session
   http://localhost:3000/products/<product-slug>/ADB153
   ```

1. Verify that the product review block displays reviews and Q&amp;A content, and that the submission forms work.

手動テストを実行するか、担当者にブラウザー機能を使用してテストを依頼します。

```shell-session
Run complete browser testing. Use the following product page 'http://localhost:3000/products/<product-slug>/ADB153'
```

### Step 8: Clean up

テストをスキップまたは完了した後、エージェントは最終的な&#x200B;**クリーンアップ** フェーズに進むよう促します。 確認すると、エージェントは実装中に作成されたすべてのドキュメントアーティファクトをアーカイブします。

## トラブルシューティング

Use the following tips if you encounter issues during the tutorial.

### Backend (App Builder)

| Symptom | 原因 | Fix |
|---------|-------|-----|
| GET or POST returns 500 &quot;Cannot find module&quot; | The product-reviews actions use `require("../../utils")` or `require("../../constants")`, which escape the package bundle. Those files are not included when the package is deployed. | Make the product-reviews package self-contained. Add `actions/product-reviews/lib/constants.js` and `actions/product-reviews/lib/utils.js`, and update all four actions to require from `../lib/...` instead of `../../`. |
| GET returns 500 with &quot;key must match pattern&quot; | State keys use colons (for example, `reviews:ADB153`). `aio-lib-state` allows only `[a-zA-Z0-9-_.]`. | Change prefixes from `reviews:` and `qa:` to `reviews.` and `qa.`. Add a `stateKey(prefix, sku)` helper that sanitizes the SKU (replace invalid chars with `_`). |
| POST returns 500 with &quot;value must be string&quot; | `aio-lib-state` accepts only string values. The code passes arrays or objects to `state.put()`. | Serialize with `JSON.stringify()` when writing and `JSON.parse()` when reading. Update all four actions. |

{style="table-layout:auto"}

### Storefront (Edge Delivery Services)

| Symptom | 原因 | Fix |
|---------|-------|-----|
| Block does not render on test page | The block element is nested inside an extra `div`, so after `decorateSections` the block selector (`div.section > div > div`) does not match. | Make the block a direct child of the section. Structure: `section > div.product-review` (or equivalent block class). Avoid `section > div > div.product-review`. |
| Invalid CSS tokens | The block uses design tokens that do not exist in `styles/styles.css` (for example, `--color-error-100`, `--type-detail-font-size`). | Ask the agent to validate tokens against the project&#39;s `styles/styles.css` and replace invalid tokens with existing ones (for example, `--color-alert-*`, `--type-details-caption-*`). |

{style="table-layout:auto"}

## チュートリアルの概要

このチュートリアルで取り上げたトピックの概要を次に示します。

- **Extension development:** Describing functionality to create and view product review and Q&amp;A content  on a storefront with an Adobe Commerce as a Cloud Service backend to an AI agent and how to implement this functionality by generating a working REST API with four endpoints using [!DNL App Builder].
- **Persistence:** Using `aio-lib-state` with correct key format and JSON-serialized values.
- **Mock data and pre-population:** Creating a mock data file and using curl to pre-populate the API for CLI and storefront testing.
- **サービス契約：** バックエンドの拡張機能とストアフロント実装を橋渡しするAPI契約を作成しています。
- **段階的なストアフロント統合：** AI支援のスキルを使用して、要件、アーキテクチャ、実装を進める。
- **PDP block:** Adding a product review block to the PDP that displays reviews and Q&amp;A with submission forms and pagination.

## 次のステップ

Use the following suggestions to extend your product reviews service:

- **Add moderation:** Implement a moderation workflow for review and Q&amp;A content before it is published.
- **Add authentication:** Require shoppers to be logged in to submit reviews or Q&amp;A content, and associate submissions with customer accounts.
- **Add a subscription management page:** Create a storefront page where shoppers can view and edit their reviews.
- **マルチテナントのデプロイメントをサポート：** ステート管理を拡張して、1つのApp Builder アプリで複数のCommerce テナントをサポートします。
- **Add rate limiting:** Implement rate limits on the API to prevent abuse.
