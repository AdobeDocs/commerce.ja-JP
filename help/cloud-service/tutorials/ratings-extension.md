---
title: レーティング拡張機能チュートリアル
description: App BuilderとAI支援の開発ツールを使用して、Adobe Commerce as a Cloud Serviceの商品レーティング拡張機能を構築する方法について説明します。
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
TQID: 'https://experienceleague.adobe.com/vqVQg6XUHNyrNMh5vJR13SgswBMj9eFXMQ7Cow-FLHU'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: ba9e5be9-7de1-4f71-a5d2-baead0e425eeid: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: cc72dcf1-72e1-48cc-b434-e7c27d62d67cid: ce44533e-8ec8-4e11-a9e9-78b0fe561832id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: ef32511703a96b5f4db32d54229e9a7cbe961f12
workflow-type: tm+mt
source-wordcount: 1738
ht-degree: 0%

---

# 評価拡張機能のチュートリアル

このチュートリアルでは、[!DNL Adobe App Builder]とAI支援の開発ツールを使用して、[!DNL Adobe Commerce as a Cloud Service]の製品評価拡張機能を構築する方法について説明します。

開始する前に、[前提条件](./tutorial-prerequisites.md)を完了してください。

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

上記のコマンドのいずれかが期待される結果を返さない場合は、ガイダンスについて[前提条件](./tutorial-prerequisites.md)を参照してください。

## 拡張機能の開発

このセクションでは、AIを活用した開発ツールを使用して、Adobe Commerce as a Cloud Serviceのレーティング拡張機能を開発する方法を説明します。

1. **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**&#x200B;に移動し、`commerce-extensibility` ツールセットがエラーなしで有効になっていることを確認します。 エラーが表示された場合は、ツールセットのオンとオフを切り替えます。

   ![MCP コマース拡張性ツールセットが有効になっているカーソル IDE設定](../assets/cursor-settings.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   >AI支援の開発ツールを使用する場合、エージェントによって生成されたコードと応答に自然なバリエーションが存在することを期待します。
   >コードで問題が発生した場合は、いつでもエージェントにデバッグを依頼できます。

1. カーソルのコンテキストで任意のドキュメントを無効にします。

   * **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Indexing & Docs]**&#x200B;に移動し、一覧されているドキュメントをすべて削除します。

   ![ カーソルのインデックス作成とドキュメントの設定（ドキュメント リストが空） ](../assets/disable-documentation.png){width="600" zoomable="yes"}

1. 商品レーティング拡張機能のコードを生成：
   * カーソル チャット ウィンドウから、**[!UICONTROL Agent]** モードを選択します。
   * 次のプロンプトを入力します。

   ```shell-session
   Implement an Adobe Commerce as a Cloud Service extension to handle Product Ratings.
   
   Implement a REST API to handle GET ratings requests.
   
   GET requests will have to support the following query parameters:
   
   sku -> product SKU
   ```

   >[!NOTE]
   >
   >担当者がドキュメントの検索をリクエストした場合は、許可します。

1. 担当者の質問に正確に答えて、最適なコードを生成できます。

   拡張機能プロンプトが入力されたエージェント モードの![ カーソル チャット ウィンドウ ](../assets/enter-prompt.png){width="600" zoomable="yes"}

   拡張機能の要件について明確な質問を求める![AI エージェント ](../assets/agent-questions.png){width="600" zoomable="yes"}

1. 次のサンプルテキストを使用して、エージェントの質問に答え、ランダムな評価データを設定します。

   ```shell-session
   Yes, this headless extension is for Adobe Commerce as a Cloud Service storefront,
   but we do not need any authentication for the GET API because guest users should be able to use it on the storefront.
   
   This extension is called directly from the storefront, no async invocation, such as events or webhooks, is required.
   
   Start with just the GET API for now, we will implement other CRUD operations at a later time.
   
   We do not need a DB or storage mechanism right now, just return random ratings data between 1 and 5 and a ratings count between 1 and 1000.
   
   The API should only return the average rating for the product and the total number of ratings.
   We do not need to add tests right now.
   ```

   エージェントは、実装の信頼できる唯一の情報源として機能する`requirements.md` ファイルを作成します。

   実装の詳細を含むAI エージェントによって作成された![Requirements.md ファイル ](../assets/requirements-file.png){width="600" zoomable="yes"}

1. `requirements.md` ファイルを確認し、計画を確認します。

   すべてが正しく見える場合は、エージェントに対して&#x200B;**フェーズ 2 - アーキテクチャ計画**&#x200B;に移動するよう指示します。

1. アーキテクチャ計画の見直し：

1. エージェントにコード生成を続行するように指示します。

   エージェントは必要なコードを生成し、次の手順を詳しく説明します。

   ![評価APIのAI エージェントフェーズ 2 アーキテクチャ計画](../assets/architecture-planning.png){width="600" zoomable="yes"}

   ![生成されたコードファイルと構造の概要](../assets/code-generation-summary.png){width="600" zoomable="yes"}

   ![ テストとデプロイメントの次の手順を提供するAI エージェント ](../assets/next-steps.png){width="600" zoomable="yes"}

### 拡張機能をローカルでテストする

次の手順では、拡張機能をデプロイする前に拡張機能が機能することを確認する方法について説明します。

1. 担当者に、コードをローカルでテストする方法を尋ねます。

   ```shell-session
   Test the ratings API locally on a dev server using cURL.
   ```

1. エージェントの指示に従い、APIがローカルで動作していることを確認します。

   ローカル API テスト用の![AI エージェントの手順](../assets/local-testing.png){width="600" zoomable="yes"}

   ![cURLを使用したローカル API テストの結果が正常に表示されたターミナル ](../assets/local-testing-1.png){width="600" zoomable="yes"}

### 拡張機能のデプロイ

エージェントを使用して拡張機能を[!DNL Adobe I/O Runtime]にデプロイします。

1. 生成されたコードを確認したら、次のプロンプトを使用して拡張機能をデプロイします。

   ```shell-session
   Deploy the ratings API.
   ```

   エージェントは、デプロイ前にデプロイ準備評価を実行します。

   ![AI エージェント導入前の準備評価チェックリスト ](../assets/pre-deployment-assessment.png){width="600" zoomable="yes"}

1. 評価結果に確信がある場合は、展開を続行するようにエージェントに指示します。

   エージェントはMCP ツールキットを使用して、検証、ビルド、デプロイを自動的に行います。

   ![MCP ツールキット検証のビルドとデプロイメントのプロセス ](../assets/deployment-process.png){width="600" zoomable="yes"}

### デプロイメントの確認

ストアフロントに統合する前に、APIをテストします。 担当者は、新しいアクションの場所とテスト戦略を提供する必要があります。

![ デプロイされたアクション URLとテストコマンドを使用したAI エージェントテスト戦略](../assets/testing-strategy.png){width="600" zoomable="yes"}

ターミナルでcURLを使用してAPIを手動でテストすることもできます。

```bash
curl -s "https://<your-site>.adobeioruntime.net/api/v1/web/ratings/ratings?sku=TEST-SKU-123"
```

![ デプロイ済み評価APIのcURL テストに成功したことを示すターミナル ](../assets/curl-test.png){width="600" zoomable="yes"}

### Edge Delivery Servicesとの統合

[!DNL Edge Delivery Services]によって提供される[!DNL Adobe Commerce] ストアフロントと評価APIを統合するには、エージェントに対して、評価APIの要件を含むサービス契約を作成するように依頼します。

```shell-session
Create a service contract for the ratings api that I can pass on to the storefront agent. Name it RATINGS_API_CONTRACT.md
```

![ ストアフロント統合用のサービス契約ファイルを作成するAI エージェント ](../assets/create-contract.png){width="600" zoomable="yes"}

エンドポイントと応答の詳細が記載された![評価API契約マークダウン ファイル ](../assets/contract.png){width="600" zoomable="yes"}

ターミナルに戻り、`extension` フォルダーで次のコマンドを実行して、契約ファイルを`storefront` フォルダーにコピーします。

```bash
cp RATINGS_API_CONTRACT.md ../storefront
```

## ストアフロントへの接続

このセクションでは、[!DNL Edge Delivery Services]とAI支援の開発ツールを使用して、評価の拡張機能のストアフロント部分を実装する方法について説明します。

>[!NOTE]
>
>提供されるプロンプトは出発点です。 変更せずに使用することはできますが、エージェントと自然な会話をすることを検討してください。
>
>AI支援の開発ツールを使用する場合、エージェントによって生成されたコードと応答には常に自然なバリエーションがあります。
>
>コードで問題が発生した場合は、担当者にデバッグのサポートを依頼してください。

### ストアフロントの前提条件

ストアフロント統合を開始する前に、次の点を確認してください。

* [!DNL Commerce] インスタンスに接続されたストアフロントプロジェクト
* Commerce ストアフロント AI ツール [CLIを使用してインストール ](./tutorial-prerequisites.md#install-the-storefront-ai-tools)

### ストアフロントワークスペースの設定

開発用にローカルのストアフロント環境を準備します。

1. `storefront` フォルダーに移動します。

   ```bash
   cd storefront
   ```

1. 新しいカーソルウィンドウでストアフロントフォルダーを開きます。

   または、[Cursor CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands)がインストールされている場合は、ターミナルで次のコマンドを使用してウィンドウを開きます。

   ```bash
   cursor .
   ```

1. ローカル開発サーバーを起動します。

   ```bash
   npm run start
   ```

1. ブラウザーで、製品ページに移動します。

   ```shell-session
   http://localhost:3000/products/llama-plush-shortie/adb336
   ```

1. 定型文のストアフロント製品詳細ページ（PDP）を確認し、視覚的な製品評価がないことに注意してください。

### 評価APIの統合

エージェントを使用して、評価APIをストアフロントの商品詳細ページに統合します。

1. エージェントで次のプロンプトを使用します。

   ```shell-session
   Integrate the ratings API into the PDP to show star ratings and a review count for products. Here's the service contract: @RATINGS_API_CONTRACT.md
   ```

1. 担当者は、タスクの複雑さを評価し、段階的なワークフローを呼び出します。 **フェーズ 1 （要件収集）**&#x200B;中、担当者は要件文書を作成し、次のような質問を明確にします。

   * PDPのどの部分に評価が表示されますか？
   * 新しいスタンドアロンブロックにするか、既存のPDP ドロップインコンポーネント内でスロットをカスタマイズするか。
   * APIが使用できない場合やデータが返されない場合、フォールバックはどうなりますか？
   * 評価はPLP （製品リスト）にも表示されますか、それともPDPのみですか？
   * デザインスペックやモックアップはありますか？

   プロジェクトの要件にもとづいて、これらの質問に答えましょう。 担当者は要件ドキュメントを更新し、フェーズを「完了」とマークします。

1. **フェーズ 2 （アーキテクチャ プランニング）**&#x200B;中、エージェントはアーキテクチャを提案する前にドキュメントとコードベースを調査します。 エージェントには次の操作を期待します。

   * PDP ドロップインコンテナ、スロット、およびイベントペイロードについて、[!DNL Commerce]のドキュメントを検索します。
   * `blocks` ディレクトリと`scripts/initializers/` フォルダーをスキャンして、既存のPDP関連コードを探します。
   * 使用可能なコンテナとスロットコンテキストシェイプのTypeScript定義について説明します。

   次に、エージェントは次のようなアーキテクチャオプションを表示します。

   * **オプション A:**&#x200B;既存のPDP ドロップインスロットをカスタマイズして、製品タイトルの近くに評価を挿入します。軽いタッチでアップグレードに対応します。
   * **オプション B:** APIから個別に取得する新しいスタンドアロン `product-ratings` ブロックを作成します。より柔軟で分離されています。
   * **オプション C:**&#x200B;製品SKUのPDP ドロップインイベントもリッスンする新しいブロックを作成します。これは、ハイブリッドなアプローチです。

   プランには、API統合、パフォーマンスに関する考慮事項（遅延読み込み、キャッシュ）、セキュリティ（入力のサニタイズ）、テストアプローチの詳細も含まれています。

   アーキテクチャプランを確認し、続行するようにエージェントに指示します。

1. **フェーズ 3 （実装アプローチ）**&#x200B;中、エージェントは次のいずれかを選択するよう求めます。

   * **オプション A:** コードを生成する前に、詳細な実装計画を確認します（最初にすべてのファイル、パターン、コード構造を参照）。
   * **オプション B:** コード生成に直接進みます。

   お好みのアプローチを選択してください。

1. **フェーズ 4 （実装）**&#x200B;中、エージェントは選択したアーキテクチャに基づいてコードを生成します。 アプローチに応じて、エージェントはいくつかの専門的なスキルを使用します。

   * **コンテンツモデリング：**&#x200B;新しいブロックが必要な場合、エージェントは、API エンドポイント URLを持つ構成テーブルなど、作成者に適したコンテンツ構造を設計します。
   * **ブロック開発：** エージェントは、JavaScriptのデコレーション関数、スコープ CSS スタイル、アクセシビリティ用のARIA ラベル、読み込みエラーの状態の処理など、[!DNL Edge Delivery Services]の規則に従ってブロックファイルを作成します。
   * **ドロップインのカスタマイズ：** アーキテクチャでスロットのカスタマイズを使用している場合、エージェントは正しいコンテナをインポートし、製品タイトルの近くに検証済みのスロットを使用し、現在のSKUの製品データイベントを購読します。

   生成されるコードを確認し、必要に応じて質問したり、担当者に連絡したりできます。 エージェントは、コード生成が完了すると、実稼動準備状況のサマリーを生成します。

1. **フェーズ 4.5 （テスト）**&#x200B;中、エージェントは実装をテストすることを提案します。 受け入れる場合、担当者：

   * 適切なスクリプトとスタイルを使用してローカルテストページを作成します。
   * 開発サーバーを開始します。
   * ビジュアルレンダリング、インタラクティブ性、レスポンシブ動作、アクセシビリティ、パフォーマンスに対して、ブラウザベースの検証を実行します。
   * 結果を含む構造化テストレポートを生成します。

   ブラウザーに従って、動作を確認し、問題を報告します。

1. コードベースの変更を確認し、製品ページの更新を確認します。

   開発環境とブラウザーに次の変更が表示されます。

   * 製品評価コンポーネントが自動的に作成されます。
   * コンポーネントは、選択したアーキテクチャに応じて、[ ドロップインスロット ](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/customize/slots)またはスタンドアロンブロックとしてPDPに統合されます。
   * 星は、APIの評定値に基づいて適切な塗りつぶしの縦横比で表示されます。

   ![製品タイトルの下に統合された星評価を表示する製品詳細ページ ](../assets/product-ratings-implementation.png){width="600" zoomable="yes"}

## チュートリアルの概要

このチュートリアルで取り上げたトピックの概要を次に示します。

* **拡張機能の開発：** AI エージェントに新しい機能を記述し、[!DNL App Builder]を使用して動作するREST APIを生成する方法を学習します。
* **ローカルテストとデプロイメント：** APIをローカルにテストし、MCP ツールキットを使用してデプロイします。
* **サービス契約：** バックエンドの拡張機能とストアフロント実装を橋渡しするAPI契約を作成しています。
* **段階的なストアフロント統合：** AI支援のスキルを使用して、要件、アーキテクチャ、実装を進める。
* **ドロップイン統合：** [!DNL Adobe Commerce]個のドロップインコンテナとスロットの操作。
* **コンポーネントの再利用性：**&#x200B;複数のブロックで使用される共有コンポーネントを作成しています。

## 次のステップ

以下の推奨事項を使用して、評価の拡張機能をカスタマイズするか、独自の変更を作成します。

### 星の色を変更

エージェントで次のプロンプトを使用します。

```shell-session
Change the star fill color to red.
```

**予想される結果：**

星が赤に変わる。

![赤い星の塗りつぶし色で表示される製品の評価](../assets/red-star-colors.png){width="600" zoomable="yes"}

### 評価の分布モーダルの追加

次の手順は、エージェントがビジュアル参照を使用して複雑なUI機能を処理する方法を示しています。

1. **開始する前：**&#x200B;次のモック画像を保存し、ストアフロント担当者とのチャットに貼り付けます。

   ![ スターレベル別の評価分布の内訳を示すモックアップ ](../assets/rating-distribution-mockup.png){width="600" zoomable="yes"}

1. 参照画像をガイドとして使用して定格分布モーダルを作成するには、次の手順に従います。

   * 評価の分布を表す追加データを返すようにAPIを更新します。
   * API コントラクトを更新します。
   * ストアフロントのコードベースで契約を更新します。
   * ストアフロントエージェントに、参照画像と更新されたAPI契約を使用して、PDP ページに評価ディストリビューションを追加するように依頼します。

1. コードベースの次の変更を確認し、製品ページで更新を確認します。

   * エージェントによるビジュアルモックアップの解釈
   * アクセシビリティに適切なHTML構造を使用しているか
   * ポジショニングとインタラクションの状態の処理方法

#### 配布モーダルのトラブルシューティング

モーダルが期待どおりに動作しない場合は、次の操作を試してください。

* モーダルが表示されない場合は、ブラウザーコンソールでエラーを確認します。
* ポジショニングがオフの場合は、次の形式で修正するように担当者に依頼します。

  ```shell-session
  adjust the modal position to be...
  ```

![ スターレベルの分類バーを使用して詳細な評価分布を表示するモーダル ](../assets/rating-distribution-modal.png){width="600" zoomable="yes"}
