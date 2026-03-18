---
title: 在庫内通知拡張機能のチュートリアル
description: App Builder、Edge Delivery Services、AI アシスト開発ツールを使用して、Adobe Commerce as a Cloud Serviceの在庫内通知拡張機能を作成する方法について説明します。
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: ce8882b8af21198a7bc57bc58124e8a2d1491a50
workflow-type: tm+mt
source-wordcount: '2599'
ht-degree: 0%

---

# 在庫内通知拡張機能のチュートリアル

このチュートリアルでは、[!DNL Adobe Commerce as a Cloud Service] および AI を利用した開発ツールを使用して、[!DNL Adobe App Builder] 用の在庫内通知拡張機能を構築する手順を説明します。 拡張機能を使用すると、買い物客は在庫切れの商品を購入し、商品が再入荷したときに通知を受け取ることができます。

次の 2 つのパーツを作成します。

- **App Builder拡張機能** - イベント駆動型かつスケジュールされた在庫切れ検出機能を使用して、在庫切れのサブスクリプション（作成、読み取り、削除）を管理するための REST API。
- **ストアフロント統合** – 選択した製品またはバリアントが在庫切れの場合にのみ表示される、製品詳細ページ（PDP）の購読フォーム。

>[!NOTE]
>
>AI エージェントは非決定的です。 このチュートリアルのプロンプト、質問および出力は、例です。 エージェントは、異なる質問、要件、またはアーキテクチャの提案を作成する場合があります。 このチュートリアルの例を使用して、エージェントを同様の結果に導きます。

開始する前に、[ 前提条件 ](./tutorial-prerequisites.md) を完了してください。 このチュートリアルでは、**統合スターターキット** を使用します。 クローンが既に作成されていて、前提条件ページに記載されている設定手順を完了していることを確認します。

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

上記のコマンドのいずれかで期待される結果が返されない場合は、[ 前提条件 ](./tutorial-prerequisites.md) を参照してガイダンスを確認してください。

さらに、次の点も確認してください。

- 製品データを含む [!DNL Adobe Commerce as a Cloud Service] インスタンスがあります。 [Commerce Cloud サービスインスタンス ](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview){target="_blank"} を参照してください。
- [!DNL Commerce] インスタンスに接続されたストアフロントプロジェクトがある。 ストアフロントがない場合は、[ ストアフロントの作成 ](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/){target="_blank"} の手順に従ってください。
- `aem` CLI がインストールされます。

  ```bash
  npm install -g @adobe/aem-cli
  ```

## 拡張機能の開発

この節では、AI を利用した開発ツールを使用して、[!DNL Adobe Commerce as a Cloud Service] 用の在庫内通知拡張機能を開発する手順を説明します。 この拡張機能は購読管理用の REST API を提供し、Commerce イベントと予定されたチェックを通じて、商品が再入荷するタイミングを検出します。

1. コーディングエージェントの MCP 設定に移動します。

   例えば、カーソルでは、**[!UICONTROL Cursor]**/**[!UICONTROL Settings]**/**[!UICONTROL Cursor Settings]**/**[!UICONTROL Tools & MCP]** に移動します。 `commerce-extensibility` ツールセットがエラーなく有効になっていることを確認します。 エラーが表示された場合は、ツールセットのオン/オフを切り替えます。

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
Implement an Adobe Commerce as a Cloud Service extension to handle out-of-stock notifications for products.

The service should provide REST API endpoints for basic create, read, update, and delete (CRUD) operations on out-of-stock notifications, allowing storefronts to manage notifications for specific product SKUs.

Back-in-stock is detected by an inventory or product event or a scheduled action that checks Commerce API and then calls the REST API to send the notification.

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>処理を進める前にエージェントに停止して質問することを伝えることで、プロセスの初期に実装を進めるのに役立ちます。 このプロセスにより、主要な前提と欠落している要件が早い段階で特定され、このチュートリアルのガイド付きワークフローを開始する際に必要になります。

### 手順 2：エージェントの質問に回答する

エージェントは、ソリューションの作成を開始する前に、必要な一連の質問を返します。 次の例は、一般的な質問と回答を示しています。 エージェントが異なる質問をする場合がありますが、トピックは一般的に同じです。

**エージェントの質問の例：**

1. **REST API - ホストおよびコンシューマー** - CRUD REST API は、ストアフロントが呼び出すこのApp Builder アプリの一部にする必要がありますか（例えば、Adobe I/O Runtimeでの web アクション）。 誰が（EDS ストアフロント、カスタム/ヘッドレスストアフロント、またはその両方）と呼びますか。 CORS、公開（未認証）アクセスが必要ですか。それとも、呼び出し元は API キー、OAuth、Commerce トークンを使用しますか。
1. **データモデル** - 1 つの「通知」は何を表すでしょうか？ 顧客識別子（電子メールのみ、または顧客 ID）? 商品識別子（SKU のみ、または SKU +店舗表示） 同じ顧客が同じ SKU に複数回購読できますか。購読を重複排除する必要がありますか？
1. **在庫切れ検出 – イベントとスケジュール済み** — イベント駆動型の検出（Commerceの在庫/商品イベントに対応）、スケジュール済みの検出（在庫を定期的にチェックするスケジュール済みアクション）、またはその両方を実行しますか？ 「通知の送信」とはどういう意味ですか（外部 Webhook を呼び出したり、メールを送信したり、ログに記録したりします）?
1. **在庫切れ – Commerce ソース** – お好みのイベント名はありますか？それとも、Commerceが提供する在庫/在庫更新イベントをデザインで使用する必要がありますか？ スケジュールされたチェックの場合、SKU 別に在庫ステータスを取得するには、どの API を使用する必要がありますか？
1. **永続性とマルチテナント機能** – 購読を保持す `aio-lib-state` のに適切な場所ですか。または、外部ストアがありますか。 デザインではマルチテナントとシングルテナントのどちらを想定するべきですか？
1. **CRUD の意味とライフサイクル** — 「削除」は購読のキャンセルを意味する必要がありますか？ 「更新」が必要ですか？ 在庫切れ通知が送信された後、購読を自動的に削除しますか、それとも通知済みとしてマークしますか？
1. **機能以外** - レート制限や最大サブスクリプションを適用できますか？ コンプライアンスのニーズ（ダブルオプトイン、同意フラグ）はありますか？

**回答の例：**

```shell-session
1. The CRUD REST API should be part of thie App Builder app. It will be called by the EDS Storefront. For this implementation there is no need for API keys or security tokens.
2. For this initial implementation the customer identifier will be the email, product is identified by SKU, customer emails should not be able to subscribe to the same SKU multiple times.
3. Implement both. For now instead of sending the notification, log it so I can audit in the Adobe Developer Console.
4. Research and use what the best event to use that commerce already provides. Research the simplest way to get the stock status by SKU.
5. Use the aio-lib-state. Single tenant for now
6. Delete means cancel subscription. Skip Update, it does not apply for this service. After subscription is sent, it should be marked as notified or removed so it won't send again until the user subscribes again.
7. No limits. Implement minimal compliance requirements.
```

>[!NOTE]
>
>あなたのエージェントは異なる質問をする可能性があります。 同じ機能上の結果に向けてエージェントを導くためのガイダンスとして、メールと SKU のサブスクリプションを備えた REST API、イベント駆動型およびスケジュールされた在庫切れ検出、`aio-lib-state` の永続性、ログベースの通知を使用します。

### 手順 3：要件とアーキテクチャのレビュー

エージェントは、確認する要件およびアーキテクチャ文書を生成します。 要件が提供した回答と一致し、アーキテクチャが次の内容をカバーしていることを確認します。

- 購読 CRUD （作成、読み取り、更新、削除）の REST API アクション
- Commerceの在庫イベントによってトリガーされる、イベント駆動型の Back-in-Stock ハンドラー
- フォールバックとしてのスケジュールされた在庫確認アクション
- `aio-lib-state` を使用した永続性

>[!NOTE]
>
>AI エージェントは非決定的で、その動作はモデルや IDE によって異なります。 異なる要件やアーキテクチャを生み出す異なる質問セットが得られる場合があります。 その場合は、続行する前に、このチュートリアルで示している内容に厳密に一致する実装を使用するように、エージェントを設定してください。

### 手順 4：実装計画の選択

エージェントでは、詳細な導入計画を作成するか、直接導入を完了するかを選択できます。

- より詳細な制御を行いながら段階的に実行できる表示可能なプランが必要な場合は、最初のオプションを選択します。
- エージェントが最小限の介入で完全な実装を行う場合は、2 番目のオプションを選択します。

### 手順 5：イベントのデプロイ、オンボーディング、登録

実装が完了したら、次の手順でアプリケーションをデプロイし、Commerce インスタンスをオンボーディングして、次のコマンドでイベントを登録します。

1. 拡張機能をデプロイします。

   ```bash
   aio app deploy
   ```

1. オンボーディングスクリプトを実行して、Commerceにイベントプロバイダーを登録します。

   ```bash
   npm run onboard
   ```

1. Commerce イベントへの登録：

   ```bash
   npm run commerce-event-subscribe
   ```

1. イベント購読を検証します。

   Commerce インスタンスに移動し、**[!UICONTROL System]**/**[!UICONTROL Event Subscriptions]** を開きます。

   イベントレコードのテーブルが表示されます。

   ![ イベント購読セクションがハイライト表示されたCommerce管理メニュー ](../assets/in-stock-event-subscriptions.png){width="600" zoomable="yes"}

   ![ 登録されたイベントエントリを含むイベント購読テーブル ](../assets/in-stock-event-table.png){width="600" zoomable="yes"}

### 手順 6：拡張機能をテストする

担当者にテスト手順の提供を依頼します。 これは API サービスなので、コマンドラインの手順をリクエストできます。

```shell-session
Give me step by step instructions to test the API service from the command line.
```

エージェントが指定する手順に従います。 次の例は、一般的なテストコマンドを示しています。

**SKU を購入：**

```bash
API_URL="https://<your-runtime-url>/api/v1/web/notify-out-of-stock/api"; curl -X POST "$API_URL" \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","sku":"ADB153"}'
```

応答は次のようになります。

```json
{
  "createdAt": "2026-03-06T22:11:00.308Z",
  "email": "test@example.com",
  "id": "b3353bf5-1007-4b10-989d-430892dd4a66",
  "sku": "ADB153"
}
```

**すべてのサブスクリプションをリストする：**

```bash
curl -X GET "$API_URL"
```

応答は、すべてのアクティブな購読のリストを返します。

```json
{
  "subscriptions": [
    {
      "createdAt": "2026-03-06T22:11:00.308Z",
      "email": "test@example.com",
      "id": "b3353bf5-1007-4b10-989d-430892dd4a66",
      "sku": "ADB153"
    }
  ]
}
```

**在庫残りフローのテスト：**

1. Commerce インスタンスから、サブスクリプションを作成した商品を編集します。
1. 製品の在庫ステータスを **[!UICONTROL Out of Stock]** に設定します。
1. 約 1 分待ってから、在庫ステータスを **[!UICONTROL In Stock]** に戻します。

   ![ 在庫あり/在庫切れのオプションがある在庫状況ドロップダウンを示すCommerce管理者の製品編集ページ ](../assets/in-stock-product-stock-status-toggle.png){width="600" zoomable="yes"}

1. イベントがトリガーしてサービスに送信されるまで、約 5 分待ちます。

1. [!DNL Adobe Developer Console] から、「App Builder ログ」セクションに移動します。

   ![Adobe Developer Console App Builderのログセクション ](../assets/in-stock-developer-console-logs.png){width="600" zoomable="yes"}

1. ログで、イベントが処理されたことを確認するエントリがあり、メールと SKU の正しいサブスクリプションペアが特定されたことを確認します。

   ![ 在庫切れイベントの処理を示すApp Builder ログエントリ ](../assets/in-stock-log-entries.png){width="600" zoomable="yes"}

>[!TIP]
>
>通知アクションが正常にログに記録されたことを確認するために、ログで何を探すかをエージェントに依頼できます。 ログエントリをコピー&amp;ペーストして、エージェントに検証を実行させることもできます。

在庫が復活したイベントが処理された後、通知された購読が削除されるので、購読のリストをリクエストすると、返されるエントリが 1 つ少なくなります。

### サービス契約の作成

サービスの実装が完了したら、エージェントに対して、ストアフロント作業用のサービス契約の作成を依頼します。

```shell-session
Create an API service contract for the Out of Stock notification service and its endpoints. Ensure that the service contract is clear and detailed enough for a frontend developer to implement the storefront UI integration without needing to ask additional questions about the API. Name this file OUT_OF_STOCK_NOTIFICATION_CONTRACT.md
```

このファイルをストアフロントプロジェクトにコピーして、ストアフロントエージェントが参照できるようにします。

## ストアフロントに接続

このセクションでは、[!DNL Edge Delivery Services] および AI アシスト開発ツールを使用して、在庫内通知拡張機能のストアフロント部分を実装する手順を説明します。 購読フォームを製品詳細ページ（PDP）に追加します。このページは、選択した製品またはバリアントが在庫切れの場合にのみ表示されます。

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
- Commerce ストアフロントの AI ツール [CLI を使用してインストール ](./tutorial-prerequisites.md#install-the-storefront-ai-tools)
- ストアフロントプロジェクトにコピーされた `OUT_OF_STOCK_NOTIFICATION_CONTRACT.md` ファイル

### 手順 1：環境を検証する

`config.json` ファイルを開き、`commerce-core-endpoint` と `commerce-endpoint` の値が [!DNL Adobe Commerce as a Cloud Service] GraphQL エンドポイントを指していることを確認します。

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### 手順 2：最初のプロンプトを指定する

サービス契約がプロジェクトに既に存在する場合は、製品の詳細ページで UI を作成するようにエージェントに促します。 エージェントで **プラン** モードが使用可能な場合は、そのモードを使用して、エージェントがプランなしで進行しないようにします。

```shell-session
Analyze @OUT_OF_STOCK_NOTIFICATION_CONTRACT.md. Add a form for subscribing to a notification for when a product is back in stock. Place this form on the product details page, underneath the add to cart and wishlist button. The form only displays when a product is out of stock. 

Use the project manager skill to plan this implementation.
```

>[!TIP]
>
>特に、プロジェクトマネージャーのスキルトリガーを使用するようリクエストすると、実装をプロセスの初期に導くのに役立つ段階的なワークフローが提供されます。 このプロセスにより、主要な前提条件と欠落している要件が早期に特定されます。また、元のプロンプトでは提供とは思わなかった詳細や要件をエージェントが提示できるようになります。

### 手順 3：計画に関する質問への回答

エージェントは、ソリューションの作成を開始する前に、回答する必要がある一連の質問を返します。 次の例は、一般的な質問と回答を示しています。 エージェントが異なる質問をする場合がありますが、トピックは一般的に同じです。

**エージェントの質問の例：**

1. **API ベース URL** - ストアフロントは在庫切れ通知の API ベース URL をどのように取得する必要がありますか？ オプションには、設定ブロック（`out-of-stock-api-base-url` を含むテーブルなど）、グローバルプレースホルダーや環境変数、またはその他のアプローチが含まれる場合があります。
1. **コピー** – 実装では、成功メッセージとエラーメッセージのプレースホルダー（ローカライゼーションなど）を使用するか、この実装に静的な英語を使用する必要がありますか？
1. **購読が成功した後** - フォームが「購読しています」とだけ表示されて非表示になる場合は（A）、フォームは表示されたまま、無効のままにして、その上に成功メッセージが表示される場合は（B）、別の動作が表示される場合は（C）。
1. **設定可能な製品** – 選択したバリアントの `inStock` 定値に基づいてフォームを表示する必要があります。選択したバリアントが在庫切れになったときにフォームが表示されるようにしますか？

**回答の例：**

```shell-session
1. Global placeholder with baseurl value of `https://<your-runtime-url>/api/v1/web/notify-out-of-stock/api`
2. Use placeholders with static English fallback
3. B
4. Use selected variant's inStock value
```

>[!NOTE]
>
>`<your-runtime-url>` をApp Builder デプロイメントの実際の [!DNL Adobe I/O Runtime] URL に置き換えます。
>
>あなたのエージェントは異なる質問をする可能性があります。 次の回答をガイダンスとして使用します。
>
>- コードを変更せずに変更できるように、API のベース URL にグローバルプレースホルダーを使用します。
>- フォールバックとして静的な英語を使用した、ユーザーに表示されるコピーのプレースホルダーを使用します。
>- 購読が成功したら、フォームを表示したまま無効にし、その上に成功メッセージを表示します。
>- 設定可能な製品の場合は、選択したバリアントの `inStock` 値を使用してフォームの表示をコントロールします。

### 手順 4：要件とアーキテクチャのレビュー

エージェントは、レビュー用に要件ドキュメントを更新します。 次のことを確認します。

- フォームは、製品または選択したバリアントが在庫切れの場合にのみ表示されます。
- フォームは、PDP の「買い物かごに追加」ボタンと「ウィッシュリスト」ボタンの下に配置されます。
- API 統合では、グローバルプレースホルダーのベース URL を使用します。
- 成功およびエラーの状態は、契約（201、409、400、503/500）に従って処理されます。

>[!NOTE]
>
>AI エージェントは非決定的で、その動作はモデルや IDE によって異なります。 異なる要件やアーキテクチャを生み出す異なる質問セットが得られる場合があります。 その場合は、続行する前に、このチュートリアルで示している内容に厳密に一致する実装を使用するように、エージェントを設定してください。

**フェーズ 2 （アーキテクチャ計画）** では、エージェントはアーキテクチャを提案する前にドキュメントとコードベースを調査します。 エージェントは次の操作を実行します。

- PDP ドロップイ [!DNL Commerce] コンテナ、スロット、イベントペイロードに関するドキュメントを検索します。
- `blocks` ディレクトリと `scripts/initializers/` フォルダーをスキャンして、既存の PDP 関連コードを探します。
- 使用可能なコンテナおよびスロットのコンテキスト形状の TypeScript 定義を調べます。

次に、エージェントはアーキテクチャオプションを提示します。 計画を確認し、担当者に続行を指示します。

### 手順 5：実装計画の選択

エージェントでは、詳細な導入計画を作成するか、直接導入を完了するかを選択できます。

- より詳細な制御を行いながら段階的に実行できる表示可能なプランが必要な場合は、最初のオプションを選択します。
- エージェントが最小限の介入で完全な実装を行う場合は、2 番目のオプションを選択します。

**フェーズ 4 （実装）** では、エージェントは選択したアーキテクチャに基づいてコードを生成します。 アプローチに応じて、エージェントはいくつかの特殊なスキルを使用します。

- **コンテンツモデリング：** 新しいブロックが必要な場合、エージェントは、作成者にとって使いやすいコンテンツ構造を設計します。
- **ブロック開発：** エージェントは、JavaScriptの装飾関数、スコープ指定された CSS スタイル、アクセシビリティ用の ARIA ラベル、読み込みとエラー状態の処理など、[!DNL Edge Delivery Services] の規則に従ってブロックファイルを作成します。
- **ドロップインカスタマイズ：** アーキテクチャでスロットのカスタマイズを使用する場合、エージェントは正しいコンテナを読み込み、製品タイトル近くの検証済みスロットを使用し、現在の SKU の製品データイベントをサブスクライブします。

生成されるコードを監視し、必要に応じて質問したり、エージェントをリダイレクトしたりできます。

### 手順 6：サーバーを起動してテストする

エージェントが実装を完了したら、開発サーバーを起動し、フォームをテストします。

1. ローカル開発サーバーを起動します。

   ```bash
   npm run start
   ```

1. ブラウザーで、在庫切れの製品ページに移動します。 例：

   ```shell-session
   http://localhost:3000/products/<out-of-stock-product-slug>/<sku>
   ```

1. 購読フォームが「買い物かごに追加」ボタンと「ウィッシュリスト」ボタンの下に表示されることを確認します。

手動でテストを実行することも、エージェントに対してブラウザー機能を使用してテストを実行するように依頼することもできます。

```shell-session
Run complete browser testing. Use the following out of stock product 'http://localhost:3000/products/<out-of-stock-product-slug>/<sku>'
```

![ 「買い物かごに追加」ボタンの下に在庫切れ通知フォームを示す製品詳細ページ ](../assets/in-stock-notification-form.png){width="600" zoomable="yes"}

### 手順 7：クリーンアップ

テストをスキップまたは完了すると、最終 **クリーンアップ** フェーズに進むようにエージェントから求められます。 確認時に、エージェントは実装時に作成されたすべてのドキュメントアーティファクトをアーカイブします。

## トラブルシューティング

チュートリアル中に問題が発生した場合は、次のヒントを参考にしてください。

- **API エラー：** CLI を使用して、動作を確認するためのリクエストを API に直接送信します。 例えば、`curl` を使用して、各エンドポイントを個別にテストします。
- **エージェントエラー：** 問題のデバッグに役立つように、エラーメッセージをコピーしてエージェントのチャットセッションに貼り付けます。 エージェントは、環境変数の欠落やアクションの設定の誤りなど、一般的な問題を診断できます。
- **イベントパイプライン：** 在庫切れイベントがトリガーされない場合は、オンボーディングとイベント購読の手順を完了していることを確認します。 `workspace.json` が正しい場所に存在し、Commerce イベント モジュールが有効になっていることを確認します。
- **ストックステータスペイロード：** Commerceは、`is_in_stock` をブール値（`"1"`）ではなく文字列（`true`）として送信する場合があります。 Back-in-stock ハンドラーがトリガーされない場合は、エージェントに問い合わせて、消費者コードの厳密なタイプ比較を確認し、両方の形式を処理するように更新します。

## チュートリアルの概要

このチュートリアルで扱うトピックの概要は次のとおりです。

- **拡張機能開発：** AI エージェントに新しい機能を記述し、[!DNL App Builder] を使用して CRUD 操作で動作する REST API を生成します。
- **イベント駆動型アーキテクチャ：** Commerce イベントと、商品が再入荷したときに検出するようにスケジュールされたアクションを設定します。
- **ローカルテストとデプロイメント：** API を `curl` でテストし、[!DNL Adobe I/O CLI] を使用してデプロイします。
- **サービス契約：** バックエンドの拡張機能とストアフロントの実装を橋渡しする API コントラクトを作成しています。
- **段階的なストアフロントの統合：** AI 支援のスキルを使用して、要件、アーキテクチャ、実装を進めます。
- **ドロップイン統合：** ドロップインコンテナとスロットを使用して、購読フォーム [!DNL Adobe Commerce]PDP に追加します。

## 次の手順

次の推奨事項を使用して、在庫内通知サービスを拡張します。

- **実際の通知を送信：** ログベースの通知を [!DNL Adobe Campaign] やサードパーティプロバイダーなどのメールサービスに置き換えます。
- **購読管理ページを追加：** 買い物客がアクティブな購読を表示およびキャンセルできるストアフロントページを作成します。
- **マルチテナントデプロイメントのサポート：** ステート管理を拡張して、1 つのApp Builder アプリで複数のCommerce テナントをサポートします。
- **レート制限を追加：** 購読 API にレート制限を実装して、不正使用を防ぎます。
