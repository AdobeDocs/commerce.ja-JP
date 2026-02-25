---
title: 評価拡張機能のチュートリアル
description: App Builderと AI 支援開発ツールを使用して、Adobe Commerce as a Cloud Serviceの製品評価拡張機能を作成する方法について説明します。
feature: App Builder, Cloud
role: Developer
level: Intermediate
source-git-commit: fb3595284761e9478c819150c27d06631de67e18
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# 評価拡張機能のチュートリアル

このチュートリアルでは、[!DNL Adobe Commerce as a Cloud Service] および AI を利用した開発ツールを使用して、[!DNL Adobe App Builder] 用の製品評価拡張機能を構築する手順を説明します。

開始する前に、[&#x200B; 前提条件 &#x200B;](./tutorial-prerequisites.md) を完了してください。

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

## 拡張機能の開発

この節では、AI を利用した開発ツールを使用して、Adobe Commerce as a Cloud Serviceの評価拡張機能を開発する手順について説明します。

1. **[!UICONTROL Cursor]**/**[!UICONTROL Settings]**/**[!UICONTROL Cursor Settings]**/**[!UICONTROL Tools & MCP]** に移動し、`commerce-extensibility` ツールセットがエラーなく有効になっていることを確認します。 エラーが表示された場合は、ツールセットのオン/オフを切り替えます。

   ![MCP コマース拡張ツールセットが有効になっていることを示すカーソル IDE 設定 &#x200B;](../assets/cursor-settings.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   >AI 支援による開発ツールを使用する場合、エージェントによって生成されるコードと応答に自然なバリエーションが生じることを期待してください。
   >コードで問題が発生した場合は、いつでもエージェントにデバッグの支援を求めることができます。

1. カーソルのコンテキストにドキュメントを追加した場合は、そのドキュメントを無効にします。

   - [!UICONTROL **カーソル**]/[!UICONTROL **設定**]/[!UICONTROL **カーソル設定**]/[!UICONTROL **インデックスとドキュメント**] に移動し、一覧表示されているドキュメントを削除します。

   ![&#x200B; ドキュメントリストが空のカーソルインデックス作成とドキュメント設定 &#x200B;](../assets/disable-documentation.png){width="600" zoomable="yes"}

1. 製品評価拡張機能のコードを生成します：
   - Cursor chat ウィンドウで、[!UICONTROL **Agent**] モードを選択します。
   - 次のプロンプトを入力します。

   ```shell-session
   Implement an Adobe Commerce as a Cloud Service extension to handle Product Ratings.
   
   Implement a REST API to handle GET ratings requests.
   
   GET requests will have to support the following query parameters:
   
   sku -> product SKU
   ```

   >[!NOTE]
   >
   >エージェントがドキュメントの検索を要求した場合は、許可します。

1. エージェントが最適なコードを生成できるように、エージェントの質問に正確に答えます。

   ![&#x200B; 拡張機能プロンプトが入力されたエージェントモードのカーソルチャットウィンドウ &#x200B;](../assets/enter-prompt.png){width="600" zoomable="yes"}

   ![&#x200B; 拡張要件を明確にする質問をする AI エージェント &#x200B;](../assets/agent-questions.png){width="600" zoomable="yes"}

1. 次のテキスト例を使用して、エージェントの質問に回答し、ランダム化された評価データを設定します。

   ```shell-session
   Yes, this headless extension is for Adobe Commerce as a Cloud Service storefront,
   but we do not need any authentication for the GET API because guest users should be able to use it on the storefront.
   
   This extension is called directly from the storefront, no async invocation, such as events or webhooks, is required.
   
   Start with just the GET API for now, we will implement other CRUD operations at a later time.
   
   We do not need a DB or storage mechanism right now, just return random ratings data between 1 and 5 and a ratings count between 1 and 1000.
   
   The API should only return the average rating for the product and the total number of ratings.
   We do not need to add tests right now.
   ```

   エージェントは、実装の信頼できるソースとして機能する `requirements.md` ファイルを作成します。

   ![AI エージェントによって作成された Requirements.md ファイルと実装の詳細 &#x200B;](../assets/requirements-file.png){width="600" zoomable="yes"}

1. `requirements.md` ファイルを確認し、計画を検証します。

   すべてが正しいと思われる場合は、エージェントに **フェーズ 2 - アーキテクチャ計画** に移行するよう指示します。
1. アーキテクチャ計画を確認します。
1. コードの生成を続行するようにエージェントに指示します。

   エージェントは、必要なコードを生成し、次の手順で詳細な概要を提供します。

   ![AI エージェントフェーズ 2 Architecture Plan for Ratings API](../assets/architecture-planning.png){width="600" zoomable="yes"}

   ![&#x200B; 生成されるコードファイルと構造の概要 &#x200B;](../assets/code-generation-summary.png){width="600" zoomable="yes"}

   ![&#x200B; テストとデプロイメントの次のステップを提供する AI エージェント &#x200B;](../assets/next-steps.png){width="600" zoomable="yes"}

### ローカルテスト

1. コードをローカルでテストできるようにエージェントに依頼します。

   ```shell-session
   Test the ratings API locally on a dev server using cURL.
   ```

1. エージェントの指示に従い、API がローカルで動作していることを確認します。

   ![&#x200B; ローカル API テスト用の AI エージェントの手順 &#x200B;](../assets/local-testing.png){width="600" zoomable="yes"}

   ![cURL でローカル API テストの結果が成功したことを示すターミナル &#x200B;](../assets/local-testing-1.png){width="600" zoomable="yes"}

### 拡張機能のデプロイ

1. 生成されたコードを検証した後、次のプロンプトを使用して拡張機能をデプロイします。

   ```shell-session
   Deploy the ratings API.
   ```

   エージェントは、デプロイ前に、デプロイメント前の準備状況の評価を実行します。

   ![AI エージェントのデプロイメント前準備状況評価チェックリスト &#x200B;](../assets/pre-deployment-assessment.png){width="600" zoomable="yes"}

1. 評価結果に自信がある場合は、エージェントにデプロイメントを続行するように指示します。

   エージェントは、MCP ツールキットを使用して、検証、ビルド、およびデプロイを自動的に行います。

   ![MCP ツールキット検証ビルドおよびデプロイメントプロセス &#x200B;](../assets/deployment-process.png){width="600" zoomable="yes"}

### デプロイメント後

API は、ストアフロントに統合する前にテストできます。 担当者は、新しいアクションの場所とテスト戦略を指定する必要があります。

![&#x200B; デプロイ済みのアクション URL とテストコマンドを使用した AI エージェントテスト戦略 &#x200B;](../assets/testing-strategy.png){width="600" zoomable="yes"}

また、ターミナルで cURL を使用して、手動で API をテストすることもできます。

```bash
curl -s "https://<your-site>.adobeioruntime.net/api/v1/web/ratings/ratings?sku=TEST-SKU-123"
```

![&#x200B; デプロイ済みの評価 API の cURL テストが成功したことを示すターミナル &#x200B;](../assets/curl-test.png){width="600" zoomable="yes"}

### Edge Delivery Servicesとの統合

Ratings API を [!DNL Adobe Commerce] を利用した [!DNL Edge Delivery Services] ストアフロントに統合するには、エージェントに依頼して、ratings API の要件を含むサービス契約を作成してください。

```shell-session
Create a service contract for the ratings api that I can pass on to the storefront agent. Name it RATINGS_API_CONTRACT.md
```

![AI エージェントがストアフロント統合用のサービス契約ファイルを作成 &#x200B;](../assets/create-contract.png){width="600" zoomable="yes"}

![&#x200B; エンドポイントと応答の詳細を含む評価 API 契約マークダウンファイル &#x200B;](../assets/contract.png){width="600" zoomable="yes"}
<!-- 
Return to the terminal and run the following command in the `extension` folder to copy the file to the `storefront` folder:

```bash
cp RATINGS_API_CONTRACT.md ../storefront
``` -->

### 次の手順

これで、評価 API を契約したので、評価拡張機能のストアフロント（フロントエンド）部分の作成を開始できます。

<!-- 
## Connect to the storefront

This section teaches you how to implement real storefront features and communicate effectively with AI agents when working with [!DNL Adobe Commerce] dropins and [!DNL Edge Delivery Services].

>[!NOTE]
>
>The prompts provided are starting points. Although you can use them without modification, consider having a natural conversation with the agent.
>
>When working with AI-assisted development tools, there are always natural variations in the code and responses generated by the agent.
>
>If you encounter any issues with your code, ask the agent to help you debug it.

### Ratings stars and review count implementation

1. Navigate to the `storefront` folder:

   ```bash
   cd storefront
   ```

1. Open the storefront folder in a new Cursor window.

    Alternatively, if you have the [Cursor CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands) installed, open the window by using the following command in your terminal:

   ```bash
   cursor .
   ```

1. Start the local development server:

   ```bash
   npm run start
   ```

1. In a browser, navigate to the Apparel page:

   ```shell-session
   http://localhost:3000/apparel
   ```

1. Observe the boilerplate storefront UI layout and note the lack of visual product ratings.

1. Use the following prompt with your agent:

   ```shell-session
   Implement product ratings in the storefront.

   Add a 5-star rating display with a review count underneath each product name on the product list page, product details page, and product recommendations.

   Use the dropin slot system where available.

   Use @RATINGS_API_CONTRACT.md to understand how to use the ratings API.
   ```

1. Observe the changes in the codebase, and watch the Apparel page for updates.

   You should see the following changes in your development environment and browser:

   * A product rating "component" is automatically created.
   * The component is integrated into product-details, product-list-page, and product-recommendations blocks using [dropin slots](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/customize/slots).
   * Stars display with proper fill proportions based on mock rating values.

![Product Ratings Implementation](../assets/product-ratings-implementation.png){width="600" zoomable="yes"}

## Tutorial recap

Here is a summary of the topics covered in this tutorial:

* **Feature implementation**: How to describe new functionality to an AI agent.
* **Iterative changes**: Making quick modifications to existing code.
* **Complex UI components**: Building interactive features with visual references.
* **Dropin integration**: Working with [!DNL Adobe Commerce] dropin containers and slots.
* **Component reusability**: Creating shared components used across multiple blocks.

## Next steps

For further experimentation with this tutorial, use the following suggestions to further customize your ratings extension, or create your own modifications:

### Change the star colors

Use the following prompt to your agent:

```shell-session
Change the star fill color to red.
```

**Expected outcome:**

The stars are changed to red.

![Red Star Colors](../assets/red-star-colors.png){width="600" zoomable="yes"}

### Add rating distribution modal

The following steps show how the agent handles complex UI features with visual references.

1. **Before starting:** Save the following mock image and paste it into the chat with your storefront agent.

   ![Rating Distribution Mockup](../assets/rating-distribution-mockup.png){width="600" zoomable="yes"}

1. Follow these steps to create the ratings distribution modal using the reference image as a guide:

   * Update the API to return additional data representing the ratings distribution.
   * Update the API Contract.
   * Update the contact in the storefront codebase.
   * Ask the storefront agent to use the reference image and updated API Contract to add the ratings distribution to the PDP page.

1. Observe the following changes in the codebase, and watch the Apparel page for updates:

   * How the agent interprets the visual mockup
   * Whether it uses appropriate HTML structure for accessibility
   * How it handles the positioning and interaction states

#### Troubleshooting

* If the modal does not appear, check the browser console for errors.
* If positioning is off, ask the agent to fix it using the following format:

   ```shell-session
   adjust the modal position to be...
   ```

![Rating Distribution Modal](../assets/rating-distribution-modal.png){width="600" zoomable="yes"}
 -->
