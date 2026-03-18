---
title: 製品レビュー拡張機能のチュートリアル
description: App Builder、Edge Delivery Services、AI 支援開発ツールを使用して、Adobe Commerce as a Cloud Serviceの製品レビューおよび Q&A 拡張機能を作成する方法について説明します。
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: 9c76bae29c05909406a40ca03a2b3d242db05f3f
workflow-type: tm+mt
source-wordcount: '2470'
ht-degree: 0%

---

# 製品レビュー拡張機能のチュートリアル

このチュートリアルでは、[!DNL Adobe Commerce as a Cloud Service] および AI 支援の開発ツールを使用して、顧客が [!DNL Adobe App Builder] バックエンドでストアフロントの製品レビューと Q&amp;A コンテンツを送信できる拡張機能の構築について説明します。 この拡張機能は、買い物客が製品のレビューや質問と回答（Q&amp;A）コンテンツを表示および送信し、製品詳細ページ（PDP）に表示するための REST API エンドポイントを提供します。

次の 2 つのパーツを作成します。

- **App Builder拡張機能** - `aio-lib-state` で検証、ページネーション、永続性を備えた製品レビューおよび Q&amp;A コンテンツを作成および表示するための、GETおよび POST 操作を含む REST API。
- **ストアフロント統合** - PDP 上の製品レビューブロックで、レビューと Q&amp;A を表示し、買い物客がレビュー、質問、回答を送信するためのフォームを備えます。

>[!NOTE]
>
>AI エージェントは非決定的です。 このチュートリアルのプロンプト、質問および出力は、例です。 エージェントは、異なる質問、要件、またはアーキテクチャの提案を作成する場合があります。 このチュートリアルの例を使用して、エージェントを同様の結果に導きます。

開始する前に、[&#x200B; 前提条件 &#x200B;](./tutorial-prerequisites.md) を完了してください。 このチュートリアルでは、**統合スターターキット** を使用します。 クローンが既に作成されていて、前提条件ページに記載されている設定手順を完了していることを確認します。

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

上記のコマンドのいずれかで期待される結果が返されない場合は、[&#x200B; 前提条件 &#x200B;](./tutorial-prerequisites.md) を参照してガイダンスを確認してください。

さらに、次の点も確認してください。

- 製品データを含む [!DNL Adobe Commerce as a Cloud Service] インスタンスがあります。 [Commerce Cloud サービスインスタンス &#x200B;](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview){target="_blank"} を参照してください。
- [!DNL Commerce] インスタンスに接続されたストアフロントプロジェクトがある。 ストアフロントがない場合は、[&#x200B; ストアフロントの作成 &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/){target="_blank"} の手順に従ってください。
- `aem` CLI がインストールされます。

  ```bash
  npm install -g @adobe/aem-cli
  ```

## 拡張機能の開発

このセクションでは、AI 支援の開発ツールを使用して、[!DNL Adobe Commerce as a Cloud Service] バックエンドでストアフロントの拡張機能に関する製品レビューと Q&amp;A コンテンツを送信および表示する拡張機能を開発する手順を説明します。 この拡張機能は、製品レビューと Q&amp;A コンテンツを送信および表示し、PDP に表示するための REST API を提供します。

1. コーディングエージェントの MCP 設定に移動します。 例えば、カーソルでは、**[!UICONTROL Cursor]**/**[!UICONTROL Settings]**/**[!UICONTROL Cursor Settings]**/**[!UICONTROL Tools & MCP]** に移動します。 `commerce-extensibility` ツールセットがエラーなく有効になっていることを確認します。 エラーが表示された場合は、ツールセットのオン/オフを切り替えます。

   >[!NOTE]
   >
   >AI 支援による開発ツールを使用する場合、エージェントによって生成されるコードと応答に自然なバリエーションが生じることを期待してください。
   >コードで問題が発生した場合は、デバッグの支援をエージェントに依頼します。

1. カーソルのコンテキストにドキュメントを追加した場合は、無効にします。

   **[!UICONTROL Cursor]**/**[!UICONTROL Settings]**/**[!UICONTROL Cursor Settings]**/**[!UICONTROL Indexing & Docs]** に移動し、一覧表示されているドキュメントをすべて削除します。

### 手順 1：最初のプロンプトを指定する

AI エージェントに実装を開始するように促します。 エージェントに停止して質問するように伝えることで、実装を早期に導くのに役立ちます。

エージェントのチャットウィンドウに次のプロンプトを入力します。

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
>処理を進める前にエージェントに停止して質問をするよう伝えると、実装をプロセスの初期に導くのに役立ちます。 これにより、主要な前提と欠落している要件が早い段階で特定され、このチュートリアルのガイド付きワークフローを開始する際に必要になります。

### 手順 2：エージェントの質問に回答する

エージェントは、ソリューションの作成を開始する前に、回答する必要がある一連の質問を返します。 次の例は、一般的な質問と回答を示しています。 エージェントが異なる質問をする場合がありますが、トピックは一般的に同じです。

**エージェントの質問の例：**

1. **REST API （ホストおよびコンシューマー**— CRUD REST API は、ストアフロントが呼び出すこのApp Builder アプリ（Adobe I/O Runtime上の web アクション）の一部にする必要がありますか？ 誰が（EDS ストアフロント、カスタム/ヘッドレスストアフロント、またはその両方）と呼びますか。 CORS、公開（未認証）アクセスが必要ですか。それとも、呼び出し元は API キーまたは OAuth を使用しますか。
1. **データモデル** - 1 つの「レビュー」または「質問」は何を表すでしょうか？ 顧客識別子（電子メールのみ、または顧客 ID）? 商品識別子（SKU のみ、または SKU +店舗表示） 同じ顧客が同じ SKU に対して複数のレビューを送信できますか？
1. **永続性** - レビュー `aio-lib-state`Q&amp;A を永続化するのに適切な場所ですか。それとも、外部ストアがありますか。 デザインではマルチテナントとシングルテナントのどちらを想定するべきですか？
1. **ページネーションセマンティクス** - Q&amp;A GETの場合、質問のみ（ネストされた回答を含む）に適用されま `limit` んか、質問と回答の総数に適用されますか？

**回答の例：**

```shell-session
1. The REST API should be part of this App Builder app. It will be called by the EDS Storefront. No authentication — public access for both GET and POST.
2. For reviews: sku, rating (1-5), optional review text, optional user name. For Q&A: sku, type (question or answer), content, optional user. Answers linked to questions via questionId. Allow multiple reviews per SKU from the same user.
3. Use aio-lib-state. Single tenant for now.
4. Pagination by question — limit and offset apply to questions; each question includes its nested answers.
```

>[!NOTE]
>
>あなたのエージェントは異なる質問をする可能性があります。 同じ機能上の結果に向けてエージェントを導くためのガイダンスとして、レビューと Q&amp;A を含むパブリック REST API、永続性、認証な `aio-lib-state` を使用します。

### 手順 3：要件とアーキテクチャのレビュー

エージェントは、確認する要件およびアーキテクチャ文書を生成します。 要件が提供した回答と一致し、アーキテクチャが次の内容をカバーしていることを確認します。

- 4 つの web アクション：`reviews-get`、`reviews-post`、`qa-get`、`qa-post`
- 許可されたパターンに準拠したキーを持つ `aio-lib-state` を使用した永続性（`[a-zA-Z0-9-_.]` — コロンなし）
- （生のオブジェクトや配列ではなく） JSON 文字列として格納された値をステートします
- 自己完結型パッケージ – バンドルをエスケープするパス経由ではなく、`product-reviews` パッケージ内の共有コード（ユーティリティ `../../` 定数）

>[!NOTE]
>
>AI エージェントは非決定的で、その動作はモデルや IDE によって異なります。 異なる要件やアーキテクチャを生み出す異なる質問セットが得られる場合があります。 その場合は、続行する前に、このチュートリアルで示している内容に厳密に一致する実装を使用するように、エージェントを誘導してください。

### 手順 4：実装計画の選択

エージェントでは、詳細な導入計画を作成するか、直接導入を完了するかを選択できます。

- より詳細な制御を行いながら段階的に実行できる表示可能なプランが必要な場合は、最初のオプションを選択します。
- エージェントが最小限の介入で完全な実装を行う場合は、2 番目のオプションを選択します。

### 手順 5：拡張機能のデプロイ

エージェントによる実装が完了したら、拡張機能をデプロイします。

```bash
aio app deploy
```

エージェントがアクションに `require-adobe-auth: true` を追加した場合は、ストアフロントから直接エンドポイントを呼び出せるように、認証を削除するように依頼します。

```shell-session
Remove the requirement to provide a valid Adobe IMS access token from all product-reviews actions.
```

その後、次の手順で再デプロイします。

```bash
aio app deploy
```

### 手順 6：モックデータの作成とテスト用の事前入力

モックデータファイルを作成し、curl を使用して API に事前入力して、CLI およびストアフロントでテストするためのサンプルレビューと Q&amp;A コンテンツを得ます。

1. サンプルデータを含むファイル `docs/mock-product-reviews-data.json` （または同様のファイル）を作成します。 例：

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

1. curl を使用して、デプロイ済みの API にデータを POST します。

   `<your-runtime-url>` を実際のApp Builder ランタイム URL （例：`https://1172492-prodreviewqa135-stage.adobeioruntime.net`）に置き換えます。

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

1. GET リクエストでデータを検証します。

   ```bash
   curl -s "$API_URL/reviews-get?sku=ADB153"
   curl -s "$API_URL/qa-get?sku=ADB153"
   ```

>[!TIP]
>
>レビューと Q&amp;A コンテンツの両方がある製品には SKU `ADB153` を使用し、レビューのない製品には `ADB152` を使用します。 このデータ設定により、ストアフロントでデータが入力された状態と空の状態の両方をテストできます。

### 手順 7：拡張機能をテストする

担当者にテスト手順を指示するか、または前の手順で示した curl の例を使用します。 次の例は、一般的なテストコマンドを示しています。

**レビューの送信：**

```bash
API_URL="https://<your-runtime-url>/api/v1/web/product-reviews"
curl -s -X POST "$API_URL/reviews-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","rating":5,"review":"Excellent!","user":"test@example.com"}'
```

**リストのレビュー：**

```bash
curl -s "$API_URL/reviews-get?sku=ADB153"
```

**質問を送信：**

```bash
curl -s -X POST "$API_URL/qa-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","type":"question","content":"Is this dishwasher safe?","user":"test@example.com"}'
```

**回答を送信** （質問に対する応答の `id` を `questionId` のように使用します）。

```bash
curl -s -X POST "$API_URL/qa-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","type":"answer","questionId":"<QUESTION-UUID>","content":"Yes, it is.","user":"support@example.com"}'
```

### サービス契約の作成

サービスの実装が完了したら、エージェントに対して、ストアフロント作業用のサービス契約の作成を依頼します。

```shell-session
Create a service contract for the Product Review and Q&A application that defines the API endpoints, request and response formats, and any necessary data models. Ensure that the service contract is clear and detailed enough for a frontend developer to implement the storefront integration without needing to ask additional questions about the API. Name this file PRODUCT_REVIEW_QA_CONTRACT.md
```

このファイルをストアフロントプロジェクトにコピーして、ストアフロントエージェントが参照できるようにします。

## ストアフロントに接続

このセクションでは、[!DNL Edge Delivery Services] と AI による開発ツールを使用して、製品レビューのストアフロント部分と Q&amp;A 拡張機能を実装する手順を説明します。 PDP に、レビューと Q&amp;A の両方のコンテンツを表示し、買い物客が新しいコンテンツを送信できるようにする製品レビューブロックを追加します。

>[!NOTE]
>
>表示されるプロンプトは開始点です。 変更せずに使用できますが、エージェントと自然に会話することを検討してください。
>
>AI 支援開発ツールを使用する場合、エージェントによって生成されるコードと応答には常に自然なバリエーションがあります。
>
>コードで問題が発生した場合は、デバッグの支援をエージェントに依頼します。

### ストアフロントの前提条件

ストアフロントの統合を開始する前に、次の点を確認してください。

- [!DNL Commerce] インスタンスに接続されたストアフロントプロジェクト
- Commerce ストアフロントの AI ツール [CLI を使用してインストール &#x200B;](./tutorial-prerequisites.md#install-the-storefront-ai-tools)
- ストアフロントプロジェクトにコピーされた `PRODUCT_REVIEW_QA_CONTRACT.md` ファイル

### 手順 1：環境を検証する

`config.json` ファイルを開き、`commerce-core-endpoint` と `commerce-endpoint` の値が [!DNL Adobe Commerce as a Cloud Service] GraphQL エンドポイントを指していることを確認します。

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### 手順 2：最初のプロンプトを指定する

サービス契約がプロジェクトに既に存在する場合は、製品レビューブロックを実装するようにエージェントに促します。 エージェントで **プラン** モードが使用可能な場合は、そのモードを使用して、エージェントがプランなしで進行しないようにします。

```shell-session
Analyze @PRODUCT_REVIEW_QA_CONTRACT.md and build a product review block using the API specified in the contract. The block displays both reviews and Q&A content on the product detail page, with forms for shoppers to submit reviews, questions, and answers. Use the project manager skill to plan this implementation.
```

>[!TIP]
>
>プロジェクトマネージャーのスキルトリガーを使用するよう特別にリクエストする場合は、実装の舵を切るのに役立つ段階的なワークフローを提供します。 これにより、主要な前提条件と欠落している要件がプロセスの早い段階で特定されます。

### 手順 3：明確な質問に回答する

エージェントは、ソリューションの作成を開始する前に、回答する必要がある一連の質問を返します。 次の例は、一般的な質問と回答を示しています。 エージェントが異なる質問をする場合がありますが、トピックは一般的に同じです。

**エージェントの質問の例：**

1. **API ベース URL** - ストアフロントは製品レビュー API ベース URL をどのように取得する必要がありますか？ オプションには、設定ブロック（`apiBaseUrl` を含むテーブルなど）、グローバルプレースホルダー、またはその他のアプローチを含めることができます。
1. **SKU ソース** - ブロックは、PDP コンテキスト（現在の製品）またはブロック設定から SKU を読み取る必要がありますか？
1. **フォームの動作** – 送信に成功した後、フォームを非表示にする、成功メッセージを表示する、または表示はされても無効のままにする必要はありますか？

**回答の例：**

```shell-session
1. Block table config with apiBaseUrl (required). Each block instance can point to its own deployment.
2. From block table if set; otherwise use getProductSku() so it works on PDP without authoring a SKU.
3. Show a success message above the form; keep the form visible but disabled.
```

>[!NOTE]
>
>ブロック設定のプレースホルダーを、実際のApp Builder ランタイム URL （例：`https://1172492-prodreviewqa135-stage.adobeioruntime.net`）に置き換えます。
>
>あなたのエージェントは異なる質問をする可能性があります。 次の回答をガイダンスとして使用します。
>
>- API ベース URL はブロックテーブルから取得する必要があるので、コードを変更せずに変更できます。
>- 設定されている場合は、ブロックテーブルからの SKU。設定されていない場合は、PDP の現在の製品からの SKU。
>- 送信に成功したら、成功メッセージを表示してフォームを無効にします。

### 手順 4：要件とアーキテクチャのレビュー

エージェントは、レビュー用に要件ドキュメントを更新します。 次のことを確認します。

- ブロックは、レビュー（評価、ユーザー、日付、テキストを含む）および Q&amp;A （ネストされた回答を含む質問）をレンダリングします。
- レビュー、質問および回答を送信するためのFormsが存在します。
- ページネーションは、レビューと Q&amp;A コンテンツの両方でサポートされます。
- API 統合では、ブロックテーブルのベース URL を使用します。
- 成功とエラーの状態は契約に従って処理されます。

>[!NOTE]
>
>AI エージェントは非決定的で、その動作はモデルや IDE によって異なります。 異なる要件やアーキテクチャを生み出す異なる質問セットが得られる場合があります。 その場合は、続行する前に、このチュートリアルで示している内容に厳密に一致する実装を使用するように、エージェントを誘導してください。

### 手順 5：実装計画の選択

エージェントでは、詳細な導入計画を作成するか、直接導入を完了するかを選択できます。

- より詳細な制御を行いながら段階的に実行できる表示可能なプランが必要な場合は、最初のオプションを選択します。
- エージェントが最小限の介入で完全な実装を行う場合は、2 番目のオプションを選択します。

実装時に、エージェントはブロック・ファイルを作成および変更します。 生成されるコードを監視し、必要に応じて質問したり、エージェントをリダイレクトしたりできます。 ブロックがレンダリングされない場合は、セクションの装飾とブロック検出パターンを分析するようにエージェントに依頼します。ブロック要素はセクションの直接の子である必要があり、フレームワークがそれを見つけられるようにします。

### 手順 6：ドキュメントオーサリングでの製品ページにブロックを追加

製品レビューブロックを製品ページテンプレートに追加して、すべての PDP に表示されるようにします。 ドキュメントオーサリングサービス（da.live）を使用して、ブロックを追加し、設定します。

1. ドキュメントオーサリングサービス（例：[da.live](https://da.live/)）を開きます。

1. プロジェクトスペースをクリックし、**products** フォルダーを開いて **default** （`products/default`）を選択します。

1. 新しいブロックセクションを追加します。

   ブロックテーブルで、ブロック名 **product-review** （またはエージェントが作成したブロック名）を持つ行を追加します。

1. 必要な設定を使用してブロックを設定します。
   - **apiBaseUrl** - App Builder ランタイム URL （例：`https://<namespace>-<app-name>-stage.adobeioruntime.net`）。
   - **sku** – 空のままにして PDP で現在の製品の SKU を使用するか、特定の SKU を入力してその製品のみのレビューを表示します。

1. 「**[!UICONTROL Publish]**」をクリックして変更を公開します。

### 手順 7：サーバーを起動してテストする

ドキュメントオーサリングで製品ページにブロックを追加したら、開発サーバーを起動してブロックをテストします。

1. ローカル開発サーバーを起動します。

   ```bash
   npm run start
   ```

1. ブラウザーで、レビューと Q&amp;A コンテンツが事前入力されている製品ページに移動します。 例：

   ```shell-session
   http://localhost:3000/products/<product-slug>/ADB153
   ```

1. 製品レビューブロックにレビューと Q&amp;A コンテンツが表示され、送信フォームが機能することを確認します。

手動でテストを実行することも、エージェントに対してブラウザー機能を使用してテストを実行するように依頼することもできます。

```shell-session
Run complete browser testing. Use the following product page 'http://localhost:3000/products/<product-slug>/ADB153'
```

### 手順 8：クリーンアップ

テストをスキップまたは完了すると、最終 **クリーンアップ** フェーズに進むようにエージェントから求められます。 確認時に、エージェントは実装時に作成されたすべてのドキュメントアーティファクトをアーカイブします。

## トラブルシューティング

チュートリアル中に問題が発生した場合は、次のヒントを参考にしてください。

### バックエンド（App Builder）

| 症状 | 原因： | 修正 |
|---------|-------|-----|
| GETまたは POST で「Cannot find module」が 500 を返す | 製品レビューアクションでは、`require("../../utils")` または `require("../../constants")` を使用して、パッケージバンドルをエスケープします。 これらのファイルは、パッケージのデプロイ時には含まれません。 | 製品レビューパッケージを自己完結型にします。 `actions/product-reviews/lib/constants.js` と `actions/product-reviews/lib/utils.js` を追加し、`../lib/...` ではなく `../../` から必要な 4 つのアクションをすべて更新します。 |
| GETは、「キーはパターンに一致する必要があります」を含む 500 を返します | 状態キーはコロンを使用します（例：`reviews:ADB153`）。 `aio-lib-state` では `[a-zA-Z0-9-_.]` のみが許可されます。 | プレフィックスを `reviews:` と `qa:` から `reviews.` と `qa.` に変更します。 SKU を不要部分から削除する `stateKey(prefix, sku)` ヘルパーを追加します（無効な文字は `_` に置き換えます）。 |
| POST は、「値は文字列である必要があります」を含んだ 500 を返します | `aio-lib-state` には、文字列値のみを使用できます。 このコードは、配列またはオブジェクトを `state.put()` に渡します。 | 書き込み時は `JSON.stringify()` で、読み取り時は `JSON.parse()` でシリアル化します。 4 つのアクションをすべて更新します。 |

{style="table-layout:auto"}

### ストアフロント（Edge Delivery Services）

| 症状 | 原因： | 修正 |
|---------|-------|-----|
| テストページでブロックがレンダリングされない | ブロック要素は余分な `div` 内にネストされているので、`decorateSections` 後のブロックセレクター（`div.section > div > div`）は一致しません。 | ブロックをセクションの直接の子にします。 構造：`section > div.product-review` （または同等のブロッククラス）。 `section > div > div.product-review` を避けます。 |
| 無効な CSS トークン | ブロックが、`styles/styles.css` に存在しないデザイントークンを使用します（例：`--color-error-100`、`--type-detail-font-size`）。 | エージェントに対してプロジェクトの `styles/styles.css` に照らしてトークンを検証し、無効なトークンを既存のトークンに置き換えるように依頼します（例：`--color-alert-*`、`--type-details-caption-*`）。 |

{style="table-layout:auto"}

## チュートリアルの概要

このチュートリアルで扱うトピックの概要は次のとおりです。

- **拡張機能の開発：** AI エージェントにバックエンドのAdobe Commerce as a Cloud Serviceを使用して、ストアフロントで製品のレビューと Q&amp;A コンテンツを作成および表示する機能と、[!DNL App Builder] を使用して 4 つのエンドポイントを持つ動作する REST API を生成して、この機能を実装する方法について説明します。
- **永続性：** 正しいキー形式と JSON シリアル化された値を持つ `aio-lib-state` を使用します。
- **モックデータと事前入力：** モックデータファイルを作成し、curl を使用して CLI およびストアフロントエンドテスト用の API に事前入力します。
- **サービス契約：** バックエンドの拡張機能とストアフロントの実装を橋渡しする API コントラクトを作成しています。
- **段階的なストアフロントの統合：** AI 支援のスキルを使用して、要件、アーキテクチャ、実装を進めます。
- **PDP ブロック：** PDP に、送信フォームとページネーションを含むレビューと Q&amp;A を表示する製品レビューブロックを追加します。

## 次の手順

次の提案を使用して、製品レビューサービスを拡張します。

- **モデレートを追加：** 公開する前にレビューおよび Q&amp;A コンテンツ用のモデレートワークフローを実装します。
- **認証を追加：** レビューまたは Q&amp;A コンテンツを送信し、送信を顧客アカウントに関連付けるために、買い物客がログインする必要があります。
- **購読管理ページを追加：** 買い物客がレビューを表示および編集できるストアフロントページを作成します。
- **マルチテナントデプロイメントのサポート：** ステート管理を拡張して、1 つのApp Builder アプリで複数のCommerce テナントをサポートします。
- **レート制限を追加：** 不正使用を防ぐために、API にレート制限を実装します。
