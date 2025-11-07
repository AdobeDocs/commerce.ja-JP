---
title: 評価拡張機能のチュートリアル
description: App Builderと AI 支援開発ツールを使用して、Adobe Commerce as a Cloud Serviceの製品評価拡張機能を作成する方法について説明します。
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 453b21f89d2024a8d6927fa082affdd5abb6e5cd
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---

# Adobe Developers Live - Adobe Commerce ラボワークブック

このラボでは、[!DNL Adobe Commerce as a Cloud Service] および AI を利用した開発ツールを使用して、[!DNL Adobe App Builder] 用の製品評価拡張機能を構築する手順を説明します。

## 前提条件を確認

次の前提条件がインストールされていることを確認します。

```bash
# Check Node.js version (should be 22.x.x)
node --version

# Check npm version (should be 9.0.0 or higher)
npm --version

# Check Git
git --version

# Check Bash
bash --version
```

## Adobe Developer Consoleにログインします

1. [Adobe Developer Console](https://developer.adobe.com/console){target="_blank"} に移動します。
1. 既にログインしている場合は、右上のプロファイルアイコンをクリックし、「**ログアウト**」ボタンをクリックします。
1. シートに指定したラボのメール ID とパスワードを使用してログインします。
1. 2 番目の電子メール アドレスまたは電話番号の追加を求めるメッセージが表示されたら、[**今すぐ追加しない**] をクリックします。
1. 組織プロファイルを選択するように求められたら、「**Adobe Commerce Labs**」を選択します。

   ![select-organization](./assets/select-org.png){width="600" zoomable="yes"}

1. 利用条件に同意するメッセージが表示されたら、リンクをクリックして利用条件を読み、「**同意して続行**」をクリックします。

   ![ 同意する条件 ](./assets/accept-terms.png){width="600" zoomable="yes"}

## セットアップスクリプトを実行します

[ 前提条件 ](#verify-prerequisites) がインストールされ、Adobe Developer Consoleにログインしている場合は、setup スクリプトをダウンロードして実行します。 または、[ ラボの前提条件 ](workbook-prerequisites.md) の手順に従って、スクリプトを手動で設定することもできます。

1. 設定スクリプトを含むリポジトリのクローンを作成します。

   ```bash
   git clone https://github.com/adobe-commerce/commerce-adl-2025.git
   ```

   >[!NOTE]
   >
   >スクリプトが失敗した場合は、[ 前提条件 ](workbook-prerequisites.md) を参照し、スクリプトでエラーが発生した場所で続行します。

1. リポジトリに移動します。

   ```bash
   cd commerce-adl-2025
   ```

1. 設定スクリプトを実行します。

   ```bash
   bash adl-setup.sh
   ```

   スクリプトの実行中は、ユーザー名とパスワードの入力を求めるプロンプトが表示されます。この入力は、ラボで行います。 ユーザー名には、場所とシート番号が反映されます。 例えば、サンノゼ（CA、シート 123）にいる場合、ユーザー名は `sjc-adl-123@adobeeventlab.com` になります。

   さらに、シート番号と **ステージ** ワークスペースに対応するプロジェクトを選択する必要があります。 プロジェクト名には、場所とシート番号が反映されます。 例えば、カリフォルニア州サンノゼの座席 123 にいる場合、プロジェクト名は `SJC ADL 123` になります。

## 拡張機能の開発

この節では、AI を利用した開発ツールを使用して、Adobe Commerce as a Cloud Serviceの評価拡張機能を開発するプロセスについて説明します。

### 拡張 AI ツールのインストール

`extension` フォルダー内に、AI を利用した開発ツールを設定します。

```bash
cd extension
```

```bash
aio commerce extensibility tools-setup
```

![AI ツールのインストール ](./assets/install-ai-tools.png){width="600" zoomable="yes"}

### カーソルを開く

>[!NOTE]
>
>AI 支援開発ツールを使用する場合、エージェントによって生成されるコードと応答には自然なバリエーションがあります。
>コードで問題が発生した場合は、いつでもエージェントにデバッグの支援を求めることができます。

[!DNL Cursor] アプリケーションを開き、`extension` フォルダーに移動します。または、[Cursor CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands) がインストールされている場合は、ターミナルで次のコマンドを入力します。

```bash
cursor .
```

![ カーソルを開く ](./assets/open-cursor.png){width="600" zoomable="yes"}

この時点で、すべてのルール [!DNL Cursor]`.cursor/rules` フォルダーにインストールされます。 MCP ツールは、**の** MCP 設定 [!DNL Cursor] にあります。 `commerce-extensibility` ツールセットがエラーなく有効になっていることを確認します。 エラーが表示された場合は、ツールセットのオン/オフを切り替えます。

![ カーソル設定 ](./assets/cursor-settings.png){width="600" zoomable="yes"}

カーソルのコンテキストにドキュメントを追加した場合は、無効にする必要があります。 [!UICONTROL **カーソル**]/[!UICONTROL **設定**]/[!UICONTROL **カーソル設定**]/[!UICONTROL **インデックスとドキュメント**] に移動し、一覧表示されているドキュメントを削除します。

![ ドキュメントを無効にする ](./assets/disable-documentation.png){width="600" zoomable="yes"}

### コードの生成

この節では、AI 支援ツールを使用して、製品評価拡張用のコードを生成する方法について説明します。

#### 要件の定義

製品の評価を API として提供する拡張機能を実装します。 [!DNL App Builder] 拡張機能は、特定の SKU の評価の詳細で応答します。

**最初のプロンプト：**

[!DNL Cursor] で次のプロンプトを使用します。

1. Cursor でチャットウィンドウを開きます。
1. **エージェント** モードを選択します。
1. 次のプロンプトを入力します。

   ```text
   Implement an Adobe Commerce as a Cloud Service extension to handle Product Ratings.
   Implement a REST API to handle GET ratings requests.
   GET requests will have to support the following query parameters:
   
   sku -> product SKU
   ```

1. エージェントがドキュメントの検索を要求した場合は、許可します。

![ カーソルにプロンプトを入力 ](./assets/enter-prompt.png){width="600" zoomable="yes"}

エージェントは要件を調査し、明確な質問をします。 エージェントが最適なコードを生成できるように、エージェントの質問に正確に答えます。

![ 代理人からの質問 ](./assets/agent-questions.png){width="600" zoomable="yes"}

**応答プロンプト：**

次の応答を使用して、エージェントの質問に答えます。

```text
Yes, this headless extension is for Adobe Commerce as a Cloud Service storefront,
but we do not need any authentication for the GET API because guest users should be able to use it on the storefront.
This extension will be called directly from the storefront,
no async invocation, such as events or webhooks, is required.
Let's start with just the GET API for now,
we will implement other CRUD operations at a later time.
We do not need a DB or storage mechanism right now,
just return random ratings data between 1 and 5 and a ratings count between 1 and 1000.
The API should only return the average rating for the product and the total number of ratings.
We do not need to add tests right now.
```

エージェントは、実装の信頼できるソースとして機能する `requirements.md` ファイルを作成します。

![ 要件ファイルが作成されました ](./assets/requirements-file.png){width="600" zoomable="yes"}

#### 要件の検証とプランアーキテクチャ

1. `requirements.md` ファイルを確認します。
1. すべてが正しいと思われる場合は、エージェントに **フェーズ 2 - アーキテクチャ計画** に移行するよう指示します。
1. アーキテクチャ計画を確認します。
1. コードの生成を続行するようにエージェントに指示します。

![ アーキテクチャの計画 ](./assets/architecture-planning.png){width="600" zoomable="yes"}

#### コードを生成

エージェントは、必要なコードを生成し、次の手順で詳細な概要を提供します。

![ コード生成の概要 ](./assets/code-generation-summary.png){width="600" zoomable="yes"}

![ 次の手順 ](./assets/next-steps.png){width="600" zoomable="yes"}

### ローカルテスト

コードをローカルでテストできるようにエージェントに依頼します。

```text
Test the ratings API locally on a dev server using cURL.
```

エージェントの指示に従い、API がローカルで動作していることを確認します。

![ ローカルテスト ](./assets/local-testing.png){width="600" zoomable="yes"}

![ ローカルテストの結果 ](./assets/local-testing-1.png){width="600" zoomable="yes"}

### 拡張機能のデプロイ

生成されたコードを検証すると、次のプロンプトを使用して拡張機能をデプロイできます。

```text
Deploy the ratings API.
```

#### 導入前評価

エージェントは、デプロイ前に、デプロイメント前の準備状況の評価を実行します。

![ 導入前評価 ](./assets/pre-deployment-assessment.png){width="600" zoomable="yes"}

#### デプロイ

評価結果に自信がある場合は、エージェントにデプロイメントを続行するように指示します。 エージェントは、MCP ツールキットを使用して、検証、ビルド、およびデプロイを自動的に行います。

![ デプロイメント ](./assets/deployment-process.png){width="600" zoomable="yes"}

### API のテスト

API は、ストアフロントに統合する前にテストできます。

エージェントは、新しいアクションの場所とテスト戦略を提供します。

![ テスト方法 ](./assets/testing-strategy.png){width="600" zoomable="yes"}

#### cURL を使用した手動のテスト

ターミナルで cURL を使用して、手動で API をテストします。

```bash
curl -s "https://<your-site>.adobeioruntime.net/api/v1/web/ratings/ratings?sku=TEST-SKU-123"
```

![cURL テスト ](./assets/curl-test.png){width="600" zoomable="yes"}

### Edge Delivery Servicesとの統合

Ratings API を [!DNL Adobe Commerce] を利用した [!DNL Edge Delivery Services] ストアフロントに統合するには、エージェントに依頼して、ratings API の要件を含むサービス契約を作成してください。

```text
Create a service contract for the ratings api that I can pass on to the storefront agent. Name it RATINGS_API_CONTRACT.md
```

![ サービス契約 ](./assets/create-contract.png){width="600" zoomable="yes"}

![ サービス契約の詳細 ](./assets/contract.png){width="600" zoomable="yes"}

ターミナルに戻り、`extension` フォルダーで次のコマンドを実行してファイルを `storefront` フォルダーにコピーします。

```bash
cp RATINGS_API_CONTRACT.md ../storefront
```

## ストアフロントに接続

この節では、実際のストアフロント機能を実装する際に役立ちます。また、[!DNL Adobe Commerce] ドロピンや [!DNL Edge Delivery Services] を使用する際に、AI エージェントと効果的に通信する方法を示します。

>[!NOTE]
>
>表示されるプロンプトは出発点であり、エージェントとの自然な会話を自由に感じるはずです。 AI 支援開発ツールを使用する場合、エージェントによって生成されるコードと応答には自然なバリエーションがあります。
>
>コードで問題が発生した場合は、いつでもエージェントにデバッグを依頼できます。

### 評価を評価およびレビュー数を実装

1. `storefront` フォルダーに移動します。

   ```bash
   cd storefront
   ```

1. 新しいカーソルウィンドウでストアフロントフォルダーを開きます。 [Cursor CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands) がインストールされている場合は、ターミナルに次のコマンドを入力します。

   ```bash
   cursor .
   ```

1. ローカル開発サーバーを起動します。

   ```bash
   npm run start
   ```

1. ブラウザーでアパレルページに移動します。

   ```text
   http://localhost:3000/apparel
   ```

1. ボイラープレートのストアフロント UI のレイアウトを確認します。

1. エージェントで次のプロンプトを使用します。

   ```text
   Implement product ratings to the storefront.
   Add a 5-star rating display with a review count underneath each product name on the product list page, product details page, and product recommendations.
   Use the dropin slot system where available.
   
   Use the @RATINGS_API_CONTRACT.md to understand how to use the ratings api.
   ```

   >[!NOTE]
   >
   >ローカル開発・サーバの起動を求めるメッセージが表示された場合は、すでに実行中であることをエージェントに通知します。

1. コードベースの変更を確認し、アパレルページで更新を確認します。

**期待される結果：**

* 「コンポーネント」という製品評価が自動的に作成されます。
* コンポーネントは、スロットを使用して product-details、product-list-page および product-recommendations ブロックに統合されます。
* 星は、モック評価値に基づいた適切な塗りの比率で表示されます。

![ 製品レーティングの実装 ](./assets/product-ratings-implementation.png){width="600" zoomable="yes"}

### 星の色を変更する

エージェントに対して次のプロンプトを使用します。

```text
Change the star fill color to red.
```

**期待される結果：**

星が赤に変わる。

![ 赤い星の色 ](./assets/red-star-colors.png){width="600" zoomable="yes"}

## ストアフロントのまとめ

このチュートリアルでは、以下のトピックを扱います。

* **機能の実装**:AI エージェントに新しい機能を記述する方法。
* **反復的な変更**：既存のコードをすばやく変更します。
* **複雑な UI コンポーネント**：視覚的参照を使用してインタラクティブ機能を構築する。
* **ドロピン統合**：ドロピンのコンテナとスロット [!DNL Adobe Commerce] 操作します。
* **コンポーネントの再利用性**：複数のブロックで使用される共有コンポーネントを作成します。

## 次の手順

時間に余裕がある場合は、次の機能を追加して、評価拡張機能をさらにカスタマイズできます。

### 評価配分モーダルの追加（オプション）

次の手順は、視覚的な参照を含む複雑な UI 機能をエージェントがどのように処理するかを示しています。

1. **開始する前に：** 次のモック画像を保存し、ストアフロントエージェントとのチャットに貼り付けます。

   ![ 格付分布モックアップ ](./assets/rating-distribution-mockup.png){width="600" zoomable="yes"}

1. 次の手順に従って、参照画像に基づいて定格分布モーダルを作成します。

   * API を更新して、評価配分を表す追加データを返すようにします。
   * API コントラクトを更新します。
   * ストアフロント コードベースの連絡先を更新します。
   * ストアフロントエージェントに、参照画像と更新された API コントラクトを使用して、PDP ページに評価分布を追加するように依頼します。

1. コードベースに次の変更が加えられたことを確認し、アパレルページで最新情報を確認します。

   * エージェントによる視覚的モックアップの解釈方法
   * アクセシビリティのために適切なHTML構造を使用しているかどうか
   * 配置およびインタラクションの状態の処理方法

**トラブルシューティング：**

* モーダルが表示されない場合は、ブラウザーコンソールでエラーを確認します。
* ポジショニングがオフの場合は、エージェントに次の操作を依頼できます。

  ```text
  adjust the modal position to be...
  ```

![ 格付けモーダル ](./assets/rating-distribution-modal.png){width="600" zoomable="yes"}
